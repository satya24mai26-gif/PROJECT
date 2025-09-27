# 🧠 Smart Attendance Management System (SAMS)

This is an advanced, multi-mode attendance system developed for educational institutions, utilizing **Facial Recognition** with OpenCV and `face_recognition` to automate the attendance process for large groups and specific courses.

## ✨ Key Features

* **Intelligent Attendance Marking:** Automates attendance by matching live camera feed faces against stored student encodings.
* **Three Attendance Modes:**
    * **Group Mode (👥):** Scans and marks multiple students simultaneously against the entire student database.
    * **Course Mode (NEW! 📚):** Matches faces *only* against students enrolled in a selected course, drastically improving speed and relevance during classes.
    * **Single Mode (👤):** Allows focused attendance by searching via **Registration Number** or scanning a **QR Code**.
* **Student Enrollment (📝):** Simple interface to enroll new students by capturing a live photo and recording essential details (Reg No, Name, Course, Mobile).
* **Comprehensive Reports (📊):** View, filter, and export attendance records (CSV/Excel) based on Date, Course, or search query.
* **Database & Tools (🛠):** Built-in utilities for **QR Code generation**, **Database Backup/Restore**, and **Student Management** (view, update, delete records).
* **Theming:** Supports a flexible **Light** and **Dark** theme interface.

---

## ⚙️ Setup and Installation

### Prerequisites

You need **Python 3.x** installed. The system relies on several core libraries, including OpenCV and the `face-recognition` library (which depends on `dlib`).

### Installation Steps

1.  **Clone the Repository:**
    ```bash
    git clone [YOUR_REPO_URL]
    cd smart-attendance-management-system
    ```

2.  **Install Dependencies:**
    Use `pip` to install all required libraries:
    ```bash
    pip install Pillow opencv-python face-recognition pandas qrcode pyzbar
    ```
    *Note: Installing `face-recognition` and `dlib` can be time-consuming, especially on Windows, where you might need C++ build tools.*

---

## 🚀 Getting Started

1.  **Run the System:**
    ```bash
    python vsv.py
    ```

2.  **Initial Run:** The application will automatically initialize the necessary environment:
    * SQLite Database: `students.db`
    * Storage Folders: `photos/` (for student images) and `qrcodes/` (for QR codes)

3.  **Enroll a Student (📝):**
    * Click the **"Enroll Student"** card on the dashboard.
    * Fill in all fields (Reg No, Name, Course, Mobile).
    * Ensure the student's face is clearly visible in the camera frame.
    * Click **"📷 Capture & Save"**.

### Using the Attendance Feature (👥)

Navigate to the **Attendance** window.

| Mode | Use Case | Instructions |
| :--- | :--- | :--- |
| **Group** | General attendance, large crowds, quick entry. | Click **"Reload Faces"**. The system checks all enrolled students. |
| **Course** | Specific class sessions where only enrolled students should be marked. | 1. Select the **Course**. 2. Click **"Load Course Faces"**. *Only* faces from that course are actively matched. |
| **Single** | Verification or individual late entry. | Enter **Reg No** and **Fetch** or click **"Scan QR"** to activate the QR scanner. |

---

## 🛠 Configuration and Tools

### Customization

Key performance and accuracy settings are easily adjustable within the script:

| Variable | Description | Recommended Change |
| :--- | :--- | :--- |
| `TOLERANCE` | Face matching strictness (lower = stricter). | Adjust between `0.35` (stricter) and `0.5` (looser). |
| `REQ_CONSEC` | Frames needed to confirm attendance in Single mode. | Increase for more reliability, decrease for faster marking. |
| `PROCESS_EVERY_N` | Processes 1 in N frames in Group/Course mode for performance. | Increase this value on low-power CPUs. |

### Utilities (🛠)

The **Tools** window provides essential management capabilities:

* **Manage Students:** Allows searching, viewing details, **updating** student information, and **permanently deleting** student records (and all associated attendance data).
* **Database Management:** Use **Backup** to save a copy of `students.db` and **Restore** to load a backup, crucial for data integrity.
* **Data Exports:** Separate functions to export the complete **Student List** and the **Attendance Summary** (count per day).



## app link🖇️
  (coming soon😁)
