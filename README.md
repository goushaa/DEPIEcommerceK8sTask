# Kubernetes Deployment for E-commerce Application

## Overview

This repository contains Kubernetes configuration files for deploying an e-commerce application using Minikube. The deployment includes a MySQL database, a Python Flask backend, and an Nginx frontend, all managed within the `ecommerce` namespace. The setup includes Ingress configuration to route external traffic.

## Components

1. **MySQL Database**
   - **Image**: `mysql:5.7`
   - **Deployment**: Managed by a StatefulSet.
   - **Service**: Exposed internally as `mysql-service`.
   - **Secret**: Managed with `mysql-secret.yaml` to store credentials.

2. **Backend**
   - **Image**: `tiangolo/uwsgi-nginx-flask:python3.8`
   - **Deployment**: Flask application deployed with 2 replicas.
   - **Service**: Exposed internally as `flask-service.yaml`.
   - **ConfigMap**: `flask-config.yaml` for storing non-sensitive environment variables.

3. **Frontend**
   - **Image**: `nginx:latest`
   - **Deployment**: Nginx web server deployed with 2 replicas.
   - **Service**: Exposed internally as `nginx-service.yaml`.

4. **Ingress**
   - **Resource**: Configured to route external traffic to the `nginx-service.yaml` based on the `/` path.
   - **Configuration**: Defined in `nginx-ingress.yaml`.

## Instructions

### Prerequisites

- Minikube installed and running.
- `kubectl` configured to use your Minikube cluster.

### Deploy the Resources

1. **Create the `ecommerce` Namespace**

   ```bash
   kubectl apply -f ecommerceNamespace.yaml
   ``` 

2. **Deploy `MySQL`**

   ```bash
    kubectl apply -f mysql.yaml
    kubectl apply -f mysql-service.yaml
    kubectl apply -f mysql-secret.yaml
   ```    

3. **Deploy the `Flask` Backend**

   ```bash
    kubectl apply -f flask-config.yaml
    kubectl apply -f flask.yaml
    kubectl apply -f flask-service.yaml
   ``` 

4. **Deploy the `Nginx` Frontend**

   ```bash
    kubectl apply -f nginx.yaml
    kubectl apply -f nginx-service.yaml
   ``` 

5. **Configure `Ingress`**

   ```bash
    kubectl apply -f nginx-ingress.yaml
   ``` 

6. **Verify the `Deployment`**

- **Check Pods:**

```bash
kubectl get pods -n ecommerce
```

- **Check Services:**

```bash
kubectl get services -n ecommerce
```

- **Check Ingress:**

```bash
kubectl get ingress -n ecommerce
```

### Accessing the Application

- **Frontend URL**: `http://kady.com/` or `http://<minikube-ip>.nip.io/` (if using Minikube IP for testing).

### Configuration Files

- **Namespace**: `ecommerceNamespace.yaml`
- **MySQL Deployment**: `mysql.yaml`
- **MySQL Service**: `mysql-service.yaml`
- **MySQL Secret**: `mysql-secret.yaml`
- **Flask ConfigMap**: `flask-config.yaml`
- **Flask Deployment**: `flask.yaml`
- **Flask Service**: `flask-service.yaml`
- **Nginx Deployment**: `nginx.yaml`
- **Nginx Service**: `nginx-service.yaml`
- **Ingress**: `nginx-ingress.yaml`

### Notes

- **Ensure the Ingress addon is enabled in Minikube:**

  ```bash
  minikube addons enable ingress
  ```
- **Update your `/etc/hosts` file for local testing if using a custom domain.**


   # DEPIEcommerceK8sTask
