# Phase 3: Data Modelling & Relationships

## 1. Standard & Custom Objects
For **CauseConnect CRM**, I designed a simple data model using a mix of standard objects (already in Salesforce) and custom objects.

**Standard Objects Used**
- **Contact**: represents donors (individuals)  
- **Campaign**: represents fundraising campaigns (optional, but useful to track donation sources)  
- **User**: represents internal users like Fundraising Manager and Program Manager  

**Custom Objects Created**
- **Program**: represents NGO programs or initiatives  
- **Beneficiary**: represents people/communities supported by programs  
- **Donation**: represents donations made by donors to programs  

Standard objects let me use Salesforce’s built-in features (contacts, reports, campaigns), while custom objects give me full control over NGO-specific data that Salesforce doesn’t provide by default.

---

## 2. Fields
I created specific fields for each custom object to capture the data needed for NGO operations.  

### Program Object
| Field Label      | API Name               | Type      | Notes                  |
|------------------|------------------------|-----------|------------------------|
| Program Name     | Name                   | Text      | Primary name field     |
| Program Start Date | Program_Start_Date__c | Date      | When the program started |
| Program End Date | Program_End_Date__c    | Date      | Optional, when it ended |
| Program Budget   | Program_Budget__c      | Currency  | Estimated budget       |
| Description      | Description__c         | Long Text | About the program      |

### Beneficiary Object
| Field Label      | API Name               | Type                | Notes                        |
|------------------|------------------------|---------------------|------------------------------|
| Beneficiary Name | Name                   | Text (standard)     | Primary name field           |
| Age              | Age__c                 | Number              | Optional demographic info    |
| Gender           | Gender__c              | Picklist            | Male, Female, Other          |
| Contact Number   | Contact_Number__c      | Phone               | --                           |
| Program          | Program__c             | Lookup (Program)    | Links each beneficiary to a program |

### Donation Object
| Field Label      | API Name               | Type                | Notes                        |
|------------------|------------------------|---------------------|------------------------------|
| Donation Name    | Name                   | Text (standard)     | Primary name field           |
| Amount           | Amount__c              | Currency            | Amount donated               |
| Date             | Donation_Date__c       | Date                | When donation was made       |
| Donor (Contact)  | Donor__c               | Lookup (Contact)    | Links donation to donor      |
| Program          | Program__c             | Lookup (Program)    | Shows which program funds are used for |
| Frequency        | Frequency__c           | Picklist            | Frequency of recurring donations |

**Field-Level Security**
- Made fields **Visible (not Read-Only)** for internal profiles: *Fundraising Manager, Program Manager, Field Officer*.  
- Will later restrict field-level access for **external users (Donors, Auditors)**.  

---

## 3. Record Types
I used **record types** to manage different kinds of records within the same object.  

### Donation Object
- **One-Time Donation**: for single contributions  
- **Recurring Donation**: for ongoing pledges  

Two record types let users choose whether a donation is one-time or recurring. Future automation/reports can analyse recurring donations separately.  

### Beneficiary Object
- Considered **Individual vs Group Beneficiaries**.  
- Decided to **keep one record type** for simplicity.  

### Program Object
- Only one record type currently.  
- Future scope: different categories (e.g., *Health* vs *Education*).  

---

## 4. Page Layouts
Customized page layouts for clarity:  
- **Program Layout**: program details (start/end date, budget, description)  
- **Beneficiary Layout**: demographic details, contact information, program lookup  
- **Donation Layouts**:  
  - One layout for *one-time donations*  
  - Another layout for *recurring donations*  
  - Includes donor, amount, date, payment status, related program  

---

## 5. Compact Layouts
Configured compact layouts for quick visibility:  

**Program Compact Layout**
- Program Name  
- Start Date  
- End Date  
- Status  
- Owner  
- Budget  

**Beneficiary Compact Layout**
- Beneficiary Name  
- Age  
- Gender  
- Program  
- Contact Number  

**Donation Compact Layout**
- Donation Name  
- Donor (Contact)  
- Amount  
- Donation Date  
- Payment Status  

---

## 6. Schema Builder
I used **Schema Builder** to visualize object relationships.  

**Relationships**
- **Program → Beneficiary (Lookup):** A program can have many beneficiaries.  
- **Program → Donation (Lookup):** A program can have many donations.  
- **Donation → Contact (Lookup):** A donor (contact) can be linked to many donations.

---

## 7. Relationship Types
- Chose **Lookup relationships** instead of Master-Detail for flexibility.  
- **Lookup**: records can exist independently (e.g., donation without a program).  
- **Master-Detail**: would force dependency, not suitable here.  
- **Hierarchical**: only applies to User object, so not relevant.  

---

## 8. Junction Objects
Currently **not implemented**.  

Potential use case:  
- If one **Beneficiary** can belong to multiple **Programs**, and one **Program** supports multiple **Beneficiaries**, then create a **junction object** called `Program Beneficiary`.  

---

## 9. External Objects
Currently **not implemented**.  

Potential use case:  
- If donation payment data is stored in **external systems (Stripe, PayPal)**, use external objects to surface data inside Salesforce without storing it directly.  
- Ensures **scalability and integration** with third-party services.  

---
