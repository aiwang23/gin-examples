# basic

A very small Gin example that demonstrates:

- how to start a Gin server
- how to define simple routes
- how to read path parameters
- how to use Basic Authentication
- how to accept JSON data with `POST`
- how to store simple data in memory

This example is good for beginners because it includes both `GET` and `POST` routes, and also shows a simple protected API.

---

## What this example does

This program creates a small HTTP server with three routes:

- `GET /ping`
- `GET /user/:name`
- `POST /admin` (protected by Basic Auth)

It also uses an in-memory map:

```go
var db = make(map[string]string)
````

This means data is only stored while the program is running.
If you stop the server, all data will be lost.

---

## Project structure

This folder contains a single Go file:

* `main.go`

You can run it directly.

---

## Requirements

* Go installed
* Gin installed in your project

---

## How to initialize the project

If you are running this example as a standalone Go project, initialize it like this:

```bash
go mod init basic
go get github.com/gin-gonic/gin
go mod tidy
```

If this folder is already inside a larger Go module, you only need:

```bash
go get github.com/gin-gonic/gin
go mod tidy
```

---

## How to run

Start the server with:

```bash
go run main.go
```

By default, the server listens on:

```text
http://localhost:8080
```

---

## Routes

### 1. Ping test

```http
GET /ping
```

Example:

```bash
curl http://localhost:8080/ping
```

Response:

```text
pong
```

---

### 2. Get user value

```http
GET /user/:name
```

This route reads the `name` from the URL path and checks whether that user has a stored value in the in-memory database.

Example:

```bash
curl http://localhost:8080/user/foo
```

Possible response when value exists:

```json
{
  "user": "foo",
  "value": "bar"
}
```

Possible response when value does not exist:

```json
{
  "user": "foo",
  "status": "no value"
}
```

---

### 3. Admin route with Basic Auth

```http
POST /admin
```

This route is protected by Basic Authentication.

Available accounts:

* `foo` / `bar`
* `manu` / `123`

You must send JSON data like this:

```json
{
  "value": "some text"
}
```

Example:

```bash
curl -X POST http://localhost:8080/admin \
  -u foo:bar \
  -H "Content-Type: application/json" \
  -d '{"value":"hello"}'
```

Response:

```json
{
  "status": "ok"
}
```

After that, you can read the stored value:

```bash
curl http://localhost:8080/user/foo
```

Response:

```json
{
  "user": "foo",
  "value": "hello"
}
```

---

## How the logic works

### `GET /ping`

Used as a quick test route:

```go
r.GET("/ping", func(c *gin.Context) {
	c.String(http.StatusOK, "pong")
})
```

When you visit `/ping`, the server returns plain text:

```text
pong
```

---

### `GET /user/:name`

This route reads the path parameter:

```go
user := c.Params.ByName("name")
```

For example, if the URL is:

```text
/user/foo
```

then `name` is `"foo"`.

The program then checks whether `foo` exists in the map:

```go
value, ok := db[user]
```

* if it exists, return the value
* if it does not exist, return `"no value"`

---

### `POST /admin`

This route is inside an authenticated route group:

```go
authorized := r.Group("/", gin.BasicAuth(gin.Accounts{
	"foo":  "bar",
	"manu": "123",
}))
```

So only users with valid username and password can access it.

Inside the handler:

```go
user := c.MustGet(gin.AuthUserKey).(string)
```

This gets the currently authenticated username.

Then Gin parses the JSON body:

```go
var json struct {
	Value string `json:"value" binding:"required"`
}
```

Example request body:

```json
{
  "value": "hello"
}
```

If parsing succeeds:

```go
db[user] = json.Value
```

That means the value is stored under the authenticated username.

So if you log in as `foo` and send:

```json
{"value":"hello"}
```

then the map becomes roughly:

```go
db["foo"] = "hello"
```

---

## Full example workflow

### Step 1: start the server

```bash
go run main.go
```

### Step 2: test the server

```bash
curl http://localhost:8080/ping
```

### Step 3: try reading a user before storing anything

```bash
curl http://localhost:8080/user/foo
```

Response:

```json
{
  "user": "foo",
  "status": "no value"
}
```

### Step 4: store a value with Basic Auth

```bash
curl -X POST http://localhost:8080/admin \
  -u foo:bar \
  -H "Content-Type: application/json" \
  -d '{"value":"hello"}'
```

### Step 5: read it back

```bash
curl http://localhost:8080/user/foo
```

Response:

```json
{
  "user": "foo",
  "value": "hello"
}
```

---

## Notes

### 1. Data is not persistent

This example uses:

```go
var db = make(map[string]string)
```

So it is only an in-memory store.

When the program stops, all values disappear.

### 2. Basic Auth is only for learning

This example hardcodes usernames and passwords in the source code:

```go
gin.Accounts{
	"foo":  "bar",
	"manu": "123",
}
```

This is fine for learning, but not suitable for a real production system.

### 3. `Bind()` is used here for simplicity

This line:

```go
if c.Bind(&json) == nil {
```

works for this example, but in real projects many developers prefer using more explicit error handling.

---

## Summary

This example teaches the following Gin basics:

* create a router with `gin.Default()`
* define `GET` and `POST` routes
* use path parameters
* return JSON responses
* parse JSON request bodies
* use Basic Authentication
* group protected routes

It is a small but useful beginner example.

---

## Source file

* `main.go`

