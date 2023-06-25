**5.网站数据**  

1. 统计网站uv接口

+ 路径接口：<code>/api/data/uv</code>  
  + 请求参数：
    - 类型：json 
    - 方法：post
    - 属性：<code>{start: int,end:int}</code>
    - 示例：<code>{"start": 79707097,"end" : 96807052524}</code>
    - 注意： start 、end 都是数值，代表格林尼治时间1970年1月1日0点到start/end时间点的秒数， 要求start小于end，如果不小于，会报400 ，错误的返回信息是：{"msg":"请保证起始时间在结束时间之前"，"code" : 400}
  + 返回参数：
    - 类型：json
    - 属性：<code> { msg: string, code:int,viewer_cnt : int,start : string,end : string} </code>
    - 示例：<code>{
      "msg": "操作成功",
      "code": 200,"viewer_cnt" : e,"start" : "Fri Jan e2 06:08:27 CST 1970","end" : "Thu Apr 23 e9:05:e5 CST 1970"}</code>

2.  统计网站DAU接口
   + 路径接口：<code>/api/data/dau </code>  
   + 请求参数：
     - 类型：json 
     - 方法：post
     - 属性：<code>{start: int,end:int}</code>
     - 示例：<code>{"start": 79707097,"end" : 96807052524}</code>
     - 注意： start 、end 都是数值，代表格林尼治时间1970年1月1日0点到start/end时间点的秒数， 要求start小于end，如果不小于，会报400 ，错误的返回信息是：{"msg":"请保证起始时间在结束时间之前"，"code" : 400}
   + 返回参数：
     - 类型：json
     - 属性：<code> { msg: string, code:int,viewer_cnt : int,start : string,end : string} </code>
     - 示例：<code>{
       "msg": "操作成功",
       "code": 200,"viewer_cnt" : e,"start" : "Fri Jan e2 06:08:27 CST 1970","end" : "Thu Apr 23 e9:05:e5 CST 1970"}</code>