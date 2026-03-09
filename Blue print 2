# Smart Scalable AI Surveillance & Attendance System
**Project Blueprint Document - Version 2.0**

**Author:** Yantra  
**Project Type:** Distributed Biometric & Behavioral Analytics System  
**Core Technology:** FaceNet Embeddings + FAISS Similarity Search + ByteTrack Persistence

---

## 1 Project Overview
This system is a distributed biometric platform designed for educational institutions. It uses facial embedding vectors to identify students quickly while preserving privacy. The architecture consists of a central administrative server and multiple edge recognition devices. It operates in both online and offline modes to ensure continuity.

## 2 Core Design Principles
* **Privacy Protection:** No raw image storage; only compact embeddings are saved.
* **Speed:** Utilizing FAISS for high-speed similarity searching.
* **Resilience:** Offline-capable devices with local buffering.
* **Efficiency:** "Mark until Uncover" logic to reduce redundant recognition.
* **Scalability:** Distributed architecture for large-scale campus deployment.

## 3 System Architecture
The system consists of a Central Admin Server, MongoDB Database, Recognition Devices (classrooms/entry points), and a Web Dashboard for reporting. The workflow moves from Camera Capture and Face Detection to Embedding Extraction, FAISS Search, and finally Identity Matching/Attendance Recording.

## 4 Complete Project Folder Structure
The project is organized into `server_admin/`, `database/`, `device_client/`, `models/`, `shared/`, `scripts/`, and `tests/` directories to maintain a clean distributed architecture.

## 5 Database Collections (MongoDB)
Key collections include `students`, `faculty`, `subjects`, `devices`, `sessions`, and `attendance`.

## 6 Student Data Model
Includes `reg_no` (e.g., 24MAI26), `name`, `contact`, and `embedding_vector`. Course and year info are derived from the registration number.

## 7 Faculty Model
Stores `faculty_id`, `name`, `email`, and `subjects_assigned`.

## 8 Subject Model
Contains `subject_id` (e.g., MAI201), `subject_name`, `faculty_id`, and `course_code`.

## 9 Device Model
Tracks `device_id`, `mac_address`, `device_key`, `location`, and `status`. Devices must authenticate before communicating with the server.

## 10 Attendance Model
Links `reg_no`, `subject_id`, `session_no`, and `timestamp`. A uniqueness rule prevents duplicate entries for the same session.

## 11 Session Model
Defines class periods with `start_time`, `end_time`, and `session_no`.

## 12 Recognition Pipeline
A multi-stage process: Capture -> Detect -> Extract Embedding -> FAISS Search -> Threshold Check -> Record.

## 13 FAISS Similarity Search
The system uses FAISS IVF indexing stored locally on the device to find the nearest neighbor to an extracted embedding. The index is updated whenever student data changes.

## 14 Attendance Modes
Supports Subject Attendance, Classroom Group Attendance, and Reading Room Entry/Exit logging.

## 15 Offline Mode
Devices store attendance locally in an `offline_buffer` during network failures and synchronize once the connection is restored.

## 16 Device–Server Communication
Communication occurs via HTTPS API endpoints for registration, embedding retrieval, and attendance posting.

## 17 Security Measures
Includes device authentication keys, HTTPS encryption, and administrative access controls.

## 18 Performance Design
Targeting 0.2–0.3 seconds per face and a capacity of 8–12 faces per frame.

## 19 Logging System
Detailed logs for device connections, recognition results, and synchronization events are stored for auditing.

## 20 Deployment Strategy
The Central Admin Server hosts the main DB and API, while Recognition Devices are installed at specific campus locations.

## 21 Future Improvements
Planned expansions include GPU acceleration, advanced ANN indexing, and mobile-based recognition.

## 22 Development Rules
Maintain backward compatibility, update documentation before architecture changes, and test FAISS updates rigorously.

## 23 Surveillance-Based Identity Memory ("Mark until Uncover")
### Concept
Repeated recognition of visible faces in crowded halls is inefficient. This system assigns an identity to a **TrackID** and stores it in **Active Identity Memory**. As long as the person is in view, recognition is skipped.

### Visual Feedback & Status Colors
The system uses color-coded boxes for real-time status:
* **Green:** Verified & Accounted (>80% confidence).
* **Blue:** Identified (70-80% confidence).
* **Yellow:** Pending Verification (60-70% confidence).
* **Red:** Unknown / Suspicious (<60% confidence).
* **Black:** Uncovered / Removing from memory.

### Identity Removal & Occlusion
Identity is preserved during temporary occlusion. If a face is not detected for more than 5 seconds (the "Uncover" event), the TrackID is removed from active memory.

## 24 Behavioral Intelligence & Multi-Class Expansion
* **Suspicious Behavior:** The system monitors "Red Box" entities for loitering, intrusion, or erratic movement.
* **Vehicle Tracking:** Future expansion to track bikes and cars using the same "Mark until Uncover" logic, focusing on license plates and vehicle color.
* **Confidence Logging:** MongoDB stores not just "P/A" but the matching percentage for every session to provide an audit trail.

---

**Notes:** This blueprint serves as the master technical document for development upon arrival at the college lab.
