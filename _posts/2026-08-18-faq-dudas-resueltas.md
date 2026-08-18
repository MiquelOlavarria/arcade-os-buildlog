---
title: "Preguntas que me hice por el camino (y respuestas que me hubiera gustado tener antes)"
date: 2026-08-18
tags: [faq, arcade, linux, dudas]
---

# Preguntas que me hice por el camino

Hay dudas que surgen en cuanto te lanzas a un proyecto así y que cuesta
responder solo. Estas son las que yo tuve, y cómo las resolví — por si alguien
las tiene antes de empezar.

## ¿Merece la pena "virtualizar" los mandos si el sistema ya detecta los físicos?

**Sí, y es el paso más importante.** Cuando conectas un encoder arcade barato,
el sistema lo ve como un mando genérico... pero un mando genérico *mentiroso*:
reporta rangos de ejes falsos, palancas que se desvían, y el mismo identificador
USB lo comparten decenas de placas con cableados distintos. Los juegos modernos
(especialmente los de lucha, que esperan mandos tipo Xbox) no lo tratan bien.

La alternativa sería configurar el mapeo juego a juego — el "infierno del mapeo
virtual" que yo mismo sufrí en Windows. En Linux lo resolvemos de raíz: el
proyecto **arcadenorm** mide lo que la placa hace de verdad, y publica un mando
**Xbox 360 virtual** a nivel de sistema. Ese mando es idéntico a un Xbox real
para *todo*: Steam, emuladores, juegos fuera de Steam, todo. Un mapeo, una vez,
para siempre.

## Si Steam también detecta los mandos físicos, ¿dan conflicto?

No. Steam ve los físicos como gamepads genéricos y los virtuales como Xbox 360.
Los juegos usan los virtuales; los físicos quedan "reservados" por el servicio
que los normaliza. Si molesta verlos duplicados en la lista de mandos de Steam,
se pueden ocultar desde la configuración, pero no es necesario.

## ¿Puede Linux escribir en discos NTFS?

**Sí.** Desde el kernel 5.15 existe el driver `ntfs3`, nativo, con lectura y
escritura completas. Un disco NTFS se monta sin problema y se escribe a toda
velocidad. Dicho esto, para juegos modernos vía Proton conviene un filesystem
nativo (permisos, prefijos de Wine, rendimiento): yo acabé convirtiendo el disco
de datos a **btrfs** (el de Bazzite), con copia verificada y sin perder nada.

## ¿Por qué no cifrar el disco al instalar?

Bazzite ofrece cifrado, pero un disco cifrado pide **teclado físico en cada
arranque**. Para un mueble arcade, que debe encender y entrar directo a la
interfaz de mando, eso rompe la experiencia. En una red doméstica privada
prefiero arranque directo sin teclado.

## ¿Por qué Bazzite y no Batocera?

Batocera es brillante para retro puro y consume poquísimo, pero el objetivo era
un híbrido: retro + juegos modernos de PC en una sola interfaz. Bazzite (el
sistema del Steam Deck, sobre Fedora) arranca directo a Steam Gaming Mode,
trae Proton, Lutris y Heroic, y la emulación se añade con EmuDeck/ES-DE. Con una
iGPU modesta como la mía (Radeon 660M), Batocera sería la elección si solo
quisiera retro; para lo que yo quería, Bazzite era la única que lo unificaba
todo. Más detalle en [la fase 1](2026-08-17-fase-1-investigacion-y-decisiones.html).

## ¿Qué pasa con los juegos de Microsoft Store / Game Pass?

No corren de forma nativa en Linux (la tienda de Microsoft es una aplicación de
Windows cerrada). Solo queda la vía cloud (xbox.com/play en el navegador). Es
una limitación real, pero con Steam, Epic, GOG y Rockstar cubiertos, el mueble
tiene de sobra.

## ¿Y los juegos con anti-cheat de kernel?

Los que exigen su módulo de kernel (tipo Vanguard) no funcionan en Linux, y no
hay vuelta de hoja. Para un arcade de salón, no es un problema práctico: los
juegos que tienen sentido ahí (lucha, plataformas, arcade) no lo usan.

## ¿Se puede montar todo esto sin teclado ni pantalla?

Sí, con un poco de ayuda: yo dejo que un agente (Bishop) acceda por **SSH con
clave pública** y haga toda la configuración por red. El mueble solo necesita
que se pulse el botón de encendido; el resto (instalación de juegos, ajustes,
actualizaciones) se hace en remoto, y el teclado queda para casos contados.
