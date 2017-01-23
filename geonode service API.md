#GeoNode services API

根据源码分析，发现services模块中有大量WebMapService、WebFeatureService等与service相关技术，估计该模块应该是与提高的地图服务相关，由于对地理相关应用不太熟悉，以提取API为前提，对service模块进行分析整理。

##方法：services
功能说明：返回所有已经注册的服务列表

接口URL：/

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |

返回参数：返回{"services"：services}

##方法：register\_service
功能说明:该方法用于仅仅以一个url作为参数手动注册一个新的服务

接口URL：/register

请求方式：get/post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|url |访问路径|是|---|——|
|name|名字|是|---|---|
|type|服务类型|---|---|

返回参数：

##方法：register\_service\_by\_type
功能说明：基于特定的type，注册服务

接口URL：/registerbytype

请求方式：post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|url|访问路径|是|---|---|
|type|服务类型|是|---|type="wms"/"ows"/"rest"|

返回参数：

##方法：\_is\_unique
功能说明：根据匹配的url，确定一个服务是否已经注册

接口URL：

请求方式：作为私有函数方法

参数说明：_is_unique(url)

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|url|访问路径|是|---|--|

返回参数：返回含有状态码和状态信息的json数据

##方法：\_clean_url
功能说明：清除一个基本url的所有参数

接口URL：_clean_url(base_url)

请求方式：作为私有函数方法

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|base_url|

返回参数：返回含有状态码和状态信息的json数据url

##方法：\_get\_valid\_name
功能说明：为一个服务返回一个唯一slug name

接口URL：\_get\_valid\_name(proposed_name)

请求方式：作为私有函数方法

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|proposed_name|建议名称|是|--|--|

返回参数：返回含有状态码和状态信息的json数据

##方法：\_verify\_service\_type
功能说明：试着通过排除法确定服务类型

接口URL：\_verify\_service\_type(base_url,service_type=None)

请求方式：作为私有函数方法

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|base_url|基本路径|是|---|--|
|service_type|服务类型|否|--|--|

返回参数：返回含有状态码和状态信息的json数据

##方法：\_process\_wms\_service
功能说明：创建一个新的WMS/OWS 服务，如果有必要，进行级联

接口URL：\_process\_wms\_service(url, name, type, username, password, wms=None, owner=None, parent=None)

请求方式：作为私有函数方法

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|url|访问路径|是|
|name|名称|是|
|type|服务类型|是|
|username|用户名|是
|password|密码|是|
|wms|wms服务|否|
|owner|拥有者|否|
|parent|上一级|否|

返回参数：返回含有状态码和状态信息的json数据

##方法 \_register\_cascaded\_service
功能说明：register a service as cascading WMS

接口URL：\_register\_cascaded\_service(url,type,name,username,password,wms=None,owner=None,parent=None)

请求方式：作为私有函数方法

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|url|访问路径|是|
|name|名称|是|
|type|服务类型|是|
|username|用户名|是
|password|密码|是|
|wms|wms服务|否|
|owner|拥有者|否|
|parent|上一级|否|

返回参数：返回含有状态码和状态信息的json数据

## 方法：\_register\_cascaded\_layers
功能说明：register layers for a cascading WMS

接口URL：
\_register\_cascaded\_layers

请求方式：作为私有函数方法

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|service|服务|是|
|owner|拥有者|否

返回参数：返回含有状态码和状态信息的json数据

##方法：\_register\_indexed\_service
功能说明：register a service -WMS or OWS currently supported

接口URL：\_register\_indexed\_service(type,url,name,username,password,verbosity=False,wms=None,owner=None,parent=None)

请求方式：作为私有函数方法

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|url|访问路径|是|
|name|名称|是|
|type|服务类型|是|
|username|用户名|是
|password|密码|是|
|verbosity|--|否|
|wms|wms服务|否|
|owner|拥有者|否|
|parent|上一级|否|

返回参数：返回含有状态码和状态信息的json数据

##方法：\_register\_indexed\_layers
功能说明：register layers for an indexed service(only WMS/OWS curently supported)

接口URL： \_register\_indexed\-layers(service,wms=None,verbosity=False)

请求方式：作为私有函数方法

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|service|服务请求|是|
|wms|---|否 |
|verbosity| --- |否|  --- |verbosity=False|

返回参数：返回含有状态码和状态信息的json数据

##方法：\_register\_harvested\_service
功能说明：register a CSW service,then step through results(or queue for asynchronous harvesting)

接口URL：\_register\_harvested\_service(url, name, username, password, csw=None, owner=None)

请求方式：作为私有函数方法

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- | --- |
|url|访问路径|是|
|name|名称|是|
|username|用户名|
|password|密码|
|csw|---|否|
\|owner|---|否|
 
返回参数：返回含有状态码和状态信息的json数据

## 方法：\_harvest\_csw
功能说明：step through CSW results, and if one seems to be WMS or Are REST service then rigster the rigester it 
 
接口URL：\_jarvest\_csw(csw,,maxrecords=10,totalrecords=float('inf'))
 
请求方式：作为私有函数方法
 
参数说明：
 
| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- | --- |
|csw | ---| 是 | --- | ---|
|maxrecords|最大记录|否|---|maxrecords=10|
|totalrecords|总记录|否|---|totalrecords=float('inf')|
 
 返回参数：返回含有状态码和状态信息的json数据
 
## 方法：\_register\_arcgis\_url
功能说明：register an ArcGIS REST service URL

接口URL：\_register\_arcgis\_url(url,name,username,password,owner=owner,parent=parent)

请求方式：作为私有函数方法

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- | --- |
|url|访问路径|是|
|name|名称|是|
|username|用户名|是|
|password|密码|是|
|owner|拥有者|否|---|owner=owner|
|parent|父级|否|---|parent=parent|

返回参数：返回含有状态码和状态信息的json数据

##方法:\_register\_arcgis\_layers
功能说明：register layers form an ArcGIS REST service

接口URL：\_register\_arcgis\_layers(service,arc=None)

请求方式：作为私有函数方法

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- | --- |
|service|请求服务|是|
|arc|---|否|---|arc=None|

返回参数：返回含有状态码和状态信息的json数据

##方法：\_process\_arcgis\_service
功能说明：create a service model instance for an ArcGIS REST service

接口URL：\_process\_arcgis\_service(arcsever,name,owner=None,parnet=None)

请求方式：作为私有函数方法

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- | --- |
|arcservice|arc服务|是|
|name|名称|是|
|owner|拥有者|否|
|parent|父级|否|

返回参数：返回含义状态码和状态信息的json数据

##方法：\_process\_arcgis\_folder
功能说明：iterate through folders and services in an ArcGIS REST service folder

接口URL：\_process\_arcgis\_folder(folder,name,services=None,owner=None,parent=None)

请求方式：作为私有函数方法

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- | --- |
|folder|文件夹|是|
|name|名称|是|
|service|服务|否|---|service=None|
|owner|拥有者|否|---|owner=None|
|parent|父级|否|parent=None|

返回参数：

##方法：\_register\_ogp\_service
功能说明：register OpenGeoPortal as a service

接口URL：\_register\_ogp\_service(url,owner=None)

请求方式：作为私有函数方法

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- | --- |
|url|访问路径|是|
|owner|拥有者|否|---|owner=None|

返回参数：返回带有状态码的json数据

##方法：\_harvest\_ogp\_layers
功能说明：query OpenGeoPortal's solr instance for layers

接口URL：\_harvest\_ogp\_layers(service,maxredords=10,start=0,totalrecords=float('inf'),owner=None,institution=None)

请求方式:作为私有函数方法

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- | --- |
|service|请求服务|是|---|---|
|maxrecords|最大记录|否|--|maxrecords=10|
|start|开始数|否|---|start=0|
|totalrecords|合计记录|否|---|totalrecords=float('inf')|
|owner|拥有者|否|---|owner=None|
|institution|机构|否|---|institution=None|

返回参数：

##方法：process_ogp_results
功能说明：create WMS services and layers from OGP results

接口URL：process_ogp_results(ogp,result_json,owner=None)

请求方式:作为私有函数方法

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- | --- |
|ogp|
|result_json|结果的json格式|是|
|owner|拥有者|否|---|owne=None

返回参数：

##方法：service_detail
功能说明：该视图方法显示服务的详细信息

接口URL：/service_id

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- | --- |
|service_id|服务id|是|服务的编号|--|

返回参数：返回图层信息和服务信息

##方法：edit\_service
功能说明：编辑已存在的服务

接口URL：/service_id/edit

请求方式:post

参数说明:

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- | --- |
|service_id|服务id|是|服务的编号|--|

返回参数：返回{“service”：service_obj,"service_form":service_form}

##方法：update_layers
功能说明：从一个已经存在的服务中导入或更新图层

接口URL：update\_layers(service)

请求方式:函数方法

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- | --- |
|service|服务名|是|---|---|

返回参数：

##方法：remove_service
功能说明：删除一个服务，以及服务的组成图层,当请求方式为get时，表示请求展示要删除的service，当请求方式为post时，表示执行删除service

接口URL：/service_id/remove

请求方式：get/post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- | --- |
|service_id|服务id|是|要删除的服务编号|--|

返回参数：当get请求时：返回{“service":service_obj}
		  当post请求时：重定向service页面
		  
##方法：ajax\_service\_permissions
功能说明：确定服务的ajax请求权限

接口URL：/service_id/ajax_permissions

请求方式：post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- | --- |
|service_id|服务id|是|服务编号|--|

返回参数：返回状态码

##方法：create\_arcgis\_links
功能说明：创建arcgis链接

接口URL：create\_argis\_links(instance)

请求方式：函数方法

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- | --- |
|instance|实例对象|是|---|---|

返回参数：










 







