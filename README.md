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
    
