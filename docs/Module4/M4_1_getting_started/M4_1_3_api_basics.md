<!-- this section should be the first one, before getting started -->
Before we start with the practical examples of using NOMAD’s API, let's briefly provide a short explanation of essential concepts:

### API (Application Programming Interface):
An API is a set of rules and protocols that allows different software programs to communicate with each other, facilitating communication and data exchange between them.  <!-- before the analogy, I see it helpful to provide some text to explain the components of an API in a formal way -->
<!-- this is an example: -->
It works by sending requests and recieving responses, using several endpoints published by the software to access particular resources or services offered. 
The interaction with an API involves three main parts: the server (which contains the resources), the client (which connects the user and the server), and the user (who initiates requests through the client). The API is hosted on the server and defines the rules and protocols for how the client can interact with the server.
The user doesn't communicate directly with the server. Instead, they send requests through the client (such as a web browser). The client, in turn, follows the rules of the API to properly format and send the request to the server. The server processes the request and uses the API to send the appropriate response back to the client, which then presents it to the user.
This structure ensures that communication is standardized and secure, with the API controlling how data is requested, processed, and delivered. 

You can think of this relationship as similar to a restaurant experience. The user is the diner who interacts with the client, the waiter, by placing an order. The server is the kitchen where the food (data) is prepared. The waiter (the client) doesn't cook the food, but communicates the user's request to the kitchen using a specific protocol (the API). When the meal is ready, the waiter delivers it back to the diner. The diner never interacts directly with the kitchen, just as the user never interacts directly with the server. The API ensures that the process of requesting and delivering data is smooth and follows the correct procedures, just as the waiter ensures that the order is communicated correctly and delivered promptly.
 For a simple explanation, check out this [YouTube video](https://www.youtube.com/watch?v=s7wmiS2mSXY).

<!-- while trying to better understand this as "dummy" in this field, I felt that the connection is missing in the text. For example what is the relationship between API, HTTP, REST-APT, JSON and XML.
I leanred that API in general have several components that are worth introducing at the stage: Endpoints, Requests, Response, Error codes. This this helped me understand that HTTP the the protocol used to make requests in API. And that responses are returned via JSON and XML. I'm still not sure why we talk about REST-API. Do you agree that it is worth explaining these? -->

APIs of software hosted on the web communicate using the Hypertext Transfer Protocol (HTTP) which offers standard methods to send responses to the server and standard responses to report on the status of the request 

Before getting into the details, lets go throught the general workflow of APIs and the essential elements 
### It all starts with Creating a Request
API requests are sent from the user to the server through the client. They include the follwoing elements:
 - HTTP method
 - Endpoints
 - Header
 - Body
<!-- create a code showing the strucutre of these -->
### The servers recieve and process the request
This involves acting on the request by interacting with the system, and perform the requested action. 

### Sending the response from the server to the users through the client
The response includes the following elements:
- Status code
- Header
- Response body (JSON or XML)
<!-- create a code showing the strucutre of these -->
### The user recieves the requested information or service.
The client parses the respons and display it to the user. 

### HTTP (Hypertext Transfer Protocol) request methods:

There are five fundamental HTTP methods used to interact with web-based software:

*   **GET**: Retrieves data from a server at the specified resource. A GET request is used to obtain either a specific item or a collection of items.
*   **POST**: Sends data to the server to create a new resource. The data sent in the request body is used to define the new resource.
*   **DELETE**: Removes the resource at the specified URL. This command is used to delete an existing resource identified by its URL.
*   **PUT**: Updates the target resource with the data provided in the request body or creates it if it doesn’t exist.


> **Note:** NOMAD provides resources to explain the type of possible requests and associated endpoints. Here is an example from the [NOMAD's API Dashboard](https://nomad-lab.eu/prod/v1/api/v1/extensions/docs):
![Example NOMAD API Dashboard](../images/API_dashboard_example.png) 

#### HTTP response status codes

When interacting with APIs, it is also necessary to understand the meaning of the HTTP status codes returned by the server. These codes can help you diagnose and address issues with your requests. Below is an overview of some common and important HTTP status and error codes that you may encounter while using the NOMAD API. For detailed explaination <!-- refer to NOMAD documentation and keep only the table -->

<!-- *   **200 Successful Response**: The request has been successfully processed and the server has sent the expected data in response.
*   **400 Bad Request**: The server could not process the request due to an error in the request itself, such as incorrect syntax or invalid arguments. Review and correct the request syntax and parameters.
*   **401 Unauthorized**: The request lacks valid authentication credentials, or the credentials provided do not grant permission for the requested operation. Verify and include correct authentication details.
*   **404 Not Found**: The server cannot find the specified resource; it may not exist or is unavailable at the given URL. Check the URL and make sure the resource exists.
*   **422 Validation Error**: The request was well-formed but was unable to be followed due to semantic errors. Review the request data for accuracy and completeness, and adjust any values to meet the expected formats and types as specified in the API documentation
-->

| Response Code | Description | Common Causes | Suggested Action |
| --- | --- | --- | --- |
| 200 | Successful Response | Correct request execution | None needed |
| 400 | Bad Request | Syntax errors, invalid arguments | Fix syntax and parameters |
| 401 | Unauthorized | Invalid credentials | Verify credentials |
| 404 | Not Found | Incorrect URL, missing resource | Check URL and resource |
| 422 | Validation Error | Semantic errors in data | Adjust data to API Documentaion |

<!-- I don't think we need to explain RESR API, lets only describe the formats of the response message sent by the client -->
### HTTP response body formats: 
Data in the response body is usually exchanged in well-known and standard formats like JSON or XML. 

**JSON** (JavaScript Object Notation) is a format for structuring data as key-value pairs, making it easy for humans to read and machines to parse.
```json
{
  "name": "Max Mustermann",
  "role": "Lab Technician",
  "email": "max.mustermann@uni-something.de",
  "phone": "+49 123 456789"
}
```

**XML** (eXtensible Markup Language): is a markup language for encoding documents, enabling both human readability and machine readability, often used for data storage and transport.

```xml
<contact>
  <name>Max Mustermann</name>
  <role>Lab Technician</role>
  <email>max.mustermann@uni-something.de</email>
  <phone>+49 123 456789</phone>
</contact>

```
