# Bloggist - API 设计说明文档

> 前后端交互的简明 API v1 如下，学习采用 RESTful 风格。
>
> 初代的简单用户认证使用 jwt 提供的 Token 生成与验证功能实现，具体使用为：
>
> - 前端获取用户登录信息返回后端，后端通过用户名密码验证可登陆后，发送用户特异的 Token 给前端保存；
> - 前端后续该用户操作下的所有请求，在 url 后拼接 token 参数，供后端 query 后验证；
> - 后端每次处理请求，先验证 token 合法 - 用户通过校验，方开始处理请求；
> - 前端请求 url 示例：`/api/user/someusername/blogs?token=blahblah`
>
> 出于自己设计 API 并发现思路欠妥之处的想法，设计时我们没有使用 API 相关工具，而是自行商讨设计，是不足必然出现的原因，但也真实记录下来。初代 API 中，存在许多不足，有待改进：
>
> - 后端状态码的对应返回不规范；
> - 后端获取状态应该有更多信息说明；
> - 应考虑更多 HTTP 动作的运用：PUT、DELETE 等；

### 用户相关

#### 用户注册

**`POST: /api/register`**

##### Request

```json
{
  "username": "<username gotten>",
  "password": "<password gotten>"
}
```

##### Response

###### 注册成功（无重复用户名 && 格式合法 && ……）

```json
{
  "status": "success"
}
```

###### 注册失败（ErrorMsg）

```json
{
  "status": "fail",
  "err_msg": "<message: duplicate name, invalid string...>"
}
```



#### 用户登陆

**`POST: /api/login`**

##### Request

```json
{
  "username": "<username gotten>",
  "password": "<password gotten>"
}
```

##### Response

###### 返回登陆情况

```json
{
  "status": "success",
  "blog_num": "<number of blogs>",           // 用户发表过的博客数
  "liked_num": "<number of likes received>", // 用户收到的总点赞数
  "token_string": "<user specific token generate by jwt>"
}
```



---

### 博客相关

#### 用户发表博客

**`POST: /api/user/:username/publish`**

##### Request

```json
{
  "title": "<blog_title>",
  "content": "<blog_content>"
}
```

##### Response

###### 发布成功

```json
{
  "status": "success",
  "blogid": "id of the published blog"
}
```



#### 获取用户博客列表

**`GET: /api/user/:username/blogs`**

##### Request

GET Request with token attached

##### Response

###### 返回获取情况

```json
{
  "status": "success",
  "blogs": ["title1", "title2", "title3", "..."], // 用户发表过的博客标题列表
  "blog_ids": ["id1", "id2", "id3", "..."],       // 博客对应的后台唯一性ID
  "liked": ["liked1", "liked2", "liked3", "..."]  // 对应博客获得的点赞数
}
```



#### 获取用户博客

**`GET: /api/user/:username/blog/:blogid`**

##### Request

GET Request with token attached

##### Response

###### 返回获取情况

```json
{
  "status": "success",
  "title": "<blog_title>",
  "content": "<blog_content>",
  "liked": "<blog_liked_number>"
}
```



#### 用户点赞博客

**`GET: /api/user/:username/blogs/:blogid/like`**

##### Request

GET Request with token attached

##### Response

###### 返回获赞后数据更新情况

```json
{
  "status": "success",
  "liked": "<number of likes received>" // 反馈实时赞数
}
```


