# minkube-installation
Installation of minikube and kubectl

# 🚀 Kubernetes on Minikube (Windows + Docker Desktop)

This README provides complete steps to set up **kubectl** and **Minikube** on Windows, deploy an **nginx pod**, expose it as a service, and access it in the browser.  

---

## 🔧 Setup & Deployment Steps

```bash
# --- Install kubectl ---
curl.exe -LO "https://dl.k8s.io/release/v1.33.0/bin/windows/amd64/kubectl.exe"
mv kubectl.exe C:\Windows\System32
kubectl version --client

# --- Install Minikube ---
curl.exe -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe
mv minikube-windows-amd64.exe C:\Windows\System32\minikube.exe
minikube version

# --- Start Minikube with Docker driver ---
minikube start --driver=docker
kubectl get nodes --show-labels

# --- Create nginx Pod (pod.yml) ---
cat > pod.yml <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
EOF

# --- Deploy pod ---
kubectl apply -f pod.yml
kubectl get pods -o wide

# --- View logs ---
kubectl logs nginx

# --- Expose nginx service ---
kubectl expose pod nginx --type=NodePort --port=80
kubectl get svc

# --- Open nginx in browser ---
minikube service nginx

# --- Useful commands ---
minikube stop
minikube delete
minikube ssh

