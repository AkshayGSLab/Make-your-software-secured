# Floow these guidelines to write a secured code

**Buffer Overrun**
*	Pay attention to each of the string-handling and make sure that you are assigning precise memory in case of languages like C++. For Java or .Net where developer is least bothered about memory management also need some attention to these aspects.
* In case of Java, do not use String copy feature i.e. creating duplicate strings un-necessarily. Keep usages of String and Buffers minimal. 
*	Pay attention to Stack Overflow errors
*	Avoid using a single variable for the data which is big in size 
*	Check Heap & Stack over run issues – (Runtime and load time)
*	Be careful with handling Array based implementations – Give preference to design patterns implemented by language itself. E.g. instead of using primitive type arrays, use ArrayList interface
*	Be careful with string concatenation while using overloaded + operator in languages like Java/.Net. Always make sure that you are writing all the unit test cases with near to accurate possible variable’s values.

**Always run with Least Privilege or make use of elevated privileges for the shortest possible time**
 * Be careful with object oriented language like Java and .Net where the member variables of the interfaces/classes would need different access level privileges (Public/Private/Protected).
 *	Always identify least required privilege for each of the variable. E.g. Try to make all the possible variables in the class or interface Private and allow them to update via protected Set() functions only.

**Have full control on each of the object/variable being used**
*	Try to avoid global variable  for the general purpose
*	Keep objects life span shorter (as much as possible)
*   Avoid instantiating all the variables in one go, instead declare those when needed
*	Avoid passing handle/object from many functions/flows. Instead make a copy and then use it to avoid original object tampering by accident

**Never trust user input and the output produced by your won code**
*	Ensure that input received from the user/system is sanitized as soon as it arrives or as early as possible before other parts of the application interact with the data.
*	When you sanitize output, you need to sanitize as late as possible. That way you can be sure that it is not modified after it is sanitized and you only sanitize it once: right before it is sent.
*	Sometime due to big data size, you cannot sanitize received data always from the performance point of view. In such case, try to find out important data and get the minimal sub-set of it which can go through the sanitation process before using it. 
*	You should not assume that developers using your API are sanitizing data on their end and that you can send them raw user input.
*	Be aware of the places in your application where SQL injections can enter in to the DB via received inputs. 
* Be careful while writing data to the file system on your server. Check the content and it should not have any code snippet.
*	Validate user input before using the input data programmatically. 
*	Sanitize or reject invalid user input to protect against code injection attacks. 
*	Include user interface controls in the input validation strategy to make compliant and safe input easy for the user. 
*	Protect against buffer overflow attacks. 
*	Protect against array index errors. 
*	Protect against parameter manipulation attacks. 
*	Use parameterized SQL queries. 
*	Defend against SQL injection attacks.
*	Put all SQL code/commands in server-side code. 
*	Do not use dynamic/concatenated database queries. 
*	Do not put SQL in client-side code. 
*	Set Autocomplete=off in HTML to prevent the caching of sensitive information.
*	Protect against URL query string manipulation attacks.

**Make separation of the possible smallest unit of the feature** 
*	Avoid clubbing multiple features in a single package/class/file
*	Especially on a class level, each of the entity should have separate class in case of OO languages
*	Even though entity has just a single member variable., it should have its own class in the code base

**Be careful with Logs and Audit messages**
*	Sanitize your log and audit messages being build using variables. Check all the possible values of these variables and make sure that you are not disclosing any sensitive information like user’s credentials, security tokens, secure unique ids etc.
*	In most of the cases, logs will be written on the local file system, make use of standard logs and audit libraries like Log4J, Log4Cpp etc. 
*	Avoid using programmer defined file writing mechanism to maintain logs
*	Logs should content time stamp and the thread ID . It will help in detecting any issue easily
*	Logger API would be an overhead in terms of file read/write operations that would result in impacting performance and in some cases, server disk space over utilization by your application. Keep logging precise.
*	There are minimum 3 levels of logging any standard library will provide, INFO, WARN, DEBUG.   Do not use INFO always for each of the message, even though the product /module is in development environment
*	Keep log messages shorter and only understandable by the technical person
*	Never log code flow with very detailed message here
*	Check with the client on which data is critical from the business point of view. Avoid using that data as is. 
*	If you want to log or audit messages with critical data then please mask it properly . e.g Creadit Card Number can be presented as xxxx xxxx xxxx xxxx 2828 or phone number like 9xxxxxxx89
*	Log events related to authentication (success or failure), use of privileged functions, administration activities and system/component starts and stops
*	Log security-related events to a separate log file when possible. This provides developers with additional flexibility for any specific rules related to the log file (e.g., special roles/permissions, chain-of-custody, etc.)
	
**Make use of ORM for the DB connectivity from your application**
*	Do not bypass ORM features like query building.
*	Always sanitize user input being passed to the ORM functions to form a query
*	Do not hard-code any SQL statement even though your ORM library  is accepting it
*	Implement strong unit test cases for ORM based code

**Avoid using below sensitive information as a part of URL or request parameters**
* Credentials. 
* Access tokens, serial numbers or record numbers. 
* PII (e.g., names, SSNs, driver’s license numbers or dates-of-birth). 
* PHI (e.g., a Medical Record Number, diagnosis, condition or name)

**Exception and Error Handling**
* Software should have: 
    -	Configure runtime environments so that they do not reveal native framework errors (e.g., .Net, J2EE) to the screen/browser. 
    -  Set up custom error pages for framework errors.
    - Handle expected errors and provide users/administrative staff enough detail in error messages to troubleshoot problems. 
* Write code so there are no unhandled errors. 
* Create (wrap code) last-resort error try-catch blocks. 
* Never use empty catch blocks. 
* Ensure catch blocks cause the application to stop running and exit in a secure state. 
* Log detailed exception and error messages to the application event logs.

**Cross site scripting** 

Developers developing software must test untrusted data or code before sending it to a web browser. Testing must include proper validation for common XSS attacks.

**Insecure Direct Object References**
Developers developing software must ensure that direct object references to any object, file, directory or database key include an access control check or other protection

**TLS and Secure APIs**
*	Force HTTPS for all browser connections. 
*	Disable HTTP.
*	Use TLS 1.2 or later to protect machine-to-machine connections (e.g., app server to DB server connections).
*	Use strict transport security header.
*	Encrypt using a separate and unique credential for Institutional Information classified at Protection Level 3 or higher.
*	Ensure that the encryption technology used is approved by the CISO.
*	Authenticate and encrypt the session when software involves the transmission of Institutional Information classified at Protection Level 3 or higher. 
*	Encrypt APIs, restful interfaces, extract tools and service bus sessions.
*	Authenticate APIs, restful interfaces, extract tools and service bus sessions.
*	Separate public and private application APIs and configure CORS (Cross Origin Resource Sharing) headers to restrict invocation rights.

**Credentials/Passphrases**
*	Never store user passphrases. 
*	Protect service account credentials with established tools and techniques. 
*	Never hardcode credentials. 
* Implement lockout after certain failed authentication attempts.
* Use secure protocols for credential or other secret exchanges (e.g., TLS 1.2 or later).

**Session and Logout**
*	Ensure that session timeout is implemented. 
*	Make sure session tokens are random and long (GUID long). 
*	Change (delete old and create new) tokens at each logon and each privilege escalation.
*	Delete, remove and invalidate tokens on logout.
*	Use TLS 1.2 or later for all session tokens and cookies.
*	Provide a logout function. 
*	Prominently display the logout function throughout the application. 
*	Properly close records, delete temporary objects and close operations on the server:
        -	As part of the logout process. 
        -	After a set period of inactivity (e.g., less than one hour). o 
        -	After a browser window close.

**Insist on SSO implementation for the web applications**

**File Management**
* Prevent/disable directory traversal/directory listing
* Filter web requests to block access to files with non-approved extensions (e.g., .dll, .config, .java, .cs, etc.).
* Ensure shared volumes/file shares have appropriate access restrictions limited to the application service account.

**Secure Configuration**
 * Use secure configuration options for supporting technology, libraries, packages and tools.
 * Perform or have performed a vulnerability scan of the entire solution and appropriately remediate findings based on risk before placing the solution into production.
*	Secure the components used in an application.
*	Run components with the least privilege possible.
*	Keep components patched and up-to-date.
*	Execute SQL with the least privilege possible.
*	Use vetted and tested hardening guides to ensure the correct application of options and settings.
*	Define, implement and maintain secure settings (e.g., do not rely on default settings).
*	Secure the software configuration used in an application.
*	Set the configuration to define which HTTPS methods (e.g., Get or Post) the application will support and whether HTTPS methods will be handled differently in different pages of the application.
*	Set Header and Content-Security-Policy when possible

**Never ever maintain code on your local machine for a long duration. It should be submitted to the central code repository always**

