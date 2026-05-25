# Docker-PythonAPI-MySQL-Kubernetes
simple, Kubernetes‑ready version of Python API + MySQL Docker project

**1. You moved from Docker Compose → Kubernetes**
Instead of one docker-compose.yml, Kubernetes uses multiple YAML files.

Each file describes one resource (Deployment, Service, PVC, etc.).

**2. Everything runs inside a Namespace**
A namespace called myproject keeps your API and MySQL grouped together.

**3. MySQL needs three things**
A Deployment → runs the MySQL container

A Service → gives MySQL a stable internal name (mysql)

A PersistentVolumeClaim (PVC) → stores database files permanently

**4. MySQL initialization uses a ConfigMap**
The init.sql file is stored in a ConfigMap.

Kubernetes loads it into MySQL at startup.

**5. The API also has two things**
A Deployment → runs your Python FastAPI container

A Service → exposes the API to the outside world

**6. API talks to MySQL using the service name**
Inside Kubernetes, the API connects to MySQL using:

Code
host = "mysql"
Kubernetes DNS resolves this automatically.

**7. API image must be pushed to a registry**
Kubernetes cannot build images.

You must push your API image (e.g., username/myapp:latest) to Docker Hub or another registry.

**8. You deploy everything with one command**
Code
kubectl apply -f k8s/
**9. You access the API using NodePort**
The API Service exposes port 30080.

You open:

Code
http://localhost:30080
