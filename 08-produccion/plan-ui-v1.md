---
tags: [produccion, ui, planificacion, godot]
status: activo
created: 2026-05-30
---

# Plan UI — Leyendas del Sur (desde cero)

> Todo el código UI anterior queda como aprendizaje. Esta es la nueva planificación.
> **Filosofía:** planificar antes de codificar. Cada componente tiene definición clara antes de implementarse.

---

## 🎨 Sistema de diseño

Derivado directamente del nuevo estilo del Mazo.

### Paleta de colores

| Token | Hex | Uso |
|-------|-----|-----|
| `color_bg_deep` | `#1A0F08` | Fondo profundo (cuero oscuro) |
| `color_bg_surface` | `#2C1A0E` | Superficies de paneles |
| `color_pergamino` | `#D4B483` | Fondos de zonas de lectura |
| `color_pergamino_dark` | `#B8934A` | Bordes/sombras de pergamino |
| `color_turquesa` | `#4ABFC1` | Marco de cartas de acción, acentos primarios |
| `color_turquesa_bandera` | `#75AADB` | Marco de cartas de Don |
| `color_verde_neon` | `#39D353` | Cartas especiales, acciones reactivas |
| `color_dorado` | `#F5C842` | Tipografía de títulos, ornamentos |
| `color_dorado_dark` | `#8B5E1A` | Texto de efectos en pergamino |
| `color_plata` | `#C8C8C8` | Ornamentos del dorso, marcos metálicos |
| `color_texto_claro` | `#F5F0E8` | Texto principal sobre fondos oscuros |
| `color_texto_oscuro` | `#1A0F08` | Texto sobre pergamino |

### Tipografía

| Rol | Familia | Uso |
|-----|---------|-----|
| **Display** | Serif decorada (EB Garamond / Pinyon Script) | Títulos de cartas, logo, nombres de pantalla |
| **Body** | Serif humanista (IM Fell English) | Textos de efectos, flavor text |
| **UI** | Sans humanista pequeña | Números, labels, datos |

> 📌 Las 4 familias ya están importadas en el proyecto Godot (`assets/fonts/`)

### Ornamentos y texturas

- **Fondo del tablero:** textura de cuero oscuro envejecido (tileable)
- **Paneles:** bordes con esquinas ornamentales art déco/colonial en plata
- **Separadores:** líneas finas doradas o plateadas
- **Highlight de turno activo:** glow dorado suave

---

## 🗺️ Flujo de pantallas

```
MainMenu
    │
    ├─ [Jugar] → Sala
    │               ├─ [Crear sala] → SalaEspera ──┐
    │               └─ [Unirse]    → SalaEspera ──┘
    │                                   │
    │                               [Iniciar]
    │                                   │
    │                            RepartoForasteros
    │                                   │
    │                              [Confirmar]
    │                                   │
    │                           Tablero (core) ◄────┐
    │                               │               │
    │                      [Overlay: TargetPicker]  │
    │                      [Overlay: Negociacion]   │
    │                      [Overlay: Victoria]      │
    │                               │               │
    └───────────────────────────────┘               │
                          [Jugar otra vez] ─────────┘
```

---

## 📱 Pantallas — definición

---

### 1. MainMenu

**Propósito:** primera impresión del juego. Debe comunicar la estética inmediatamente.

**Elementos:**
- Fondo: tablero/mesa de cuero oscuro con textura, velas o luz ambiental
- Logo **LEYENDAS DEL SUR** centrado, grande, tipografía 3D metálica plateada (como el dorso)
- Subtítulo: *"Refugio del Sur"* en serif dorado pequeño
- Botones (dos únicos):
  - `[JUGAR]` — botón principal, tipografía serif dorada sobre fondo oscuro con borde ornamental
  - `[SALIR]` — botón secundario, más discreto
- Versión del juego discreta en esquina inferior (pequeño, semitransparente)

**Animaciones:**
- Fade in del logo al cargar
- Partículas de luz/brasa muy sutiles en el fondo (opcional, no para MVP)

---

### 2. Sala (Crear / Unirse)

**Propósito:** configurar la sala antes de jugar.

**Elementos:**
- Panel de pergamino centrado, con marco ornamental
- Título: *"Nueva Partida"*
- Campo de nombre del jugador (input con estilo de tinta sobre pergamino)
- Dos opciones:
  - `[CREAR SALA]` → genera código de 4 letras, pasa a SalaEspera
  - `[UNIRSE A SALA]` → muestra input para código
- Botón `[VOLVER]` discreto

---

### 3. SalaEspera

**Propósito:** esperar a que se unan los jugadores antes de arrancar.

**Elementos:**
- Panel principal con lista de jugadores conectados (nombre + ícono de Forastero si está disponible)
- Código de sala visible y copiable, destacado
- Botón `[INICIAR PARTIDA]` (solo visible para el creador)
- Estado: *"Esperando jugadores… (2/6)"*

---

### 4. RepartoForasteros

**Propósito:** mostrar qué Forastero le tocó a cada jugador antes de arrancar.

**Elementos:**
- Fondo de tablero oscuro
- 6 posiciones radiales (o en grilla), una por jugador
- Cada posición muestra: carta de Forastero (grande, frontal) + nombre del jugador debajo
- Animación de "reveal": las cartas aparecen boca abajo y giran para revelar
- Botón `[COMENZAR]` una vez que todos vieron

---

### 5. Tablero — pantalla principal (el core)

Esta es la pantalla más compleja. Se divide en **zonas fijas**:

```
┌─────────────────────────────────────────────────────┐
│                  ZONA OPONENTES                     │
│     [Jugador 2]  [Jugador 3]  [Jugador 4]           │
│      [Jugador 5]    [Jugador 6]                     │
├─────────────────────────────────────────────────────┤
│                                                     │
│          ZONA CENTRAL                               │
│   ┌──────────────────────────────────┐              │
│   │  [Don1] [Don2] [Don3]            │  [Mazo]      │
│   │  [Don4] [Don5] [Don6]            │  [Descarte]  │
│   └──────────────────────────────────┘              │
│                                                     │
├─────────────────────────────────────────────────────┤
│                  ZONA ACTIVA                        │
│   [Forastero propio]  [Mano: carta1] [Mano: carta2] │
│   Dones acumulados    [turno, ronda, alianzas]      │
└─────────────────────────────────────────────────────┘
│   LOG DE EVENTOS (desplegable o lateral)            │
└─────────────────────────────────────────────────────┘
```

**Sub-zonas:**

#### 5A. ZonaOponentes
- Cada oponente: panel compacto con nombre, Forastero (icono pequeño), cantidad de Dones acumulados (número con ícono), indicador de turno activo (glow dorado), indicadores de alianza/inmunidad/bloqueo
- Diseño: panel de pergamino compacto con marco turquesa

#### 5B. ZonaCentral
- 6 pilas de Don, cada una: ícono del Don + número de cartas restantes + nombre
- Mazo: pila con dorso visible + contador de cartas
- Descarte: última carta visible encima
- Las pilas se destacan visualmente cuando son target seleccionable

#### 5C. ZonaActiva (jugador local)
- Carta del Forastero propio (tarot, más grande)
- Dones acumulados: 6 íconos con el número de cada Don
- Mano: 2 cartas de acción, interactuables (hover lift + click para jugar)
- Info de turno: ronda actual, de quién es el turno, alianzas activas

#### 5D. LogEventos
- Panel pequeño colapsable
- Lista scrolleable de los últimos eventos de la partida
- Tipografía serif pequeña, fondo pergamino oscuro

---

### 6. Overlay — TargetPicker

**Propósito:** cuando el jugador juega una carta que requiere objetivos.

**Elementos:**
- Panel modal semi-transparente sobre el tablero
- Instrucción clara: *"Seleccioná 2 jugadores"* / *"Elegí un Don del centro"*
- Los elementos válidos se iluminan (glow dorado), los inválidos se atenúan
- Botón `[CANCELAR]`

---

### 7. Overlay — Negociacion

**Propósito:** la fase de negociación al final de cada ronda.

**Tipos:** Trueque | Alianza | Traición

**Elementos:**
- Panel de pergamino central, más grande que TargetPicker
- Título del tipo de negociación con ícono
- Para **Trueque:** selector de qué Don ofrecés y qué pedís
- Para **Alianza:** seleccionás jugador, esperás respuesta
- Para **Traición:** confirmación (con consecuencia: Dones revelados)
- Timer visible (60 segundos, barra que decrece)
- `[PROPONER]` / `[PASAR]`

---

### 8. Overlay — Victoria

**Propósito:** anunciar quién ganó.

**Elementos:**
- Overlay dramático sobre toda la pantalla
- Fondo oscuro semitransparente con partículas de luz
- Texto épico: *"¡[Nombre] completó los 6 Dones de la Argentinidad!"*
- Carta del Forastero ganador, grande, centrada
- Nombre del Forastero en tipografía display dorada
- `[NUEVA PARTIDA]` / `[MENÚ PRINCIPAL]`

---

## 🧩 Componentes reutilizables

Orden de construcción sugerido (de átomo a molécula):

| Orden | Componente | Descripción |
|-------|-----------|-------------|
| 1 | `CardAccion` | Carta de acción completa (marco, ilustración, nombre, efecto). Verticale 2:3 |
| 2 | `CardDon` | Carta de Don cuadrada (1:1), marco turquesa bandera |
| 3 | `CardBack` | Dorso del mazo (acción o Don) |
| 4 | `DonIcon` | Ícono + número de un Don específico |
| 5 | `DonPile` | Pila central de un Don (CardDon + contador) |
| 6 | `PlayerPanel` | Panel compacto de oponente |
| 7 | `ActivePlayerPanel` | Panel expandido del jugador local |
| 8 | `HandContainer` | Contenedor de la mano (2 × CardAccion interactuables) |
| 9 | `EventLog` | Panel de log colapsable |
| 10 | `ActionButton` | Botón estilizado con marco ornamental |
| 11 | `OrnamentalPanel` | Panel genérico con marco art déco |
| 12 | `TargetPicker` | Overlay de selección de objetivos |
| 13 | `NegociacionPanel` | Overlay de negociación |
| 14 | `VictoriaOverlay` | Overlay de victoria |

---

## 📐 Resolución y escala

- **Resolución base:** 1920×1080 (como define el spec)
- **Scaling:** `CanvasItem` con `viewport` — Godot 4 maneja el escalado
- **Cartas de acción:** ~200×266 px en pantalla (ratio 2:3), agrandables a ~280×373 en hover
- **Cartas de Don:** ~120×120 px en pila, ~180×180 en vista expandida
- **Tipografía mínima:** 14px a 1080p

---

## 🚀 Orden de implementación

### Sprint 1 — Fundación visual
- [ ] Crear `theme.tres` global con paleta, tipografías y estilos base
- [ ] `OrnamentalPanel` — el contenedor base reutilizable
- [ ] `ActionButton` — botón estilizado
- [ ] `MainMenu` — primera pantalla funcional y con estética correcta

### Sprint 2 — Componentes de carta
- [ ] `CardBack` (dorso, para el mazo)
- [ ] `CardDon` (cuadrada, con ícono y nombre)
- [ ] `CardAccion` (vertical, con ilustración y efecto)
- [ ] `DonIcon` + `DonPile`

### Sprint 3 — Tablero
- [ ] Layout base del Tablero (zonas)
- [ ] `ZonaCentral` (6 pilas de Don + mazo + descarte)
- [ ] `ActivePlayerPanel` + `HandContainer`
- [ ] `PlayerPanel` (oponentes)

### Sprint 4 — Interacción
- [ ] Conectar motor de reglas al tablero
- [ ] `TargetPicker` overlay
- [ ] `EventLog`
- [ ] Hover y animaciones básicas (Tween)

### Sprint 5 — Pantallas auxiliares + overlays
- [ ] `Sala` y `SalaEspera`
- [ ] `RepartoForasteros`
- [ ] `NegociacionPanel`
- [ ] `VictoriaOverlay`

### Sprint 6 — Polish
- [ ] Sonidos UI (5 SFX básicos)
- [ ] Transiciones entre pantallas
- [ ] Animaciones de carta (draw, play, win)

---

## ❓ Decisiones pendientes — responder antes de Sprint 3

1. **Layout del tablero:** ¿los oponentes van en arco arriba o en grilla 2×2 arriba?
2. **Cartas de Forastero:** ¿se muestran siempre visibles en el tablero o solo en RepartoForasteros?
3. **Información de Dones propios:** ¿visible siempre o solo cuando es tu turno?
4. **Log de eventos:** ¿lateral (columna derecha) o inferior (barra desplegable)?
