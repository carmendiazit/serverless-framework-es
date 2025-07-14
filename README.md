# 🍕 Pizza Ordering System - Serverless Framework

> A modern, scalable pizza ordering system built with Node.js and deployed on AWS Lambda using the Serverless Framework.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js Version](https://img.shields.io/badge/Node.js-20.x-green.svg)](https://nodejs.org/)
[![AWS Lambda](https://img.shields.io/badge/AWS-Lambda-orange.svg)](https://aws.amazon.com/lambda/)
[![Serverless Framework](https://img.shields.io/badge/Serverless-Framework-red.svg)](https://serverless.com/)

## 📄 Table of Contents

- [📝 Overview](#-overview)
- [🏗️ Architecture](#️-architecture)
- [🚀 Features](#-features)
- [🛠️ Technologies](#️-technologies)
- [📋 Prerequisites](#-prerequisites)
- [⚙️ Installation](#️-installation)
- [🚀 Deployment](#-deployment)
- [📡 API Endpoints](#-api-endpoints)
- [🔧 Usage Examples](#-usage-examples)
- [📊 Monitoring & Logging](#-monitoring--logging)
- [🧪 Testing](#-testing)
- [☁️ AWS Configuration](#️-aws-configuration)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

---

## 📝 Overview

This project implements a **serverless pizza ordering system** built with Node.js and designed to run on AWS Lambda. It leverages key AWS services including **API Gateway**, **SQS** (Simple Queue Service), and **DynamoDB** to manage orders in a scalable, cost-effective, and serverless manner.

### Key Benefits:
- ⚡ **Serverless Architecture**: No server management, automatic scaling
- 💰 **Cost-Effective**: Pay only for what you use
- 🔄 **Event-Driven**: Asynchronous processing with SQS
- 📊 **Real-time Updates**: DynamoDB Streams for instant notifications
- 🛡️ **Secure**: AWS IAM roles and permissions
- 🌐 **Global Scale**: AWS infrastructure worldwide

## 🏗️ Architecture

The system follows a serverless, event-driven architecture:

![Architecture Diagram](assets/architecture-diagram.png)

### Flow Description:
1. **Client** → API Gateway → **newOrder** Lambda
2. **newOrder** → DynamoDB (save) → SQS (pending queue)
3. **SQS** → **prepOrder** Lambda → DynamoDB (update status)
4. **DynamoDB Stream** → **sendOrder** Lambda → SQS (delivery queue)

## 🚀 Features

- 📱 **RESTful API** for order management
- 🔄 **Asynchronous Processing** with SQS queues
- 📊 **Real-time Order Tracking** via DynamoDB Streams
- 🛡️ **Secure Authentication** with AWS IAM
- 📈 **Auto-scaling** Lambda functions
- 🔍 **Comprehensive Logging** with CloudWatch
- 🎯 **Event-driven Architecture** for reliability

## 🛠️ Technologies

| Technology | Purpose | Version |
|------------|---------|---------|
| **Node.js** | Runtime Environment | 20.x |
| **Serverless Framework** | Deployment & Management | Latest |
| **AWS Lambda** | Serverless Computing | - |
| **Amazon API Gateway** | API Management | v2 |
| **Amazon SQS** | Message Queuing | - |
| **Amazon DynamoDB** | NoSQL Database | - |
| **DynamoDB Streams** | Real-time Data Processing | - |
| **AWS IAM** | Identity & Access Management | - |
| **UUID** | Unique ID Generation | ^11.0.3 |

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- ✅ **Node.js** (v14 or higher) - [Download](https://nodejs.org/)
- ✅ **npm** (comes with Node.js)
- ✅ **AWS CLI** - [Installation Guide](https://aws.amazon.com/cli/)
- ✅ **AWS Account** with appropriate permissions
- ✅ **Git** - [Download](https://git-scm.com/)

### AWS Permissions Required:
- Lambda function creation and execution
- API Gateway management
- SQS queue creation and messaging
- DynamoDB table creation and operations
- IAM role creation
- CloudFormation stack management

## ⚙️ Installation

### 1. Clone the Repository
```bash
git clone https://github.com/carmendiazit/serverless-framework-es.git
cd serverless-framework-es
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Install Serverless Framework
```bash
npm install -g serverless
```

### 4. Configure AWS Credentials
```bash
aws configure
```

Or create `~/.aws/credentials`:
```ini
[default]
aws_access_key_id = YOUR_ACCESS_KEY_ID
aws_secret_access_key = YOUR_SECRET_ACCESS_KEY
```

### 5. Configure Serverless Framework
1. **Register** at [Serverless Framework](https://app.serverless.com/)
2. **Create Organization** (e.g., "Carmechas")
3. **Generate Access Key** in the dashboard
4. **Set Environment Variable**:
   ```bash
   export SERVERLESS_ACCESS_KEY=your_access_key_here
   ```

### 6. Update Configuration
Edit `serverless.yml` and update the `org` field:
```yaml
org: your-organization-name
```

### 7. Verify Installation
```bash
serverless --version
node --version
aws --version
```

## 🚀 Deployment

### Deploy to AWS
```bash
serverless deploy
```

### Deploy Specific Function
```bash
serverless deploy function --function newOrder
```

### Deploy to Different Stage
```bash
serverless deploy --stage production
```

After deployment, you'll see output similar to:
![Deployment Output](assets/endpoints-functions.png)

## 📡 API Endpoints

### Base URL
```
https://your-api-id.execute-api.us-east-1.amazonaws.com/
```

### Available Endpoints

| Method | Endpoint | Function | Description |
|--------|----------|----------|-------------|
| `POST` | `/order` | `newOrder` | Create a new pizza order |
| `GET` | `/order/{orderId}` | `getOrder` | Retrieve order details |

### Request/Response Examples

#### Create Order
```bash
curl -X POST https://your-api-endpoint/order \
  -H "Content-Type: application/json" \
  -d '{
    "pizza": "Margherita",
    "customerId": "customer123",
    "quantity": 2
  }'
```

**Response:**
```json
{
  "message": {
    "orderId": "550e8400-e29b-41d4-a716-446655440000",
    "pizza": "Margherita",
    "customerId": "customer123",
    "quantity": 2,
    "order_status": "PENDING"
  }
}
```

#### Get Order
```bash
curl https://your-api-endpoint/order/550e8400-e29b-41d4-a716-446655440000
```

**Response:**
```json
{
  "orderId": "550e8400-e29b-41d4-a716-446655440000",
  "pizza": "Margherita",
  "customerId": "customer123",
  "quantity": 2,
  "order_status": "COMPLETED"
}
```

## 🔧 Usage Examples

### Using Postman
![Postman Example](assets/postman-sample.png)

### Using curl
```bash
# Create order
ORDER_ID=$(curl -s -X POST https://your-api-endpoint/order \
  -H "Content-Type: application/json" \
  -d '{"pizza":"Pepperoni","customerId":"user456","quantity":1}' | \
  jq -r '.message.orderId')

# Get order status
curl https://your-api-endpoint/order/$ORDER_ID
```

### Using JavaScript
```javascript
const createOrder = async (orderData) => {
  const response = await fetch('https://your-api-endpoint/order', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(orderData)
  });
  return response.json();
};

// Usage
const order = await createOrder({
  pizza: 'Hawaiian',
  customerId: 'user789',
  quantity: 1
});
```

## 📊 Monitoring & Logging

### CloudWatch Logs
![CloudWatch Monitoring](assets/monitoreo.png)

### View Function Logs
```bash
# View logs for specific function
serverless logs --function newOrder

# Tail logs in real-time
serverless logs --function newOrder --tail
```

![Real-time Logs](assets/logs_t.png)

### AWS Console
- **CloudFormation** → Your Stack → Resources → Lambda Functions
- **CloudWatch** → Log Groups → `/aws/lambda/pizzaApp-dev-newOrder`

![Event Logs](assets/eventos-registro.png)

## 🧪 Testing

### Unit Tests
```bash
npm test
```

### Integration Tests
```bash
# Test API endpoints
curl -X POST https://your-api-endpoint/order \
  -H "Content-Type: application/json" \
  -d '{"pizza":"Test Pizza","customerId":"test123","quantity":1}'
```

### Load Testing
```bash
# Using Apache Bench
ab -n 100 -c 10 -H "Content-Type: application/json" \
  -p test-data.json https://your-api-endpoint/order
```

## ☁️ AWS Configuration

### Services Used

| Service | Purpose | Configuration |
|---------|---------|---------------|
| **Lambda** | Function execution | Node.js 20.x runtime |
| **API Gateway** | HTTP API endpoints | HTTP API (v2) |
| **SQS** | Message queuing | Standard queues |
| **DynamoDB** | Order storage | On-demand billing |
| **IAM** | Permissions | Least privilege roles |
| **CloudWatch** | Monitoring & logs | Automatic log retention |

### Cost Optimization
- 💰 **Lambda**: Pay per invocation
- 💰 **DynamoDB**: On-demand billing
- 💰 **SQS**: Pay per message
- 💰 **API Gateway**: Pay per request

### Security Best Practices
- 🔒 Least privilege IAM roles
- 🔒 VPC configuration (optional)
- 🔒 API Gateway throttling
- 🔒 DynamoDB encryption at rest

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. **Fork** the repository
2. **Create** a feature branch:
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Commit** your changes:
   ```bash
   git commit -m 'Add some amazing feature'
   ```
4. **Push** to the branch:
   ```bash
   git push origin feature/amazing-feature
   ```
5. **Open** a Pull Request

### Code Style
- Use ESLint for code formatting
- Follow Node.js best practices
- Write meaningful commit messages
- Add tests for new features

## 🙏 Acknowledgments

Special thanks to:
- 👩‍💻 **@MarciaVillalba** - Marcia Villalba
- 👩‍💻 **@LauraBolaños** - Laura Bolaños

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🔄 Cleanup

To remove all AWS resources:
```bash
serverless remove
```

## 🆘 Troubleshooting

### Common Issues

#### 1. Deployment Fails
```bash
# Check AWS credentials
aws sts get-caller-identity

# Verify Serverless configuration
serverless config credentials --list
```

#### 2. Function Timeout
- Increase timeout in `serverless.yml`
- Optimize function code
- Check CloudWatch logs

#### 3. Permission Errors
- Verify IAM roles
- Check resource policies
- Review CloudFormation events

### Getting Help
- 📚 [Serverless Framework Docs](https://www.serverless.com/framework/docs/)
- 📚 [AWS Lambda Docs](https://docs.aws.amazon.com/lambda/)
- 💬 [GitHub Issues](https://github.com/carmendiazit/serverless-framework-es/issues)

---

**Made with ❤️ by Carmen Diaz**
