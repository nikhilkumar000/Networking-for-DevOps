# Hyper Text Transfer Protocol (HTTP)



HTTP (Hypertext Transfer Protocol) is an application layer protocol used for communication between a client (like a web browser) and a server over the internet. It is the foundation of data communication for the web and is used to transfer resources such as HTML pages, images, videos, and APIs. 

HTTP follows a request-response model, where the client sends a request to the server and the server responds with the requested data. 

It works on top of Transmission Control Protocol, which ensures reliable data delivery. By default, HTTP uses port 80, while its secure version, HTTPS, uses port 443.

 HTTP is stateless, meaning each request is independent and does not remember previous interactions unless additional mechanisms like cookies or sessions are used.

## Working of HTTP 

The working of HTTP starts when a user enters a URL in the browser, such as a website address. The browser first resolves the domain name into an IP address using DNS, and then establishes a connection with the server using TCP.

After the connection is established, the browser sends an HTTP request to the server, which includes details like the request method (GET, POST, etc.), headers, and sometimes a body. The server receives this request, processes it (for example, fetching data from a database or generating a webpage), and then sends back an HTTP response. 

This response contains a status code (like 200 OK or 404 Not Found), headers, and the requested content such as HTML or JSON data. 

Once the response is received, the browser renders the content and displays it to the user. After the communication is complete, the connection may be closed or reused depending on the configuration (like keep-alive).

##  HTTP Methods (CRUD Operations)

Most web interaction revolves around these four methods, which map directly to CRUD (Create, Read, Update, Delete) operations.



| Method | CRUD Action | Description                                                                 |
|--------|------------|-----------------------------------------------------------------------------|
| GET    | Read       | Requests data from a resource. It should only retrieve data and have no other effect. |
| POST   | Create     | Sends data to the server to create a new resource (e.g., submitting a sign-up form). |
| PUT    | Update     | Replaces a current resource entirely with new data.                         |
| DELETE | Delete     | Removes the specified resource.                                             |


### Other Common Methods

While the big four do most of the heavy lifting, these methods handle more specific tasks:

#### PATCH:
 Used for partial updates. While PUT replaces the whole file, PATCH might just change one field (like updating only your email address).

#### HEAD:
 Identical to GET, but it only asks for the headers and not the actual body. It’s great for checking if a file exists or how big it is before downloading.

#### OPTIONS:
 Asks the server which methods are allowed for a specific URL. It’s often used by browsers for security checks (CORS).

## HTTP Status Codes

HTTP status codes are standard response codes returned by a server to indicate the result of a client’s request in HTTP. When a client (like a browser, API client, or load balancer) sends a request, the server processes it and responds with a status code that tells whether the request was successful, failed, redirected, or encountered an error. These codes are extremely important for DevOps engineers because they help in monitoring system health, debugging issues, configuring load balancers, and analyzing logs. Status codes are grouped into five categories (1xx to 5xx), each representing a different type of response.

## HTTP Status Codes Categories

### 1xx — Informational (Rare in DevOps)

These indicate the request is received and still being processed.

#### Example:

- 100 Continue

 Rarely used in real-world debugging.

### 2xx — Success Responses

These mean the request was successfully processed.

Common ones:

- 200 OK → Request successful

- 201 Created → Resource created (API)

- 204 No Content → Success but no response body

####  DevOps Use Case:

- Health checks (e.g., /health endpoint returning 200)

- Monitoring systems expect 200 OK

### 3xx — Redirection

These indicate the client must take additional action.

#### Common ones:

- 301 Moved Permanently → URL permanently changed

- 302 Found → Temporary redirect

- 304 Not Modified → Cached version is valid

####  DevOps Use Case:

- Redirect HTTP → HTTPS

- CDN caching (304 reduces load)

### 4xx — Client Errors

These occur when the client makes a bad request.

#### Common ones:

- 400 Bad Request → Invalid request

- 401 Unauthorized → Authentication required

- 403 Forbidden → Access denied

- 404 Not Found → Resource not found

####  DevOps Use Case:

- API errors due to wrong input
- Unauthorized access attempts
- Broken frontend routes → 404 spikes in logs

### 5xx — Server Errors (VERY IMPORTANT)

These indicate server-side issues.



#### Common ones:

- 500 Internal Server Error → Generic server failure
- 502 Bad Gateway → Upstream server failed
- 503 Service Unavailable → Server overloaded/down
- 504 Gateway Timeout → Upstream timeout


####  DevOps Use Case:

- Alerts triggered on 5xx spikes
- Debugging backend, load balancer, or microservices
- Indicates production issues

## Real DevOps Scenario (Very Important)

Imagine architecture:

User → Load Balancer → Nginx → Backend → Database

### Case 1: Backend Crash
- Nginx cannot reach backend
- Response → 502 Bad Gateway

### Case 2: High Traffic
- Server overloaded
- Response → 503 Service Unavailable

### Case 3: Slow Backend
- Timeout occurs
- Response → 504 Gateway Timeout

### Case 4: Wrong API Route
- API endpoint does not exist
- Response → 404 Not Found


## Commands to Check Status Codes (DevOps)

### Using curl
curl -I https://example.com

### Output:

HTTP/1.1 200 OK


### Check only status code

 curl -o /dev/null -s -w "%{http_code}\n" https://example.com

### Check logs (Nginx)
tail -f /var/log/nginx/access.log

Example log:

"GET /api HTTP/1.1" 500

### Monitoring & Alerts (DevOps Insight)

DevOps engineers track:

- % of 2xx → success rate
- % of 4xx → client issues
- % of 5xx → critical alerts 

#### Example:

- 5xx > 2% → trigger alert
- 200 drops → service down

#### Tools used:

- Prometheus
- Grafana
- ELK Stack

---

# WebSockets vs HTTP


**HTTP** is a request-response protocol where the client sends a request and the server responds, after which the connection is usually closed. It is stateless and works well for typical web interactions like loading pages or APIs.

**WebSockets,** on the other hand, provide a persistent, full-duplex communication channel between client and server over a single connection. Once established, both client and server can send data anytime without repeated requests, making it ideal for real-time applications.

##  HTTP vs WebSockets (Key Differences)

| Feature        | HTTP                         | WebSockets                     |
|----------------|------------------------------|--------------------------------|
| Connection     | Short-lived                  | Persistent                     |
| Communication  | Request → Response           | Two-way (bi-directional)       |
| State          | Stateless                    | Stateful                       |
| Speed          | Slower for real-time         | Faster for real-time           |
| Overhead       | High (headers each request)  | Low (after connection established) |
| Use Case       | Web pages, REST APIs         | Real-time apps                 |

### Working Difference (Simple)

**HTTP**

- Client → Request → Server  
- Server → Response → Client  (Connection closes)

 Every interaction needs a new request

**WebSockets**

- Client → Handshake → Server  (Connection stays open)  
- Client ↔ Server (continuous data exchange)

 No need to reconnect again and again


## Use Cases

**HTTP**

- Website loading
- REST APIs
- File downloads
- Authentication systems

**WebSockets**

- Chat applications
- Live notifications
- Stock trading apps
- Online gaming
- Real-time dashboards

**DevOps Perspective**
- HTTP is easy to scale using load balancers and caching
- WebSockets require sticky sessions or special handling in load balancers
- WebSockets consume more persistent connections → need careful scaling