HTTP is a foundational technology for the World Wide Web, enabling communication between clients (usually web browsers) and servers. It operates at the application layer of the [[OSI]] model and is characterized by its stateless [[protocols#Main Network Protocols|protocol]]
nature, though modern web applications often employ various methods to create a stateful session.

## Core Features of HTTP

### Client-Server Model
HTTP follows a request-response pattern where the client initiates an HTTP request, and the [[server]] responds with the requested resources or an error message.
### Port
The default [[port]] for HTTP is `80`, but it can operate on any other specified port.
### Stateless Protocol
HTTP itself does **not retain** any memory of past transactions. However, for web applications requiring user sessions, mechanisms like cookies, headers, and session storage are used to maintain state.
### Methods (Verbs)
HTTP defines a set of request methods, which indicate the desired action to be performed:
- `GET`: Retrieve data from the server.
- `POST`: Send data to the server to create or update a resource.
- `PUT`: Replace the current representation of the resource with the uploaded content.
- `PATCH`: Partially update the resource.
- `DELETE`: Delete the specified resource.
- `OPTIONS`: Describe the communication options for the target resource.
### Status Codes
HTTP response status codes indicate whether a specific HTTP request has been successfully completed:

- `100-199`: Informational responses, indicating that the request was received and understood.
- `200-299`: Success, indicating that the request was successfully received, understood, and accepted.
- `300-399`: Redirection, indicating that further action needs to be taken to complete the request.
- `400-499`: Client errors, indicating that there was likely an error in the request.
- `500-599`: Server errors, indicating that the server failed to fulfill a valid request.
### Headers
HTTP headers let the client and the server pass additional information with an HTTP request or response. Headers can be used for negotiating content-type, caching policies, authentication, etc.
### Caching
HTTP caching can be used to temporarily store copies of resources, reducing latency and server load.
### Cookies
Cookies are data sent from the server and stored on the client's computer by the web browser while the user is browsing, often used to remember stateful information.
### Sessions
Sessions are server-side storages which help in maintaining user state and data across multiple HTTP requests.
## Content Negotiation
Clients and servers can use HTTP headers to specify and negotiate resource formats like HTML, XML, JSON, etc.
## Data Encoding and Forms

### `application/x-www-form-urlencoded`
This is the default content type. Form data is encoded as key-value pairs, similar to URI query strings.
### `multipart/form-data`
Used for more complex form submissions, including file uploads. Data is sent as a series of "parts," each with its own content disposition and type.
### `application/json`
Commonly used with RESTful APIs, data is encoded as a JSON object.
### `text/plain`
A simple encoding of data where the body is not parsed, sent as-is.

## Security Considerations
HTTP is plainly not secure, everything is send on plain text, anyone could sniff your data, This is why [[HTTPS]] was created
## Integration with [[REST]]

HTTP is often used as the basis for REST (Representational State Transfer), an architectural style for distributed hypermedia systems. RESTful APIs use HTTP requests to perform CRUD operations (Create, Read, Update, Delete) on resources, using the protocol's built-in methods.