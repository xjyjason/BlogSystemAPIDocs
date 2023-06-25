##### **3. 首页**  

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

2. 500 错误界面接口

   - 路径接口：<code>/api/posts/error</code>  
   - 请求参数：
     - 类型：json 
     - 方法：get
     - 属性：<code>null</code>
   - 返回参数：
     - 类型：json
     - 属性：<code>{code: int,msg:string}</code>
     - 示例：<code>{
       "code": 500,
       "msg": "服务器发生错误"}</code>

3. 没有权限访问时的错误界面接口

   - 路径接口：<code>/api/posts/denied</code>  

   - 请求参数：
     - 类型：json 
     - 方法：get
     - 属性：`null`
   - 返回参数
     - 类型：json
     - 属性：<code>{code: int,msg:string}</code>
     - 示例：<code>{
           "msg": "没有权限访问",
           "code": 403
        }</code>