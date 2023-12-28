# Deno cheatsheet for Web Software Development Course

## 1. Components of a request
**request body**
The request is sent to `localhost` port 7777 with a pathname `/hello`
```bash
curl http://localhost:7777/hello
```
```bash
# if you want the method to be specified, use -X
curl -X POST http://localhost:7777
```
- **Request method:** `request.method`, return `GET`, default method is `GET`
- **Request url:** `request.url`, return `http://localhost:7777/hello`
- **Full url pathname:** (String) `new URL(request.url).pathname`, return `/hello`  

**Request with Parameters**
Parameters can be included in either **pathname** or **request body**
```bash
# request including parameters as pathname
curl "http://localhost:7777?param1=value1&param2=value2"
# request including parameters in request body
# TODO
```
- **Request parameters:** `new URL(request.url).searchParams`, return `URLSearchParams` instance. `get(paramName)`and `getAll()` can be use to retrieve value

## 2. Serve static files (html, css, js)
**file structure**
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

## 3. `Eta` view template
> Templates (or view templates) are HTML-like pages with places into which data from the server can be injected.

**Eta syntax**
`variable: "<h1>Hello</h1>"` 
When using `<%=`, the html content will be escaped. In this case, the output will be `<h1>Hello</h1>`
```eta
    <%= it.variable %>
```

