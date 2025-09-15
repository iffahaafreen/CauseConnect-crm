# Phase 1: Problem Understanding & Industry Analysis

## 1. Requirement Gathering

### Pain Points (NGO side)
- **Manual donation records (Excel/Email) are prone to errors**  
  Most small to mid-scale NGOs don’t have a centralized system to track and maintain donations. Staff manually input records in spreadsheets or maintain bank receipts in email threads. This can cause:
  - Wrong inputs (human error)
  - Difficulty in tracking recurrent donors
  - Wastage of resources and time

- **Lack of transparency leads to donors dropping off after one-time donations**  
  Donors often don’t receive closure on how their money was used, only acknowledgments with receipts. This reduces trust and forces NGOs to spend extra time finding new donors.

- **No unified donor history makes personalized communication difficult**  
  Scattered donor information prevents NGOs from identifying high-value donors. Mass emails often feel generic, and opportunities for targeted campaigns are missed.

- **Difficult to measure program impact (funds and beneficiaries)**  
  Linking donations to actual outcomes is hard due to manual tracking, subjective observations, or delayed reporting. Donors cannot easily see impact reports.

### Pain Points (Donor side)
- **No visibility into how their donation is used**  
  Donors only receive receipts, not detailed impact reports, which reduces trust.

- **Lack of regular communication/updates**  
  NGOs engage donors mainly around donation events, with little ongoing communication.

- **No personalized experience, treated as “transactional”**  
  High-value donors or donors with specific interests do not get tailored communications.

### Project Requirements
- **Centralized donor management system**  
  Data must be stored in one place, not scattered.

- **Automated donation receipts, acknowledgments, and impact updates**  
  Improves process feasibility, reduces time, and minimizes errors.

- **Donor dashboards showing personalized impact reports**  
  Connects with donors psychologically and represents their individuality.

- **Fundraising campaign management & donor segmentation**  
  Segregates donors for special attention to VIPs.

- **Transparent reports for management & stakeholders**  
  Allows stakeholders to see fund flow and impact in real-time.

---

## 2. Stakeholder Analysis

### Primary Stakeholders
- Donors (Individuals/Corporates)  
- Fundraising Managers  
- Program Managers (NGO staff)  
- NGO Leadership/Board Members  

### Secondary Stakeholders
- Payment Gateway Providers  
- Volunteers/Field Officers  
- Auditors/Regulators  

### Stakeholder to Salesforce Org Representation Mapping

| Stakeholder | Type of User | Profile/Role | What They Do | Access & Permissions |
|------------|-------------|--------------|-------------|-------------------|
| Donors (Individuals / Corporates) | External Users | Portal Profile: Donor | Log in to donor portal to see donations and impact | - Access to Experience Cloud site<br>- Read-only access to their own Donation records<br>- Read-only to their own impact dashboards<br>- Can update their contact info |
| Fundraising Managers | Internal Users | Profile: Fundraising Manager | Manage donation campaigns, segment donors, follow up with leads | - Full CRUD on Donor, Donation, Campaign objects<br>- Run reports & dashboards<br>- Approve large donations<br>- Limited edit access on Program & Beneficiary (read-only mainly) |
| Program Managers (NGO Staff) | Internal Users | Profile: Program Manager | Manage programs and beneficiaries, link funds to impact outcomes | - Full CRUD on Program and Beneficiary<br>- Read access to Donation & Donor<br>- Can upload beneficiary updates and outcomes |
| NGO Leadership / Board | Internal Users | Profile: NGO Leadership (Read Only) | View fundraising performance, donor growth, compliance reports | - Read-only access to all data<br>- Full access to executive dashboards<br>- No record editing |
| Volunteers / Field Officers | Internal Users | Profile: Field Officer | Collect on-ground data about beneficiaries | - Create/Update Beneficiary records<br>- Read-only on Program<br>- No access to Donor personal data |
| Payment Gateway Integration | Integration User (API only) | Profile: API User | Post payment data into Salesforce as donation records | - No UI login<br>- Access to create Donation records via REST API<br>- Read-only access to Donor object |
| Auditors / Regulators | External Users | Portal Profile: Auditor | Periodically review donation and program records for compliance | - Read-only access to Donation, Program, Beneficiary data<br>- Access to selected reports & dashboards via Experience Cloud site |

---

## 3. Business Process Mapping

### Current (As-Is)
- Donor makes donation → staff logs in Excel → acknowledgment email sent manually → no structured follow-up → impact reporting delayed quarterly/annually.

### Future (To-Be with Salesforce)
- Donor makes donation via website → Salesforce auto-creates record → thank-you email triggered instantly → funds linked to specific campaign/program → donor dashboard updated → periodic automated impact updates → management dashboard updated in real time.

### Key Mapped Processes
- **Donation Capture Process** (Web/Social/Offline → Salesforce record)  
- **Fund Allocation Process** (Donation → Campaign → Beneficiary)  
- **Donor Engagement Process** (Acknowledgments, updates, retention workflows)  
- **Reporting Process** (Dashboards for donors, managers, leadership)  

---

## 4. Industry-Specific Use Case Analysis (Non-Profit Sector)
- NGOs are shifting toward impact-driven donor engagement because donors expect clarity on “where did my money go?”  
- Recurring donation programs are growing and require automation for monthly contributions.  
- Corporate Social Responsibility (CSR) compliance requires accurate reporting on fund utilization.  
- Salesforce Nonprofit Success Pack (NPSP) supports many non-profit use cases but needs customization for impact-tracking dashboards and LWC donor portals.  

---

## 5. AppExchange Exploration
A free Salesforce package created specifically for NGOs. It provides a pre-built data model for nonprofits, saving time and offering built-in reports/dashboards. Custom objects can be added to enhance features.

### Recommended Packages / Plugins
- **Nonprofit Success Pack (NPSP):** Pre-built nonprofit data model (Households, Donations, Recurring Gifts)  
- **Donor Management Apps:** Causeview, DonorPerfect connectors  
- **Payment Gateway Connectors:** Stripe, PayPal integrations  
- **Document Management:** Conga Composer, DocuSign for receipts and tax forms
