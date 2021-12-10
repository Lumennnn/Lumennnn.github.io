---
title: python基础模块学习
date: 2021-03-13 23:19:30
index_img: https://resource.liangzai.online/resource/python.png
categories:
  - 计算机学习
tags:
    -python
    -基础
---
Python基础模块的了解和学习

<!-- more -->

## 内置模块

🎉

### time模块

1. 时间获取函数

   ```python
   import time
   print(time.time())  # 获取当前时间戳
   print(time.ctime()) # 获取当前时间并以易读方式表示，返回字符串
   print(time.gmtime()) # 获取当前时间，表示为计算机可处理的时间格式,UTC时间，以格式化模板输出  <UTC：协调世界时>
   print(time.asctime()) # 未被定义，表示当前时间
   print(time.localtime()) # 输出当前时间，以格式化模板输出,本地时间
   ```

   输出：

   ```bash
   1615626615.496064
   Sat Mar 13 17:10:15 2021
   time.struct_time(tm_year=2021, tm_mon=3, tm_mday=13, tm_hour=9, tm_min=10, tm_sec=15, tm_wday=5, tm_yday=72, tm_isdst=0)
   Sat Mar 13 17:10:15 2021
   time.struct_time(tm_year=2021, tm_mon=3, tm_mday=13, tm_hour=17, tm_min=10, tm_sec=15, tm_wday=5, tm_yday=72, tm_isdst=0)
   ```

2. 时间格式化

   ```python
   import time
   t = time.gmtime()
   t1 = time.strftime("%Y-%m-%d %H:%M:%S",t)    # 格式化时间
   t2 = time.strptime(t1,"%Y-%m-%d %H:%M:%S")   # 转化时间格式
   print(t1,t2)
   ```

   输出：

   ```bash
   2021-03-13 08:26:17
   time.struct_time(tm_year=2021, tm_mon=3, tm_mday=13, tm_hour=8, tm_min=45, tm_sec=48, tm_wday=5, tm_yday=72, tm_isdst=-1)
   ```

   ![格式化字符串对应属性](https://resource.liangzai.online/notebook/20210313234205.png#pic_left)

   ```python
   import time    # 返回一个CPU级别的精确时间计数，单位为秒
   start = time.perf_counter()
   time.sleep(3)    # 模拟休眠，可以是浮点数。推迟调用线程的运行，可通过参数 secs 指秒数，表示进程挂起的时间。
   end = time.perf_counter()
   print(end - start)
   ```

   输出：

   ```bash
   3.004556
   ```

   > perf_counter()适合小一点的程序测试，会计算sleep()时间。
   > time()精确度不高，而且受系统影响，适合表示日期或者大程序的计时。
   >

   ---

### os模块

1. os模块

   ```python
   import os

   os.listdir("path")[:]  # 返回一个列表。列表为给定目录下所有文件和子目录，但不包含特殊目录 . 和 ..。默认为当前目录。
   os.makedirs("path")  # 递归方式创建路径为 path 的目录。并以数字形式指定目录权限，默认权限为 777 。可以看作功能更强大的 mkdir，它会自动创建叶子节点目录的所有上级目录，而 mkdir 必须在上级目录已经存在情况下，才能创建叶子节点的目录。
   os.rmdir("path")  # 删除目录。目录必须存在，并且只能删除空目录。不存在或不为空，都会异常。要想递归删除整个目录树，请使用 shutil.rmtree()。
   os.removedirs("parent/child/newdir")  # 递归删除目录。目录必须存在，并且只能删除空目录。不存在或不为空，都会异常。与 rmdir 不同的是，在删除了叶子节点目录后，会逐次删除上级目录，直到遇到不为空的目录。
   os.remove("dog.copy.jpeg")  # 删除文件。不能删除目录，给定路径必须为文件，否则会异常。
   os.getenv("PATH")  # 获取环境变量。  getenv(key, default=None)
   os.get_exec_path("path")  # 返回用于搜索可执行文件的目录列表。看以看作是 PATH 环境变量的列表形式。
   os.rename("name","newname")  # 重命名文件
   os.remove()  # 删除文件
   os.getcwd()  # 获取当前工作路径
   os.walk()    # 遍历目录
   os.chdir()   # 改变当前工作目录
   ```

2. os.path模块

   ```python
   os.path.join()  # 连接目录与文件名
   os.path.split() # 分割文件名与目录
   os.path.abspath()  # 获取绝对路径
   os.path.dirname()  # 获取路径
   os.path.basename() # 获取文件名或文件夹名
   os.path.splitext() # 分离文件名与扩展名
   os.path.isfile()   # 判断所给出的路径是否是一个文件
   os.path.isdir()    # 判断给出的路径是否是一个目录
   ```

   ---

### json模块

1. dumps和dump

   ```python
   import json
   # json.dumps(obj, skipkeys=False, ensure_ascii=True, check_circular=True, allow_nan=True, cls=None, indent=None, separators=None, encoding="utf-8", default=None, sort_keys=False, **kw)
   # 将 Python 对象编码成 JSON 字符串
   data = [ { 'a' : 1, 'b' : 2, 'c' : 3, 'd' : 4, 'e' : 5 } ]
   data2 = json.dumps(data)
   data3 = json.dumps({'a': 'Runoob', 'b': 7}, sort_keys=True, indent=4, separators=(',', ': '))
   print(data2,data3,sep='\n')

   # 使用 dumps（）：将可以转换为 json 对象的对象转换为 String，然后可通过字符流或字节流写入文件
   def save_conf(confiuration_path, pre_trans_obj):
   #先用dunps转为string，然后字符流写入
   #ensure_ascii=False, 减少乱码
       json_string = json.dumps(pre_trans_obj, ensure_ascii=False)
       with open(confiuration_path,'w') as f:
           f.write(json_string)

   # 使用 dump（）：将可转为 json 对象的对象直接写入文件（将两个步骤结合成一个步骤）
   def save_conf(confiuration_path, pre_trans_obj):
       with open（confiuration_path,'w') as f:
           json.dump(pre_trans_obj, f, ensure_ascii=False)

   ```

   输出：

   ```bash
   [{"a": 1, "b": 2, "c": 3, "d": 4, "e": 5}]
   {
   "a": "Runoob",
   "b": 7
   }
   ```

   <!-- 表格（table） -->

   **Python原始类型向Json类型的转换对照表：**

   |     Python     |  Json  |
   | :--------------: | :------: |
   |      dict      | object |
   |   list,tuple   | array |
   |  str,unicode  | string |
   | int,long.float | number |
   |      True      |  true  |
   |     False     | fasle |
   |      None      |  null  |
2. loads和load

   ```python
   import json
   # json.loads(s[, encoding[, cls[, object_hook[, parse_float[, parse_int[, parse_constant[, object_pairs_hook[, **kw]]]]]]]])
   # 用于解码 JSON 数据。该函数返回 Python 字段的数据类型。
   jsonData = '{"a":1,"b":2,"c":3,"d":4,"e":5}';
   text = json.loads(jsonData)
   print(text)

   # 加载配置，configuration_path：配置文件路径
   # 使用 loads（string）：作用将 string 类型转为 dict 字典或 dict 链表
   def load_conf(configuration_path):
       with open(configuration_path, 'r') as f:
           string = f.read()
       return json.loads(string)

   # 使用 load（file_stream）：作用从文件流直接读取并转换为 dict 字典或 dict 字典链表
   def load_conf(configuration_path):
       with open(configuration_path, 'r') as f:
           data = json.load(f)
       return data
   ```

   输出：

   ```bash
   {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}
   ```

   **Python原始类型向Json类型的转换对照表：**

   |     Json     |  Python  |
   | :------------: | :--------: |
   |    object    |   dict   |
   |    array    |   list   |
   |    string    | unicode |
   | number(int) | int,long |
   | number(real) |  float  |
   |     true     |   True   |
   |    false    |  False  |
   |     null     |   None   |
3. 大 JSON 字符串

   ```python
   import tempfile
   data = [{'name':'rocky','like':('python','c++'),'age':23}]
   f = tempfile.NamedTemporaryFile(mode = 'w+')
   json.dump(data,f)
   f.flush()
   print(open(f.name,'r').read())
   ```

   输出：

   ```bash
   [{"name": "rocky", "like": ["python", "c++"], "age": 23}]
   ```

   > Python 中提供了一个 tempfile 的模块来解决json数据量大时内存溢出的问题
   >

   ---

### Random模块

1. random模块随机生成元素

   ```python
   import random
   print(random.random())  # 生成0到1之间的一个随机浮点数
   print(random.randint(1,10))  # 生成1到10的一个整数型随机数
   print(random.uniform(1.1,5.4))  # 生成1.1到5.4之间的随机浮点数，区间可以不是整数
   print(random.randrange(1,100,2))  # 生成1到100的间隔为2的随机整数
   ```

   输出：

   ```bash
   0.10421592338776642
   9
   1.7904868611069884
   87
   ```

2. random模块随机选取元素

   ```python
   import random
   l = [1,2,3,4,5]
   print(random.choice(l))  # 从对象中随机抽取一个元素
   random.shuffle(l)  # 将对象序列打乱,该函数没有返回值，完成一种功能，就是对list进行排序打乱
   print(l)
   print(random.choice("tomorrow"))  # 从序列中随机选取一个元素
   print(random.sample("tomorrow",3))  # 从对象中随机抽取指定数量的随机字符
   import string
   print("".join(random.sample(string.ascii_letters + string.digits, 8)))  # 从a-z,A-Z中生成指定数量的随机字符
   ```

   输出：

   ```bash
   5
   [3, 5, 4, 1, 2]
   o
   ['r', 'o', 'o']
   qOnfit8x

   ```

### IO模块

1. StringIO使用

   ```python
   from io import StringIO  # 类似文件的缓冲区
   cache_file = StringIO()
   print(cache_file.write('hello world')) # 11
   print(cache_file.seek(0)) # 让指针移动到最开始的位置，否则读取不到内容（写入后指针在最末尾）
   print(cache_file.read()) # 读取写入的内容
   print(cache_file.close())  # 释放缓冲区（在关闭文件的缓冲区之后就不能再进行读写操作了）
   # getvalue () 方法：直接获得写入后的 str
   ```

   输出：

   ```bash
   11
   0
   hello world
   None
   ```

2. BytesIO使用

   ```python
   from io import BytesIO  # 类似文件的缓冲区
   bytes_file = BytesIO()  # 操作二进制数据，需要使用 BytesIO
   bytes_file.write(b'hello world')  # BytesIO 实现了在内存中读写 bytes，写入的不是 str，而是经过 UTF-8 编码的 bytes
   bytes_file.seek(0)
   print(bytes_file.read()) # b'hello world'
   bytes_file.close()
   ```

   输出：

   ```bash
   b'hello world'
   ```

### String模块

1. 常用函数

   |                     常用函数                     |                               说明                               |
   | :------------------------------------------------: | :----------------------------------------------------------------: |
   |               **str.capitalize()**               |                         字符串首字母大写                         |
   |              **str.center(width)**              |     字符串用空格填充成一个长度为width的字符串，原字符串居中     |
   |                 str.ljust(width)                 |   返回一个原字符串左对齐的并使用空格填充至长度width的新字符串   |
   |                 str.rjust(width)                 |   返回一个原字符串右对齐的并使用空格填充至长度width的新字符串   |
   |                 str.zfill(width)                 |      返回长度为width的字符串，原字符串str右对齐，前面填充0      |
   |                **str.counts(s)**                |                   返回字符串s在str中出现的次数                   |
   | **str.decode(encoding='UTF-8',errors='strict')** |                     以指定编码格式解码字符串                     |
   | **str.encode(encoding='UTF-8',errors='strict')** |                     以指定编码格式编码字符串                     |
   |                **str.endwith(s)**                |                  判断字符串str是否以字符串s结尾                  |
   |              **str.startswith(s)**              |      检查字符串str是否以s开头，是则返回True，否则返回False      |
   |                 **str.find(s)**                 |         返回字符串s在字符串str中的位置索引，没有则返回-1         |
   |               **str.replace(a,b)**               |                    将字符串中str中的a替换成b                    |
   |                 **str.split(s)**                 |                        以s为分隔符切片str                        |
   |              **str.splitlines(s)**              |            按照行分隔，返回一个包含各行作为元素的列表            |
   |                   str.rfind(s)                   |                 类似于find()函数，但是从右边开始                 |
   |                   str.index(s)                   |          和find()方法一样，但如果s不存在与str则抛出异常          |
   |                  str.rindex(s)                  |                类似于index()函数，但是从右边开始                |
   |                  str.isalunm()                  | 如果str至少有一个字符并且都是字母或者数字则返回True否则返回False |
   |                  str.isalpha()                  |     如果str至少有一个字符并且都是字母则返回True否则返回False     |
   |                  str.isdigit()                  |             如果str只包含数字则返回True否则返回False             |
   |                  str.isspace()                  |          如果str中只包括空格，则返回True，否则返回False          |
   |                  str.istitle()                  |          如果str是首字母大写的则返回True，否则返回False          |
   |                 **str.title()**                 |    返回标题化的str，所有单词都是以大写开始，其余字母均为小写    |
   |                 **str.upper()**                 |                 返回str所有字符串为大写的字符串                 |
   |                 **str.lower()**                 |                   转换str中所有大写字符为小写                   |
   |                  str.isupper()                  | 如果str存在区分大小写的字符，并且都是大写则返回True否则返回False |
   |                  str.islower()                  | 如果str存在区分大小写的字符，并且都是小写则返回True否则返回False |
   |                   str.lstrip()                   |                     去掉str左边的不可见字符                     |
   |                   str.rstrip()                   |                     去掉str右边的不可见字符                     |
   |                 **str.strip()**                 |                 等同于同时执行rstrip()和lstrip()                 |
   |                 str.partiton(s)                 |                       用s将str切分成三个值                       |
   |                str.rpartition(s)                |            类似于partition()函数，但是从右边开始查找            |
2. 字符串常量

   |          常量          |                            含义                            |
   | :----------------------: | :----------------------------------------------------------: |
   | string.ascii_lowercase |                        小写字母a-z                        |
   | string.ascii_uppercase |                        大写字母A-Z                        |
   |  string.ascii_letters  | string.ascii_lowercase和string.ascii_uppercase常量的连接串 |
   |     string.digits     |                       字符串数字0-9                       |
   |    string.hexdigits    |               字符串'0123456789abcdefABCDEF'               |
   |     string.letters     |                         字符串a-Z'                         |
   |    string.octdigits    |                      字符串'01234567                      |
   |    string.lowercase    |                      小写字母的字符串                      |
   |    string.uppercase    |                      大写字母的字符串                      |
   |   string.punctuation   |                        所有标点符号                        |
   |   string.whitespace   |                  空白字符'\t\n\x0b\xoc\r'                  |
3. 字符串模板Template（使用时查询）

### Math模块

1. 常用函数

   |         函数         |                      说明                      |
   | :---------------------: | :-----------------------------------------------: |
   |      **math.e**      |                    自然常数e                    |
   |      **math.p**      |                    圆周率pi                    |
   |    math.degrees(x)    |                    弧度转度                    |
   |    math.radians(x)    |                    度转弧度                    |
   |      math.exp(x)      |                  返回e的x次方                  |
   |     math.expm1(x)     |                返回e的x次方减一                |
   |  math.log(x[,base])  |      返回x的以base为底的对数，base默认为e      |
   |     math.log10(x)     |              返回x的以10为底的对数              |
   |     math.log1p(x)     |          返回1+x的自然对数（以e为底）          |
   |     math.pow(x,y)     |                  返回x的y次方                  |
   |     math.sqrt(x)     |                  返回x的平方根                  |
   |   **math.ceil(x)**   |                返回不小于x的整数                |
   |   **math.floor(x)**   |                返回不大于x的整数                |
   |     math.trunc(x)     |                 返回x的整数部分                 |
   |     math.modf(x)     |                返回x的小数和整数                |
   |     math.fmod(x)     |                 返回x%y（取余）                 |
   |     math.fabs(x)     |                  返回x的绝对值                  |
   | math.fsum([x,y,...]) |                返回无损精度的和                |
   | **math.factorial(x)** |                   返回x的阶乘                   |
   |     math.isinf(X)     |     若x为无穷大，返回True；否则，返回False     |
   |   **math.isnan(x)**   |     若x不是数字，返回True；否则，返回False     |
   |   math.hypot(x, y)   |           返回以x和y为直角边的斜边长           |
   |  math.copysign(x, y)  | 若y<0，返回-1乘以x的绝对值；否则，返回x的绝对值 |
   |      math.sin(x)      |            返回x（弧度）的三角正弦值            |
   |     math.asin(x)     |               返回x的反三角正弦值               |
   |      math.cos(x)      |            返回x（弧度）的三角余弦值            |
   |     math.acos(x)     |               返回x的反三角余弦值               |
   |      math.tan(x)      |            返回x（弧度）的三角正切值            |
   |     math.atan(x)     |               返回x的反三角正切值               |
   |   math.atan2(x, y)   |              返回x/y的反三角正切值              |
   |         ……         |                      ……                      |
