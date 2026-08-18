# 🕹️ Arcade OS — Build Log

Bitácora pública del proyecto para convertir un mini PC **CHUWI UBox** en un
**arcade híbrido**: juegos retro clásicos + juegos modernos de PC, en una sola
interfaz tipo consola.

Este repositorio documenta cada fase: decisiones, pasos exactos, problemas
reales encontrados y cómo los resolvimos. Escrito por humanos y agentes de IA
(con un agente haciendo el trabajo pesado y un humano supervisando 😉).

## Hardware

| Componente | Detalle |
|---|---|
| Mini PC | CHUWI UBox (CWI604) — Ryzen 5 6600H, Radeon 660M, 32 GB DDR5 dual |
| Mueble arcade | Kit EG STARTS 2P — 2 encoders USB Zero Delay independientes |
| Almacenamiento | Disco 1: sistema · Disco 2: ROMs/emulación (NTFS) |

## Decisiones clave

- **SO**: [Bazzite deck edition](https://bazzite.gg/) (Fedora Atomic) → arranca a Steam Gaming Mode
- **Mandos**: [arcadenorm](https://github.com/evandeilton/arcadenorm) → encoders Zero Delay como 2 gamepads Xbox 360 virtuales
- **Retro**: EmuDeck (EmulationStation + RetroArch)
- **Launchers**: Heroic (Epic/GOG/Amazon) + Lutris (Rockstar/EA/Ubisoft)
- **Unificación**: Steam ROM Manager → todo en una librería con carátulas

## Fases

- [x] **Fase 1 — Investigación y decisiones** (2026-08-17): [ver artículo](_posts/2026-08-17-fase-1-investigacion-y-decisiones.md)
- [ ] Fase 2 — Instalación del sistema (en curso)
- [ ] Fase 3 — Mandos arcade (arcadenorm)
- [ ] Fase 4 — Emulación retro (EmuDeck)
- [ ] Fase 5 — Launchers y juegos modernos
- [ ] Fase 6 — Unificación y pulido

## Incidencias

[Registro de problemas y soluciones](incidencias.md) — el apartado más útil de este repo.

---
*Documentado por [Miquel](https://github.com/MiquelOlavarria) + Bishop (agente Hermes) · [Licencia CC BY-SA 4.0](LICENSE)*
