## tofu-middleware-jwt

JWT (json web token) middleware of tofu
详细参考 https://jwt.io/

### 安装

```lua
-- 在项目配置文件 tofu.package.lua 添加

deps = {

	-- 
	-- 其它配置 ... 
	--
	-- jwt 中间件依赖
	'd80x86/tofu-middleware.jwt',
	{'luarocks', 'cdbattagw/lua-resty-jwt'},

	-- 注:因为有使用到 luarocks 依赖, 所以系统须有 luarocks 环境
}


```
> luarocks 可参其它资料进行安装和使用





```sh
## 使用命令 tofu 安装
./tofu install

```




### 使用

```lua
-- 项目配置文件 conf/middleware.lua

middleware = {
	-- 
	-- .. 其它中间件.. 
	-- ..

	-- 添加jwt中间件配置
	{
		handle = 'resty.tofu.middleware.jwt',
		options = {
				secret = 'jwt secret',
		}
	},

	-- .. 其它中间件.. 
}

```




### 配置options

| 参数名      | 类型     | 说明                                         | 缺省  |
| ----------- | -------- | -------------------------------------------- | ----- |
| secret      | string   | jwt 签名安全码                               |       |
| key         | string   | jwt payload 信息保存在 ngx.ctx.state[key] 中 | user  |
| passthrough | bool     | 如果jwt验证出错，是否续续后面的中间件        | false |
| gettoken    | function | 默认是获取 http header authorization bearer  |       |



jwt 验证错误消息 jwt_obj 保存在 ngx.ctx.state.jwt_error
 
```lua
-- jwt_obj 结构 样列
{
   raw_header  = 'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9',
   raw_payload = 'eyJmb28iOiJiYXIifQ',
   signature   = 'wrong-signature ...',
   header      = {typ='JWT', alg='HS256'},
   payload     = {foo='bar'},
   verified    = false,
   valid       = true,
   reason      = 'signature mismatched: wrong-signature'
}
 
```
> 更多详细 https://github.com/cdbattags/lua-resty-jwt




## 依赖
| 管理     | 包名                    | 链接                                                         |
| -------- | ----------------------- | ------------------------------------------------------------ |
| luarocks | cdbattagw/lua-resty-jwt | [lua-resty-jwt - LuaRocks](https://luarocks.org/modules/cdbattags/lua-resty-jwt) |


