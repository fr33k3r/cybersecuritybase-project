
Cyber Security Base - Course Project I
======================================

*For the identification process of the vulnerabilites I have used OWASP ZAP as suggested.

*The original form usability has been removed and so has the test file.

*The server will run on http://localhost:8081

===========================================================================================

The project will involve a small blog site, where different users will post their thoughts and I'll try to expose at least 5 vulnerabilities according to the OWASP Top 10 as of 2013. For that purpose, I have intenionally included extra information like a password and a credit card number for when I demonstrate and SQLi vulnerability.
As a final note, I do intend to use bootstrap in the future and make it more user friendly.


First flaw : Cross-Site Scripting (XSS)
======================================

Issue: Stored XSS Attack 
Steps to reproduce: 
1. Open link localhost:8081/posts 
2. Go to New Post and choose a Name of your choice such as "Jim" 
3. Put \<script>alert(document.cookie);\</script> for Post content
4. Press "Submit Post"
5. Congratulations. You have successfully completed this attack.

When the site reloads, you will be greeted with a couple of pop-ups, which shows that we were able to make the browser execute our JavaScript code. 
The solution to this would be to sanitize the input and not let special characters be executed like the <script> command. We could replace the thymeleaf directive "th:utext" with "th:text". That would make thymeleaf recognize it as plain text. 


Second flaw : SQL Injection 
============================

Issue: SQL Injection Steps to reproduce: 
Steps to reproduce:
1. Open link localhost:8081/posts
2. Insert: 1' OR '1'= '1 to the "retrieve users posts" field
3. Press "Retrieve Post" 
4. You can now see all the names and posts being displayed even though it is only supposed to return posts from the specific name

To fix this flaw, we can again sanitize all input. We can also use "Prepared Statements (with Parameterized Queries)" and binding parameters. Also, we can pretty much use the repository default functions and not write any raw SQL at all. 

