# 🐧 Ben's AWS CLI

A lightweight, developer-friendly CLI tool for managing AWS EC2 instances using Python, `boto3`, and `click`.  
This tool allows developers to create, start, stop, and list EC2 instances while enforcing safe, standardized practices.

---

## 🚀 Features

### EC2

| Command     | Description                            | Behavior & Constraints                                                                 |
|-------------|----------------------------------------|----------------------------------------------------------------------------------------|
| `create`    | Provision a new EC2 instance           | Allowed types: `t3.micro`, `t2.small`. Max 2 non-terminated instances created by this CLI. |
| `list`      | List EC2 instances created by this CLI | Shows non-terminated instances tagged by the CLI.                                      |
| `stop`      | Stop a running EC2 instance (by ID)    | Only instances created by this CLI.                                        |
| `start`     | Start a stopped EC2 instance (by ID)   | Same tagging constraints as above.                                                     |

### S3
| Command       | Description                              | Behavior & Constraints                                                      |
|---------------|------------------------------------------|-----------------------------------------------------------------------------|
| `s3create`    | Create S3 bucket                         | Default private. With `--public` asks for confirmation to make public-read. |
| `s3upload`    | Upload file to bucket                    | Only allowed to buckets created by this CLI.                                |
| `s3list`      | List S3 buckets created by this CLI       | Shows only buckets created by this CLI.                         |

---

## 📋 Requirements

- Active **AWS account**
- IAM role or AWS profile with **EC2** and **S3** permissions
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

### EC2 Examples

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

### S3 Examples

Create a new bucket (private by default):

```bash
ben-awscli s3create mybucket123
```

Create a new bucket as public-read (with confirmation):

```bash
ben-awscli s3create mybucket123 --public
```

Upload a file to a bucket:

```bash
ben-awscli s3upload --bucket mybucket123 --file ./hello.txt
```

List all buckets created by this CLI:

```bash
ben-awscli s3list
```

## 📸 Demo Evidence

```bash
$ ben-awscli ec2create TestInstance
Created instance: i-0abcde12345f67890, named: TestInstance

$ ben-awscli ec2list
Instance id: i-0abcde12345f67890
Instance name: TestInstance
State: running
Type: t3.micro
IP: 3.23.45.67

$ ben-awscli s3create mybucket123
Bucket mybucket123 created (private).

$ ben-awscli s3upload --bucket mybucket123 --file ./hello.txt
Uploaded ./hello.txt to s3://mybucket123/hello.txt

$ ben-awscli s3list
- mybucket123

```
