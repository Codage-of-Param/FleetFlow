# 📙 TECHNICAL REQUIREMENT DOCUMENT (TRD)

---

## 1️⃣ System Architecture

### 🖥 Frontend
- Odoo XML Views  
- Kanban View  
- Tree View  
- Form View  

### ⚙ Backend
- Python (Odoo ORM)  
- Automated state transitions  
- Validation using `@api.constrains`  

### 🗄 Database
- PostgreSQL (Odoo default database)

---

## 2️⃣ Database Schema

### 🚛 Vehicle Table

| Field            | Type       |
|------------------|------------|
| id               | PK         |
| name             | Char       |
| license_plate    | Unique     |
| max_capacity     | Float      |
| odometer         | Float      |
| acquisition_cost | Float      |
| status           | Selection  |

---

### 👨‍✈️ Driver Table

| Field          | Type      |
|---------------|----------|
| id            | PK       |
| name          | Char     |
| license_number| Char     |
| license_expiry| Date     |
| safety_score  | Float    |
| status        | Selection|

---

### 📦 Trip Table

| Field        | Type       |
|-------------|------------|
| id          | PK         |
| vehicle_id  | Many2One   |
| driver_id   | Many2One   |
| cargo_weight| Float      |
| distance    | Float      |
| revenue     | Float      |
| status      | Selection  |

---

### 🔧 Maintenance Table

| Field        | Type     |
|-------------|----------|
| id          | PK       |
| vehicle_id  | Many2One |
| service_type| Char     |
| cost        | Float    |
| date        | Date     |

---

### ⛽ Fuel Log Table

| Field      | Type     |
|-----------|----------|
| id        | PK       |
| vehicle_id| Many2One |
| trip_id   | Many2One |
| liters    | Float    |
| cost      | Float    |
| date      | Date     |

---

## 3️⃣ State Management Logic

### 🚛 Vehicle States
```
Available → On Trip → Available  
Available → In Shop → Available  
Available → Retired (Final)
```

### 👨‍✈️ Driver States
```
On Duty → On Trip → On Duty  
On Duty → Suspended
```

---

## 4️⃣ Validation Logic (Backend)

- Capacity validation  
- License expiry check  
- Driver status check  
- Vehicle availability check  

If violated → Raise `ValidationError`

---

## 5️⃣ Computed Fields

- total_operational_cost  
- cost_per_km  
- fuel_efficiency  
- vehicle_roi  
- utilization_rate  
- trip_completion_rate  

Use `@api.depends` decorator for computed fields.

---

## 6️⃣ Security Model

Use:

- `security.xml`  
- Access Control Lists (ACLs)  
- Record Rules  

**Example:**  
Dispatcher cannot modify financial data.

---

## 7️⃣ Reporting Engine

- Use Odoo QWeb for PDF reports  
- Export CSV using Odoo export functionality  

---

## 8️⃣ Real-Time Data Integrity Rules

- Maintenance automatically updates vehicle status  
- Completing trip updates odometer  
- State transitions controlled via action buttons  

---

## 9️⃣ Performance Considerations

- Index `license_plate`  
- Index `vehicle_id` in trips  
- Use computed stored fields where required  

---

## 🔟 Risk & Edge Case Handling

| Risk              | Handling          |
|-------------------|------------------|
| Overload          | Hard validation  |
| Expired License   | Block assignment |
| Double Assignment | Status check     |
| Missing Expense   | Mandatory fields |
| Negative ROI      | Allowed but reported |

---