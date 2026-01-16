# Hytale Server – Docker Setup

This setup uses **my custom Docker image** for the Hytale server:  
https://github.com/Logikoz/hytale-server/pkgs/container/hytale-server

This guide explains how to run the Hytale server using **Docker Compose**.

---

## Tested Environment

This setup was tested with the following versions (for reference):

- **Docker Compose:** v2.40.3  
- **Docker Engine:** v29.1.3 (build f52814d)

Your environment does not need to match these versions exactly, but using similar or newer versions is recommended.

---

## Step 1 – Start the server

In the directory that contains `docker-compose.yml`, run:

```bash
docker compose up -d
```

---

## Step 2 – Check if the container is running

```bash
docker ps
```

You should see `hytale-server` with status `Up`.

---

## Step 3 – Attach to the server console (first-time auth / troubleshooting)

### Option A (recommended): enable interactive console in Compose

If this is your **first time** (or the session is unauthenticated) and `docker attach` doesn’t behave as expected, enable interactive mode by uncommenting these lines in your `docker-compose.yml`:

```yaml
# stdin_open: true
# tty: true
```

Then recreate the container:

```bash
docker compose down
docker compose up -d
```

Now attach to the server console:

```bash
docker attach hytale-server
```

### Option B: attach directly (if it works for you)

```bash
docker attach hytale-server
```

---

## Step 4 – Authenticate in the server console

Inside the container console, run:

```text
/auth login device
```
More info: https://support.hytale.com/hc/en-us/articles/45326769420827-Hytale-Server-Manual#running-a-hytale-server

Follow the authentication instructions printed by the server.

---

## Step 5 – Detach from the container (WITHOUT stopping it)

To leave the container **without shutting it down**, use one of the following key combinations:

### Recommended (safe detach)

```text
CTRL + P, then CTRL + Q
```

### Alternative (may suspend your local shell in some terminals)

```text
CTRL + Z
```

> ⚠️ Do NOT use `CTRL + C` unless you want to stop the server process.

---

## Step 6 – How to join the server

Your `docker-compose.yml` exposes this port:

```yaml
ports:
  - "5520:5520/udp"
```

So players should connect using:

```text
<your-server-ip>:5520
```

Example:

```text
192.168.0.10:5520
```

### Notes

* Make sure **UDP 5520** is allowed in your firewall/router (LAN and/or WAN, depending on your use case).
* If you are hosting for the internet, you may need to forward UDP 5520 on your router to the machine running Docker.

---

## Step 7 – Basic management

### View logs

```bash
docker logs -f hytale-server
```

### Restart

```bash
docker compose restart
```

### Stop (and remove container)

```bash
docker compose down
```

---

## ✅ Setup Complete

Your Hytale server is now running via Docker Compose and ready for players.

Happy hosting! 🎮
