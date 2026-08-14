# 🏠 My Homelab

My personal homelab is a small environment where I experiment with **Linux, Docker, networking, automation and DevOps**.

The goal is to learn by building, breaking, fixing and documenting real systems.

---

## 🖥️ Mini PC

**Main purpose:** Docker, automation & learning


| Component   | Specification                              |
| ----------- | ------------------------------------------ |
| **CPU**     | Intel Core i3-6100T                        |
| **RAM**     | 10 GB DDR3L SO-DIMM 1600 MHz (8 GB + 2 GB) |
| **GPU**     | Intel HD Graphics 530                      |
| **Storage** | 256 GB SATA SSD                            |
| **OS**      | Linux                                      |

### Main services

- 🐳 Docker
- ⚙️ Automation
- 🧪 DevOps experiments
- 📚 Learning environment
- 🔧 Self-hosted tools

The Mini PC is my main **lab machine**. I use it to experiment with Docker, Linux services, automation and different DevOps concepts without affecting my main storage server.

### Planned upgrades

- ⬆️ Upgrade RAM to **16 GB (2 × 8 GB DDR3L)**
- ⬆️ Possible CPU upgrade in the future

---

## 🗄️ HomeServer

**Main purpose:** Storage & media


| Component        | Specification              |
| ---------------- | -------------------------- |
| **CPU**          | Intel Core i5              |
| **RAM**          | 12 GB DDR3                 |
| **GPU**          | NVIDIA GeForce GT 720      |
| **Storage**      | 2 × 1 TB HDD + 500 GB HDD |
| **System Drive** | 120 GB SSD                 |
| **OS**           | TrueNAS                    |

### Main services

- 🎬 **Jellyfin** — media server
- 📸 **Immich** — photo & video backup
- 💾 Network storage

This machine is focused on **storage and media services**. It handles my personal data while the Mini PC is used primarily for experimentation and learning.

---

## 💻 Main Laptop

**Main purpose:** Development & administration


| Component   | Specification          |
| ----------- | ---------------------- |
| **Model**   | ASUS Zenbook UX3402ZA  |
| **CPU**     | Intel Core i5-1240P    |
| **GPU**     | Intel Iris Xe Graphics |
| **RAM**     | 16 GB DDR5             |
| **Storage** | 512 GB NVMe SSD        |
| **Display** | 14" 1920×1200         |
| **OS**      | Ubuntu 26.04 LTS       |
| **Desktop** | GNOME 50.1             |
| **Kernel**  | Linux 7.0.29-generic   |

### Main uses

- 👨‍💻 Programming
- 🐧 Linux administration
- 🐳 Docker & Docker Compose
- ☁️ DevOps / Cloud learning
- 🔐 Server administration
- 📝 Documentation
- 🛠️ Homelab management

This is my primary workstation for development, learning and managing the homelab.

---

## 🌐 Homelab Overview

```text
                         ┌─────────────────────────┐
                         │      Main Laptop        │
                         │                         │
                         │  i5-1240P               │
                         │  16 GB DDR5             │
                         │  512 GB NVMe            │
                         │  Ubuntu 26.04 LTS       │
                         │                         │
                         │  Development            │
                         │  Linux / DevOps         │
                         │  Administration         │
                         └────────────┬────────────┘
                                      │
                                      │ Network
                                      │
                    ┌─────────────────┴─────────────────┐
                    │                                   │
                    ▼                                   ▼
       ┌─────────────────────────┐        ┌─────────────────────────┐
       │        Mini PC          │        │       HomeServer        │
       │                         │        │                         │
       │  i3-6100T               │        │  Intel Core i5          │
       │  10 GB RAM              │        │  12 GB RAM              │
       │  256 GB SSD             │        │  120 GB SSD             │
       │                         │        │  2 × 1 TB HDD + 500 GB  │
       │  Docker                 │        │                         │
       │  Automation             │        │  TrueNAS                │
       │  DevOps Lab             │        │  Jellyfin               │
       │  Self-hosted Services   │        │  Immich                  │
       └─────────────────────────┘        │  Storage                 │
                                          └─────────────────────────┘
```

---

## 🎯 Why I Built It

This homelab is part of my journey into **DevOps and Cloud Engineering**.

Instead of learning everything only through courses and tutorials, I want to build and manage real infrastructure.

Things I practice in my homelab:

- 🐧 Linux
- 🐚 Bash & Python automation
- 🐳 Docker
- 📦 Docker Compose
- 🌐 Networking
- 🔎 DNS
- 🔀 Reverse proxies
- 🏠 Self-hosting
- 📊 Monitoring
- 🔀 Git & GitHub
- 🔄 CI/CD
- 🏗️ Infrastructure as Code
- 🔐 Server administration
- 🛠️ Troubleshooting

The hardware isn't powerful — and that's intentional.
