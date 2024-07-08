# Blackstar API Documentations

### Introduction

Welcome to the Blackstar Developer Documentation where you'll learn how to integrate our Investment products with Blackstar APIs.

#### API Basics

> **_Before you begin!_**
> To get started, please contact us to create an account for your organization. We will provide you with test accounts that you can use to test and make API calls.


The Blackstar API provides access to virtually all the features available on our [app](), allowing you to integrate and extend them within your own application. Designed to be RESTful, the API is organized around the primary resources you'll interact with.

##### HTTP Methods

| Method | Description                                                                                                                                                                                                                                                                                                       |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| POST   | Used to create a new resource on the server. The client sends data to the server in the body of the request, and the server processes the data to create a new record. The response typically contains the newly created resource's location and details.                                                         |
| GET    | Retrieves a specific resource or a collection of resources from the server. The client sends a request with optional parameters to filter or specify the data, and the server responds with the requested information. This method does not modify any data on the server.                                        |
| PUT    | Updates an existing resource on the server. The client sends the complete resource data in the body of the request, and the server replaces the current resource with the provided data. This method is idempotent, meaning multiple identical requests will produce the same result.                             |
| GET    | Similar to the previous GET method, it retrieves a specific resource or a collection of resources from the server. The client sends a request with optional parameters to filter or specify the data, and the server responds with the requested information. This method does not modify any data on the server. |

#### Sample Requests

We provide sample API calls for each endpoint using cURL and Axios. All you need to do is insert your specific parameters, and you can test the calls from your HTTP client.

#### Request and Response

Both request body data and response data are formatted as JSON. Examples are given for each endpoint. Content type for responses will always be `application/json` except for file uploads.

#### Base URL

- UAT : `https://api.uatdev.gnii.ai`
- PRODUCTION: `https://api.gnii.ai`

`Note: You need your IP address whitelisted to use in PRODUCTION`
