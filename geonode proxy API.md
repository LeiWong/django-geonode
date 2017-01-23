# geonode proxy API
geonode proxy 的作用是辅助js应用连接远程服务器，Django 应用为访问远程数据提供了一些http代理，来克服浏览器的同源访问政策，这种方法帮助geonode站点的GeoExt可以访问OGC-compliant 数据服务的多种xml文档。

##方法：proxy

功能说明：代理服务器

接口URL：/opensearch

请求方式：get

参数说明：

参数	名字	是否必须	说明	示例
