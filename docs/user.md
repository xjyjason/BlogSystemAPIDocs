##### **2.用户页面**  

1. 账号设置界面接口
   + 路径接口：<code>/user/setting</code>  
   + 请求参数：
     - 类型：json 
     - 方法：get
     - 属性：null
     - 示例：null
   + 返回参数：
     - 类型：json 
     - 属性：<code>{
       fileName: string,
       uploadToken: string}</code>
     - 示例：<code>{
         "fileName": "ef1420d10b4c41ab8d96dca4b4ee927a",
         "uploadToken": "_oNkRR16ItKyzIsqRBBWnICun0PVhnNuVFSGIoy7:vR550TW73Z48TGYBzFd9tiCPL_E=:eyJzY29wZSI6ImVjaG8tYXZhdGFyczplZjE0MjBkMTBiNGM0MWFiOGQ5NmRjYTRiNGVlOTI3YSIsInJldHVybkJvZHkiOiJ7XCJtc2dcIjpudWxsLFwiY29kZVwiOjB9IiwiZGVhZGxpbmUiOjE2ODc1NDI2NzF9"
       }</code>
     - 注意：需要与七牛云的账号交互
2. 更新图像路径接口
   + 路径接口：<code>/user/header/url</code>  
   + 请求参数：
     - 类型：json 
     - 方法：post
     - 属性：<code>{fileName:string}</code>
     - 示例：<code>{fileName:"test.jpg"}</code>
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
     - 示例：<code>{oldPassword: "root",newPassword: "root"}</code>
     - 注意：新密码与原密码不能相同，且会校验原密码是否输入正确
   + 返回参数：
     - 类型：json 
     - 属性：<code>{code: int,msg:string}</code>
     - 示例：<code>{"msg":"新密码和原密码相同","code":400}</code>
4. 个人主页接口
   + 路径接口：<code>/user/profile/{userId}</code>  
   + 请求参数：
     - 类型：json 
     - 方法：get
     - 属性：<code>{userId: int}</code>
     - 示例：<code>{userId: 103}</code>
   + 返回参数：
     - 类型：json 
     - 属性：<code>{
       msg: string,
       code: int,
       followeeCount: int,tab: string,
       hasFollowed: boolean,
       user: {
       activationCode: string,createTime:int,
       email: string,
       headerUrl: string,
       id: int,
       password: string,
       salt: string,
       status: int,
       type: int,username: string },
       followerCount: int,
       userLikeCount: int
       }</code>
     - 示例：<code>{
         "msg": "操作成功",
         "code": 200,
         "followeeCount": 0,
         "tab": "profile",
         "hasFollowed": false,
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
         "followerCount": 0,
         "userLikeCount": 0
       }</code>
5. 查询某个用户的帖子列表接口
   + 路径接口：<code>/user/discuss/{userId}/{page}</code>  
   + 请求参数：
     - 类型：json 
     - 方法：get
     - 属性：<code>{userId: int,page: int}</code>
     - 示例：<code>{userId: 103,page:1}</code>
   + 返回参数：
     - 类型：json 
     - 属性：<code>{
       msg:string,
       code: int,
       page_cnt: int,discussPosts: [],user: {
       activationCode: string,createTime:int,
       email: string,
       headerUrl: string,
       id: int,
       password: string,
       salt: string,
       status: int,
       type: int,username: string }, page_current: int
       }</code>
     - 示例：<code>{
         "msg": "获取成功",
         "code": 200,
         "page_cnt": 0,
         "discussPosts": [],
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
6. 查询某个用户的评论/回复列表接口
   + 路径接口：<code>/user/comment/{userId}</code>  
   + 请求参数：
     - 类型：json 
     - 方法：get
     - 属性：<code>{userId: int,page: int}</code>
     - 示例：<code>{userId: 1,page:1}</code>
   + 返回参数：
     - 类型：json 
     - 属性：<code>{msg: string,
       code: int,
       comments: [],
       page_cnt: int,
       page_current: 1}</code>
     - 示例：<code>{
         "msg": "获取成功",
         "code": 200,
         "comments": [],
         "page_cnt": 0,
         "page_current": 1
       }</code>