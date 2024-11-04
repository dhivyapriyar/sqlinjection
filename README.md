# NAME: DHIVYAPRIYA. R
# REG.NO.: 212222230032
# EX 8 sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2

![image](https://github.com/user-attachments/assets/52a7d28f-cbf1-4d92-8133-cdb338ae09e9)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.

![image](https://github.com/user-attachments/assets/f0e574a0-53d6-4283-adf3-01ad1a4cfbae)

Select Multidae from the menu listed as shown above. You will get the page as displayed below:

![image](https://github.com/user-attachments/assets/6f0636a0-9b79-4760-88e8-293d7d66d157)

Click on the menu Login/Register and register for an account

![image](https://github.com/user-attachments/assets/fc59d0df-bc69-4276-aa07-eef3a8a5a70b)

Click on the link “Please register here”

![image](https://github.com/user-attachments/assets/47b0c62d-bc7d-4a1f-a3b1-231db92df006)

Click on “Create Account” to display the following page:

![image](https://github.com/user-attachments/assets/15674d3f-76fd-4b14-ab00-55a8791be883)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

![image](https://github.com/user-attachments/assets/0e8d29ef-61a2-4035-9a09-376d988a5e5a)

Click “Login”. The logged in page will show as below:

![image](https://github.com/user-attachments/assets/8d3919ba-d094-4e0e-bd7a-8bdcad245d36)

##Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.

![image](https://github.com/user-attachments/assets/7bcb3c37-0672-4ada-8f95-51c13a007aeb)

Click the login button and you will see it enter into the administrator page.

![image](https://github.com/user-attachments/assets/96c1f05c-9c11-4c18-89ec-d4f2235bbbf5)

## Union-based SQL injection:

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below:
![image](https://github.com/user-attachments/assets/239facbb-5796-4267-8e11-8989442de37b)

![image](https://github.com/user-attachments/assets/578bfcbd-8512-46d2-b0eb-c50253cb75c8)

![image](https://github.com/user-attachments/assets/4a2a5c3e-6e2d-4b71-84b6-3c835b629383)

![image](https://github.com/user-attachments/assets/5675ea86-c3da-4f13-8e85-a30c66efea0a)

![image](https://github.com/user-attachments/assets/800164de-d3af-48e6-8dff-597cc782f244)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

![image](https://github.com/user-attachments/assets/493b88e5-2ad8-418a-9a9e-b8de83453bea)

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

![image](https://github.com/user-attachments/assets/d1396fb6-1be2-4872-8f0f-71e83f54ccb8)

After adding the order by 6 into the existing url , the following error statement will be obtained:

![image](https://github.com/user-attachments/assets/6adc8d8b-c0ed-4d64-995b-bb11e5d1eb43)

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.

![image](https://github.com/user-attachments/assets/0b9e5dbb-0782-4792-8c10-ec61cbba20c9)

![image](https://github.com/user-attachments/assets/317f7e80-5d32-4baf-a4df-2b9ba132889b)

As it is having 5 columns the query worked fine and it provides the correct result

![image](https://github.com/user-attachments/assets/0527648b-bd2b-49f2-ad39-84eda2e1db78)

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)

![image](https://github.com/user-attachments/assets/a05c3406-c4ce-4419-af69-dd06b4f1a747)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.

![image](https://github.com/user-attachments/assets/61274ec7-2787-44d3-82de-7dbc631a3e5b)

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

![image](https://github.com/user-attachments/assets/a27f1d9d-c229-4d16-baae-9ca713acee66)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

![image](https://github.com/user-attachments/assets/7232b488-57c4-4140-a579-d91df48befa3)

![image](https://github.com/user-attachments/assets/ee786bf1-a17f-4343-8e8a-a773b10b46d9)

Reading and writing files on the web-server We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

![image](https://github.com/user-attachments/assets/c129c14b-6a46-46d1-a178-8182a0466b19)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
