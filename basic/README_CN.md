# basic

这是一个非常小的 Gin 示例，用来演示：

- 如何启动一个 Gin 服务器
- 如何定义简单路由
- 如何读取路径参数
- 如何使用 Basic Authentication（基础认证）
- 如何接收 `POST` 请求中的 JSON 数据
- 如何把简单数据存到内存中

这个示例很适合初学者，因为它同时包含了 `GET` 和 `POST` 路由，也展示了一个最基础的受保护接口。

---

## 这个示例做了什么

这个程序创建了一个简单的 HTTP 服务器，包含三个路由：

- `GET /ping`
- `GET /user/:name`
- `POST /admin`（受 Basic Auth 保护）

它还使用了一个内存中的 map：

```go
var db = make(map[string]string)
````

这意味着数据只会在程序运行期间存在。
只要服务器停止，数据就会丢失。

---

## 项目结构

这个文件夹里只有一个 Go 文件：

* `main.go`

你可以直接运行它。

---

## 环境要求

* 已安装 Go
* 当前项目已经安装 Gin

---

## 如何初始化项目

如果你把这个示例当作一个独立 Go 项目来运行，可以这样初始化：

```bash
go mod init basic
go get github.com/gin-gonic/gin
go mod tidy
```

如果这个目录已经在一个更大的 Go module 里面了，那你一般只需要执行：

```bash
go get github.com/gin-gonic/gin
go mod tidy
```

---

## 如何运行

使用下面的命令启动服务：

```bash
go run main.go
```

默认监听地址是：

```text
http://localhost:8080
```

---

## 路由说明

### 1. Ping 测试接口

```http
GET /ping
```

示例：

```bash
curl http://localhost:8080/ping
```

返回：

```text
pong
```

---

### 2. 获取用户对应的值

```http
GET /user/:name
```

这个接口会从 URL 路径中读取 `name`，然后去内存数据库中查找这个用户是否有对应的值。

示例：

```bash
curl http://localhost:8080/user/foo
```

当值存在时，可能返回：

```json
{
  "user": "foo",
  "value": "bar"
}
```

当值不存在时，可能返回：

```json
{
  "user": "foo",
  "status": "no value"
}
```

---

### 3. 带 Basic Auth 的管理接口

```http
POST /admin
```

这个接口受 Basic Authentication 保护。

可用账号如下：

* `foo` / `bar`
* `manu` / `123`

你必须发送如下 JSON 数据：

```json
{
  "value": "some text"
}
```

示例：

```bash
curl -X POST http://localhost:8080/admin \
  -u foo:bar \
  -H "Content-Type: application/json" \
  -d '{"value":"hello"}'
```

返回：

```json
{
  "status": "ok"
}
```

之后你就可以读取这个用户保存的值：

```bash
curl http://localhost:8080/user/foo
```

返回：

```json
{
  "user": "foo",
  "value": "hello"
}
```

---

## 代码逻辑说明

### `GET /ping`

这是一个最简单的测试路由：

```go
r.GET("/ping", func(c *gin.Context) {
	c.String(http.StatusOK, "pong")
})
```

当你访问 `/ping` 时，服务器会返回纯文本：

```text
pong
```

---

### `GET /user/:name`

这个路由会先读取路径参数：

```go
user := c.Params.ByName("name")
```

例如如果 URL 是：

```text
/user/foo
```

那么 `name` 的值就是 `"foo"`。

然后程序会检查 `foo` 是否存在于 map 中：

```go
value, ok := db[user]
```

* 如果存在，就返回对应值
* 如果不存在，就返回 `"no value"`

---

### `POST /admin`

这个路由放在一个带认证的路由组中：

```go
authorized := r.Group("/", gin.BasicAuth(gin.Accounts{
	"foo":  "bar",
	"manu": "123",
}))
```

所以只有用户名和密码正确时才能访问。

在处理函数里：

```go
user := c.MustGet(gin.AuthUserKey).(string)
```

这行代码会拿到当前已经认证通过的用户名。

接着 Gin 会解析请求体中的 JSON：

```go
var json struct {
	Value string `json:"value" binding:"required"`
}
```

例如请求体：

```json
{
  "value": "hello"
}
```

如果解析成功，就会执行：

```go
db[user] = json.Value
```

这表示把这个值存到当前认证用户对应的位置。

所以如果你是用 `foo` 登录，然后发送：

```json
{"value":"hello"}
```

那么 map 大致就会变成：

```go
db["foo"] = "hello"
```

---

## 完整使用流程

### 第一步：启动服务

```bash
go run main.go
```

### 第二步：测试服务是否正常

```bash
curl http://localhost:8080/ping
```

### 第三步：在未保存任何值之前读取用户数据

```bash
curl http://localhost:8080/user/foo
```

返回：

```json
{
  "user": "foo",
  "status": "no value"
}
```

### 第四步：使用 Basic Auth 保存一个值

```bash
curl -X POST http://localhost:8080/admin \
  -u foo:bar \
  -H "Content-Type: application/json" \
  -d '{"value":"hello"}'
```

### 第五步：再把它读出来

```bash
curl http://localhost:8080/user/foo
```

返回：

```json
{
  "user": "foo",
  "value": "hello"
}
```

---

## 注意事项

### 1. 数据不会持久化

这个示例使用的是：

```go
var db = make(map[string]string)
```

所以它只是一个内存存储。

程序退出后，里面的数据就全部消失了。

### 2. Basic Auth 这里只是教学用途

这个例子把用户名和密码直接写死在源码里：

```go
gin.Accounts{
	"foo":  "bar",
	"manu": "123",
}
```

这对于学习来说没问题，但不适合真实生产环境。

### 3. 这里使用 `Bind()` 只是为了简单

这一行：

```go
if c.Bind(&json) == nil {
```

在这个示例里可以正常工作，但在真实项目中，很多开发者会更喜欢写得更明确一点，把错误处理分开写清楚。

---

## 总结

这个示例主要帮助你掌握以下 Gin 基础知识：

* 使用 `gin.Default()` 创建路由器
* 定义 `GET` 和 `POST` 路由
* 使用路径参数
* 返回 JSON 响应
* 解析 JSON 请求体
* 使用 Basic Authentication
* 对受保护路由进行分组

这是一个很小，但非常实用的入门示例。

---

## 源码文件

* `main.go`


