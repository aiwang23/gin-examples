# gin-examples
[English](README.md)

一个基于官方 [`gin-gonic/examples`](https://github.com/gin-gonic/examples) 仓库整理出来的 Gin 学习路径。

这个仓库 fork 自官方示例仓库，并额外补充了一个更适合初学者的阅读顺序。
原始仓库包含很多小示例项目，但并没有提供一个清晰的学习路线。
这个 fork 的目标，就是把这些零散示例整理成一个更适合循序渐进学习的工作区。

## 为什么要做这个仓库

原始的 `gin-gonic/examples` 仓库确实很有用，但它对初学者来说也容易让人一开始就有点懵，因为里面有很多小文件夹，而且没有明显的学习顺序。

这个仓库适合用来：

- 按步骤学习 Gin
- 降低面对很多示例目录时的混乱感
- 优先关注更常用、更实用的功能
- 把原本零散的示例仓库整理成更清晰的个人学习路径

## 原始仓库

Fork 自：

- [`gin-gonic/examples`](https://github.com/gin-gonic/examples)

## 开始之前

建议你已经具备以下环境或基础：

- 已安装 Go
- 会基本的命令行操作
- 有一个代码编辑器，比如 VS Code
- 有浏览器，或者会使用 `curl` / Postman 之类的接口测试工具

## 安装 Go

先确认你的 Go 是否已经安装：

```bash
go version
````

如果还没有安装 Go，请先通过 Go 官方网站或者系统包管理器安装。

## 克隆这个仓库

```bash
git clone https://github.com/aiwang23/gin-examples.git
cd gin-examples
```

## 安装依赖

这个仓库已经自带 `go.mod`，所以通常你只需要执行：

```bash
go mod tidy
```

或者：

```bash
go mod download
```

## 在你自己的项目里安装 Gin

如果你是想从零开始新建一个自己的 Gin 项目，可以这样做：

```bash
go mod init your-project-name
go get github.com/gin-gonic/gin
```

例如：

```bash
mkdir my-gin-app
cd my-gin-app
go mod init my-gin-app
go get github.com/gin-gonic/gin
```

然后创建一个 `main.go` 文件：

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

运行：

```bash
go run main.go
```

然后打开：

```text
http://localhost:8080/ping
```

## 如何运行本仓库中的示例

大多数示例都可以通过进入对应目录后直接运行。

通用方式：

```bash
cd 示例目录名
go run .
```

或者：

```bash
go run main.go
```

例如：

```bash
cd basic
go run .
```

然后在浏览器中打开终端里显示的本地地址，通常类似于：

```text
http://localhost:8080
```

## 推荐的学习方式

对于每一个示例，建议按下面的顺序来学：

1. 先进入示例目录
2. 先把它跑起来
3. 用浏览器 / curl / Postman 实际测试接口
4. 再去看代码
5. 自己做一点小修改
6. 然后再继续下一个示例

这样会比单纯看很多文件夹代码更有效。

## 用 curl 快速测试

测试服务最简单的方法之一就是 `curl`。

例如：

```bash
curl http://localhost:8080/ping
```

对于 POST 请求，也可以这样测试：

```bash
curl -X POST http://localhost:8080/login \
  -H "Content-Type: application/json" \
  -d '{"user":"tom","password":"123456"}'
```

## 如何使用这个仓库

推荐的学习方法：

1. 从列表里的第一个示例开始
2. 在看太多代码之前，先把示例运行起来
3. 先理解这个示例的核心点
4. 自己做一点小改动
5. 然后再进入下一个示例

不要一开始就试图把所有文件夹一次性学完。

对于大多数学习者来说：

* 前 **10 个示例** 已经足够熟悉 Gin 的基本使用
* 前 **15 个示例** 已经足够应付大多数小型项目
* 前 **20 个示例** 已经足够理解 Gin 最常见的使用场景

## 建议的学习顺序

### 前 5 个示例

1. `basic`
2. `form-binding`
3. `group-routes`
4. `upload-file`
5. `graceful-shutdown`

### 前 10 个示例

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

### 前 15 个示例

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

### 前 20 个示例

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

## 学习 Gin 时建议重点关注的内容

学习 Gin 时，建议重点关注这些核心主题：

* 路由
* 查询参数
* 路径参数
* JSON 响应
* 表单绑定
* 文件绑定
* 路由分组
* 中间件
* 参数校验
* 优雅关闭

这些内容已经足够支撑大多数常规后端服务的开发。

## 个人学习规则

一种简单实用的学习方式：

* 按顺序看
* 把代码跑起来
* 自己改一点东西
* 总结你学到了什么
* 然后继续下一个示例

例如：

* 学完 `basic` 之后，自己加几个路由
* 学完 `form-binding` 之后，自己写一个请求结构体
* 学完 `group-routes` 之后，把路由组织成 `/api/v1/...`
* 学完 `upload-file` 之后，自己手动测试一次文件上传
* 学完 `graceful-shutdown` 之后，理解为什么生产环境需要它

## 初学者常见问题

### 1. `go: command not found`

说明 Go 没有正确安装，或者环境变量 PATH 没有配置好。

### 2. `no required module provides package ...`

可以先执行：

```bash
go mod tidy
```

### 3. 端口被占用

可能是 `8080` 已经被其他程序占用了。
你可以在代码里把端口改掉，例如：

```go
r.Run(":8081")
```

### 4. 不知道该从哪个示例开始

建议直接从下面这几个开始：

* `basic`
* `form-binding`
* `group-routes`
* `upload-file`
* `graceful-shutdown`

这几个作为入门已经非常扎实了。

## 学完这些示例之后做什么

学完前 10 到 20 个示例后，建议你自己动手写一个小项目，例如：

* 一个简单的 REST API 服务
* 一个登录演示
* 一个文件上传服务
* 一个迷你聊天室服务
* 一个带路由分组和中间件的后端项目

目标不是把每一个示例都学完。

目标是让你具备自己写 Gin 项目的能力。

## 说明

这个仓库主要用于个人学习和练习。

如果你也觉得原始的示例仓库不太容易上手，那么这个 fork 也许能给你一个更清晰的起点。
