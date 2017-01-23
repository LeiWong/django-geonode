# geonode 搜索的实现

在geonode模块中，如果是对图层和文本的显示搜索，主要是通过数据库查询语句来返回搜索结果，例如geonode提供了一些get 请求支持的json API，这些API
同样作为主要的搜索引擎。

## 查询API端点

* "/api/base" 查询ResourceBase数据库表，返回与地图、图层相关的结果
* "/api/layers" 查询 Layer 数据库表
*  "/api/maps" 查询 Map 数据库表
*  "/api/documents" 查询 Docuemnt 数据库表
*  "/api/groups" 查询 GroupProfile 数据库表
*  "/api/profiles" 查询Profile 数据库表
*  "/api/categories" 查询 Category 数据库表
*  "/api/keywords" 查询 Tag 数据库表
*  "/api/featured" 查询ResourceBase 数据库表，通过限制一个字段的flageed作为featured

## API过滤
API过滤方法搜索，允许添加django风格的过滤模式到url。
例如：可以通过title过滤的url："/api/layers?title_contains=grid"
在django框架中，存在很多种可能的过滤，可以参见django filters guide

## API 限制和分页(pagination)
可以通过限制API的返回数来对指定的查询结果进行返回，例如："/api/layers?limit=10,同时可以进行跳过一些数量的返回数，对特定的数据进行返回。

##Haystack 搜索
geonode准备实现使用全文搜索引擎，注意到haystack仅仅被使用作为base，layers，maps和document的API
可以通过添加“search"到url使用全文API搜索，例如："/api/base/search?limit=0&offset=0"

尽管后端的类型是非强制的，geonode建议为了更简单的实现，使用Elasticsearch

为了实现后端的搜索，确保已经运行了Elasticsearch 实例，同时取消以下geonode设置中的注释：

1.修改 # Location of url mappings 为 Location of url mappings

2.设置以下配置：
UPLOADER={ 'BACKEND':'geonode.rest',)

3.取消以下注释，纠正Elasticsearch 的地址：

4.haystack配置如下，可根据实际情况进行配置：
\# Haystack Search Backend Configuration. To enable,

\# first install the following:

\# - pip install django-haystack

\# - pip install pyelasticsearch

\# Set HAYSTACK_SEARCH to True

\# Run "python manage.py rebuild_index"

HAYSTACK_SEARCH = False

\# Avoid permissions prefiltering

SKIP_PERMS_FILTER = False

\# Update facet counts from Haystack

HAYSTACK_FACET_COUNTS = False

\# HAYSTACK_CONNECTIONS = {

\#    'default': {

\#        'ENGINE': 
'haystack.backends.elasticsearch_backend.'

\#        'ElasticsearchSearchEngine',

\#        'URL': 'http://127.0.0.1:9200/',

\#        'INDEX_NAME': 'geonode',

\#        },

\#    }
\# HAYSTACK_SIGNAL_PROCESSOR = 

'haystack.signals.RealtimeSignalProcessor'

\# HAYSTACK_SEARCH_RESULTS_PER_PAGE = 20


##使用django实现全文搜索

django-haystack是专门针对django实现全文搜索的一个第三方应用，可以实现方便地对model里的内容进行搜索、索引。

django-haystack设计支持whoosh，solr，Xapian，elasticsearch四种全文检索引擎后端，是全文检索的框架。

1.安装django-haystack：pip install django-haystack ,pip 版本是1.x，可到官网下载最新2.0版本

2.在应用app目录下建立一个search_indexes.py

search_indexes.py:

from haystack import indexes

from project.app.models import Profile


class ProfileIndex(indexes.SearchIndex,indexes.Indexable):
	
	id = indexes.IntegerField(model_attr='id')
	
	username = indexes.CharField(model_attr='username',null=True)
	
	profile = indexes.CharField(model_attr='profile',null=True)
	
	def get_model(self):
		return Profile
	def prepare_title(self.obj):
		return str(obj)
	def prepare_title_sort(self,obj):
		return str(obj).lower().lstrip()
	def prepare_type(self,obj):
		return "user”
		
	def index_queryset(self):
		'''used when the entire index for model is updated'''
		return self.get_model().objects.all()#确定在建立索引时有些记录记录被索引，这里返回所有记录‘’‘
		

3.在模板目录templates/indexes/app/Profile_text.txt
	
	{{object.Content}}
	{{object.username}}
	{{object.name}}
	{{object.profile}}
	
模板的作用是让text字段包含的内容，在后面的模板中可能显示

4.在settings.py中配置：

		HAYSTACK_CONNECTIONS = {
			'default':{
				'ENGINE':'haystack.backends.whoosh_backend.WhooshEngine',
				'PATH':os.path.join(PROJECT_PATH,'whoosh_index'),
				},
			}
			
5.最后，重建索引文件：
python manage.py rebuild_index 或者使用update_index

##中文分词，jieba的使用
1.安装jieba：

sudo pip install whoosh django-haystack jieba

2.配置whoosh：

将文件whoosh_backend.py(/lib/python2.7/site-packages/haystack/backends/whoosh_backend.py) 拷贝到app下面，并重命名
为whoosh_ch_backend.py,并修改：

from jieba.analyse import ChineseAnalyzer

schema_filelds[field_class.index_fieldname]=TEXT(stored=True,ananlyzer=ChineseAnalyzer(),field_boost=field_class.boost)

3.在settings.py中修改引擎：

import os

HAYSTACK_CONNECTIONS={
	'default':{ 'ENGINE':blog.whoosh_cn_backend.WhooshEngine',
	'PATH':os.path.join(BASE_DIR,'whoosh_index'},
	}

4.重建索引，便可进行中文搜索：

python manage.py rebuild_index

5.索引自动更新：

如果没有自动索引，每当新数据添加，都必须手动执行update_index

自动索引可通过在settings.py中添加一个信号实现：

进入settings.py文件，添加以下设置：

HAYSTACK_SIGNAL_PROCESSOR = "haystack.signals.RealtimeSignalProcesso"



	
	

                                          
                                 
                                          
                                          
                                          
                                          
                                          
                                             
