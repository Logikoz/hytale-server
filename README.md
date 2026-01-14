# Hytale Server

This repository provides everything you need to **build, run, and deploy** a Hytale server using Docker and Kubernetes.

The project supports three different workflows, depending on your use case:

- **Build locally** using a Dockerfile  
- **Run with Docker Compose**  
- **Deploy to Kubernetes**  

Choose the option that best fits your environment and follow the corresponding guide below.

---

## 📂 Project Structure

```text
.
├─ build/
│  └─ README.md              # Build the image locally (Dockerfile)
│
├─ deploy/
│  ├─ 1-Docker/
│  │  └─ README.md          # Run with Docker Compose (prebuilt image)
│  │
│  └─ 2-Kubernetes/
│     └─ README.md          # Deploy to Kubernetes
│
└─ README.md                # You are here
```

---

## 🚀 Getting Started

### 1️⃣ Build Mode — Local image (Dockerfile)

If you want to **build the image locally** and run the server from source:

➡️ Go to:
**[`build/README.md`](./build/README.md)**

This guide covers:

* Building the image from a local `Dockerfile`
* Running the server with Docker Compose
* Local development and testing

---

### 2️⃣ Docker Mode — Production / Docker Compose

If you just want to **run the server quickly** using a prebuilt image:

➡️ Go to:
**[`deploy/1-Docker/README.md`](./deploy/1-Docker/README.md)**

This guide covers:

* Running the server with `docker compose up -d`
* Attaching to the container console
* Authenticating with `/auth`
* Connecting to the server

---

### 3️⃣ Kubernetes Mode — Production / Cluster

If you want to **deploy the server on a Kubernetes cluster**:

➡️ Go to:
**[`deploy/2-Kubernetes/README.md`](./deploy/2-Kubernetes/README.md)**

This guide covers:

* StorageClass validation
* Namespace creation
* StatefulSet and Service deployment
* Pod access and authentication
* Player connection instructions

---

## 🎮 Which option should I choose?

| Use case                    | Recommended mode    |
| --------------------------- | ------------------- |
| Local development / testing | **Build Mode**      |
| Small server / home hosting | **Docker Mode**     |
| Production / scalability    | **Kubernetes Mode** |

---

## 🤝 Contributing

Contributions are welcome!
Feel free to open issues, submit pull requests, or suggest improvements to the documentation.

---

## 📜 License (MIT)

This project is provided as-is for educational and community use.
Please check the repository license for more details.

---

Happy hosting! 🚀