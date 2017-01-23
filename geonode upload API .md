#geonode upload API
upload模块提供了进行上载的函数功能，上载的过程可以是多部进行的，所有的视图都是通过视图函数来处理。


##方法：\_is\_async\_step
功能说明：是否是异步操作步骤

接口URL：\_is\_async\_step(upload_session)

请求方式：私有函数方法

参数说明：

| 参数 | 名字 | 是否必须| 说明 | 示例 |
| --- | --- | --- | --- | --- |
|upload_session|上传session|是|上传会话操作|---|

返回参数：_ASYNC_UPLOAD 

##方法：_progress\_redirect
功能说明：重定向到前进的步骤

接口URL：\_progress\_redirect(step,upload_id)

请求方式：私有函数方法

参数说明：

| 参数 | 名字 | 是否必须| 说明 | 示例 |
| --- | --- | --- | --- | --- |
|step|步骤|是|下一步操作|---|
|upload_id|上传id|是|上传步骤编号|--|

返回参数：

##方法：\_error\_response
功能说明：错误回应

接口URL：\_error\_response(req,exception=None,errors=None,force_ajax=True)

请求方式：私有函数方法

参数说明：

| 参数 | 名字 | 是否必须| 说明 | 示例 |
| --- | --- | --- | --- | --- |
|req|请求|是|request请求对象|--|
|exception|接受错误|否|---|errors=None|
|errors|错误|否|---|errors=None|
force_ajax|强制ajax|否|---|force_ajax=True|

返回参数：返回状态信息

##方法：\_next\_step\_response
功能说明：如果当前步骤是post请求，再进一步执行 

接口URL：\_next\_step\_response(req,upload_session,force_ajax=True)

请求方式：私有函数方法

参数说明：

| 参数 | 名字 | 是否必须| 说明 | 示例 |
| --- | --- | --- | --- | --- |
|req|请求|是|request请求对象|---|---|
|upload_session|上传session|是|上传会话对象|---|--|
|force_ajax|强制ajax|否|--|force_ajax=True|

返回参数：

##方法：\_create\_time\_form
功能说明：创建时间表单

接口URL：\_create\_time\_form(import\_session,form\_data)

请求方式：私有函数方法

参数说明：

| 参数 | 名字 | 是否必须| 说明 | 示例 |
| --- | --- | --- | --- | --- |
|import\_session|导入的session|是|
|from_data|表单数据|是|

返回参数：form.TimeForm(**args)

##方法：save\_step\_view
功能说明：存储步骤的视图

接口URL：save\_step\_view(req,session)

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须| 说明 | 示例 |
| --- | --- | --- | --- | --- |
|req|请求对象|是|---|
|session|会话对象|是|

返回参数：

##方法：data\_upload\_progress
功能说明：当geoserver REST要求admin操作时执行数据上传

接口URL：data\_upload\_progress(req)

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须| 说明 | 示例 |
| --- | --- | --- | --- | --- |
|req|请求方式|是|

返回参数：{“state”：NONE}

##方法：srs\_step\_view
功能说明：

接口URL：srs\_step\_view(req,upload_session)

请求方式：post

参数说明：

| 参数 | 名字 | 是否必须| 说明 | 示例 |
| --- | --- | --- | --- | --- |
|req|请求方式|是|
|upload_session|上传session|是

返回参数：

##方法：is_latitude
功能说明:判断是否是经度

接口URL：is\_latitude(colname)

请求方式：函数方法

参数说明：

| 参数 | 名字 | 是否必须| 说明 | 示例 |
| --- | --- | --- | --- | --- |	
|colname|

返回参数：

##方法：is\_longitude
功能说明：判断是否是纬度

接口URL：is\_longitude(colname)

请求方式：函数方法

参数说明：

| 参数 | 名字 | 是否必须| 说明 | 示例 |
| --- | --- | --- | --- | --- |
|colname|

返回参数：

##方法：csv\_step\_view                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     
功能说明：上传csv格式文件

接口URL：

请求方式：post

参数说明：

| 参数 | 名字 | 是否必须| 说明 | 示例 |
| --- | --- | --- | --- | --- |
|upload_session|上传session对象|是|

返回参数：

##方法：time\_step\_view
功能说明：

接口URL：

请求方式：get/post

参数说明：

| 参数 | 名字 | 是否必须| 说明 | 示例 |
| --- | --- | --- | --- | --- |
|upload_session|上传session对象|是|

返回参数：

##方法：final\_step\_view
功能说明：最后步骤执行视图

接口URL：final\_step\_view(req,upload_session)

请求方式：函数方法

参数说明：

| 参数 | 名字 | 是否必须| 说明 | 示例 |
| --- | --- | --- | --- | --- |
|upload_session|上传session对象|是|

返回参数：

##方法：get\_next\_step
功能说明：

接口URL：get\_next\_step(upload_session,offset=1)

请求方式：函数方法

参数说明:

| 参数 | 名字 | 是否必须| 说明 | 示例 |
| --- | --- | --- | --- | --- |
|upload_session|上传session对象|是
|offset|偏移量|否|表示跳过的upload_session|offset=1|

返回参数：pages

##方法：get\_previous\_step
功能说明:

接口URL：

请求方式：函数方法

参数说明：

| 参数 | 名字 | 是否必须| 说明 | 示例 |
| --- | --- | --- | --- | --- |
|upload_session|上传session对象|是|
|post_to|---|是|

返回参数：

##方法：view
功能说明：上传视图
 
 接口URL：view(req,step)
 
 请求方式：函数方法
 
 参数说明：
 
| 参数 | 名字 | 是否必须| 说明 | 示例 |
| --- | --- | --- | --- | --- |
|step|步骤|是|

返回参数：

##方法：delete
功能说明：删除 上传

接口uRL：delete(req,id)

请求方式:函数方法

参数说明：

| 参数 | 名字 | 是否必须| 说明 | 示例 |
| --- | --- | --- | --- | --- |
|id|编号|是|upload的编号|---|

返回参数：


##	方法:run\_import
功能说明：使用异步执行导入

接口URL：run\_import(upload_session,async)

请求方式：函数方法

参数说明：











