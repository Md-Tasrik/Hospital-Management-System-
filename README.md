# Hospital Management System

A comprehensive, desktop-based hospital management application built with Java, designed to streamline and efficiently manage hospital operations including patient records, doctor information, admissions, and discharges.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [System Architecture](#system-architecture)
- [Technology Stack](#technology-stack)
- [Prerequisites](#prerequisites)
- [Installation Guide](#installation-guide)
- [Configuration](#configuration)
- [Usage Guide](#usage-guide)
- [Project Structure](#project-structure)
- [Key Modules](#key-modules)
- [Database Schema](#database-schema)
- [Security Features](#security-features)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)
- [Author](#author)

---

## Overview

The **Hospital Management System** is a robust desktop application developed to manage and organize hospital operations efficiently. It provides an intuitive user interface for hospital administrators, staff, and medical professionals to:

- Manage patient admissions and discharges
- Maintain comprehensive doctor records
- Track patient medical history
- Generate operational reports
- Ensure secure data access through authentication

This system is particularly designed for small to medium-sized hospitals and can be easily scaled for larger operations. Built with **Java Swing** for the user interface and **MySQL** for persistent data storage, it ensures reliability and ease of deployment across Windows-based systems.

---

## Features

### 👥 Patient Management
- **Admit New Patients**: Register and admit patients with complete medical information
- **View Patient Records**: Access comprehensive patient history and medical details
- **Edit Patient Information**: Update patient records with current health status and treatment plans
- **Discharge Patients**: Process patient discharges with discharge summaries and documentation

### 👨‍⚕️ Doctor Management
- **Add Doctors**: Register new doctors with their specializations and contact information
- **View Doctor Details**: Access doctor profiles and availability
- **Edit Doctor Information**: Update doctor records with current information
- **Remove Doctors**: Archive or remove doctor records from the system

### 🔐 Authentication & Security
- **User Login System**: Secure login portal with username and password validation
- **Role-Based Access**: Different user roles with appropriate access levels
- **Session Management**: Automatic session tracking and logout functionality

### 📊 Data Management
- **Database Integration**: Persistent data storage using MySQL
- **Data Validation**: Input validation to ensure data integrity
- **Record Viewing**: Tabular display of records with search and filter capabilities

### 🎨 User Interface
- **Intuitive Design**: Clean and user-friendly interface using Java Swing
- **Navigation**: Easy-to-use menu system for accessing different modules
- **Visual Feedback**: Dialog boxes and notifications for user actions

---

## System Architecture

```
┌─────────────────────────────────────────────────────┐
│          Hospital Management System                 │
├─────────────────────────────────────────────────────┤
│                                                     │
│  ┌──────────────────────────────────────────────┐  │
│  │       Presentation Layer (Swing GUI)        │  │
│  │  - LoginPage, Welcome, PATIENT, DOCTORS     │  │
│  │  - admitPatient, dischargePatient, etc.     │  │
│  └──────────────────────────────────────────────┘  │
│                        ↓                            │
│  ┌──────────────────────────────────────────────┐  │
│  │     Business Logic Layer                    │  │
│  │  - Data Processing                          │  │
│  │  - Validation                               │  │
│  │  - Navigation                               │  │
│  └──────────────────────────────────────────────┘  │
│                        ↓                            │
│  ┌──────────────────────────────────────────────┐  │
│  │  Data Access Layer (JDBC)                   │  │
│  │  - MySQL Connector                          │  │
│  │  - PreparedStatement & ResultSet            │  │
│  └──────────────────────────────────────────────┘  │
│                        ↓                            │
│  ┌──────────────────────────────────────────────┐  │
│  │     Database Layer (MySQL)                  │  │
│  │  - user_login table                         │  │
│  │  - patient records                          │  │
│  │  - doctor records                           │  │
│  └──────────────────────────────────────────────┘  │
│                                                     │
└─────────────────────────────────────────────────────┘
```

---

## Technology Stack

### Backend
- **Language**: Java (Core)
- **Framework**: Java Swing (GUI Framework)
- **Database**: MySQL 8.0.36 or later
- **JDBC Driver**: MySQL Connector/J 8.3.0

### Frontend
- **GUI Framework**: Java Swing
- **Layout Manager**: AbsoluteLayout, BorderLayout
- **Components**: JFrame, JButton, JTextField, JTable, JDialog

### Database
- **DBMS**: MySQL 8.0+
- **Connection**: JDBC (Java Database Connectivity)

### Development Tools
- **IDE**: NetBeans (nbproject structure detected)
- **Build System**: Standard Java Compilation

### Additional Libraries
- **rs2xml.jar**: For converting ResultSet to XML format (table display enhancement)

---

## Prerequisites

Before installing and running the Hospital Management System, ensure you have the following installed:

### System Requirements
- **Operating System**: Windows 7 or later (macOS and Linux require modifications)
- **RAM**: Minimum 2GB (4GB recommended)
- **Disk Space**: At least 500MB free space

### Software Requirements
1. **Java Development Kit (JDK)** - Version 11 or higher
   - Download from: https://www.oracle.com/java/technologies/javase-downloads.html
   - Set up JAVA_HOME environment variable

2. **MySQL Server** - Version 8.0.36 or compatible
   - Download from: https://dev.mysql.com/downloads/mysql/
   - Installer included in repository: `mysql-installer-web-community-8.0.36.0.msi`

3. **MySQL Connector/J** - Version 8.3.0 or compatible
   - Already included in the repository

4. **Apache NetBeans** (Optional, for development)
   - Download from: https://netbeans.apache.org/

---

## Installation Guide

### Step 1: Install Java Development Kit (JDK)

1. Download JDK from Oracle official website
2. Run the installer and follow on-screen instructions
3. Verify installation by opening Command Prompt and running:
   ```bash
   java -version
   javac -version
   ```

### Step 2: Install and Configure MySQL Server

#### Option A: Using the Installer Included in Repository
1. Navigate to the repository root directory
2. Double-click `mysql-installer-web-community-8.0.36.0.msi`
3. Follow the MySQL installer wizard
4. During configuration:
   - Choose port: `3306` (default)
   - MySQL Server Type: `Development Computer`
   - TCP/IP enabled
   - Default Admin User: `root` with empty password (as per configuration)

#### Option B: Using MySQL Official Installer
1. Download from: https://dev.mysql.com/downloads/mysql/
2. Run the installer
3. Follow similar setup steps as Option A

### Step 3: Set Up the Database

1. Open MySQL Command Line Client or MySQL Workbench
2. Log in as root user:
   ```bash
   mysql -u root -p
   ```
   (Press Enter if no password when prompted)

3. Create the database:
   ```sql
   CREATE DATABASE hms;
   USE hms;
   ```

4. Create the user_login table:
   ```sql
   CREATE TABLE user_login (
       id INT AUTO_INCREMENT PRIMARY KEY,
       username VARCHAR(50) NOT NULL UNIQUE,
       password VARCHAR(50) NOT NULL,
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );
   ```

5. Create the patient table:
   ```sql
   CREATE TABLE patient (
       patient_id INT AUTO_INCREMENT PRIMARY KEY,
       first_name VARCHAR(50) NOT NULL,
       last_name VARCHAR(50) NOT NULL,
       date_of_birth DATE,
       gender VARCHAR(10),
       contact_number VARCHAR(15),
       email VARCHAR(100),
       address TEXT,
       admission_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
       discharge_date TIMESTAMP NULL,
       status VARCHAR(20) DEFAULT 'Active',
       medical_history TEXT
   );
   ```

6. Create the doctor table:
   ```sql
   CREATE TABLE doctor (
       doctor_id INT AUTO_INCREMENT PRIMARY KEY,
       first_name VARCHAR(50) NOT NULL,
       last_name VARCHAR(50) NOT NULL,
       specialization VARCHAR(100),
       contact_number VARCHAR(15),
       email VARCHAR(100),
       experience_years INT,
       qualifications TEXT,
       availability VARCHAR(255),
       hire_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
       status VARCHAR(20) DEFAULT 'Active'
   );
   ```

7. Insert a test user for login:
   ```sql
   INSERT INTO user_login (username, password) VALUES ('admin', 'admin123');
   ```

### Step 4: Set Up the Project

1. **Clone or Download the Repository**
   ```bash
   git clone https://github.com/Md-Tasrik/Hospital-Management-System-.git
   cd Hospital-Management-System-
   ```

2. **Configure JDBC Driver**
   - Ensure MySQL Connector JAR files are in the project classpath:
     - `mysql-connector.jar` - Main connector (included in repository)
     - `mysql-connector-j-8.3.0.zip` - Complete driver package

3. **Compile the Project**
   ```bash
   cd src
   javac hospital/*.java
   ```

4. **Run the Application**
   ```bash
   java hospital.LoginPage
   ```

---

## Configuration

### Database Connection Configuration

The database connection settings are defined in the Java source files. To modify connection parameters, edit the following in each Java file:

**Location in LoginPage.java (Line 112):**
```java
Connection conn=DriverManager.getConnection("jdbc:mysql://localhost/hms","root","");
```

**Parameters:**
- **URL**: `jdbc:mysql://localhost/hms`
  - `localhost`: Database server address (change if remote)
  - `3306`: Default MySQL port (change if configured differently)
  - `hms`: Database name

- **Username**: `root`
  - Change to your MySQL user if different

- **Password**: `` (empty string)
  - Update with your MySQL password if set

### Update Connection String in All Files

Modify the connection string in the following files if your MySQL configuration differs:
- `src/hospital/LoginPage.java`
- `src/hospital/admitPatient.java`
- `src/hospital/dischargePatient.java`
- `src/hospital/editPatient.java`
- `src/hospital/viewrecordsPatient.java`
- `src/hospital/DOCTORS.java`
- `src/hospital/addDoctor.java`
- `src/hospital/editDoctor.java`
- `src/hospital/fireDoctor.java`
- `src/hospital/viewdetailDoc.java`

### Image Path Configuration

The application uses local image paths. Update the image paths in the GUI files if deploying to different systems:

**In LoginPage.java (Line 96):**
```java
jLabel4.setIcon(new javax.swing.ImageIcon("C:\\Users\\HP\\Desktop\\heartrate.jpg"));
```

Change to appropriate image directory in your system, or place images in the `src/hospital/` directory and use:
```java
jLabel4.setIcon(new javax.swing.ImageIcon(getClass().getResource("/hospital/heartrate.jpg")));
```

---

## Usage Guide

### Initial Setup

1. **Start the Application**
   ```bash
   java hospital.LoginPage
   ```

2. **Login Page**
   - Default credentials:
     - **Username**: `admin`
     - **Password**: `admin123`
   - Click "LOGIN" to proceed
   - Click "CLEAR" to reset the form

### Welcome Screen

After successful login, you'll see the welcome screen with two main options:

- **PATIENT'S RECORD**: Manage patient information
- **DOCTOR'S RECORD**: Manage doctor information

### Patient Management Workflow

#### Admit a New Patient
1. Click "PATIENT'S RECORD"
2. Click "ADMIT NEW PATIENT"
3. Enter patient details:
   - First Name
   - Last Name
   - Date of Birth
   - Gender
   - Contact Number
   - Email
   - Address
   - Medical History
4. Click "SUBMIT" to save

#### View Patient Records
1. Click "PATIENT'S RECORD"
2. Click "VIEW PATIENT DETAILS"
3. View all admitted patients in table format
4. Use search functionality to find specific patients

#### Edit Patient Information
1. Click "PATIENT'S RECORD"
2. Click "EDIT PATIENT DETAILS"
3. Select patient from list
4. Update required information
5. Click "UPDATE" to save changes

#### Discharge a Patient
1. Click "PATIENT'S RECORD"
2. Click "DISCHARGE PATIENT"
3. Select patient to discharge
4. Enter discharge date and notes
5. Click "DISCHARGE" to complete

### Doctor Management Workflow

#### Add a New Doctor
1. From welcome screen, click "DOCTOR'S RECORD"
2. Click "ADD DOCTOR"
3. Enter doctor details:
   - First Name
   - Last Name
   - Specialization
   - Contact Number
   - Email
   - Years of Experience
   - Qualifications
4. Click "ADD" to save

#### View Doctor Details
1. Click "DOCTOR'S RECORD"
2. Click "VIEW DOCTOR DETAILS"
3. View all doctors in table format

#### Edit Doctor Information
1. Click "DOCTOR'S RECORD"
2. Click "EDIT DOCTOR"
3. Select doctor from list
4. Update information
5. Click "UPDATE" to save

#### Remove a Doctor
1. Click "DOCTOR'S RECORD"
2. Click "REMOVE DOCTOR"
3. Select doctor to remove
4. Confirm removal

### Navigation Features

- **BACK**: Return to previous screen
- **LOGOUT**: Exit the system and return to login page
- **CLEAR**: Reset form fields

---

## Project Structure

```
Hospital-Management-System-/
│
├── src/
│   └── hospital/
│       ├── LoginPage.java           # Authentication module
│       ├── LoginPage.form           # GUI design file
│       │
│       ├── welcome.java             # Main dashboard
│       ├── welcome.form
│       │
│       ├── PATIENT.java             # Patient management menu
│       ├── PATIENT.form
│       ├── admitPatient.java         # Patient admission
│       ├── admitPatient.form
│       ├── editPatient.java          # Patient edit
│       ├── editPatient.form
│       ├── dischargePatient.java     # Patient discharge
│       ├── dischargePatient.form
│       ├── viewrecordsPatient.java   # View patient records
│       ├── viewrecordsPatient.form
│       │
│       ├── DOCTORS.java             # Doctor management menu
│       ├── DOCTORS.form
│       ├── addDoctor.java            # Add doctor
│       ├── addDoctor.form
│       ├── editDoctor.java           # Edit doctor
│       ├── editDoctor.form
│       ├── fireDoctor.java           # Remove doctor
│       ├── fireDoctor.form
│       ├── viewdetailDoc.java        # View doctor details
│       ├── viewdetailDoc.form
│       │
│       ├── Hospital.java             # Main entry point
│       │
│       └── images/                   # Image assets
│           ├── heartrate.jpg
│           ├── steth.jpg
│           ├── pat wheel.jpg
│           ├── patbed.jpg
│           ├── graphs.jpg
│           ├── fire doc.jpg
│           └── ... (other images)
│
├── build/                           # Compiled bytecode
├── nbproject/                       # NetBeans project files
│
├── mysql-connector.jar              # MySQL JDBC Driver
├── mysql-connector-j-8.3.0.zip      # MySQL Connector source
├── mysql-installer-web-community-8.0.36.0.msi  # MySQL Installer
├── rs2xml.jar                       # ResultSet to XML converter
│
└── README.md                        # This file
```

---

## Key Modules

### 1. **Authentication Module** (`LoginPage.java`)
- Validates user credentials against the database
- Implements secure login with username and password
- Displays error messages for invalid credentials
- Provides clear button to reset form

### 2. **Dashboard Module** (`welcome.java`)
- Provides main navigation menu
- Routes users to patient or doctor management
- Implements logout functionality
- Session management

### 3. **Patient Management Module** (`PATIENT.java`)
- Provides patient-related operations menu
- Routes to specific patient management features
- Patient admission, editing, discharge, and viewing

#### Sub-modules:
- **admitPatient.java**: Patient registration and admission
- **editPatient.java**: Update patient information
- **dischargePatient.java**: Process patient discharge
- **viewrecordsPatient.java**: Display patient records in table format

### 4. **Doctor Management Module** (`DOCTORS.java`)
- Provides doctor-related operations menu
- Routes to specific doctor management features
- Doctor registration, editing, deletion, and viewing

#### Sub-modules:
- **addDoctor.java**: Register new doctors
- **editDoctor.java**: Update doctor information
- **fireDoctor.java**: Remove doctors from system
- **viewdetailDoc.java**: Display doctor profiles

---

## Database Schema

### user_login Table
```sql
CREATE TABLE user_login (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) UNIQUE NOT NULL,
    password VARCHAR(50) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### patient Table
```sql
CREATE TABLE patient (
    patient_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    date_of_birth DATE,
    gender VARCHAR(10),
    contact_number VARCHAR(15),
    email VARCHAR(100),
    address TEXT,
    admission_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    discharge_date TIMESTAMP NULL,
    status VARCHAR(20) DEFAULT 'Active',
    medical_history TEXT
);
```

### doctor Table
```sql
CREATE TABLE doctor (
    doctor_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    specialization VARCHAR(100),
    contact_number VARCHAR(15),
    email VARCHAR(100),
    experience_years INT,
    qualifications TEXT,
    availability VARCHAR(255),
    hire_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    status VARCHAR(20) DEFAULT 'Active'
);
```

---

## Security Features

### Authentication
- User login system with credentials validation
- Secure password handling (stored in database)
- Session-based access control

### Data Protection
- JDBC PreparedStatement usage to prevent SQL injection
- Input validation on all forms
- Error handling with user-friendly messages

### Access Control
- Login required before system access
- Role-based access (can be extended)
- Logout functionality to prevent unauthorized access

### Recommendations for Enhanced Security
1. **Implement Password Hashing**: Use BCrypt or similar algorithms instead of plain text
2. **Add Encryption**: Encrypt sensitive data in the database
3. **Implement Audit Logging**: Track all user actions
4. **Use SSL/TLS**: If deploying over network
5. **Implement Role-Based Access Control (RBAC)**: Different roles for admin, doctors, and staff
6. **Add 2FA**: Two-factor authentication for critical operations

---

## Troubleshooting

### Common Issues and Solutions

#### 1. **MySQL Connection Error**
**Error**: "error while establish connection"

**Solutions**:
- Verify MySQL Server is running
- Check if database `hms` exists
- Confirm connection string in code matches your MySQL configuration
- Ensure MySQL Connector JAR is in classpath
- Verify username and password are correct

```sql
-- Test connection from MySQL CLI
mysql -u root -p -h localhost
USE hms;
SELECT * FROM user_login;
```

#### 2. **"Wrong username and password" Error**
**Solutions**:
- Verify correct username and password
- Ensure user_login table has data
- Check for case sensitivity in credentials
- Verify no extra spaces in input fields

```sql
-- Check existing users
SELECT * FROM user_login;

-- Add new user if needed
INSERT INTO user_login (username, password) VALUES ('newuser', 'password');
```

#### 3. **ClassNotFoundException: com.mysql.cj.jdbc.Driver**
**Solutions**:
- Add MySQL Connector JAR to classpath
- In NetBeans: Right-click Project → Properties → Libraries → Add JAR
- Ensure `mysql-connector.jar` is properly configured

#### 4. **NullPointerException When Loading Images**
**Solutions**:
- Verify image file paths are correct
- Place images in `src/hospital/` directory
- Use relative paths: `new javax.swing.ImageIcon(getClass().getResource("/hospital/imagename.jpg"))`

#### 5. **Table Not Found Error**
**Solutions**:
- Verify all required tables are created
- Check table names match in SQL and Java code
- Ensure database name is correct in connection string

```sql
-- Show all tables in HMS database
USE hms;
SHOW TABLES;
```

#### 6. **Port Already in Use (MySQL)**
**Error**: Port 3306 already in use

**Solutions**:
- Check if MySQL is already running
- Stop existing MySQL process
- Use different port: Modify connection string to `jdbc:mysql://localhost:3307/hms`

#### 7. **Application Won't Start**
**Solutions**:
- Verify Java installation: `java -version`
- Check file permissions
- Ensure all source files are compiled
- Review console output for specific errors
- Check system classpath configuration

### Debug Mode

To run with verbose output:
```bash
java -verbose hospital.LoginPage
```

### Getting Help

1. Check database connectivity:
```sql
mysql -u root -h localhost
STATUS;
```

2. Verify table structure:
```sql
USE hms;
DESCRIBE user_login;
DESCRIBE patient;
DESCRIBE doctor;
```

3. Check application logs (if available)

4. Review MySQL error log: `C:\ProgramData\MySQL\MySQL Server 8.0\Data\*.err`

---

## Future Enhancements

Potential features to be added:

1. **Advanced Features**
   - Appointment scheduling
   - Medical billing system
   - Prescription management
   - Lab report integration

2. **Technical Improvements**
   - Migrate to JavaFX for modern UI
   - Implement MVC architecture properly
   - Add unit tests and integration tests
   - Create REST API backend
   - Implement multi-user concurrent access

3. **Security**
   - Password hashing (BCrypt)
   - Role-based access control (RBAC)
   - Audit logging
   - Data encryption

4. **Reporting**
   - Generate PDF reports
   - Statistical analysis and dashboards
   - Export to Excel/CSV

5. **Deployment**
   - Docker containerization
   - Cloud deployment (AWS, Azure, GCP)
   - Web-based version using Spring Boot

---

## Contributing

Contributions are welcome! To contribute to this project:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Code Style Guidelines
- Follow Java naming conventions (camelCase for variables, PascalCase for classes)
- Add meaningful comments for complex logic
- Use PreparedStatement for all database queries
- Implement proper error handling

---

## License

This project is open source. Feel free to use, modify, and distribute as per your requirements.

---

## Author

**Md-Tasrik**
- GitHub: [@Md-Tasrik](https://github.com/Md-Tasrik)
- Repository: [Hospital-Management-System-](https://github.com/Md-Tasrik/Hospital-Management-System-)

---

## Acknowledgments

- Java Swing Framework documentation
- MySQL official documentation
- NetBeans IDE community
- All contributors and testers

---

## Support

For issues, bugs, or feature requests, please:
- Open an issue on GitHub
- Contact the project maintainer
- Check existing issues for solutions

---

**Last Updated**: June 8, 2026  
**Version**: 1.0  
**Status**: Active Development

---

## Quick Start Command Reference

```bash
# Compile the project
javac -d bin src/hospital/*.java

# Run the application
java -cp "bin:mysql-connector.jar:rs2xml.jar" hospital.LoginPage

# Connect to MySQL
mysql -u root -h localhost

# Create database
mysql> CREATE DATABASE hms;
mysql> USE hms;

# View all tables
mysql> SHOW TABLES;

# Check MySQL status
mysql> STATUS;
```

---

For detailed information, please refer to the inline code documentation and comments within each Java source file.
