**8.点赞**  

1. 点赞接口

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