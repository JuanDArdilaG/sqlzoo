# 1. There are three issues that include the words "index" and "Oracle". Find the call_date for each of them

```sql
SELECT
  DATE_FORMAT(call_date,'%Y-%m-%d %H:%i:%s') AS call_date,
  call_ref
FROM Issue
WHERE detail LIKE '%index%'
  AND detail LIKE '%Oracle%'
```

# 2. Samantha Hall made three calls on 2017-08-14. Show the date and time for each

```sql
SELECT
  DATE_FORMAT(call_date,'%Y-%m-%d %H:%i:%s') AS call_date,
  first_name,
  last_name
FROM Issue
JOIN Caller ON Caller.caller_id = Issue.caller_id
WHERE call_date >= '2017-08-14' AND call_date < '2017-08-15'
  AND first_name = 'Samantha' AND last_name = 'Hall'
```

# 3. There are 500 calls in the system (roughly). Write a query that shows the number that have each status.

```sql
SELECT status, COUNT(*) as Volume
FROM Issue
GROUP BY status
```

# 4. Calls are not normally assigned to a manager but it does happen. How many calls have been assigned to staff who are at Manager Level?

```sql
SELECT COUNT(*) AS mlcc
FROM Issue
JOIN Staff ON Issue.assigned_to = Staff.staff_code
WHERE level_code IN
  (SELECT level_code FROM Level WHERE manager = 'Y')
```

# 5. Show the manager for each shift. Your output should include the shift date and type; also the first and last name of the manager.

```sql
SELECT shift_date, shift_type, first_name, last_name
FROM Shift
JOIN Staff ON manager = staff_code
ORDER BY shift_date
```
