# 🐍 Python for DevOps — Learning Roadmap

I want to learn enough Python to use it as a **tool for DevOps automation** — working with Linux, servers, APIs, Docker, cloud and Kubernetes.

---

## 1. Python Basics

### What to learn

* Variables and basic data types
* Lists, dictionaries, tuples and sets
* `if` statements
* `for` and `while` loops
* Functions
* Imports and modules
* List comprehensions
* Error handling with `try / except`
* Basic classes and objects

### I should be able to

Write a simple script that takes some data, processes it and gives me a useful result.

```python
servers = ["web01", "web02", "db01"]

for server in servers:
    print(f"Checking {server}")
```

---

## 2. Python + Linux 

I want to be able to use Python to interact with the Linux system and run commands automatically.

### What to learn

* Working with files and directories
* Environment variables
* Processes
* Exit codes
* File permissions
* System information
* Running Linux commands with `subprocess`
* Working with paths using `pathlib`

For example:

```python
import subprocess

result = subprocess.run(
    ["docker", "ps"],
    capture_output=True,
    text=True
)

print(result.stdout)
```

### Project

Create a **Server Health Checker** that checks:

```text
CPU
RAM
Disk
Docker
Running services
Uptime
```

---

## 3. Files, Logs and Configuration

Need to learn how to read them, modify them and extract useful information.

### What to learn

* Reading and writing files
* `pathlib`
* JSON
* YAML
* CSV
* Regular expressions
* Environment variables
* Basic log parsing

For example:

```text
Total requests: 1520
Errors: 32
404 errors: 71
500 errors: 4
```

### Project

Build a **Log Analyzer** that reads a log file and creates a simple report.

---

## 4. APIs and HTTP 

Need to understand how HTTP and REST APIs work and how to use them from Python.

### What to learn

* GET
* POST
* PUT
* PATCH
* DELETE
* HTTP status codes
* Headers
* Authentication
* JSON
* REST APIs

The main Python library to start with is:

```python
requests
```

For example:

```python
import requests

response = requests.get("https://example.com/api/servers")

data = response.json()
```

### Project

Build a small **API monitoring script** that checks a service and tells me whether it is working.

---

## 5. Python CLI Tools

Instead of writing scripts that only work in one specific situation, I want to learn how to create useful command-line tools.

Start with:

```python
argparse
```

Eventually, I should be able to run something like:

```bash
python server.py check
python server.py disk
python server.py docker
python server.py logs
```

### Project

Build a **Server Management CLI** that combines some of the things learned in previous sections.

---

## 6. SSH and Remote Automation

Python can connect to remote machines and execute commands.

### What to learn

* SSH
* SSH keys
* Remote commands
* SCP / SFTP
* Connection errors
* Timeouts

Useful libraries:

```text
Paramiko
Fabric
```

### Project

Create a script that connects to several servers and checks their:

```text
CPU
RAM
Disk
Docker
Services
```

Then display everything in one report.

---

## 7. Python + Docker 

Since Docker is an important part of DevOps, I want to be able to control Docker using Python.

### What to learn

* Dockerfiles
* Python containers
* Environment variables
* Volumes
* Networks
* Docker Compose
* Docker API / SDK

For example, Python could check which containers are running and restart one if necessary.

### Project

Build a **Docker Manager**:

```bash
python docker.py list
python docker.py start nginx
python docker.py stop nginx
python docker.py restart nginx
python docker.py logs nginx
```

---

## 8. Logging and Error Handling

My scripts should not just work when everything is perfect. They should also handle problems properly.

Instead of using only:

```python
print("Something went wrong")
```

I should learn Python's `logging` module.

### What to learn

* Log levels
* `logging`
* Exceptions
* Retries
* Timeouts
* Exit codes

For example:

```python
logging.info("Server is running")
logging.warning("Disk usage is high")
logging.error("Connection failed")
```

This is especially important for scripts that will run automatically.

---

## 9. Testing

I should know how to make sure my automation actually works.

### What to learn

* Basic unit tests
* `pytest`
* Fixtures
* Mocking
* Testing errors

For example:

```python
def test_check_server():
    assert check_server("web01") == "OK"
```

---

## 10. Python + Cloud ☁️

Once I am comfortable with Python and basic DevOps tools, I can start using Python with cloud platforms.

I would start with **AWS**.

### What to learn

* EC2
* S3
* IAM
* VPC
* Security Groups
* CloudWatch
* AWS APIs

The main Python library is:

```text
boto3
```

### Project

Build an **AWS Instance Manager**:

```bash
python aws.py list
python aws.py start web01
python aws.py stop web01
```

The goal is to automate things that I would normally have to do manually.

---

## 11. Python + Terraform and Ansible

I should **learn Terraform and Ansible themselves first**.

For Terraform:

```text
HCL
Providers
Resources
Variables
Outputs
State
Modules
```

For Ansible:

```text
Inventory
Playbooks
Tasks
Variables
Handlers
Roles
```

After I understand these tools, I can use Python to automate or integrate them into larger workflows.

Python shouldn't replace Terraform or Ansible. It should **work alongside them**.

---

## 12. Python + Kubernetes 

Only after learning the basics of Kubernetes should I start using Python with it.

### What to understand first

* Pods
* Deployments
* Services
* Namespaces
* ConfigMaps
* Secrets
* Jobs
* RBAC

Then I can learn the Kubernetes Python client and use Python to communicate directly with the Kubernetes API.

### Project

Build a small Kubernetes CLI:

```bash
python k8s.py pods
python k8s.py deployments
python k8s.py namespaces
python k8s.py restart nginx
```

---

## 13. Monitoring and Security

Python can also help with monitoring and security automation.

### Monitoring

I should understand the basics of:

* Prometheus
* Grafana
* Metrics
* Logs
* Alerts

For example, a Python script could detect:

```text
CPU > 90%
RAM > 90%
Disk > 85%
Container is down
Pod is crashing
```

and generate an alert.

### Security

Later, I can use Python for things like:

* Checking permissions
* Checking Kubernetes RBAC
* Finding configuration problems
* Container security scanning
* Working with CVE data

---

## 14. More Advanced Python

I can start learning more advanced Python features.

### Useful topics

* Type hints
* `dataclasses`
* Decorators
* Generators
* Context managers
* `asyncio`
* Threading
* Multiprocessing
* Python packaging
* `pyproject.toml`

These are useful, but **they are not the priority at the beginning**.

---

## 15. AI + Python 🤖

AI should come later.

Once I have solid DevOps fundamentals, I can use Python to work with:

* LLM APIs
* Log analysis
* AI-assisted troubleshooting
* AI automation
* RAG
* AI agents

For example:

```text
Kubernetes logs
       ↓
     Python
       ↓
      AI
       ↓
Possible cause + suggested solution
```

AI is an additional skill. It should not replace learning Linux, networking, Docker, Kubernetes or automation.

---

# 🎯 What I Should Focus On

The most important part of this roadmap is the order:

```text
Python Basics
      ↓
Python + Linux
      ↓
Files + Logs + JSON + YAML
      ↓
APIs + HTTP
      ↓
CLI Tools
      ↓
SSH Automation
      ↓
Docker + Python
      ↓
Logging + Error Handling
      ↓
Testing
      ↓
Cloud
      ↓
Terraform + Ansible
      ↓
Kubernetes
      ↓
Monitoring + Security
      ↓
Advanced Python
      ↓
AI
```

I don't need to master every topic before moving on. The best approach is to **learn something, build something with it, and then move to the next topic**.

---

# 🏴‍☠️ Projects

I want to build projects alongside the roadmap:

### 1. Server Health Checker

Python + Linux

### 2. Log Analyzer

Python + Files + Regex

### 3. API Monitor

Python + HTTP + REST API

### 4. Remote Server Manager

Python + SSH

### 5. Docker Manager

Python + Docker

### 6. AWS Manager

Python + AWS

### 7. Kubernetes Manager

Python + Kubernetes API

### 8. DevOps Toolkit

Finally, combine everything into one CLI tool:

```bash
devops-tool server check
devops-tool docker ps
devops-tool docker logs nginx
devops-tool k8s pods
devops-tool aws instances
devops-tool logs analyze
```

The final goal is not simply to say **"I know Python."**

The goal is to be able to say:

> **"I can use Python to automate DevOps tasks, work with Linux servers, APIs, Docker, cloud infrastructure and Kubernetes."**
>
