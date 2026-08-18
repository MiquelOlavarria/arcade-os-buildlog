---
title: "Fase 2 — La instalación y el desembarco (o cómo montar un sistema sin morir en el intento)"
date: 2026-08-18
tags: [bazzite, instalación, arcade, ssh, problemas]
---

# Fase 2 — La instalación y el desembarco

Con la fase de investigación cerrada (Bazzite deck edition, arcadenorm para los
mandos, Heroic/Lutris para los juegos modernos), tocaba bajar a la realidad: **instalar
todo en el mini PC**. Esta fase fue un rosario de pequeños contratiempos, cada uno
con su solución. Los cuento todos porque son justo el material que no aparece en
las guías oficiales.

## La descarga de la ISO (o por qué un gestor de descargas a veces es necesario)

La ISO de Bazzite deck pesa 9,6 GB. Al descargarla con `curl` desde el CDN
(protegido por Cloudflare), el servidor cortaba la conexión a mitad de camino,
una y otra vez: primero con un error de HTTP/2, después con "faltan 5 GB". La
solución fue **aria2c con 8 conexiones en paralelo**, resume y reintentos
automáticos: 23 MB/s y sin un solo corte. Lección: para descargas grandes desde
CDNs quisquillosos, un descargador multi-conexión es más robusto que un simple
`curl -L`.

## El USB y Ventoy

Grabé la ISO en un USB con Ventoy y... no arrancaba. Probé con un SSD NVMe en
caja USB con Ventoy y ahí sí. Al final el proceso fue: menú de arranque del
mini PC → Ventoy → seleccionar la ISO → instalador.

## El instalador y el SSH de emergencia

El instalador de Fedora (Anaconda) da miedo cuando tienes dos discos: uno con
Windows (para borrar) y otro con todas las ROMs del arcade (para conservar).
Quería que mi agente verificara los discos antes de tocar nada, así que arranqué
el instalador con `inst.sshd` para entrar por SSH. El sshd del instalador no
arrancaba — faltaban las **claves de host** (`ssh-keygen -A` las genera y listo).

Al final la instalación se hizo a la antigua: seleccionar el disco de Windows,
borrarlo y a instalar. Sin cifrar (nada de teclados en cada arranque para una
consola).

## El desembarco: SSH, usuario y el proceso fantasma

Una vez instalado, el plan era dar acceso remoto a Bishop con su clave pública.
La odisea del usuario: el instalador crea `bazzite/bazzite` (el default) y
queríamos **`miquel` con contraseña propia**. Renombrar el usuario parecía
simple... hasta que `usermod` se negaba: *"user bazzite is currently used by
process 1669"*. El culpable era el `systemd --user` del propio usuario (un
proceso que vive mientras haya sesión). La solución limpia: `loginctl
terminate-user` (cierra las sesiones del usuario ordenadamente) lanzado en un
job desprendido, porque... sí, mataba mi propia conexión SSH al ejecutarse 😄

De paso descubrí que había dejado abierto el acceso **root por contraseña** como
puerta de emergencia; una vez recuperado el control, lo cerramos (solo clave
pública, sin root). Y al revisar la configuración de SSH me encontré con que los
drop-ins de Red Hat habían acabado en una carpeta `disabled/`: los devolvimos a
su sitio, uno de ellos estaba incompleto (le faltaba el `Include` de la política
criptográfica) y lo restauramos.

## El disco de datos: de NTFS a btrfs

El disco de las ROMs estaba en NTFS. Linux lo lee y escribe sin problema
(ntfs3), pero para juegos modernos vía Proton y para vivir en paz con los
permisos, lo pasamos a **btrfs** (el nativo de Bazzite). Proceso seguro: copia
completa con verificación de checksums a un temporal, formateo, copia de vuelta,
y actualizar el fstab. Aquí pasó la única tontería del día: el script cambió el
UUID del fstab pero dejó el tipo `ntfs3` → el arranque fallaba al montar. Un
`s/Ntfs3/btrfs/` a mano y a correr. Los datos: 25 GB, 36.384 archivos, todo
intacto.

## Los flatpaks y el nombre secreto de Heroic

Bazzite trae Flathub de sistema *filtrado*: no te deja instalar cualquier cosa
(protege la imagen). La solución: añadir el remoto Flathub **de usuario**. Y
después de varios "no encuentro la aplicación", descubrí que el ID real de
Heroic en Flathub es `com.heroicgameslauncher.hgl` — no el nombre bonito con
mayúsculas que aparece en la web. Detalles que te quitan una hora.

## arcadenorm: la odisea del instalador

arcadenorm es la pieza que convierte las placas del mueble en mandos Xbox 360.
Instalarlo en Bazzite (imagen inmutable) fue un curso acelerado:

1. `/usr/bin` es de solo lectura en Fedora Atomic → instalar con
   `PREFIX=$HOME/.local`
2. El servicio systemd fallaba con `status=203/EXEC`: **SELinux** no deja
   ejecutar un binario desde el home del usuario en un servicio del sistema →
   copia del wrapper a `/usr/local/bin`
3. La calibración es **interactiva y en portugués** (el proyecto es brasileño).
   Nada de i18n. Así que me preparé una chuleta traducida: "mueve la palanca
   arriba y mantenla", "pulsa el botón cuando diga AGORA"...
4. Con dos placas independientes (una por jugador), el flag `--jogadores 2`
   que aparece en la documentación es para **encoders duales** (una sola placa
   con mandos para dos). Para dos placas USB separadas, la calibración se
   ejecuta **una vez por placa**, eligiéndolas en el menú.
5. Las dos placas son gemelas (misma huella digital, mismo lote) → hay que
   identificarlas por el **puerto físico** (`/dev/input/by-path`): la del
   jugador 1 es `event3`, la del jugador 2 es `event15`.

## Dónde estamos

- ✅ Sistema Bazzite instalado, usuario `miquel`, SSH seguro por clave
- ✅ Disco de datos en btrfs, montado automáticamente
- ✅ Heroic, RetroArch, Lutris y arcadenorm instalados
- ✅ Jugador 1 calibrado como **Microsoft X-Box 360 pad** (¡el mueble ya es un
  mando de Xbox!)
- ⏳ Calibración del jugador 2 (pendiente)
- ⏳ Emulación retro con las ROMs de RetroBat
- ⏳ Juegos de Epic (DNF Duel, Gigabash, Sifu) importados en Heroic

La próxima entrega: los dos mandos funcionando, el frontend unificado y los
juegos modernos en el mueble. El feeling arcade está cada vez más cerca.
