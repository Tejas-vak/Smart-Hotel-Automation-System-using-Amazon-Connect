# Smart Hotel Management System using Amazon Connect

This project implements a cloud-based, intelligent contact solution for hotel management using Amazon Connect and other AWS services. It enables customers to interact with the hotel via voice for booking services, accessing support, and leaving voicemails — all powered by conversational AI and serverless automation.

---

## 🧠 Features

- **Conversational AI with Amazon Lex**: Detects customer intent using natural language and routes them to the appropriate service queue.
- **Dynamic IVR Flow**: Built using Amazon Connect contact flows with modular blocks for routing, prompts, and logic.
- **DynamoDB-Driven Prompts**: All voice prompts are stored in a DynamoDB table. A single Lambda function is used to fetch the correct message based on the key provided in the play prompt block. The play prompt uses `Namespace: External` and a dynamic `Key` to signal the Lambda function to retrieve the appropriate message.
- **Callback Option**: If a customer waits too long in a queue, they are offered a callback option to avoid long hold times.
- **Voicemail Support**: Customers can leave a voicemail. Two Lambda functions handle voicemail recording and processing.

---

## 🏗️ Architecture Overview

1. **Amazon Connect**: Hosts the virtual contact center and IVR flow.
2. **Amazon Lex**: Captures customer intent and routes to the correct queue.
3. **AWS Lambda**:
   - One function fetches prompt messages from DynamoDB.
   - Two functions manage voicemail logic.
4. **Amazon DynamoDB**: Stores all IVR prompt messages.
5. **Amazon S3 (optional)**: Can be used to store voicemail recordings.
6. **Amazon CloudWatch**: For logging and monitoring Lambda executions.

---

## 🔁 How It Works

1. **Customer Call Initiation**:
   - Customer calls the hotel contact number hosted on Amazon Connect.
   - Amazon Lex listens to the customer's request and matches it to a predefined intent.

2. **Intent Routing**:
   - Based on the matched intent, the call is routed to the appropriate queue or flow block.

3. **Dynamic Prompts**:
   - At each play prompt block, the system uses `Namespace: External` and a `Key` to trigger the Lambda function.
   - The Lambda function queries DynamoDB using the provided key to fetch the appropriate message and returns it to the IVR flow.

4. **Callback Option**:
   - If the customer waits too long in a queue, they are offered the option to receive a callback.
   - The system captures their number and schedules a callback.

5. **Voicemail Handling**:
   - If the customer chooses to leave a voicemail, the system records it.
   - Two Lambda functions manage the voicemail logic (e.g., storing, notifying, or processing).
