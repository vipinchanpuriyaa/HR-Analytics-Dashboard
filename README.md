Here’s a **clean, professional, GitHub-ready README.md update** for your project.
You can copy-paste this directly into your GitHub repository.

---

# 📊 HR Analytics Dashboard (Power BI)

## 🔹 Project Overview

This project demonstrates how **HR data can be transformed into actionable insights** using **Power BI**.
The dashboard enables HR teams and leadership to monitor **workforce distribution, promotions, and retrenchment trends** across departments, job roles, and demographics—supporting data-driven HR decision-making.

---

## 🔹 Key Features & Insights

### 1️⃣ HR Analytics Overview Dashboard

![HR Overview](https://github.com/user-attachments/assets/8cc466b2-7d45-46e8-86f4-3e6fa427a4e2)

**Workforce Summary**

* 👥 **Total Employees:** 1,470
* 👨 **Male Employees:** 882 (60%)
* 👩 **Female Employees:** 588 (40%)

**Employee Status**

* ⬆️ **Promoted Employees:** 1,398 (95.1%)
* ⏳ **Due for Promotion:** 72 (4.9%)
* ❌ **Lay-offs:** 117
* ✅ **On-Service Employees:** 1,353

**📌 Visuals Included**

* Employee distribution by **Job Level & Overtime**
* **Promotion vs Lay-off** analysis by Department
* Employee distribution by **Education Field**
* **Average Monthly Income** by Job Role

---

### 2️⃣ Due for Promotion Dashboard

![Due for Promotion](https://github.com/user-attachments/assets/ea67f540-d0b0-409e-b031-7214d098cb0b)

* 📈 **72 employees** identified as **due for promotion**
* **Top Job Roles Due for Promotion**

  * Manager: 22
  * Healthcare Representative: 16
  * Sales Executive: 16

**📌 Visuals Included**

* Promotions due by **Job Role**
* **Gender-wise** breakdown of employees due for promotion
* Employee-level table with:

  * Employee ID
  * Name
  * Gender
  * Promotion Status

---

### 3️⃣ Due for Retrenchment Dashboard

![Due for Retrenchment](https://github.com/user-attachments/assets/736fa122-0a67-4414-bae1-8f0b293326d4)

* ⚠️ **117 employees** identified for retrenchment
* **Most Affected Job Roles**

  * Manager: 44
  * Research Director: 20
  * Sales Executive: 20

**📌 Visuals Included**

* Retrenchment analysis by **Job Role & Department**
* **Gender-wise** retrenchment distribution
* Employee-level table with:

  * Employee ID
  * Name
  * Gender
  * Department
  * Lay-off Status

---

## 🔹 Tools & Technologies

**power BI ** → Data Modeling, DAX measures, KPI creation, and interactive visualizations

**SQL (MySQL)** → Data extraction, transformation, aggregation, business-rule implementation (promotion eligibility, retrenchment logic), and validation queries for Power BI dashboards

**Excel / CSV** → Raw HR dataset used as the primary data source

Power Query → Data cleaning, transformation, ETL processes, and data preparation before modeling

---

## 🔹 Business Value

This dashboard enables HR and leadership teams to:

* 📊 Track workforce demographics and distribution
* 🚀 Identify employees due for promotion and support career planning
* ⚠️ Monitor retrenchment risks across departments
* 🧠 Improve **data-driven HR strategy and workforce planning**




---

## 📬 Contact

If you have feedback or would like to collaborate, feel free to connect!


    Below are **clean, ready-to-use MySQL queries** that match your **HR Analytics Dashboard (Power BI)** metrics, visuals, and insights.
    You can use these queries directly for **Power BI, reporting, or validation**.
    
    *Assumption:*
    Table name = **`hr_data`**
    Employee name table (optional) = **`employees`**
    Primary key = `EmployeeNumber`
    
    ------------------------------------------------------------------------------------------------------------------------------------------
    
    ## 🔹 1. Total Employees
    
    
    SELECT COUNT(*) AS TotalEmployees
    FROM hr_data;
    ```
    
    ---
    
    **🔹 2. Gender Distribution** 
    
    
    SELECT 
        Gender,
        COUNT(*) AS EmployeeCount,
        ROUND(COUNT(*) * 100.0 / (SELECT COUNT(*) FROM hr_data), 1) AS Percentage
    FROM hr_data
    GROUP BY Gender;
    ```
    
    ---
    
    ## 🔹 3. Promotion Status
    
    ### Promoted vs Due for Promotion
    
    *(Assumption: Employees with `YearsSinceLastPromotion > 5` are due for promotion)*
    
    
    SELECT
        CASE 
            WHEN YearsSinceLastPromotion > 5 THEN 'Due for Promotion'
            ELSE 'Promoted'
        END AS PromotionStatus,
        COUNT(*) AS EmployeeCount
    FROM hr_data
    GROUP BY PromotionStatus;
    ```
    
    ---
    
    ## 🔹 4. Employees Due for Promotion
    
    
    SELECT COUNT(*) AS DueForPromotion
    FROM hr_data
    WHERE YearsSinceLastPromotion > 5;
    ```
    
    
    
    ## 🔹 5. Employees Due for Promotion by Job Role
    
    
    SELECT 
        JobRole,
        COUNT(*) AS DueForPromotion
    FROM hr_data
    WHERE YearsSinceLastPromotion > 5
    GROUP BY JobRole
    ORDER BY DueForPromotion DESC;
    
    
    ## 🔹 6. Gender-wise Promotion Due **
    
    ```sql
    SELECT 
        Gender,
        COUNT(*) AS DueForPromotion
    FROM hr_data
    WHERE YearsSinceLastPromotion > 5
    GROUP BY Gender;
    
    
    ** 🔹 7. Lay-offs / Retrenchment **
    
    ### Employees Identified for Retrenchment
    
    *(Assumption: Attrition = 'Yes' indicates retrenchment)*
    
    
    SELECT COUNT(*) AS Layoffs
    FROM hr_data
    WHERE Attrition = 'Yes';
    
    
    ## 🔹 8. On-Service Employees
    
    ```sql
    SELECT COUNT(*) AS OnServiceEmployees
    FROM hr_data
    WHERE Attrition = 'No';
    
    
    ## 🔹 9. Retrenchment by Job Role
    
    
    SELECT 
        JobRole,
        COUNT(*) AS RetrenchmentCount
    FROM hr_data
    WHERE Attrition = 'Yes'
    GROUP BY JobRole
    ORDER BY RetrenchmentCount DESC;
    
    
    ## 🔹 10. Retrenchment by Department
    
    
    SELECT 
        Department,
        COUNT(*) AS RetrenchmentCount
    FROM hr_data
    WHERE Attrition = 'Yes'
    GROUP BY Department;
    
    
    ## 🔹 11. Gender-wise Retrenchment
    
    SELECT 
        Gender,
        COUNT(*) AS RetrenchmentCount
    FROM hr_data
    WHERE Attrition = 'Yes'
    GROUP BY Gender;
    ```
    
    ---
    
    ## 🔹 12. Employee Distribution by Job Level & Overtime
    
    
    SELECT 
        JobLevel,
        OverTime,
        COUNT(*) AS EmployeeCount
    FROM hr_data
    GROUP BY JobLevel, OverTime
    ORDER BY JobLevel;
    
    
    ## 🔹 13. Employee Distribution by Education Field
    
    
    SELECT 
        EducationField,
        COUNT(*) AS EmployeeCount
    FROM hr_data
    GROUP BY EducationField
    ORDER BY EmployeeCount DESC;
    
    
    ## 🔹 14. Average Monthly Income by Job Role
    
    
    SELECT 
        JobRole,
        ROUND(AVG(MonthlyIncome), 2) AS AvgMonthlyIncome
    FROM hr_data
    GROUP BY JobRole
    ORDER BY AvgMonthlyIncome DESC;
    
    
    ## 🔹 15. Due for Promotion – Employee-Level Detail (Dashboard Table)
    
    SELECT 
        h.EmployeeNumber,
        e.EmployeeName,
        h.Gender,
        h.JobRole,
        'Due for Promotion' AS PromotionStatus
    FROM hr_data h
    LEFT JOIN employees e 
        ON h.EmployeeNumber = e.EmployeeNumber
    WHERE h.YearsSinceLastPromotion > 5;
    
    ## 🔹 16. Retrenchment – Employee-Level Detail (Dashboard Table)
    
    SELECT 
        h.EmployeeNumber,
        e.EmployeeName,
        h.Gender,
        h.Department,
        'Lay-off' AS Status
    FROM hr_data h
    LEFT JOIN employees e 
        ON h.EmployeeNumber = e.EmployeeNumber
    WHERE h.Attrition = 'Yes';
    
    
    ## 🔹 17. KPI Summary Query (For Power BI Cards)
    
    SELECT
        COUNT(*) AS TotalEmployees,
        SUM(CASE WHEN Gender = 'Male' THEN 1 ELSE 0 END) AS MaleEmployees,
        SUM(CASE WHEN Gender = 'Female' THEN 1 ELSE 0 END) AS FemaleEmployees,
        SUM(CASE WHEN YearsSinceLastPromotion > 5 THEN 1 ELSE 0 END) AS DueForPromotion,
        SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) AS Layoffs,
        SUM(CASE WHEN Attrition = 'No' THEN 1 ELSE 0 END) AS OnServiceEmployees
    FROM hr_data;
    
