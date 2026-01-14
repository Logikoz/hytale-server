# Hytale Server – Local Docker Build (Dockerfile)

This guide explains how to run the Hytale server **locally** using Docker Compose, building the image from a **Dockerfile** in this repository.

---

## Tested Environment

This setup was tested with the following versions (for reference):

- **Docker Compose:** v2.40.3  
- **Docker Engine:** v29.1.3 (build f52814d)

---

## Requirements

- Docker installed
- Docker Compose installed
- A `Dockerfile` present in the project root (same folder as `docker-compose.yml`)

Check with:

```bash
docker --version
docker compose version
```

---

## Step 1 – Build and start the server

In the directory that contains your `docker-compose.yml` and `Dockerfile`, run:

```bash
docker compose up -d --build
```

This will:

* Build the image from the local `Dockerfile`
* Create the container `hytale-server-local`
* Run the server in the background

---

## Step 2 – Check if the container is running

```bash
docker ps
```

You should see `hytale-server-local` with status `Up`.

---

## Step 3 – Attach to the server console (first-time auth / troubleshooting)

### Option A (recommended): enable interactive console in Compose

If this is your **first time** (or `docker attach` doesn’t behave as expected), enable interactive mode by uncommenting these lines in your `docker-compose.yml`:

```yaml
# stdin_open: true
# tty: true
```

Then recreate the container:

```bash
docker compose down
docker compose up -d --build
```

Now attach to the server console:

```bash
docker attach hytale-server-local
```

### Option B: attach directly (if it works for you)

```bash
docker attach hytale-server-local
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

Your Compose file exposes:

```yaml
ports:
  - "5520:5520/udp"
```

So connect using:

```text
<your-server-ip>:5520
```

Examples:

* Same machine:

  ```text
  127.0.0.1:5520
  ```
* LAN:

  ```text
  192.168.0.10:5520
  ```

### Notes

* Make sure **UDP 5520** is allowed in your firewall (especially on Linux).
* If you’re hosting for the internet, forward **UDP 5520** on your router to this machine.

---

## Step 7 – Basic management

### View logs

```bash
docker logs -f hytale-server-local
```

### Restart

```bash
docker compose restart
```

### Stop (and remove container)

```bash
docker compose down
```

### Rebuild after changing the Dockerfile

```bash
docker compose up -d --build
```

---

## ✅ Setup Complete

Your Hytale server is now running from a **local Dockerfile build** and ready for players.

Happy hosting! 🎮