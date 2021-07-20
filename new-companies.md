> Practice > SQL > Advanced Select > New Companies

# New Companies [link](https://www.hackerrank.com/challenges/the-company/problem)

Amber's conglomerate corporation just acquired some new companies. Each of the companies follows this hierarchy: 

![image](https://user-images.githubusercontent.com/74973306/126268193-309bce6f-02f6-4ba9-aac4-efbebd22a73c.png)

Given the table schemas below, write a query to print the company_code, founder name, total number of lead managers, total number of senior managers, total number of managers, and total number of employees. Order your output by ascending company_code.

Note:

- The tables may contain duplicate records.
- The company_code is string, so the sorting should not be numeric. For example, if the company_codes are C_1, C_2, and C_10, then the ascending company_codes will be C_1, C_10, and C_2.

---

- 내 풀이

```sql
SET @a := 0;

SELECT concat('C',(@a := @a + 1)) as company_code, (SELECT founder 
                                    FROM Company
                                    WHERE company_code = concat('C',@a)),
                                    
                                    (SELECT count(distinct lead_manager_code)
                                    FROM Lead_Manager
                                    WHERE company_code = concat('C',@a)),
                                    
                                    (SELECT count(distinct senior_manager_code )
                                    FROM Senior_Manager
                                    WHERE company_code = concat('C',@a)),
                                    
                                    (SELECT count(distinct manager_code)
                                    FROM Manager 
                                    WHERE company_code = concat('C',@a)),
                                    
                                    (SELECT count(distinct employee_code)
                                    FROM Employee 
                                    WHERE company_code = concat('C',@a))
                                    
FROM COMPANY
ORDER BY company_code;
```

- 다른 사람 풀이

```sql
select c.company_code, c.founder, 
    count(distinct l.lead_manager_code), count(distinct s.senior_manager_code), 
    count(distinct m.manager_code),count(distinct e.employee_code) 
from Company c, Lead_Manager l, Senior_Manager s, Manager m, Employee e 
where c.company_code = l.company_code 
    and l.lead_manager_code=s.lead_manager_code 
    and s.senior_manager_code=m.senior_manager_code 
    and m.manager_code=e.manager_code 
group by c.company_code order by c.company_code;
```
