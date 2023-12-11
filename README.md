# POSTMAN
---

## API Request Methods 

### POST
POST is the only RESTful API HTTP method that primarily operates on resource collections. When creating a subordinate resource in a collection, applying POST to the parent resource prompts it to create a new resource, associate it with the proper hierarchy and return a dedicated URL for later reference. However, keep in mind that POST is not idempotent; you can't use this method more than once and expect a consistent outcome or result.

A significant benefit of POST is that it enables developers to explicitly define resources. This feature helps prevent teams from accidentally creating subordinate resources that pollute code, muddy references and cause applications to experience problems.

### PUT
The single-resource equivalent of POST is PUT, which updates a resource by replacing its content entirely. As a RESTful API HTTP method, PUT is the most common way to update resource information.

It's possible to create a resource with a PUT method, but this approach carries the risk of creating resources by accident, as noted above. If PUT is applied to a collection of resources, the entire resource collection gets replaced, which usually isn't the intention.

### PATCH
PATCH is another HTTP method used to update resources. As opposed to replacing resources, like the PUT method does, PATCH only modifies resource contents. As a general rule, these modifications should be expressed in a standard format, like JSON or XML.

Much like in PUT, it's poor practice to specifically apply PATCH methods to a whole resource collection -- that is, unless you truly intend to update every resource it contains.


### GET
The most common HTTP method is GET, which returns a representational view of a resource's contents and data. GET should be used in read-only mode, which keeps the data safe and the resource idempotent. You should get the same results no matter how many times you use this method, unless it is modified by another client in the interim.

The GET method is sometimes used to change the contents of a resource, but this is a precarious use of the method. It's common to compromise a client's ability to PATCH a resource if the resource detects a change since the PATCH client last conducted a GET.

### DELETE
The last HTTP method to examine is DELETE. When a DELETE method targets a single resource, that resource is removed entirely.

Implementations of DELETE are typically somewhat inconsistent: The URL for the resource may remain available even if the actual resource is absent. In this type of scenario, it's possible the server or resource implementation still changes the state of the vanished resource using the URL and likely reacts differently to subsequent DELETE executions.

While it's certainly possible, you should generally avoid using the DELETE method in a resource collection since it deletes all the contents within. Remember, the method isn't idempotent and shouldn't be treated as such.

---

## VARIABLE SCOPES
There are multiple scopes that let us process the development and testing of API in various environments with different values. Below are the variable scopes defined from the broadest to the narrowest area covered:

- [x] Global variables: These are accessible throughout the workspace and have the broadest scope in Postman. They can be used anywhere among multiple requests and collections within the workspace.

- [x] Collection variables: These variables are accessible only inside a certain collection. They are available across all the requests within a collection. Also, they don’t change based on the selected environment.

- [x] Environment variables: These variables let us scope the work as per the different environments. They change along with the change in the environment we are working on like local environment, staging or the production environment.

- [x] Data variables: These types of variables are external and define the data sets while running collections with the Collection Runner. We can extract this from a CSV or a JSON file. They have current values that don’t persist after a request or collection executes.

- [x] Local variables: These variables are also known as temporary variables that are only accessible through a request script. They have scope only till the current request or collection. Once the execution completes, they are no longer available.

## Defining Variables in Scripts
Similar to defining variables in a collection, an environment, or globally, we can also set variables programmatically in our request scripts.

All of these methods take in (variable_key, variable_value) as input:

- [x] pm.globals: This method is used for defining the global variables in a request script, e.g., pm.globals.set(“variable_key”, “variable_value”);

- [x] pm.collectionVariables: We can define a variable with scope as ‘collection’ with this method, e.g., pm.collectionVariables.set(“variable_key”, “variable_value”);

- [x] pm.environment: This can be used for defining an environment variable with scope as current environment, e.g., pm.environment.set(“variable_key”, “variable_value”);

- [x] pm.variables: This defines the local variable with local/temporary scope, e.g., pm.variables.set(“variable_key”, “variable_value”);

- [x] unset: This method can be used for removing a set variable. The unset can be defined with the above variable instances as per their scope, e.g., pm.environment.unset(“variable_key”, “variable_value”);

## Using Variables in Scripts
We’ve stored the variables in scripts by using the above methods. Therefore, we can retrieve their current value using these methods:

- [x] pm.variables.get(“variable_key”): This will access a variable at any scope including the local.
- [x] pm.globals.get(“variable_key”): This can access a global variable
- [x] pm.collectionVariables.get(“variable_key”): This can access a collection variable.
- [x] pm.environment.get(“variable_key”): This can access an environment variable.
- [ ] Here, we can retrieve the values using variable_key. The object represents the scope level and the get() method retrieves the value.
- [ ] The pm.variables.get() method also provides the option to change variable scopes without actually affecting the script functionality. It returns the variable that currently has the highest precedence.

---
## Library API:
Base URI:  https://rahulshettyacademy.com (or) http://216.10.245.166

1.	Method: POST
Add Book Complete URL - https://rahulshettyacademy.com/Library/Addbook.php

aisle value should be number only. Isbn should be unique to insert. So provide random isbn which makes unique
Input Payload: Json:
```json
{

"name":"Learn Appium Automation with Java",
"isbn":"bcd",
"aisle":"227",
"author":"John foe"
}
 
Output Json 
{
   "Msg": "successfully added",
   "ID": "bcd227"
} 
```

 
 
1.	Resource : /Library/GetBook.php?AuthorName=somename        Method : GET 
 
Output Json:
Output the array of Json object books with all below details 


{
 
Name : “bookname”   ( String)
Isbn :  “A2fdsf”   (String)
Aisle : 32 (Integer)
 
}

 
1.	Resource: Library/GetBook.php?ID=3389      - Method : GET 
 
Output Json:
```json
{
      "book_name": "Selenium automation using Java",
      "isbn": "a23hd738",
      "aisle": "1223"
   } 
 
1.	Resource :/Library/DeleteBook.php      Method : POST
 
Input Payload: Json:
{
 
"ID" : "a23h345122332"
 
} 
Output Response:
{

msg : book is successfully deleted”
 
}
Automation Scenarios to Test Library API -

Verify if API responses returns Success Codes with Proper Assertions
Verify if Response Json Schema is displayed as expected
Create Environment/Global/Collection variables to dynamically switch end points of APIs to test in different stages of QA Life cycle
Pass response ID of Add Book to Get Book and Delete ID request Parameters for full functional Automation Testing
Validate the book ID response calculation Logic
Validate if Get Book API retrieves the correct response with Book Details requested
Validate if Delete Book API successfully deleted Book
Implement Try Catch Error Handling Mechanism for every Automation test as Tear Down Script
If Book Already exists in DB, Implement Smart Strategy to delete the existing Book first before Adding the Book again as Prerequisite Automation Step
Parse the complete Json response and verify if the values are displayed as expected
Generate Unique ISBN/ aisle value for every run to make Book Unique using Automation Script
Import the Book Details from CSV/Json without hard coding for Validating API’s
Run the APIs with multiple data sets by iterating the data from the CSV as a Data driven testing

//




What are Environments and variables in Postman?

An environment is a set of variables you can use in your Postman requests. You can use environments to group related sets of values together and manage access to shared Postman data if you are working as part of a team.

Variables allow you to store and reuse values in your requests and scripts. By storing a value in a variable, you can reference it throughout your collections, environments, and requests—and if you need to update the value, you only have to change it in one place. Using variables increases your ability to work efficiently and minimizes the likelihood of error.


How to use Environments and Variables in Postman?

Variable scopes
Postman supports the following variable scopes:
•	Global
•	Collection
•	Environment
•	Data
•	Local


Scripting in Postman
Postman contains a powerful runtime based on Node.js that allows you to add dynamic behavior to requests and collections. This allows you to write test suites, build requests that can contain dynamic parameters, pass data between requests, 
 
The pm object
You will carry out most of the Postman JavaScript API functionality using “pm” which provides access to request and response data, and variables.


Verify if there is an entry called Cypress.
Verify if Cypress entry has course Title and Price properties/keys
Verify if sum of API Courses equals to 90
Verify if Web Automation Course titles are shown as expected titles














Postman can also test Soap Webservices in addition to Rest HTTP requests
How Soap Webservices are different from Rest Services?
Rest API’s use HTTP protocol to send the request and receive the response
Whereas Soap Webservices/API’s use Soap Protocol to send the request ad receive the response
In Soap Services, requests/responses are sent in XML Format.
What will we learn from this Course?
How to Call Soap Services from Postman- Understand the rules of setting up Soap Project in Postman
How to write automation tests on the XML response of Soap Services.

Soap End Point example
https://www.dataaccess.com/webservicesserver/NumberConversion.wso



What is Newman?

•	Newman is a command line Collection Runner for Postman. 
•	It allows you to run and test a Postman Collection directly from the command line.
•	Using Newman, you can easily integrate it with your continuous integration servers and build systems.

•	Newman is built on Node.js. To run Newman, Install Node.js as prerequisite.
•	After Node.js install, Install Newman from npm globally on your system, which allows you to run it from anywhere.
npm install -g newman

•	How to run collection from Newman?
	$ newman run <CollectionFile>

•	Learn about Newman Configuration options

•	Generate HTML reports for Test execution results with newman - htmlextra plugin
https://www.npmjs.com/package/newman-reporter-htmlextra

•	Integrate Postman Automation Scripts to Jenkins CI/CD with the help of Newman commands










Trigger the Postman Automation Scripts from Terminal with the help of Newman CLI
Integrate the Automation Tests with Jenkins for CI/CD Implementation
Prepare neat HTML reports for the Postman API Test Automation results
Understand how to collaborate as a Team by forking the existing Project – Creating branches- Creating Pull requests – Merging 

