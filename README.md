# 🕹️ El arcade que quería ser consola

Tengo un mueble arcade de dos jugadores en casa, construido sobre una cómoda
KULLEN de IKEA. Lo monté para tener el sabor de los recreativos, y con el tiempo
se me ocurrió una idea que parecía sencilla: ¿y si esa misma máquina pudiera
jugar también a los juegos modernos que ya tengo en propiedad — los nuevos
Street Fighter, Killer Instinct, Injustice —, en una sola interfaz tipo consola,
sin cambiar de equipo y sin volverme loco con los mandos?

Este blog es la bitácora real de ese proyecto: un mini PC **CHUWI UBox** (Ryzen
5 6600H, Radeon 660M, 32 GB) convertido en consola arcade híbrida con
**Bazzite**. Contado mientras lo hago, con decisiones, problemas reales y
soluciones.

- [Sobre este proyecto](about.md)
- [Incidencias: problemas y soluciones](incidencias.md)

## El plan en una frase

Retro + juegos modernos, todo en una sola librería navegable con el mando:
EmuDeck para lo clásico, Heroic y Lutris para Epic/GOG/Rockstar, Proton para los
juegos de Windows, y **arcadenorm** para que las dos placas del mueble
funcionen como mandos de Xbox 360 en cualquier juego.

## Fases

- [x] **Fase 1 — La idea y la investigación** (2026-08-17): [El arcade que quería ser consola](_posts/2026-08-17-fase-1-investigacion-y-decisiones.md)
- [x] **Fase 2 — Instalación y desembarco** (2026-08-18): [La instalación y el desembarco](_posts/2026-08-18-fase-2-instalacion-y-desembarco.md)
- [x] **FAQ** (2026-08-18): [Preguntas que me hice por el camino](_posts/2026-08-18-faq-dudas-resueltas.md)
- [x] **Fase 3 — Mandos arcade (arcadenorm)** (2026-08-18): 2 placas independientes → 2 configs + 2 servicios → **2 gamepads Xbox 360 virtuales** ✅
- [ ] Fase 4 — Emulación retro (ROMs de RetroBat)
- [ ] Fase 5 — Launchers y juegos modernos (Heroic: DNF Duel, Gigabash, Sifu)
- [ ] Fase 6 — Unificación y pulido

## Hardware del proyecto

- **Mini PC**: CHUWI UBox (CWI604) — Ryzen 5 6600H, Radeon 660M, 32 GB DDR5 dual
- **Mueble arcade**: kit 2 jugadores con 2 encoders USB Zero Delay independientes
- **Almacenamiento**: un disco para el sistema, otro (NTFS) con las ROMs

---
*Escrito por una persona con ayuda de su agente de IA. Los errores son nuestros; los aciertos, del arcade.*
