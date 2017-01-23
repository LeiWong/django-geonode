#GeoNode groups API

geonode 的group模块提供了组织或群体的社区功能，允许用户或组织创建一个群组，可以邀请其他的用户加入该群组，进行社区相关活动，同时可以进行对群组或用户的移除、更新等相关操作，该模块增进了用户之间的联系与交流。


##方法：group_create
功能说明：创建群组

接口URL：/create

请求方式：post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|slug|群组简称|是|对群组的简短描述|--|

返回参数：

##方法：group_update
功能说明：更新群组信息

接口URL：/slug/update

请求方式：post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|slug|群组简称|是|---|---|

返回参数：

##方法：group_members
功能说明：群组成员

接口URL：/slug/members

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|slug|群组简称|是|---|---|

返回参数：

##方法：group_members_add
功能说明：添加群组成员

接口URL：/slug/members_add

请求方式：post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|role|角色|是|成员性质|member/manager|
|user_idntifiers|用户认证|是|--|---|

返回参数：

##方法：group_member_remove
功能说明：移除群组成员

接口URL：/slug/member_remove/username

请求方式：

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|slug|群组名字|是|---|---|
|username|用户名|是|移除用户的名字|---|

返回参数：

## 方法：group_join
功能说明：加入群组

接口URL：/slug/join

请求方式：post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|slug|群组名字|是|---|---|

返回参数：

##方法：group_invite
功能说明：邀请用户加入群组

接口URL：/slug/invite

请求方式：post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|slug|群组名字|是|---|---|
|invite_role|角色|是|成员性质|member/manager|
|invite_user|邀请用户|是|---|--|

返回参数：slug=group.slug

##方法：group_invite_response
功能说明：回应群组邀请

接口URL：/group/\w/invite/token/

请求方式：post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|token|口令|是||---|---|

返回参数：ctx={”invite“：invite}

##方法：group_remove
功能说明：移除群组，请求方式为get，表示加载删除页面，请求方式为post，表示执行删除操作

接口URL：/slug/remove

请求方式：get/post

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|slug|群组名字|是|删除的群组名称|---|

##类：GroupActivityView
功能说明：返回最近的群组活动

接口URL：group/slug/activity

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|slug|群组名字|是|---|---|


##类：GroupDetailView
功能说明：混合group和member的信息

接口URL：/group/slug

请求方式：get

参数说明：

| 参数 | 名字 | 是否必须 | 说明 | 示例 |
| --- | --- | --- | --- | --- |
|slug|群组名字|是|---|---|





