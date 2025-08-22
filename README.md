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
| `terminate` | Terminate an EC2 instance (by ID)      | Removes the instance and frees a slot under the cap.                                   |

**Consistent tagging applied to every instance:**
CreatedBy = Ben-cli
Owner = Ben Elbaz
Project = Python-Project
Environment = dev

yaml
Copy
Edit

---

## 📋 Requirements

- Active **AWS account**
- IAM role or AWS profile with EC2 permissions
- **Python 3.7+**
- `pip` installed
- AWS CLI configured:
  ```bash
  aws configure
  # or
  export AWS_PROFILE=myprofile
## ⚙️ Installation

Clone this repository:
```bash
git clone https://github.com/benelbaz82/ben-awscli.git
cd ben-awscli
Install dependencies:

bash
Copy
Edit
pip install -r requirements.txt
Make the CLI executable and place it in your PATH:

bash
Copy
Edit
chmod +x ben-awscli
mv ben-awscli ~/.local/bin/
▶️ Usage
Create a new instance

bash
Copy
Edit
ben-awscli create MyInstance
List instances created by this CLI

bash
Copy
Edit
ben-awscli list
Stop an instance (by ID)

bash
Copy
Edit
ben-awscli stop i-0123456789abcdef0
Start an instance (by ID)

bash
Copy
Edit
ben-awscli start i-0123456789abcdef0
