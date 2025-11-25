# 🏥 Hospital Management System

A simple, clean, and beginner‑friendly **SQL-based Hospital Management System** designed to demonstrate real‑world database design, relationships, and query handling. This project represents how a small hospital tracks patients, doctors, appointments, room allocations, and admissions.

---

## 🚀 Overview

This project provides a complete relational database system with:

* Patient management
* Doctor management
* Appointment scheduling
* Room allocation
* Patient admissions

It includes:

* Full SQL schema
* Sample data
* ER diagram
* Important SQL queries
* Clear explanations

---

## 📊 ER Diagram

Below is the entity‑relationship diagram (ERD) used to design the system:

https://www.figma.com/board/al1vIYp8ste1e5eMMcaVnE/Hospital-ER-Diagram-Detailed?node-id=0-1&t=ohTrDUKDKabLaosu-1

---

## 📁 Project Structure

```
📦 hospital-management-system
 ┣ 📄 README.md
 ┣ 📄 Queries.sql
 ┣ 📄 InsertionEx.sql
 ┣ 📄 ExampleQueries.sql
 ┗ 🖼️ Hospital ER Diagram Detailed.png
```

---

## 🧱 SQL Schema (Table Definitions)

These are the core tables that make up the system.

### **Patients Table**

```sql
CREATE TABLE Patients (
    patient_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    age INT,
    gender VARCHAR(10),
    phone VARCHAR(15)
);
```

### **Doctors Table**

```sql
CREATE TABLE Doctors (
    doctor_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    specialization VARCHAR(100),
    phone VARCHAR(15)
);
```

### **Appointments Table**

```sql
CREATE TABLE Appointments (
    appointment_id INT PRIMARY KEY AUTO_INCREMENT,
    patient_id INT,
    doctor_id INT,
    appointment_date DATE,
    appointment_time TIME,
    reason VARCHAR(255),

    FOREIGN KEY (patient_id) REFERENCES Patients(patient_id),
    FOREIGN KEY (doctor_id) REFERENCES Doctors(doctor_id)
);
```

### **Rooms Table**

```sql
CREATE TABLE Rooms (
    room_id INT PRIMARY KEY AUTO_INCREMENT,
    room_number VARCHAR(10),
    room_type VARCHAR(50),     -- General, Private, ICU
    is_occupied BOOLEAN DEFAULT FALSE
);
```

### **Admissions Table**

```sql
CREATE TABLE Admissions (
    admission_id INT PRIMARY KEY AUTO_INCREMENT,
    patient_id INT,
    room_id INT,
    admit_date DATE,
    discharge_date DATE,

    FOREIGN KEY (patient_id) REFERENCES Patients(patient_id),
    FOREIGN KEY (room_id) REFERENCES Rooms(room_id)
);
```

---

## 🧪 Sample Inserts

```sql
-- Patients
INSERT INTO Patients (name, age, gender, phone)
VALUES
('Rahul Sharma', 35, 'Male', '9876543210'),
('Priya Singh', 28, 'Female', '8877665544'),
('Amit Verma', 42, 'Male', '9998887776');

-- Doctors
INSERT INTO Doctors (name, specialization, phone)
VALUES
('Dr. Priya Mehta', 'Cardiology', '9823456789'),
('Dr. Rohan Das', 'Orthopedics', '9855544332'),
('Dr. Sneha Nair', 'Dermatology', '9944332211');

-- Rooms
INSERT INTO Rooms (room_number, room_type)
VALUES
('101', 'General'),
('201', 'Private'),
('301', 'ICU');

-- Appointments
INSERT INTO Appointments (patient_id, doctor_id, appointment_date, appointment_time, reason)
VALUES
(1, 1, '2025-01-10', '10:30:00', 'Heart checkup'),
(2, 2, '2025-01-11', '12:00:00', 'Knee pain'),
(3, 3, '2025-01-12', '15:00:00', 'Skin allergy');

-- Admissions
INSERT INTO Admissions (patient_id, room_id, admit_date, discharge_date)
VALUES
(1, 1, '2025-01-09', NULL),
(3, 3, '2025-01-11', NULL);
```

---

## 🔍 Useful Queries

### **1. List all appointments with patient and doctor names**

```sql
SELECT
    a.appointment_id,
    p.name AS patient,
    d.name AS doctor,
    a.appointment_date,
    a.appointment_time
FROM Appointments a
JOIN Patients p ON a.patient_id = p.patient_id
JOIN Doctors d ON a.doctor_id = d.doctor_id;
```

### **2. Get all available rooms**

```sql
SELECT room_number, room_type
FROM Rooms
WHERE is_occupied = FALSE;
```

### **3. Patient visit history**

```sql
SELECT
    p.name AS patient,
    d.name AS doctor,
    a.appointment_date,
    a.reason
FROM Appointments a
JOIN Patients p ON a.patient_id = p.patient_id
JOIN Doctors d ON a.doctor_id = d.doctor_id
ORDER BY a.appointment_date DESC;
```

### **4. List all admitted patients with room details**

```sql
SELECT
    p.name AS patient,
    r.room_number,
    a.admit_date
FROM Admissions a
JOIN Patients p ON a.patient_id = p.patient_id
JOIN Rooms r ON a.room_id = r.room_id;
```

### **5. Count appointments per doctor**

```sql
SELECT
    d.name AS doctor,
    COUNT(*) AS total_appointments
FROM Appointments a
JOIN Doctors d ON a.doctor_id = d.doctor_id
GROUP BY d.name;
```

---

## ▶️ How to Run This Project

1. Install **MySQL** or **MariaDB**.
2. Import the schema:

```bash
mysql -u root -p < Queries.sql
```

3. Insert sample data:

```bash
mysql -u root -p < InsertionEx.sql
```

4. Execute the example queries or test your own.

---

## 📘 What I Learned

* Designing a clean relational database
* Creating ER diagrams and mapping relationships
* Working with primary & foreign keys
* Understanding 1‑to‑many relationships
* Writing useful SQL queries (JOIN, GROUP BY, ORDER BY)
* Organizing a project in a professional, developer‑friendly way

---

## ⭐ Final Notes

This project is simple, clear, and intentionally beginner‑friendly — but structured to look clean, professional, and real‑world ready. If you’re exploring SQL and relational design, this is a strong foundational project to showcase.
