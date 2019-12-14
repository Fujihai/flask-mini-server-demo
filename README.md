# flask-mini-server-demo

> 基于 Python Flask 框架，用于前端接口调试的后端 Demo，简单易用。

## 模板示例

```python
from flask import Flask, request
from flask_cors import *
import json
import time
import copy
import random
import os

app = Flask(__name__)
CORS(app, supports_credentials=True, resources=r'/*')

CORS(app)

@app.route('/')
def index():
  return 'Hello,Python Flask!'

app.run(debug=True, host='0.0.0.0', port=8000)
```

注意：浏览器测试访问时，需要将 host 的 ip 地址由 `0.0.0.0` 改成实际的 ip 地址。

## 路由

路由通过 `app.route` 进行设置 ，通过 `ip 地址:端口号 + 路由` 访问。

```python
@app.route('/api/name')
def name():
  return 'Name: Leif'
```

## 请求方法

GET 请求方法设置。此方法默认，可不设置。

```python
@app.route('/api/info', methods=['GET'])
```

POST 请求方法设置。

```python
@app.route('/api/info', methods=['POST'])
```

## 请求参数读取

GET 请求参数读取，通过 `request.args.get('参数名')`

```python
@app.route('/api/info', methods=['GET'])
def info():
  type = request.args.get('type')
  time = request.args.get('time')
```

POST 请求参数读取，通过 `request.form.get(字段名)`

```python
@app.route('/api/params', methods=['POST'])
def params():
  # browser & os & computer & folder
  browser = request.form.get('browser')
  os = request.form.get('os')
  computer = request.form.get('computer')
  folder = request.form.get('folder')
```

## 图片读取与保存

```python
@app.route('/api/pic', methods=['POST'])
def pic():
  img = request.files.get('file')
  if img is None:
    return json.dumps({'msg': 'File upload fail!'})
  else:
    img.save(img.filename)
    return json.dumps({'msg': 'File upload success!'})
```

## 返回错误码返回

```python
@app.route('/api/stcode')
def statusCode():
  return json.dumps({'retcode': 0}), 411
```

## json 文件读取

```python
with open('./table.json', 'r+') as f:
  data = json.loads(f.read())

@app.route('/api/json')
def getJson():
  return json.dumps(data)
```

