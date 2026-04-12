# gin-examples
[中文](README_CN.md)

A personal learning path for Gin, based on the official [`gin-gonic/examples`](https://github.com/gin-gonic/examples) repository.

This repository is a fork of the original examples repo, with an added reading order to make learning easier for beginners.
The original repository contains many small example projects, but it does not provide a clear study path.
This fork is meant to turn that collection into a more structured learning workspace.

## Why this repository

The original `gin-gonic/examples` repository is useful, but it can feel overwhelming at first because there are many small example folders and no obvious order to follow.

This repository is for:

- learning Gin step by step
- reducing confusion when facing many example folders
- focusing on practical and commonly used features first
- turning the original examples collection into a clearer personal study path

## Original repository

Forked from:

- [`gin-gonic/examples`](https://github.com/gin-gonic/examples)

## Before you start

You should already have:

- Go installed
- basic command line usage
- a code editor such as VS Code
- a browser or API tool such as `curl` / Postman for testing

## Install Go

First, make sure Go is installed:

```bash
go version
````

If Go is not installed yet, install it first from the official Go website or your package manager.

## Clone this repository

```bash
git clone https://github.com/aiwang23/gin-examples.git
cd gin-examples
```

## Install dependencies

This repository already contains `go.mod`, so you usually only need:

```bash
go mod tidy
```

or:

```bash
go mod download
```

## Install Gin in your own project

If you are creating your own Gin project from scratch, use:

```bash
go mod init your-project-name
go get github.com/gin-gonic/gin
```

Example:

```bash
mkdir my-gin-app
cd my-gin-app
go mod init my-gin-app
go get github.com/gin-gonic/gin
```

Then create a `main.go` file:

```go
package main

import "github.com/gin-gonic/gin"

func main() {
    r := gin.Default()

    r.GET("/ping", func(c *gin.Context) {
        c.JSON(200, gin.H{
            "message": "pong",
        })
    })

    r.Run(":8080")
}
```

Run it with:

```bash
go run main.go
```

Open:

```text
http://localhost:8080/ping
```

## How to run examples in this repository

Most examples can be run by entering the example folder and starting its main file.

General pattern:

```bash
cd example-folder
go run .
```

or:

```bash
go run main.go
```

Example:

```bash
cd basic
go run .
```

Then open the local address shown in the terminal, usually something like:

```text
http://localhost:8080
```

## Recommended way to study each example

For each example, follow this order:

1. enter the folder
2. run it first
3. test the endpoint in browser / curl / Postman
4. read the code
5. change something small by yourself
6. move to the next example

This is much better than reading many folders without running them.

## Quick test with curl

A simple way to test your server:

```bash
curl http://localhost:8080/ping
```

For POST requests, you can do things like:

```bash
curl -X POST http://localhost:8080/login \
  -H "Content-Type: application/json" \
  -d '{"user":"tom","password":"123456"}'
```

## How to use this repository

Recommended learning method:

1. Start from the first example in the list.
2. Run the example before reading too much code.
3. Focus on understanding the main idea of the example.
4. Make a small modification by yourself.
5. Then move on to the next example.

Do not try to finish every folder immediately.

For most learners:

* the first **10 examples** are enough to get comfortable with Gin
* the first **15 examples** are enough for most small projects
* the first **20 examples** are enough to understand most common Gin use cases

## Suggested learning order

### First 5 examples

1. `basic`
2. `form-binding`
3. `group-routes`
4. `upload-file`
5. `graceful-shutdown`

### First 10 examples

1. `basic`
2. `form-binding`
3. `file-binding`
4. `group-routes`
5. `versioning`
6. `upload-file`
7. `cookie`
8. `cors-middleware`
9. `graceful-shutdown`
10. `websocket`

### First 15 examples

1. `basic`
2. `form-binding`
3. `file-binding`
4. `group-routes`
5. `versioning`
6. `upload-file`
7. `cookie`
8. `custom-validation`
9. `struct-lvl-validations`
10. `cors-middleware`
11. `graceful-shutdown`
12. `template`
13. `websocket`
14. `server-sent-event`
15. `ratelimiter`

### First 20 examples

1. `basic`
2. `form-binding`
3. `file-binding`
4. `group-routes`
5. `versioning`
6. `upload-file`
7. `cookie`
8. `custom-validation`
9. `struct-lvl-validations`
10. `cors-middleware`
11. `graceful-shutdown`
12. `template`
13. `server-sent-event`
14. `send_chunked_data`
15. `websocket`
16. `realtime-chat`
17. `realtime-advanced`
18. `ratelimiter`
19. `reverse-proxy`
20. `multiple-service`

## Recommended focus areas

When learning Gin, pay attention to these core topics:

* routing
* query parameters
* path parameters
* JSON responses
* form binding
* file binding
* route groups
* middleware
* validation
* graceful shutdown

These topics are enough for building most normal backend services.

## Personal study rules

A simple way to learn from this repository:

* read in order
* run the code
* change something small
* summarize what you learned
* continue to the next example

Examples:

* after reading `basic`, add your own routes
* after reading `form-binding`, create your own request struct
* after reading `group-routes`, organize routes into `/api/v1/...`
* after reading `upload-file`, test file upload manually
* after reading `graceful-shutdown`, understand why production services need it

## Common beginner problems

### 1. `go: command not found`

Go is not installed correctly, or PATH is not configured.

### 2. `no required module provides package ...`

Run:

```bash
go mod tidy
```

### 3. Port already in use

Maybe port `8080` is already occupied by another program.
Change the port in code, for example:

```go
r.Run(":8081")
```

### 4. Not sure which example to start with

Start with:

* `basic`
* `form-binding`
* `group-routes`
* `upload-file`
* `graceful-shutdown`

That is enough for a very solid beginning.

## After finishing these examples

After the first 10 to 20 examples, try building a small project by yourself, such as:

* a simple REST API service
* a login demo
* a file upload service
* a mini chat server
* a backend project with route groups and middleware

The goal is not to finish every example.

The goal is to become able to build your own Gin project.

## Notes

This repository is mainly for personal learning and practice.

If you also feel the original examples repository is hard to follow, this fork may provide a clearer starting point.
