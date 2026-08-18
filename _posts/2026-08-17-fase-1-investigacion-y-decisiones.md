---
title: "Fase 1 — Investigación y decisiones (SO, mandos, launchers)"
date: 2026-08-17
tags: [bazzite, batocera, arcade, investigación]
---

# Fase 1 — Investigación y decisiones

**Objetivo**: unificar el arcade (mini PC CHUWI UBox) con UNA sola interfaz para
juegos arcade/retro + juegos modernos de PC (Steam, Epic, GOG, Rockstar) que ya
tenemos en propiedad. Requisitos: mandos arcade funcionando como mando Xbox en
cualquier juego, máximo rendimiento con recursos limitados, y poder añadir
juegos nuevos fácilmente.

## 1. Decisión del sistema operativo

Comparamos **Batocera**, **Bazzite**, **ChimeraOS** y SteamOS (descartado: solo
hardware Valve) con fuentes oficiales + investigación RAG cruzada.

| Criterio | Batocera 43 | Bazzite deck | ChimeraOS |
|---|---|---|---|
| Arranque a interfaz mando | Muy rápido (ES) | Rápido (Gaming Mode) | Rápido |
| Juegos modernos | Limitado (foco retro) | **Excelente** (Steam+Lutris, Heroic, Proton-GE) | Muy bueno (sin Lutris nativo) |
| Mandos genéricos | Plug&Play (tweaks) | Excelente con arcadenorm | Excelente con arcadenorm |
| Recursos (iGPU) | Muy bajos | Requiere iGPU moderna | Requiere iGPU moderna |
| Mantenimiento | Imagen | Atómico + rollback | Auto |

**Veredicto**: con nuestro hardware (Ryzen 5 6600H + Radeon 660M + 32 GB dual)
→ **Bazzite deck edition**. La 660M es iGPU RDNA2 moderna: soporta el Gaming
Mode (Gamescope) y corre retro perfecto + juegos ligeros/medios. Batocera queda
como plan B si algún día quisiéramos un foco 100% retro.

## 2. Mandos arcade: el problema que en Windows era un infierno

El kit trae 2 encoders USB **Zero Delay** (DragonRise 0079), uno por jugador.
En Windows solo funcionaban vía mapeo virtual de Steam. En Linux:

- El kernel los detecta como gamepad genérico (usbhid → evdev) — plug & play
- Para que TODO los vea como Xbox: **arcadenorm** — calibra el encoder *midiendo*
  lo que hace (ejes espejados, palancas a 90°, rangos mentirosos) y publica un
  **gamepad virtual Xbox 360** (GUID `030000005e04...`) que Steam, RetroArch,
  MAME y Proton reconocen nativamente
- Dos placas independientes = dos dispositivos con el MISMO VID:PID → arcadenorm
  los distingue por puerto/huella de hardware

## 3. Launchers y juegos modernos

- **Epic / GOG / Amazon** → Heroic (Legendary + gogdl + Nile), importa juegos ya instalados
- **Rockstar / EA / Ubisoft** → instaladores automáticos de Lutris
- **Juegos Windows copiados** → "juego local" apuntando al .exe (prefijo aislado) o non-Steam en Steam con Proton
- **Unificación** → Steam ROM Manager (carátulas automáticas) en Steam Gaming Mode
- **Limitaciones reales**: AAA pesados (iGPU), anti-cheat kernel, y Game Pass/Play Anywhere (solo cloud)

## 4. Cómo investigamos (dato curioso)

Los buscadores convencionales nos fallaron (cuota agotada, rate-limits). La
solución: **Google NotebookLM como buscador + RAG** — añadimos fuentes por URL,
pedimos búsquedas web relacionadas, y las consultas cruzadas devuelven análisis
con citas. Resultado: tabla comparativa y plan verificados contra fuentes
oficiales sin depender de un solo backend de búsqueda.

## Siguiente paso

Instalación de Bazzite deck (ISO `bazzite-deck-stable-amd64.iso`, 9.6 GB,
verificada por SHA256). En el [siguiente post](2026-08-18-instalacion-bazzite.md) documentaremos la instalación — incluyendo los
problemas de descarga (Cloudflare) y el SSH del instalador (ver [incidencias](../incidencias.md)).
