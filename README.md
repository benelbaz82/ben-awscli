# 🐧 Ben's AWS CLI

A lightweight, developer-friendly CLI tool for managing AWS EC2 instances using Python, `boto3`, and `click`.  
This tool allows developers to create, start, stop, and list EC2 instances while enforcing safe, standardized practices.

---

## 🚀 Features

### 💻 EC2

| Command     | Description                            | Behavior & Constraints                                                                 |
|-------------|----------------------------------------|----------------------------------------------------------------------------------------|
| `create`    | Provision a new EC2 instance           | Allowed types: `t3.micro`, `t2.small`. Max 2 non-terminated instances created by this CLI. |
| `list`      | List EC2 instances created by this CLI | Shows non-terminated instances tagged by the CLI.                                      |
| `stop`      | Stop a running EC2 instance (by ID)    | Only instances created by this CLI.                                        |
| `start`     | Start a stopped EC2 instance (by ID)   | Same tagging constraints as above.                                                     |

### 🪣 S3
| Command       | Description                              | Behavior & Constraints                                                      |
|---------------|------------------------------------------|-----------------------------------------------------------------------------|
| `s3create`    | Create S3 bucket                         | Default private. With `--public` asks for confirmation to make public-read. |
| `s3upload`    | Upload file to bucket                    | Only allowed to buckets created by this CLI.                                |
| `s3list`      | List S3 buckets created by this CLI       | Shows only buckets created by this CLI.                         |

### 🌐 Route53
| Command       | Description                                  | Behavior & Constraints                                        |
|---------------|----------------------------------------------|---------------------------------------------------------------|
| `r53create`   | Create a new hosted zone                     | Creates zone.                 |
| `r53manage`   | Manage DNS records (create/update/delete)    | Works only in zones created by this CLI.                      |
| `r53list`     | List CLI-created hosted zones and their records | Shows only zones and records tagged by this CLI.             |
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

### 💻 EC2 Examples

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

### 🪣 S3 Examples

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

### 🌐 Route53 Examples

Create a new hosted zone:

```bash
ben-awscli r53create benben.com
```

Create a DNS record inside a zone:
```bash
ben-awscli r53manage create --zone benben.com --name www.benben.com --type A --value 1.2.3.4
```

Update a record:
```bash
ben-awscli r53manage update --zone benben.com --name www.benben.com --type A --value 5.6.7.8
```

Delete a record:
```bash
ben-awscli r53manage delete --zone benben.com --name www.benben.com --type A --value 5.6.7.8
```

List CLI-created zones and their records:
```bash
ben-awscli r53list
```

## 🧹 Cleanup Instructions

To avoid unwanted charges, you should clean up the resources created by this CLI.

-  **EC2**:  
  Stop and start are supported by the CLI.  
  For full termination (delete instance), use the **AWS Console**.

- **S3**:  
  Bucket creation and upload are supported by the CLI.  
  For full deletion of buckets (must be emptied first), use the **AWS Console**.

- **Route53**:  
  DNS record creation, update and delete are supported by the CLI.  
  Hosted zone deletion should be done manually from the **AWS Console**.

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

$ ben-awscli r53create benben.com
Hosted zone created: benben.com (id: Z04567891ABCDEFG12345)

$ ben-awscli r53manage create --zone benben.com --name www.benben.com --type A --value 1.2.3.4
CREATE A www.benben.com -> 1.2.3.4 (zone benben.com)

$ ben-awscli r53list
Zone: benben.com (ID: Z04567891ABCDEFG12345)
  Records:
    - A benben.com. -> 1.2.3.4
    - A www.benben.com. -> 1.2.3.4
```
