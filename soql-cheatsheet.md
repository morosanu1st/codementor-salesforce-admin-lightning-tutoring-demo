# SOQL Cheatsheet (Beginner)

Tiny reference for tutoring sessions. Practice in **Developer Console → Query Editor** or VS Code with Salesforce extensions.

---

## Basic shape
```sql
SELECT Id, Name, CreatedDate
FROM Account
WHERE Industry = 'Technology'
ORDER BY Name
LIMIT 50
```

## Useful WHERE patterns
```sql
-- Comparisons
WHERE AnnualRevenue > 1000000
WHERE Rating IN ('Hot', 'Warm')
WHERE Name LIKE 'Acme%'

-- Null checks
WHERE Phone != null
WHERE BillingCity = null

-- Logic
WHERE Type = 'Customer' AND Rating = 'Hot'
WHERE Industry = 'Finance' OR Industry = 'Insurance'
```

## Relationship queries (intro)

**Child → parent** (dot notation):
```sql
SELECT Name, Account.Name, Account.Industry
FROM Contact
WHERE Account.Industry = 'Technology'
```

**Parent → child** (subquery):
```sql
SELECT Name,
  (SELECT LastName, Email FROM Contacts)
FROM Account
WHERE Name = 'Acme Corporation'
```

## Date literals (common)
```sql
WHERE CreatedDate = TODAY
WHERE CreatedDate = THIS_WEEK
WHERE CreatedDate > LAST_N_DAYS:30
```

## Habits that save pain later
- Always start with the fields you need — avoid `SELECT *` (SOQL doesn’t support it anyway)  
- Filter early with WHERE; use LIMIT while exploring  
- Don’t put queries inside loops in Apex (governor limits) — learn the pattern now even as an Admin  
- Test relationship API names in Object Manager if a query fails  

## Tiny practice prompts
1. List 10 Opportunities with Amount and StageName, ordered by Amount descending  
2. Contacts whose Account BillingCountry is `'United States'`  
3. Accounts that have at least one related Contact (parent-to-child subquery)  

Bring your attempt (even if it errors) to the session — debugging queries together is the point.
