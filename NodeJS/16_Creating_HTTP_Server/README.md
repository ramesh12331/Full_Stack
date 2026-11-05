# 🚀 Chapter 16 — Creating an HTTP Server in Node.js



Chapter 16

Beginner to Advanced



In this chapter, you will learn how to create your own backend server using the built-in HTTP module in Node.js.

You will build a server that can:

- Start and listen on a port.
- Receive HTTP requests.
- Send HTTP responses.
- Handle different HTTP methods.
- Create simple API endpoints.
- Return JSON data.
- Handle 404 errors.
- Read URL paths and query parameters.
- Handle POST request data.

This is an important foundation before learning Express.js.

## 📖 Interactive learning icons

# 📖

Read

Learning guidance

# 💡

Important

Remember this

## 🔑 Requires Before Starting

Before starting this chapter, understand these previous topics:

| Topic       | What you should know                  |
| ----------- | ------------------------------------- |
| Node.js     | What Node.js is                       |
| Modules     | How to import built-in modules        |
| Functions   | How to create and call functions      |
| Callbacks   | How callback functions work           |
| Promises    | How asynchronous operations work      |
| Async/Await | How to handle asynchronous operations |
| HTTP        | Client, server, request and response  |
| JSON        | How to represent data                 |

### Quick revision

In the previous chapter, you learned that:

1. A client sends an HTTP request.
2. A server receives the request.
3. The server processes it.
4. The server returns an HTTP response.

Now let's create that server ourselves!

# 1. What is an HTTP Server?

An HTTP server is a program that receives HTTP requests from clients and sends HTTP responses.

Node.js provides a built-in module called `http` to create HTTP servers.

### Simple example

Imagine you open this URL in your browser:

```
http://localhost:3000
```

Your browser sends a request to your Node.js server.

The server receives the request and sends back:

```
Hello from Node.js Server!
```

### Important terms

| Term        | Meaning                                        |
| ----------- | ---------------------------------------------- |
| HTTP module | Node.js built-in module for HTTP communication |
| Server      | Program that receives and processes requests   |
| Request     | Message sent by the client                     |
| Response    | Message sent by the server                     |
| Port        | Communication endpoint used by the server      |
| `localhost` | Address referring to your own computer         |
| `listen()`  | Starts listening for incoming connections      |

💡 Important: Node.js does not require Express.js to create an HTTP server. You can create one directly using the built-in `http` module.

# 2. Why do we need an HTTP Server?

Suppose you create a React application for a Student Management System.

Your React frontend needs to communicate with the backend.

For example:

- Fetch all students.
- Register a student.
- Update student details.
- Delete a student.
- Login a user.

Where will these requests go?

They go to your backend server.

### Without a server

Your React application has no backend endpoint to receive and process its HTTP requests.

### With a Node.js HTTP server

Your backend can receive requests and send responses.

Example:

```
React Frontend
      |
      | GET /students
      |
      v
Node.js HTTP Server
      |
      | Process request
      |
      v
Database
      |
      | Student data
      |
      v
Node.js HTTP Server
      |
      | JSON response
      |
      v
React Frontend
```

# 3. Real-world analogy

Think about a hotel reception.

| Hotel           | Node.js HTTP Server |
| --------------- | ------------------- |
| Guest           | Client              |
| Reception desk  | HTTP server         |
| Guest's request | HTTP request        |
| Receptionist    | Request handler     |
| Hotel service   | Backend logic       |
| Service result  | HTTP response       |

When a guest asks for a room, the receptionist receives the request, processes it and provides a response.

Similarly, an HTTP server receives requests, processes them and sends responses.

# 4. Architecture / flow

### Node.js HTTP server architecture

\#chatgpt-mermaid-\_r_3v1\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_3v1\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_3v1\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_3v1\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_3v1\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3v1\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_3v1\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_3v1\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_3v1\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_3v1\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_3v1\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_3v1\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3v1\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3v1\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_3v1\_ p{margin:0;}#chatgpt-mermaid-\_r_3v1\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3v1\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3v1\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3v1\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_3v1\_ .label text,#chatgpt-mermaid-\_r_3v1\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3v1\_ .node rect,#chatgpt-mermaid-\_r_3v1\_ .node circle,#chatgpt-mermaid-\_r_3v1\_ .node ellipse,#chatgpt-mermaid-\_r_3v1\_ .node polygon,#chatgpt-mermaid-\_r_3v1\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_3v1\_ .rough-node .label text,#chatgpt-mermaid-\_r_3v1\_ .node .label text,#chatgpt-mermaid-\_r_3v1\_ .image-shape .label,#chatgpt-mermaid-\_r_3v1\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_3v1\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_3v1\_ .rough-node .label,#chatgpt-mermaid-\_r_3v1\_ .node .label,#chatgpt-mermaid-\_r_3v1\_ .image-shape .label,#chatgpt-mermaid-\_r_3v1\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_3v1\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_3v1\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3v1\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3v1\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_3v1\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_3v1\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_3v1\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_3v1\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_3v1\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_3v1\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_3v1\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3v1\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3v1\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_3v1\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3v1\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_3v1\_ .icon-shape,#chatgpt-mermaid-\_r_3v1\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_3v1\_ .icon-shape p,#chatgpt-mermaid-\_r_3v1\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_3v1\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_3v1\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_3v1\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_3v1\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_3v1\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_3v1\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_3v1\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_3v1\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_3v1\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3v1\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_3v1\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_3v1\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_3v1\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3v1\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_3v1\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_3v1\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3v1\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_3v1\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_3v1\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3v1\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_3v1\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3v1\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_3v1\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_3v1\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_3v1\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_3v1\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_3v1\_ .node rect,#chatgpt-mermaid-\_r_3v1\_ .node circle,#chatgpt-mermaid-\_r_3v1\_ .node ellipse,#chatgpt-mermaid-\_r_3v1\_ .node polygon,#chatgpt-mermaid-\_r_3v1\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_3v1\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_3v1\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_3v1\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_3v1\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3v1\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}User / BrowserNode.js HTTP ServerRequest HandlerCheck URL and MethodHome ResponseStudent DataCreate Student404 Not FoundHTTP ResponseBrowser / ClientHTTP RequestGET /GET /studentsPOST /studentsOther Route

### Request-response flow

1. The server is created using `http.createServer()`.
2. The server receives a request.
3. The callback function executes.
4. The request URL and method are checked.
5. The server prepares the response.
6. The server sends the response using `res.end()`.
7. The client receives the response.

### GitHub README architecture

GitHub supports Mermaid diagrams directly.

Node.js ServerClientNode.js ServerClient#chatgpt-mermaid-\_r_3v8\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_3v8\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_3v8\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_3v8\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_3v8\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3v8\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_3v8\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_3v8\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_3v8\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_3v8\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_3v8\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_3v8\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3v8\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3v8\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_3v8\_ p{margin:0;}#chatgpt-mermaid-\_r_3v8\_ .actor{stroke:rgb(83, 154, 248);fill:rgb(222, 234, 251);stroke-width:1;}#chatgpt-mermaid-\_r_3v8\_ rect.actor.outer-path[data-look="neo"]{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3v8\_ rect.note[data-look="neo"]{stroke:rgb(107, 198, 127);fill:rgb(243, 243, 243);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3v8\_ text.actor>tspan{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_3v8\_ .actor-line{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3v8\_ .innerArc{stroke-width:1.5;stroke-dasharray:none;}#chatgpt-mermaid-\_r_3v8\_ .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3v8\_ .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3v8\_ [id$="-arrowhead"] path{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3v8\_ .sequenceNumber{fill:#707070;}#chatgpt-mermaid-\_r_3v8\_ [id$="-sequencenumber"]{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3v8\_ [id$="-crosshead"] path{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3v8\_ .messageText{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_3v8\_ .labelBox{stroke:rgba(0, 0, 0, 0.1);fill:rgb(252, 252, 252);filter:none;}#chatgpt-mermaid-\_r_3v8\_ .labelText,#chatgpt-mermaid-\_r_3v8\_ .labelText>tspan{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_3v8\_ .loopText,#chatgpt-mermaid-\_r_3v8\_ .loopText>tspan{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_3v8\_ .sectionTitle,#chatgpt-mermaid-\_r_3v8\_ .sectionTitle>tspan{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_3v8\_ .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:rgba(0, 0, 0, 0.1);fill:rgba(0, 0, 0, 0.1);}#chatgpt-mermaid-\_r_3v8\_ .note{stroke:rgb(107, 198, 127);fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_3v8\_ .noteText,#chatgpt-mermaid-\_r_3v8\_ .noteText>tspan{fill:rgb(13, 13, 13);stroke:none;font-weight:normal;}#chatgpt-mermaid-\_r_3v8\_ .activation0{fill:rgb(243, 243, 243);stroke:hsl(0, 0%, 85.2941176471%);}#chatgpt-mermaid-\_r_3v8\_ .activation1{fill:rgb(243, 243, 243);stroke:hsl(0, 0%, 85.2941176471%);}#chatgpt-mermaid-\_r_3v8\_ .activation2{fill:rgb(243, 243, 243);stroke:hsl(0, 0%, 85.2941176471%);}#chatgpt-mermaid-\_r_3v8\_ .actorPopupMenu{position:absolute;}#chatgpt-mermaid-\_r_3v8\_ .actorPopupMenuPanel{position:absolute;fill:rgb(222, 234, 251);box-shadow:0px 8px 16px 0px rgba(0,0,0,0.2);filter:drop-shadow(3px 5px 2px rgb(0 0 0 / 0.4));}#chatgpt-mermaid-\_r_3v8\_ .actor-man circle,#chatgpt-mermaid-\_r_3v8\_ line{fill:rgb(222, 234, 251);stroke-width:2px;}#chatgpt-mermaid-\_r_3v8\_ g rect.rect{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_3v8\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_3v8\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_3v8\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_3v8\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_3v8\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3v8\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_3v8\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_3v8\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_3v8\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3v8\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_3v8\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_3v8\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3v8\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_3v8\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_3v8\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3v8\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_3v8\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3v8\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}GET /studentsCheck request URLPrepare student dataHTTP 200 + JSONDisplay student data

Suggested project structure:

```
16_HTTP_Server/
│
├── README.md
│
├── 01_server_intro.js
├── 02_server_response.js
├── 03_server_port.js
├── 04_request_object.js
├── 05_response_object.js
├── 06_http_methods.js
├── 07_url_routing.js
├── 08_json_response.js
├── 09_post_request.js
├── 10_student_api.js
│
└── images/
    ├── server-architecture.png
    ├── request-response.png
    └── server-routing.png
```

GitHub image example:

```
![Node.js Server Architecture](./images/server-architecture.png)
```

Remember: Add the actual image files to your GitHub repository. The Markdown reference alone does not create an image.

# 5. HTTP module syntax

Node.js provides the `http` module as a built-in module.

### Step 1 — Import HTTP module

CommonJS:

```
const http = require("http");
```

ES Modules:

```
import http from "node:http";
```

Use the import style that matches your project configuration.

### Step 2 — Create server

```
const server = http.createServer((req, res) => {

    // Handle incoming request

});
```

### Step 3 — Start server

```
server.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

### Complete syntax

```
const http = require("http");

const server = http.createServer((req, res) => {

    // Request handling logic

    res.end("Hello World");

});

server.listen(3000, () => {

    console.log("Server running");

});
```

### Understand the important methods

| Method                | Purpose                               |
| --------------------- | ------------------------------------- |
| `http.createServer()` | Creates an HTTP server                |
| `server.listen()`     | Starts listening for connections      |
| `res.writeHead()`     | Sets status code and response headers |
| `res.write()`         | Writes response data                  |
| `res.end()`           | Completes the response                |
| `req.url`             | Gets the requested URL                |
| `req.method`          | Gets the HTTP method                  |

# 6. Basic example — Create your first server

Let's create your first HTTP server.

File: `01_server_intro.js`

```
// Import the built-in HTTP module
const http = require("http");

// Create an HTTP server
const server = http.createServer((req, res) => {

    // Send response to the client
    res.end("Hello from Node.js Server!");

});

// Start the server on port 3000
server.listen(3000, () => {

    console.log("Server running at http://localhost:3000");

});
```

### Step 1 — Run the program

Open your VS Code terminal.

```
node 01_server_intro.js
```

### Step 2 — Open browser

Visit:

[Open your local Node.js server](http://localhost:3000?utm_source=chatgpt.com)

You should see:

```
Hello from Node.js Server!
```

Congratulations!

You have created your first Node.js HTTP server.

### Step 3 — Stop the server

In the terminal, press:

```
Ctrl + C
```

This stops the running server.

# 7. Dry run

Let's understand how the first server works.

```
const http = require("http");

const server = http.createServer((req, res) => {

    res.end("Hello from Node.js Server!");

});

server.listen(3000, () => {

    console.log("Server running");

});
```

### Step-by-step execution

| Step | Code                    | What happens?                   |
| ---- | ----------------------- | ------------------------------- |
| 1    | `require("http")`       | Imports HTTP module             |
| 2    | `http.createServer()`   | Creates server                  |
| 3    | `(req, res) => {}`      | Defines request handler         |
| 4    | `server.listen(3000)`   | Starts server                   |
| 5    | Browser opens localhost | Sends HTTP request              |
| 6    | `res.end()`             | Sends response and completes it |

### Important understanding

The server does not execute the request handler only once when it starts.

The handler executes when an incoming request is received.

For example, if you refresh the browser three times, the server can handle three separate requests.

# 8. Output

### Terminal output

```
Server running at http://localhost:3000
```

### Browser output

```
Hello from Node.js Server!
```

### What if the server is already running on port 3000?

You may receive an error similar to:

```
Error: listen EADDRINUSE: address already in use :::3000
```

This means another process is already using that port.

Stop the other server or choose a different available port.

# 9. Line-by-line explanation

Now let's understand the important HTTP server concepts.

## A. Request object — `req`

The request object contains information about the incoming client request.

Example:

```
const http = require("http");

const server = http.createServer((req, res) => {

    console.log("URL:", req.url);

    console.log("Method:", req.method);

    res.end("Request received");

});

server.listen(3000);
```

Open:

```
http://localhost:3000/students
```

Terminal output:

```
URL: /students
Method: GET
```

Important request properties:

| Property                   | Purpose                      |
| -------------------------- | ---------------------------- |
| `req.url`                  | Requested URL path and query |
| `req.method`               | HTTP method                  |
| `req.headers`              | Request headers              |
| `req.socket.remoteAddress` | Remote connection address    |

## B. Response object — `res`

The response object helps the server send data to the client.

### `res.writeHead()`

Used to set the HTTP status code and response headers.

```
res.writeHead(200, {
    "Content-Type": "text/plain"
});
```

Here:

- `200` means success.
- `Content-Type` tells the client the response format.

### `res.write()`

Writes response content.

```
res.write("Hello ");
res.write("Node.js");
```

### `res.end()`

Finishes the response.

```
res.end();
```

You can also send the final content directly:

```
res.end("Hello Node.js");
```

💡 Important: Always complete the response. If a request handler does not end or otherwise complete the response, the client may keep waiting.

## C. Send HTML response

File: `02_server_response.js`

```
const http = require("http");

const server = http.createServer((req, res) => {

    // Set response status and content type
    res.writeHead(200, {
        "Content-Type": "text/html; charset=utf-8"
    });

    // Send HTML content
    res.end(`
        <h1>Welcome to Node.js</h1>
        <p>My first HTTP server</p>
    `);

});

server.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

Browser output:

# Welcome to Node.js

My first HTTP server

## D. Send JSON response

Backend APIs commonly return JSON data.

File: `08_json_response.js`

```
const http = require("http");

const server = http.createServer((req, res) => {

    // Student information
    const student = {
        id: 101,
        name: "Ramesh",
        course: "Node.js"
    };

    // Set JSON response header
    res.writeHead(200, {
        "Content-Type": "application/json"
    });

    // Convert JavaScript object into JSON text
    res.end(JSON.stringify(student));

});

server.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

Output:

```
{
    "id": 101,
    "name": "Ramesh",
    "course": "Node.js"
}
```

Why use `JSON.stringify()`?

`student` is a JavaScript object. `JSON.stringify()` converts it into JSON text so it can be sent in the HTTP response.

## E. URL routing

Routing means deciding what response to send based on the requested URL and HTTP method.

For example:

| URL         | Response            |
| ----------- | ------------------- |
| `/`         | Home page           |
| `/students` | Student information |
| `/products` | Product information |
| `/about`    | About page          |

File: `07_url_routing.js`

```
const http = require("http");

const server = http.createServer((req, res) => {

    // Home route
    if (req.url === "/" && req.method === "GET") {

        res.writeHead(200, {
            "Content-Type": "text/plain"
        });

        res.end("Welcome to Home Page");

    }

    // Students route
    else if (req.url === "/students" && req.method === "GET") {

        res.writeHead(200, {
            "Content-Type": "application/json"
        });

        res.end(JSON.stringify([
            { id: 1, name: "Ramesh" },
            { id: 2, name: "Kumar" }
        ]));

    }

    // Products route
    else if (req.url === "/products" && req.method === "GET") {

        res.writeHead(200, {
            "Content-Type": "application/json"
        });

        res.end(JSON.stringify([
            { id: 101, name: "Laptop" },
            { id: 102, name: "Mobile" }
        ]));

    }

    // Unknown route
    else {

        res.writeHead(404, {
            "Content-Type": "application/json"
        });

        res.end(JSON.stringify({
            message: "Route not found"
        }));

    }

});

server.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

Try these URLs:

- [Home page](http://localhost:3000/?utm_source=chatgpt.com)
- [Students](http://localhost:3000/students?utm_source=chatgpt.com)
- [Products](http://localhost:3000/products?utm_source=chatgpt.com)
- [Unknown route example](http://localhost:3000/about?utm_source=chatgpt.com)

### URL routing flow

\#chatgpt-mermaid-\_r_43j\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_43j\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_43j\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_43j\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_43j\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_43j\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_43j\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_43j\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_43j\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_43j\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_43j\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_43j\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_43j\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_43j\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_43j\_ p{margin:0;}#chatgpt-mermaid-\_r_43j\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_43j\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_43j\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_43j\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_43j\_ .label text,#chatgpt-mermaid-\_r_43j\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_43j\_ .node rect,#chatgpt-mermaid-\_r_43j\_ .node circle,#chatgpt-mermaid-\_r_43j\_ .node ellipse,#chatgpt-mermaid-\_r_43j\_ .node polygon,#chatgpt-mermaid-\_r_43j\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_43j\_ .rough-node .label text,#chatgpt-mermaid-\_r_43j\_ .node .label text,#chatgpt-mermaid-\_r_43j\_ .image-shape .label,#chatgpt-mermaid-\_r_43j\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_43j\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_43j\_ .rough-node .label,#chatgpt-mermaid-\_r_43j\_ .node .label,#chatgpt-mermaid-\_r_43j\_ .image-shape .label,#chatgpt-mermaid-\_r_43j\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_43j\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_43j\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_43j\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_43j\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_43j\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_43j\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_43j\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_43j\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_43j\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_43j\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_43j\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_43j\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_43j\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_43j\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_43j\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_43j\_ .icon-shape,#chatgpt-mermaid-\_r_43j\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_43j\_ .icon-shape p,#chatgpt-mermaid-\_r_43j\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_43j\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_43j\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_43j\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_43j\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_43j\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_43j\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_43j\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_43j\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_43j\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_43j\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_43j\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_43j\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_43j\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_43j\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_43j\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_43j\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_43j\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_43j\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_43j\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_43j\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_43j\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_43j\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_43j\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_43j\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_43j\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_43j\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_43j\_ .node rect,#chatgpt-mermaid-\_r_43j\_ .node circle,#chatgpt-mermaid-\_r_43j\_ .node ellipse,#chatgpt-mermaid-\_r_43j\_ .node polygon,#chatgpt-mermaid-\_r_43j\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_43j\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_43j\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_43j\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_43j\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_43j\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Incoming RequestRead req.urlCheck RouteHome PageStudent DataProduct Data404 Not FoundSend Response//students/productsOther

## F. Handle query parameters

Consider this URL:

```
http://localhost:3000/students?name=Ramesh
```

Here:

- Path: `/students`
- Query parameter: `name=Ramesh`

Use the `URL` class to read the query parameters.

```
const http = require("http");

const server = http.createServer((req, res) => {

    // Create URL object
    const requestUrl = new URL(
        req.url,
        `http://${req.headers.host}`
    );

    // Read query parameter
    const name = requestUrl.searchParams.get("name");

    res.writeHead(200, {
        "Content-Type": "application/json"
    });

    res.end(JSON.stringify({
        message: `Hello ${name || "Guest"}`
    }));

});

server.listen(3000);
```

Visit:

```
http://localhost:3000/students?name=Ramesh
```

Output:

```
{
    "message": "Hello Ramesh"
}
```

## G. Handle POST request body

When the client sends a POST request, the request body arrives as a stream of data chunks.

We can listen to:

- `data` — receives incoming data chunks.
- `end` — indicates that all request data has arrived.
- `error` — handles request stream errors.

File: `09_post_request.js`

```
const http = require("http");

const server = http.createServer((req, res) => {

    if (req.url === "/students" && req.method === "POST") {

        let body = "";

        // Receive incoming data
        req.on("data", (chunk) => {

            body += chunk.toString();

        });

        // All data has arrived
        req.on("end", () => {

            try {

                // Convert JSON text into JavaScript object
                const student = JSON.parse(body);

                res.writeHead(201, {
                    "Content-Type": "application/json"
                });

                res.end(JSON.stringify({
                    message: "Student created successfully",
                    data: student
                }));

            } catch (error) {

                res.writeHead(400, {
                    "Content-Type": "application/json"
                });

                res.end(JSON.stringify({
                    message: "Invalid JSON data"
                }));

            }

        });

        // Handle request stream error
        req.on("error", () => {

            if (!res.writableEnded) {

                res.writeHead(400, {
                    "Content-Type": "application/json"
                });

                res.end(JSON.stringify({
                    message: "Request error"
                }));

            }

        });

    } else {

        res.writeHead(404, {
            "Content-Type": "application/json"
        });

        res.end(JSON.stringify({
            message: "Route not found"
        }));

    }

});

server.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

### Test using Postman

Method:

```
POST
```

URL:

```
http://localhost:3000/students
```

Body → raw → JSON:

```
{
    "name": "Ramesh",
    "course": "Node.js"
}
```

Expected response:

```
{
    "message": "Student created successfully",
    "data": {
        "name": "Ramesh",
        "course": "Node.js"
    }
}
```

This example returns the submitted student data but does not save it permanently. Database storage will be covered in later backend chapters.

# 10. Practical example — Student API

Now let's combine the concepts and create a small Student API.

### Requirements

1. Create an HTTP server.
2. Display all students.
3. Display a single student by ID.
4. Create a new student.
5. Return 404 when a student is not found.

File: `10_student_api.js`

```
const http = require("http");

// Sample student data
let students = [
    { id: 1, name: "Ramesh", course: "Node.js" },
    { id: 2, name: "Kumar", course: "React.js" }
];

// Create HTTP server
const server = http.createServer((req, res) => {

    // Parse incoming URL
    const requestUrl = new URL(
        req.url,
        `http://${req.headers.host}`
    );

    // GET all students
    if (requestUrl.pathname === "/students" && req.method === "GET") {

        res.writeHead(200, {
            "Content-Type": "application/json"
        });

        res.end(JSON.stringify(students));

    }

    // GET one student
    else if (
        requestUrl.pathname.startsWith("/students/") &&
        req.method === "GET"
    ) {

        const id = Number(
            requestUrl.pathname.split("/")[2]
        );

        const student = students.find(
            (item) => item.id === id
        );

        if (!student) {

            res.writeHead(404, {
                "Content-Type": "application/json"
            });

            res.end(JSON.stringify({
                message: "Student not found"
            }));

            return;
        }

        res.writeHead(200, {
            "Content-Type": "application/json"
        });

        res.end(JSON.stringify(student));

    }

    // POST create student
    else if (
        requestUrl.pathname === "/students" &&
        req.method === "POST"
    ) {

        let body = "";

        req.on("data", (chunk) => {
            body += chunk.toString();
        });

        req.on("end", () => {

            try {

                const data = JSON.parse(body);

                if (!data.name || !data.course) {

                    res.writeHead(400, {
                        "Content-Type": "application/json"
                    });

                    res.end(JSON.stringify({
                        message: "Name and course are required"
                    }));

                    return;
                }

                const newStudent = {
                    id: Date.now(),
                    name: data.name,
                    course: data.course
                };

                students.push(newStudent);

                res.writeHead(201, {
                    "Content-Type": "application/json"
                });

                res.end(JSON.stringify({
                    message: "Student created",
                    data: newStudent
                }));

            } catch (error) {

                res.writeHead(400, {
                    "Content-Type": "application/json"
                });

                res.end(JSON.stringify({
                    message: "Invalid JSON data"
                }));

            }

        });

    }

    // Unknown route
    else {

        res.writeHead(404, {
            "Content-Type": "application/json"
        });

        res.end(JSON.stringify({
            message: "Route not found"
        }));

    }

});

// Start server
server.listen(3000, () => {

    console.log("Student API running at http://localhost:3000");

});
```

### Test endpoints

| Method | URL             | Purpose                |
| ------ | --------------- | ---------------------- |
| GET    | `/students`     | Get all students       |
| GET    | `/students/1`   | Get student by ID      |
| POST   | `/students`     | Create student         |
| GET    | `/students/999` | Test student not found |

### POST body

```
{
    "name": "Ramesh",
    "course": "Node.js"
}
```

### Important limitation

This example stores data in a JavaScript array.

When you restart the server, newly added student records disappear. In a real application, you will use a database such as MongoDB or PostgreSQL.

# 11. Common mistakes

### Mistake 1 — Forgetting `res.end()`

Wrong

```
const server = http.createServer((req, res) => {

    console.log("Request received");

});
```

The client may keep waiting because the response was not completed.

Correct

```
const server = http.createServer((req, res) => {

    console.log("Request received");

    res.end("Response completed");

});
```

### Mistake 2 — Sending a JavaScript object directly

Wrong

```
res.end({ name: "Ramesh" });
```

`res.end()` expects response data such as a string or buffer, not an ordinary JavaScript object.

Correct

```
res.end(JSON.stringify({
    name: "Ramesh"
}));
```

### Mistake 3 — Forgetting Content-Type

Wrong:

```
res.writeHead(200);
res.end(JSON.stringify({ name: "Ramesh" }));
```

Better:

```
res.writeHead(200, {
    "Content-Type": "application/json"
});

res.end(JSON.stringify({ name: "Ramesh" }));
```

### Mistake 4 — Using the wrong HTTP method

A GET request and a POST request are different operations.

Check both:

```
if (req.url === "/students" && req.method === "GET") {

    // Get students

}
```

### Mistake 5 — Not handling invalid JSON

Incorrect:

```
const data = JSON.parse(body);
```

Better:

```
try {

    const data = JSON.parse(body);

} catch (error) {

    console.log("Invalid JSON");

}
```

### Mistake 6 — Using an already occupied port

Error:

```
EADDRINUSE
```

Solution: stop the existing server or select a different available port.

# 12. Best practices

1. Use meaningful route names such as `/students` and `/products`.
2. Use appropriate HTTP methods.
3. Send correct status codes.
4. Always complete responses.
5. Use `Content-Type` headers correctly.
6. Validate incoming request data.
7. Handle invalid JSON safely.
8. Avoid hard-coding passwords and API keys.
9. Use environment variables for configuration.
10. Separate routing, business logic and data storage as your application grows.
11. Use a database for persistent storage.
12. Use HTTPS in production.
13. Avoid exposing internal error details to clients.
14. Add request size limits when processing user-submitted data.
15. Handle server startup and runtime errors appropriately.

### Professional project structure

As your backend application grows, organize it into separate files:

```
student-api/
│
├── src/
│   ├── server.js
│   ├── routes/
│   │   └── studentRoutes.js
│   ├── controllers/
│   │   └── studentController.js
│   ├── services/
│   │   └── studentService.js
│   └── data/
│       └── students.js
│
├── .env
├── .gitignore
├── package.json
└── README.md
```

This structure separates responsibilities and makes the project easier to maintain.

# 13. Interview questions

## Beginner level

Q1. What is the HTTP module in Node.js?

The HTTP module is a built-in Node.js module used to create HTTP servers and handle HTTP communication.

Q2. How do you import the HTTP module?

```
const http = require("http");
```

Q3. What is `http.createServer()`?

It creates an HTTP server and accepts a request handler function.

Q4. What are `req` and `res`?

- `req` contains incoming request information.
- `res` is used to send a response.

Q5. What is `server.listen()`?

It starts the server and listens for incoming connections on a specified port.

## Intermediate level

Q6. What is the difference between `res.write()` and `res.end()`?

`res.write()` adds response data. `res.end()` completes the response and can also send final data.

Q7. What is `req.url`?

It contains the requested URL path and query string.

Q8. What is `req.method`?

It contains the HTTP method, such as GET, POST, PUT or DELETE.

Q9. What is routing?

Routing is the process of selecting a response based on the request URL and method.

Q10. How do you send JSON from a Node.js HTTP server?

Set the JSON content type and use `JSON.stringify()` to convert an object into JSON text.

## Advanced level

Q11. What happens when a client sends a POST request body?

The body arrives as a readable stream. The server can collect chunks using the `data` event and process the complete body using the `end` event.

Q12. What is the difference between Node.js HTTP module and Express.js?

The HTTP module is built into Node.js and provides low-level HTTP server functionality. Express.js is a framework that provides convenient routing, middleware and request/response helpers.

Q13. Why do we use `JSON.stringify()`?

To convert a JavaScript object into JSON text that can be sent in an HTTP response.

Q14. What is a port number?

A port number identifies a communication endpoint on a computer where an application can listen for connections.

Q15. Does the HTTP module require installation?

No. It is built into Node.js.

# 14. Practice problems

Try these exercises in VS Code.

Practice checklist

0/7

Exercise 1: Create a server on port 3000 that returns Hello Node.js.

💡 Show hint

Exercise 2: Create a server that returns your name and course as JSON.

💡 Show hint

Exercise 3: Create a GET /students route that returns an array of students.

💡 Show hint

Exercise 4: Create a GET /about route that returns an HTML response.

💡 Show hint

Exercise 5: Create a GET /students/1 route that returns one student.

💡 Show hint

Exercise 6: Create a POST /students route that reads JSON request data.

💡 Show hint

Exercise 7: Return a JSON 404 response for unknown routes.

💡 Show hint

# 15. Mini challenge — Student Management HTTP Server

Practical challenge

Build a small Student Management API using the Node.js HTTP module.

### Requirements

Your server should support:

| Method | Endpoint      | Function             |
| ------ | ------------- | -------------------- |
| GET    | `/students`   | Get all students     |
| GET    | `/students/1` | Get student by ID    |
| POST   | `/students`   | Create a student     |
| DELETE | `/students/1` | Delete student by ID |

### Additional requirements

- Use an array to store student information.
- Use `JSON.stringify()` for JSON responses.
- Return `201` when a student is created.
- Return `404` when a student is not found.
- Return `400` for invalid JSON or missing required fields.
- Handle unknown routes.
- Use proper HTTP methods.

### Starter code

```
const http = require("http");

let students = [
    { id: 1, name: "Ramesh", course: "Node.js" },
    { id: 2, name: "Kumar", course: "React.js" }
];

const server = http.createServer((req, res) => {

    // 1. GET all students

    // 2. GET student by ID

    // 3. POST new student

    // 4. DELETE student by ID

    // 5. Handle unknown routes

});

server.listen(3000, () => {

    console.log("Student API running");

});
```

Try building the logic yourself before looking at a complete solution.

# 16. Chapter summary

| Topic            | What you learned             |
| ---------------- | ---------------------------- |
| HTTP module      | Built-in Node.js module      |
| `createServer()` | Creates HTTP server          |
| `listen()`       | Starts server                |
| `req`            | Incoming request             |
| `res`            | Outgoing response            |
| `req.url`        | Requested URL                |
| `req.method`     | HTTP method                  |
| `writeHead()`    | Sets status and headers      |
| `write()`        | Writes response data         |
| `end()`          | Completes response           |
| Routing          | Selects the correct endpoint |
| JSON response    | Sends JSON data              |
| POST body        | Reads incoming request data  |
| 404              | Resource or route not found  |

# 17. Quick revision

Remember these important lines:

```
const http = require("http");

const server = http.createServer((req, res) => {

    res.writeHead(200, {
        "Content-Type": "application/json"
    });

    res.end(JSON.stringify({
        message: "Hello Node.js"
    }));

});

server.listen(3000);
```

Five important points:

1. `http` is a built-in Node.js module.
2. `createServer()` creates the server.
3. `req` contains incoming request information.
4. `res` sends the response.
5. `listen()` starts the server.

## 📁 GitHub README checklist

- Create `16_HTTP_Server` folder.
- Create `README.md`.
- Add all JavaScript examples.
- Add Mermaid architecture diagrams.
- Add actual images to the `images/` directory if required.
- Verify image paths in GitHub.
- Run the server using VS Code terminal.
- Test endpoints using Postman.
- Complete the Student Management API challenge.

Suggested GitHub image references:

```
![Server Architecture](./images/server-architecture.png)

![Request Response](./images/request-response.png)

![Server Routing](./images/server-routing.png)
```

Chapter 16 completed

You have now learned how to create a basic backend HTTP server using Node.js without Express.js.

Practice the Student Management API challenge before moving forward.

When you are ready, type `NEXT` to start:

# Chapter 17 — Express.js Introduction 🚀