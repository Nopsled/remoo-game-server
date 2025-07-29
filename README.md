# Simple WebSocket Game Server

A **pure‑Python** WebSocket server for a top‑down multiplayer game prototype (think _MooMoo.io_–style).  
It handles the entire handshake and framing layer itself (no `websockets` or `aiohttp`), packs packets with **MessagePack**, maintains a tiny game world, and streams real‑time player / object updates to connected clients.

> **Status: experimental / proof‑of‑concept**  
> The code is intentionally minimal and not production‑ready. Use it to learn how WebSocket framing works, how to structure a lightweight game loop, or as a starting point for your own hobby project.

---

## ✨  Features

| Area | Details |
|------|---------|
| **WebSocket handshake** | Custom implementation — no third‑party WebSocket library required. |
| **Binary framing** | Supports `OPCODE_TEXT`, `OPCODE_BINARY`, `PING`, `PONG`, and `CLOSE`. |
| **Message format** | Uses [`msgpack`](https://msgpack.org/) for compact packets. |
| **Game objects** | Players (`PlayerObject`) and scenery (`GameObject`) with IDs, position, scale, etc. |
| **Minimal game loop** | Position updates, simple 8‑direction movement, basic attack flag. |
| **Broadcast helpers** | Framework in place (`GameWorldManager`) for global messages / resource grants. |
| **Threaded I/O** | Separate threads per client for receive & game‑loop ticks. |

---

## 📦  Requirements

* Python 3.8 +  
* [`msgpack`](https://pypi.org/project/msgpack/)   `pip install msgpack`

> **Note**  
> The script imports a local module `Net.PacketCodes` that maps packet IDs ↔ codes.  
> Provide your own or stub it out if you only want to test the transport layer.

---

## 🚀  Quick start

```bash
git clone https://github.com/<your‑user>/<your‑repo>.git
cd <your‑repo>

# (optional) create a venv
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

pip install msgpack

python server.py           # or whatever filename you choose
By default the server binds to 0.0.0.0:3000:
