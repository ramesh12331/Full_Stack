# 🌐 Chapter 15 — HTTP Fundamentals in Node.js



Chapter 15

Beginner to Advanced



In this chapter, you will learn how websites and backend applications communicate with each other using HTTP (Hypertext Transfer Protocol).

HTTP is one of the most important concepts for becoming a professional Node.js backend developer.

You will learn:

- What is HTTP?
- Client and server communication
- HTTP request and response
- HTTP methods: GET, POST, PUT, PATCH, DELETE
- URL structure
- Request headers and body
- HTTP status codes
- HTTP vs HTTPS
- Stateless communication
- How APIs work

## 📖 Interactive learning icons

# 📖

Read

Learning guidance

# 💡

Important

Remember this

## 🔑 Requires Before Starting

Before starting this chapter, you should understand:

| Previous concept     | Why is it needed?                     |
| -------------------- | ------------------------------------- |
| JavaScript functions | To understand server-side code        |
| Node.js basics       | To understand the backend runtime     |
| Modules              | To organize Node.js code              |
| Callbacks            | To understand asynchronous operations |
| Promises             | To understand asynchronous requests   |
| Async/Await          | To handle asynchronous operations     |
| JSON                 | To understand API data                |

### Quick revision: JSON

JSON is a common format used to exchange data between frontend and backend applications.

Example:

```
{
    "id": 101,
    "name": "Ramesh",
    "role": "Full Stack Developer"
}
```

# 1. What is HTTP?

HTTP stands for Hypertext Transfer Protocol.

HTTP is a communication protocol that allows a client and a server to exchange information over a network.

In simple words:

- The client sends a request.
- The server receives the request.
- The server processes it.
- The server sends a response.
- The client receives the response.

### Real-world example

Imagine you open an online shopping website.

1. You open the website.
2. Your browser requests product information.
3. The backend receives the request.
4. The backend gets products from the database.
5. The backend sends product information.
6. Your browser displays the products.

This communication commonly happens using HTTP or HTTPS.

### Basic communication

Client

Browser / React

Server

Node.js

Client sends HTTP request → Server sends HTTP response

💡 Important: HTTP is a protocol, not a programming language. Node.js can use HTTP to build backend servers.

# 2. Why do we need HTTP?

Imagine you build a React frontend and a Node.js backend.

Your React application needs to communicate with your Node.js backend.

For example:

- Display all students.
- Register a new student.
- Update student information.
- Delete a student.
- Login a user.

How does React communicate with Node.js?

It sends HTTP requests.

### Without HTTP

Your frontend would have no standard web communication mechanism to request information from your backend.

### With HTTP

React can send requests to backend endpoints.

Example:

```
fetch("http://localhost:3000/students");
```

This sends a request to the Node.js server.

The server can return:

```
[
    {
        "id": 1,
        "name": "Ramesh"
    },
    {
        "id": 2,
        "name": "Kumar"
    }
]
```

# 3. Real-world analogy

Think about a restaurant.

| Restaurant                | HTTP communication       |
| ------------------------- | ------------------------ |
| Customer                  | Client                   |
| Waiter receives the order | HTTP request             |
| Order details             | Request data             |
| Kitchen                   | Backend server           |
| Food preparation          | Server processing        |
| Food delivered            | HTTP response            |
| Customer receives food    | Client receives response |

The customer does not directly enter the kitchen. The waiter carries the order and brings back the result.

Similarly, the client communicates with the server through HTTP requests and responses.

# 4. Architecture / flow

### HTTP request-response architecture

\#chatgpt-mermaid-\_r_3ih\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_3ih\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_3ih\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_3ih\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_3ih\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3ih\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_3ih\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_3ih\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_3ih\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_3ih\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_3ih\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_3ih\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3ih\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3ih\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_3ih\_ p{margin:0;}#chatgpt-mermaid-\_r_3ih\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3ih\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3ih\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3ih\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_3ih\_ .label text,#chatgpt-mermaid-\_r_3ih\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3ih\_ .node rect,#chatgpt-mermaid-\_r_3ih\_ .node circle,#chatgpt-mermaid-\_r_3ih\_ .node ellipse,#chatgpt-mermaid-\_r_3ih\_ .node polygon,#chatgpt-mermaid-\_r_3ih\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_3ih\_ .rough-node .label text,#chatgpt-mermaid-\_r_3ih\_ .node .label text,#chatgpt-mermaid-\_r_3ih\_ .image-shape .label,#chatgpt-mermaid-\_r_3ih\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_3ih\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_3ih\_ .rough-node .label,#chatgpt-mermaid-\_r_3ih\_ .node .label,#chatgpt-mermaid-\_r_3ih\_ .image-shape .label,#chatgpt-mermaid-\_r_3ih\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_3ih\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_3ih\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3ih\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3ih\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_3ih\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_3ih\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_3ih\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_3ih\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_3ih\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_3ih\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_3ih\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3ih\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3ih\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_3ih\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3ih\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_3ih\_ .icon-shape,#chatgpt-mermaid-\_r_3ih\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_3ih\_ .icon-shape p,#chatgpt-mermaid-\_r_3ih\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_3ih\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_3ih\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_3ih\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_3ih\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_3ih\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_3ih\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_3ih\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_3ih\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_3ih\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3ih\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_3ih\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_3ih\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_3ih\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3ih\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_3ih\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_3ih\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3ih\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_3ih\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_3ih\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3ih\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_3ih\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3ih\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_3ih\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_3ih\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_3ih\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_3ih\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_3ih\_ .node rect,#chatgpt-mermaid-\_r_3ih\_ .node circle,#chatgpt-mermaid-\_r_3ih\_ .node ellipse,#chatgpt-mermaid-\_r_3ih\_ .node polygon,#chatgpt-mermaid-\_r_3ih\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_3ih\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_3ih\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_3ih\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_3ih\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3ih\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}UserReact Frontend / BrowserNode.js BackendBusiness LogicDatabaseDisplay DataHTTP RequestHTTP ResponseJSON Response

### Example: Fetch students

Suppose the frontend sends:

```
GET /students HTTP/1.1
Host: localhost:3000
```

The Node.js server processes the request and responds:

```
HTTP/1.1 200 OK
Content-Type: application/json

[
    {
        "id": 1,
        "name": "Ramesh"
    }
]
```

### GitHub README diagram

GitHub supports Mermaid diagrams directly.

DatabaseNode.js ServerReact ClientUserDatabaseNode.js ServerReact ClientUser#chatgpt-mermaid-\_r_3j0\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_3j0\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_3j0\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_3j0\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_3j0\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3j0\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_3j0\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_3j0\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_3j0\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_3j0\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_3j0\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_3j0\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3j0\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3j0\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_3j0\_ p{margin:0;}#chatgpt-mermaid-\_r_3j0\_ .actor{stroke:rgb(83, 154, 248);fill:rgb(222, 234, 251);stroke-width:1;}#chatgpt-mermaid-\_r_3j0\_ rect.actor.outer-path[data-look="neo"]{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3j0\_ rect.note[data-look="neo"]{stroke:rgb(107, 198, 127);fill:rgb(243, 243, 243);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3j0\_ text.actor>tspan{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_3j0\_ .actor-line{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3j0\_ .innerArc{stroke-width:1.5;stroke-dasharray:none;}#chatgpt-mermaid-\_r_3j0\_ .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3j0\_ .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3j0\_ [id$="-arrowhead"] path{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3j0\_ .sequenceNumber{fill:#707070;}#chatgpt-mermaid-\_r_3j0\_ [id$="-sequencenumber"]{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3j0\_ [id$="-crosshead"] path{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3j0\_ .messageText{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_3j0\_ .labelBox{stroke:rgba(0, 0, 0, 0.1);fill:rgb(252, 252, 252);filter:none;}#chatgpt-mermaid-\_r_3j0\_ .labelText,#chatgpt-mermaid-\_r_3j0\_ .labelText>tspan{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_3j0\_ .loopText,#chatgpt-mermaid-\_r_3j0\_ .loopText>tspan{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_3j0\_ .sectionTitle,#chatgpt-mermaid-\_r_3j0\_ .sectionTitle>tspan{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_3j0\_ .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:rgba(0, 0, 0, 0.1);fill:rgba(0, 0, 0, 0.1);}#chatgpt-mermaid-\_r_3j0\_ .note{stroke:rgb(107, 198, 127);fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_3j0\_ .noteText,#chatgpt-mermaid-\_r_3j0\_ .noteText>tspan{fill:rgb(13, 13, 13);stroke:none;font-weight:normal;}#chatgpt-mermaid-\_r_3j0\_ .activation0{fill:rgb(243, 243, 243);stroke:hsl(0, 0%, 85.2941176471%);}#chatgpt-mermaid-\_r_3j0\_ .activation1{fill:rgb(243, 243, 243);stroke:hsl(0, 0%, 85.2941176471%);}#chatgpt-mermaid-\_r_3j0\_ .activation2{fill:rgb(243, 243, 243);stroke:hsl(0, 0%, 85.2941176471%);}#chatgpt-mermaid-\_r_3j0\_ .actorPopupMenu{position:absolute;}#chatgpt-mermaid-\_r_3j0\_ .actorPopupMenuPanel{position:absolute;fill:rgb(222, 234, 251);box-shadow:0px 8px 16px 0px rgba(0,0,0,0.2);filter:drop-shadow(3px 5px 2px rgb(0 0 0 / 0.4));}#chatgpt-mermaid-\_r_3j0\_ .actor-man circle,#chatgpt-mermaid-\_r_3j0\_ line{fill:rgb(222, 234, 251);stroke-width:2px;}#chatgpt-mermaid-\_r_3j0\_ g rect.rect{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_3j0\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_3j0\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_3j0\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_3j0\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_3j0\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3j0\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_3j0\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_3j0\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_3j0\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3j0\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_3j0\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_3j0\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3j0\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_3j0\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_3j0\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3j0\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_3j0\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3j0\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Open students pageGET /studentsFetch studentsStudent recordsHTTP 200 + JSONDisplay students

Suggested folder structure:

```
15_HTTP_Fundamentals/
│
├── README.md
│
├── 01_http_intro.md
├── 02_client_server.md
├── 03_http_request.md
├── 04_http_response.md
├── 05_http_methods.md
├── 06_status_codes.md
├── 07_headers.md
├── 08_request_body.md
├── 09_url_structure.md
├── 10_http_vs_https.md
│
└── images/
    ├── http-architecture.png
    ├── request-response.png
    └── http-methods.png
```

To show an image in GitHub, add the actual image file to the repository and reference it:

```
![HTTP Architecture](./images/http-architecture.png)
```

The image will not appear if the file does not exist in that folder. Mermaid diagrams do not require separate image files.

# 5. HTTP syntax

An HTTP communication has two important parts:

1. HTTP Request
2. HTTP Response

## A. HTTP Request

An HTTP request is a message sent by a client to a server.

Basic structure:

```
GET /students HTTP/1.1
Host: localhost:3000
Accept: application/json
```

It contains:

| Part         | Meaning                          |
| ------------ | -------------------------------- |
| Method       | What operation to perform        |
| Path         | Which resource to access         |
| HTTP version | Protocol version                 |
| Headers      | Additional request information   |
| Body         | Optional data sent to the server |

## B. HTTP Response

An HTTP response is a message sent by the server to the client.

Example:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
    "message": "Students fetched successfully"
}
```

It contains:

| Part           | Meaning                         |
| -------------- | ------------------------------- |
| HTTP version   | Protocol version                |
| Status code    | Result of the request           |
| Status message | Human-readable description      |
| Headers        | Additional response information |
| Body           | Returned data                   |

# 6. Basic example

Let's understand HTTP methods.

An HTTP method tells the server what action the client wants to perform.

Suppose we have a Student API.

### Main HTTP methods

GET

Read or retrieve student information

GET /students

POST

Create a new student

POST /students

PUT

Replace an existing student resource

PUT /students/1

PATCH

Partially update student information

PATCH /students/1

DELETE

Delete a student

DELETE /students/1

### Example 1 — GET

Retrieve all students:

```
GET /students
```

### Example 2 — POST

Create a student:

```
POST /students
Content-Type: application/json

{
    "name": "Ramesh",
    "course": "Node.js"
}
```

### Example 3 — PUT

Replace a student's information:

```
PUT /students/1
Content-Type: application/json

{
    "name": "Ramesh Kumar",
    "course": "React.js"
}
```

### Example 4 — PATCH

Update only a student's course:

```
PATCH /students/1
Content-Type: application/json

{
    "course": "Node.js"
}
```

### Example 5 — DELETE

Delete a student:

```
DELETE /students/1
```

### Practice: Identify the HTTP method

Choose the correct method

1\. You want to display all products.

GET

POST

PUT

PATCH

DELETE



2\. You want to register a new user.

GET

POST

PUT

PATCH

DELETE



3\. You want to change only a user's email.

GET

POST

PUT

PATCH

DELETE



4\. You want to remove a product.

GET

POST

PUT

PATCH

DELETE



5\. You want to replace all editable details of a student.

GET

POST

PUT

PATCH

DELETE



Check answers

# 7. Dry run

Let's understand a GET request.

Request:

```
GET /students
```

Assume the database contains:

```
[
    {
        "id": 1,
        "name": "Ramesh"
    },
    {
        "id": 2,
        "name": "Kumar"
    }
]
```

Execution:

| Step | Action                           |
| ---- | -------------------------------- |
| 1    | User opens the student page      |
| 2    | React sends `GET /students`      |
| 3    | Node.js receives the request     |
| 4    | Backend requests student records |
| 5    | Database returns student records |
| 6    | Backend sends HTTP response      |
| 7    | React displays the students      |

The important point is that the client requests information and the server provides the response.

# 8. Output

For a successful GET request, the server might return:

HTTP Response

200 OK

```
{
  "success": true,
  "message": "Students fetched successfully",
  "data": [
    {
      "id": 1,
      "name": "Ramesh"
    },
    {
      "id": 2,
      "name": "Kumar"
    }
  ]
}
```

This is an example response format. Your actual backend decides what data to return.

# 9. Line-by-line explanation

Now let's understand the important HTTP concepts.

## A. HTTP status codes

A status code tells the client what happened when the server processed its request.

### 1xx — Informational

The request has been received and processing is continuing.

### 2xx — Success

The request was successfully received and processed.

| Code | Meaning    | Example                                   |
| ---- | ---------- | ----------------------------------------- |
| 200  | OK         | Data fetched                              |
| 201  | Created    | User registered                           |
| 202  | Accepted   | Request accepted for processing           |
| 204  | No Content | Successful deletion with no response body |

### 3xx — Redirection

The client needs to follow a different location or use a cached resource.

| Code | Meaning                       |
| ---- | ----------------------------- |
| 301  | Moved Permanently             |
| 302  | Found (temporary redirection) |
| 304  | Not Modified                  |

### 4xx — Client errors

The request has a problem.

| Code | Meaning               | Example                           |
| ---- | --------------------- | --------------------------------- |
| 400  | Bad Request           | Invalid input                     |
| 401  | Unauthorized          | Authentication required or failed |
| 403  | Forbidden             | User does not have permission     |
| 404  | Not Found             | Student not found                 |
| 405  | Method Not Allowed    | Unsupported HTTP method           |
| 409  | Conflict              | Duplicate email                   |
| 422  | Unprocessable Content | Validation error                  |

### 5xx — Server errors

The server failed to complete a valid request.

| Code | Meaning               |
| ---- | --------------------- |
| 500  | Internal Server Error |
| 501  | Not Implemented       |
| 502  | Bad Gateway           |
| 503  | Service Unavailable   |
| 504  | Gateway Timeout       |

Remember

- 2xx = Success
- 3xx = Redirection
- 4xx = Client-side error
- 5xx = Server-side error

## B. HTTP Headers

Headers provide additional information about a request or response.

Example:

```
GET /students HTTP/1.1
Host: localhost:3000
Accept: application/json
Authorization: Bearer your_token
```

Common request headers:

| Header          | Purpose                                  |
| --------------- | ---------------------------------------- |
| `Content-Type`  | Describes the format of the request body |
| `Accept`        | Describes acceptable response formats    |
| `Authorization` | Carries authentication credentials       |
| `User-Agent`    | Identifies the client software           |
| `Host`          | Identifies the target host               |

Example response headers:

```
HTTP/1.1 200 OK
Content-Type: application/json
Cache-Control: no-cache
```

## C. Request Body

The request body contains data sent by the client.

Example:

```
{
    "name": "Ramesh",
    "email": "ramesh@example.com",
    "course": "Node.js"
}
```

The body is commonly used with POST, PUT and PATCH requests.

## D. URL Structure

Consider this URL:

```
https://example.com:443/students/101?course=nodejs&page=1
```

| Part         | Value                   | Meaning                |
| ------------ | ----------------------- | ---------------------- |
| Protocol     | `https`                 | Communication protocol |
| Domain       | `example.com`           | Server hostname        |
| Port         | `443`                   | Server port            |
| Path         | `/students/101`         | Resource location      |
| Query string | `?course=nodejs&page=1` | Additional parameters  |

### Path parameter

```
/students/101
```

Here, `101` identifies a student.

### Query parameters

```
/students?course=nodejs&page=1
```

Here:

- `course=nodejs`
- `page=1`

Query parameters are commonly used for filtering, searching and pagination.

## E. HTTP vs HTTPS

| HTTP                                                          | HTTPS                                    |
| ------------------------------------------------------------- | ---------------------------------------- |
| Hypertext Transfer Protocol                                   | HTTP Secure                              |
| Data is not encrypted by HTTP itself                          | Data is protected using TLS encryption   |
| Common default port: 80                                       | Common default port: 443                 |
| Not suitable for sensitive data without additional protection | Recommended for modern websites and APIs |

💡 Important: HTTPS protects data while it travels between client and server. It does not automatically make an application secure; authentication, authorization and secure coding are still necessary.

## F. Stateless protocol

HTTP is called a stateless protocol.

It means that each request is independent by default. The server does not automatically remember previous requests.

Example:

1. User sends a login request.
2. Server verifies the credentials.
3. User sends another request to access their profile.

The server needs a way to identify the authenticated user, such as a session cookie or an authentication token.

This is why authentication mechanisms are important in backend applications.

# 10. Practical example

Let's test HTTP requests using Postman.

We will use a free public testing API:

`https://jsonplaceholder.typicode.com`

[image](https://www.google.com/s2/favicons?domain=https://jsonplaceholder.typicode.com\&sz=32)

JSONPlaceholder

A public fake REST API for learning and testing.

## A. GET request

1. Open Postman.
2. Select GET.
3. Enter:

```
https://jsonplaceholder.typicode.com/users
```

4\. Click Send.

You will receive a list of sample users.

## B. GET a single user

```
https://jsonplaceholder.typicode.com/users/1
```

Expected response includes user information such as:

```
{
    "id": 1,
    "name": "Leanne Graham",
    "username": "Bret"
}
```

## C. POST request

Select POST and enter:

```
https://jsonplaceholder.typicode.com/posts
```

Select Body → raw → JSON.

Send:

```
{
    "title": "Learning Node.js",
    "body": "Learning HTTP fundamentals",
    "userId": 1
}
```

The testing API will return a sample created resource, typically with an ID.

## D. PUT request

```
https://jsonplaceholder.typicode.com/posts/1
```

Body:

```
{
    "id": 1,
    "title": "Updated title",
    "body": "Updated post content",
    "userId": 1
}
```

## E. PATCH request

```
https://jsonplaceholder.typicode.com/posts/1
```

Body:

```
{
    "title": "Only title updated"
}
```

## F. DELETE request

```
https://jsonplaceholder.typicode.com/posts/1
```

Select DELETE and click Send.

Note: JSONPlaceholder simulates API operations. These requests do not permanently change a real database.

### Test HTTP using JavaScript fetch()

You can also send HTTP requests from Node.js.

File: `01_http_get.js`

```
// Async function to fetch users
async function getUsers() {

    try {

        // Send HTTP GET request
        const response = await fetch(
            "https://jsonplaceholder.typicode.com/users"
        );

        // Check HTTP status
        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }

        // Convert response into JavaScript data
        const users = await response.json();

        // Display users
        console.log(users);

    } catch (error) {

        // Handle network or processing errors
        console.log("Error:", error.message);

    }

}

// Execute function
getUsers();
```

Run:

```
node 01_http_get.js
```

Expected result: An array of sample users appears in the terminal.

Understand these lines:

- `fetch()` sends an HTTP request.
- `await` waits for the response.
- `response.ok` checks whether the HTTP status is in the 200–299 range.
- `response.json()` reads and parses the JSON response body.
- `catch` handles errors.

# 11. Common mistakes

### Mistake 1 — Using GET to create data

Wrong approach

```
GET /students
```

Trying to use GET to create a new student is not appropriate.

Correct approach

```
POST /students
```

### Mistake 2 — Confusing 401 and 403

| Status | Meaning                                                 |
| ------ | ------------------------------------------------------- |
| 401    | Authentication is missing or invalid                    |
| 403    | Server understood the request, but permission is denied |

### Mistake 3 — Forgetting to check the response status

Incorrect:

```
const response = await fetch(url);
const data = await response.json();

console.log(data);
```

Better:

```
const response = await fetch(url);

if (!response.ok) {
    throw new Error(`Request failed: ${response.status}`);
}

const data = await response.json();

console.log(data);
```

### Mistake 4 — Confusing path and query parameters

Path:

```
/students/101
```

Query:

```
/students?page=1
```

The first identifies a resource. The second provides additional filtering or pagination information.

### Mistake 5 — Sending JSON without Content-Type

When sending a JSON body, specify the content type.

```
const response = await fetch(
    "https://jsonplaceholder.typicode.com/posts",
    {
        method: "POST",

        headers: {
            "Content-Type": "application/json"
        },

        body: JSON.stringify({
            title: "Node.js",
            body: "Learning HTTP",
            userId: 1
        })
    }
);
```

# 12. Best practices

1. Use the correct HTTP method for each operation.
2. Return meaningful HTTP status codes.
3. Validate incoming request data.
4. Use HTTPS in production.
5. Do not expose passwords or secret tokens in responses.
6. Use appropriate request and response headers.
7. Handle network errors and HTTP errors.
8. Use JSON consistently when building JSON APIs.
9. Keep URLs meaningful and resource-oriented.
10. Use authentication and authorization where required.
11. Use pagination for large data collections.
12. Do not put sensitive information in query parameters.

# 13. Interview questions

## Beginner level

Q1. What is HTTP?

HTTP is a communication protocol used by clients and servers to exchange information over a network.

Q2. What is a client?

A client is an application that sends requests to a server, such as a browser or React application.

Q3. What is a server?

A server receives requests, processes them and sends responses.

Q4. What is an HTTP request?

A message sent from the client to the server.

Q5. What is an HTTP response?

A message returned by the server to the client.

## Intermediate level

Q6. What is the difference between GET and POST?

GET retrieves information. POST commonly creates a resource or submits data for processing.

Q7. What is the difference between PUT and PATCH?

PUT generally replaces the resource representation. PATCH applies a partial update.

Q8. What is an HTTP status code?

A numeric code that describes the result of an HTTP request.

Q9. What are HTTP headers?

Headers provide additional information about a request or response.

Q10. What is a request body?

It is the data sent by a client as part of an HTTP request.

## Advanced level

Q11. What is a stateless protocol?

A protocol where each request is independent by default. HTTP does not automatically remember previous requests.

Q12. What is the difference between HTTP and HTTPS?

HTTPS uses TLS to encrypt communication between the client and server.

Q13. What is the difference between 401 and 403?

401 means valid authentication is missing or has failed. 403 means access is forbidden.

Q14. What is the difference between path parameters and query parameters?

Path parameters identify a resource. Query parameters provide additional information such as filters, search terms or pagination.

Q15. What is REST API?

REST is an architectural style for designing network APIs. REST APIs commonly use HTTP methods and resource-oriented URLs.

# 14. Practice problems

Try these exercises using Postman and Node.js.

Practice checklist

0/7

Exercise 1: Send a GET request to retrieve all users from JSONPlaceholder.

💡 Show hint

Exercise 2: Retrieve the user with ID 1.

💡 Show hint

Exercise 3: Send a POST request to create a sample post.

💡 Show hint

Exercise 4: Update the title of post 1 using PATCH.

💡 Show hint

Exercise 5: Send a DELETE request for post 1.

💡 Show hint

Exercise 6: Write a Node.js fetch() program to retrieve users and handle errors.

💡 Show hint

Exercise 7: Identify the correct status code for a resource that does not exist.

💡 Show hint

# 15. Mini challenge — Student REST API planning

Real-world challenge

Imagine you are developing a Student Management System.

Your task is to design the HTTP API endpoints. You do not need to build the server yet.

### Requirements

Plan these five operations:

| Operation        | HTTP method | Endpoint |
| ---------------- | ----------- | -------- |
| Get all students | ?           | ?        |
| Get one student  | ?           | ?        |
| Create a student | ?           | ?        |
| Update a student | ?           | ?        |
| Delete a student | ?           | ?        |

### Your challenge

Fill in the missing methods and endpoints.

Design your API

1\. Get all students

GET /students

POST /students

DELETE /students



2\. Get student with ID 10

GET /students/10

PATCH /students

POST /students/10



3\. Create a student

PUT /students/10

POST /students

GET /students



4\. Partially update student 10

PATCH /students/10

GET /students/10

DELETE /students/10



5\. Delete student 10

POST /students/10

DELETE /students/10

GET /students



Check my API design

# 16. Chapter summary

| Concept      | What you learned                          |
| ------------ | ----------------------------------------- |
| HTTP         | Communication protocol                    |
| Client       | Sends requests                            |
| Server       | Processes requests                        |
| Request      | Message sent to server                    |
| Response     | Message returned by server                |
| GET          | Retrieve data                             |
| POST         | Create or submit data                     |
| PUT          | Replace a resource                        |
| PATCH        | Partially update a resource               |
| DELETE       | Delete a resource                         |
| Headers      | Additional request/response information   |
| Body         | Data sent with a request                  |
| Status codes | Indicate request outcome                  |
| HTTPS        | HTTP communication protected by TLS       |
| Stateless    | Requests are independent by default       |
| REST API     | Resource-oriented API architectural style |

# 17. Quick revision

Remember these important points:

1. HTTP allows clients and servers to communicate.
2. A client sends a request.
3. A server returns a response.
4. GET retrieves data.
5. POST creates or submits data.
6. PUT replaces data.
7. PATCH partially updates data.
8. DELETE removes a resource.
9. Status codes describe the request result.
10. HTTPS protects communication using TLS.

Most important HTTP status codes

| Code | Meaning               |
| ---- | --------------------- |
| 200  | OK                    |
| 201  | Created               |
| 204  | No Content            |
| 400  | Bad Request           |
| 401  | Unauthorized          |
| 403  | Forbidden             |
| 404  | Not Found             |
| 500  | Internal Server Error |

## 📁 GitHub README checklist

- Create `15_HTTP_Fundamentals` folder.
- Create `README.md`.
- Add HTTP request and response examples.
- Add Mermaid architecture diagrams.
- Add Postman screenshots to `images/` if needed.
- Verify all image paths.
- Run the Node.js fetch example.
- Complete the practice problems.

Suggested GitHub image references:

```
![HTTP Architecture](./images/http-architecture.png)

![HTTP Request Response](./images/request-response.png)

![HTTP Methods](./images/http-methods.png)
```

Remember: These image files must actually be added to your GitHub `images/` folder. Mermaid diagrams are already included in this chapter and can render directly in GitHub.

Chapter 15 completed

You have now learned how a frontend application communicates with a backend using HTTP.

Practice the Postman requests before moving forward.

When you are ready, type `NEXT` to start:

Chapter 16 — Creating an HTTP Server in Node.js 🚀