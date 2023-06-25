**4. 帖子** 

1. 更新帖子接口
   -    路径接口：<code>/api/discuss/uploadMdPic</code>  
   - 请求参数：
     - 类型：json 
     - 方法：post
     - 属性：<code>{file:MultipartFile}</code>
     - 示例：<code>{file:null}</code>
   - 返回参数：
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

   -  路径接口：<code>/api/discuss/detail/{discussPostId}</code>  

   - 请求参数：
     - 类型：json
     - 方法：get
     - 属性：<code>{discussPostId: int}</code>
     - 示例：<code>{discussPostId: 1}</code>
   - 返回参数 
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
     - 示例：<code>{
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
       }</code>

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
    - 示例：<code>{"msg":"加精成功","code":0}</code>  

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
    - 示例：<code>{"msg":"删帖成功","code":0}</code>