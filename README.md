# 🚀 Ansible Automation Playbooks

This repository contains a collection of **Ansible playbooks** designed to automate common system administration and DevOps tasks such as **Docker installation, Nginx setup, and user management**.

---

## 📌 Project Overview

The goal of this project is to demonstrate **infrastructure automation using Ansible**, reducing manual configuration effort and ensuring consistency across servers.

---

## 📂 Repository Structure

```
ansible-playbooks/
│── docker/
│   ├── install_docker.yml
│   └── README.md
│
│── nginx/
│   ├── install_nginx.yml
│   └── README.md
│
│── user_management/
│   └── user_management.yml
    └── README.md

```

---

## ⚙️ Tech Stack

- 🔧 Ansible (Configuration Management)
- 🐳 Docker (Containerization)
- 🌐 Nginx (Web Server)
- 🐧 Linux (Target Environment)
- 📜 YAML (Playbook scripting)

---

## 🚀 Features

✅ Automated Docker installation  
✅ Automated Nginx setup and configuration  
✅ User creation and management using Ansible  
✅ Idempotent playbooks (safe to run multiple times)  
✅ Modular and reusable structure  

---

## ▶️ How to Use

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/ajay-mall13/ansible-playbooks.git
cd ansible-playbooks
```

### 2️⃣ Configure Inventory
Create or edit your inventory file:
```ini
[servers]
your-server-ip
```

### 3️⃣ Run Playbooks

#### 🔹 Install Docker
```bash
ansible-playbook docker/install_docker.yml -i inventory
```

#### 🔹 Install Nginx
```bash
ansible-playbook nginx/install_nginx.yml -i inventory
```

#### 🔹 User Management
```bash
ansible-playbook user_management/user_management.yml -i inventory
```

---

## 🔐 Prerequisites

- Ansible installed on control node
- SSH access to target servers
- Sudo privileges on target machines

---

## 💡 Future Improvements

- 🔁 Integrate with CI/CD (Jenkins / GitHub Actions)
- ☁️ Deploy on AWS/GCP using Terraform
- 📊 Add monitoring (Prometheus + Grafana)
- 🔐 Enhance security automation (firewall, SSH hardening)

---

## 👨‍💻 Author

**Ajay Mohan**  
B.Tech ECE | Cloud & DevOps Enthusiast  
Google Cloud Certified Associate Cloud Engineer  

---

## ⭐ Contribute

Feel free to fork this repo, raise issues, or submit pull requests to improve the project.

---

## 📜 License

This project is open-source and available under the MIT License.
