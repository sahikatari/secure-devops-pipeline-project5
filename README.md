# 🚀 Secure-Devops-Pipeline-Project5 

## 📌 Project Title
CI/CD Pipeline with Automated Docker Security Scanning and Deployment to Kubernetes

---

# 🔄 CI/CD Pipeline Workflow

Developer → GitHub → Jenkins → Docker → Trivy → Kubernetes

- Code pushed to GitHub  
- Jenkins pipeline triggered  
- Docker image built  
- Image pushed to Docker Hub  
- Trivy scans image  
- ❌ If vulnerabilities → Pipeline FAIL  
- ✅ If secure → Deploy to Kubernetes  

---

# 🛠️ Technologies Used

- Docker  
- Jenkins  
- Kubernetes (Minikube)  
- Trivy  
- GitHub  

---

# ☁️ AWS EC2 Setup

## 🔹 Launch EC2 Instance

- Go to AWS Console  
- Open EC2 Dashboard  
- Click **Launch Instance**

### Configure:
- AMI: Ubuntu  
- Instance Type: t3.small  
- Key Pair: Create or select existing  

---

# 💾 EC2 Disk Storage & Volume Expansion

## 📈 Step 1: Increase Volume in AWS Console

- Go to **AWS EC2 Dashboard**
- Navigate to **Elastic Block Store → Volumes**
- Select your volume
- Click **Modify Volume**
- Increase size (e.g., 19GB → 30GB)
- Click **Modify**

---

## 🔧 Step 2: Extend Partition in Linux

```bash
sudo growpart /dev/nvme0n1 1
```

---

## 🔧 Step 3: Resize File System

```bash
sudo resize2fs /dev/root
```

---

## 🔍 Step 4: Verify Updated Size

```bash
df -h
```

---

# ⚙️ Installation Commands

## 🐳 Docker Installation

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
docker --version
```

---

## 🔧 Jenkins Installation (Using Docker)

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
java --version

sudo docker pull jenkins/jenkins:lts

docker run -d -p 8080:8080 -p 50000:50000 --name jenkins jenkins/jenkins:lts
```

---

## 🔐 Trivy Installation

```bash
sudo apt install wget apt-transport-https gnupg lsb-release -y

wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -

echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | \
sudo tee /etc/apt/sources.list.d/trivy.list

sudo apt update
sudo apt install trivy -y

trivy --version
```

---

## ☸️ Minikube Installation

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

minikube start
```

---

## 📦 kubectl Installation

```bash
sudo apt install -y kubectl
kubectl version --client
```

---

# 📁 Project Structure

```
DevOps-project-CI-CD/

├── myapp/
│   ├── Dockerfile
│   ├── Jenkinsfile
│   ├── trivy-report.txt
│   ├── docker_build_log.txt
│   ├── package.json
│   ├── service.js
│   ├── app.js
│   └── kubernetes/
│       ├── deployment.yaml
│       └── service.yaml
│
├── Screenshots/
│  
│   ├── Docker_container_status.png
│   ├── Dockerhub_image_pushed.png
│   ├── EC2_instance.png
│   ├── Jenkins_Pipeline_Success.png
│   ├── Kubernetes_Pods_and_Service_Running.png
│   ├── Pipeline_Failed_Due_To_Trivy_Scan.png
│   ├── Security_group_add.png
│   └── Trivy_Vulnerability_Report.png
│
└── README.md
```

---

# 🐳 Push Docker Image to Docker Hub

## 🔹 Login

```bash
docker login
```

## 🔹 Build Image

```bash
docker build -t sahikatari/secure-app:latest .
```

## 🔹 Push Image

```bash
 docker push sahikatari/secure-app:latest
```

## 🔹 Verify

- Go to Docker Hub  
- Check repository  
- Image should be visible  

---

# ☸️ Kubernetes Deployment

## 🔹 Deploy Application

```bash
kubectl apply -f /kubernetes/deployment.yaml
kubectl apply -f /kubernetes/service.yaml
```

## 🔹 Check Pods

```bash
kubectl get pods
```

## 🔹 Check Services

```bash
kubectl get svc
```

## 🔹 Access Application

```bash
minikube service <service-name>
```

## 🔹 Expected Output

- Pods: Running  
- Service: Active  
- App accessible in browser  

---

# 🔐 Trivy Security Scan

## 🔹 Scan Image

```bash
trivy image your-dockerhub-username/secure-app:latest
```

## 🔹 Save Report (TXT)

```bash
trivy image -f table -o trivy-report.txt your-dockerhub-username/secure-app:latest
```

## 🔹 Save Report (JSON)

```bash
trivy image -f json -o trivy-report.json your-dockerhub-username/secure-app:latest
```

## 🔹 Expected Output

- Vulnerabilities (LOW, MEDIUM, HIGH, CRITICAL)  
- Summary report  
- Fix suggestions  

## 🔹 Pipeline Behavior

- ❌ HIGH/CRITICAL → Pipeline FAIL  
- ✅ No critical issues → Deployment allowed  

---

# 🔄 Jenkins Pipeline

## 🔹 Pipeline Flow

- Code pushed to GitHub  
- Jenkins triggers pipeline  
- Pipeline executes stages  

## 🔹 Stages

- 📥 Clone Code  
- 🐳 Build Docker Image  
- 📤 Push Image  
- 🔐 Trivy Scan  
- 🚀 Run Container  
- ☸️ Deploy to Kubernetes  

## 🔹 Run Pipeline

- Open Jenkins Dashboard  
- Select pipeline job  
- Click **Build Now**  
- View **Console Output**

## 🔹 Result

- ✅ Success → App deployed  
- ❌ Fail → Security issues detected  

---

# 🔐 Security Implementation

- ✔️ Trivy vulnerability scanning  
- ✔️ Automated security gating  
- ✔️ Secure container deployment  
- ✔️ CI/CD integrated security checks  

---
