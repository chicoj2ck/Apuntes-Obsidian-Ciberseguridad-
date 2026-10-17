___
- tags: #blind_sql
___
## Blind SQLi
Unlike In-Band SQL injection, where we can see the results of our attack directly on the screen, blind SQLi is when we get little to no feedback to confirm whether our injected queries were, in fact, successful or not, this is because the error messages have been disabled, but the injection still works regardless.

### Boolean Based
Refers to the response we receive from our injection attempts, whic cloud be a true/false, yes/no, on/off, 1/0 or any response that can only have two outcomes.

### Time Based
is very similar to the above boolean-based one in that the same requests are sent, but there is no visual indicator of your queries being wrong or right this time.

### Out-of-Band SQLi
Out-of-band SQL Injection isn't as common as it either depends on specific features being enabled on the database server or the web application's business logic, which makes some kind of external network call based on the results from an SQL query.

## Remediation
 - Prepared Statements (With Parameterized Queries)
 - Input Validation
 - Escaping User Input