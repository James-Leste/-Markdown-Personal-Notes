# Deno cheatsheet for Web Software Development Course

## 1. Getting components of request (Deno)
**request body**
The request is sent to `localhost` port 7777 with a pathname `/hello`.
```bash
curl http://localhost:7777/hello
```
```bash
# if you want the method to be specified, use -X
curl -X POST http://localhost:7777
```
- **Request method:** `request.method`, return `GET`, default method is `GET`.
- **Request url:** `request.url`, return `http://localhost:7777/hello`.
- **Full url pathname:** (String) `new URL(request.url).pathname`, return `/hello`. 

**Request with Parameters**
Parameters can be included in either **pathname** or **request body**.

```bash
# request including parameters as pathname
curl "http://localhost:7777?param1=value1&param2=value2"
# request including parameters in request body
# TODO
```
- **Request parameters:** `new URL(request.url).searchParams`, return `URLSearchParams` instance. `get(paramName)`and `getAll()` can be use to retrieve value

Deno example web application
```javascript
const handleRequest = (request) => {
    const url = new URL(request.url); //Full path object
    const pathname = fullPath.pathname; // request path
    const method = request.method; // request method
    const params = url.searchParams; // list of all parameters
    const exampleParam = params.get("example"); // get param value by name

    return new Response(`Full Path: ${request.url}\nPathname: ${pathname}\nMethod: ${method}\nParam: ${exampleParam}`);
};

Deno.serve(handleRequest);
```
## 2. Hono framework
> Hono is a web framework that provides routing, middlewares, and other utilities that help in web development.
> Unlike Deno web applications(`app.js`), those created using Hono have at least one `app.js` and entry point `app-run.js` 

**Example application**
**`app.js`**
```javascript
import { Hono } from "https://deno.land/x/hono@v3.7.4/mod.ts";

const app = new Hono();

app.get("/", (c) => c.text("Hello World!"));
/*
    (c) => c.text("Hello World!")
is the simple way of saying
    (c) => {return c.text("Hello World!");}
*/

export default app;
```
**`app-run.js`**
```javascript
import app from "./app.js";

Deno.serve(app.fetch);
```
**Getting components of a request(Hono)**
`app.js`
```javascript
import { Hono } from "https://deno.land/x/hono@v3.7.4/mod.ts";

const app = new Hono();

app.get("/:id", (c) => {
    // Get request method
    const method = c.req.method;

    // Get '/hello' from 'localhost:8000/hello'
    const path = c.req.path;

    // Get param value by name
    const param1 = c.req.query("param1");

    // Get path param by name
    // In this case, if the request is localhost:8000/1, the value is 1;
    const id = c.req.param("id");

    return c.text("Hello World!");
});

export default app;
```
---
## 3. Serve static files (html, css, js)
**File structure**
```tree
.
├── app.js
└── static
    ├── script.js
    └── index.html
```

**app.js**
```javascript
    import { serve } from "https://deno.land/std@0.202.0/http/server.ts";
    import { serveFile } from "https://deno.land/std@0.202.0/http/file_server.ts";

    const handleRequest = async (request) => {
        const path = new URL(request.url).pathname;
        if (path.includes("js")){
            return await serveFile(request, "static/script.js");
        }
        return await serveFile(request, "static/index.html");
    };

    serve(handleRequest, { port: 7777 });
```
---
## 4. `Deno.dev` deployment
**Deno deploy website**
> A github account is needed to link to the deno account.
> <a href="https://deno.com/deploy">Deno Deploy: https://deno.com/deploy</a>

**Create an empty project & Access token** 

> Every deployment needs a **`project name`** and an **`access token`**.
> A new project can be created on <a href="https://dash.deno.com/projects">dashboard</a>, and a new access token can be created on <a href="https://dash.deno.com/account#access-tokens">access token page</a>.

**Install `deployctl`**

> `deployctl` is a command line tool for deploying software.
> Installation command can be found on its <a href="https://github.com/denoland/deployctl">github page</a>.
> 
**Deployment**
Both `ACCESS_TOKEN` and `PROJECT_NAME` can be either passed directly or stored in environment variables.
```bash
deployctl deploy --token=${ACCESS_TOKEN} --project=${PROJECT_NAME} app-run.js
```
**Update Project**
Deployment using `deployctl` is deploy a preview version by default. If you want to put the latest deployment into production, you can use `--prod` flag.
```bash
deployctl deploy --prod --token=${ACCESS_TOKEN} --project=${PROJECT_NAME} app-run.js
```

---

## 5. `Eta` view template
> Templates (or view templates) are HTML-like pages with places into which data from the server can be injected.

**Eta syntax**
`variable: "<h1>Hello</h1>"` 
When using `<%=`, the html content will be escaped. In this case, the output will be `<h1>Hello</h1>`
```eta
    <%= it.variable %>
```


