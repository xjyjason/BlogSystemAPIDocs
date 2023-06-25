**7. 关注**   

1. 关注某个对象

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

2. 取消关注
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
3. 某个用户的关注列表接口

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

4. 某个用户的粉丝列表接口
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