**10.搜索**    

1. 搜索帖子接口

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