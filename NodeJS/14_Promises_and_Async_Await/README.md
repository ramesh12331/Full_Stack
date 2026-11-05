# 🚀 Chapter 14 — Promises and Async/Await in Node.js



Chapter 14

Beginner to Advanced



In this chapter, you will learn how to handle asynchronous operations in Node.js using Promises and Async/Await.

These concepts are very important when working with:

- Database operations
- API requests
- File handling
- User authentication
- Login and registration
- Sending emails
- Backend applications

## 📖 Interactive learning icons

# 📖

Read

Learning guidance

# 💡

Important

Remember this

## 🔑 Requires Before Starting

Before learning this chapter, you should understand:

| Concept              | What you should know                   |
| -------------------- | -------------------------------------- |
| JavaScript functions | How to create and call functions       |
| Callbacks            | Passing a function to another function |
| Synchronous code     | Code that runs step by step            |
| Asynchronous code    | Code that can finish later             |
| `setTimeout()`       | Running code after a delay             |
| `try...catch`        | Handling errors                        |

Quick revision:

A callback is a function passed as an argument to another function.

```
function greet(callback) {
    console.log("Hello");

    callback();
}

function message() {
    console.log("Welcome!");
}

greet(message);
```

Output:

```
Hello
Welcome!
```

Now let's learn a better way to manage asynchronous operations.

# 1. What is a Promise?

A Promise is a JavaScript object that represents the result of an asynchronous operation.

That result may be available:

- Immediately in the future.
- Successfully.
- With an error.

### Simple real-world example

Imagine you order food online.

1. You place an order.
2. The restaurant accepts your order.
3. The food is prepared.
4. The food is delivered.

When you place the order, you don't receive the food immediately.

A Promise works similarly. It represents a result that may arrive later.

### Promise has three states

1\. Pending

Waiting for the result

The asynchronous operation is still running.

2\. Fulfilled

Operation successful

The Promise has successfully completed.

3\. Rejected

Operation failed

The Promise completed with an error.

### Basic syntax

```
const myPromise = new Promise((resolve, reject) => {

    // Asynchronous operation

    resolve("Success");

    // Or use reject("Error");
});
```

- `new Promise()` creates a Promise.
- `resolve()` marks it as successful.
- `reject()` marks it as failed.

💡 Important: A Promise settles only once. Once fulfilled or rejected, its state cannot change.

# 2. Why do we need Promises?

Before Promises, developers commonly used callbacks to handle asynchronous operations.

### Callback example

```
function getData(callback) {

    setTimeout(() => {

        callback("Data received");

    }, 2000);
}

getData((result) => {
    console.log(result);
});
```

This works, but when multiple operations depend on each other, callbacks can become deeply nested.

This problem is called Callback Hell.

### Promise solution

```
function getData() {

    return new Promise((resolve) => {

        setTimeout(() => {
            resolve("Data received");
        }, 2000);

    });
}

getData().then((result) => {
    console.log(result);
});
```

Promises help us:

- Handle asynchronous operations.
- Handle errors using `.catch()`.
- Chain multiple operations.
- Avoid deeply nested callbacks.
- Write cleaner asynchronous code.

# 3. Real-world analogy

Imagine you are applying for a job.

| Real-world situation         | Promise concept |
| ---------------------------- | --------------- |
| Application submitted        | Promise created |
| Waiting for interview result | Pending         |
| Selected                     | Fulfilled       |
| Rejected                     | Rejected        |
| Read the final result        | `.then()`       |
| Handle rejection             | `.catch()`      |
| Perform final cleanup        | `.finally()`    |

The important point: you submit an application now, but the result comes later.

Similarly, a Promise represents a future result.

# 4. Architecture / flow

### Promise execution flow

\#chatgpt-mermaid-\_r_374\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_374\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_374\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_374\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_374\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_374\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_374\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_374\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_374\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_374\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_374\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_374\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_374\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_374\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_374\_ p{margin:0;}#chatgpt-mermaid-\_r_374\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_374\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_374\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_374\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_374\_ .label text,#chatgpt-mermaid-\_r_374\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_374\_ .node rect,#chatgpt-mermaid-\_r_374\_ .node circle,#chatgpt-mermaid-\_r_374\_ .node ellipse,#chatgpt-mermaid-\_r_374\_ .node polygon,#chatgpt-mermaid-\_r_374\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_374\_ .rough-node .label text,#chatgpt-mermaid-\_r_374\_ .node .label text,#chatgpt-mermaid-\_r_374\_ .image-shape .label,#chatgpt-mermaid-\_r_374\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_374\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_374\_ .rough-node .label,#chatgpt-mermaid-\_r_374\_ .node .label,#chatgpt-mermaid-\_r_374\_ .image-shape .label,#chatgpt-mermaid-\_r_374\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_374\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_374\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_374\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_374\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_374\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_374\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_374\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_374\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_374\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_374\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_374\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_374\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_374\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_374\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_374\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_374\_ .icon-shape,#chatgpt-mermaid-\_r_374\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_374\_ .icon-shape p,#chatgpt-mermaid-\_r_374\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_374\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_374\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_374\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_374\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_374\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_374\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_374\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_374\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_374\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_374\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_374\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_374\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_374\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_374\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_374\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_374\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_374\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_374\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_374\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_374\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_374\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_374\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_374\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_374\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_374\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_374\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_374\_ .node rect,#chatgpt-mermaid-\_r_374\_ .node circle,#chatgpt-mermaid-\_r_374\_ .node ellipse,#chatgpt-mermaid-\_r_374\_ .node polygon,#chatgpt-mermaid-\_r_374\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_374\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_374\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_374\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_374\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_374\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Create PromisePendingOperation resultresolve()reject().then().catch().finally()SuccessFailure

### Promise execution example

```
const promise = new Promise((resolve, reject) => {

    const success = true;

    if (success) {
        resolve("Operation successful");
    } else {
        reject("Operation failed");
    }

});

promise
    .then((result) => {
        console.log(result);
    })
    .catch((error) => {
        console.log(error);
    })
    .finally(() => {
        console.log("Operation completed");
    });
```

Output:

```
Operation successful
Operation completed
```

### GitHub README diagram

GitHub supports Mermaid diagrams directly in Markdown.

\#chatgpt-mermaid-\_r_37k\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_37k\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_37k\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_37k\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_37k\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_37k\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_37k\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_37k\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_37k\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_37k\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_37k\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_37k\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_37k\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_37k\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_37k\_ p{margin:0;}#chatgpt-mermaid-\_r_37k\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_37k\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_37k\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_37k\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_37k\_ .label text,#chatgpt-mermaid-\_r_37k\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_37k\_ .node rect,#chatgpt-mermaid-\_r_37k\_ .node circle,#chatgpt-mermaid-\_r_37k\_ .node ellipse,#chatgpt-mermaid-\_r_37k\_ .node polygon,#chatgpt-mermaid-\_r_37k\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_37k\_ .rough-node .label text,#chatgpt-mermaid-\_r_37k\_ .node .label text,#chatgpt-mermaid-\_r_37k\_ .image-shape .label,#chatgpt-mermaid-\_r_37k\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_37k\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_37k\_ .rough-node .label,#chatgpt-mermaid-\_r_37k\_ .node .label,#chatgpt-mermaid-\_r_37k\_ .image-shape .label,#chatgpt-mermaid-\_r_37k\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_37k\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_37k\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_37k\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_37k\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_37k\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_37k\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_37k\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_37k\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_37k\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_37k\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_37k\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_37k\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_37k\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_37k\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_37k\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_37k\_ .icon-shape,#chatgpt-mermaid-\_r_37k\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_37k\_ .icon-shape p,#chatgpt-mermaid-\_r_37k\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_37k\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_37k\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_37k\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_37k\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_37k\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_37k\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_37k\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_37k\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_37k\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_37k\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_37k\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_37k\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_37k\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_37k\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_37k\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_37k\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_37k\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_37k\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_37k\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_37k\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_37k\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_37k\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_37k\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_37k\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_37k\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_37k\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_37k\_ .node rect,#chatgpt-mermaid-\_r_37k\_ .node circle,#chatgpt-mermaid-\_r_37k\_ .node ellipse,#chatgpt-mermaid-\_r_37k\_ .node polygon,#chatgpt-mermaid-\_r_37k\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_37k\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_37k\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_37k\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_37k\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_37k\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Create PromisePendingOperation resultresolverejectthencatchfinallySuccessFailure

Suggested project folder:

```
14_Promises_Async_Await/
│
├── README.md
│
├── 01_promise_intro.js
├── 02_resolve_reject.js
├── 03_then_catch.js
├── 04_finally.js
├── 05_async_await.js
├── 06_try_catch.js
├── 07_sequential.js
├── 08_parallel.js
├── 09_promise_all.js
├── 10_promise_allSettled.js
├── 11_promise_race.js
├── 12_promise_any.js
│
└── images/
    └── promise-flow.png
```

To display an image in your GitHub README, commit the actual image file into your repository and use:

```
![Promise Flow](./images/promise-flow.png)
```

The example image path is a suggested location. The image will appear only after you add the actual image file to GitHub. Mermaid diagrams can be displayed directly without a separate image file.

# 5. Promise syntax

Let's understand the important Promise methods.

### Creating a Promise

```
const promise = new Promise((resolve, reject) => {

    // Operation

});
```

### Resolving a Promise

```
resolve("Success");
```

### Rejecting a Promise

```
reject("Something went wrong");
```

### Handling the result

```
promise
    .then()
    .catch()
    .finally();
```

| Method       | Purpose                          |
| ------------ | -------------------------------- |
| `resolve()`  | Successfully completes a Promise |
| `reject()`   | Fails a Promise                  |
| `.then()`    | Handles successful results       |
| `.catch()`   | Handles errors                   |
| `.finally()` | Runs after the Promise settles   |

# 6. Basic example

Let's create your first Promise.

File: `01_promise_intro.js`

```
// Create a Promise
const myPromise = new Promise((resolve, reject) => {

    // Simulate an asynchronous operation
    setTimeout(() => {

        // Complete successfully
        resolve("Data received successfully!");

    }, 2000);

});

// Handle the Promise result
myPromise.then((result) => {

    console.log(result);

});
```

### What happens?

1. A Promise is created.
2. It starts in the pending state.
3. `setTimeout()` waits for two seconds.
4. `resolve()` completes the Promise successfully.
5. `.then()` receives the result.

Run:

```
node 01_promise_intro.js
```

# 7. Dry run

Let's execute the previous code step by step.

| Step | Execution            | Promise state |
| ---- | -------------------- | ------------- |
| 1    | Create Promise       | Pending       |
| 2    | Start `setTimeout()` | Pending       |
| 3    | Wait for 2 seconds   | Pending       |
| 4    | Call `resolve()`     | Fulfilled     |
| 5    | Execute `.then()`    | Fulfilled     |
| 6    | Print the message    | Fulfilled     |

The output appears after approximately two seconds.

### Try changing the delay

```
setTimeout(() => {
    resolve("Success");
}, 5000);
```

Now the result takes approximately five seconds.

# 8. Output

For the first example:

```
Data received successfully!
```

For a rejected Promise:

```
const myPromise = new Promise((resolve, reject) => {

    reject("Something went wrong!");

});

myPromise
    .then((result) => {
        console.log(result);
    })
    .catch((error) => {
        console.log(error);
    });
```

Output:

```
Something went wrong!
```

# 9. Line-by-line explanation

Let's understand the main Promise methods.

### A. `resolve()`

Used when an operation succeeds.

```
const promise = new Promise((resolve, reject) => {

    resolve("Student registered successfully!");

});
```

### B. `reject()`

Used when an operation fails.

```
const promise = new Promise((resolve, reject) => {

    reject("Registration failed!");

});
```

### C. `.then()`

Receives the successful result.

```
promise.then((result) => {

    console.log(result);

});
```

### D. `.catch()`

Receives the error when the Promise rejects.

```
promise.catch((error) => {

    console.log(error);

});
```

### E. `.finally()`

Runs after the Promise settles, whether it succeeds or fails.

```
promise.finally(() => {

    console.log("Process completed");

});
```

### Complete example

File: `02_resolve_reject.js`

```
const checkResult = new Promise((resolve, reject) => {

    const marks = 75;

    if (marks >= 35) {

        // Promise successful
        resolve("Student passed!");

    } else {

        // Promise failed
        reject("Student failed!");

    }

});

// Handle success
checkResult
    .then((result) => {

        console.log("SUCCESS:", result);

    })

    // Handle error
    .catch((error) => {

        console.log("ERROR:", error);

    })

    // Always execute after settlement
    .finally(() => {

        console.log("Result checking completed");

    });
```

Output:

```
SUCCESS: Student passed!
Result checking completed
```

### F. `async` keyword

The `async` keyword makes a function return a Promise.

```
async function getData() {

    return "Hello Node.js";

}

getData().then((result) => {
    console.log(result);
});
```

Output:

```
Hello Node.js
```

Even though we returned a normal string, an `async` function automatically wraps the returned value in a fulfilled Promise.

### G. `await` keyword

`await` waits for a Promise to settle before continuing inside the async function.

```
function getData() {

    return new Promise((resolve) => {

        setTimeout(() => {
            resolve("Data received");
        }, 2000);

    });

}

async function displayData() {

    const result = await getData();

    console.log(result);

}

displayData();
```

Output after approximately two seconds:

```
Data received
```

💡 Important: Use `await` inside an `async` function. Modern JavaScript also supports top-level `await` in ES modules.

### H. `try...catch`

Use `try...catch` to handle errors when using `await`.

```
async function getUser() {

    try {

        const result = await Promise.reject("User not found");

        console.log(result);

    } catch (error) {

        console.log("Error:", error);

    }

}

getUser();
```

Output:

```
Error: User not found
```

# 10. Practical example

Let's create a small student management example.

Requirement: Get student information asynchronously and display it.

File: `05_async_await.js`

```
// Function that returns student data using a Promise
function getStudent() {

    return new Promise((resolve, reject) => {

        setTimeout(() => {

            const student = {
                id: 101,
                name: "Ramesh",
                course: "Node.js"
            };

            resolve(student);

        }, 2000);

    });

}

// Async function
async function displayStudent() {

    try {

        // Wait for student data
        const student = await getStudent();

        // Display student details
        console.log("Student ID:", student.id);
        console.log("Student Name:", student.name);
        console.log("Course:", student.course);

    } catch (error) {

        console.log("Error:", error);

    }

}

// Call function
displayStudent();
```

Output:

```
Student ID: 101
Student Name: Ramesh
Course: Node.js
```

### How the practical example works

1. `getStudent()` creates a Promise.
2. The Promise waits for two seconds.
3. `resolve(student)` returns student information.
4. `await` waits for the Promise result.
5. The student information is displayed.
6. `catch` handles any error.

## Sequential operations

Sequential means completing one operation before starting the next dependent operation.

Example:

```
function getUser() {

    return new Promise((resolve) => {

        setTimeout(() => {
            resolve("User received");
        }, 1000);

    });

}

function getOrders() {

    return new Promise((resolve) => {

        setTimeout(() => {
            resolve("Orders received");
        }, 1000);

    });

}

async function getUserDetails() {

    const user = await getUser();

    console.log(user);

    const orders = await getOrders();

    console.log(orders);

}

getUserDetails();
```

Output:

```
User received
Orders received
```

The second operation starts only after the first one finishes.

## Parallel operations

Parallel here means starting independent asynchronous operations without waiting for each one to finish before starting the next.

```
function getUser() {

    return new Promise((resolve) => {

        setTimeout(() => {
            resolve("User received");
        }, 2000);

    });

}

function getProducts() {

    return new Promise((resolve) => {

        setTimeout(() => {
            resolve("Products received");
        }, 2000);

    });

}

async function getData() {

    // Start both operations
    const userPromise = getUser();
    const productPromise = getProducts();

    // Wait for both results
    const user = await userPromise;
    const products = await productPromise;

    console.log(user);
    console.log(products);

}

getData();
```

Both operations start immediately. The total waiting time is approximately two seconds, not four seconds.

### Sequential vs Parallel

| Sequential                                            | Parallel                              |
| ----------------------------------------------------- | ------------------------------------- |
| One operation after another                           | Independent operations start together |
| Can take longer                                       | Often faster                          |
| Use when the next task depends on the previous result | Use when tasks are independent        |

# 11. Common mistakes

### Mistake 1 — Forgetting to return a Promise

Wrong

```
function getData() {

    new Promise((resolve) => {
        resolve("Success");
    });

}
```

The function does not return the Promise.

Correct

```
function getData() {

    return new Promise((resolve) => {
        resolve("Success");
    });

}
```

### Mistake 2 — Forgetting `await`

```
async function display() {

    const result = getData();

    console.log(result);

}
```

Here, `result` contains a Promise, not necessarily the resolved value.

Correct:

```
async function display() {

    const result = await getData();

    console.log(result);

}
```

### Mistake 3 — Not handling errors

```
async function getData() {

    const result = await fetchData();

    console.log(result);

}
```

Better:

```
async function getData() {

    try {

        const result = await fetchData();

        console.log(result);

    } catch (error) {

        console.log(error);

    }

}
```

### Mistake 4 — Using `await` without an async function

Incorrect in an ordinary CommonJS script:

```
const result = await getData();
```

Correct:

```
async function main() {

    const result = await getData();

    console.log(result);

}

main();
```

### Mistake 5 — Confusing parallel and sequential operations

Incorrect if the goal is to start both tasks together:

```
const user = await getUser();
const products = await getProducts();
```

Better for independent tasks:

```
const [user, products] = await Promise.all([
    getUser(),
    getProducts()
]);
```

# 12. Best practices

1. Use `async/await` when it makes asynchronous code easier to understand.
2. Handle errors using `try...catch`.
3. Use `Promise.all()` for independent operations when all results are required.
4. Use sequential execution when one operation depends on another.
5. Do not create unnecessary nested Promises.
6. Return Promises from reusable asynchronous functions.
7. Use meaningful function names.
8. Never store passwords or API secrets directly in source code.
9. Use `finally` for cleanup, such as releasing resources.
10. Avoid ignoring rejected Promises.

## Important Promise methods

### `Promise.all()`

Waits for all Promises to fulfill. If one rejects, the returned Promise rejects.

```
const results = await Promise.all([
    getUser(),
    getProducts()
]);
```

### `Promise.allSettled()`

Waits for every Promise to settle, whether fulfilled or rejected.

```
const results = await Promise.allSettled([
    getUser(),
    getProducts()
]);

console.log(results);
```

Example result:

```
[
    { status: "fulfilled", value: "User received" },
    { status: "rejected", reason: "Products failed" }
]
```

### `Promise.race()`

Returns the result of the first Promise that settles, whether fulfilled or rejected.

```
const result = await Promise.race([
    getUser(),
    getProducts()
]);
```

### `Promise.any()`

Returns the first fulfilled result. It ignores rejected Promises unless all of them reject.

```
const result = await Promise.any([
    getUser(),
    getProducts()
]);
```

If all Promises reject, `Promise.any()` rejects with an `AggregateError`.

### Comparison

| Method                 | What happens?               |
| ---------------------- | --------------------------- |
| `Promise.all()`        | All must fulfill            |
| `Promise.allSettled()` | Waits for all to settle     |
| `Promise.race()`       | First settled result wins   |
| `Promise.any()`        | First fulfilled result wins |

## Visual comparison for GitHub

\#chatgpt-mermaid-\_r_3ei\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_3ei\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_3ei\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_3ei\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_3ei\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3ei\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_3ei\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_3ei\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_3ei\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_3ei\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_3ei\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_3ei\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3ei\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3ei\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_3ei\_ p{margin:0;}#chatgpt-mermaid-\_r_3ei\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3ei\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3ei\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3ei\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_3ei\_ .label text,#chatgpt-mermaid-\_r_3ei\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3ei\_ .node rect,#chatgpt-mermaid-\_r_3ei\_ .node circle,#chatgpt-mermaid-\_r_3ei\_ .node ellipse,#chatgpt-mermaid-\_r_3ei\_ .node polygon,#chatgpt-mermaid-\_r_3ei\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_3ei\_ .rough-node .label text,#chatgpt-mermaid-\_r_3ei\_ .node .label text,#chatgpt-mermaid-\_r_3ei\_ .image-shape .label,#chatgpt-mermaid-\_r_3ei\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_3ei\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_3ei\_ .rough-node .label,#chatgpt-mermaid-\_r_3ei\_ .node .label,#chatgpt-mermaid-\_r_3ei\_ .image-shape .label,#chatgpt-mermaid-\_r_3ei\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_3ei\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_3ei\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3ei\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3ei\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_3ei\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_3ei\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_3ei\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_3ei\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_3ei\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_3ei\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_3ei\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3ei\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3ei\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_3ei\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_3ei\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_3ei\_ .icon-shape,#chatgpt-mermaid-\_r_3ei\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_3ei\_ .icon-shape p,#chatgpt-mermaid-\_r_3ei\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_3ei\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_3ei\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_3ei\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_3ei\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_3ei\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_3ei\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_3ei\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_3ei\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_3ei\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3ei\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_3ei\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_3ei\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_3ei\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3ei\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_3ei\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_3ei\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3ei\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_3ei\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_3ei\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3ei\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_3ei\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_3ei\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_3ei\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_3ei\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_3ei\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_3ei\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_3ei\_ .node rect,#chatgpt-mermaid-\_r_3ei\_ .node circle,#chatgpt-mermaid-\_r_3ei\_ .node ellipse,#chatgpt-mermaid-\_r_3ei\_ .node polygon,#chatgpt-mermaid-\_r_3ei\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_3ei\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_3ei\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_3ei\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_3ei\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_3ei\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Start multiple PromisesWhich method?Promise.allPromise.allSettledPromise.racePromise.anyAll must fulfillWait for all outcomesFirst settledFirst fulfilled

### GitHub image reference

If you create a comparison image and commit it to your repository:

```
![Promise Methods](./images/promise-methods.png)
```

# 13. Interview questions

### Beginner level

Q1. What is a Promise?

A Promise is a JavaScript object representing the eventual success or failure of an asynchronous operation.

Q2. What are the three states of a Promise?

- Pending
- Fulfilled
- Rejected

Q3. What is `resolve()`?

It fulfills a Promise with a value.

Q4. What is `reject()`?

It rejects a Promise with a reason or error.

Q5. What is `.then()`?

It handles a fulfilled Promise and returns another Promise.

### Intermediate level

Q6. What is the difference between `.then()` and `.catch()`?

`.then()` handles successful results, while `.catch()` handles rejections.

Q7. What is async/await?

It is syntax for working with Promises in a more readable way.

Q8. Why do we use try/catch?

To handle errors from awaited operations.

Q9. What is the difference between sequential and parallel execution?

Sequential operations run one after another. Parallel operations start independently without waiting for one another.

### Advanced level

Q10. What is the difference between Promise.all() and Promise.allSettled()?

`Promise.all()` rejects as soon as one input rejects. `Promise.allSettled()` waits for all inputs to settle and returns their individual outcomes.

Q11. What is the difference between Promise.race() and Promise.any()?

`race()` returns the first settled result. `any()` returns the first fulfilled result.

Q12. Does async always return a Promise?

Yes. An async function always returns a Promise.

Q13. Does await block the entire Node.js application?

No. It pauses the execution of the surrounding async function while the Promise settles. Other JavaScript work can continue through the event loop.

# 14. Practice problems

Try these problems in VS Code.

Your practice checklist

0/7 completed

Problem 1: Create a Promise that returns the message 'Hello Node.js'.

💡 Show hint

Problem 2: Create a Promise that rejects with 'Login failed'.

💡 Show hint

Problem 3: Use setTimeout() to return student data after 3 seconds.

💡 Show hint

Problem 4: Create an async function that waits for a Promise and displays its result.

💡 Show hint

Problem 5: Use try/catch to handle a rejected Promise.

💡 Show hint

Problem 6: Run three independent Promises using Promise.all().

💡 Show hint

Problem 7: Use Promise.allSettled() with one fulfilled and one rejected Promise.

💡 Show hint

# 15. Mini challenge — Student Result System

Practical challenge

Create a Student Result System using Promises and Async/Await.

### Requirements

1. Create a `getStudent()` function.
2. Return student details using a Promise.
3. Use `setTimeout()` to simulate a database request.
4. Use `async/await` to receive the student data.
5. Use `try...catch` to handle errors.
6. Display the student's name, marks and result.

### Expected output

```
Student Name: Ramesh
Marks: 85
Result: Passed
```

### Starter code

```
function getStudent() {

    return new Promise((resolve, reject) => {

        // Your code here

    });

}

async function displayStudent() {

    try {

        // Your code here

    } catch (error) {

        console.log(error);

    }

}

displayStudent();
```

Try to complete this challenge yourself before checking any solution.

# 16. Chapter summary

| Topic                | Important point                              |
| -------------------- | -------------------------------------------- |
| Promise              | Represents a future result                   |
| Pending              | Operation is waiting                         |
| Fulfilled            | Operation succeeded                          |
| Rejected             | Operation failed                             |
| resolve()            | Fulfills a Promise                           |
| reject()             | Rejects a Promise                            |
| then()               | Handles success                              |
| catch()              | Handles errors                               |
| finally()            | Runs after settlement                        |
| async                | Function returns a Promise                   |
| await                | Waits for a Promise inside an async function |
| try/catch            | Handles errors                               |
| Promise.all()        | All inputs must fulfill                      |
| Promise.allSettled() | Waits for all outcomes                       |
| Promise.race()       | First settled result                         |
| Promise.any()        | First fulfilled result                       |

# 17. Quick revision

Remember these five points:

1. Promise handles asynchronous operations.
2. Promise has three states: Pending, Fulfilled and Rejected.
3. Use `.then()` and `.catch()` to handle results.
4. Use `async/await` to write cleaner asynchronous code.
5. Use `Promise.all()` for independent operations that need all results.

Important syntax

```
async function main() {

    try {

        const result = await getData();

        console.log(result);

    } catch (error) {

        console.log(error);

    }

}

main();
```

## 📁 GitHub README checklist

Before pushing this chapter to GitHub:

- Create `14_Promises_Async_Await` folder.
- Add the JavaScript example files.
- Create `README.md`.
- Add the Mermaid diagrams.
- Add actual image files inside `images/` if using image references.
- Check that all relative image paths are correct.
- Run every JavaScript example in VS Code.

Chapter 14 completed

Stop here. Practice the examples and mini challenge. When you are ready, type `NEXT` to start Chapter 15 — HTTP Fundamentals.