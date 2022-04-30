# Nodejs基础
> **Node.js 是一个基于 Chrome V8 引擎 的 JavaScript 运行时环境**
> - 基于 Express 框架，可以快速构建 Web 应用
> - 基于 Electron 框架，可以构建跨平台的桌面应用
> - 基于 restify 框架，可以快速构建 API 接口项目
> - 读写和操作数据库、创建实用的命令行工具辅助前端开发、etc…
> 
> **fs 文件系统模块**
> fs模块是Nodejs官方提供的、用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求，例如：
> `fs.readFile()`方法，用来读取指定文件中的内容
> `fs.writeFile()`方法，用来向指定的文件中写入内容
> 如果要在javascript代码中使用fs模块来操作文件，则需要使用如下的方式先导入它：
```javascript
const fs = require('fs')
```
> 1. `fs.readFile()`的语法格式
> 使用`fs.readFile()`方法，可以读取指定文件中的内容，语法格式如下：
> ```javascript
>    fs.readFile(path[,options],callback)
> ```
>   - 参数解读：
>       - 参数1[path]：必选参数，字符串，表示文件的路径
>       - 参数2[options]：可选参数，表示以什么编码格式来读取文件
>       - 参数3[callback]：必选参数，文件读取完成后，通过回调函数拿到读取的结果
>           - [err]：读取失败返回错误信息，读取成功返回null
>           - [dataStr]：读取的数据，如果未指定编码格式则返回一个 Buffer
> 
> 代码示例：
 ```javascript
 const fs = require('fs')
 fs.readFile('./files/11.text','utf8',function(err,dataStr){
   console.log(err)
   console.log('---')
   console.log(dataStr)
 })
 ```
> 2. `fs.writeFile()`的语法格式
> 使用`fs.writeFile()`方法，可以向指定的文件种写入内容，语法格式如下：
> ```javascript
>    fs.writeFile(file,data[,options],callback)
> ```
> 
>   - 参数解读：
>       - 参数1[file]：必选参数，需要指定一个文件路径的字符串，表示文件的存放路径
>       - 参数2[data]：必选参数，表示要写入的内容
>       - 参数3[options]：可选参数，表示以什么格式写入文件内容，默认值是utf8
>       - 参数4[callback]：回调函数
>
> 代码示例：
 ```javascript
 const fs = require('fs')
 fs.writeFile('./files/2.text','Hello Node.js',function(err){
   console.log(err)
 })
 ```
> 3. 路径动态拼接问题
> - 在使用 fs 模块操作文件时，如果提供的操作路径是以 ./ 或 ../ 开头的相对路径时，容易出现路径动态拼接错误的问题
> - 原因：代码在运行的时候，会以执行 node 命令时所处的目录，动态拼接出被操作文件的完整路径
> - 解决方案：在使用 fs 模块操作文件时，直接提供完整的路径，从而防止路径动态拼接的问题
> - `__dirname` 获取文件所处的绝对路径
```javascript
fs.readFile(__dirname + '/files/1.txt', 'utf8', function(err, data) {
  ...
})
```
> **path 路径模块**
> path 模块是 Node.js 官方提供的、用来处理路径的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理需求。导入：
> ```javascript
> const path = require('path')
> ```
> **http模块**
> http模块是Nodejs官方提供的、用来创建web服务器的模块
> 如果希望使用http模块创建按web服务器，需要先导入它：
> ```javascript
> const http = require('http')
> ```
> 创建基本 Web 服务器:
```javascript
const http = require('http')

// 创建 web 服务器实例
const server = http.createServer()

// 为服务器实例绑定 request 事件，监听客户端的请求
server.on('request', function (req, res) {
  // req.url是客户端请求的url地址
  const url = req.url
  // req.method是客户端请求的method类型
  const method = req.method
  const str = `Your request url is ${url}, and request method is ${method}`
  console.log(str)

  // 设置 Content-Type 响应头，解决中文乱码的问题
  res.setHeader('Content-Type', 'text/html; charset=utf-8')
  // 向客户端响应内容
  res.end(str)
})

server.listen(8080, function () {
  console.log('server running at http://127.0.0.1:8080')
})
```