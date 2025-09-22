# 🏦 James Bank PLC - Real-time Suspicious Activity Detection System

A comprehensive banking application that demonstrates real-time fraud detection and customer notification using Apache Kafka, Flask, and Telegram integration. The system monitors customer profile changes and instantly alerts customers of suspicious activities via Telegram notifications.

## 🎯 Project Overview

This project showcases a complete event-driven architecture for banking security, featuring:

- **Real-time Event Processing**: Using Apache Kafka for streaming customer profile changes
- **Suspicious Activity Detection**: Automated detection of profile modifications (email changes, etc.)
- **Instant Customer Alerts**: Telegram notifications sent directly to customers' phones
- **Banking Web Interface**: Professional customer profile management system
- **Event Monitoring**: Kafka Control Center for real-time event visualization

## 🏗️ Architecture

```
┌─────────────────┐    ┌──────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Bank Web App  │───▶│    Kafka     │───▶│   Consumer      │───▶│   Telegram      │
│   (Flask)       │    │   Broker     │    │  Application    │    │  Notification   │
│  localhost:5000 │    │              │    │ (Change Detect) │    │                 │
└─────────────────┘    └──────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                    │
         └───────────────────────┼────────────────────┘
                                 ▼
                        ┌──────────────┐
                        │    Control   │
                        │    Center    │
                        │localhost:9021│
                        └──────────────┘
```

## 🚀 Quick Start

### Prerequisites

- Docker and Docker Compose installed
- Git installed
- Internet connection for Telegram notifications

### Step 1: Clone the Repository

```bash
git clone https://github.com/ekelejames/banking-suspicious-activity-detection-system.git
cd banking-suspicious-activity-detection-system
```

### Step 2: Start the Complete Stack

```bash
# Build and start all services in detached mode
docker-compose up -d
```

This command will spin up the following containers:
- **Kafka Broker**: Message streaming platform (running in Kraft mode)
- **Control Center**: Kafka monitoring and management UI
- **Bank Web Application**: Customer profile management interface
- **Consumer Application**: Suspicious activity detection and Telegram notification service

### Step 3: Access the Applications

Once all containers are running, access:

- **🏦 Bank Web Interface**: [http://localhost:5000](http://localhost:5000)
- **📊 Kafka Control Center**: [http://localhost:9021](http://localhost:9021)

Wait for all services to be fully initialized (usually 2-3 minutes for first startup).

### Step 4: Create a Customer Profile

1. Navigate to the Bank Web Interface at `localhost:5000`
2. Fill out the customer profile form with:
   - Personal information (name, email, address, etc.)
   - **Important**: Use your actual Telegram phone number in the format `+1234567890`
   - Select an account type
3. Click "Create Profile"
4. Note the generated Customer ID for reference
<img width="1450" height="910" alt="Screenshot 2025-09-22 104511" src="https://github.com/user-attachments/assets/7831bd3a-11a5-4218-9e1d-e1a652dad827" />


### Step 5: Trigger Suspicious Activity Detection

1. Click on the "View/Edit Profile" link for your created customer
2. **Change the email address** to a different email
3. Click "Update Profile"
4. The system will detect this as suspicious activity (email change)

### Step 6: Verify Telegram Notification

Within seconds of updating the profile:

1. **Check your Telegram** for a security alert message
2. The message will include:
   - Alert about profile changes
   - Details of what was changed (old email → new email)
   - Customer ID for reference
   - Timestamp of the change

**Sample Telegram Message:**
```
🚨 SECURITY ALERT - Email Change Detected

Hi {Customer Name},

An email change has been detected on your James Bank account. If you authorized this change, please ignore this message.

👤 Account: {Customer Name}
🆔 Customer ID: {Customer ID}
🕐 Time: 2025-09-20T10:07:02.327914
📧 Old Email: {Old Email}
📧 New Email: {New Email}

If you did NOT make this change:
• Contact James Bank immediately
• Change your account password
• Review your recent account activity

This is an automated security notification.
```

### Step 7: Monitor Events (Optional)

1. Go to Kafka Control Center at `localhost:9021`
2. Navigate to Topics → `customer-profiles`
3. View real-time messages showing profile creation and update events
4. Observe the event-driven architecture in action

### Step 8: Tear Down the Cluster

```bash
# Stop and remove all containers
docker-compose down

# Optional: Remove volumes and networks
docker-compose down -v --remove-orphans
```

## 🛠️ Technology Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| **Web Application** | Flask + Python | Customer profile management |
| **Message Broker** | Apache Kafka | Event streaming and processing |
| **Consumer Service** | Python + kafka-python | Change detection and notifications |
| **Notification Service** | Telegram Bot API | Customer alerts |
| **Monitoring** | Confluent Control Center | Kafka cluster management |
| **Containerization** | Docker + Docker Compose | Service orchestration |

## 📋 Services Overview

### 🏦 Bank Web Application (`localhost:5000`)
- Professional banking interface
- Customer profile CRUD operations
- Real-time form validation
- Responsive design with James Bank PLC branding

### 📊 Kafka Control Center (`localhost:9021`)
- Kafka cluster monitoring
- Topic and partition management
- Real-time message inspection
- Consumer group monitoring

### 🔍 Consumer Application
- Monitors `customer-profiles` topic
- Detects suspicious profile changes
- Sends Telegram notifications
- Logs all security events

### ⚡ Apache Kafka Broker
- Handles event streaming
- Manages topic partitions
- Ensures message durability
- Enables real-time processing


## 🔧 Configuration
## 📊 Monitoring and Observability

The system provides comprehensive monitoring through:

- **Kafka Control Center**: Real-time topic and consumer monitoring
- **Application Logs**: Detailed logging of all operations
- **Health Check Endpoints**: Service health monitoring
- **Message Tracing**: End-to-end event tracking

## 🚀 Production Considerations

For production deployment:

- **Database Integration**: Replace in-memory storage with PostgreSQL/MongoDB
- **Authentication**: Implement OAuth2/JWT authentication
- **SSL/TLS**: Enable encryption for all communications
- **Rate Limiting**: Implement API rate limiting
- **Backup Strategy**: Configure Kafka data retention and backup
- **Monitoring**: Add Prometheus/Grafana for metrics
- **Load Balancing**: Use NGINX for load distribution

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📞 Support

For questions or issues:

- **GitHub Issues**: [Create an issue](https://github.com/ekelejames/banking-suspicious-activity-detection-system/issues)
- **Email**: ekeleejames@gmail.com
- **Documentation**: (adding soon)

## 🙏 Acknowledgments

- Apache Kafka community for the excellent streaming platform
- Confluent for the Control Center interface
- Telegram for providing the Bot API
- Flask community for the web framework

---

**⚠️ Disclaimer**: This is a demonstration project for educational purposes. Do not use in production without proper security hardening and compliance reviews.
