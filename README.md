🏥 Smart Healthcare Monitoring System — Backend

A scalable backend system for a smart healthcare monitoring platform built using Node.js, Express.js, MongoDB, and Socket.IO.

This repository contains the complete backend implementation for the graduation project including:

Authentication & Authorization
Staff Management
Patient Management
IoT Sensor Readings
Real-Time Chat System
Appointment Management
Metrics & Monitoring APIs

The complete deployment infrastructure, CI/CD pipelines, Kubernetes manifests, and DevOps setup are available in a separate repository.

🚀 Tech Stack
Node.js
Express.js
MongoDB
Mongoose
JWT Authentication
Socket.IO
Prometheus Metrics
REST APIs
🧩 Backend Architecture

The backend is designed using a service-oriented architecture and consists of multiple logical services:

Service	Description
Auth Service	Handles login and JWT authentication
Core Service	Manages staff, patients, and appointments
IoT Service	Handles medical sensor readings
Chat Service	Real-time messaging using Socket.IO
Metrics Service	Exposes Prometheus monitoring metrics
🔐 Authentication
Login API
Endpoint
POST /api/login
Request Body
{
  "email": "doc002@gmail.com",
  "password": "doc002"
}
Response
{
  "status": "success",
  "data": {
    "token": "JWT_TOKEN",
    "user_id": "doc002",
    "role": "doctor"
  }
}
Supported Roles
admin
doctor
nurse
receptionist
patient

JWT tokens are used for authentication across protected APIs.

👨‍⚕️ Staff Management APIs
Features
Add new staff members
Get all staff
Filter staff by role
Update staff information
Delete staff members
Main Endpoints
Method	Endpoint	Description
POST	/api/staff/add	Add new staff member
GET	/api/staff	Get all staff
GET	/api/staff/doctors	Get all doctors
GET	/api/staff/nurses	Get all nurses
GET	/api/staff/receptionists	Get all receptionists
GET	/api/staff/{staffMem_id}	Get staff by ID
PATCH	/api/staff/{staffMem_id}	Update staff
DELETE	/api/staff/{staffMem_id}	Delete staff
🧑‍🦽 Patient Management APIs
Features
Add patients
Assign doctors
Manage linked IoT devices
Update patient information
Delete patients
Main Endpoints
Method	Endpoint
GET	/api/patients
POST	/api/patients/add
GET	/api/patients/{patient_id}
PATCH	/api/patients/{patient_id}
DELETE	/api/patients/{patient_id}
📡 IoT Sensor Readings Service

The IoT service stores and retrieves real-time medical sensor readings coming from patient monitoring devices.

Supported Sensors
Heart Rate
SpO2
Temperature
Respiration Rate
Respiration Pattern
Main Endpoints
Method	Endpoint	Description
GET	/api/readings	Get all readings
POST	/api/readings/add	Add sensor readings
GET	/api/readings/{dev_id}	Get readings for specific device
💬 Real-Time Chat Service

The platform supports real-time communication using Socket.IO between:

Doctor ↔ Patient
Doctor ↔ Nurse

Messages are stored in MongoDB for future retrieval.

🧵 Conversation APIs
Doctor ↔ Patient Conversations
Method	Endpoint
GET	/api/conversations/pats_of_doc/{doc_id}
Doctor ↔ Nurse Conversations
Method	Endpoint
GET	/api/conversations/nurs_of_doc/{doc_id}
GET	/api/conversations/docs_of_nur/{nur_id}
✉️ Messaging APIs
Method	Endpoint	Description
POST	/api/messages/send	Send message
GET	/api/messages/{conversation_id}	Get conversation messages
POST	/api/messages/read	Mark messages as read
⚡ Socket.IO Events
Connection Events
User Online
socket.emit("online", user_id);
Join Conversation
socket.emit("joinConversation", conversation_id);
👨‍⚕️ Doctor ↔ Patient Messaging
Send Message
socket.emit("sendDocPatMessage", {
  conversation_id: "conv_pat001",
  sender_id: "doc001",
  receiver_id: "pat001",
  message: "Hello!"
});
Receive Message
socket.on("receiveDocPatMessage", (data) => {
  console.log(data);
});
👩‍⚕️ Doctor ↔ Nurse Messaging
Send Message
socket.emit("sendDocNurMessage", {
  conversation_id: "conv_doc001_nur001",
  sender_id: "doc001",
  receiver_id: "nur001",
  message: "Hello!"
});
Receive Message
socket.on("receiveDocNurMessage", (data) => {
  console.log(data);
});
📅 Appointment Management

Patients can book appointments with doctors and doctors can manage appointment status.

Main Endpoints
Method	Endpoint	Description
POST	/api/appointments/add	Book appointment
POST	/api/appointments/fulfill	Mark appointment as fulfilled
GET	/api/appointments/for_doc/{doctor_id}	Get doctor appointments
GET	/api/appointments/for_pat/{patient_id}	Get patient appointments
DELETE	/api/appointments/{_id}	Cancel/Delete appointment
🔔 Real-Time Appointment Events
New Appointment
socket.emit("newAppointment", data);
Cancel Appointment
socket.emit("CancelAppointment", data);

Doctors receive appointment updates in real time through Socket.IO.

📊 Metrics Service
Endpoint
GET /api/metrics

This endpoint exposes Prometheus-compatible metrics for monitoring backend services and system performance.

🗄️ Database

MongoDB collections include:

users
staff
patients
readings
conversations
messages
appointments
📁 Project Structure
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
🔒 Security Features
JWT Authentication
Role-Based Access Control
Protected APIs
Input Validation
Secure Password Handling
🎯 System Features
Multi-role healthcare platform
Real-time communication
IoT medical monitoring
Appointment scheduling
Prometheus monitoring support
Persistent chat history
Modular backend architecture
🛠️ Running the Project
Install Dependencies
npm install
Start Development Server
npm run dev
Start Production Server
npm start
🌐 Environment Variables

Example .env file:

PORT=5000
MONGO_URI=your_mongodb_uri
JWT_SECRET=your_secret
📌 Notes
Conversations are automatically created when a patient is assigned to a doctor.

Conversation IDs follow this pattern:

conv_<patient_id>

Doctor-Nurse conversation IDs follow:

conv_<doctor_id>_<nurse_id>
👨‍💻 Graduation Project

This repository contains only the backend implementation of the system.

The full deployment infrastructure including:

Docker
Kubernetes
CI/CD
Monitoring Stack
GitOps Deployment

is maintained in a separate repository.

📄 License

This project is developed for educational and graduation project purposes.