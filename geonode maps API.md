# GeoNode maps模块 API文档

geonode.maps app 被用来把GeoNode的多层地图组合起来，地图和地图层对象用来形成和显示GeoExplorer应用生产的地图。地图类同样继承于为地图提供了丰富的元数据集合的基资源类。

## 方法：_resolve_map
功能说明：提供的类型名和权限，对地图进行解析

接口URL：

请求方式:get

## 方法：map_detail
功能说明：显示每个地图的详细信息

接口URL：/mapid

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
| mapid | 地图Id | 是 | 地图编号 | /mapid |
 
返回参数：

## 方法：map_metadata
功能说明：返回地图的元数据信息

接口URL：/mapid/*/metadata

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|mapid |地图ID|是|地图编号|/mapid/metadata|

返回参数：地图对象（map_obj），地图表单，作者信息表单等地图相关数据

## 方法：map_remove
功能说明：删除地图以及构成地图的图层

接口URL：mapid/remove

请求方式：get/post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|mapid|地图ID|是|地图编号|、mapid/remove|

返回参数：

## 方法：map_embed
功能说明：嵌入地图

接口URL：/mapid/embed

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|mapid|地图ID|否|地图编号|/mapid/embed|
|snapshot|快照|否| ---| /mapid/snapshot|
返回参数：

## 方法：map_view
功能说明：returns the map composer opened to the map with the given map ID

接口URL：/mapid/snapshot/view

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|mapid|地图ID|否|地图编号|/mapid/embed|
|snapshot|快照|否| ---| /mapid/snapshot|

返回参数：返回map_obj对象

## 方法：map_view_js 

功能说明：执行地图视图的js

接口URL：

请求方式：

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|mapid|地图ID|是|地图编号|/mapid/embed|
|snapshot|--|否| ---| /mapid/snapshot|

返回参数：

## 方法：map_json
参数说明：

接口URL：

请求方式：get/put

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|mapid|地图ID|是|地图编号|/mapid/embed|
|snapshot|--|否| ---| /mapid/snapshot|

返回参数：

#新地图

## 方法:new_map_config
功能说明：创建新地图的方法，如果有查询参数copy，则复制编号为id的地图，如果没有则使用默认地图配置

接口URL：

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|copy|复制|否|是否复制地图|---|
|layer|图层|否|图层名|---|

返回参数：

## 方法：map_download
功能说明：下载组成地图的所以图层，并删除图层状态

接口URL：mapid/download

请求方式：post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|mapid|地图ID|是|地图编号|/mapid/download|

返回参数：geoserver,map_status,map,locked_layers，remote_layers,downloadable_layers,siteurl

## 方法：map_wmc
功能说明：序列化一个OGC(开放地图空间信息）)地图内容文档

接口URL：/mapid/wmc

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|mapid|地图ID|是|地图编号|/mapid/wmc|

返回参数：

## 方法：map_wms
方法说明：把本地地图作为一组图层发布到本地OWS
    GET: return endpoint information for group layer,
    PUT: update existing or create new group layer.

接口URL：/mapid/wms

请求方式：get/put

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|mapid|地图ID|是|地图编号|/mapid/wms|
返回参数：

## featured_map
方法说明：根据给出的官方站点url返回 map composer opened to the map

接口URL：
请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|url|地图url|是|地图官方站点|---|

返回参数：地图对象id

## 方法：map_thumbnail
方法说明：返回地图缩略图

接口URL：/mapid/thumbnail

请求方式：post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|mapid|地图ID|是|地图编号|/mapid/thumbnail|

返回参数：thumbnail saved

## 方法：map_metadata_detail
方法说明：返回地图元数据的详细信息

接口URL：/mapid/metadata_detail

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|mapid|地图ID|是|地图编号|/mapid/metadata_detail|

返回参数：map_obj,mapid,siteurl


















 






