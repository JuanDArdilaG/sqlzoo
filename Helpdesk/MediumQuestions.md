# 6. List the Company name and the number of calls for those companies with more than 18 calls.

```sql
SELECT Company_name, COUNT(*) AS cc
FROM Issue
JOIN Caller ON Issue.Caller_id = Caller.Caller_id
JOIN Customer ON Caller.Company_ref = Customer.Company_ref
GROUP BY Company_name
HAVING COUNT(*) > 18
```

# 7. Find the callers who have never made a call. Show first name and last name

```sql
SELECT first_name, last_name
FROM Caller
LEFT JOIN Issue ON Caller.Caller_id = Issue.Caller_id
WHERE Issue.Caller_id IS NULL
```

# 8. For each customer show: Company name, contact name, number of calls where the number of calls is fewer than 5

```sql
SELECT Company_name, C.first_name, C.last_name, COUNT(*) AS nc
FROM Issue
JOIN Caller ON Caller.Caller_id = Issue.Caller_id
JOIN Customer ON Customer.Company_ref = Caller.Company_ref
JOIN Caller AS C ON C.caller_id = Customer.contact_id
GROUP BY Company_name
HAVING COUNT(*) < 5
```
