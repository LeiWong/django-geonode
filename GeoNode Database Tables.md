# 数据库结构表



1.  表 Profile

from app people models.py

表说明：用户个人信息

| 序号 | 字段名 | 字段意义 | 字段类型 | 允许为NULL | 允许为空 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | organization | 组织名 | CharField(255) | 是 | 是 |   |
| 2 | profile | 个人介绍 | TextField(255) | 是 | 是 |   |
| 3 | position | 职位名 | CharField(255) | 是 | 是 |   |
| 4 | voice | 组织或个人的联系电话 | CharField(255) | 是 | 是 |   |
| 5 | fax | 传真 | CharField(255) | 是 | 是 |   |
| 6 | delivery | 物理地址或邮箱地址 | CharField(255) | 是 | 是 |   |
| 7 | city | 城市 | CharField(255) | 是 | 是 |   |
| 8 | area | 行政地区 | CharField(255) | 是 | 是 |   |
| 9 | zipcode | 邮编号码 | CharField(255) | 是 | 是 |   |
| 10 | country | 国家 | CharField(3) | 是 | 是 |   |
| 11 | keywords | 项目描述关键词 | TaggableManager |   | 是 |   |



2.表 Style

from app layers models.py

表说明：层的存储样式

| 序号 | 字段名 | 字段意义 | 字段类型 | 允许为NULL | 允许为空 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | name | 样式名 | CharField(255) |   |   | unique |
| 2 | sld\_title | sld 标题 | CharField(255) | 是 | 是 |   |
| 3 | sld\_body | sld 文本内容 | TextField | 是 | 是 |   |
| 4 | sld\_version | sld 版本 | CharField(12) | 是 | 是 |   |
| 5 | sld\_url | sld 网址 | CharField(1000) | 是 |   |   |
| 6 | workspace |   | CharField(255) | 是 | 是 |   |

3.表 Layer

from app layers models.py

表说明：图层信息表

| 序号 | 字段名 | 字段意义 | 字段类型 | 允许为NULL | 允许为空 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | object | 对象 | LayerManager |   |   |   |
| 2 | workspace |   | CharField(128) |   |   |   |
| 3 | store |   | CharField(128) |   |   |   |
| 4 | storeType |   | CharField(128) |   |   |   |
| 5 | name |   | CharField(128) |   |   |   |
| 6 | typename |   | CharField(128) |   | 是 |   |
| 7 | is\_mosaic |   | BooleanField(False) |   |   |   |
| 8 | has\_time |   | BooleanField(False) |   |   |   |
| 9 | has\_elevation |   | BooleanField(False) |   |   |   |
| 10 | time\_regex |   | CharField(128) |   | 是 |   |
| 11 | elevation\_regex |   | CharField(128) |   | 是 |   |
| 12 | default\_style |   | ForeignKey(Style) |   | 是 |   |
| 13 | styles |   | ManyToManyField |   |   |   |
| 14 | charset |   | CharField(255) |   |   | default=&#39;UTF-8&#39; |
| 15 | upload\_session | 上传session | ForeignKey(UploadSession) |   | 是 |   |
| 16 | service | services.Service | Foreignkey(services.Service) |   | 是 |   |



4.表 LayerStyle

from app layers models.py

| 序号 | 字段名 | 字段意义 | 字段类型 | 允许为NULL | 允许为空 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | layer |   | ForeignKey(Layer) |   |   |   |
| 2 | style |   | ForeignKey(Layer) |   |   |   |

表说明：图层样式信息



5.表 UploadSession

from app layers models.py

表说明：上传图层的session信息

| 序号 | 字段名 | 字段意义 | 字段类型 | 允许为NULL | 允许为空 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | date |   | DataTimeField(auto\_now=True) |   |   |   |
| 2 | user |   | ForeignKey |   |   |   |
| 3 | processed |   | BoolearnField(False) |   |   |   |
| 4 | error |   | TextField |   | 是 |   |
| 5 | traceback |   | TextField |   | 是 |   |
| 6 | context |   | TextField |   | 是 |   |



6.表 LayerFile

from app layers models.py

表说明：上传图层文件信息表

| 序号 | 字段名 | 字段意义 | 字段类型 | 允许为NULL | 允许为空 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | upload\_session |   | ForeignKey(UploadSession) |   |   |   |
| 2 | name |   | CharField(255) |   |   |   |
| 3 | base |   | Bloolearn(False) |   |   |   |
| 4 | file |   | FileField(upload\_to=&#39;layers&#39;) |   |   |   |



7.表 Attribute

from app layers models.py

表说明：辅助存储层模型的属性

| 序号 | 字段名 | 字段意义 | 字段类型 | 允许为NULL | 允许为空 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | layers | 层 | ForeignKey(Layer) | 否 | 否 |   |
| 2 | attribute | 属性名 | CharField(255) | 是 | 否 |   |
| 3 | description | 属性描述 | CharField(255) | 是 | 是 |   |
| 4 | attribute\_label | 属性在geonode中的显示名称 | CharField(255) | 是 | 是 |   |
| 5 | attribute\_type | 属性的数据类型 | CharField(255) | 否 | 否 | default=&#39;xsd:string&#39; |
| 6 | visible | 属性是否可见 | BooleanField |   |   | default=&#39;True&#39; |
| 7 | display\_order | 显示顺序 | IntegerField |   |   | default=1 |
| 8 | count | 字段计数 | IntegerField |   |   | default=1 |
| 9 | min | 字段的最小值 | CharField(255) | 是 | 否 | default=&#39;NA&#39; |
| 10 | max | 字段的最大值 | CharField(255) | 是 | 否 | default=&#39;NA&#39; |
| 11 | average | 字段的平均值 | CharField(255) | 是 | 否 | default=&#39;NA&#39; |
| 12 | median | 字段的中值 | CharField(255) | 是 | 否 | default=&#39;NA&#39; |
| 13 | stddev | 字段的标准偏差（standard deviation） | CharField(255) | 是 | 否 | default=&#39;NA&#39; |
| 14 | sum | 字段的和 | CharField(255) | 是 | 否 | default=&#39;NA&#39; |
| 15 | unique\_values | 字段的唯一值 | TextField | 是 | 是 | default=&#39;NA&#39; |
| 16 | last\_stats\_updated | 最后更新状态时间 | DateTimeField |   |   | default=datetime.now |
| 17 | object |   | AttributeManager |   |   |   |



8.表 Document

from app documents models.py

表说明：文档是可以附加到地图的任何类型的信息，例如pdf，图像，视频，xls

| 序号 | 字段名 | 字段意义 | 字段类型 | 允许为NULL | 允许为空 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | content\_type | 内容类型 | ForeignKey(ContentType) | 是 | 是 |   |
| 2 | object\_id | 对象ID | PositiveIntegerField | 是 | 是 |   |
| 3 | resource |   | GenericForeignKey(&#39;content\_type&#39;,&#39;object\_id&#39;) |   |   |   |
| 4 | doc\_file | 文档文件存储位置 | FileField(upload\_to=&#39;documents&#39;，255) | 是 | 是 | verbose\_name=\_(&#39;File&#39;) |
| 5 | exension |   | CharField(128) | 是 | 是 |   |
| 6 | doc\_type | 文档类型 | CharField(128) | 是 | 是 |   |
| 7 | doc\_url | 文档url | URLField(255) | 是 | 是 | verbose\_name=\_(&#39;URL&#39;) |



9.表 GroupProfile

from app groups models.py

表说明：群组信息

| 序号 | 字段名 | 字段意义 | 字段类型 | 允许为NULL | 允许为空 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | group | 群组 | OneToOneField(Group) |   |   |   |
| 2 | title | 名称 | CharField(50) |   |   |   |
| 3 | slug | 短标题 | SlugField |   |   | unique |
| 4 | logo | 图标 | ImageField(upload\_to=&quot;people\_group&quot;) |   | 是 |   |
| 5 | description | 组描述 | TextField |   |   |   |
| 6 | email | 邮箱 | EmailField | 是 | 是 |   |
| 7 | keywords | 关键词 | TaggableManager |   | 是 |   |
| 8 | access | 权限 | CharField(15) |   |   | default=&#39;public&#39; |
| 9 | last\_modified | 最后修改时间 | DataTimeField(auto\_now=true) |   |   |   |



10.表 GroupMember

from app groups models.py

表说明：群组织的成员信息

| 序号 | 字段名 | 字段意义 | 字段类型 | 允许为NULL | 允许为空 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | group | 加入的群组 | ForeignKey(GroupProfile) |   |   |   |
| 2 | User | 用户 | ForeignKey(settings.AUTH\_USER\_MODEL) |   |   |   |
| 3 | role | 在群组中的角色 | CharField(10) |   |   |   |
| 4 | joined | 加入群组时间 | DataTimeField（default=datetime.datetime.now) |   |   |   |



11.表 GroupInvitation

from app groups models.py

表说明：群组邀请信息

| 序号 | 字段名 | 字段意义 | 字段类型 | 允许为NULL | 允许为空 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | group | 群组 | ForeignKey(GroupProfile) |   |   |   |
| 2 | token | 进群口令 | CharField(40) |   |   |   |
| 3 | email | 邮箱 | EmailField |   |   |   |
| 4 | user | 被邀请用户 | ForeignKey(settings.AUTH\_USER\_MODEL) |   |   |   |
| 5 | from\_user | 邀请者 | ForeignKey(settings.AUTH\_USER\_MODEL) |   |   |   |
| 6 | role | 角色 | CharField(10) |   |   |   |
| 7 | state | 状态 | CharField(10) |   |   |   |
| 8 | created | 记录建立时间 | DateTimeField(default=datetime.datetime.now) |   |   |   |
