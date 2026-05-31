---
tags: [comfyui, fal, nodos, referencia]
status: activo
created: 2026-05-31
---

# ComfyUI — Nodos fal.ai disponibles

Setup: ComfyUI en `desktop-linux` (2080 Super), expuesto en `https://comfyui.ramsesvii.com/`
Extensiones instaladas: `ComfyUI-fal-API` + `ComfyUI-fal-Connector`
Inferencia pesada: delegada a `fal.ai` (cuenta con crédito)

---

## Conectores de entrada/salida (`fal-Connector`)

Nodos utilitarios para construir workflows. Son los "bloques" de input y output.

| Nodo | Uso |
|------|-----|
| `String Input (fal)` | Texto — prompts, rutas, strings |
| `Integer Input (fal)` | Números enteros — steps, seed, cantidad |
| `Float Input (fal)` | Números decimales — guidance scale, strength |
| `Boolean Input (fal)` | Verdadero/falso — flags de opciones |
| `Save Image (fal)` | Guardar imagen resultante a disco |
| `Load Image From URL (fal)` | Cargar imagen desde URL como input |
| `Load LoRA from URL (fal)` | Cargar LoRA desde URL |
| `Load Checkpoint from URL (fal)` | Cargar checkpoint desde URL |

---

## Generación de imagen — Text to Image (`fal-api`)

| Nodo | Calidad / Velocidad | Cuándo usar |
|------|---------------------|-------------|
| `Flux Schnell (fal)` | ⚡ Muy rápido, menor calidad | Bocetos rápidos, probar composiciones |
| `Flux Dev (fal)` | ✅ Buena calidad, precio medio | Iteración de concepto — nuestro caballo de batalla |
| `Flux Pro (fal)` | 🔝 Alta calidad | Renders de aprobación |
| `Flux Pro 1.1 (fal)` | 🔝 Alta calidad v2 | Idem, versión mejorada |
| `Flux Ultra (fal)` | 💎 Máxima calidad | Render final, producción |
| `Flux General (fal)` | Flexible | Con LoRAs personalizadas |
| `Flux LoRA (fal)` | Con estilo controlado | Cuando tengamos LoRA de Forasteros |
| `Nano Banana Text-to-Image (fal)` | Rápido | Bocetos conceptuales |
| `Sana (fal)` | Rápido | Alternativa ligera |
| `Recraft V3 (fal)` | Vectorial / ilustración | Íconos, UI, arte plano |
| `Ideogramv3 (fal)` | Texto integrado | Cuando necesitemos texto EN la imagen |
| `HidreamFull (fal)` | Alta calidad alternativa | Variantes estilísticas |
| `Reve Text-to-Image (fal)` | Alta fidelidad | Alternativa a Flux Pro |
| `Dreamina v3.1 Text-to-Image (fal)` | Estilo artístico | Composiciones artísticas |
| `Imagen4 Preview (fal)` | Google Imagen 4 | Fotorrealismo |

---

## Edición de imagen — Image to Image / Edit (`fal-api`)

| Nodo | Uso |
|------|-----|
| `Flux Pro Kontext (fal)` | Edición contextual de imagen con Flux Pro — inpainting inteligente |
| `Flux Pro Kontext Multi (fal)` | Idem con múltiples referencias de imagen |
| `FAL Flux Kontext` *(comfyui-fal-nodes)* | Versión local del Kontext |
| `Flux Pro 1 Fill (fal)` | Inpainting / outpainting con Flux Pro |
| `SeedEdit 3.0 (fal)` | Edición guiada por texto de imagen existente |
| `Seedream 4.0 Edit (fal)` | Edición avanzada de imagen |
| `Nano Banana Edit (fal)` | Edición rápida de imagen |
| `Qwen Image Edit (fal)` | Edición con modelo Qwen |

---

## Segmentación y capas (`comfyui-fal-nodes`)

Útiles para separar personajes del fondo, crear masks, compositing.

| Nodo | Uso |
|------|-----|
| `FAL Birefnet (Remove BG)` | Eliminar fondo de una imagen — extrae personaje en transparente |
| `FAL SAM2 (Florence→SAM2)` | Segmentación semántica completa |
| `FAL SAM2 Auto-Segment` | Segmentación automática de objetos |
| `FAL SAM2 by Point` | Segmentación clickeando un punto |
| `FAL Florence-2` | Detección y descripción de objetos |

---

## Upscale (`fal-api`)

| Nodo | Uso |
|------|-----|
| `Clarity Upscaler (fal)` | ✅ Upscale con detalle — para subir renders a 1920×1080 |
| `Seedvr Upscaler (fal)` | Upscale alternativo |

---

## Generación de video (`fal-api`)

Anotados para cuando lleguemos a animaciones del MainMenu o cutscenes.

| Nodo | Tipo | Nota |
|------|------|------|
| `Kling Video Generation (fal)` | Text-to-Video | Alta calidad, movimiento fluido |
| `Luma Dream Machine (fal)` | Text/Image-to-Video | Cinematic |
| `Veo3 Video Generation (fal)` | Text-to-Video | Google Veo3 |
| `MiniMax Video Generation (fal)` | Text-to-Video | |
| `MiniMax Text-to-Video (fal)` | Text-to-Video | |
| `MiniMax Subject Reference (fal)` | Con referencia de personaje | Útil para consistencia de Forasteros |
| `Wan Pro Image-to-Video (fal)` | Image-to-Video | Animar una imagen estática |
| `Seedance Text-to-Video (fal)` | Text-to-Video | |
| `Seedance Image-to-Video (fal)` | Image-to-Video | |
| `Runway Gen3 Image-to-Video (fal)` | Image-to-Video | Runway ML |
| `Google Veo2 Image-to-Video (fal)` | Image-to-Video | |
| `Krea Wan 14b Video-to-Video (fal)` | Video-to-Video | |
| `Wan 2.5 Preview Image-to-Video (fal)` | Image-to-Video | |
| `Wan VACE Video Edit (fal)` | Edición de video | |
| `Combined Video Generation (fal)` | Múltiples fuentes | |
| `Video Upscaler (fal)` | Upscale de video | |
| `Topaz Upscale Video (fal)` | Upscale con Topaz | |
| `Seedvr Upscale Video (fal)` | Upscale de video | |

---

## Training (`fal-api`)

Para cuando entrenemos LoRA propia de los Forasteros.

| Nodo | Uso |
|------|-----|
| `Flux LoRA Trainer (fal)` | Entrenar LoRA en Flux — consistencia de personajes |
| `WAN LoRA Trainer (fal)` | LoRA para video WAN |
| `LTX Video LoRA Trainer (fal)` | LoRA para video LTX |
| `Hunyuan Video LoRA Trainer (fal)` | LoRA para video Hunyuan |

---

## LLM / VLM (`fal-api`)

| Nodo | Uso |
|------|-----|
| `LLM (fal)` | Modelo de lenguaje — para generar/mejorar prompts dentro del workflow |
| `VLM (fal)` | Vision Language Model — describir imágenes generadas, validar resultados |

---

## Otros (`fal-api`)

| Nodo | Uso |
|------|-----|
| `Upload File (fal)` | Subir archivo a fal.ai |
| `Upload Video (fal)` | Subir video a fal.ai |

---

## Workflows planeados para el proyecto

| Workflow | Nodos clave | Estado |
|----------|-------------|--------|
| BG MainMenu — concepto | String Input → Flux Dev → Save Image | 🔶 Próximo |
| BG MainMenu — render final | String Input → Flux Ultra → Clarity Upscaler → Save Image | 🔲 |
| Consistencia Forasteros (LoRA) | Flux LoRA Trainer → Flux LoRA | 🔲 Futuro |
| Animación MainMenu | Flux Ultra → Wan Pro Image-to-Video | 🔲 Futuro |
| Ilustraciones de cartas | Flux LoRA (con LoRA entrenada) | 🔲 Futuro |
