# Hospital Management System - Architecture

## 1. Project Title
**Hospital Management System**

## 2. Domain
**Healthcare Industry**

### 2.1 Description
The Hospital Management System streamlines hospital operations such as patient registration, doctor appointments, medical record management, billing, and reporting. The system will be cloud-based, ensuring scalability and security.

## 3. Problem Statement

Manual management of hospital data often results in inefficiencies, errors, and delays. The system aims to:
- Improve appointment scheduling.
- Ensure secure and efficient handling of patient records.
- Automate billing to prevent financial discrepancies.

## 4. Scope & Feasibility

### 4.1 Technology Stack
- **Frontend**: React.js
- **Backend**: Node.js with Express.js
- **Database**: MongoDB
- **Security**: JWT for authentication
- **Deployment**: Cloud-based (AWS/Firebase)
- **Payment Gateway**: Integrated for secure payment processing

### 4.2 C4 Diagrams

#### **C4 Context: Hospital Management System Context**

```mermaid
C4Context
  title Hospital Management System Context
  Person(patient, "Patient", "Schedules appointments, views medical records, and makes payments")
  Person(doctor, "Doctor", "Manages patient records, schedules, and medical history")
  Person(admin, "Admin", "Oversees hospital operations, appointments, and billing")
  System(hms, "Hospital Management System", "Digitizes hospital workflows, manages appointments, medical records, and billing")
  System_Ext(paymentGateway, "Payment Gateway", "Processes payments securely for medical bills")
  System_Ext(labService, "Laboratory Service", "Handles lab test orders and results processing")
  System_Ext(notificationService, "Notification System", "Sends appointment reminders and medical updates")
  
  Rel(patient, hms, "Schedules appointments, views records, and pays bills")
  Rel(doctor, hms, "Manages patient medical history and schedules appointments")
  Rel(admin, hms, "Oversees operations, billing, and patient management")
  Rel(hms, paymentGateway, "Processes medical bill payments")
  Rel(hms, labService, "Sends and retrieves lab test results")
  Rel(hms, notificationService, "Sends appointment reminders and notifications")
```

```mermaid
C4Container
  title Hospital Management System - Containers
  Person(patient, "Patient", "Schedules appointments and views medical records")
  Person(doctor, "Doctor", "Manages patient records and appointments")
  System_Boundary(hms, "Hospital Management System") {
    Container(webApp, "Web Application", "React.js", "User interface for patients and doctors")
    Container(backendAPI, "Backend API", "Node.js/Express", "Processes hospital operations and business logic")
    ContainerDb(database, "Database", "MongoDB", "Stores patient data, appointments, and billing records")
  }
  System_Ext(thirdPartyBilling, "Third-Party Billing System", "Processes insurance claims and payments")
  System_Ext(notificationService, "Notification Service", "Sends appointment reminders and alerts")
  Rel(patient, webApp, "Interacts to book appointments and view records")
  Rel(doctor, webApp, "Manages patient records and schedules")
  Rel(webApp, backendAPI, "Sends and retrieves data")
  Rel(backendAPI, database, "Stores and retrieves hospital data")
  Rel(backendAPI, thirdPartyBilling, "Handles insurance claims and payments")
  Rel(backendAPI, notificationService, "Sends notifications and reminders")
```

```mermaid

C4Component
  title Hospital Management System - Backend API Components
  Container_Boundary(backendAPI, "Backend API") {
    Component(auth, "Authentication Service", "JWT", "Handles user authentication and authorization")
    Component(appointmentService, "Appointment Management Service", "Node.js", "Schedules and manages appointments")
    Component(patientRecords, "Patient Records Service", "MongoDB", "Stores and retrieves patient medical data")
    Component(billingService, "Billing Service", "Express.js", "Processes invoices and payments")
    Component(notificationService, "Notification Service", "Email/SMS API", "Sends appointment reminders")
  }
  Rel(auth, appointmentService, "Secures appointment scheduling")
  Rel(appointmentService, patientRecords, "Links appointments with patient records")
  Rel(billingService, patientRecords, "Handles billing for medical procedures")
  Rel(notificationService, appointmentService, "Sends appointment reminders")
  Rel(patientRecords, notificationService, "Notifies patients about test results and updates")

```
