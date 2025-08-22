# 🐧 Ben's AWS CLI

A lightweight, developer-friendly CLI tool for managing AWS EC2 instances using Python, `boto3`, and `click`.  
This tool allows developers to create, start, stop, and list EC2 instances while enforcing safe, standardized practices.

---

## 🚀 Features

| Command     | Description                            | Behavior & Constraints                                                                 |
|-------------|----------------------------------------|----------------------------------------------------------------------------------------|
| `create`    | Provision a new EC2 instance           | Allowed types: `t3.micro`, `t2.small`. Max 2 non-terminated instances created by this CLI. |
| `list`      | List EC2 instances created by this CLI | Shows non-terminated instances tagged by the CLI.                                      |
| `stop`      | Stop a running EC2 instance (by ID)    | Only instances tagged with `CreatedBy=Ben-cli`.                                        |
| `start`     | Start a stopped EC2 instance (by ID)   | Same tagging constraints as above.                                                     |

---

## 📋 Requirements

- Active **AWS account**
- IAM role or AWS profile with EC2 permissions
- AWS CLI configured:
  ```bash
  aws configure
  ```
## ⚙️ Installation

Clone this repository:
```bash
git clone https://github.com/benelbaz82/ben-awscli.git
cd ben-awscli
```
Install dependencies:
```bash
pip install -r requirements.txt
```
Make the CLI executable and place it in your PATH:

```bash
chmod +x ben-awscli
mv ben-awscli ~/.local/bin/
```
## ▶️ Usage

Create a new instance

```bash
ben-awscli create MyInstance
```
List instances created by this CLI

```bash
ben-awscli list
```
Stop an instance (by ID)

```bash
ben-awscli stop {Instance ID}
```
Start an instance (by ID)

```bash
ben-awscli start {Instance ID}
```
