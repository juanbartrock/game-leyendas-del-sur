---
tags: [ui, godot, tarea, mainmenu]
status: en-curso
created: 2026-05-31
---

# Tarea: Main Menu

## Objetivo

Pantalla de título de Leyendas del Sur al estilo Kingdom Hearts Birth by Sleep:
composición épica con los Forasteros en poses heroicas, logo plateado metálico,
menú vertical mínimo. Primera impresión del juego — tiene que comunicar la
identidad visual de Refugio del Sur al instante.

## Referencia visual

**Kingdom Hearts Birth by Sleep** — los tres protagonistas en poses dinámicas
contra un fondo de oscuridad y estrellas. Logo grande, menú discreto abajo a la
izquierda. Los personajes "sangran" al borde de la pantalla.

Nuestro equivalente: los 6 Forasteros en composición similar, fondo cuero oscuro
con atmósfera de Buenos Aires mítica. Logo "LEYENDAS DEL SUR" en tipografía
metálica plateada.

## Estructura en Godot

```
MainMenu (Control)
├── BG (TextureRect)         ← imagen generada, full rect
├── Logo (Label o Texture)   ← "LEYENDAS DEL SUR" + subtítulo
├── Menu (VBoxContainer)     ← JUGAR / OPCIONES / SALIR
└── Version (Label)          ← v0.1.0-mvp, esquina inferior
```

Animaciones planeadas (post-BG):
- Fade in del logo al cargar
- Leve parallax o flotación de algún Forastero
- Highlight dorado del ítem de menú seleccionado

## Subtareas

### ✅ S1 — Script de lógica limpio
Script `main_menu.gd` reducido a navegación por teclado.
Layout 100% en el editor, sin construcción programática.

### 🔲 S2 — Generación del BG con ComfyUI
**La tarea más importante y creativa.**

Generar una imagen 1920×1080 con los Forasteros en composición épica.

**Assets disponibles como referencia:**
- Renders 3D: Carpincho Ronin, La Llama, Hornero Arquitecto
  (en `assets/art/forasteros_3d/` — tienen basecolor, normal, roughness)
- Arte 2D de cartas: los 6 Forasteros
  (en `assets/art/forasteros/`)

**Approach en ComfyUI:**
- IPAdapter o img2img con los renders 3D como reference
- ControlNet OpenPose si queremos controlar poses
- Estilo: epic fantasy digital painting, dark atmosphere
- Paleta forzada: `#1A0F08` (fondo), turquesa `#4ABFC1`, dorado `#F5C842`,
  plata `#C8C8C8`
- Resolución: 1920×1080

**Alternativa si ComfyUI no da el resultado esperado:**
- Gemini / AI Studio (suscripción disponible) para variantes
- Nano Banana 2 para iteraciones rápidas de concepto

**Criterio de aprobación:**
- Los Forasteros son reconocibles
- Composición deja espacio libre a la izquierda para el logo y menú
- Atmósfera oscura y épica, paleta respetada
- Se ve bien a 1920×1080

### 🔲 S3 — Layout en Godot sobre el BG
Una vez aprobado el BG, armar en el editor:
- TextureRect BG full rect
- Logo (tipografía o imagen si lo genera la IA con el logo integrado)
- VBoxContainer con las 3 opciones de menú
- Label versión

### 🔲 S4 — Conectar script a los nodos (@onready)
- `_menu_labels` apuntando a los Labels del VBoxContainer
- Navegación con teclado funcional
- `_select_item()` conectado

### 🔲 S5 — Animaciones
- AnimationPlayer o Tween para fade in del logo
- Highlight del ítem seleccionado (color dorado)
- Posible: parallax sutil del BG con el mouse

## Decisiones abiertas

- ¿El logo es un Label con tipografía o una imagen generada con la IA?
  (imagen generada da más control visual pero menos flexibilidad)
- ¿Animamos personajes individualmente o el BG es 100% estático?

## Archivos relevantes

- `ui/screens/main_menu/main_menu.gd`
- `ui/screens/main_menu/main_menu.tscn`
- `ui/theme/lds_theme.gd`
- `assets/art/forasteros_3d/` — renders de referencia para ComfyUI
- `assets/art/forasteros/` — arte 2D de cartas
