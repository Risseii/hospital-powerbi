# Hospital Performance Analysis: María Auxiliadora Hospital (2023)

[![Español](https://img.shields.io/badge/Leer%20en-Español-71bcf0?style=for-the-badge&logo=es-spain&logoColor=white)](README-es.md)

## 1. Introduction
This project presents an analysis of medical appointment management at María Auxiliadora Hospital. The main objective is to transform data into strategic information to optimize hospital management and improve the quality of patient care by monitoring key performance indicators (KPIs).

## 2. 🔍 The problem
María Auxiliadora Hospital has a serious problem with missed appointments: many patients book an appointment but do not show up for their consultation. In 2023, 143,646 of 450,629 appointments (31.9%) were not attended. Some consultation rooms operate empty because no one attends, which results in a significant loss of medical time, while other patients continue to wait weeks to be seen.

**Key business questions:**
- Which specialties have the biggest bottlenecks in waiting times?
- Which areas require immediate intervention to reduce appointment abandonment?
- Does a longer wait lead to more no-shows?
- How does no-show behave by month and day of the week within each specialty?
- Which specialties generate the most revenue?

## 3. 🛠️ Technology Stack
- **BI tool:** Power BI Desktop.
- **Data source:** CSV file with 2023 appointments, plus an Excel data dictionary.
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
- **Value of missed appointments:** Revenue not collected from appointments that were not attended (S/ 1.62 million in 2023).
- **No-show rate:** Share of booked appointments that were not attended (31.9%). Each specialty is compared against this hospital average.
- **Attended appointments and unique patients:** 306,983 attended appointments from 73,625 unique patients, an average of 4.2 appointments per patient.
- **Timeliness of Care:** Average waiting time from request to appointment (19.8 days), shown together with the median (17 days) because a few very long waits pull the average up.
- **Financial Impact:** Top N specialties by revenue from attended appointments.

**Ranking rules:** The no-show and waiting time rankings only include specialties with at least 100 appointments and at least one attended appointment, so that small or inactive units do not distort the comparison. The 17 specialties with no attended appointments in 2023 (20,212 appointments) are reported in a separate view.

## 7. 🚀 Business Insights
- 📌 **Longest waits:** Among specialties with real activity, Physical Medicine and Rehabilitation (43 days), Endocrinology (33 days) and Rheumatology (30 days) have the longest average waiting times.
- 📌 **Alert in Physical Medicine and Rehabilitation:** This specialty is in a critical situation, with a no-show rate of 98.1% (17,332 missed appointments) and the longest average wait (43 days), which suggests that the long wait discourages attendance.
- 📌 **Wait and no-show are only weakly related:** Across specialties, the correlation between average waiting time and no-show rate is r = 0.23. Waiting time alone does not explain no-shows, so other causes should be reviewed by specialty.
- 📌 **Specialties with no recorded attendance:** 17 specialties, including Nutrition and Endocrinology, Mental Health, High-risk Gynecology, Pediatric Neurology and Pediatric Dermatology, did not record a single attended appointment in 2023 (20,212 appointments). Pediatric Dermatology also has the longest average wait in the hospital (59 days).
- 📌 **Anomaly in Pediatric Dermatology:** A pattern of non-attendance was detected on January 31, 2023, where 100% of patients (14 appointments) scheduled specifically on Tuesdays did not attend. This finding suggests an operational disconnect, such as an error in communicating the specialist's availability or an administrative closure not recorded in the appointment system, resulting in a total loss of efficiency for that shift.
- 📌 **Obstetrics above the hospital average every month:** Its no-show rate is 55.5% versus 31.9% for the hospital, and it stays above the average in all 12 months of 2023.
- 📌 **Financial Performance:** Despite attendance issues, Ophthalmology, Psychiatry and Cardiology lead in revenue, consolidating themselves as the economic pillars of the hospital during the period analyzed.

## 8. 📊 Dashboard preview
- **Page 1, Performance:** Executive summary with the four KPIs and the ranking of specialties with the highest no-show rate. A button switches to the specialties with no recorded attendance.
  <img width="1600" height="900" alt="Maria Auxiliadora Hospital Dashboard" src="https://github.com/user-attachments/assets/27bcd110-5bc5-4e47-b66f-2c3298d7da28" />
- **Page 2, Value by specialty:** Specialties with the longest waits, the relationship between waiting time and no-show, and the top specialties by revenue.
  <img width="1920" height="1080" alt="Maria Auxiliadora Hospital Dashboard (1)" src="https://github.com/user-attachments/assets/4bd2ce63-7504-4d4c-b1db-21a97f1780a3" />
- **Page 3, Specialty detail (drillthrough):** Right click on a specialty and choose "Drill through" to see its KPIs, its monthly no-show rate and its no-show rate by day of the week, each compared with the hospital average. The month filter selected on page 1 is kept.
  <!-- Add the Page 3 image here -->

## 9. Conclusions and Recommendations
- **Intervention in critical cases:** Long waiting times are concentrated in a few specialties, led by Physical Medicine and Rehabilitation (43 days) and Pediatric Dermatology (59 days). An audit is recommended in these areas to determine whether the delay is due to a lack of medical staff, an oversupply of appointments, or another reason.
- **Reminder System:** Implement alerts (SMS/WhatsApp) specifically in the 17 specialties with total abandonment and in Physical Medicine and Rehabilitation.
- **Synchronization of Medical Schedules:** It is necessary to audit specialties with no attendance during specific periods to ensure that the appointment system schedules coincide with the actual availability of physicians, thus preventing patients from occupying slots on days when the service is not operational.
- **Resource optimization:** Reassign staff from specialties with 100% non-attendance to areas of greater demand and revenue, thus maximizing the use of hospital infrastructure.

## 10. Limitations
- **Meaning of the Attended field:** The dataset defines the field with Yes or No values; however, in the data dictionary, the field is described as Came or Did Not Come (Attendance).
  - **Impact on Analysis:** There is an interpretation gap between patient responsibility (not attending the appointment) and hospital management (the patient attended but was not seen due to lack of doctor, time, or supplies).
  - **Technical Decision:** For the purposes of this dashboard, the field has been assumed to be Attendance. However, it is recommended that this field be standardized at the source to differentiate non-attendance.
- **Ranking threshold:** The minimum of 100 appointments to enter the rankings is an analytical decision to avoid unreliable rates.
