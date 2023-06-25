### 前后端交互接口文档 ###

------



1. ##### **登陆页面**  #####

   1. 注册接口
      + 接口路径：<code>/api/status/register</code>  
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{name:string, passwd: string}</code>
        - 示例：<code>{name:'xxx', passwd: 'xxx'}</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{code: state code,msg:"是否注册成功"}</code>
        - 示例：<code>{"code":200,"msg":"注册成功, 我们已经向您的邮箱发送了一封激活邮件，请尽快激活!"}</code>
      + 注意：
        - 注意：用户以用户名作为id，注册时应进行用户名查重，同时向邮箱发送激活邮件，成功发送返回<code>{"code":200,"msg":"注册成功, 我们已经向您的邮箱发送了一封激活邮件，请尽快激活!"}</code>
   2. 激活用户接口
      + 接口路径：<code>/api/status/activation/{userId}/{code}</code>  
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{userId:int}/{code: string}</code>
        - 示例：<code>{userId:XXX}/{code: XXX}</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{code: state code,msg:"是否激活成功"}</code>
        - 示例：<code>{"code":200,"msg":"激活成功，您的账号已经可以正常使用！"}</code>
      + 注意：
        - 注意：如果激活成功，返回<code>{"code":200,"msg":"激活成功，您的账号已经可以正常使用！"}</code>；如果账号已经被激活过，返回<code>{"code":400,"msg":"无效的操作，您的账号已被激活过！"}</code>；如果经过验证，账号的激活码不正确，则返回<code>{"code":400,"msg":"激活失败，您提供的激活码不正确！"}</code>
   3. 生成验证码接口
      + 路径接口：/api/status/kaptcha
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{response:HttpServletResponse}</code>
        - 示例：<code>{response:XXX}</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{code: state code,msg:"是否激活成功"}</code>
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
        - **示例：<code>{kaptchaOwner:String,checkCode:String}</code>**
      + 返回参数：
        - 类型：json 
        - 属性：<code>{code: state code,msg:"是否激活成功"}</code>
        - 示例：<code>{
            "msg": "未发现输入的图片验证码"}</code>
      + 注意：
        - 注意：会校验图片验证码是否为空、过期和错误，如果没有返回错误信息，证明验证通过。
   5. 用户登录接口
      + 路径接口：/api/status/login
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{loginData:Map<String, String>,response:HttpServletResponse}</code>
        - **示例：<code>{loginData:Map<String, String>,response:HttpServletResponse}</code>**
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
        - 属性：<code>{requestData:Map<String, Object>}</code>
        - **示例：<code>{requestData:Map<String, Object>}</code>**
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
        - 属性：<code>{requestData:Map<String, Object>}</code>
        - **示例：<code>{requestData:Map<String, Object>}</code>**
      + 返回参数：
        - 类型：json 
        - 属性：<code>{code: int,msg:string}</code>
        - 示例：<code>{
            "code": 200,
            "msg": "已经往您的邮箱发送了一封验证码邮件, 请查收!"}</code>
      + 注意：
        - 注意：requestData里面需包含kaptchaOwner、kaptchaCode、username用于校验
   8. **检查邮件验证码 **
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

2. ##### **用户页面**  #####

   1. 账号设置界面接口
      + 路径接口：<code>/user/setting</code>  
      + 请求参数：
        - 类型：json 
        - 方法：get
        - **属性：null**
        - 示例：null
      + 返回参数：
        - 类型：json 
        - 属性：<code>{response: Map<string, Object>}</code>
        - **示例：<code>{response: Map<string, Object>}</code>**
        - 注意：需要与七牛云的账号交互
   2. 更新图像路径接口
      + 路径接口：<code>/user/header/url</code>  
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{fileName:string}</code>
        - 示例：<code>{fileName:"file"}</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{code: int,msg:string}</code>
        - 示例：<code>{
            "code": 200,
            "msg": "更新成功"}</code>
        - 注意：是将本地的图像路径更新为云服务器上的图像路径
   3. 修改用户密码接口
      + 路径接口：<code>/user/password</code>  
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{oldPassword: string,newPassword: string}</code>
        - 示例：<code>{oldPassword: "aaaa",newPassword: "bbbb"}</code>
        - 注意：新密码与原密码不能相同，且会校验原密码是否输入正确
      + 返回参数：
        - 类型：json 
        - 属性：<code>{code: int,msg:string}</code>
        - 示例：<code>{
            "code": 200,
            "msg": "修改成功"}</code>
   4. 个人主页接口
      + 路径接口：<code>/user/profile/{userId}</code>  
      + 请求参数：
        - 类型：json 
        - 方法：get
        - 属性：<code>{userId: int}</code>
        - 示例：<code>{userId: 1}</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{code: int,msg:string}</code>
        - 示例：<code>{
            "code": 200,
            "msg": "操作成功"}</code>
   5. 查询某个用户的帖子列表接口
      + 路径接口：<code>/user/discuss/{userId}/{page}</code>  
      + 请求参数：
        - 类型：json 
        - 方法：get
        - 属性：<code>{userId: int,page: int}</code>
        - 示例：<code>{userId: 1,page:1}</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{code: int,msg:string,response Map<String, Object>}</code>
        - **示例：<code>{code: int,msg:string,response Map<String, Object>}</code>**
   6. 查询某个用户的评论/回复列表接口
      + 路径接口：<code>/user/comment/{userId}</code>  
      + 请求参数：
        - 类型：json 
        - 方法：get
        - 属性：<code>{userId: int,page: int}</code>
        - 示例：<code>{userId: 1,page:1}</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{code: int,msg:string,response Map<String, Object>}</code>
        - **示例：<code>{code: int,msg:string,response Map<String, Object>}</code>**

3. ##### **首页**  #####

  1. 首页接口
      + 路径接口：<code>/api/posts/{page}</code>  
      + 请求参数：
        - 类型：json 
        - 方法：get
        - 属性：<code>{orderMode:int, page:int}</code>
        - 示例：<code>{ page:1}</code>
        - 注意：orderMode参数是可选的
      + 返回参数：
        - 类型：json 
        - 属性：<code>{
          msg: string,
       code: int,
          orderMode: int,discussPosts: [],
       page_cnt:int,
          page_current:int
          }</code>
        - 示例：<code>{
            "msg": "获取成功",
            "code": 200,
            "orderMode": 0,
            "discussPosts": [],
            "page_cnt": 0,
            "page_current": 0
          }</code>      
  
4. **帖子**  
  1. 更新帖子接口
      + 路径接口：<code>/api/discuss/uploadMdPic</code>  
         + 请求参数：
           - 类型：json 
           - 方法：post
           - 属性：<code>{file:MultipartFile}</code>
           - 示例：<code>{file:null}</code>
         + 返回参数：
           - 类型：json 
           - 属性：<code>{success: int,message:string}</code>
           - 示例：{"success":0,"message":"上传失败"}
  2. 发布帖子接口
      + 路径接口：<code>/api/discuss/add</code>  
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{
          title: string,
          content: string
          }</code>
        - 示例：<code>{
            "title": "test",
            "content": "test"
          }</code>
      + 返回参数：
        - 类型：json
        - 属性：<code>{code: int,msg:string}</code>
        - 示例：<code>{"msg":"发布成功","code":0}</code>
  3. 获取帖子详情接口
   + 路径接口：<code>/api/discuss/detail/{discussPostId}</code>  
      + 请求参数：
        - 类型：json 
        - 方法：get
        - 属性：<code>{discussPostId: int}</code>
        - 示例：<code>{discussPostId: 1}</code>
      + 返回参数：
        - 类型：json
        - 属性：<code>{
          msg: string,
          code: int,
          like_status: int,post: {
              commentCount:int,
          content: string,
          createTime: int,
          id: 1,
          score: float,
          status: int,
          title: string,
          type: int,userId: 103
            },
          user: {
          activationCode: string,
          createTime: int,
          email: string,
          headerUrl: string,
          id: int,
          password: string,
          salt: string,
          status:int,
          type: int,
          username:string
            },
            "like_cnt": int}</code>
        - 示例：
          <code>{
            "msg": "操作成功",
            "code": 200,
            "like_status": 0,
            "post": {
              "commentCount": 0,
              "content": "test",
              "createTime": 1687587052000,
              "id": 1,
              "score": 0.0,
              "status": 0,
              "title": "test",
              "type": 0,
              "userId": 103
            },
            "user": {
              "activationCode": "0f43f336e8bd423fa7ca3fdb5f70b7e6",
              "createTime": 1687532597000,
              "email": "2687335304@qq.com",
              "headerUrl": "http://rwg0efxom.hb-bkt.clouddn.com/test.jpg",
              "id": 103,
              "password": "fe421aa28fc4ea47e12b4d4cb7ae77dc",
              "salt": "5d47c",
              "status": 1,
              "type": 0,
              "username": "root"
            },
            "like_cnt": 0
          }
          </code>
  4. 获取帖子评论接口
   + 路径接口：<code>/api/discuss/comments</code>  
      + 请求参数：
        - 类型：json 
        - 方法：get
        - 属性：<code>{discussPostId: int,pageId:int}</code>
        - 示例：<code>{discussPostId: 1,pageId:1}</code>
      + 返回参数：
        - 类型：json
        - 属性：<code>{
          msg: string,
          code: int,
          comments: [],page_cnt: int,
          page_current: int
          }</code>
        - 示例：<code>{
            "msg": "获取成功",
            "code": 200,
            "comments": [],
            "page_cnt": 0,
            "page_current": 1
          }</code>
  5. 置顶帖子接口 
   + 路径接口：<code>/api/discuss/top</code>  
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：{  post : JSONObject  }
        - 示例：<code>{
            "id": 1 }</code>
      + 返回参数：
        - 类型：json
        - 属性：<code>{code: int,msg:string}</code>
        - **示例：<code>{"msg":"置顶成功","code":0}</code>**  0？
  6. 加入精选帖子接口
   + 路径接口：<code>/api/discuss/wonderful</code>  
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：{  post : JSONObject  }
        - 示例：<code>{
            "id": 1 }</code>
      + 返回参数：
        - 类型：json
        - 属性：<code>{code: int,msg:string}</code>
        - **示例：<code>{"msg":"加精成功","code":0}</code>**  0？
  7. 删除帖子接口   
   + 路径接口：<code>/api/discuss/delete</code>    
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：{  post : JSONObject  }
        - 示例：<code>{
            "id": 2
          }</code>
      + 返回参数：
        - 类型：json
        - 属性：<code>{code: int,msg:string}</code>
        - **示例：<code>{"msg":"删帖成功","code":0}</code>**
   
5. **网站数据**  
    1. 统计网站uv接口
      + 路径接口：<code>/api/data/uv</code>  
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{start: int,end:int}</code>
        - 示例：<code>{"start": 79707097,"end" : 96807052524}</code>
        - 注意： start 、end 都是数值，代表格林尼治时间1970年1月1日0点到start/end时间点的秒数， 要求start小于end，如{}果不小于，会报400 ，错误的返回信息是：{"msg":"请保证起始时间在结束时间之前"，"code" : 400}
      + 返回参数：
        - 类型：json
        - 属性：<code> { msg: string, code:int,viewer_cnt : int,start : string,end : string} </code>
        - 示例：<code>{
          "msg": "操作成功",
          "code": 200,"viewer_cnt" : e,"start" : "Fri Jan e2 06:08:27 CST 1970","end" : "Thu Apr 23 e9:05:e5 CST 1970"}</code>
  1. 统计网站DAU接口
      + 路径接口：<code>/api/data/dau </code>  
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{start: int,end:int}</code>
        - 示例：<code>{"start": 79707097,"end" : 96807052524}</code>
        - 注意： start 、end 都是数值，代表格林尼治时间1970年1月1日0点到start/end时间点的秒数， 要求start小于end，如{}果不小于，会报400 ，错误的返回信息是：{"msg":"请保证起始时间在结束时间之前"，"code" : 400}
      + 返回参数：
        - 类型：json
        - 属性：<code> { msg: string, code:int,viewer_cnt : int,start : string,end : string} </code>
        - 示例：<code>{
          "msg": "操作成功",
          "code": 200,"viewer_cnt" : e,"start" : "Fri Jan e2 06:08:27 CST 1970","end" : "Thu Apr 23 e9:05:e5 CST 1970"}</code>
   
6. **评论**   
7. 添加评论接口
   
   + 路径接口：<code> /api/comments/add/{discussPostId}</code>  
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{discussPostId:int, comment:Comment}</code>
        - 示例：<code>{discussPostId:1, comment:"string"}</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{msg:string,code: int,discussPostId:int}</code>
        - 示例：<code>{"msg":"操作成功","code":200,"discussPostId":1}</code>
   
8.  **关注**   
9.  关注某个对象
   
   + 路径接口：<code>/api/follow/to-follow</code>  
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{entity:JSONObject}</code>
        - 示例：<code>{
            "entity_type": 0,
            "entity_id": 103
          }</code>
        - 注意：默认是 0（最新）
      + 返回参数：
        - 类型：json 
        - 属性：<code>{msg:string,code: int}</code>
        - 示例：<code>{"msg":"已关注","code":200}</code>
   1. 取消关注
      + 路径接口：<code>/api/follow/to-unfollow</code>   
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{entity:JSONObject}</code>
        - 示例：<code>{
            "entity_type": 0,
            "entity_id": 103
          }</code>
      + 返回参数：
        - 类型：json
        - 属性：<code>{msg:string,code: int}</code>
        - 示例：<code>{"msg":"已取消关注","code":200}</code>
   2. 某个用户的关注列表接口
   
   + 路径接口：<code>/api/follow/followees/{userId}/{page}</code>    
      + 请求参数：
        - 类型：json 
        - 方法：get
        - 属性：<code>{userId:  int,page: int}</code>
        - 示例：{userId:  103 ,  page : 1 }
      + 返回参数：
        - 类型：json
        - 属性：<code>{
          msg: string,
          code: int,
          page_cnt: int,follows: [],
          user: {
          activationCode: string,
          createTime:int,
          email: string,
          headerUrl: string,
          id: int,
          password: string,
          salt: string,
          status:int,
          type: int,
          username: string
            },page_current: int }</code>
        - 示例：<code>{
            "msg": "获取关注列表成功",
            "code": 200,
            "page_cnt": 0,
            "follows": [],
            "user": {
              "activationCode": "0f43f336e8bd423fa7ca3fdb5f70b7e6",
              "createTime": 1687532597000,
              "email": "2687335304@qq.com",
              "headerUrl": "http://rwg0efxom.hb-bkt.clouddn.com/test.jpg",
              "id": 103,
              "password": "fe421aa28fc4ea47e12b4d4cb7ae77dc",
              "salt": "5d47c",
              "status": 1,
              "type": 0,
              "username": "root"
            },
            "page_current": 1
          }</code>
   1. 某个用户的粉丝列表接口
      + 路径接口：<code>/api/follow/followers/{userId}/{page}</code>    
      + 请求参数：
        - 类型：json 
        - 方法：get
        - 属性：<code>{userId:  int,page: int}</code>
        - 示例：{userId:  103 ,  page : 1 }
      + 返回参数：
        - 类型：json
        - 属性：<code>{
          msg: string,
          follwer_cnt: int,
          code: int,page: int,user: {
          activationCode: string,
          createTime:int,
          email: string,
          headerUrl: string,
          id: int,
          password: string,
          salt: string,
          status:int,
          type: int,
          username: string
            },
          users: []
          }</code>
        - 示例：<code>{
            "msg": "获取粉丝列表成功",
            "follwer_cnt": 0,
            "code": 0,
            "page": 1,
            "user": {
              "activationCode": "0f43f336e8bd423fa7ca3fdb5f70b7e6",
              "createTime": 1687532597000,
              "email": "2687335304@qq.com",
              "headerUrl": "http://rwg0efxom.hb-bkt.clouddn.com/test.jpg",
              "id": 103,
              "password": "fe421aa28fc4ea47e12b4d4cb7ae77dc",
              "salt": "5d47c",
              "status": 1,
              "type": 0,
              "username": "root"
            },
            "users": []
          }</code>
   
10. **点赞**  
11. 点赞接口
   
   + 路径接口：<code>/api/likes/to-like</code>  
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{
          entityType: int,
          entityId:int,
          entityUserId: int,postId: int
          }</code>
        - 示例：<code>{
            "entityType": 1,
            "entityId":102,
            "entityUserId": 103,
            "postId": 1
          }</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{msg:string,code:int,likeCount:int,likeStatus:int}</code>
        - 示例：<code>{"msg":"点赞成功","code":200,"likeCount":1,"likeStatus":1}</code>
   
12. **通知**

   1. 获取私信列表接口

      + 路径接口：<code>/api/messages/letter/list</code>  
      + 请求参数：
        - 类型：json 
        - 方法：get
        - 属性：<code>{page:int}</code>
        - 示例：<code>{page:int}</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{
          msg: string,
          code: int,
          page_cnt: int,letterUnreadCount: int,
          conversations: [],noticeUnreadCount: int,
          page_current: int
          }</code>
        - 示例：<code>{
            "msg": "获取成功",
            "code": 200,
            "page_cnt": 0,
            "letterUnreadCount": 0,
            "conversations": [],
            "noticeUnreadCount": 0,
            "page_current": 1
          }</code>
   2. 私信详情页接口
      + 路径接口：<code>/api/messages/letter/detail/{conversationId}</code>    
      + 请求参数：
        - 类型：json 
        - 方法：get
        - 属性：<code>{conversationId: string, page :int}</code>
        - 示例：<code>{"conversationId": "104_103", "page" :1}</code>
      + 返回参数：
        - 类型：json
        - 属性：<code>{
          msg: string,
          notices: [],
          code:int,
          page_cnt: int,
          page_current: int
          }</code>
        - 示例：<code>{
            "msg": "获取成功",
            "notices": [],
            "code": 200,
            "page_cnt": 0,
            "page_current": 1
          }</code>
   3. 发送私信接口

      + 路径接口：<code>/api/messages/letter/send</code>    
      + 请求参数：
        - 类型：json 
        - 方法：post
        - 属性：<code>{ toName: string,content:string}</code>
        - 示例：<code>{ "toName":" root", "content": "hhh"}</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{msg:string,code:int}</code>
        - 示例：<code>{"msg":"发送成功","code":200}</code>
   4. 通知列表接口

      + 路径接口：：<code>/api/messages/notice/list</code>  
      + 请求参数：
        - 类型：json 
        - 方法：get
        - 属性：null
      + 返回参数：
        - 类型：json 
        - 属性：<code>{
          msg: string,
          commentNotice: {},
          code:int,likeNotice: {},
          letterUnreadCount: int,followNotice: {},
          noticeUnreadCount:int}</code>
        - 示例：<code>{
            "msg": "获取成功",
            "commentNotice": {},
            "code": 200,
            "likeNotice": {},
            "letterUnreadCount": 0,
            "followNotice": {},
            "noticeUnreadCount": 0
          }</code>
   5. 查询某个主题所包含的通知列表接口

      + 路径接口：<code>/api/messages/notice/detail/{topic}/{page}</code>  
      + 请求参数：
        - 类型：json 
        - 方法：get
        - 属性：<code>{topic:int}/{page:int}</code>
        - 示例：<code>{104_103}/{1}</code>
      + 返回参数：
        - 类型：json 
        - 属性：<code>{
          msg: string,
          notices: [],
          code: int,
          page_cnt: int,
          page_current: int
          }</code>
        - 示例：<code>{
            "msg": "获取成功",
            "notices": [],
            "code": 200,
            "page_cnt": 0,
            "page_current": 1
          }</code>

13. **搜索**    
14. 搜索帖子接口
    
   + 路径接口：<code>/api/search</code>  
       + 请求参数：
         - 类型：json 
         - 方法：get
         - 属性：<code>{keyword:string, page:int}</code>
         - 示例：<code>{keyword:"root", page:1}</code>
       + 返回参数：
         - 类型：json 
         - 属性：<code>{
           msg: string,
           code: int,
           discussPosts: [],page_cnt:int,
           keyword: string,
           page_current: int
           }</code>
         - 示例：<code>{
             "msg": "查询成功",
             "code": 200,
             "discussPosts": [],
             "page_cnt": 0,
             "keyword": "root",
             "page_current": 1
           }</code>