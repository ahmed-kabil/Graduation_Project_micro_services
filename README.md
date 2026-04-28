# 🏥 Smart Healthcare Monitoring System - Backend

A scalable backend system for a smart healthcare monitoring platform built using Node.js, Express.js, MongoDB, and Socket.IO.

This repository contains the backend implementation for the graduation project including:

- Authentication & Authorization
- Staff Management
- Patient Management
- IoT Sensor Readings
- Real-Time Chat System
- Appointment Management
- Metrics & Monitoring APIs

> The full deployment infrastructure, Kubernetes manifests, CI/CD pipelines, and DevOps setup are maintained in a separate repository.

---

# 🚀 Tech Stack

- Node.js
- Express.js
- MongoDB
- Mongoose
- JWT Authentication
- Socket.IO
- Prometheus Metrics

---

# 🧩 Backend Architecture

The backend is divided into multiple services:

| Service | Description |
|---|---|
| Auth Service | Handles authentication and JWT tokens |
| Core Service | Handles staff, patients, and appointments |
| IoT Service | Handles medical sensor readings |
| Chat Service | Handles real-time messaging |
| Metrics Service | Exposes Prometheus metrics |

---

# 🔐 Authentication

## Login API

### Endpoint

```http
POST /api/login
```

### Request Body

```json
{
  "email": "doc002@gmail.com",
  "password": "doc002"
}
```

### Response

```json
{
  "status": "success",
  "data": {
    "token": "JWT_TOKEN",
    "user_id": "doc002",
    "role": "doctor"
  }
}
```

## Supported Roles

- admin
- doctor
- nurse
- receptionist
- patient

---

# 👨‍⚕️ Staff Management

## Features

- Add new staff members
- Get all staff members
- Filter by role
- Update staff data
- Delete staff members

## APIs

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/staff/add` | Add staff member |
| GET | `/api/staff` | Get all staff |
| GET | `/api/staff/doctors` | Get doctors |
| GET | `/api/staff/nurses` | Get nurses |
| GET | `/api/staff/receptionists` | Get receptionists |
| GET | `/api/staff/{staffMem_id}` | Get specific staff member |
| PATCH | `/api/staff/{staffMem_id}` | Update staff member |
| DELETE | `/api/staff/{staffMem_id}` | Delete staff member |

---

# 🧑‍🦽 Patient Management

## Features

- Add patients
- Assign doctors
- Manage linked devices
- Update patient information
- Delete patients

## APIs

| Method | Endpoint |
|---|---|
| GET | `/api/patients` |
| POST | `/api/patients/add` |
| GET | `/api/patients/{patient_id}` |
| PATCH | `/api/patients/{patient_id}` |
| DELETE | `/api/patients/{patient_id}` |

---

# 📡 IoT Readings Service

The IoT service stores and retrieves patient medical sensor readings.

## Supported Sensors

- Heart Rate
- SpO2
- Temperature
- Respiration Rate
- Respiration Pattern

## APIs

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/readings` | Get all readings |
| POST | `/api/readings/add` | Add readings |
| GET | `/api/readings/{dev_id}` | Get device readings |

---

# 💬 Real-Time Chat Service

The system supports real-time communication using Socket.IO between:

- Doctor ↔ Patient
- Doctor ↔ Nurse

Messages are stored in MongoDB for future retrieval.

---

# 🧵 Conversation APIs

## Doctor ↔ Patient Conversations

| Method | Endpoint |
|---|---|
| GET | `/api/conversations/pats_of_doc/{doc_id}` |

## Doctor ↔ Nurse Conversations

| Method | Endpoint |
|---|---|
| GET | `/api/conversations/nurs_of_doc/{doc_id}` |
| GET | `/api/conversations/docs_of_nur/{nur_id}` |

---

# ✉️ Messaging APIs

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/messages/send` | Send message |
| GET | `/api/messages/{conversation_id}` | Get conversation messages |
| POST | `/api/messages/read` | Mark messages as read |

---

# ⚡ Socket.IO Events

## User Online

```javascript
socket.emit("online", user_id);
```

## Join Conversation

```javascript
socket.emit("joinConversation", conversation_id);
```

---

# 👨‍⚕️ Doctor ↔ Patient Messaging

## Send Message

```javascript
socket.emit("sendDocPatMessage", {
  conversation_id: "conv_pat001",
  sender_id: "doc001",
  receiver_id: "pat001",
  message: "Hello!"
});
```

## Receive Message

```javascript
socket.on("receiveDocPatMessage", (data) => {
  console.log(data);
});
```

---

# 👩‍⚕️ Doctor ↔ Nurse Messaging

## Send Message

```javascript
socket.emit("sendDocNurMessage", {
  conversation_id: "conv_doc001_nur001",
  sender_id: "doc001",
  receiver_id: "nur001",
  message: "Hello!"
});
```

## Receive Message

```javascript
socket.on("receiveDocNurMessage", (data) => {
  console.log(data);
});
```

---

# 📅 Appointment Management

Patients can book appointments and doctors can manage appointment status.

## APIs

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/appointments/add` | Book appointment |
| POST | `/api/appointments/fulfill` | Fulfill appointment |
| GET | `/api/appointments/for_doc/{doctor_id}` | Get doctor appointments |
| GET | `/api/appointments/for_pat/{patient_id}` | Get patient appointments |
| DELETE | `/api/appointments/{_id}` | Delete appointment |

---

# 🔔 Real-Time Appointment Events

## New Appointment

```javascript
socket.emit("newAppointment", data);
```

## Cancel Appointment

```javascript
socket.emit("CancelAppointment", data);
```

---

# 📊 Metrics Service

## Endpoint

```http
GET /api/metrics
```

Exposes Prometheus-compatible metrics for monitoring backend services.

---

# 🗄️ Database Collections

- users
- staff
- patients
- readings
- conversations
- messages
- appointments

---

# 📁 Project Structure

```bash
backend/
│
├── auth-service/
├── core-service/
├── chat-service/
├── iot-service/
├── metrics-service/
│
├── models/
├── routes/
├── controllers/
├── middleware/
├── sockets/
└── config/
```

---

# 🔒 Security Features

- JWT Authentication
- Role-Based Access Control
- Protected APIs
- Input Validation
- Secure Password Handling

---

# 🎯 System Features

- Multi-role healthcare platform
- Real-time communication
- IoT patient monitoring
- Appointment scheduling
- Persistent chat history
- Prometheus monitoring support
- Modular backend architecture

---

# 🛠️ Running The Project

## Install Dependencies

```bash
npm install
```

## Start Development Server

```bash
npm run dev
```

## Start Production Server

```bash
npm start
```

---

# 🌐 Environment Variables

Example `.env` file:

```env
PORT=5000
MONGO_URI=your_mongodb_uri
JWT_SECRET=your_secret
```

---

# 📌 Notes

- Conversations are automatically created when assigning a patient to a doctor.
- Patient conversation IDs follow this format:

```text
conv_<patient_id>
```

- Doctor-Nurse conversation IDs follow:

```text
conv_<doctor_id>_<nurse_id>
```

---

# 👨‍💻 Graduation Project

This repository contains only the backend implementation.

The complete deployment infrastructure including:

- Docker
- Kubernetes
- CI/CD
- Monitoring Stack
- GitOps Deployment

exists in a separate repository.

---

# 📄 License

This project was developed for educational and graduation project purposes.