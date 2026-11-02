# Web Development and Computer Fundamentals

## Interview Preparation Notes

### Goal

Understand what happens from the moment a user enters a website address until the page is displayed and can interact with data.

---

## 1. What is the Internet?

The **Internet** is a global network of interconnected computer networks. Devices communicate over it using agreed networking protocols, such as the Internet Protocol (IP) and TCP.

The Internet is infrastructure: it carries data between devices. The World Wide Web, email, messaging, voice calls, and many other services use that infrastructure.

**Interview answer:** The Internet is the underlying global network that connects devices and transports data.

## 2. What is the World Wide Web?

The **World Wide Web (WWW or Web)** is a system of interlinked documents and resources that users access over the Internet. Web browsers retrieve resources using protocols such as HTTP and HTTPS and display them using formats such as HTML, CSS, and JavaScript.

A webpage can link to other resources using hyperlinks, which form part of the Web's interconnected structure.

## 3. Internet vs. World Wide Web

| Internet | World Wide Web |
|---|---|
| Global network infrastructure | A service that operates over the Internet |
| Connects networks and devices | Provides linked websites and web applications |
| Carries many types of traffic | Commonly uses HTTP or HTTPS |
| Also supports services such as email and voice calls | Accessed primarily through browsers or other HTTP clients |

**Analogy:** The Internet is the road network; the Web is one kind of service that travels over it.

## 4. What is a website?

A **website** is a collection of related web pages and resources, commonly served under a domain name. A website may contain documents, images, stylesheets, scripts, and other media.

The word “website” often refers to the published collection of pages, while “webpage” refers to one individual document. A website can be static, dynamic, or a combination of both.

## 5. What is a web application?

A **web application** is software accessed through a web browser or another web client. It typically provides interactive tasks, such as editing a document, submitting a form, managing projects, or viewing a dashboard.

Web applications commonly combine:

- A user interface rendered in the browser.
- Application logic running in the browser, on a server, or both.
- Server endpoints for processing requests.
- Data sources such as databases or external services.

The distinction between a website and a web application is not strict. A single product can contain both informational pages and application features.

## 6. Static vs. dynamic websites

### Static websites

A static site serves files such as HTML, CSS, and JavaScript, often without generating personalized page content for each request.

- Easy to cache and distribute through a content delivery network.
- Can be fast and straightforward to host.
- JavaScript can still make a static page interactive.
- “Static” describes how the page is delivered; it does not mean the page must be visually or behaviorally inert.

### Dynamic websites

A dynamic site can generate or personalize a response using request data, server-side code, application state, or database information.

- May return different content depending on a user's request or account.
- Often interacts with backend services and databases.
- Requires appropriate application logic, infrastructure, and security.

Many modern sites use a hybrid approach: some pages are statically generated or cached, while interactive features fetch changing data from APIs.

## 7. Frontend vs. backend

### Frontend

The **frontend** is the part of an application presented to users, commonly running in a browser. It includes the interface, layout, styling, and client-side interactions.

Common technologies include HTML, CSS, and JavaScript or TypeScript.

### Backend

The **backend** handles server-side responsibilities such as application rules, authentication, authorization, data processing, and database access. It can expose APIs that frontend clients use.

### How they work together

The frontend sends a request to a backend endpoint. The backend validates and processes the request, may retrieve or update data, and returns a response. The frontend then presents the result.

Frontend input is not automatically trustworthy. The backend must enforce validation, authentication, and authorization where required.

## 8. Client vs. server

- A **client** initiates a request for a resource or service. A web browser is a common client.
- A **server** receives requests, processes them, and returns responses. A server may be a physical machine, a virtual machine, a container, or a managed cloud service.

“Client” and “server” describe roles in communication, not necessarily particular hardware. A program can act as a client in one interaction and a server in another.

## 9. What is a browser?

A **browser** is application software that retrieves, interprets, and presents web resources. Examples include Chrome, Firefox, Safari, and Edge.

A browser commonly:

- Parses HTML and builds a DOM (Document Object Model).
- Parses CSS and calculates styles and layout.
- Executes JavaScript.
- Fetches additional resources such as images, stylesheets, and API responses.
- Draws the page and handles user input.
- Provides developer tools, storage, and browser APIs.

Browser behavior is not just “show the HTML”: it combines parsing, resource loading, layout, painting, scripting, and user interaction.

## 10. How browsers work

At a high level, navigating to a webpage involves these activities:

1. **Parse the URL** to identify the scheme, host, port if present, path, query, and fragment.
2. **Resolve the hostname** to an IP address, commonly through DNS and possibly cached results.
3. **Establish a network connection** to the destination. HTTPS also negotiates a secure TLS connection.
4. **Send an HTTP request** for the resource.
5. **Receive the response**, including a status code, headers, and possibly an HTML document.
6. **Parse HTML** and build the DOM. The browser discovers linked CSS, scripts, images, and other resources.
7. **Fetch and process resources.** CSS contributes to style calculation; JavaScript can modify the DOM and request more data.
8. **Calculate layout** and **paint** the visible result.
9. **Respond to user actions** such as clicks, typing, scrolling, and navigation.

This is a conceptual sequence. Browsers can overlap network and processing work, reuse connections, use caches, and render parts of a page before every resource has finished loading.

### Rendering terms to know

- **DOM:** tree-like representation of parsed HTML.
- **CSSOM:** representation of parsed CSS rules.
- **Render tree:** structures used to determine what is rendered and how.
- **Layout:** calculation of element positions and dimensions.
- **Paint:** drawing pixels for visual output.
- **JavaScript execution:** can update the DOM, styles, or application state and cause rendering work.

## 11. What is a web server?

A **web server** is software that accepts HTTP requests and returns HTTP responses. It may:

- Serve files such as HTML, images, or CSS.
- Route requests to application code.
- Forward requests to another service or API.
- Apply configuration such as caching and TLS handling.

The term “server” can refer to server software, the computer it runs on, or the role that software plays. Common server software includes Nginx, Apache HTTP Server, and application servers built with various programming languages.

## 12. What is hosting?

**Hosting** is providing the compute, storage, networking, and related services needed to make a site or application available over a network.

Hosting may be provided by:

- Static hosting or a content delivery network for static assets.
- A virtual machine, container platform, or application hosting service.
- A serverless or managed platform.
- A combination of these services.

Hosting and a domain name are different: hosting provides the infrastructure; a domain provides a human-readable name that can be configured to point to services.

## 13. What is a domain name?

A **domain name** is a human-readable name used to identify a location or service on the Internet, such as `example.com`.

- A domain name is not the same as a webpage or website, although people often use it as shorthand.
- Domain names are organized hierarchically. In `www.example.com`, `com` is the top-level domain, `example` is a label beneath it, and `www` is a subdomain.
- Domain registration and DNS configuration are related but separate tasks.

## 14. What is DNS?

The **Domain Name System (DNS)** is a distributed naming system that helps translate domain names into information clients can use to locate services, commonly including IP addresses.

Conceptually:

```text
www.example.com  →  DNS lookup  →  an IP address
```

In practice:

- A resolver may answer from its cache.
- DNS records can provide different kinds of information, such as address records or mail-routing information.
- One domain can resolve to multiple addresses, and DNS answers can change over time.
- DNS locates a destination; it does not itself serve the webpage.

## 15. What is an IP address?

An **IP address** is a numerical address used to identify a network interface or destination for Internet Protocol communication.

- IPv4 addresses use a 32-bit format, commonly written as four decimal numbers, such as `192.0.2.10`.
- IPv6 addresses use a 128-bit format, commonly written in hexadecimal groups, such as `2001:db8::10`.
- A domain name can resolve to one or more IP addresses.
- An IP address is not necessarily a permanent identifier for a person or device; addresses can be shared, assigned dynamically, or hidden behind network infrastructure.

## 16. What is HTTP?

**HTTP** (Hypertext Transfer Protocol) is an application-layer protocol used to transfer web resources through requests and responses.

An HTTP request commonly includes:

- A method, such as `GET`, `POST`, `PUT`, `PATCH`, or `DELETE`.
- A path and optional query parameters.
- Headers describing the request.
- An optional body, often used to send data.

An HTTP response commonly includes:

- A status code, such as `200`, `404`, or `500`.
- Response headers.
- An optional body, such as HTML or JSON.

### Common methods

- **GET:** retrieve a resource; should not be used to perform a state-changing action.
- **POST:** submit data or request processing; commonly used when creating or submitting data.
- **PUT:** create or replace a resource at a known URL, according to the API's design.
- **PATCH:** apply a partial update, according to the API's design.
- **DELETE:** request removal of a resource.

The exact behavior depends on the server and API. Do not rely on a frontend method alone to enforce permissions or correctness.

### Common status-code groups

- **1xx:** informational.
- **2xx:** success, for example `200 OK` or `201 Created`.
- **3xx:** redirection.
- **4xx:** client/request-related issue, for example `400 Bad Request`, `401 Unauthorized`, `403 Forbidden`, or `404 Not Found`.
- **5xx:** server-side failure, for example `500 Internal Server Error`.

## 17. What is HTTPS?

**HTTPS** is HTTP carried over a connection protected by TLS (Transport Layer Security).

TLS helps provide:

- **Confidentiality:** protects data in transit from being read by network observers.
- **Integrity:** helps detect tampering with data in transit.
- **Authentication:** certificates help the client verify the identity of the server for the requested hostname.

HTTPS does **not** by itself guarantee that:

- The website is trustworthy or free of malicious content.
- A user's device is secure.
- Data is encrypted while stored on the server.
- The application has correct authorization or protects data against every attack.

Never ask users to send sensitive information over an unprotected connection. HTTPS is essential for secure web applications, but application security requires more than TLS.

## 18. What is a URL?

A **URL** (Uniform Resource Locator) identifies a resource and describes how to locate it. Example:

```text
https://shop.example.com:443/products?category=books#featured
```

| Component | Example | Purpose |
|---|---|---|
| Scheme | `https` | Protocol or access method |
| Hostname | `shop.example.com` | Destination name |
| Port | `443` | Network service port; often omitted when it is the default |
| Path | `/products` | Resource or route |
| Query string | `?category=books` | Parameters sent with the request |
| Fragment | `#featured` | Location within a resource, often handled by the browser |

A fragment is generally not sent to the server as part of the HTTP request; the browser uses it to identify a location or client-side state.

In everyday development, “URL” is commonly used for a web address. More formally, a URI is a broader identifier category and a URL is a locator.

## 19. What is an API?

An **API** (Application Programming Interface) is a defined way for software components to communicate. A web API lets a client send requests to endpoints and receive responses, often using HTTP and JSON.

Example request:

```http
GET /api/projects/42 HTTP/1.1
Host: api.example.com
Accept: application/json
```

Example response:

```http
HTTP/1.1 200 OK
Content-Type: application/json

{"id":42,"name":"Image preparation"}
```

An API contract typically describes endpoints, request methods, parameters, authentication requirements, response formats, and errors.

- An API is not necessarily a database; it may coordinate multiple services or return computed results.
- A frontend should handle loading, success, and error responses.
- Never assume that hiding a button in the frontend protects an API; authorization must be enforced by the server.

## 20. What is a database?

A **database** is an organized system for storing and retrieving data.

Examples of database models include:

- **Relational databases:** store data in tables with defined relationships and are commonly queried with SQL.
- **Document databases:** store records as document-like structures, often JSON-like.
- Other systems specialize in key-value access, graph relationships, time series, and more.

In a web application, the backend commonly communicates with the database instead of exposing database credentials or direct database access to the browser.

Important concepts:

- **Schema:** describes the structure and constraints of stored data.
- **Query:** asks the database to retrieve or change data.
- **Transaction:** groups operations with defined consistency properties.
- **Index:** can speed up certain queries at a storage and maintenance cost.

## 21. Request-response lifecycle

A typical request to a dynamic website may look like this:

1. The user enters a URL or clicks a link.
2. The browser parses the URL and checks relevant caches.
3. DNS resolution identifies an address for the hostname if needed.
4. The browser establishes a connection. With HTTPS, it negotiates TLS.
5. The browser sends an HTTP request to the server.
6. A web server, gateway, or load balancer receives and routes the request.
7. Backend application code validates the request and applies authentication and authorization where needed.
8. The backend may call other APIs or query a database.
9. The backend creates an HTTP response with a status code, headers, and content.
10. The server sends the response to the browser.
11. The browser processes the response and displays or updates the page.
12. The browser may make additional requests for stylesheets, scripts, images, fonts, or API data.

Not every request follows every step. Caches, content delivery networks, service workers, static hosting, and server-side rendering can change the route and timing.

## 22. Basic client-server architecture

```text
User
  ↓ interacts with
Browser / frontend (client)
  ↓ HTTP(S) request
Web server / gateway
  ↓ route or invoke
Backend application
  ↓ query / transaction
Database
  ↑ result
Backend application
  ↑ HTTP(S) response
Browser renders the result for the user
```

The client is responsible for presenting and collecting information. The backend owns trusted application rules and coordinates data access. The database stores information. These are logical responsibilities; in a small app they may run on one machine, while at scale they may run across many services.

### Why not connect a public browser directly to a private database?

- Database credentials would be exposed to users.
- Access rules and validation could be bypassed.
- The database would be exposed to untrusted clients.
- A backend provides a controlled interface for authentication, authorization, validation, and auditing.

## End-to-end example: opening a project page

Suppose a user visits:

```text
https://app.example.com/projects?sort=recent
```

1. The browser parses HTTPS, the hostname, the path, and the query string.
2. DNS resolves `app.example.com` to an address (or a cached answer is used).
3. The browser establishes a TLS-protected connection to the service.
4. It sends a request for `/projects?sort=recent`.
5. The web service serves a page or routes the request to the application.
6. The application may check the user's access and retrieve project data from a database.
7. The service responds with HTML, JSON, or another representation and an HTTP status.
8. The browser processes the response, loads required resources, and renders the page.
9. A user interaction may trigger another HTTP request to an API endpoint.

## Common interview misconceptions

- **The Internet and the Web are not synonyms.** The Web is one service that uses the Internet.
- **DNS resolves names; it does not serve the website.**
- **A domain is a name, not the hosting service or website itself.**
- **HTTPS protects a connection; it does not prove that the site's content is safe.**
- **Frontend validation can improve usability, but backend validation is still required.**
- **A browser is more than a renderer:** it fetches resources, parses documents, runs scripts, lays out and paints content, and manages user interactions.
- **A static site can still have interactive JavaScript.**
- **An API is an interface; it is not necessarily a database.**
- **The browser should not contain private database credentials.**

## Quick interview questions

### 1. What happens when you enter a URL in a browser?

The browser parses the URL, resolves its hostname using DNS when necessary, establishes a connection, negotiates TLS for HTTPS, sends an HTTP request, receives a response, and processes its content. It then loads relevant resources, builds the page representation, calculates layout, paints the page, and runs its interactive code. Browsers can cache and parallelize parts of this process.

### 2. How do a website and a web application differ?

A website commonly presents related web pages or information. A web application emphasizes interactive tasks and application behavior. The categories overlap: one product can be both.

### 3. What is the difference between HTTP and HTTPS?

HTTPS is HTTP protected by TLS. TLS helps protect data in transit and verify the server's identity; it does not guarantee that the application itself is trustworthy or correctly secured.

### 4. What is the role of DNS?

DNS maps domain names to records, commonly IP addresses, so clients can locate network services. It does not retrieve the webpage content itself.

### 5. What is the difference between a client and a server?

A client initiates a request for a resource or service. A server receives requests and provides responses. These are communication roles, not necessarily fixed hardware types.

### 6. Why does an application usually use a backend between the browser and its database?

The backend provides a controlled place to enforce authentication, authorization, validation, application logic, and database access without exposing database credentials to untrusted browsers.

### 7. Where do query parameters and fragments go?

Query parameters are part of the URL sent with an HTTP request. A fragment identifies a location or client-side state and is generally handled by the browser rather than sent to the server in the request.

## Quick glossary

| Term | Short definition |
|---|---|
| Internet | Global network infrastructure connecting devices and networks |
| WWW | Interlinked web resources accessed over the Internet |
| Browser | Client software that retrieves and processes web resources |
| Client | Software or device that initiates a request |
| Server | Software or system that receives requests and returns responses |
| DNS | Distributed system for resolving domain names to records |
| IP address | Network-layer address used to route Internet Protocol traffic |
| HTTP | Request-response protocol for transferring web resources |
| HTTPS | HTTP protected by TLS |
| URL | Address that identifies how and where to locate a resource |
| API | Defined interface through which software components communicate |
| Database | System that stores and retrieves organized data |
| Hosting | Infrastructure and services used to make an application available |

## Final study checklist

- Explain Internet vs. Web without treating the terms as interchangeable.
- Describe the roles of the browser, DNS, IP address, HTTP, server, and database.
- Walk through a request-response lifecycle in the correct general order.
- Distinguish frontend, backend, client, and server responsibilities.
- Compare static, dynamic, and hybrid sites.
- Explain what HTTPS protects and what it does not guarantee.
- Identify the major parts of a URL.
- Explain why validation and authorization belong on the backend, even if the frontend also checks input.
