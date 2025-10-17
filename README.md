# **Streamlining Ticket Assignment For Efficient Support Operations**

## **Objective**

The objective of this project is to implement an **automated ticket assignment system** in **ServiceNow** for **ABC Corporation’s support operations**.
This solution automatically routes incoming support tickets to the most suitable teams based on the issue type. The automation is designed to:

* Eliminate manual ticket triage.
* Reduce overall resolution time.
* Improve customer satisfaction through quicker responses.
* Maximize the efficiency of internal support resources.

---

## **Implementation Steps**

### **1. User Setup**

**Navigation:** *ServiceNow → All → Users (under System Security)*

1. Click **New**, enter the required user details, and click **Submit**.
2. Repeat the process to add additional users.

---

### **2. Group Setup**

**Navigation:** *ServiceNow → All → Groups (under System Security)*

1. Click **New**, provide group details, and click **Submit**.
2. Repeat for each required support group.

---

### **3. Role Setup**

**Navigation:** *ServiceNow → All → Roles (under System Security)*

1. Click **New**, specify the role name and description, and click **Submit**.
2. Repeat for all required roles.

---

### **4. Table Creation**

**Navigation:** *ServiceNow → All → Tables (under System Definition)*

1. Click **New**, then enter the following details:

   * **Label:** Operations Related
   * **Enable:** Create Module and Create Mobile Module
   * **Menu Name:** Operations Related
2. Define all necessary table columns and click **Submit**.
3. Configure the **Issue** field with the following choice options:

   * Unable to login to platform
   * 404 Error
   * Regarding Certificates
   * Regarding User Expired

---

### **5. Assign Roles and Users to Groups**

* **Certificates Group:**

  * **Member:** Katherine Pierce
  * **Role:** Certification_Role

* **Platform Group:**

  * **Member:** Manne Niranjan
  * **Role:** Platform_Role

---

### **6. Assign Roles to Table**

**Navigation:** *ServiceNow → Tables → Operations Related Table*
Under **Application Access**, configure as follows:

* **Read Access:** Requires *Platform_Role* or *Certification_Role*
* **Write Access:** Requires *Platform_Role* or *Certification_Role*

---

### **7. Create Access Control Lists (ACLs)**

**Navigation:** *ServiceNow → All → Access Control (ACL) (under System Security)*

1. Create four ACLs to enforce field-level and role-based data access.
2. Under **Requires Role**, add the *admin* role where applicable.

---

### **8. Flow Designer Automation**

#### **Flow 1: Certificates-Related Issues**

* **Flow Name:** Regarding Certificate
* **Application:** Global
* **Run As:** System User
* **Trigger:** When a record is created or updated in the *Operations Related* table
* **Condition:** *Issue = “Regarding Certificates”*
* **Action:** Update *Assigned to Group = Certificates Group*
* **Status:** Saved and Activated

#### **Flow 2: Platform-Related Issues**

* **Flow Name:** Regarding Platform
* **Application:** Global
* **Run As:** System User
* **Trigger:** When a record is created or updated in the *Operations Related* table
* **Condition:** *Issue = “Unable to login to platform” OR “404 Error” OR “Regarding User Expired”*
* **Action:** Update *Assigned to Group = Platform Group*
* **Status:** Saved and Activated

---

## **Project Structure**

```
Streamlining-Ticket-Assignment/
│
├── Users/
│   ├── Katherine Pierce (Certificates Group)
│   └── Manne Niranjan (Platform Group)
│
├── Groups/
│   ├── Certificates Group
│   └── Platform Group
│
├── Roles/
│   ├── Certification_Role
│   └── Platform_Role
│
├── Tables/
│   └── u_operations_related
│       ├── Issue (Choice field)
│       ├── Assigned to Group
│       └── Other custom columns
│
├── Assign Roles and Users to Groups/
│   ├── Certificates Group → Member: Katherine Pierce | Role: Certification_Role
│   └── Platform Group → Member: Manne Niranjan | Role: Platform_Role
│
├── Assign Roles to Table/
│   ├── Read Access → Requires Platform_Role or Certification_Role
│   └── Write Access → Requires Platform_Role or Certification_Role
│
├── ACLs/
│   ├── Read Access (Platform/Certification Roles)
│   ├── Write Access (Platform/Certification Roles)
│   └── Field-Level Restrictions
│
└── Flows/
    ├── Regarding Certificate → Assigns to Certificates Group
    └── Regarding Platform → Assigns to Platform Group
```

---

## **Outcome**

The automated ticket routing solution has transformed ABC Corporation’s support operations by:

* Automatically assigning tickets to the correct support groups.
* Eliminating manual effort in triaging tickets.
* Reducing response and resolution times.
* Increasing customer satisfaction through faster issue handling.
* Ensuring optimal allocation and utilization of internal support resources.

---
