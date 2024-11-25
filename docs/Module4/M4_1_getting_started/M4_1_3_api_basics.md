Before we start with the practical examples of using NOMAD’s API, let's briefly provide a short explanation of essential concepts:

## What is API?

An API, Application Programming Interface, is a set of rules and protocols that allows different software programs or hardware to communicate with each other, facilitating communication and data exchange between them. APIs are widely used across various systems, including web-based services, database systems, operating systems, and even hardware interactions.

In the context of this tutorial, we focus on APIs used for web-based interactions, such as those employed by NOMAD to facilitate data access and management.

An API works by sending **requests** and receiving **responses**, using specific **endpoints** defined by the API to access particular resources or services. Data are usually exchanged in standard formats like JSON or XML. The interaction with an API involves three main parts:

* **The User**: Initiates requests, typically through a client application.
* **The Client**: A software that formats and sends the user’s requests according to the API's rules.
* **The Server**: A system that processes requests and provides the appropriate responses, often hosting the API.

??? info "What is an API Client?"
    API clients are tools, libraries, or software that enable interaction with APIs. Each type serves specific purposes, from quick testing to developing full-scale applications. Here are some common types:

    - **Command-line tools** like `cURL` are lightweight and flexible, ideal for testing and debugging APIs.
    - **Programming libraries** such as Python's `requests` allow to integrate API calls into analysis applications and automation programmatically.
    - **Software** like web browsers (e.g., Chrome, Firefox) or Postman provide user-friendly interfaces for exploring and interacting with APIs.

The user does not directly interact with the server. Instead, they rely on the client to communicate with the API. The client formats the user’s request, sends it to the server, and processes the response from the API to present it to the user. The API specifies how these requests and responses are structured, ensuring that communication is standardized and secure.

You can think of this relationship as similar to a restaurant experience.:[^1] you (the user) place your order (the request), and the waiter (the client) brings it to the kitchen (the server). After your dish (the data) is prepared, the waiter delivers it back to you (the response). This *waiter-service interaction* is similar to how an API functions as a *messenger* between you and an application. The API ensures that requests are formatted correctly and responses are delivered accurately, much like the waiter ensures the order is communicated to the kitchen and delivered to the diner.

Web-hosted APIs often use the Hypertext Transfer Protocol (HTTP), which provides standard methods for sending requests and receiving responses, as well as reporting the status of these interactions.

??? info "What are different types of APIs?"
    APIs connect systems, and their types differ to meet diverse functionality and performance demands. Here are the 3 widely used ones.

    - **REST (Representational State Transfer)**: The most commonly used API for web-hosted services, relying on HTTP methods and data formats like JSON (e.g., NOMAD).
    - **GraphQL**: A flexible API type that allows clients to request only the data they need, reducing inefficiencies (e.g., GitHub).
    - **Webhooks**: Event-driven APIs that send real-time updates to clients when specific events occur (e.g., Discord, PayPal).

??? info "Common data formats used by APIs: JSON and XML"
    APIs often use standardized formats to exchange data. The two most common ones are:

    - **JSON (JavaScript Object Notation)**: A lightweight format that represents data as key-value pairs, making it easy for both humans and machines to read and process.

    ```json
    {
      "name": "Max Mustermann",
      "role": "Lab Technician",
      "email": "max.mustermann@uni-something.de",
      "phone": "+49 123 456789"
    }
    ```

    - **XML (eXtensible Markup Language)**: A markup language designed for data transport and storage, structured in a readable, hierarchical format.

    ```xml
    <contact>
      <name>Max Mustermann</name>
      <role>Lab Technician</role>
      <email>max.mustermann@uni-something.de</email>
      <phone>+49 123 456789</phone>
    </contact>
    ```


??? info "What is HTTP?"
    HTTP, or Hypertext Transfer Protocol, is a standardized set of rules for exchanging data over the web. It enables communication between clients (like browsers or applications) and servers, allowing requests for and delivery of resources such as webpages, images, or data.

    When you enter a website address (URL) into your browser, the browser sends an HTTP request to the server hosting that site. The server processes the request and responds with the required data, which the browser then renders for you to interact with. HTTP is not just for web browsing—it also forms the foundation for APIs, enabling communication and data exchange between systems.

    The most frequently used HTTP methods for interacting with resources are:
    
    - **GET**: Retrieves data from a server. Commonly used to fetch webpages or resources.
    - **POST**: Sends data to the server to create a new resource.
    - **DELETE**: Removes a resource from the server at a specified URL.
    - **PUT**: Updates an existing resource or creates a new one if it doesn’t exist.

Before getting into the details, lets go throught the general workflow of APIs and the essential elements:

## What is the general API workflow?

**1. It all starts with creating a request:**

API requests are prepared by the user and sent to the server through the client. A request typically includes the following elements:

- **HTTP Method**: Specifies the action to be performed (e.g., GET, POST, DELETE).
- **Endpoint**: The URL of the resource or service on the srver.
- **Headers**: Provide metadata, such as authentication tokens or content type.
- **Body**: Contains the data required for actions like creating or updating resources.

??? info "What is an API endpoint?"
    An API endpoint is a specific URL that acts as an entry point to interact with a particular resource or service provided by an API. Endpoints define *where* requests should be sent and *what actions* can be performed.

    For example, in NOMAD's API, each resource is associated with specific endpoints that allow you to retrieve, create, update, or delete data. The [NOMAD API Dashboard](https://nomad-lab.eu/prod/v1/api/v1/extensions/docs){:target="_blank"} highlights these endpoints and the types of requests they support:
    ![Example NOMAD API Dashboard](../images/API_dashboard_example.png)

**2. Processing the request by the server:**

The server receives the request, and validates it. If valid, the server interacts with its resources (e.g., a database or application) and prepares a response. Otherwise, it prepares an error response (e.g., status code 400 for a bad request).

**3. Sending the back the response:**

The server sends the response back through the client, which includes:

  * **Status Code**: A numeric code telling that the request was successful (200), or why it failed. (e.g., 404). 
  * **Headers**: Provide metadata about the response.
  * **Body**: Contains the data or error details, and typically comes in formats like JSON or XML.

??? info "What are HTTP status codes?"
    These codes can help you diagnose and address issues with your requests by indicating whether the request was successful or if an error occurred. Here are the main status codes you might receive from NOMAD API and how to address errors in case of a failure:

    | Response Code | Description           | Common Causes                   | Suggested Action                     |
    |---------------|-----------------------|----------------------------------|--------------------------------------|
    | **200**       | Successful Response   | Correct request execution       | None needed                          |
    | **400**       | Bad Request           | Syntax errors, invalid arguments| Fix syntax and parameters            |
    | **401**       | Unauthorized          | Invalid credentials             | Verify credentials                   |
    | **404**       | Not Found             | Incorrect URL, missing resource | Check URL and resource               |
    | **422**       | Validation Error      | Semantic errors in data         | Adjust data to API documentation     |



---
[^1]: For a visual explanation of how APIs work, you may find this [YouTube video](https://www.youtube.com/watch?v=s7wmiS2mSXY){:target="_blank"} helpful.
