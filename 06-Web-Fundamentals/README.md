# Module 6: How the Web Works

## Overview

In this module, I learned how websites and web applications communicate
over the Internet.

The module helped me understand what happens behind the scenes when I enter
a website address into a browser, including how DNS resolves domain names,
how HTTP requests and responses work, how web servers deliver content, and
how technologies such as HTML, CSS, and JavaScript are used to build websites.

I also learned about HTTP methods, status codes, headers, cookies, URLs,
web servers, and some basic web security concepts.

---

# 1. DNS - Domain Name System

DNS (Domain Name System) provides a way for us to use easy-to-remember
domain names instead of having to remember IP addresses.

For example, instead of remembering an IP address for a website, I can use
a domain name such as:

example.com

DNS can translate that domain name into the IP address needed to communicate
with the server.

A simple way I understand DNS is:

Domain Name → DNS Lookup → IP Address → Connect to Server

---

## Domain Name Structure

A domain name can contain different sections.

For example:

www.example.com

### Top-Level Domain (TLD)

The TLD is the rightmost part of a domain name.

Examples include:

- `.com`
- `.org`
- `.net`
- `.edu`
- `.uk`

There are different categories of TLDs.

### Generic Top-Level Domains (gTLD)

These are general-purpose top-level domains.

Examples:

- `.com`
- `.org`
- `.net`

### Country-Code Top-Level Domains (ccTLD)

These are associated with countries or territories.

Examples:

- `.uk` - United Kingdom
- `.ca` - Canada
- `.ng` - Nigeria

### Subdomains

A subdomain appears before the main domain.

For example:

blog.example.com

Here, `blog` is the subdomain.

Organizations can use subdomains to separate different parts of their
services, such as:

mail.example.com

support.example.com

---

# 2. DNS Record Types

DNS contains different types of records.

Some important ones I learned about are:

| Record | Purpose |
|---|---|
| A | Maps a hostname/domain to an IPv4 address |
| AAAA | Maps a hostname/domain to an IPv6 address |
| CNAME | Points one hostname to another hostname |
| MX | Identifies mail servers responsible for receiving email for a domain |
| TXT | Stores text information associated with a domain |

The two records I focused on initially were `A` and `AAAA`.

### A Record

An A record is used to resolve a hostname to an IPv4 address.

### AAAA Record

An AAAA record is used to resolve a hostname to an IPv6 address.

---

# 3. HTTP and HTTPS

HTTP stands for **Hypertext Transfer Protocol**.

It defines rules that clients and web servers use to communicate.

A typical interaction involves:

1. A client sends an HTTP request.
2. The web server receives and processes the request.
3. The server returns an HTTP response.

The browser is an example of an HTTP client.

---

## HTTPS

HTTPS stands for **Hypertext Transfer Protocol Secure**.

It is HTTP communication protected using TLS encryption.

HTTPS helps protect information travelling between the client and server
from being easily read or modified by someone intercepting the traffic.

Common ports are:

| Protocol | Common Port |
|---|---:|
| HTTP | 80 |
| HTTPS | 443 |

A port number alone does not guarantee what application or protocol is
actually being used, but these are the standard ports associated with HTTP
and HTTPS.

---

# 4. URLs

URL stands for **Uniform Resource Locator**.

A URL tells a client where a resource is located and how it should be
accessed.

An example structure is:

https://example.com:443/products?id=10#reviews

A URL can contain several components.

### Scheme

Example:

https://

The scheme identifies the protocol that should be used.

Common examples include HTTP and HTTPS.

### Host

Example:

example.com

The host identifies the server the client wants to communicate with.

It can be a domain name or an IP address.

### Port

Example:

:443

The port identifies the network service the client wants to connect to.

HTTP normally uses port 80 and HTTPS normally uses port 443.

### Path

Example:

/products

The path identifies a particular resource or location on the server.

### Query String

Example:

?id=10

Query strings can pass additional information to a web application.

### Fragment

Example:

#reviews

A fragment normally points the browser to a particular section of a page.
It is generally handled by the client/browser and is not normally sent to
the web server as part of the HTTP request.

---

# 5. HTTP Requests and Responses

Communication using HTTP normally consists of a request and a response.

## HTTP Request

The client sends a request to the server.

A simplified request could look like:

GET /index.html HTTP/1.1
Host: example.com
User-Agent: Browser

The request can contain:

- HTTP method
- Requested path
- Protocol version
- Headers
- Sometimes a request body

## HTTP Response

The server processes the request and sends a response.

A simplified response could look like:

HTTP/1.1 200 OK
Content-Type: text/html

The response can contain:

- HTTP version
- Status code
- Headers
- Response body

---

# 6. HTTP Methods

HTTP methods tell the server what action the client wants to perform.

## GET

`GET` is commonly used to retrieve information or resources from a server.

Example:

GET /profile

## POST

`POST` is commonly used to submit data to a server.

Examples include:

- submitting a form
- sending login information
- creating data through a web application

## PUT

`PUT` is generally used to create or replace/update a resource at a
specified location.

## DELETE

`DELETE` requests that a resource be removed.

These methods describe the intended action, but the server ultimately
decides whether the request is allowed and how it is processed.

---

# 7. HTTP Status Codes

HTTP status codes tell the client what happened after the server processed
a request.

They are grouped into five main categories.

| Range | Meaning |
|---|---|
| 100-199 | Informational |
| 200-299 | Success |
| 300-399 | Redirection |
| 400-499 | Client errors |
| 500-599 | Server errors |

I do not need to memorize every HTTP status code, but understanding the
categories and recognizing common ones is useful.

---

## Common HTTP Status Codes

### 200 - OK

The request was successfully processed.

### 201 - Created

The request succeeded and resulted in a new resource being created.

### 301 - Moved Permanently

The requested resource has permanently moved to another location.

### 302 - Found

The resource is temporarily available at another location.

### 400 - Bad Request

The server could not properly process the request, often because the
request was malformed or invalid.

### 401 - Unauthorized

Authentication is required or the supplied authentication credentials are
missing or invalid.

Despite the name "Unauthorized", this status is mainly associated with
authentication.

### 403 - Forbidden

The server understood the request but refuses to allow access.

### 404 - Not Found

The requested resource could not be found.

### 405 - Method Not Allowed

The requested HTTP method is not allowed for that resource.

### 429 - Too Many Requests

The client has sent too many requests within a certain period of time.

This is commonly associated with rate limiting.

### 500 - Internal Server Error

The server encountered an unexpected problem while processing the request.

### 503 - Service Unavailable

The server is temporarily unable to handle the request.

---

# 8. HTTP Headers

HTTP headers contain additional information about requests and responses.

They help the client and server understand how the communication should be
handled.

## Common Request Headers

### Host

Identifies the hostname the client wants to access.

Example:

Host: example.com

### User-Agent

Provides information about the client making the request, such as a browser
or other software.

### Content-Length

Indicates the size of the request body in bytes.

### Accept-Encoding

Tells the server which content encodings/compression methods the client can
understand.

### Cookie

Sends previously stored cookie information back to the server.

---

## Common Response Headers

### Set-Cookie

Tells the browser to store a cookie.

### Content-Type

Describes the type of content being returned.

Examples include:

text/html

application/json

### Content-Encoding

Describes any encoding or compression applied to the response content.

### Cache-Control

Provides instructions about how the response may be cached.

---

# 9. Cookies

Cookies are small pieces of data that a website can ask a browser to store.

HTTP itself is **stateless**, meaning each HTTP request is independent and
does not automatically remember previous requests.

Cookies can help websites maintain state across multiple requests.

They can be used for things such as:

- session management
- authentication/session identifiers
- website preferences
- other application state

For example, after logging into a website, a session cookie may help the
website recognize subsequent requests as belonging to the same session.

Because cookies may contain sensitive session information, protecting them
is important for web security.

---

# 10. How Websites Work

A website generally involves two major sides:

## Front End - Client Side

The front end is the part of a website that users interact with through
their browser.

Common technologies include:

### HTML

HTML (HyperText Markup Language) provides the structure and content of a
web page.

### CSS

CSS (Cascading Style Sheets) controls the presentation and appearance of
the page.

### JavaScript

JavaScript adds logic and interactive behaviour to websites.

A simple way I remember them is:

HTML → Structure

CSS → Appearance

JavaScript → Behaviour and interactivity

---

# 11. Back End - Server Side

The back end runs on servers and handles the processing that users normally
do not see directly.

Depending on the application, the back end may:

- process requests
- authenticate users
- interact with databases
- apply application logic
- return information to the client

The front end and back end communicate through requests and responses.

---

# 12. Web Servers

A web server is software that listens for incoming web requests and uses
HTTP/HTTPS to deliver web content to clients.

Examples of widely used web server software include Apache HTTP Server,
Nginx, and Microsoft IIS.

When I visit a website, the basic process can be simplified as:

Browser
   ↓
DNS resolves the domain
   ↓
Browser connects to the server
   ↓
HTTP/HTTPS request
   ↓
Web server processes request
   ↓
HTTP response
   ↓
Browser displays the content

---

# 13. Virtual Hosts

One web server can host multiple websites.

Virtual hosting allows the server to determine which website should handle
a request, commonly based on information such as the requested hostname.

For example, the same server could host:

example-one.com

example-two.com

even though both websites may be running on the same physical or virtual
server.

---

# 14. Static vs Dynamic Content

## Static Content

Static content is generally delivered as stored and does not need to be
generated differently for each request.

Examples can include:

- images
- CSS files
- simple HTML files

## Dynamic Content

Dynamic content is generated or changed based on application logic, user
input, database information, sessions, or other conditions.

Examples could include:

- a user's account dashboard
- search results
- personalized content

---

# 15. Basic Web Security Concepts

This module also introduced me to some of the security risks that can occur
when web applications do not handle data correctly.

## Sensitive Data Exposure

Sensitive data can be exposed when an application does not properly protect
information.

Examples of sensitive information can include:

- passwords
- authentication tokens
- personal information
- financial information

Using HTTPS is one important way of protecting information while it travels
between a client and server, although HTTPS alone does not fix every
application security problem.

---

## HTML Injection

HTML injection can occur when a web application takes untrusted user input
and places it into a page as HTML without handling it safely.

This can allow unexpected HTML content to appear on the page.

One important lesson for me is that applications should not automatically
trust user-controlled input.

---

# 16. Why Web Fundamentals Matter in Cybersecurity

Understanding normal web communication is important before trying to
identify suspicious web activity.

As I move toward SOC and Blue Team work, HTTP information can help me
understand web-related logs and alerts.

Useful information may include:

- source and destination IP addresses
- requested domain
- URL/path
- HTTP method
- HTTP status code
- User-Agent
- request time
- amount of traffic
- authentication activity

For example, seeing one `404 Not Found` response does not automatically
mean an attack occurred.

However, a large number of requests for unusual or nonexistent paths from
the same source may be worth investigating depending on the context.

Similarly, status codes such as `401`, `403`, `404`, and `500` can provide
useful clues, but they should be investigated together with other evidence
rather than treated as proof of malicious activity by themselves.

---

# Key Takeaway

My biggest takeaway from this module is that using a website involves much
more than simply entering a URL into a browser.

I learned how DNS helps locate servers, how clients and servers communicate
using HTTP/HTTPS, how requests and responses work, and how HTTP methods,
status codes, headers, and cookies provide information about web activity.

I also gained a better understanding of how HTML, CSS, JavaScript, web
servers, and front-end/back-end technologies work together.

These are foundational concepts, but understanding normal web behaviour
gives me a stronger starting point for identifying unusual web activity as
I continue toward SOC and Blue Team-focused learning.
