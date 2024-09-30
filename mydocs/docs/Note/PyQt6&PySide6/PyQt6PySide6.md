# PyQt6/PySide6

## 前期配置与界面设计

要用到Qt designer，找到官网发现只有试用版，后来了解到Pyside6包中有`Qtdesigner.exe`可以直接用：

设计登陆界面用Widget就可以了

![](.\picture\image-20240806161247195.png)

`ctrl + R`可以预览窗口，一些基本的设计略过不记，最后界面如下（密码处设计了暗文处理）

![](.\picture\image-20240806171046350.png)

将ui文件转化为python文件时，我先是采用了使用pyuic，过程大致如下：

> 在Pycharm设置界面找到 工具 -> 外部工具
>
> 在编辑工具对话框里填写：
>
> - **名称**: PyUIC
> - **描述**: File of .ui be converted to .py
> - **程序**: 选择 `python.exe` 的文件路径
> - **参数**: 填写
>   ```
>   -m PyQt5.uic.pyuic $FileName$ -o $FileNameWithoutExtension$.py
>   ```
> - **工作目录**: 选择 `ui` 文件存放的目录
>

但最后出来的Python文件报错，可能是没有设置虚拟环境，或者是因为这个方法是适用于PyQt5的，而我采用的是Pyside6目录下的`Qt designer.exe`进行开发的，应该是有不兼容

采用`pyside6`将`ui`文件转换为`py`即可行：（在`ui`文件目录下执行）

```
pyside6-uic <name>.ui -o <name>.py
```

## 数据库操作工具包dbUtil.py封装

先在SQLyog中新建一个数据库，再在项目文件里进行连接：

```python
from pymysql import Connection


def getCon():
    """
    获取数据连接
    :return: 数据库连接
    """
    con = Connection(
        host="localhost",    # 主机名
        port=3306,           # 端口
        user="root",         # 账户
        password="Zqc20040813",   # 密码
        database="db_book",  # 数据库
        autocommit=True      # 设置自动提交
    )
    return con


def closeCon(con: Connection):
    """
    关闭数据库连接
    :param con: 数据库连接
    :return:
    """
    if con:
        con.close()
```

测试是否能连接：

```python
if __name__ == '__main__':
    con = None
    try:
        con = getCon()
        cursor = con.cursor()
        cursor.execute("SELECT * FROM t_user")
        print(cursor.fetchall())
    except Exception as e:
        print(e)
    finally:
        closeCon(con)
```

```
output:
((1, 'test', '1234'),)
```

## 实现登录功能





