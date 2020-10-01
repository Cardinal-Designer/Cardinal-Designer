# Api

>API（Application Programming Interface，应用程序接口）降低组成单元间的耦合程度，从而提高系统的可维护性和可扩展性。

Cardinal 的 Api 是针对图包对外交互不丰富的情况下设计出来的具有程序核心功能的对外接口

Api不能独立于自编脚本而存在，只有自己编写扩展功能的Python脚本将其引用才能实现调用

**注意：所有__xx__形式的参数才可以更改，其他模板中的字均为关键字，不可更改**

## 注册脚本的配置

### 注册模板
```json
"Import": {
    "__name__": {
        "WorkPath": ["__Plugin__"],
        "module_name": "__Extensions__",
        "init": {
            "Target": ["__Target__"],
            "kwargs": {"__keyword__":"__content__"},
            "lock": true
        }
    }
}
```
Target 是指 [对象] 为了方便调用编程接口，所以采取按照层次获取成员函数的书写方式。

kwargs 是指 [关键字参数] 是一种依靠关键字传入参数的方式

### 例子
文件位置: 图包根目录>插件>T  
文件名称: mod.py
```python
class Func():
    def I(W):
        print(W)
Use = Func()
```

如果我需要在扩展被加载时初始化并打印输出 "Nice to meet you" ，并且在引用时把这个扩展叫做Hello_World那么:

module_name 为 去除文件后缀的文件名称 即 mod
WorkPath 为 子目录名称，目前展示的是多级子目录的写法
```json
"Import": {
    "Hello_World": {
        "WorkPath": ["插件","T"],
        "module_name": "mod",
        "init": {
            "Target": ["Use"],
            "kwargs": {"W":"Nice to meet you"},
            "lock": true
        }
    }
}
```



在基本触发语句OnClick中的Actions调用书写格式：

```json
{
    "From": "Import",
    "locate": [false,157,187,4,49],
    "Action": {
        "module": "Script",
        "Target": ["MoveAround"],
        "kwargs": {},
        "lock": true
    }
}
```

