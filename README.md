# 📦 AWX Deployment Using AWX Operator and Helm 

## (⚠️ Work-in-progress learning project — issues expected, improvements ongoing)

## 📖 Overview

This project demonstrates deploying AWX (Ansible Web eXecutable) on a Kubernetes cluster using the AWX Operator Helm chart.
AWX is an open-source web-based UI for managing Ansible automation.

## 📋 Prerequisites

A Kubernetes cluster (local or cloud)

kubectl configured to access your cluster

Helm 3 installed

Basic knowledge of Kubernetes and Helm

## 🚀 Installation Steps

### 1️⃣ Create the AWX Namespace

```console
kubectl create ns awx
```

### 2️⃣ Add the AWX Operator Helm Repository

```console
helm repo add awx-operator-helm https://ansible-community.github.io/awx-operator-helm/
```

```console
helm repo update
```

### 3️⃣ Prepare Configuration

A configuration file named awx-values.yaml is included in this repository.
It defines deployment settings like service type, PostgreSQL connection details, and admin credentials.

Important: Before deploying, review and update the awx-values.yaml file — especially the AWX.postgres.password field.

### 4️⃣ Install AWX Operator and AWX
Run this Helm install command:

```console
helm install my-awx-operator awx-operator-helm/awx-operator --version 3.1.0 -n awx -f awx-values.yaml --set AWX.postgres.password="YourStrongPassword"
```

### 5️⃣ Verify Deployment
Check pod status by running:

```console
kubectl get pods -n awx
```

Wait until all pods show Running or Completed.

![](Images/Pods.PNG)

### 6️⃣ Access AWX
Forward the AWX web service port to your local machine:

```console
kubectl port-forward svc/awx-service -n awx 10000:80 --address=0.0.0.0
```

Then open your browser and go to: 

```console
http://localhost:10000
```

![](Images/Login.PNG)

Login using the admin username and password configured in your awx-values.yaml file.

![](Images/AfterLogin.PNG)

**## 📖 Additional Help**


AWX Official Documentation: https://awx.readthedocs.io/en/latest/

AWX Operator Helm Chart Repo: https://github.com/ansible/awx-operator



