---
tags: [gdd, tecnico, godot, status]
status: activo
created: 2026-05-30
updated: 2026-05-30
---

# 07 — Técnico

## [[../HOME|← Volver al índice]]

---

### Stack del MVP digital

| Capa | Tecnología |
|------|-----------|
| **Motor** | Godot 4.6.3-stable |
| **Lenguaje** | GDScript (no C#) |
| **Networking** | WebSocketMultiplayerPeer sobre WSS |
| **Servidor** | Mismo binario Godot exportado, `--headless` |
| **Persistencia** | PostgreSQL 16 (db `leyendas` en `panel-db`) |
| **Proxy** | Caddy (TLS automático) |
| **Orquestación** | systemd (`leyendas-server.service`) |
| **Host** | VPS srv1404743 (212.85.13.145), Ubuntu 24.04 |

### Proyecto en disco

```
/opt/desarrollo/leyendas-del-sur/
├── core/              → Motor de Reglas (GDScript puro, headless)
│   ├── motor_reglas.gd
│   ├── data_loader.gd
│   ├── state/         → EstadoPartida, Accion, Evento, etc.
│   └── efectos/       → Efectos de cartas + sinergias
├── ui/                → Escenas Godot del cliente
│   ├── hud/           → HUD del tablero
│   └── screens/       → Pantallas (tablero, etc.)
├── effects/           → Animaciones y efectos visuales
├── data/              → JSON de Forasteros, Dones, cartas
├── assets/            → Art, fonts, sfx
├── cli/               → CLI debug client (play.gd)
├── tests/             → Tests headless (13 archivos, 203 tests)
├── docs/              → spec.md, source/ (fuentes fundacionales)
└── CLAUDE.md          → Documentación del proyecto
```

### Estado del desarrollo (30/05/2026)

**✅ Completado — Motor de Reglas (M1 completo):**
- 203 tests verdes, 0 fallidos
- 6 Forasteros, 6 Dones, 45 cartas (27 Personajes + 18 Suerte)
- 6 sinergias Forastero+Carta implementadas
- Economía cerrada de 18 tokens verificada por fuzzer (8.000 acciones, 100 partidas)
- Determinismo bit-exacto verificado por replay
- CLI debug client jugable (hotseat)
- Invariantes validados (mano siempre 2 cartas, 18 tokens en juego)

**🔜 Pendiente (para próximos milestones):**
- UI gráfica en Godot (tablero, cartas, HUD)
- Networking (WebSocket server + client)
- Salas + matchmaking
- Conexión a PostgreSQL
- Sistema de efectos visuales / animaciones

### Configuración del servidor (planeada)

| Recurso | Asignación |
|---------|-----------|
| Subdominio | `leyendas.ramsesvii.com` |
| Puerto game server (WS) | `127.0.0.1:3130` |
| Puerto lobby futuro | `127.0.0.1:3140` (reservado) |
| Servicio systemd | `leyendas-server.service` |
| DB | `leyendas` en `panel-db` |

### Enlaces útiles

- [[../12-assets/Informe_Sectorial_Juegos_Cartas_Mesa_2026.md|Informe Sectorial de Mercado]]
- [[../12-assets/Leyendas_del_Sur_Brief_Diseno_2026.txt|Brief de Diseño completo]]
- [[../12-assets/Leyendas_del_Sur_Ficha_Tecnica_Produccion.md|Ficha Técnica de Producción]]
