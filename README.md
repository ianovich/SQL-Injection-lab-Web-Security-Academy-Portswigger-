# SQL-Injection-lab-Web-Security-Academy-Portswigger-

## Lab Description:
This lab demonstrates a SQL injection vulnerability in the WHERE clause of a web application's search functionality. By exploiting this vulnerability, we can retrieve hidden data from the database.

## Tools Used:
- Burp Suite

## Steps to Exploit:

1. **Intercepting the Request:**
   - Configure Burp Suite as a proxy.
   - Intercept a search request from the web application.
   - Example request: `GET /filter?category=Tech+gifts HTTP/2`

 2. **Testing for SQL Injection:**
   - Modify the intercepted request in Burp Suite Interceptor to include a single quote (`'`).
   - Example: `GET /search?query=search+term' HTTP/1.1`

3. **Crafting the Payload:**
   - Identify the SQL injection point and create a payload to retrieve hidden data.
   - Payload: `search term' OR 1=1 --`
   - Example: `GET /search?query=search+term' OR 1=1 -- HTTP/1.1`

4. **Sending the Modified Request:**
   - Forward the modified request using Burp Suite Interceptor.
   - Analyze the response to verify the retrieval of hidden data.

## Screenshots:      
### Intercepted Request:
1 ![intercept](https://github.com/user-attachments/assets/a3c9830d-61de-402e-8e03-3299950e34ba)
When I use a GET request, I'm asking the website to send me information from a specific page. For instance, in this request, I'm looking for products or items listed under the "Tech gifts" category on the site.<br/>

Here's how it breaks down:<br/>

GET- This is my way of asking the website to send me some information.<br/>
/filter?category=Tech+gifts: This is the particular page or section I want to see, which shows items related to "Tech gifts."<br/>


2 ![modified](https://github.com/user-attachments/assets/fa671f3e-eea1-4354-85da-e02626fc9f7a)

- **Injection Breakdown/modified request:**
- **'**: Ends the current category filter.
- **or 1=1**: This is a common SQL injection technique that always evaluates to true, effectively bypassing the original filter conditions.
- **--**: Comments out the rest of the SQL query, so any additional conditions or filters are ignored.

By injecting this extra text, I’m trying to bypass the usual filtering mechanisms and access more data than I should, or manipulate the website’s response to show everything or unauthorized information.

### Response with Hidden Data
![final](https://github.com/user-attachments/assets/2d393b85-d66b-4882-ab23-09734c6cdf22)
In the response, we can observe additional records that were previously hidden. This indicates that the SQL injection allowed us to retrieve unauthorized information from the database. 
- Sensitive application data that could be exploited further.

This demonstrates the critical need for input validation and parameterized queries to prevent such vulnerabilities.
## SQL Injection Prevention Summary

To protect your applications from the above  SQL injection vulnerability:

1. **Use Prepared Statements (Parameterized Queries):**
   - Always use prepared statements to separate SQL code from user input, ensuring that inputs are treated as data and not executable code.
   - Ensure that all SQL queries are prepared and executed with parameters rather than directly concatenating user input into the SQL string.










