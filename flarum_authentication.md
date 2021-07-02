# flarum authentication

`authentication` ：身份认证。

一般来说在网页页面上我们使用  `cookie`  和  `session`  来维持页面用户的登录状态，

但是在前后端分离的大趋势下现在基本上都是通过接口的方式来实现前后端的交互。



**Flarum** 论坛程序中身份认证主要关注两个文件：

> session 认证

```json
vendor\flarum\core\src\Http\Middleware\AuthenticateWithSession.php
```



> header 头信息的  `authorization` 字段
>
> 字段值：`Token bgpl1zL4IjpYElVtwESPEvbEdiF7nmcIIKETJ4d3` ，注意 `Token` 后面有个空格

```json
vendor/flarum/core/src/Http/Middleware/AuthenticateWithHeader.php
```



当然 **Flarum** 也提供了身份验证的  `api`  接口

##### 请求类型：

```js
Content-Type: application/json; charset=UTF-8
```

```json
POST /api/token
```



##### 字段说明：

| 字段名         | 字段说明 | 是否必须 | 默认值 |
| -------------- | -------- | -------- | ------ |
| identification | 用户名   | 是       |        |
| password       | 密码     | 是       |        |
| lifetime       | 有效时长 | 否       | 3600s  |

> 当前  `flarum`  版本的  `lifetime`  参数，如果传入大于 3600 的值会有提示性错误。



##### 请求参数示例：

```json
{
"identification":"Toby",
"password":"pass7word"
}
```



##### 响应示例：

```json
{
"token":"YACub2KLfe8mfmHPcUKtt6t2SMJOGPXnZbqhc3nX",
"userId":"1"
}
```

> 没错，这个  `token`  就是用来放在  `header`  头信息里的。



