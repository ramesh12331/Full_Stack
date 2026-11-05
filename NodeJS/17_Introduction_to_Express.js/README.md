# 🚀 PART 5 — EXPRESS.JS

# Chapter 17 — Introduction to Express.js



Chapter 17

Beginner to Advanced



Welcome to Express.js! 🎉

Until now, you have learned how to create an HTTP server using the built-in Node.js `http` module.

Now you will learn Express.js, a popular framework used to build backend applications and REST APIs more easily.

In this chapter, you will learn:

- What is Express.js?
- Why do we need Express?
- Node.js vs Express.js
- Installing Express
- Creating an Express server
- `app.listen()`
- Request (`req`)
- Response (`res`)

## 📖 Interactive learning icons

# 📖

Read

Learning guidance

# 💡

Important

Remember this

## 🔑 Requires Before Starting

Before learning Express.js, you should understand these concepts:

| Previous topic | What you should know             |
| -------------- | -------------------------------- |
| Node.js        | JavaScript runtime environment   |
| NPM            | Installing packages              |
| Modules        | Importing and exporting files    |
| Functions      | Creating and calling functions   |
| Callbacks      | Passing functions as arguments   |
| Promises       | Handling asynchronous operations |
| Async/Await    | Writing asynchronous code        |
| HTTP           | Request and response             |
| HTTP methods   | GET, POST, PUT, PATCH, DELETE    |
| JSON           | Sending and receiving data       |

### Quick revision

You previously created an HTTP server using Node.js.

```
const http = require("http");

const server = http.createServer((req, res) => {

    res.end("Hello from Node.js");

});

server.listen(3000);
```

This works, but as your backend grows, you need to write more code for routing, request handling and middleware.

Express makes these tasks easier.

# 1. What is Express.js?

Express.js is a web framework for Node.js.

It helps developers build web applications and REST APIs with less code.

In simple words:

- Node.js allows JavaScript to run outside the browser.
- Express.js makes it easier to create backend servers using Node.js.

### Simple example

Using Node.js HTTP module:

```
const http = require("http");

const server = http.createServer((req, res) => {

    if (req.url === "/") {
        res.end("Welcome Home");
    }

});

server.listen(3000);
```

Using Express.js:

```
const express = require("express");

const app = express();

app.get("/", (req, res) => {

    res.send("Welcome Home");

});

app.listen(3000);
```

Notice the difference?

Express provides convenient methods such as:

- `app.get()`
- `app.post()`
- `app.put()`
- `app.patch()`
- `app.delete()`
- `res.send()`
- `res.json()`

You will learn these methods in upcoming chapters.

💡 Important: Express does not replace Node.js. Express runs on top of Node.js.

# 2. Why do we need Express.js?

Imagine you are developing a Student Management System.

Your backend needs to:

1. Get all students.
2. Get one student.
3. Register a student.
4. Update student information.
5. Delete a student.

Using only the Node.js HTTP module, you need to manually check URLs and HTTP methods.

As your application grows, this code becomes difficult to manage.

### Without Express

```
if (req.url === "/students" && req.method === "GET") {

    // Get students

} else if (req.url === "/students" && req.method === "POST") {

    // Create student

} else if (req.url === "/students/1" && req.method === "GET") {

    // Get one student

}
```

### With Express

```
app.get("/students", (req, res) => {

    res.send("Get all students");

});

app.post("/students", (req, res) => {

    res.send("Create student");

});
```

Express provides a cleaner way to organize backend code.

### Benefits of Express.js

| Benefit           | Explanation                                    |
| ----------------- | ---------------------------------------------- |
| Easy routing      | Define endpoints easily                        |
| Middleware        | Process requests before handlers               |
| Request handling  | Access incoming request information            |
| Response handling | Send responses easily                          |
| REST APIs         | Build backend APIs                             |
| Modular structure | Organize routes and controllers                |
| Integration       | Work with databases and other Node.js packages |

# 3. Real-world analogy

Imagine a restaurant.

[Week 14 — Behavioral Design Pattern: Command | by Heliotechie | Coffee☕ And Code💚 | Jan, 2026 | Medium](https://images.openai.com/static-rsc-4/UJGromwfE3v3PKO1oWM0yc9vDysdf1Gpf62QYYvheOasDq4pUXVVMdT7i9Jfpe1OxflARmbgZsAzFFa6UA8fEDevY2u04UN0Ej2SKDGh5cwKwZKF5ZTPCy9sOVr9pjJ44RrazuuNApcTjx8Ub-neVnUv7BWC93ZL6ckSXr4feWY?purpose=inline)

[medium.com](https://medium.com/techtrends-digest/week-14-behavioral-design-pattern-command-87198cba8d58?utm_source=chatgpt.com)

| Restaurant         | Backend application |
| ------------------ | ------------------- |
| Customer           | Client / Browser    |
| Order              | HTTP request        |
| Reception / Waiter | Express routing     |
| Kitchen            | Backend logic       |
| Food preparation   | Processing          |
| Food delivery      | HTTP response       |

A customer places an order.

The waiter receives it and sends it to the correct kitchen section.

Similarly, Express receives a request and sends it to the appropriate route handler.

# 4. Architecture / flow

### Node.js + Express architecture

\#chatgpt-mermaid-\_r_4c7\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_4c7\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_4c7\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_4c7\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_4c7\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4c7\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_4c7\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_4c7\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_4c7\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_4c7\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_4c7\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_4c7\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4c7\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4c7\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_4c7\_ p{margin:0;}#chatgpt-mermaid-\_r_4c7\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4c7\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4c7\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4c7\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_4c7\_ .label text,#chatgpt-mermaid-\_r_4c7\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4c7\_ .node rect,#chatgpt-mermaid-\_r_4c7\_ .node circle,#chatgpt-mermaid-\_r_4c7\_ .node ellipse,#chatgpt-mermaid-\_r_4c7\_ .node polygon,#chatgpt-mermaid-\_r_4c7\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_4c7\_ .rough-node .label text,#chatgpt-mermaid-\_r_4c7\_ .node .label text,#chatgpt-mermaid-\_r_4c7\_ .image-shape .label,#chatgpt-mermaid-\_r_4c7\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_4c7\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_4c7\_ .rough-node .label,#chatgpt-mermaid-\_r_4c7\_ .node .label,#chatgpt-mermaid-\_r_4c7\_ .image-shape .label,#chatgpt-mermaid-\_r_4c7\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_4c7\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_4c7\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4c7\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4c7\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_4c7\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_4c7\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_4c7\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_4c7\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_4c7\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_4c7\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_4c7\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4c7\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4c7\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_4c7\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4c7\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_4c7\_ .icon-shape,#chatgpt-mermaid-\_r_4c7\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_4c7\_ .icon-shape p,#chatgpt-mermaid-\_r_4c7\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_4c7\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_4c7\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_4c7\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_4c7\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_4c7\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_4c7\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_4c7\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_4c7\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_4c7\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4c7\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_4c7\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_4c7\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_4c7\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4c7\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_4c7\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_4c7\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4c7\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_4c7\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_4c7\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4c7\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_4c7\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4c7\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_4c7\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_4c7\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_4c7\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_4c7\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_4c7\_ .node rect,#chatgpt-mermaid-\_r_4c7\_ .node circle,#chatgpt-mermaid-\_r_4c7\_ .node ellipse,#chatgpt-mermaid-\_r_4c7\_ .node polygon,#chatgpt-mermaid-\_r_4c7\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_4c7\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_4c7\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_4c7\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_4c7\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4c7\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Client / React ApplicationNode.js RuntimeExpress ApplicationExpress RouterRoute HandlerBusiness LogicDatabaseHTTP ResponseHTTP Request

### Understand the flow

1. React sends an HTTP request.
2. Node.js receives the network connection.
3. Express handles the request.
4. Express identifies the matching route.
5. The route handler executes.
6. Backend logic processes the request.
7. The server sends a response.
8. React receives the response.

### GitHub README diagram

GitHub supports Mermaid diagrams directly.

DatabaseExpressNode.jsReact ClientDatabaseExpressNode.jsReact Client#chatgpt-mermaid-\_r_4ce\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_4ce\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_4ce\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_4ce\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_4ce\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4ce\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_4ce\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_4ce\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_4ce\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_4ce\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_4ce\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_4ce\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4ce\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4ce\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_4ce\_ p{margin:0;}#chatgpt-mermaid-\_r_4ce\_ .actor{stroke:rgb(83, 154, 248);fill:rgb(222, 234, 251);stroke-width:1;}#chatgpt-mermaid-\_r_4ce\_ rect.actor.outer-path[data-look="neo"]{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4ce\_ rect.note[data-look="neo"]{stroke:rgb(107, 198, 127);fill:rgb(243, 243, 243);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4ce\_ text.actor>tspan{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_4ce\_ .actor-line{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4ce\_ .innerArc{stroke-width:1.5;stroke-dasharray:none;}#chatgpt-mermaid-\_r_4ce\_ .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4ce\_ .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4ce\_ [id$="-arrowhead"] path{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4ce\_ .sequenceNumber{fill:#707070;}#chatgpt-mermaid-\_r_4ce\_ [id$="-sequencenumber"]{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4ce\_ [id$="-crosshead"] path{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4ce\_ .messageText{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_4ce\_ .labelBox{stroke:rgba(0, 0, 0, 0.1);fill:rgb(252, 252, 252);filter:none;}#chatgpt-mermaid-\_r_4ce\_ .labelText,#chatgpt-mermaid-\_r_4ce\_ .labelText>tspan{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_4ce\_ .loopText,#chatgpt-mermaid-\_r_4ce\_ .loopText>tspan{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_4ce\_ .sectionTitle,#chatgpt-mermaid-\_r_4ce\_ .sectionTitle>tspan{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_4ce\_ .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:rgba(0, 0, 0, 0.1);fill:rgba(0, 0, 0, 0.1);}#chatgpt-mermaid-\_r_4ce\_ .note{stroke:rgb(107, 198, 127);fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_4ce\_ .noteText,#chatgpt-mermaid-\_r_4ce\_ .noteText>tspan{fill:rgb(13, 13, 13);stroke:none;font-weight:normal;}#chatgpt-mermaid-\_r_4ce\_ .activation0{fill:rgb(243, 243, 243);stroke:hsl(0, 0%, 85.2941176471%);}#chatgpt-mermaid-\_r_4ce\_ .activation1{fill:rgb(243, 243, 243);stroke:hsl(0, 0%, 85.2941176471%);}#chatgpt-mermaid-\_r_4ce\_ .activation2{fill:rgb(243, 243, 243);stroke:hsl(0, 0%, 85.2941176471%);}#chatgpt-mermaid-\_r_4ce\_ .actorPopupMenu{position:absolute;}#chatgpt-mermaid-\_r_4ce\_ .actorPopupMenuPanel{position:absolute;fill:rgb(222, 234, 251);box-shadow:0px 8px 16px 0px rgba(0,0,0,0.2);filter:drop-shadow(3px 5px 2px rgb(0 0 0 / 0.4));}#chatgpt-mermaid-\_r_4ce\_ .actor-man circle,#chatgpt-mermaid-\_r_4ce\_ line{fill:rgb(222, 234, 251);stroke-width:2px;}#chatgpt-mermaid-\_r_4ce\_ g rect.rect{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_4ce\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_4ce\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_4ce\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_4ce\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_4ce\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4ce\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_4ce\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_4ce\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_4ce\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4ce\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_4ce\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_4ce\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4ce\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_4ce\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_4ce\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4ce\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_4ce\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4ce\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}HTTP RequestPass requestMatch routeGet dataReturn dataHTTP JSON Response

### Suggested project structure

```
17_Introduction_Express/
│
├── README.md
│
├── 01_express_intro.js
├── 02_express_server.js
├── 03_app_listen.js
├── 04_request_response.js
│
└── images/
    ├── express-architecture.png
    └── express-request-flow.png
```

To display images in GitHub, add the actual image files to the repository.

Example:

```
![Express Architecture](./images/express-architecture.png)
```

Mermaid diagrams can display directly in GitHub without creating separate image files.

# 5. Express.js installation and syntax

Let's install Express.js in your computer.

### Step 1 — Create project folder

Open VS Code terminal.

```
mkdir 17_Introduction_Express

cd 17_Introduction_Express
```

### Step 2 — Initialize Node.js project

```
npm init -y
```

This command creates:

```
package.json
```

The `package.json` file contains project information and dependencies.

### Step 3 — Install Express

```
npm install express
```

NPM downloads Express and adds it to your project's dependencies.

Your project now contains:

```
17_Introduction_Express/
│
├── node_modules/
├── package-lock.json
└── package.json
```

### Step 4 — Create JavaScript file

Create:

```
server.js
```

### Step 5 — Import Express

We will use CommonJS in this chapter.

```
const express = require("express");
```

### Step 6 — Create Express application

```
const app = express();
```

### Step 7 — Create a route

```
app.get("/", (req, res) => {

    res.send("Hello Express!");

});
```

### Step 8 — Start server

```
app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

# 6. Basic example — Create your first Express server

Let's build a simple Express application.

File: `01_express_intro.js`

```
// Import Express package
const express = require("express");

// Create Express application
const app = express();

// Create home route
app.get("/", (req, res) => {

    // Send response to client
    res.send("Hello from Express.js!");

});

// Start server
app.listen(3000, () => {

    console.log("Express server running at http://localhost:3000");

});
```

### Run the program

```
node 01_express_intro.js
```

### Open your browser

[Open Express server](http://localhost:3000?utm_source=chatgpt.com)

Expected browser response:

```
Hello from Express.js!
```

Congratulations!

You have successfully created your first Express server.

# 7. Dry run

Let's understand the execution step by step.

```
const express = require("express");

const app = express();

app.get("/", (req, res) => {

    res.send("Hello Express!");

});

app.listen(3000);
```

### Execution flow

| Step | Code                    | What happens?       |
| ---- | ----------------------- | ------------------- |
| 1    | `require("express")`    | Imports Express     |
| 2    | `express()`             | Creates application |
| 3    | `app.get()`             | Registers GET route |
| 4    | `app.listen(3000)`      | Starts server       |
| 5    | Browser opens localhost | Sends GET request   |
| 6    | Route handler executes  | Processes request   |
| 7    | `res.send()`            | Sends response      |

### Important understanding

`app.get()` does not immediately send a response when the application starts.

It registers a route.

When a client sends a GET request to `/`, Express executes that route handler.

# 8. Output

### Terminal output

```
Express server running at http://localhost:3000
```

### Browser output

```
Hello from Express.js!
```

### Test another route

Add this route:

```
app.get("/about", (req, res) => {

    res.send("This is About Page");

});
```

Now visit:

[Open About page](http://localhost:3000/about?utm_source=chatgpt.com)

Output:

```
This is About Page
```

# 9. Line-by-line explanation

Let's understand the important Express concepts.

## A. `express()`

This creates an Express application.

```
const app = express();
```

Here:

- `express` is the imported framework function.
- `express()` creates the application.
- `app` is the object used to configure your backend.

You use `app` to define routes, middleware and server behavior.

## B. `app.listen()`

This starts your Express server and makes it listen for incoming connections on a port.

Syntax:

```
app.listen(PORT, callback);
```

Example:

```
app.listen(3000, () => {

    console.log("Server started");

});
```

Here:

- `3000` is the port number.
- The callback runs when the server starts listening.

### Using a separate port variable

```
const PORT = 3000;

app.listen(PORT, () => {

    console.log(`Server running on port ${PORT}`);

});
```

## C. Request object — `req`

The request object contains information about the incoming request.

Example:

```
app.get("/students", (req, res) => {

    console.log(req.method);

    console.log(req.url);

    res.send("Students API");

});
```

Open:

[Students endpoint](http://localhost:3000/students?utm_source=chatgpt.com)

Terminal output:

```
GET
/students
```

Some important request properties:

| Property      | Purpose          |
| ------------- | ---------------- |
| `req.method`  | HTTP method      |
| `req.url`     | Requested URL    |
| `req.params`  | Route parameters |
| `req.query`   | Query parameters |
| `req.body`    | Request body     |
| `req.headers` | Request headers  |

You will study `params`, `query` and `body` in detail in Chapter 18 and Chapter 25.

## D. Response object — `res`

The response object is used to send information back to the client.

### `res.send()`

Sends a response.

```
app.get("/", (req, res) => {

    res.send("Welcome to Express!");

});
```

### `res.json()`

Sends a JSON response.

```
app.get("/student", (req, res) => {

    res.json({
        id: 101,
        name: "Ramesh",
        course: "Node.js"
    });

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

### `res.status()`

Sets the HTTP response status code.

```
app.get("/students", (req, res) => {

    res.status(200).json({
        message: "Students fetched successfully"
    });

});
```

### `res.sendStatus()`

Sends a status code with its standard status message.

```
app.get("/not-found", (req, res) => {

    res.sendStatus(404);

});
```

### Important request vs response comparison

| `req`                 | `res`                  |
| --------------------- | ---------------------- |
| Incoming request      | Outgoing response      |
| Client sends it       | Server sends it        |
| Contains request data | Contains response data |
| `req.method`          | `res.status()`         |
| `req.url`             | `res.send()`           |
| `req.body`            | `res.json()`           |

💡 Remember: `req` means request. `res` means response.

# 10. Practical example — Student API

Let's create a small Student API using Express.

### Requirements

1. Create Express application.
2. Create a home route.
3. Create a student route.
4. Create a products route.
5. Return JSON responses.
6. Handle unknown routes.

File: `02_express_server.js`

```
// Import Express
const express = require("express");

// Create application
const app = express();

// Server port
const PORT = 3000;

// Home route
app.get("/", (req, res) => {

    res.send("Welcome to Student Management API");

});

// Students route
app.get("/students", (req, res) => {

    const students = [
        {
            id: 1,
            name: "Ramesh",
            course: "Node.js"
        },
        {
            id: 2,
            name: "Kumar",
            course: "React.js"
        }
    ];

    res.status(200).json({
        success: true,
        data: students
    });

});

// Products route
app.get("/products", (req, res) => {

    const products = [
        {
            id: 101,
            name: "Laptop",
            price: 50000
        },
        {
            id: 102,
            name: "Mobile",
            price: 20000
        }
    ];

    res.json({
        success: true,
        data: products
    });

});

// Handle unknown routes
app.use((req, res) => {

    res.status(404).json({
        success: false,
        message: "Route not found"
    });

});

// Start server
app.listen(PORT, () => {

    console.log(`Server running at http://localhost:${PORT}`);

});
```

### Test your endpoints

| Method | Endpoint    | Expected response |
| ------ | ----------- | ----------------- |
| GET    | `/`         | Welcome message   |
| GET    | `/students` | Student list      |
| GET    | `/products` | Product list      |
| GET    | `/about`    | 404 error         |

Try:

- [Home](http://localhost:3000/?utm_source=chatgpt.com)
- [Students](http://localhost:3000/students?utm_source=chatgpt.com)
- [Products](http://localhost:3000/products?utm_source=chatgpt.com)
- [Unknown route](http://localhost:3000/about?utm_source=chatgpt.com)

### Architecture flow

\#chatgpt-mermaid-\_r_4hs\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_4hs\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_4hs\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_4hs\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_4hs\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4hs\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_4hs\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_4hs\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_4hs\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_4hs\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_4hs\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_4hs\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4hs\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4hs\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_4hs\_ p{margin:0;}#chatgpt-mermaid-\_r_4hs\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4hs\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4hs\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4hs\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_4hs\_ .label text,#chatgpt-mermaid-\_r_4hs\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4hs\_ .node rect,#chatgpt-mermaid-\_r_4hs\_ .node circle,#chatgpt-mermaid-\_r_4hs\_ .node ellipse,#chatgpt-mermaid-\_r_4hs\_ .node polygon,#chatgpt-mermaid-\_r_4hs\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_4hs\_ .rough-node .label text,#chatgpt-mermaid-\_r_4hs\_ .node .label text,#chatgpt-mermaid-\_r_4hs\_ .image-shape .label,#chatgpt-mermaid-\_r_4hs\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_4hs\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_4hs\_ .rough-node .label,#chatgpt-mermaid-\_r_4hs\_ .node .label,#chatgpt-mermaid-\_r_4hs\_ .image-shape .label,#chatgpt-mermaid-\_r_4hs\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_4hs\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_4hs\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4hs\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4hs\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_4hs\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_4hs\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_4hs\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_4hs\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_4hs\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_4hs\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_4hs\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4hs\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4hs\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_4hs\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4hs\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_4hs\_ .icon-shape,#chatgpt-mermaid-\_r_4hs\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_4hs\_ .icon-shape p,#chatgpt-mermaid-\_r_4hs\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_4hs\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_4hs\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_4hs\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_4hs\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_4hs\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_4hs\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_4hs\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_4hs\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_4hs\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4hs\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_4hs\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_4hs\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_4hs\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4hs\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_4hs\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_4hs\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4hs\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_4hs\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_4hs\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4hs\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_4hs\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4hs\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_4hs\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_4hs\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_4hs\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_4hs\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_4hs\_ .node rect,#chatgpt-mermaid-\_r_4hs\_ .node circle,#chatgpt-mermaid-\_r_4hs\_ .node ellipse,#chatgpt-mermaid-\_r_4hs\_ .node polygon,#chatgpt-mermaid-\_r_4hs\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_4hs\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_4hs\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_4hs\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_4hs\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4hs\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Browser / PostmanExpress ServerRequested URLHome RouteStudents RouteProducts Route404 HandlerResponse//students/productsUnknown

### Practical note

This example uses arrays for student and product data. It does not store information permanently in a database.

Database integration will come later.

# 11. Common mistakes

## Mistake 1 — Forgetting to install Express

Wrong situation

```
const express = require("express");
```

If Express is not installed, Node.js may show:

```
Error: Cannot find module 'express'
```

Solution

Run:

```
npm install express
```

## Mistake 2 — Forgetting to call `express()`

Wrong:

```
const express = require("express");

express.get("/", (req, res) => {
    res.send("Hello");
});
```

Correct:

```
const express = require("express");

const app = express();

app.get("/", (req, res) => {
    res.send("Hello");
});
```

## Mistake 3 — Forgetting `app.listen()`

Without starting the server, your application will not listen for incoming HTTP requests.

Correct:

```
app.listen(3000, () => {
    console.log("Server started");
});
```

## Mistake 4 — Using `res.send()` multiple times

Wrong:

```
app.get("/", (req, res) => {

    res.send("Hello");

    res.send("Welcome");

});
```

The response has already been sent. Trying to send another response can cause an error.

Correct:

```
app.get("/", (req, res) => {

    res.send("Hello and Welcome");

});
```

## Mistake 5 — Forgetting the correct HTTP method

If you define:

```
app.get("/students", (req, res) => {
    res.send("Students");
});
```

A POST request to `/students` will not match this GET route.

HTTP method and URL both matter.

# 12. Best practices

1. Use meaningful route names.
2. Keep server configuration organized.
3. Use environment variables for port and other configuration.
4. Return appropriate HTTP status codes.
5. Use `res.json()` for JSON APIs.
6. Avoid sending multiple responses for one request.
7. Separate routes and controllers as the application grows.
8. Validate incoming data.
9. Handle errors properly.
10. Keep passwords and API secrets out of source code.
11. Use a `.gitignore` file for `node_modules` and `.env`.
12. Use a consistent response structure.

### Environment variable example

Instead of hard-coding the port:

```
const PORT = 3000;
```

You can use:

```
const PORT = process.env.PORT || 3000;
```

This means:

- Use the port provided by the environment.
- If no port is provided, use `3000`.

For this example, set the variable in your terminal:

PowerShell:

```
$env:PORT=4000
node server.js
```

Your server will run on port 4000.

# 13. Interview questions

## Beginner level

Q1. What is Express.js?

Express.js is a web framework for Node.js used to build web applications and APIs.

Q2. Is Express.js a programming language?

No. Express.js is a JavaScript framework.

Q3. Why do we use Express.js?

It simplifies routing, request handling, response handling and middleware.

Q4. How do you install Express.js?

```
npm install express
```

Q5. What is `express()`?

It creates an Express application.

## Intermediate level

Q6. What is `app.listen()`?

It starts the Express server and listens for incoming connections.

Q7. What is the difference between Node.js and Express.js?

Node.js is a JavaScript runtime environment. Express.js is a framework that runs on Node.js.

Q8. What is `req`?

It represents the incoming HTTP request.

Q9. What is `res`?

It represents the outgoing HTTP response.

Q10. What is the difference between `res.send()` and `res.json()`?

`res.send()` can send different types of response content. `res.json()` sends a JSON response.

## Advanced level

Q11. Can we create a backend server without Express?

Yes. Node.js provides the built-in HTTP module.

Q12. Is Express built into Node.js?

No. Express is an external package that must be installed.

Q13. What happens if we do not call `app.listen()`?

The application does not start listening for incoming connections.

Q14. Can Express handle multiple routes?

Yes. Express supports multiple routes with different URLs and HTTP methods.

Q15. What is the difference between `app.get()` and `app.post()`?

`app.get()` handles GET requests, while `app.post()` handles POST requests.

# 14. Practice problems

Try these exercises in VS Code.

Your practice checklist

0/7

Exercise 1: Install Express and initialize a Node.js project.

💡 Show hint

Exercise 2: Create an Express server on port 3000.

💡 Show hint

Exercise 3: Create a GET /home route that returns Welcome Home.

💡 Show hint

Exercise 4: Create a GET /students route that returns three students as JSON.

💡 Show hint

Exercise 5: Create a GET /products route that returns product details.

💡 Show hint

Exercise 6: Create a GET /about route that returns an HTML response.

💡 Show hint

Exercise 7: Create a 404 handler for unknown routes.

💡 Show hint

# 15. Mini challenge — Student Management Server

Practical challenge

Build a small Express application.

### Requirements

Your application should have these endpoints:

| Method | Endpoint      | Function                  |
| ------ | ------------- | ------------------------- |
| GET    | `/`           | Display welcome message   |
| GET    | `/students`   | Display all students      |
| GET    | `/products`   | Display all products      |
| GET    | `/about`      | Display about information |
| GET    | Unknown route | Display 404 message       |

### Starter code

Create `student-server.js`:

```
const express = require("express");

const app = express();

const PORT = 3000;

// Sample data
const students = [
    { id: 1, name: "Ramesh" },
    { id: 2, name: "Kumar" }
];

// 1. Create home route


// 2. Create students route


// 3. Create products route


// 4. Create about route


// 5. Create 404 handler


// Start server
```

Try to complete the code yourself.

### Expected output

For `/students`:

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

# 16. Chapter summary

| Topic                 | What you learned                 |
| --------------------- | -------------------------------- |
| Express.js            | Node.js web framework            |
| `npm install express` | Installs Express                 |
| `express()`           | Creates Express application      |
| `app`                 | Express application object       |
| `app.listen()`        | Starts server                    |
| `req`                 | Incoming request                 |
| `res`                 | Outgoing response                |
| `app.get()`           | Handles GET requests             |
| `res.send()`          | Sends response                   |
| `res.json()`          | Sends JSON response              |
| `res.status()`        | Sets response status             |
| `app.use()`           | Registers middleware or handlers |

# 17. Quick revision

Remember these five steps:

1. Install Express.
2. Import Express.
3. Create an application.
4. Define routes.
5. Start the server.

Important syntax:

```
const express = require("express");

const app = express();

app.get("/", (req, res) => {

    res.json({
        message: "Hello Express.js"
    });

});

app.listen(3000, () => {

    console.log("Server running");

});
```

## 📁 GitHub README checklist

- Create `17_Introduction_Express` folder.
- Create `README.md`.
- Add installation commands.
- Add JavaScript examples.
- Add Mermaid architecture diagrams.
- Add actual images to the `images/` directory if required.
- Check all relative image paths.
- Run the Express server in VS Code.
- Test endpoints using Postman.

Suggested GitHub image references:

```
![Express Architecture](./images/express-architecture.png)

![Express Request Flow](./images/express-request-flow.png)
```

Remember: The actual image files must be committed to GitHub. The interactive 📖 Read and 💡 Important controls are available here in ChatGPT; GitHub will display the Markdown diagrams and images instead.

Chapter 17 completed

You have now created your first Express.js server!

Practice the Student Management Server challenge before moving forward.

When you are ready, type `NEXT` to start:

# Chapter 18 — Express Routing 🚀