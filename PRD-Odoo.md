# 📘 PRODUCT REQUIREMENT DOCUMENT (PRD)

## 🏷 Product Name
# FleetFlow – Modular Fleet & Logistics Management System

---

## 1️⃣ Product Overview

FleetFlow is a centralized, rule-based digital fleet management system designed to replace manual logbooks and optimize:

- Fleet lifecycle management  
- Driver compliance & safety  
- Trip dispatch operations  
- Financial & operational analytics  

The system ensures automated validation, real-time state updates, and data-driven decision-making.

---

## 2️⃣ Problem Statement

Manual fleet tracking leads to:

- Inaccurate trip records  
- Overloaded vehicles  
- Expired license risks  
- Poor maintenance tracking  
- No financial transparency  

FleetFlow solves these issues by enforcing:

- Automated validation rules  
- Role-based access control  
- State-based workflow management  
- Financial performance tracking  

---

## 3️⃣ Target Users

| Role              | Responsibilities                          |
|-------------------|--------------------------------------------|
| Fleet Manager     | Monitor fleet health & utilization        |
| Dispatcher        | Assign trips & validate loads             |
| Safety Officer    | Monitor driver compliance                 |
| Financial Analyst | Track cost, ROI & performance             |

---

## 4️⃣ Functional Requirements

### 🔐 4.1 Authentication & Authorization

**Features:**

- Role-Based Access Control (RBAC)  
- Login / Logout  
- Password reset  
- Permission-based module visibility  

**Roles:**

- Manager  
- Dispatcher  
- Safety Officer  
- Financial Analyst  

---

### 📊 4.2 Dashboard (Command Center)

**KPIs:**

- Active Fleet Count  
- Maintenance Alerts  
- Utilization Rate  
- Pending Cargo  

**Formula:**

```
Utilization Rate = (Active Vehicles / Total Vehicles) × 100
```

**Filters:**

- Vehicle Type  
- Status  
- Region  

---

### 🚛 4.3 Vehicle Registry (Asset Management)

**CRUD Operations:**

- Add Vehicle  
- Update Vehicle  
- Deactivate / Retire  

**Fields:**

- Name / Model  
- License Plate (Unique)  
- Max Load Capacity  
- Odometer  
- Acquisition Cost  
- Status (Available / On Trip / In Shop / Retired)  

**Business Rules:**

- License plate must be unique  
- Retired vehicle cannot be assigned  
- In Shop vehicle cannot be dispatched  

---

### 📦 4.4 Trip Management

**Trip Lifecycle:**

```
Draft → Dispatched → Completed → Cancelled
```

**Required Validations:**

- Cargo Weight Rule  
- Driver License Validity  
- Driver Status must be "On Duty"  
- Vehicle Status must be "Available"  

**Status Automation:**

When trip = **Dispatched**:
- Vehicle → On Trip  
- Driver → On Trip  

When trip = **Completed**:
- Vehicle → Available  
- Driver → On Duty  

---

### 🔧 4.5 Maintenance Management

**Features:**

- Log Service  
- Preventive Maintenance  
- Record Cost  

**Business Logic:**

- If Maintenance Log Created → Vehicle Status = In Shop  
- If Maintenance Completed → Vehicle Status = Available  

---

### ⛽ 4.6 Fuel & Expense Logging

**Fields:**

- Liters  
- Cost  
- Date  
- Vehicle ID  
- Trip ID (optional)  

**Calculations:**

```
Total Operational Cost = Fuel Cost + Maintenance Cost + Other Expenses

Cost Per KM = Total Operational Cost / Total Distance Traveled
```

---

### 👨‍✈️ 4.7 Driver Performance

**Fields:**

- License Number  
- License Expiry  
- Safety Score  
- Status (On Duty / Off Duty / Suspended)  

**Performance Metrics:**

```
Trip Completion Rate = (Completed Trips / Assigned Trips) × 100
```

**Blocked if:**

- Suspended  
- License expired  
- Off duty  

---

### 📈 4.8 Analytics & Reporting

**Metrics:**

- Fuel Efficiency  
- Vehicle ROI  

**Exports:**

- CSV  
- PDF  

---

## 5️⃣ Workflow Summary

```
Add Vehicle → Available  
Add Driver → Validate License  
Create Trip → Validate Capacity & Status  
Dispatch → Update State  
Complete Trip → Update Odometer  
Log Fuel & Expense  
Log Maintenance → Auto State Change  
Dashboard Updates  
```

---

## 6️⃣ Non-Functional Requirements

- Real-time status update  
- Relational database integrity  
- High data consistency  
- Secure access control  
- Scalable modular architecture  

---

## 7️⃣ Success Metrics

- Zero overloaded trips  
- Zero expired license assignments  
- Accurate cost tracking  
- Real-time fleet visibility  

---