# python

## Python 判断列表不为空

在 Python 中，False,0,’’,[],{},()都视为假，因此可以直接进行逻辑运算。此方法效率最高

## post/get 请求

使用 requests 包

```python
import requests
headers = {
    "Accept": "application/json"
}
response = requests.post(url,headers=headers)
res = response.json()

requests.get(url,headers=headers)
```
