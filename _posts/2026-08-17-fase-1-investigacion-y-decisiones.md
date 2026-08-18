---
title: "El arcade que quería ser consola: cómo nació la idea"
date: 2026-08-17
tags: [arcade, bazzite, motivación, proyecto]
---

# El arcade que quería ser consola

## La idea

Hace tiempo me monté un mueble arcade. De esos que quedan bien en el salón: dos
joysticks, botones de colores, luces LED... Lo monté con la idea de tener el
sabor de los recreativos en casa, de esos que te dejaban sin calderilla los
domingos por la tarde. El mueble en sí lo construí a partir de una cómoda
**KULLEN de IKEA** (la de cinco cajones: dos estrechos arriba y tres grandes
abajo), a la que le monté el panel con los joysticks y los botones. Algún día
publicaré los planos, las fotos del proceso y cómo quedó — pero ojo, ese no es
el objeto de este blog. Aquí el protagonista es el *motor*: lo que hace
funcionar la máquina. El mueble ya está; lo que quiero renovar es lo que hay
dentro. Y durante un tiempo fue exactamente eso: una máquina de juegos retro
donde echar una partida a los clásicos cuando venía alguien a casa.

Pero con el tiempo empezó a faltarme algo. El mueble era genial para lo retro,
pero nada más. Los juegos modernos, los que de verdad jugaba a menudo, se
quedaban en mi otro equipo, con su escritorio, su ratón y su teclado. Y cada vez
que quería jugar a algo me encontraba con la misma disyuntiva: ¿juego al arcade
o juego "en condiciones"?

¿Por qué no las dos cosas? ¿Por qué no tener **una sola caja** que lo hiciera
todo: el clásico de los ochenta y el juego de PC que compré el año pasado, en la
misma pantalla, con el mismo mando, sin cambiarme de equipo?

## El feeling arcade

Y aquí va la motivación de fondo, la que de verdad mueve el proyecto. Hay juegos
actuales que solo existen en las plataformas de hoy: los nuevos *Street
Fighter*, *Killer Instinct*, *Injustice*, plataformas modernos que no tienen
versión retro. Esos juegos están pensados para jugarse sentado en un sofá con un
mando de consola. Pero la experiencia cambia por completo cuando los juegas con
un joystick y botones, de pie, delante de una pantalla: vuelves a estar en el
salón recreativo, con los dedos sudando y la semanada en el bolsillo. Eso es lo
que quiero recuperar con los juegos de hoy. No se trata solo de conservar el
pasado, sino de traer el espíritu del recreativo al presente.

Esa era la idea. Y como todas las ideas que parecen sencillas, tenía su miga.

## El problema de siempre: los mandos

Mi mueble usa dos encoders USB baratos (de los "Zero Delay", los típicos de los
kits de Amazon) que convierten los botones y el joystick en un mando genérico.
En Windows, eso es un infierno: el sistema ve el mando, los juegos ven el mando,
pero los botones no hacen lo que tienen que hacer. El único modo de que
funcionara decentemente era usando el mapeo virtual de Steam y peleándome con
configuraciones por juego. Cada vez que conectaba el mueble a un equipo nuevo,
otra vez a empezar.

Lo que yo quería era simple: que el joystick y los botones **fueran un mando de
Xbox** para cualquier juego, siempre, sin configuraciones raras. Por eso, cuando
empecé a plantearme el sistema, la compatibilidad de mandos era el requisito
número uno.

## La idea toma forma

Tenía además una restricción física: el mini PC que iba a usar para esto es
modesto. Un CHUWI UBox con un Ryzen 5 6600H y su gráfica integrada, la Radeon
660M. Suficiente para lo retro y para juegos ligeros o medianos, pero con un
límite claro: los juegos gordos de última generación no van a correr ahí. Y eso
está bien — no es lo que le pido.

Así que los requisitos del proyecto quedaron así:

- Una **única interfaz** tipo consola: enciendes y juegas, sin escritorio.
- Los mandos del mueble funcionando como mando Xbox en **cualquier** juego.
- Juegos retro y emulación, con sus carátulas, bien presentados.
- Mis juegos modernos (los que ya tengo en propiedad: Steam, Epic, GOG,
  Rockstar) también ahí, en la misma interfaz.
- Poder añadir juegos nuevos sin volverme loco.
- Máximo rendimiento con lo que tengo.

## La investigación

Aquí es donde entró mi agente de IA, Bishop. Le planteé el proyecto y nos
pusimos a investigar: ¿qué sistema operativo? ¿Batocera, el clásico de los
muebles arcade? ¿Bazzite, el Linux basado en Fedora que usa el Steam Deck?
¿ChimeraOS?

Lo primero que descubrimos es que la pregunta correcta no era "cuál es el
mejor", sino "cuál encaja con lo que quiero". Batocera es una maravilla si tu
vida es la emulación: arranca en segundos, es ligerísimo y está hecho para
muebles arcade. Pero los juegos modernos de PC son su punto débil. Bazzite, en
cambio, está construido alrededor de Steam, arranca directamente en la interfaz
de consola (el Steam Gaming Mode, el mismo sistema del Steam Deck) y encima
trae integración con Lutris, EmuDeck y compañía.

Con mi hardware (una iGPU moderna pero modesta y 32 GB de RAM), la decisión fue
clara: **Bazzite**. La 660M da de sobra para el Gaming Mode, y el catálogo
moderno iba a quedar mucho mejor integrado. Batocera se queda como plan B si
algún día quisiera un equipo 100% retro.

Y luego estaba el miedo de siempre: ¿y los mandos? Aquí Linux me dio la
sorpresa buena. Resulta que en Linux los encoders genéricos se detectan solos, y
existe una herramienta llamada **arcadenorm** que hace exactamente lo que yo
llevaba años deseando en Windows: mide cómo responde tu placa de verdad y
publica un mando virtual de Xbox 360 que todos los juegos reconocen. Sin
configuraciones por juego. Sin infierno.

## El plan

La hoja de ruta quedó así:

1. **Instalar Bazzite** en el UBox (y documentar todo el proceso).
2. **Los mandos**: arcadenorm, calibración de las dos placas.
3. **Lo retro**: EmuDeck, con sus emuladores y carátulas.
4. **Lo moderno**: Heroic para Epic/GOG, Lutris para Rockstar y compañía, y
   juegos de Windows copiados ejecutándose con Proton.
5. **Unificarlo todo**: Steam ROM Manager para que toda la colección viva en una
   sola librería navegable con el mando.

Con sus límites, claro, y me parece honesto decirlo desde el principio: los AAA
pesados no van a correr en esta máquina, los juegos con anti-cheat a nivel de
kernel (como Valorant) no tienen versión para Linux, y el catálogo de Xbox/Game
Pass de la Microsoft Store tampoco funciona aquí — solo su versión en la nube.
Pero para lo que le pido al mueble, el plan es más que suficiente.

## Por qué escribo esto

Porque este tipo de proyectos casi siempre se cuentan al final, cuando todo
funciona, y se pierde toda la parte interesante: las dudas, los callejones sin
salida, las decisiones que se tomaron y por qué. Este blog es la bitácora real
del proyecto, con sus problemas y sus soluciones, escrita mientras pasa. Si a
alguien le sirve para montar el suyo, habrá valido la pena.

**Siguiente capítulo**: la instalación, con sus aventuras (spoiler: Cloudflare
nos cortó la descarga dos veces y el instalador no quería abrir SSH — lo
contamos todo en el [registro de incidencias](../incidencias.md)).
