# Hytale Server – Kubernetes Setup

This setup uses **my custom Docker image** for the Hytale server:  
https://github.com/Logikoz/hytale-server/pkgs/container/hytale-server

This guide explains how to deploy the Hytale server resources using Kubernetes YAML files and how to access the running pod.

---

## Step 0 – Check StorageClass (IMPORTANT)

Make sure a `local-path` StorageClass exists in your cluster.

To verify, run:

```bash
kubectl get storageclass
```

If `local-path` is **not listed**, create it by running:

```bash
kubectl apply -f ./maybe/local-path-storageclass.yaml
```

---

## Step 1 – Create the Namespace

Apply the namespace configuration:

```bash
kubectl apply -f 1-namespace.yaml
```

---

## Step 2 – Deploy the Hytale Hub (StatefulSet)

Create the StatefulSet for the Hytale Hub:

```bash
kubectl apply -f 2-hytale-hub-statefulset.yaml
```

---

## Step 3 – Expose the Hytale Hub (Service)

Create the Service to expose the Hytale Hub:

```bash
kubectl apply -f 3-hytale-hub-service.yaml
```

---

## Step 4 – Find the Running Pod

List the pods in the namespace:

```bash
kubectl get pods -n hytale
```

You should see something like:

```text
hytale-hub-0   Running
```

---

## Step 5 – Attach to the Pod

Attach to the running pod to access the server console:

```bash
kubectl attach -it hytale-hub-0 -n hytale
```

> ⚠️ Important:
> If the pod has more than one container, specify it with:
> `-c <container-name>`

Example:

```bash
kubectl attach -it hytale-hub-0 -n hytale -c hytale-hub
```

---

## Step 6 – Authenticate in the Server Console

Inside the pod console, run:

```text
/auth login device
```
More info: https://support.hytale.com/hc/en-us/articles/45326769420827-Hytale-Server-Manual#running-a-hytale-server

Follow the authentication instructions provided by the server.

---

## Step 7 – Detach from the Pod (WITHOUT stopping it)

To leave the pod **without shutting it down**, use one of the following key combinations:

### Recommended (safe detach)

```text
CTRL + P, then CTRL + Q
```

### Alternative (may suspend your local shell)

```text
CTRL + Z
```

> ⚠️ Do NOT use `CTRL + C` unless you want to stop the process inside the container.

---

## ✅ Setup Complete

Your Hytale Hub is now:

* Deployed in Kubernetes
* Exposed via Service
* Accessible through the pod console
* Authenticated and ready to use


---

## How to Join the Server

After completing the setup, you can connect to your Hytale server using the information below.

### 1. Get the Service address

First, check how the service is exposed:

```bash
kubectl get svc -n hytale
```

Look for your service, for example:

```text
hytale-hub   NodePort   10.43.120.55   <none>   25565:30007/TCP
```

---

### 2. Choose how to connect

#### If using NodePort

Use your node IP and the exposed port:

```text
<node-ip>:<node-port>
```

Example:

```text
192.168.0.10:30007
```

---

#### If using LoadBalancer

Wait for an external IP:

```bash
kubectl get svc hytale-hub -n hytale
```

Then connect using:

```text
<external-ip>:25565
```

---

#### If using Port Forward (local testing)

```bash
kubectl port-forward svc/hytale-hub 25565:25565 -n hytale
```

Then connect to:

```text
localhost:25565
```

---

### 3. Join the server in Hytale

1. Open **Hytale**
2. Go to **Multiplayer**
3. Click **Add Server**
4. Enter the address you obtained above
5. Join the server 🎮

---

Your server is now ready for players! 🚀

---

## 🛠 Troubleshooting

### Pod not running?

```bash
kubectl describe pod hytale-hub-0 -n hytale
kubectl logs hytale-hub-0 -n hytale
```

### PVC stuck in Pending?

Check if the `local-path` StorageClass exists:

```bash
kubectl get storageclass
```

---

Happy hosting! 🎮
