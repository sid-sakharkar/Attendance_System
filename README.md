# 🎓 Face Recognition & QR Code Based Attendance Management System

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-4.x-green?logo=opencv)
![MySQL](https://img.shields.io/badge/MySQL-8.0-orange?logo=mysql&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-purple)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

A smart, automated attendance management system that combines **facial recognition** and **QR code scanning** to accurately and securely mark student attendance — powered by Python, OpenCV, and MySQL.

---

## 📸 Screenshots

> Terminal Interface — Main Menu

```
1. Register Student and capture image
2. Take Attendance
3. Exit
Enter your choice:
```

> Student registered successfully with ID: 101
> QR code generated and saved as D:\Minor-project\qr_code_details\101.png

---

## ✨ Features

- 👤 **Student Registration** — Registers student name, age, gender, and email into MySQL
- 📷 **Live Image Capture** — Uses webcam to capture and store student face images
- 🔍 **Face Recognition** — Identifies students via `face_recognition` library during attendance
- 🔲 **QR Code Generation** — Auto-generates unique QR codes per student on registration
- ✅ **Dual Verification** — Attendance is marked only after both face match AND QR scan succeed
- 🗄️ **MySQL Integration** — All student records and attendance logs stored in a relational database
- 🕐 **Timestamped Records** — Captures exact date and in-time for each attendance entry

---

## 🗂️ Project Structure

```
Minor-project/
│
├── main.py                        # Main application file
├── student_image_details/         # Stored student face images (named by student ID)
│   ├── 101.jpg
│   └── 102.jpg
├── qr_code_details/               # Generated QR codes (named by student ID)
│   ├── 101.png
│   └── 102.png
└── README.md
```

---

## 🛠️ Tech Stack

| Technology        | Purpose                         |
|-------------------|---------------------------------|
| Python 3.8+       | Core programming language       |
| OpenCV (`cv2`)    | Webcam feed & QR code detection |
| face_recognition  | Face encoding & matching        |
| MySQL             | Database for students & attendance |
| mysql-connector   | Python-MySQL bridge             |
| qrcode            | QR code image generation        |
| NumPy             | Face distance calculations      |

---

## 🗄️ Database Schema

### `students` Table

```sql
CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    name       VARCHAR(100),
    age        INT,
    gender     VARCHAR(10),
    email      VARCHAR(100)
);
```

### `attendance` Table

```sql
CREATE TABLE attendance (
    id         INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    date       DATE,
    in_time    TIME,
    FOREIGN KEY (student_id) REFERENCES students(student_id)
);
```

---

## ⚙️ Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/attendance-management-system.git
cd attendance-management-system
```

### 2. Install Dependencies

```bash
pip install opencv-python face_recognition mysql-connector-python qrcode numpy
```

> ⚠️ `face_recognition` requires `dlib`. On Windows, install Visual Studio Build Tools or use a prebuilt wheel.
> On Linux/macOS: `pip install dlib` should work directly.

### 3. Configure MySQL

- Create a database named `attendance-management-system`
- Run the SQL schema above to create required tables
- Update your credentials in `main.py`:

```python
conn = mysql.connector.connect(
    host="localhost",
    user="your_username",
    password="your_password",
    database="attendance-management-system"
)
```

### 4. Set Image & QR Code Directories

Update these paths in `main.py` to match your system:

```python
image_dir   = r"path\to\student_image_details"
qr_code_dir = r"path\to\qr_code_details"
```

Make sure both folders exist before running:

```bash
mkdir student_image_details
mkdir qr_code_details
```

### 5. Run the Application

```bash
python main.py
```

---

## 🚀 How It Works

### Registering a Student

1. Run the app and choose **Option 1**
2. Enter student details (name, age, gender, email)
3. The student is saved to the `students` table with an auto-generated ID
4. Webcam opens — press **SPACE** to capture the student's face photo
5. A unique QR code is generated and saved automatically

### Marking Attendance

1. Choose **Option 2**
2. Webcam opens — press **SPACE** to capture the student's live face
3. The system compares the face against all stored images using face encodings
4. If a match is found, the webcam re-opens for QR code scanning
5. The student holds up their QR code — if it matches the recognized student ID, attendance is marked
6. Record with `student_id`, `date`, and `in_time` is inserted into the `attendance` table

---

## 📋 Usage Flow Diagram

```
Start
  │
  ├── [1] Register Student
  │       ├── Input Details → Save to DB
  │       ├── Capture Face → Save as {student_id}.jpg
  │       └── Generate QR Code → Save as {student_id}.png
  │
  ├── [2] Mark Attendance
  │       ├── Capture Live Face → Face Recognition
  │       ├── Match Found? ──No──→ "Face not recognized"
  │       │        │
  │       │       Yes
  │       │        ↓
  │       ├── Scan QR Code → Verify Student ID
  │       └── Insert attendance record (student_id, date, in_time)
  │
  └── [3] Exit
```

---

## ⚠️ Known Limitations

- Attendance is marked on first successful QR scan in each session; the webcam does not auto-close
- Face recognition accuracy may decrease in poor lighting conditions
- Currently supports one face per image capture (group attendance not supported)
- Windows paths are hardcoded — update for cross-platform use

---

## 🔮 Future Improvements

- [ ] GUI interface using Tkinter or PyQt5
- [ ] Automated daily attendance reports (PDF/Excel export)
- [ ] Email notification on successful attendance
- [ ] Web dashboard for teachers/admins
- [ ] Multiple face detection for group photos
- [ ] Liveness detection to prevent photo spoofing

---

## 👨‍💻 Author

**Your Name**
- GitHub: [@your-username](https://github.com/your-username)
- Email: your.email@example.com

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
[output_screenshots.html](https://github.com/user-attachments/files/25779826/output_screenshots.html)

---

> ⭐ If you found this project helpful, please give it a star!
