# django中使用celery
## 1.安装 celery 和django-celery
```
pip install celery
pip install django-celery
# 注意celery和django版本的兼容性
```
## 2.建立celery app
### 在Django project下建立文件 __init__.py,添加一下代码:
```
from __future__ import absolute_import, unicode_literals
from .celery import app as celery_app

__all__ = ['celery_app']

```
### 在Django project下建立文件 celery.py, 添加代码:
```
from __future__ import absolute_import

import os

from celery import Celery
from django.conf import settings

# set the default Django settings module for the 'celery' program.
os.environ.setdefault("DJANGO_SETTINGS_MODULE", "django_server.settings")

app = Celery('django_server')

app.config_from_object('django.conf:settings')
app.autodiscover_tasks(lambda: settings.INSTALLED_APPS)
```
## 3.在配置celery settings
### 在django projet 的INSTALLED_APPS添加djcelery:
```
INSTALLED_APPS = (
'djcelery',
)
```
### 添加celery配置 (中央服务配置)
```
# ==========
# = Celery =
# ==========
djcelery.setup_loader()

BROKER_URL = 'amqp://zboper:rabbit123456@10.30.48.112:5672//'
CELERY_TASK_SERIALIZER = 'json'
CELERY_TIMEZONE = TIME_ZONE
CELERY_ENABLE_UTC = False
CELERY_IGNORE_RESULT = True
```
### 或本地配置 celery 任务
```
# ==========
# = Celery =
# ==========
djcelery.setup_loader()
CELERY_QUEUES = {
    "work_queue": {
        "exchange": "work_queue",
        "exchange_type": "direct",
        "binding_key": "work_queue"
    },
    "beat_tasks": {
        "exchange": "beat_tasks",
        "exchange_type": "direct",
        "binding_key": "beat_tasks"
    },
    "email": {
        "exchange": "email",
        "exchange_type": "direct",
        "binding_key": "email"
    },
    "message_tasks": {
        "exchange": "message_tasks",
        "exchange_type": "direct",
        "binding_key": "message_tasks"
    }
}

CELERY_DEFAULT_QUEUE = "work_queue"


CELERY_ACCEPT_CONTENT = ['json']
CELERY_TASK_SERIALIZER = 'json'
CELERY_RESULT_SERIALIZER = 'json'
CELERY_TIMEZONE = TIME_ZONE
CELERY_ENABLE_UTC = True
CELERY_IGNORE_RESULT = False

CELERYBEAT_SCHEDULE = {
   
    'bulletin-message': {
        'task': 'bulletin-message',
        'schedule': crontab(minute='0', hour='11'),  # 11
        'options': {'queue': 'message_tasks'},
        'args': (11,)
    },
    'bulletin-message1': {
        'task': 'bulletin-message',
        'schedule': crontab(minute='0', hour='16'),  # 16
        'options': {'queue': 'message_tasks'},
        'args': (16,)
    },
    'zone-new-org-message': {
        'task': 'zone-new-org-message',
        'schedule': crontab(minute='30', hour='9'),  # 9:30
        'options': {'queue': 'message_tasks'},
        'args': ()
    },
    'zone-activity-message': {
        'task': 'zone-activity-message',
        'schedule': crontab(minute='0', hour='17', day_of_week=5),  # 17:00 friday
        'options': {'queue': 'message_tasks'},
        'args': ()
    },
    'zone-state-message': {
        'task': 'zone-state-message',
        'schedule': crontab(minute='30', hour='9', day_of_week=1),  # 9:30  monday
        'options': {'queue': 'message_tasks'},
        'args': ()
    },
    }
```
### 4.在django app中添加ccelery的定时任务(crontab)任务
#### 在app下新建 tasks.py文件
```
from celery.task import Task


class MessageTask(Task):
  name = 'dynamic-message'
  
  def run(self, *args):
    a=1
    b=3
    return a+b
```

### 5.在django app中添加ccelery的即时任务(delay)任务
 ###  在app下新建 tasks.py文件
 ```
 from celery import shared_task
 
 @shared_task
def celery_export(*args):
  a=1
  b=3
  return a+b
  
```
### 在view.py中调用task
```
from .tasks import celery_export

class ExportViewSet(viewsets.ViewSet):
  def list(self, request, *args, **kwargs):
    celery_export.apply_sync((*args), queue='marketbox-svr-ict-staging')
    
```

## django 运行celery
```
python manage.py celery
```




