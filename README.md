# 📘 Minikube Kubernetes Project Documentation

## PHP + MySQL + FTP (FTP access + Database in Webpage)

---

## 🧰 1. Requirements

* Ubuntu installed
* Docker installed
* Minikube installed
* kubectl installed
* Git installed

---

## 🔄 2. Clone the GitHub Repository

Run this command to clone the repo with all deployment files:

```bash
git clone 
cd minikub_tp
```
This downloads the entire project including YAML files, SQL init script, and PHP file.

---

## 🚀 3. Start Minikube with Docker Runtime

```bash
minikube start --driver=docker
```
Starts a local Kubernetes cluster on your machine using Docker as the VM.

---

## 🧱 4. Create a Namespace

```bash
kubectl create namespace sports-app
```
Isolates the resources of this project inside the `sports-app` namespace.

---

## 🗂 5. Verify Files in the Cloned Directory

Make sure you are in the project folder and list files:

```bash
ls
```

You should see:

```text
apache-php-deployment.yaml
ftp-deployment.yaml
mysql-deployment.yaml
mysql-init.sql
index.php
```

---

## 📦 6. Deploy MySQL with Initialization Script

```bash
kubectl apply -f mysql-deployment.yaml -n sports-app
```
This deploys the MySQL pod and runs the `mysql-init.sql` to:

* Create the `football_db` database
* Create `players` table and insert sample players
* Create user `webuser` with password `webpassword`

---

## 📁 7. Deploy FTP Server

```bash
kubectl apply -f ftp-deployment.yaml -n sports-app
```

**Explanation**:
Deploys the FTP server with credentials:

* Username: `admin`
* Password: `admin`

---

## 🌐 8. Deploy Apache + PHP Pod

```bash
kubectl apply -f apache-php-deployment.yaml -n sports-app
```
Deploys the Apache PHP pod running the web server with `index.php` to display MySQL data.

---

## 📊 9. Check Service Ports

List services to get assigned NodePorts:

```bash
kubectl get svc -n sports-app
```

Example output:

```text
apache-php-service   NodePort   80:32103/TCP
ftp-service          NodePort   21:32594/TCP
mysql-service        ClusterIP  3306/TCP
```

---

## 🌍 10. Access the PHP Web Interface

Get Minikube IP address:

```bash
minikube ip
```

Open the browser and navigate to:

```
http://<minikube-ip>:32103
```

You should see the football players displayed in a table.

---

## 📤 11. Connect to FTP Server

Using terminal:

```bash
ftp <minikube-ip> 32594
```

* Username: `admin`
* Password: `admin`

Or use any FTP client like FileZilla.
  ```


