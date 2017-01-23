# geonode catalogue API归档

geonode catalogue 应用提供了一个关键的元数据目录集合功能在geonode本身，geonode是作为执行这些功能的的pycsw库的集成版本的配置使用，但也可以作为任何符合OGC的CS-W实现的配置，例如GeoNetwork，Deegree。元数据应用允许用户为他们的图层、地图和文档进行导入或者编辑元数据，并提供一个OGC兼容搜索界面，用于与其他系统联合使用




##方法：csw_global_dispatch
功能说明：pycsw装饰器，只有当本地pycsw作为后端时，才执行此方法，否则重定向非本地pycsw后端

接口URL：/csw

请求方式：get

参数说明：无

返回参数：content_type=csw.contenttype

##方法：opensearch_dispatch
功能说明：Opensearch 装饰器

接口URL：/opensearch

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |

返回参数：json格式的ctx

## 方法：data_json
功能说明：返回catalogue展示的json数据

接口URL：

请求方式：get

参数说明：无

返回参数：返回元数据记录的json格式

##方法：csw_render_extra_format_txt
功能说明：pycsw 装饰器

接口URL：/csw_to_extra_format/layeruuid/resname.txt

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|layeruuid|图层uuid编号|是|图层的唯一标识|--|
|resname|---|是|---|---|

返回参数：返回csv格式的content

## 方法：csw_render_extra_format_html
功能说明：

接口URL：/csw_to_extra_foramt/layeruuid/resname.html

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|layeruuid|图层uuid编号|是|图层的唯一标识|---|
|resname|

返回参数：








