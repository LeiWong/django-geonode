#Layer App API文档

Layer中的API实现了layer模块中对图层的操作，显示以及一些地图的实现，这些应用接口主要由layer app中的views函数(views.py)实现，layer app 中的API详细信息如下：

 Layer API：

## 方法：layers

功能说明：进入layer界面，加载layer页面列表

接口URL：/layers

请求方式：get

返回参数：返回json格式数据，包括地图的详细信息(地图名，作者，时间等)列表以及http状态码

## 方法：layer\_upload

功能说明：当请求方法为get时，加载上传图层页面；当请求方法为post时，用户上传图层，要求登录后操作

接口URL：/upload

请求方式：get/post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
| Limit | 每页返回layer的最大数量 | 是 | 限制每页返回layer数量 | limit=100 |
| Offset | 偏移量 | 是 | 略过的layer数量，从0开始 | offset=0 |

返回参数：

##方法：layer\_detail

功能说明：根据用户请求的layername返回layer的详细数据

接口URL：/layername

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
| layerename | 图层名字 | 是 | 图层的名字 | /geonode:brasil\_1 |

返回参数：主要返回地图ulr（eg:c.tile.openstreetmap/2/3/0.png），地图API（/geoserver/wms）及地图信息、属性等

## 方法：layer\_replace

功能说明：当请求方式为get时，表示点击进入替换图层页面，当请求方式为post时，表示替换图层操作

接口URL：/layername/\*/repalce

请求方式：get/post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
| layername | 图层名字 | 是 | 图层的名字 |   

返回参数：

## 方法：layer\_metadata

功能说明：当请求方式为get时，表示非元数据拥有者查看元数据操作，当请求方式为post时，表示元数据拥有者对图层的元数据进行的修改操作

接口URL：/layername/\*/metadata

请求方式：get、post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
| layerename | 层名字 | 是 | 层的名字 |   

返回参数：

## 方法：layer\_remove

功能说明：删除用户拥有的图层

接口URL：、layername/\*/remove

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
| layerename | 层名字 | 是 | 层的名字 |   |

返回参数：

## 方法：layer\_granule\_remove

功能说明：当请求方式为get时，返回请求图层和颗粒，当请求方式为post时表示登录用户在自己的图层上进行删除图层上的颗粒操作

接口URL：/granule\_id/layername/granule\_remove

请求方式：get/post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
| layerename | 层名字 | 是 | 层的名字 |   |
| granule\_id | 颗粒id | 是 | 颗粒的编号 |   |

返回参数：

## 方法：layer\_thumbnail

功能说明：

接口URL：/layername/\*/thumbnail

请求方式：post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
| Layername | 图层名 | 是 | 图层的名字 |   |

返回参数：

## 方法：get\_layer

功能说明：获取layer对象的json数据

接口URL：/layername/\*/get

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
| layerename | 层名字 | 是 | 层的名字 |   |

返回参数：

## 方法：layer\_metadata\_detail

功能说明：返回元数据的详细信息

接口URL：/layername/\*/metadata\_detail

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
| layerename | 层名字 | 是 | 层的名字 |   |

返回参数：

## 方法：layer\_chang\_poc

功能说明：

接口URL：

请求方式：post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
| ids |   | 是 |   |   |

返回参数：

## 方法：layers\_acls

功能说明：

接口URL：/acls/

请求方式：

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
| layerename | 层名字 | 是 | 层的名字 |   |

返回参数：

## 方法：resolve\_user

功能说明：

接口URL：/resolve\_user/

请求方式：

参数说明：

返回参数：

## 方法：layer\_batch\_download

功能说明：当请求为post时，表示开始下载完整图层的组合图层集合，当请求为get时，表示监控下载情况

接口URL：/download

请求方式：get/post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
| download\_id | 下载id | 是 | 下载编号 |   |

返回参数：

##方法：/maps/new

功能说明：使用当前图层生成一张新的地图

接口URL：/maps/new

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
| layer | 层 | 是 | 当前图层信息 | /new？layer=geonode:tb\_poi\_brasil\_l |

返回参数：

#GeoServer API

web map service （wms）提供了标准的地理地图图片请求界面，在layer层的地图操作中，实时地图由geoserver的API动态生成，在geonode的geoserver app中提供了本项目所需要的geoserver API。

 geoserver API：

##方法：wms

功能说明：wms请求根据提供的参数执行geoserver提供的地图信息

接口URL：/geoserver/vms?

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
| SERVICE | 服务名 | 是 |   | SERVICE=WMS |
| REQUEST | 请求操作 | 是 |   | REQUEST=Exceptions、GetCapabilities、GetMap、DescribeLayer、GetLegendGraphic |
| TILED |   |   |   | TILED=true |
| VERSION |   | 是 |   | VERSION=1.1 |

REQUEST 操作 描述：

#
[ANNOTATION:

BY &#39;华农天时&#39;
ON &#39;2017-01-06T09:15:28&#39;
NOTE: &#39;&#39;
NOTE: &#39;Request参数值的详细描述&#39;]

http://docs.geoserver.org/stable/en/user/services/wms/reference.html

返回参数：

对地图的操作主要依靠wms中的request参数值，再调用request参数值对应的geoserver API，详细的geoserver API信息描述见一下链接：

#
[ANNOTATION:

BY &#39;华农天时&#39;
ON &#39;2017-01-06T09:14:47&#39;
NOTE: &#39;&#39;
NOTE: &#39;geoserver API 文档&#39;]

http://docs.geoserver.org/stable/en/user/services/wms/reference.html
