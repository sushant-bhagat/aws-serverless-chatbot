# AWS-SERVERLESS-CHATBOT
# ☁️ AWS Serverless Chatbot

> A fully serverless conversational chatbot built on AWS — powered by Amazon Lex,
> AWS Lambda, EC2, and S3 with IAM least-privilege security throughout.

---

## 🏗️ Architecture
```
User Message
     │
     ▼
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│ Amazon Lex  │────▶│ AWS Lambda   │────▶│  Amazon S3  │
│  (NLP/NLU)  │     │ (Logic/API)  │     │  (Storage)  │
└─────────────┘     └──────────────┘     └─────────────┘
                            │
                            ▼
                    ┌──────────────┐
                    │   Amazon EC2 │
                    │   (Server)   │
                    └──────────────┘
```

---

## 🛠️ Tech Stack
https://github.com/users/sushant-bhagat/achievements/quickdraw

---

## ✨ Features

- 🤖 **Natural Language Understanding** via Amazon Lex — handles user intents and slots
- ⚡ **Serverless Logic** via AWS Lambda — zero server management, auto-scaling
- 🖥️ **EC2 Application Server** — hosts the web interface and API gateway layer
- 🗄️ **S3 Storage** — stores conversation logs, media, and static assets
- 🔒 **IAM Security** — least-privilege roles applied to every service interaction
- 📈 **Auto-scaling** — serverless architecture scales with demand automatically

---

## 🔒 Security Design

| Component | Security Measure |
|-----------|-----------------|
| Lambda | IAM role with only required S3 and Lex permissions |
| EC2 | Security group restricting inbound to port 443/80 only |
| S3 | Bucket policy blocking public access; access via signed URLs |
| Lex | Bot access restricted to authorised Lambda ARN only |

---

## 🚀 How to Deploy

### Prerequisites
- AWS Account with admin access
- AWS CLI configured (`aws configure`)
- Python 3.9+ installed

### Steps

**1. Clone this repo**
```bash
git clone https://github.com/sushant_bhagat/aws-serverless-chatbot
cd aws-serverless-chatbot
```

**2. Deploy Lambda function**
```bash
cd lambda/
zip function.zip handler.py
aws lambda create-function \
  --function-name chatbot-handler \
  --runtime python3.9 \
  --role arn:aws:iam::YOUR_ACCOUNT_ID:role/lambda-role \
  --handler handler.lambda_handler \
  --zip-file fileb://function.zip
```

**3. Create S3 bucket**
```bash
aws s3 mb s3://your-chatbot-storage-bucket
aws s3api put-public-access-block \
  --bucket your-chatbot-storage-bucket \
  --public-access-block-configuration BlockPublicAcls=true
```

**4. Configure Amazon Lex**
- Go to AWS Console → Amazon Lex → Create Bot
- Set the Lambda function as the fulfillment hook
- Define intents: `Greeting`, `Help`, `Fallback.`

**5. Launch EC2 instance**
```bash
aws ec2 run-instances \
  --image-id ami-0abcdef1234567890 \
  --instance-type t2.micro \
  --key-name your-key-pair \
  --security-group-ids sg-xxxxxxxx
```

---

## 📁 Project Structure
```
aws-serverless-chatbot/
├── lambda/
│   └── handler.py          # Lambda function logic
├── lex/
│   └── bot-config.json     # Lex bot export configuration
├── ec2/
│   └── setup.sh            # EC2 bootstrap script
├── iam/
│   └── policies.json       # IAM role and policy definitions
├── s3/
│   └── bucket-policy.json  # S3 bucket policy
└── README.md
```

---

## 👨‍💻 Author
Sushant Bhagat  — DevOps & Cloud Engineer
🌏 Pune, India | Seeking roles in Abroad
LinkedIn:- https://www.linkedin.com/in/sushant-bhagat-p1/
Email:- sushantb057@gmail.com
