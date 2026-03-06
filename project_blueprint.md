# Smart Scalable Attendance System Blueprint

Author: PSD Rao
Project Type: Distributed Face Recognition Attendance System
Core Technology: Face Embeddings + FAISS Similarity Search

---

# 1. Project Overview

A distributed biometric attendance system designed for classrooms and campus spaces.
The system uses facial embeddings and FAISS similarity search to identify students
efficiently while preserving privacy.

Key characteristics:

- No face images stored
- Only embedding vectors stored
- Distributed recognition devices
- Offline capability
- Centralized reporting server

---

# 2. Core Design Principles

1. Privacy-first biometric system
2. Fast similarity search using FAISS
3. Distributed device architecture
4. Offline attendance capability
5. Secure device-server communication
6. Modular system design

---

# 3. System Architecture

Main components:

Admin Server
MongoDB Database
Classroom Devices
Reading Room Entry Devices
Web Dashboard

Data Flow:

Camera
→ Face Detection
→ Embedding Generation
→ FAISS Search
→ Attendance Decision
→ Local Storage
→ Server Sync

---

# 4. Device Architecture

Each device contains:

Camera Module
Face Detection Module
Embedding Generation Module
FAISS Search Engine
Attendance Buffer
API Communication Module

Device Responsibilities:

- Face recognition
- Attendance capture
- Offline buffering
- Sync with central server

---

# 5. Database Collections

Collections used in MongoDB:

students
faculty
subjects
devices
sessions
attendance

---

# 6. Student Data Model

Fields:

reg_no
name
contact
embedding_vector
created_at

Note:
Registration number encodes course information.

Example:

24MAI26

24 → admission year
MAI → MSc AI & DS
26 → student number

---

# 7. Subject Model

Fields:

subject_id
faculty_id
class_code
timetable

---

# 8. Device Model

Fields:

device_id
mac_address
verification_key
location
status

Purpose:

Authenticate classroom devices.

---

# 9. Attendance Model

Fields:

reg_no
subject_id
session_no
device_id
timestamp

Duplicate rule:

reg_no + subject_id + session_no must be unique

---

# 10. Session Model

Used when subject occurs multiple times per day.

Fields:

subject_id
date
session_no
start_time

Example:

Session 1 → 10:00
Session 2 → 14:00

---

# 11. Recognition Pipeline

Recognition process:

Camera Capture
→ Face Detection
→ Embedding Extraction
→ FAISS Index Search
→ Distance Threshold Check
→ Attendance Marked

---

# 12. FAISS Index Strategy

FAISS index stored on classroom devices.

Index updated when:

new student enrolled
student removed
embedding updated

Devices periodically check for embedding updates.

---

# 13. Attendance Modes

## Subject Attendance

Rule:

1 student
1 subject
1 session

Duplicate attendance prevented.

---

## Classroom Group Attendance

Multiple students detected simultaneously.

Used during lectures.

---

## Reading Room Entry

Entry–Exit model.

entry → exit pairing required.

Multiple entries allowed per day.

QR scanning supported.

---

# 14. Offline Mode

Devices can operate without internet.

Process:

Attendance stored locally
↓
Device attempts sync periodically
↓
Server confirms receipt
↓
Local buffer cleared

---

# 15. Device-Server API

Endpoints:

POST /api/device/register
GET /api/device/embeddings
GET /api/device/session
POST /api/device/attendance
POST /api/device/heartbeat

---

# 16. Security Rules

Devices must authenticate using device_key.

Server validates:

device identity
subject session
attendance duplicates

All communication uses HTTPS.

---

# 17. Performance Considerations

FAISS used for fast nearest neighbor search.

Typical recognition time:

0.2 – 0.3 seconds per face.

Simultaneous recognition capacity:

8–12 faces per frame.

---

# 18. Logging System

System logs events:

device connection
attendance recorded
sync success
sync failure
recognition results

Logs stored for debugging and auditing.

---

# 19. Future Improvements

Possible future extensions:

AI surveillance analytics
GPU accelerated recognition
large-scale biometric database
mobile device integration

---

# 20. Development Rules

Before coding:

Design architecture
Define modules
Define database models
Define API communication

Avoid changing core logic without updating all dependent modules.

---

# 21. Notes and Ideas

(Add any new ideas here during development.)
