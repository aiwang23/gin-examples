# gin-examples

一个基于官方 [`gin-gonic/examples`](https://github.com/gin-gonic/examples) 仓库整理的 **Gin 学习路径仓库**。

这个仓库 fork 自官方示例仓库，并额外补充了一个更清晰的学习顺序，方便初学者按步骤学习。
原仓库里有很多小示例项目，但缺少一个适合新手的阅读路径。
这个仓库的目的，就是把这些零散的示例整理成一条更适合入门的学习路线。

## 为什么要做这个仓库

官方的 `gin-gonic/examples` 仓库本身很有价值，但对初学者来说也有一个明显问题：

**示例很多，但是不知道应该先看哪个。**

如果直接打开仓库，你会看到很多独立的小项目目录。
它们更像“示例集合”而不是“教程”。
对于已经有经验的人来说，这种结构没有问题；但对于刚开始学 Gin 的人来说，容易看得有点乱。

所以我 fork 了这个仓库，并增加了一个更适合学习的顺序。

这个仓库主要用于：

- 按顺序学习 Gin
- 降低面对大量示例目录时的混乱感
- 优先学习最常用、最核心的功能
- 把官方示例仓库整理成一个更适合个人学习的版本

## 原始仓库

本仓库 fork 自：

- [`gin-gonic/examples`](https://github.com/gin-gonic/examples)

## 这个仓库怎么用

推荐这样学习：

1. 从第一个示例开始
2. 先运行，再读代码
3. 先理解这个示例要解决什么问题
4. 自己动手改一点
5. 然后再进入下一个示例

不要一开始就想着把整个仓库全部看完。

对于大多数学习者来说：

- 前 **10 个示例** 已经足够熟悉 Gin 的基本开发方式
- 前 **15 个示例** 已经足够支撑一般的小项目开发
- 前 **20 个示例** 已经可以覆盖大部分常见的 Gin 使用场景

## 推荐学习顺序

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

## 学习 Gin 时建议重点关注什么

在学习 Gin 的过程中，建议重点关注这些核心内容：

- 路由
- 查询参数
- 路径参数
- JSON 响应
- 表单绑定
- 文件绑定
- 路由分组
- 中间件
- 参数校验
- 优雅退出

这些内容基本已经覆盖了大部分普通后端服务开发的核心需求。

## 一个简单的学习规则

我个人更推荐这样学：

- 按顺序看
- 先运行起来
- 小改一点代码
- 自己总结一下
- 再进入下一个示例

例如：

- 看完 `basic` 后，自己加几个路由
- 看完 `form-binding` 后，自己写一个请求结构体
- 看完 `group-routes` 后，试着把接口组织成 `/api/v1/...`
- 看完 `upload-file` 后，自己实际上传一个文件测试
- 看完 `graceful-shutdown` 后，理解它为什么对生产环境重要

## 看完这些示例之后做什么

当你完成前 10 到 20 个示例之后，最好不要继续只停留在“看示例”阶段，而是自己尝试做一个小项目，比如：

- 一个简单的 REST API 服务
- 一个登录接口示例
- 一个文件上传服务
- 一个简单聊天服务
- 一个带路由分组和中间件的后端项目

学习的重点，不是把所有示例都刷完。

真正的重点是：  
**看完这些示例之后，你能不能自己写出一个 Gin 项目。**

## 说明

这个仓库主要用于个人学习和练习。

如果你也觉得官方 `gin-gonic/examples` 仓库不太容易直接上手，希望先有一个更清晰的阅读顺序，那么这个 fork 版本也许会更适合作为起点。
