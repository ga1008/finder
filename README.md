这是做什么的？
=======================
这是一个任意文件查找器，支持文件夹，文件名以及文件内容的关键字查找，支持正则模式，并且用突出颜色显示

怎么安装？
=========
pip install finder

怎么使用
=========

### 1. 在终端直接使用：

```
$ finder -k "要查找关键字" [-f --folder] [-o --filename_only] [-r --re_mode]
```

#### 参数解释：

##### -h, --help          ---> 显示帮助

##### -k, --keyword       ---> 要查找的关键字，必须值

##### -f, --folder        ---> 需要查找的文件夹，默认在运行目录下

##### -r, --re_mode       ---> y/n 是否以正则方式查找，默认n

##### -o, --filename_only ---> y/n 是否只查找文件夹名和文件名，默认n


#### 示例：

```shell script

# 当前文件夹下查找所有符合关键字的文件内容
$ finder -k "good job"
# in file [ /root/Finder/README.md ]: 
# >>> [ 36 ] [ $ finder -k "good job" ]

# 上面输出的是当前 README 文件的第36行，找到了需要的关键字

# 在指定文件夹下查找关键字：
$ finder -k "nice job" -f "/root/search_folder"

# 在当前文件夹下查找带有关键字的文件夹名或者文件名：
$ finder -k "finder" -o y
# >>> [ folder ] [ /root/Finder/finder.egg-info ]
# >>> [ folder ] [ /root/Finder/build/lib/finder ]
# >>> [ file name ] [ /root/Finder/finder/finder.py ]
# >>> [ folder ] [ /root/Finder/finder ]
# ...

# 正则模式查找所有以 .py 结尾的行：
$ finder -k ".*?\.py$" -r y
# in file [ /root/Finder/finder.egg-info/SOURCES.txt ]: 
# >>> [ 2 ] [ setup.py ]
# >>> [ 3 ] [ finder/__init__.py ]
# >>> [ 4 ] [ finder/finder.py ]

# 正则模式查找所有以 .py 结尾的文件夹和文件名：
$ finder -k ".*?\.py$" -r y -o y
# >>> [ file name ] [ /root/Finder/setup.py ]
# >>> [ file name ] [ /root/Finder/build/lib/finder/finder.py ]
# >>> [ file name ] [ /root/Finder/build/lib/finder/__init__.py ]
# >>> [ file name ] [ /root/Finder/finder/finder.py ]
# >>> [ file name ] [ /root/Finder/finder/__init__.py ]

# 正则模式查找所有带有 0.1 版本字样的行：
$ finder -k "[Vv]ersion[\': ]+0\.1\.\d" -r y
# in file [ /root/Finder/setup.py ]: 
# >>> [ 8 ] [ 'version': '0.1.0', ]

# in file [ /root/Finder/finder.egg-info/PKG-INFO ]: 
# >>> [ 3 ] [ Version: 0.1.0 ]

```


### 2. 在代码中调用：

#### 下载 Finder/finder/finder.py 文件到你的代码目录中

```
from finder import Finder

folder = "/root/search_folder"
kw = "正则表达式或者关键字"
fn_only = False     # 如果只返回文件夹或文件夹名则 True
re_mode = False     # 如果kw是正则表达式则 True

fd = Finder(folder, kw, fn_only, re_mode, True)
res = fd.start()

print(res)
```