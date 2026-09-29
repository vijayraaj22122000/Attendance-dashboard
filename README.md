# 🎓 Student Attendance & Performance Dashboard (Power BI)

A Power BI dashboard that tracks student attendance and academic performance across classes, sections, and subjects. 

## 📌 Project Overview

This dashboard helps a school track:
- Overall attendance and academic performance across all students
- Which students need attention for low attendance or low marks
- Subject-wise and exam-wise performance trends
- Side-by-side comparison between any two (or more) students

---

## 🗂️ Dataset

The dataset is a synthetic Excel workbook with 3 core tables:

| Table | Description | Rows |
|---|---|---|
| **Students** | Student ID, Name, Class, Section, Gender, Age | 52 |
| **Attendance** | Daily attendance record per student (Present / Absent / Leave) | ~2,750 |
| **Marks** | Exam records per student, per subject, per exam type | 780 |

Relationships: `Students[StudentID]` → `Attendance[StudentID]` and `Students[StudentID]` → `Marks[StudentID]` (one-to-many).

---

## 📊 Dashboard Pages

### 1. Overview
- KPI cards: Total Students, Attendance %, Average Marks %
- Attendance % trend by month
- Top 10 students by average marks

### 2. Attendance
- KPI cards: Highest Attendance, Lowest Attendance, Low Attendance Students (below 75%)
- Attendance % by student (sorted lowest first)
- Slicers: Class, Section, Month

### 3. Performance
- KPI cards: Highest Average Marks, Average Marks %, Fail Count
- Average Marks % by subject
- Grade distribution (A+ to D/F)
- Slicers: Subject, Exam Type, Class

### 4. Comparison
- Multi-select student slicer
- Side-by-side table: Class, Section, Attendance %, Average Marks %, Grade
- Head-to-head bar chart: Attendance % vs Average Marks % per selected student

All 4 pages share a left-side page navigator for quick switching.

---

## 🧮 Key DAX Measures

```DAX
Attendance % =
DIVIDE(
    CALCULATE(COUNTROWS(Attendance), Attendance[Status] = "Present"),
    COUNTROWS(Attendance)
)

Average Marks % =
DIVIDE(SUM(Marks[MarksObtained]), SUM(Marks[MaxMarks]))

Low Attendance Students =
CALCULATE(
    DISTINCTCOUNT(Students[StudentID]),
    FILTER(VALUES(Students[StudentID]), [Attendance %] < 0.75)
)

Fail Count =
CALCULATE(
    COUNTROWS(Marks),
    FILTER(Marks, DIVIDE(Marks[MarksObtained], Marks[MaxMarks]) < 0.4)
)
```

---

## 🛠️ Tools Used

- **Excel** — source dataset preparation
- **Power Query** — data cleaning, type correction, date locale formatting
- **Power BI Desktop** — data modeling, DAX measures, report visuals
- **DAX** — calculated measures for attendance %, marks %, and flags

---

## 🚀 How to Open

1. Open `Student_Attendance_Performance.pbix` in Power BI Desktop.
2. If prompted, click **Refresh** to reload data from the source Excel file.
3. Use the left-side navigator or the page tabs at the bottom to move between pages.
4. On the Comparison page, hold **Ctrl** and click multiple student names to compare them.

---

## 📈 Key Insights (sample)

- Overall attendance across all students: **87.16%**
- Overall average marks: **71.39%**
- **5 students** are below the 75% attendance threshold and may need follow-up
- **7 exam results** fall below the pass mark (40%)

---

## 🔮 Possible Future Improvements

- Add a Grade-over-time trend once multiple terms of data are available
- Add a class teacher / subject teacher drill-through page
- Automate low-attendance email alerts using Power Automate

---


