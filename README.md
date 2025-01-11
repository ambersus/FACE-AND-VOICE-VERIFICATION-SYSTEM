# Biometric Authentication System (Face and Voice Recognition)

This project implements a two-step biometric authentication system using face recognition and voice password. The system stores and retrieves user data from a MySQL database, and the user is authenticated by verifying both their face and voice password.

### Prerequisites

Before running the application, ensure you have the following libraries and tools installed:

- **Python 3.x**
- **MySQL Database**
- **Libraries:**
  - `opencv-python` (for face recognition)
  - `numpy` (for numerical operations)
  - `mysql-connector-python` (for MySQL database interaction)
  - `SpeechRecognition` (for voice password recognition)
  - `PyAudio` (for microphone access, needed by SpeechRecognition)

You can install the required libraries using pip:

```bash
pip install opencv-python numpy mysql-connector-python SpeechRecognition PyAudio
```

### Setup

1. **MySQL Database Setup:**
   Create a MySQL database named `auth_system` with a `users` table using the following SQL schema:

   ```sql
   CREATE DATABASE auth_system;

   USE auth_system;

   CREATE TABLE users (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(100),
       face_data LONGBLOB,
       voice_password VARCHAR(255)
   );
   ```

2. **Configure Database Connection:**
   In the Python code, update the `DB_CONFIG` dictionary with your MySQL database credentials.

### Features

1. **Face Recognition Registration:**
   - The system uses OpenCV’s Local Binary Patterns Histograms (LBPH) face recognizer to register a user's face.
   - It captures 20 samples of the user’s face and stores the trained face model on the disk.

2. **Voice Password Registration:**
   - Users are prompted to say their voice password, which is then captured and stored in the database.

3. **Two-Step Authentication:**
   - During authentication, the system verifies the user's face and voice password.
   - The user has 20 attempts for face recognition.
   - The system compares the captured voice password with the one stored in the database.

### Usage

1. **Register a New User:**
   - Run the program and select the option to register a new user.
   - The system will prompt you to look into the camera to register your face and then ask you to say your voice password.
   - The face model and voice password will be stored in the database.

2. **Perform Two-Step Authentication:**
   - Select the option for two-step authentication.
   - Enter your name.
   - The system will first try to recognize your face and then ask you to say your voice password.
   - If both the face and voice match, access will be granted.
