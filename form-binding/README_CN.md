# Gin 表单绑定示例

本示例演示了如何在 Go Web 应用中使用 Gin 进行表单数据绑定与校验。
该示例实现了一个简单的预订 API，能够接收表单提交、校验字段，并按照自定义格式解析日期值。

## 功能特点

* 将客户端提交的表单数据绑定到 Go 结构体中
* 使用 Gin 的绑定与校验标签对表单字段进行校验
* 支持按自定义格式解析日期字段
* 以 JSON 形式返回状态和解析后的数据

## 前置要求

* 已安装 [Go](https://golang.org/dl/) 1.13 及以上版本
* 已安装 [Gin](https://github.com/gin-gonic/gin) Web 框架

安装 Gin：

```bash
go get -u github.com/gin-gonic/gin
```

## 工作原理

[`main.go`](main.go) 文件中定义了一个带有表单标签和校验规则的 `Booking` 结构体：

```go
type Booking struct {
    Name     string     `form:"name" binding:"required"`
    CheckIn  *time.Time `form:"check_in" time_format:"2006-01-02" binding:"required"`
    CheckOut *time.Time `form:"check_out" time_format:"2006-01-02"`
}
```

* `form:"..."`：将接收到的表单字段名映射到结构体字段
* `binding:"required"`：表示该字段是必填项，若缺失则绑定失败并返回错误
* `time_format:"..."`：告诉 Gin 按照指定格式将日期字符串解析为 [`time.Time`](https://pkg.go.dev/time#Time)

`/book` 路由接收 POST 请求，将表单数据绑定到 `Booking` 结构体中，并返回 JSON 响应。

## 运行示例

1. 进入 `form-binding` 目录：

   ```bash
   cd form-binding
   ```

2. 运行程序：

   ```bash
   go run main.go
   ```

3. 服务器将启动在 [http://localhost:8080](http://localhost:8080)。

## 使用示例

### 请求

向 `/book` 发送一个带有表单数据的 POST 请求：

```bash
curl -X POST http://localhost:8080/book \
  -d "name=John Doe" \
  -d "check_in=2025-06-21" \
  -d "check_out=2025-06-25"
```

### 成功响应

```json
{
  "name": "John Doe",
  "check_in": "2025-06-21T00:00:00Z",
  "check_out": "2025-06-25T00:00:00Z"
}
```

### 校验失败示例

如果缺少必填字段，例如 `name` 或 `check_in`：

```json
{
  "error": "Key: 'Booking.Name' Error:Field validation for 'Name' failed on the 'required' tag"
}
```

## 关键点

* `ShouldBind` 方法会根据结构体标签自动完成数据绑定和校验
* 如果校验失败，处理函数会返回 HTTP 400 和错误信息
* 日期会按照 `time_format` 中指定的格式进行解析，也就是 `YYYY-MM-DD`

## 参考资料

* [Gin 文档：Binding and Validation](https://gin-gonic.com/docs/examples/binding-and-validation/)
* [Go 文档：time.Time](https://pkg.go.dev/time#Time)


