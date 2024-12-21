# 🏠 Home Lab Setup

Welcome to my **Home Lab Setup** repository! 🚀 This project documents the configurations, setups, and optimizations I’ve implemented to create an efficient, flexible, and scalable home lab environment. 

## 📂 Folder Structure

```
home-lab-setup/ 
├── docs/          # Documentation and guides
├── config/        # Configuration files for systems and VMs
├── scripts/       # Automation and utility scripts
├── iso-storage/   # ISO files for operating systems
├── vm-storage/    # Virtual Machine files and disk images
└── backup/        # Backup files and configurations
```

## 🛠️ Features
- **Multi-Partition Setup**: Organized storage for VMs, ISOs, and backups. 🗂️
- **Automated Mounting**: Configured `/etc/fstab` for seamless partition management. 🖥️
- **VM Support**: Optimized storage for running virtual machines with KVM and VirtualBox. 🖧
- **Documentation**: Step-by-step guides to recreate and expand the setup. 📘

## 📖 Documentation
Detailed documentation is available in the `docs/` folder, including:
- [Partitioning and Mounting](docs/partitioning_and_setup.md)
- [Virtual Machine Configurations](docs/vm_configurations.md)
- [Backup Strategies](docs/backup_strategies.md)

## Table of Contents
1. Overview  
2. System Requirements  
3. Key Features  
4. Directory Structure  
5. Setup Guide  
6. Scripts and Automation  
7. VM Configurations  
8. Future Roadmap  
9. Contributing  
10. License  

---

### 1. Overview
This project outlines my personal journey in setting up and configuring a home lab environment optimized for virtualization, networking, and system administration practice. It is designed to:

- Simulate enterprise-level IT systems for hands-on learning.
- Test various technologies such as Linux, Virtual Machines, KVM, and VirtualBox.
- Optimize resources for storage, virtualization, and data processing.

### 2. System Requirements

**Hardware:**  
- Desktop: Dell OptiPlex 3050  
- CPU: Intel i5  
- RAM: 16 GB (Expandable as needed)  

**Storage:**  
- 256GB SSD - Primary OS Drive  
- 500GB HDD - VM Storage  
- 1TB NVMe SSD - High-performance VM and data transfers  

**Software:**  
- Primary OS: Ubuntu Linux  
- Virtualization Tools:  
  - KVM/QEMU  
  - VirtualBox  
- Monitoring Tools:  
  - htop, netstat, vnstat  

---

### 3. Key Features
- **Multi-Disk Storage Configuration:** OS, VM storage, and backup disks are separated for performance optimization.  
- **VM Setup for Networking Practice:** Virtual Machines preconfigured for testing server setups, networking configurations, and media station deployment.  
- **Automation Scripts:** Shell scripts for simplifying tasks like disk partitioning, mounting, and software installations.  
- **Scalable Architecture:** Supports adding more virtual machines and disks as the lab grows.  
- **Focus on Documentation:** Guides and scripts ensure repeatability for future projects.  

---

### 4. Directory Structure
```
├── docs/                  # Documentation and setup guides  
├── config/                # Configuration files for VMs, networking, and services  
├── scripts/               # Automation scripts for system setup and maintenance  
├── iso/                   # ISO storage for OS and VM images  
├── backups/               # Backup strategies and files  
├── examples/              # Example setups for VMs and network configurations  
├── logs/                  # Log management and scripts  
└── README.md              # Project overview and usage instructions  
```

---

### 5. Setup Guide

**Step 1: Preparing the System**
1. Install Ubuntu on the 256GB SSD.
2. Partition and mount the HDD and NVMe SSD for storage and VMs.
3. Configure the BIOS settings to enable Virtualization Technology (VT-x).

**Step 2: Install Virtualization Tools**
```bash
sudo apt update && sudo apt install qemu-kvm libvirt-daemon-system virt-manager bridge-utils
```

**Step 3: Create Virtual Machines**
- Use KVM or VirtualBox for creating VMs.
- Refer to the VM Configurations section for examples.

---

### 6. Scripts and Automation

**Examples:**
- **Partition and Mount Disks:**
```bash
sudo bash scripts/partition_disks.sh
```

- **Create a Virtual Machine Template:**
```bash
sudo bash scripts/create_vm_template.sh --name ubuntu-template
```

For more scripts, check the `scripts/` directory.

---

### 7. VM Configurations
The repository includes configuration files for prebuilt VMs optimized for specific tasks:
- **Ubuntu Server VM** - For hosting services.
- **Networking VM** - For routing and firewall testing.
- **Media Server VM** - For multimedia storage and streaming.

Each configuration comes with networking and storage options pre-defined.

---

### 8. Future Roadmap

Planned updates and expansions:
- **Active Directory (AD) Setup and Integration:**
  - Simulate domain controllers for user authentication, group policy management, and centralized administration.
  - Explore both Windows Server and Samba AD DC options.
- **Docker Support:**
  - Integrating Docker containers alongside VMs for flexible deployments.
- **Proxmox VE Implementation:**
  - Exploring alternative hypervisors.
- **Monitoring Tools:**
  - Adding Grafana and Prometheus dashboards for system monitoring.
- **Home Media Station:**
  - Finalizing setup for Plex or Jellyfin for multimedia management.

---

### 9. Contributing🤝

Contributions are welcome!

**How to Contribute:**
1. Fork the repository.
2. Create a feature branch:
```bash
git checkout -b feature-name
```
3. Commit your changes:
```bash
git commit -m "Add new feature or fix bug"  
```
4. Push to your branch and create a pull request.

---

## 🧑‍💻 About Me
I'm an aspiring systems administrator and IT support specialist with a passion for learning and building hands-on projects. Follow my journey as I optimize and expand my home lab! 🌟

## 📬 Contact
For questions or suggestions, please reach out via GitHub Issues or connect with me on [LinkedIn](https://www.linkedin.com/in/troy-edmonds/).
