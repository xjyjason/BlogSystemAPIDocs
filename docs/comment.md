**6.评论**   

1. 添加评论接口

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