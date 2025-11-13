# sqlinjection
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

SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. 
Identify IP address using ifconfig in Metasploitable2
## OUTPUT

<img width="916" height="519" alt="01_ifconfig" src="https://github.com/user-attachments/assets/be3f6679-635d-49b2-9881-15e578e836c3" />

Use the above ip address to access the apache webserver of Metasploitable2 from kali/parrot linux. In Kali Linux use the ip address in a web browser.
##  OUTPUT

<img width="1257" height="902" alt="02_webpage" src="https://github.com/user-attachments/assets/ed5c4a77-1145-4dff-bd85-61401dc28993" />

Select Multidae from the menu listed as shown above. The page is displayed as below:
##  OUTPUT

<img width="1920" height="1200" alt="03_mutillidae" src="https://github.com/user-attachments/assets/d6db3dc9-70d0-48ed-a62a-d08ac8d53427" />

Click on the menu Login/Register and register for an account
##  OUTPUT

<img width="1920" height="1200" alt="04_mutillidae_login" src="https://github.com/user-attachments/assets/d0599091-430a-4e89-a230-4a04e0eb1fbb" />

Click on the link “Please register here”
##  OUTPUT

<img width="1920" height="1200" alt="05_mutillidae_register_page" src="https://github.com/user-attachments/assets/3348e089-be08-4450-b734-f289b9229225" />

Click on “Create Account” to display the following page:
##  OUTPUT

<img width="1920" height="1200" alt="06_mutillidae_account_register" src="https://github.com/user-attachments/assets/d6a055d9-3982-4e8c-83b0-584b5118bd52" />

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:


($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;).
 For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.
##  OUTPUT

<img width="1920" height="1200" alt="07_mutillidae_login_page_sql_injected" src="https://github.com/user-attachments/assets/2afacdbd-6263-4041-a1fb-901bfe770ac3" />

Click “Login”. The logged in page will show as below:
##  OUTPUT

<img width="1920" height="1200" alt="08_mutillidae_login_page" src="https://github.com/user-attachments/assets/6422cf10-a89a-47c4-93b4-cbb549fdce66" />

If error faced in registration follow the following steps in metasploitable 2:


This issue is caused by a misconfiguration in the config.inc located in the /var/www/mutillidae folder on Metasploitable 2 VM.

Edit config.inc
Edit config.inc file located in /var/www/mutillidae folder on Metasploitable 2 by typing the following commands [one at the time]:
cd /
sudo nano /var/www/mutillidae/config.inc
Type msfadmin when prompted for the root password. 
Once nano opens config.inc file, look for the line $dbname = ‘metasploit’ as shown in Figure  below:
##  OUTPUT

Replace ‘metasploit’ with ‘owasp10’ and make sure the lines end with semicolon ; as shown in Figure

##  OUTPUT

<img width="1920" height="1200" alt="09_metasploitable_config" src="https://github.com/user-attachments/assets/a10b85ec-4e15-47cc-8798-b77d057c1528" />


Save and exit the config.inc
Save than exit the config.inc file by typing CTRL+X keys on your keyboard and the Y [Enter] when prompted to save the file
Restart the Apache server
To restart Apache, type the following command in the terminal. Alternatively, you can just reboot Metasploitalbe 2 VM.
sudo /etc/init.d/apache2 reload
##  OUTPUT

<img width="1920" height="1200" alt="09_metasploitable_config" src="https://github.com/user-attachments/assets/f3fdee0a-cd27-4216-b0f6-0eede3165bd1" />


# Reset Mutillidae database
Refresh the page then clicking on the Reset DB menu option to reset the Mutillidae database [Figure ]. Click OK when prompted.
##  OUTPUT

<img width="1920" height="1200" alt="10_mutillidae_resetDB" src="https://github.com/user-attachments/assets/678c9b43-26ef-48ca-a149-1a9f6bc725b1" />


# Test the new configuration
Alright. Now is time to test if we managed to fix the database issue. Go ahead and register a new account on the Mutillidae webpage.

 The Mutillidae database error no longer appears 
## OUTPUT



Now after logging out you will see the login page. In the login page give ganesh’# (myusername). You can see the page now enters into the administrator page as before when giving the password.
## OUTPUT


Click the login button and you will see it enter into the administrator page.
## OUTPUT



## Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. 
we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” 

After logging out, Now choose the menu as shown below:
##  OUTPUT

<img width="1536" height="836" alt="11_owasp_top_10" src="https://github.com/user-attachments/assets/c5971e95-0e12-4fa6-a81e-fdf91225ebad" />

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
##  OUTPUT

<img width="1920" height="1200" alt="19" src="https://github.com/user-attachments/assets/f9979f52-de58-4b67-9597-ce10745a7600" />

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.






After adding the order by 6 into the existing url , the following error statement will be obtained:
##  OUTPUT

<img width="1920" height="1200" alt="19" src="https://github.com/user-attachments/assets/57c2851a-ffdd-490c-a437-6b6985e5797f" />


When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
## OUTPUT

<img width="1920" height="1200" alt="20" src="https://github.com/user-attachments/assets/c59b5d12-9060-489d-81f9-0bafff0c5c66" />


 As it is having 5 columns the query worked fine and it provides the correct result
##  OUTPUT

<img width="1920" height="1200" alt="20" src="https://github.com/user-attachments/assets/19f82ec4-5543-4cb0-99c6-a9c4b45a3611" />


Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5).
##  OUTPUT

<img width="1920" height="1200" alt="13" src="https://github.com/user-attachments/assets/5e1577e9-4cf2-4ebd-9257-c5a557d6b6bb" />

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
##  OUTPUT

<img width="1920" height="1200" alt="14" src="https://github.com/user-attachments/assets/fc13431d-8007-4c82-9f22-bc7cae717e68" />




Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.
##  OUTPUT

<img width="1920" height="1200" alt="15" src="https://github.com/user-attachments/assets/1a601b57-0de2-4455-b8d1-11994bbda596" />

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5.
In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one:
union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’
##  OUTPUT

<img width="1920" height="1200" alt="16" src="https://github.com/user-attachments/assets/3573da38-8ca9-41fb-a795-37de0ef4f763" />


The url once executed will  retrieve table names from the “owasp 10” database.
##Extracting sensitive data such as passwords 

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.
##  OUTPUT

<img width="1920" height="1200" alt="17" src="https://github.com/user-attachments/assets/1c0ac5cc-dccb-4151-9a44-48914bb4d371" />


The column names of the accounts is displayed below for the following url:


Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).
##  OUTPUT

<img width="1920" height="1200" alt="18" src="https://github.com/user-attachments/assets/d5ab9af0-a6b6-42bd-b8d7-c2f9de1d85eb" />

## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).



## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
