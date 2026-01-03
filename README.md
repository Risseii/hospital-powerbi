# Hospital Performance Analysis: María Auxiliadora Hospital (2023)

[![Español](https://img.shields.io/badge/Leer%20en-Español-71bcf0?style=for-the-badge&logo=es-spain&logoColor=white)](README-es.md)

## 1. Introduction
This project presents an analysis of medical appointment management at María Auxiliadora Hospital. The main objective is to transform data into strategic information to optimize hospital management and improve the quality of patient care by monitoring key performance indicators (KPIs).
## 2. 🔍 The problem
María Auxiliadora Hospital has a serious problem with missed appointments: many patients book an appointment but do not show up for their consultation. Currently, some consultation rooms are operating empty because no one attends, which results in a significant loss of medical time, while other patients continue to wait weeks to be seen.

**Key business questions:**
- Which specialties have the biggest bottlenecks in waiting times?
- Which areas require immediate intervention to reduce appointment abandonment?
- Is there a profile associated with the highest rates of non-attendance?
- Which specialties generate the most revenue?
## 3. 🛠️ Technology Stack
- **BI tool:** Power BI Desktop.
- **Data source:** Excel.
- **DAX:** For calculating measures.
## 4. 🔄 Data Processing (ETL)
- **Cleaning:** Removal of duplicate records and purging of irrelevant columns to optimize model weight.
- **Time Intelligence:** Creation of a calendar table, designed to analyze specific trends for the 2023 period.
## 5. ⚙️ Data Modeling
Implementation of a Star Schema, facilitating scalability and query speed.
- **Fact Table (Fact_Appointments):** Contains appointment events, costs, and care status.
- **Dimensions:**
  - Dim_Calendar: For analysis of temporal trends (month, day of the week).
  - Dim_Specialty: Attributes of medical units.
  - Dim_Patient: Demographic data.
## 6. 📊 Key Performance Indicators (KPIs)
- **Care Efficiency:** Attendance rate vs. no-show rate.
- **Patient Volume:** Total number of visits segmented by gender.
- **Timeliness of Care:** Average waiting time (days) from request to appointment.
- **No-show rate by specialty:** Analysis of specialties with a 100% no-show rate, allowing for the detection of areas where the
availability of appointments does not translate into actual care.
- **Financial Impact:** Top 5 total revenue by specialty.
## 7. 🚀 Business Insights
- 📌 **A pattern was identified in the top 3 specialties with the longest wait times:**
  + The first (pediatric dermatology) and third (pediatric neurology) specialties with the longest wait times have a 100% no-show rate.
  + The second specialty with the longest wait (physical medicine) has a 98.1% no-show rate.
- 📌 **Alert in physical medicine and rehabilitation:** This specialty is in a critical situation with a no-show rate of 98.10%
(17,332 patients lost). In addition, it is in the Top 3 in terms of waiting time with an average of 43 days, suggesting that the long wait
discourages final attendance.
- 📌 **Anomalies in Pediatric Specialties:** Pediatric Dermatology and 17 other areas (including Nutrition and Mental Health) recorded a
100% non-attendance rate. In the case of pediatric dermatology, the average waiting time is 59 days.
- 📌 **Anomaly in pediatric dermatology:** A pattern of non-attendance was detected on January 31, 2023, where 100% of patients
(14 appointments) scheduled specifically on Tuesdays did not attend. This finding suggests an operational disconnect, such as an error in communicating the specialist's availability or an administrative closure not recorded in the appointment system, resulting in a
total loss of efficiency for that shift.
- 📌 **Financial Performance:** Despite attendance issues, the specialties of Ophthalmology, Psychiatry, and Cardiology lead
in revenue, consolidating themselves as the economic pillars of the hospital during the period analyzed.
## 8. 📊 Dashboard preview
- Page 1: Executive summary of hospital performance.
  <img width="1600" height="900" alt="Maria Auxiliadora Hospital Dashboard" src="https://github.com/user-attachments/assets/27bcd110-5bc5-4e47-b66f-2c3298d7da28" />
- Page 2: Further analysis.
  <img width="1920" height="1080" alt="Maria Auxiliadora Hospital Dashboard (1)" src="https://github.com/user-attachments/assets/4bd2ce63-7504-4d4c-b1db-21a97f1780a3" />

## 9. Conclusions and Recommendations
- **Intervention in critical cases:** It was identified that the problem of extreme waiting times (greater than 36 days) is concentrated in
three specialties: pediatric dermatology, physical medicine and rehabilitation, and pediatric neurology. An audit is recommended in
these areas to determine whether the delay is due to a lack of medical staff, an oversupply of appointments, or another reason.
- **Reminder System:** Implement alerts (SMS/WhatsApp) specifically in the 18 specialties with total abandonment
and in the specialty of Physical Medicine and Rehabilitation.
- **Synchronization of Medical Schedules:** It is necessary to audit specialties with perfect attendance during specific periods to
ensure that the appointment system schedules coincide with the actual availability of physicians, thus preventing patients from
occupying slots on days when the service is not operational.
- **Resource optimization:** Reassign staff from specialties with 100% non-attendance to areas of greater demand and revenue, thus maximizing the use of hospital infrastructure.
  
## 10. Limitations
During the development of the project, a discrepancy was identified in the Attended column:
The dataset defines the field with Yes or No values; however, in the data dictionary, the field is described as Came or Did Not Come (Attendance).
- **Impact on Analysis:** There is an interpretation gap between patient responsibility (not attending the appointment) and hospital management (the patient attended but was not seen due to lack of doctor, time, or supplies).
- **Technical Decision:** For the purposes of this dashboard, the field has been assumed to be Attendance. However, it is recommended that this field be standardized at the source to differentiate non-attendance.
