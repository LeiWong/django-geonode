# GeoNode geoserver模块 API文档
geoserver模块被用来实现GeoNode的python代码与GeoServer的交互，geoserver高度依赖于提供GeoServer's REST configuration API的gsconfig库。额外的，geoserver的uploader模块用来实现上传和配置图层跟GeoServer's importer API 进行交互。

例如访问url：http://127.0.0.1:8080/geoserver/topp/wms?service=WMS&version=1.1.0&request=GetMap&layers=topp:states&styles=&bbox=-124.73142200000001,24.955967,-66.969849,49.371735&width=780&height=330&srs=EPSG:4326&format=application/openlayers

显然这是一个对WMS服务的GetMap请求，format=application/openlayers这个参数告诉GeoServer分发OpenLayer JavaScript 应用，severice参数告诉GeoServer用哪一种服务，version参数表示版本，layers参数定义了在地图上显示的数据，bbox是边界参数，格式为bbox=minx, miny, maxx, maxy

## 方法：updatelayers
功能说明：超级用户更新已有图层信息

接口URL：/updatelayers

请求方式：post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|owner|拥有者|是|图层拥有者|/updatelayers|
|workspace|--|是|--|--|
|store|

返回参数：

## 方法：layer_style
功能说明：处理默认图层样式

接口URL：/layername/style

请求方式：post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|layername|图层名|是|图层名称|/layername/style|

返回参数：

## 方法：layer_style_upload
功能说明：上传图层样式

接口URL：/layername/style/upload

请求方式：post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|layername|图层名|是|图层样式|/layername/style/upload|

返回参数：

##方法：layer_style_manage
功能说明：图层样式管理，当请求方式为get时，表示首次从数据库提取图层样式信息，当请求方式为post时，表示提交用户选择的图层样式信息

接口URL：/layername/style/manage

请求方式：get/post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|layername|图层名|是|图层样式|/layername/style/manage|
|selected_styles|选择的样式|是|---|---|
|default_style|默认样式|是|---|---|

返回参数：get：返回图层和错误信息
			
		  post：返回图层和错误信息

## 方法：feature_edit_check
方法说明：检验用户是否有特征编辑权限

接口URL：/layername/edit-check

请求方式：post/put

参数说明：

## 方法：style_change_check
方法说明：

接口URL：

请求方式：

参数说明：


| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|path|路径|是|用户请求路径|/gs/rest/styles|

返回参数：返回authorized，其值为True或False

##方法geoserver_rest_proxy
方法说明：geoserver 代理

接口URL：/rest/layers
			/rest/sldservice
			/rest/styles

请求方式：post/put

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|proxy_path|代理路径|是|代理路径|---|
|downstream_path|下游路径|是|---|---|

返回参数：

## 方法：layer_batch_download
方法说明：batch download a set of layers

接口URL：/download

请求方式：get/post

参数说明：

返回参数：

## 方法：resolve_user
方法说明：用户解析

接口URL：/resolve_user

请求方式：

参数说明：

返回参数：


## 方法：layer_acls


















