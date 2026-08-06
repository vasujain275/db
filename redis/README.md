# 🧠 Valkey + Redis Commander Setup

A modern, fully open-source replacement for Redis + RedisInsight — powered by **Valkey** (Linux Foundation fork of Redis) and **Redis Commander** (a lightweight, Adminer-like dashboard).

---

## 🚀 Overview

This stack provides:
- **Valkey** → open-source drop-in replacement for Redis  
- **Redis Commander** → clean web dashboard to explore, edit, and manage Valkey data  
- **Persistent storage** via Docker volumes  

---

## 🧩 Services

| Service | Description | Port | URL |
|----------|--------------|------|-----|
| **Valkey** | In-memory data store (Redis-compatible) | `6379` | `redis://default:valkey123@localhost:6379/0` |
| **Redis Commander** | Web-based Redis GUI | `8091` | [http://localhost:8091](http://localhost:8091) |

---

## 🛠️ Setup Instructions

1. **Start the stack**
   ```bash
   docker compose up -d
   ```

2. **Verify running containers**
   ```bash
   docker ps
   ```
   You should see:
   - `valkey`
   - `redis-commander`

3. **Access Redis Commander**
   Open [http://localhost:8091](http://localhost:8091) in your browser.  
   You’ll see the connected Valkey instance.

---

## 🔑 Connection Details

| Property | Value |
|-----------|--------|
| **Host** | `localhost` |
| **Port** | `6379` |
| **Password** | `valkey123` |
| **Database** | `0` |
| **Connection URL** | `redis://default:valkey123@localhost:6379/0` |

You can use this URL directly in apps, e.g.:
```python
# Example (Python)
import redis
r = redis.Redis.from_url("redis://default:valkey123@localhost:6379/0")
r.set("hello", "world")
print(r.get("hello"))
```

---

## 🧹 Stop & Cleanup

Stop the containers:
```bash
docker compose down
```

Stop and remove volumes (⚠️ deletes all stored data):
```bash
docker compose down -v
```

---

## 📦 Volumes

| Volume | Purpose |
|---------|----------|
| `valkey-data` | Persists Valkey data on host |

---

## ⚙️ Environment Variables

You can change credentials and ports in `docker-compose.yml`:

```yaml
command: ["valkey-server", "--requirepass", "yourpassword"]
```

and update:
```yaml
- REDIS_HOSTS=local:valkey:6379:0:yourpassword
```

---

## 🧠 Notes

- Valkey is fully compatible with Redis clients — you can use any existing Redis SDK.
- Redis Commander auto-connects to your local Valkey instance.
- No telemetry, no cloud dependencies — 100% local setup.

---

## 🧾 License

This setup is open and free for personal and commercial use.
