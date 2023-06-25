1. ##### **登陆页面**  

   1. 注册接口
      + 接口路径：<code>/api/status/register</code>  
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{username:string, password: string,email:string}</code>
        - 示例：<code>{
            "username": "root",
            "password": "root",
            "email": "2687335304@qq.com"
          }</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{code: int, msg:string, userid: int}</code>
        - 示例：<code>{"code":200,"msg":"注册成功, 我们已经向您的邮箱发送了一封激活邮件，请尽快激活!, userid: 102"}</code>
      + 注意：
        - 注意：用户以用户名作为id，注册时应进行用户名查重，同时向邮箱发送激活邮件，成功发送返回<code>{"code":200,"msg":"注册成功, 我们已经向您的邮箱发送了一封激活邮件，请尽快激活!"}</code>
   2. 激活用户接口
      + 接口路径：<code>/api/status/activation/{userId}/{code}</code>  
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{userId:int}/{code: string}</code>
        - 示例：<code>{userId:103}/{code:"0f43f336e8bd423fa7ca3fdb5f70b7e6"}</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{code: int,msg:string}</code>
        - 示例：<code>{"code":200,"msg":"激活成功，您的账号已经可以正常使用！"}</code>
      + 注意：
        - 注意：如果激活成功，返回<code>{"code":200,"msg":"激活成功，您的账号已经可以正常使用！"}</code>；如果账号已经被激活过，返回<code>{"code":400,"msg":"无效的操作，您的账号已被激活过！"}</code>；如果经过验证，账号的激活码不正确，则返回<code>{"code":400,"msg":"激活失败，您提供的激活码不正确！"}</code>
   3. 生成验证码接口
      + 路径接口：/api/status/kaptcha
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：null
      + 返回参数：
        - 类型：json 
        - 属性：<code>{code: int,msg:string}</code>
        - 示例：<code>{
          "msg": "图片成功获取",
          "image": "data:image/jpg;base64,iVBORw0KGgoAAAANSUhEUgAAAGQAAAAoCAIAAACHGsgUAAAQgElEQVR4Xu3aZ7QV1RnG8XNDsyv2jhW7omJFRcGKvSC67Iq9N1TsqNh7l4gFG+rCgr2ThJiYbjTBJGIaJtE0S",
          "code": 200
          }</code>
      + 注意：
        - 注意：只有传入正确的response才能生成验证码。
   4. 验证用户输入的图片验证码是否和redis中存入的是否相等接口
      + 路径接口：/api/status/check-kaptcha
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{kaptchaOwner:String,checkCode:String}</code>
        - 示例：<code>{  "kaptchaOwner":"add1457620954263b03bfcb7d60585bd",checkCode:""}</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{code: int,msg: string}</code>
        - 示例：<code>{
          "msg": "未发现输入的图片验证码"}</code>
      + 注意：
        - 注意：会校验图片验证码是否为空、过期和错误，如果没有返回错误信息，证明验证通过。
   5. 用户登录接口
      + 路径接口：/api/status/login
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{
          username: string,
          password: string,
          code: string,
            kaptchaOwner: string }</code>
        - 示例：<code>{
            "username": "root",
            "password": "root",
            "code": "TFY0",
            "kaptchaOwner": "d574025032ff462cb910d879071804d7"
          }</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{code: int,msg:string}</code>
        - 示例：<code>{
          "code": 200,
          "msg": "登录成功"}</code>
      + 注意：
        - 注意：会同时校验用户名和密码，校验成功后，服务端生成ticket，浏览器通过cookie存储ticket
   6. 重置密码接口
      + 路径接口：/api/status/reset-password-verify
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{
          username: string,
          password: string,emailVerifyCode: string
          }</code>
        - 示例：<code>{
            "username": "root",
            "password": "root",
            "emailVerifyCode": "940417"
          }</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{code: int,msg:string}</code>
        - 示例：<code>{
          "code": 200,
          "msg": "重置密码成功！"}</code>
      + 注意：
        - 注意：重置密码需要邮箱验证才能执行重置密码操作
   7. 发送邮件验证码(用于重置密码)接口
      + 路径接口：/api/status/reset-password
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{kaptchaOwner:string,
          kaptchaCode: string,username: string}</code>
        - 示例：<code>{
            "kaptchaOwner":"add1457620954263b03bfcb7d60585bd",
            "kaptchaCode": "CWO3",
            "username": "root"
          }</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{code: int,msg:string}</code>
        - 示例：<code>{
          "code": 200,
          "msg": "已经往您的邮箱发送了一封验证码邮件, 请查收!"}</code>
      + 注意：
        - 注意：requestData里面需包含kaptchaOwner、kaptchaCode、username用于校验
   8. 检查邮件验证码 
      + 路径接口：/api/status/
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{username:String,checkCode:String}</code>
        - 示例：<code>{username:"XXX",checkCode:" "}</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{msg:String}</code>
        - 示例：<code>{
          "msg": "未发现输入的邮件验证码"
          }</code>
      + 注意：
        - 注意：验证成功返回""，失败返回原因