---
tags: [gdd, produccion, roadmap]
status: activo
created: 2026-05-30
updated: 2026-05-30
---

# 08 — Producción

## [[../HOME|← Volver al índice]]

---

### Roadmap general

#### 🎮 Fase 0 — Fundación (completada)
- [x] Proyecto Godot bootstrapeado
- [x] CLAUDE.md con convenciones del proyecto
- [x] Git init, .gitignore, estructura de carpetas
- [x] Spec.md v1.0/v1.1/v1.2 escrito
- [x] Data de Forasteros, Dones, cartas en JSON
- [x] 4 ilustraciones de Forasteros generadas

#### ⚙️ Fase 1 — Motor de Reglas (completada)
- [x] M1.0 — Bootstrap Godot + DataLoader
- [x] M1.1 — Resource classes + DataLoader real
- [x] M1.2 — Estado de partida (7 clases serializables)
- [x] M1.3 — Motor de reglas core
- [x] M1.4a — Efectos simples (4 cartas)
- [x] M1.4b — Efectos restantes (14 cartas)
- [x] M1.4c — 6 sinergias Forastero+Carta
- [x] M1.5 — Tests de replay + victoria
- [x] M2 — CLI debug client jugable (hotseat)
- [x] Fuzzer: 100 partidas, 8.000 acciones, 0 fallos

#### 🖥️ Fase 2 — MVP Cliente (próxima)
- [ ] UI gráfica del tablero de juego
- [ ] Animaciones y efectos visuales
- [ ] Conexión WebSocket al servidor
- [ ] Vista filtrada por jugador (info oculta)
- [ ] Fase de negociación (trueque, alianza, traición)
- [ ] Tooltips de cartas

#### 🌐 Fase 3 — Servidor (próxima)
- [ ] Servidor headless autoritativo
- [ ] Salas con código
- [ ] Reconnect
- [ ] Persistencia PostgreSQL
- [ ] Healthcheck `/healthz`

#### 🚀 Fase 4 — Lanzamiento MVP
- [ ] Sistema de efectos visuales
- [ ] Overlay de victoria
- [ ] Sonidos UI básicos
- [ ] Builds desktop (Win/Mac/Linux)
- [ ] Deploy a producción

#### 🃏 Fase F — Juego físico (paralelo)
- [ ] Brief de diseño visual completo ✅
- [ ] Cotizaciones de producción ✅
- [ ] Análisis de mercado ✅
- [ ] Generación de ilustraciones (ComfyUI / Nano Banana)
- [ ] Prototipo físico
- [ ] Campaña Gamefound

---

### Costos de producción física (referencia)

Para **1.000 unidades** fabricadas en China:

| Concepto | Estimado USD |
|----------|-------------|
| Producción (3 mazos + caja + reglamento + extras) | $6.400 - $11.300 |
| Flete marítimo | $2.000 - $3.500 |
| **Subtotal CIF (puesto en Argentina)** | **$8.400 - $14.800** |
| Aranceles + IVA (~45%) | $3.780 - $6.660 |
| **Costo por unidad en depósito** | **$12.50 - $22.00 USD** |

> Ver detalle completo en [[../12-assets/Leyendas_del_Sur_Ficha_Tecnica_Produccion.md|Ficha Técnica]]
> Y costos en [[../12-assets/Leyendas_del_Sur_Costos_Produccion.csv|Costos CSV]]

---

### Estado actual del proyecto

📍 **30 de mayo de 2026**
- Motor de reglas COMPLETO ✅ (203 tests, fuzzer validado)
- Brief de diseño físico COMPLETO ✅
- Documentos de mercado y producción COMPLETOS ✅
- **Próximo gran hito:** UI gráfica del tablero en Godot

---

### Decisiones de alcance (lo que NO hacemos en MVP)

- ❌ Cuentas persistentes, login, ranking
- ❌ Mazo personalizable / colección
- ❌ Modo single-player vs IA
- ❌ Chat en partida (negociación por voz/Discord externo)
- ❌ Música y voice acting
- ❌ Mobile / touch
- ❌ Sinergias entre Forasteros (solo Forastero+Carta)
