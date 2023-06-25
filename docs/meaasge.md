**9. 通知**

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