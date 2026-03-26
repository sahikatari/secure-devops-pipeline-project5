# 🚀 Secure-Devops-Pipeline-Project5 

## 📌 Project Title
CI/CD Pipeline with Automated Docker Security Scanning and Deployment to Kubernetes

---

## 🧩 Scenario

As a DevOps Engineer, the security team identified vulnerabilities in production containers.  

The CTO mandated:

> "Before any Docker image goes to production, it must be scanned for vulnerabilities. Automate security scanning inside the CI/CD pipeline."

---

## 🎯 Objective

Design a **secure CI/CD pipeline** where:

- Application is containerized using Docker
- Docker image is scanned for vulnerabilities
- Build fails if **HIGH/CRITICAL vulnerabilities** are found
- Only **secure images** are deployed to Kubernetes

---

## 📁 Project Structure
- Dockerfile 
- Jenkinsfile 
- app
- requirements.txt 
- k8s/ 
   - deployment.yaml
   - service.yaml 
- scan-report.txt 
- README.md

## 🛠️ Technologies Used
- Docker
- Jenkins
- Kubernetes
- Trivy
- GitHub 

## ⚙️ Setup Instructions (t3.small)
 🐳 1.  Install Docker
 ```bash
sudo apt update
sudo apt install -y docker.io
sudo usermod -aG docker ubuntu
newgrp docker
```
⚙️ 2. Install Jenkins
```bash
sudo apt update && sudo apt upgrade -y
```
```bash
sudo apt install -y openjdk-17-jdk
```
```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
/usr/share/keyrings/jenkins-keyring.asc > /dev/null
```
```
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null
```
```bash
sudo apt update
sudo apt install -y jenkins
sudo systemctl status jenkins
```
  - 👉 Open:
http://EC2-IP:8080

🔐 3. Install Trivy (Security Scanner)

```bash
sudo apt install -y wget apt-transport-https gnupg lsb-release

```
```bash
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
```
```bash
echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee /etc/apt/sources.list.d/trivy.list
```
```bash
sudo apt update
sudo apt install -y trivy
```
☸️ 4. Install K3s (Lightweight Kubernetes)
```bash
curl -sfL https://get.k3s.io | sh -
```
```bash
sudo systemctl status k3s
```
```bash
sudo kubectl get nodes
```
## 🔗 5. Important Integrations
Allow Jenkins to use Docker & Jenkins to use kubectl
```bash
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
sudo chmod 644 /etc/rancher/k3s/k3s.yaml
export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
echo "export KUBECONFIG=/etc/rancher/k3s/k3s.yaml" >> ~/.bashrc
```
## ⚙️  Jenkins Setup
Install plugins:
- Git
- Pipeline
- Docker Pipeline

## 🔗  Connect GitHub
In Jenkins:
- New Item → Pipeline
- Pipeline script from SCM
- Add your GitHub repo URL

## ✅ Final Verification
```bash
docker ps
jenkins --version
trivy --version
kubectl get nodes
```
## 🔐 Security Implementation
- Trivy scans Docker images
- Detects HIGH and CRITICAL vulnerabilities
- Pipeline fails if vulnerabilities found
- Prevents insecure deployments

 ## 🧪 Security Testing
 - Vulnerable dependency used:
  ```bash
   flask
```
### Output Example:
- CRITICAL: 2
- HIGH: 5
- BUILD FAILED


## 🚀 Push Code to GitHub (Step-by-Step after creating files)
```bash
git init
git add .
git commit -m "Initial commit - CI/CD pipeline project"
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin master
```
## ✅ Final Result
- Automated CI/CD pipeline
- Security integrated
- Deployment blocked on vulnerabilities
- Runs on AWS Free Tier




