# httpcodes

- Intro:
    - HTTP status codes are a set of standardized responses returned by web servers when a client (like a web browser or an API client) makes a request to that server. 
    - These codes are divided into five classes, each signifying a different type of response. Understanding HTTP status codes is crucial for debugging and handling responses in web development.

## Overview of HTTP Status Codes:

1. 1xx Informational:

    - 100 Continue: The server has received the request headers, and the client should proceed to send the request body.
    - 101 Switching Protocols: The requester has asked the server to switch protocols, and the server has agreed.

2. 2xx Success: Indicates that the client's request was successfully received, understood, and accepted.

    - 200 OK: The request was successful, and the server returned the requested resource.
    - 201 Created: The request was successful, and a new resource was created as a result.
    - 204 No Content: The request was successful, but there's no content to send in the response.

3. 3xx Redirection: Indicates that the client must take additional action to complete the request.

    - 301 Moved Permanently: The requested resource has been moved to a new URL permanently.
    - 302 Found: The requested resource is temporarily located at a different URL.
    - 304 Not Modified: The resource has not been modified since the last request, so the client can use the cached version.

4. 4xx Client Errors: Indicates that the client seems to have made an error.

    - 400 Bad Request: The server could not understand the request due to invalid syntax.
    - 401 Unauthorized: The client must authenticate itself to get the requested response.
    - 403 Forbidden: The client does not have access rights to the content.
    - 404 Not Found: The server cannot find the requested resource.
    - 409 Conflict: The request could not be completed due to a conflict with the current state of the target resource.

5. 5xx Server Errors: Indicates that the server failed to fulfill a valid request.

    - 500 Internal Server Error: The server encountered a situation it doesn't know how to handle.
    - 502 Bad Gateway: The server received an invalid response from the upstream server.
    - 503 Service Unavailable: The server is not ready to handle the request, often due to maintenance or overloading.

## Usage in Web Development:

- Success Codes (2xx): Used to confirm that the server has successfully processed the request. For instance, when fetching data from an API, a 200 OK response indicates that the data retrieval was successful.

- Redirection Codes (3xx): Commonly used in URL redirection. For example, when a website moves to a new domain, a 301 Moved Permanently ensures that users are redirected to the new URL.

- Client Error Codes (4xx): Indicate that there was a problem with the request. For example, a 404 Not Found error is shown when a user tries to access a non-existent page.

- Server Error Codes (5xx): These codes are returned when there is a server issue. For example, a 500 Internal Server Error indicates that something went wrong on the server's side.

