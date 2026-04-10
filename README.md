# gin-examples

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

## How to use this repository

Recommended learning method:

1. Start from the first example in the list.
2. Run the example before reading too much code.
3. Focus on understanding the main idea of the example.
4. Make a small modification by yourself.
5. Then move on to the next example.

Do not try to finish every folder immediately.

For most learners:

- the first **10 examples** are enough to get comfortable with Gin
- the first **15 examples** are enough for most small projects
- the first **20 examples** are enough to understand most common Gin use cases

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

- routing
- query parameters
- path parameters
- JSON responses
- form binding
- file binding
- route groups
- middleware
- validation
- graceful shutdown

These topics are enough for building most normal backend services.

## Personal study rules

A simple way to learn from this repository:

- read in order
- run the code
- change something small
- summarize what you learned
- continue to the next example

Examples:

- after reading `basic`, add your own routes
- after reading `form-binding`, create your own request struct
- after reading `group-routes`, organize routes into `/api/v1/...`
- after reading `upload-file`, test file upload manually
- after reading `graceful-shutdown`, understand why production services need it

## After finishing these examples

After the first 10 to 20 examples, try building a small project by yourself, such as:

- a simple REST API service
- a login demo
- a file upload service
- a mini chat server
- a backend project with route groups and middleware

The goal is not to finish every example.

The goal is to become able to build your own Gin project.

## Notes

This repository is mainly for personal learning and practice.

If you also feel the original examples repository is hard to follow, this fork may provide a clearer starting point.
