---
title: Python 并发简介
date: '2022-10-12 12:32'
tags: Python
categories: Python
abbrlink: 59877
comment: 'cusdis'
---

<meta name="referrer" content="no-referrer" />

# Python 并发简介

![程序提速的方法](https://raw.githubusercontent.com/hedyvhan/Pictrue/master/img/202310122314876.png)

 - 多线程：threading，利用CPU和IO可以同时执行的原理，让CPU不会干巴巴的等待IO完成。
 - 多进程：multiprocessing，利用多核CPU的能力，真正并行执行任务。
 - 异步IO：asyncio，在单线程利用CPU和IO同时执行的原理，实现函数异步执行。

 - 使用 Lock对资源加锁，防止冲突访问
 - 使用Queue实现不同线程、进程之间的数据通信，实现生产者-消费者模式
 - 使用线程池Pool、进程池Pool，简化线程、进程的任务提交、等待结束、获取结果

## 一、多线程、多进程、多协程对比

| CPU密集型 <br />（CPU-bound） | CPU密集型也叫计算密集型，是指I/O在很短的时间就可以完成，CPU需要大量的计算和处理，特点是CPU占用率相当高<br/>例如：压缩解压缩、加密解密、正则表达式搜索 |
| :---------------------------: | ------------------------------------------------------------ |
|  IO密集型<br />（CPU-bound）  | IO密集型指的是系统运作大部分的状况是CPU在等I/O（硬盘/内存） 的读/写 操作，CPU占用率仍然较低。<br /> 例如：文件处理程序、网络爬虫程序、读写数据库程序 |

IO(读写内存、发送、网络等)

|                                  |              优点              |                             缺点                             |                         适用于                         |
| -------------------------------- | :----------------------------: | :----------------------------------------------------------: | :----------------------------------------------------: |
| 多进程Process（multiprocessing） |    可以利用多核CPU并行计算     |               占用资源最多、可启动数目比线程少               |                     CPU密集型计算                      |
| 多线程Thread (threading)         | 相比进程，更轻量级、占用资源少 | 相比进程：多线程只能并发执行，不能利用多CPU（GIL）（python多线程中只能使用单CPU） <br /> 相比协程：启动数目有限制，占用内存资源，有线程切换开销 |        IO密集型计算、同时运行的任务数目要求不多        |
| 多协程Coroutine(asyncio)         | 内存开销最少、启动协程数量最多 |                 支持的库有限制、代码实现复杂                 | IO密集型计算、需要超多任务运行、但有现成的库支持的场景 |

关系：进程 > 线程 > 协程，一个进程中可以启动多个线程，一个线程中可以启动多个协程。

##  二、GIL

### python速度慢的原因

1. 动态类型语言，边解释边执行
2. **GIL，无法利用多核CPU并发执行**

### GIL

同步线程的一种机制，使得任何时刻仅有一个线程在执行。在多核心处理器上，使用 GIL 的解释器也只允许同一时间执行一个线程

<img src="Python 并发简介.assets/GIL.png" style="zoom:50%;" />

为什么有GIL这个东西？避免多线程可能导致的一些变量的引用计数，为了能更好的清理内存空间，每个变量都加锁的话，会带来开销和死锁问题。简而言之：python设计初期，为了规避并发问题引入了GIL，现在想去除却去不掉

###  怎么规避GIL带来的限制？

1. 多线程threading机制依然是有用的，用于IO密集型计算

   - 因为在IO期间，线程会释放GIL，实现CPU和IO并行，因此多线程用于**IO密集型**计算依然可以大幅提升速度，
   
   
      - 但是多线程用于**CPU密集型**计算时，只会更加拖慢速度。
   
2. 使用multiprocessing的多进程机制实现并行计算、利用多核CPU优势

   - 为了应对GIL的问题，python提供了multi-processing

## 三、多线程编程

应用于IO密集型计算，比如几乎所有的网络后台服务、网络爬虫

### 引入模块

```python
from threading import Thread
```

###  新建、启动、等待结束

```python
t=Thread(target=func, args=(100, ))
t.start()
t.join()
```

### 多线程示例：（多线程适用于IO密集型）

```python
import threading
import time

# 定义爬取的函数，返回url，和当前url内容的长度
def craw(url):
    import requests
    r = requests.get(url)
    print(url,len(r.text))

# 定义单线程
def sigleThread():
    print("sigleThread start!")
    for url in urls:
        craw(url)
    print("sigleThread end!")

# 定义多线程
def multiThread():
    print("multiThread start!")
    threads = []
    for url in urls:
        t = threading.Thread( target = craw, args = (url,) ) # target = craw引用函数，加了括号就是调用函数，这里不是调用
                                                            # args = (url,)，逗号，是元组，不加逗号表明是字符串。
        threads.append(t)
    for thread in threads:
        thread.start()

    for thread in threads:
        thread.join()
    print("multiThread end!")


if __name__ == '__main__':
    urls = [  f'https://www.cnblogs.com/#p{page}' for page in range(1, 51)  ]

    # 调用单线程，观察时间
    start = time.time()
    sigleThread()
    end = time.time()
    print("sigleThread cost", end - start, "seconds")

    # 调用多线程，观察时间
    start = time.time()
    multiThread()
    end = time.time()
    print("multiThread  cost", end - start, "seconds")
```

结果为

```python
sigleThread start!
sigleThread end!
sigleThread cost 6.9972569942474365 seconds
multiThread start!
multiThread end!
multiThread  cost 0.26952552795410156 seconds

```



### 数据通信

```python
import queue
# 创建Queue
q = queue.Queue()
# 添加元素
q.put(item)
# 获取元素
item = q.get()
# 查看元素多少
q.qsize()
# 判断是否为空
q.empty()
# 判断是否已满
q.full()
```

#### 多线程数据通信示例：

####  Pipeline技术架构

<img src="Python 并发简介.assets/pipeline.png" style="zoom:50%;" />

##### 实现生产者消费者架构的爬虫

<img src="Python 并发简介.assets/生产者消费者爬虫的架构.png" style="zoom:50%;" />

```python
import threading
import time
import requests
from bs4 import BeautifulSoup
import queue

# 爬取
def craw(url):
    r = requests.get(url)
    return r.text

# 解析
def parse(html):
    # post - item - title
    soup = BeautifulSoup(html, "html.parser")
    links = soup.find_all("a", class_= "post-item-title")
    return [(link["href"], link.get_text()) for link in links]

# 生产者: 获取网页数据
def do_craw(url_queue: queue.Queue, html_queue: queue.Queue ):
    while True:
        url = url_queue.get()
        html = craw(url)
        # 将处理的结果放进html_queue里面
        html_queue.put(html)
        print(threading.current_thread().name, f"craw:{url}", "url_queue.size=", url_queue.qsize())
        time.sleep(0.5)

# 消费者：解析网页数据
def do_parse(html_queue:queue.Queue, fout):
    while True:
        html = html_queue.get()
        # 得到解析后的数据
        results = parse(html)
        for result in results:
            fout.write(str(result)+"\n")
        print(threading.current_thread().name, f"results.size",len(results), "html_queue.size=", html_queue.qsize())
        time.sleep(0.5)

if __name__ == "__main__":
    urls = [f'https://www.cnblogs.com/#p{page}' for page in range(1, 51)]
    url_queue = queue.Queue()
    html_queue = queue.Queue()
    # 将所有的url放入url_queue里面
    for url in urls:
        url_queue.put(url)

     # 3个生产者线程
    for index in range(3):
        t = threading.Thread(target=do_craw, args=(url_queue, html_queue), name=f"craw{index}")
        t.start()
    # 得到html_queue

    fout = open("data.txt","w")
    # 2个消费者线程
    for index in range(2):
        t = threading.Thread(target=do_parse, args=(html_queue, fout), name=f"parse{index}")
        t.start()

'''
	结果的解释：
	生产者负责获取网页数据，
    消费者负责解析生产者获取到的数据
    运行结果显示：
    url_queue（要获取数据的网页）逐渐减少，
    html_queue（生产者获取到的数据）在波动，因为生产者生产，消费者在消耗
    最后，生产者停止工作，消费者解析完剩下的数据
    
    |网页| --> |url_queue| --> |生产者 craw| --> |html_queue| --> |消费者 parse| --> result
'''
```

输出结果：

```python
craw0 craw:https://www.cnblogs.com/#p1 url_queue.size= 47
parse0 results.size 20 html_queue.size= 0
craw2 craw:https://www.cnblogs.com/#p3 url_queue.size= 47
parse1 results.size 20 html_queue.size= 0
craw1 craw:https://www.cnblogs.com/#p2 url_queue.size= 47
parse0 results.size 20 html_queue.size= 0
craw0 craw:https://www.cnblogs.com/#p4 url_queue.size= 44
parse1 results.size 20 html_queue.size= 0
craw2 craw:https://www.cnblogs.com/#p5 url_queue.size= 44
craw1 craw:https://www.cnblogs.com/#p6 url_queue.size= 44
parse0 results.size 20 html_queue.size= 1
parse1 results.size 20 html_queue.size= 0
craw2 craw:https://www.cnblogs.com/#p7 url_queue.size= 41
craw0 craw:https://www.cnblogs.com/#p8 url_queue.size= 41
craw1 craw:https://www.cnblogs.com/#p9 url_queue.size= 41
parse0 results.size 20 html_queue.size= 2
parse1 results.size 20 html_queue.size= 1
craw2 craw:https://www.cnblogs.com/#p10 url_queue.size= 38
craw0 craw:https://www.cnblogs.com/#p11 url_queue.size= 38
craw1 craw:https://www.cnblogs.com/#p12 url_queue.size= 38
parse0 results.size 20 html_queue.size= 3
parse1 results.size 20 html_queue.size= 2
craw2 craw:https://www.cnblogs.com/#p13 url_queue.size= 35
craw0 craw:https://www.cnblogs.com/#p14 url_queue.size= 35
parse0 results.size 20 html_queue.size= 3
craw1 craw:https://www.cnblogs.com/#p15 url_queue.size= 35
parse1 results.size 20 html_queue.size= 3
parse0 results.size 20 html_queue.size= 2
craw0 craw:https://www.cnblogs.com/#p16 url_queue.size= 32
craw2 craw:https://www.cnblogs.com/#p17 url_queue.size= 32
parse1 results.size 20 html_queue.size= 3
craw1 craw:https://www.cnblogs.com/#p18 url_queue.size= 32
parse0 results.size 20 html_queue.size= 3
parse1 results.size 20 html_queue.size= 2
craw0 craw:https://www.cnblogs.com/#p19 url_queue.size= 29
craw2 craw:https://www.cnblogs.com/#p20 url_queue.size= 29
craw1 craw:https://www.cnblogs.com/#p21 url_queue.size= 29
parse0 results.size 20 html_queue.size= 4
parse1 results.size 20 html_queue.size= 3
craw0 craw:https://www.cnblogs.com/#p22 url_queue.size= 26
craw2 craw:https://www.cnblogs.com/#p23 url_queue.size= 26
craw1 craw:https://www.cnblogs.com/#p24 url_queue.size= 26
parse0 results.size 20 html_queue.size= 5
parse1 results.size 20 html_queue.size= 4
craw0 craw:https://www.cnblogs.com/#p25 url_queue.size= 23
craw2 craw:https://www.cnblogs.com/#p26 url_queue.size= 23
craw1 craw:https://www.cnblogs.com/#p27 url_queue.size= 23
parse0 results.size 20 html_queue.size= 6
parse1 results.size 20 html_queue.size= 5
craw0 craw:https://www.cnblogs.com/#p28 url_queue.size= 20
parse0 results.size 20 html_queue.size= 5
craw2 craw:https://www.cnblogs.com/#p29 url_queue.size= 20
craw1 craw:https://www.cnblogs.com/#p30 url_queue.size= 20
parse1 results.size 20 html_queue.size= 6
parse0 results.size 20 html_queue.size= 5
craw0 craw:https://www.cnblogs.com/#p31 url_queue.size= 18
craw2 craw:https://www.cnblogs.com/#p32 url_queue.size= 17
parse1 results.size 20 html_queue.size= 6
craw1 craw:https://www.cnblogs.com/#p33 url_queue.size= 17
parse0 results.size 20 html_queue.size= 6
craw0 craw:https://www.cnblogs.com/#p34 url_queue.size= 15
parse1 results.size 20 html_queue.size= 6
craw2 craw:https://www.cnblogs.com/#p35 url_queue.size= 14
craw1 craw:https://www.cnblogs.com/#p36 url_queue.size= 14
parse0 results.size 20 html_queue.size= 7
parse1 results.size 20 html_queue.size= 6
craw0 craw:https://www.cnblogs.com/#p37 url_queue.size= 12
craw2 craw:https://www.cnblogs.com/#p38 url_queue.size= 11
craw1 craw:https://www.cnblogs.com/#p39 url_queue.size= 11
parse0 results.size 20 html_queue.size= 8
parse1 results.size 20 html_queue.size= 7
craw0 craw:https://www.cnblogs.com/#p40 url_queue.size= 9
craw2 craw:https://www.cnblogs.com/#p41 url_queue.size= 8
parse0 results.size 20 html_queue.size= 8
craw1 craw:https://www.cnblogs.com/#p42 url_queue.size= 8
parse1 results.size 20 html_queue.size= 8
craw0 craw:https://www.cnblogs.com/#p43 url_queue.size= 6
parse0 results.size 20 html_queue.size= 8
craw2 craw:https://www.cnblogs.com/#p44 url_queue.size= 5
craw1 craw:https://www.cnblogs.com/#p45 url_queue.size= 5
parse1 results.size 20 html_queue.size= 9
parse0 results.size 20 html_queue.size= 8
craw0 craw:https://www.cnblogs.com/#p46 url_queue.size= 3
craw2 craw:https://www.cnblogs.com/#p47 url_queue.size= 2
parse1 results.size 20 html_queue.size= 9
craw1 craw:https://www.cnblogs.com/#p48 url_queue.size= 2
parse0 results.size 20 html_queue.size= 9
craw0 craw:https://www.cnblogs.com/#p49 url_queue.size= 0
parse1 results.size 20 html_queue.size= 9
craw2 craw:https://www.cnblogs.com/#p50 url_queue.size= 0
parse0 results.size 20 html_queue.size= 9
parse1 results.size 20 html_queue.size= 8
parse0 results.size 20 html_queue.size= 7
parse1 results.size 20 html_queue.size= 6
parse0 results.size 20 html_queue.size= 5
parse1 results.size 20 html_queue.size= 4
parse0 results.size 20 html_queue.size= 3
parse1 results.size 20 html_queue.size= 2
parse0 results.size 20 html_queue.size= 1
parse1 results.size 20 html_queue.size= 0

Process finished with exit code -1

```



### 线程安全加锁

```python
from threading import Lock
lock = Lock()
with lock:
```

RLock和Lock的区别：

RLock支持嵌套锁，Lock只支持锁一次解一次，不支持嵌套锁。RLock又叫递归锁，Lock又叫互斥锁。如果Lock锁上没有解锁，再锁上一次，会造成死锁。死锁另外一种情况是由于竞争资源或由于彼此通信而造成阻塞的现象。

eg：两个线程函数func1和func2，分别被lock1和lock2锁上，在func1里（lock1未解锁）再用lock2上锁，在func2里在用lock1上锁.

### 信号量限制并发

- ```python
  from threading import Semaphore
  semaphre = Semaphore(10)
  with semaphre:
  ```

### 线程池

1. 线程池的原理![请添加图片描述](https://img-blog.csdnimg.cn/4c19043ac3f240568817f8ff7931f2fa.png)


2. 使用线程池的好处

   1. 提升性能：因为减去了大量新建、终止线程的开销，重用了线程资源
   2. 适用场景：适合处理突发性大量请求或者需要大量线程完成任务、但实际任务处理时间短（不适合单线程使用时间太长）
   3. 防御功能：能有效避免系统因为创建线程过多，而导致系统符合过大相应变慢等问题
   4. 代码优势：使用线程池的语法比自己新建线程、执行线程更加简洁

   

3. ThreadPoolExecutor的使用语法

   1. ```python
      from concurrent.futures import ThreadPoolExecutor
      with ThreadPoolExecutor() as pool:
          results = pool.map(func, args)
          # args 对应着 results
          # 需要一次准备好所有的参数
      ```
      
   2. ```python
      with ThreadPoolExecutor() as pool:
          future = pool.submit(func, 1)
          # 一个一个执行，一个arg对应一个future
          futures = [pool.submit(func, arg)  for arg in args]
          # 两种遍历方式
          # 1  等待按顺序返回
          for future in futures:
              print(future.result())
          # 2  哪个先好了先返回哪一个，返回顺序不定
          for future in as_completed(futures):
              print(future.result())
      ```

4. 使用线程池改造爬虫

   ```python
   import threading
   import time
   import requests
   from bs4 import BeautifulSoup
   import queue
   import concurrent.futures
   
   urls = [f'https://www.cnblogs.com/#p{page}' for page in range(1, 51)]
   
   # 爬取
   def craw(url):
       r = requests.get(url)
       return r.text
   
   # 解析
   def parse(html):
       # post - item - title
       soup = BeautifulSoup(html, "html.parser")
       links = soup.find_all("a", class_= "post-item-title")
       return [(link["href"], link.get_text()) for link in links]
   
   # craw多线程爬取
   # 使用线程池方式1
   with concurrent.futures.ThreadPoolExecutor() as pool:
       # 一下全部执行，urls需要一次性准备好，结果按顺序返回，htmls是排序好的
       htmls = pool.map(craw, urls)
       htmls = list(zip(urls, htmls))
       for url, html in htmls:
           print(url, len(html))
   print("craw over")
   
   # ******此已经得到url和获取的数据htmls*****
   
   # parse多线程解析
   # 使用使用线程池方式2，另外一种线程池方式
   with concurrent.futures.ThreadPoolExecutor() as pool:
       futures = {}
       for url, html in htmls:
           # 一个一个执行
           future = pool.submit(parse, html)
           futures[future] = url
       # 两种遍历
       
       # 1 顺序遍历
       # for future, url in futures.items():
       #     print(url, future.result())
       
       # 2 哪个任务先完成就先返回
       for future in concurrent.futures.as_completed(futures):
           url = futures[future]
           print(url, future.result())
   print("parse over")
   
   
   
   ```

   输出结果：

   ![](Python 并发简介.assets/线程池输出结果1.png)



### 使用线程池在Web服务中实现加速

```python
import flask
import json
import time
from concurrent.futures import ThreadPoolExecutor

app = flask.Flask(__name__)
pool = ThreadPoolExecutor()

# 模拟web服务
def read_file():
    time.sleep(0.1)
    return "file result"

def read_db():
    time.sleep(0.2)
    return "db result"

def read_api():
    time.sleep(0.3)
    return "api result"

@app.route("/")
def index():
    result_file = pool.submit(read_file)
    result_db = pool.submit(read_db)
    result_api = pool.submit(read_api)

    return json.dumps({
        "result_file": result_file.result(),
        "result_db": result_db.result(),
        "result_api": result_api.result(),
    })


if __name__ == "__main__":
    app.run()

'''
不用线程：0.1+0.2+0.3 = 600ms
使用线程：max(0.1, 0.2, 0.3) 

'''

```



## 多进程编程

如果遇到了 CPU密集型计算，线程自动切换反而变成了负担，多线程反而会降低执行速度，multiprocessing模块就是python为了解决GIL缺陷引入的模块，原理就是用多进程在多CPU上并发执行。

|             语法             | 多线程                                                       | 多进程                                                       |
| :--------------------------: | ------------------------------------------------------------ | ------------------------------------------------------------ |
|           引入模块           | `from threading import Thread`                               | `from multiprcessing import Prcoess`                         |
| 新建<br />启动<br />等待结束 | `t = Thread(target=func, args=(100,))`<br />`t.start`<br />`t.join()` | `p = Process(target=func, args=('bob',))`<br />`p.start`<br />`p.join()` |
|           数据通信           | import queue<br />`q = queue.Queue()`<br />`q.put(item)`<br />`item = q.get()` | `from multiprcessing import Queue`<br />`q = Queue()`<br />`q.put([42, None, 'hello']])`<br />`item = q.get()` |
|           安全加锁           | `from threading import Lock`<br />`lock = Lock()`<br />`with lock:`<br />    `pass` | `from multiprocessing import Lock`<br />`lock = Lock()`<br />`with lock:`<br />    `pass` |
|           池化技术           | `from concurrent.futures import ThreadPoolExecutor`<br />`with ThreadPoolExecutor() as pool:`<br/>    ` # 方法1` <br />   `results = pool.map(func, args)`<br/>   `# args 对应着results`<br />   `# 方法2 ` <br />   `future = pool.submit(func, 1)`<br />   `result = future.result()` | `from concurrent.futures import ProcessPoolExecutor`<br />`with ProcessPoolExecutor() as pool:`<br/>    ` # 方法1` <br />   `results = pool.map(func, args)`<br/>   `# args 对应着results`<br />   `# 方法2 ` <br />   `future = pool.submit(func, 1)`<br />   `result = future.result()` |

### 单线程、多线程、多进程对比

```python
import math
import time
import multiprocessing
from concurrent.futures import ThreadPoolExecutor, ProcessPoolExecutor

lst = [112272535095293] * 10

def isPrime(n):
    print(multiprocessing.current_process())
    if n < 2:
        return False
    if n == 2:
        return True
    if n % 2 == 0:
        return False
    for i in range(3, int(math.floor(math.sqrt(n)))+1, 2 ):
        if n % i == 0:
            return False
    return True

# 单线程
def single_thread():
    print("single_thread")
    for num in lst:
        isPrime(num)

# 多线程
def multi_thread():
    print("multi_thread")
    with ThreadPoolExecutor() as pool:
        pool.map(isPrime, lst)

# 多进程
def multi_process():
    print("multi_process")
    with ProcessPoolExecutor() as pool:
        # pool.map(isPrime, lst)
        for i in range(len(lst)):
            pool.submit(isPrime, lst[i])

if __name__ == '__main__':
    '''
    判断lst中所有的数，是否是素数
    '''
    start = time.time()
    single_thread()
    end = time.time()
    print("singleThread:", end - start)

    start = time.time()
    multi_thread()
    end = time.time()
    print("multiThread:", end - start)


    start = time.time()
    multi_process()
    end = time.time()
    print("multiProcess:", end - start)
```

输出结果：

```python
single_thread
<_MainProcess(MainProcess, started)>
<_MainProcess(MainProcess, started)>
<_MainProcess(MainProcess, started)>
<_MainProcess(MainProcess, started)>
<_MainProcess(MainProcess, started)>
<_MainProcess(MainProcess, started)>
<_MainProcess(MainProcess, started)>
<_MainProcess(MainProcess, started)>
<_MainProcess(MainProcess, started)>
<_MainProcess(MainProcess, started)>
singleThread: 3.6966350078582764
multi_thread
<_MainProcess(MainProcess, started)>
<_MainProcess(MainProcess, started)><_MainProcess(MainProcess, started)>

<_MainProcess(MainProcess, started)>
<_MainProcess(MainProcess, started)>
<_MainProcess(MainProcess, started)><_MainProcess(MainProcess, started)>
<_MainProcess(MainProcess, started)>

<_MainProcess(MainProcess, started)>
<_MainProcess(MainProcess, started)>
multiThread: 3.358914613723755
multi_process
<SpawnProcess(SpawnProcess-1, started)>
<SpawnProcess(SpawnProcess-3, started)>
<SpawnProcess(SpawnProcess-2, started)>
<SpawnProcess(SpawnProcess-4, started)>
<SpawnProcess(SpawnProcess-5, started)>
<SpawnProcess(SpawnProcess-6, started)>
<SpawnProcess(SpawnProcess-7, started)>
<SpawnProcess(SpawnProcess-8, started)>
<SpawnProcess(SpawnProcess-1, started)>
<SpawnProcess(SpawnProcess-6, started)>
multiProcess: 1.3042821884155273

Process finished with exit code 0
```



### 进程间通信

进程间相互独立

1. ![](https://raw.githubusercontent.com/hedyvhan/Pictrue/master/img/202310122315494.jpg)
2. ![](https://raw.githubusercontent.com/hedyvhan/Pictrue/master/img/202310122315002.jpg)
3. ![](https://raw.githubusercontent.com/hedyvhan/Pictrue/master/img/202310122315462.jpg)
3. ![](https://raw.githubusercontent.com/hedyvhan/Pictrue/master/img/202310122315833.jpg)
3. 

线程池里，multiporcessing.RLock() 不可使用

使用： 

```python
manager = multiprocessing.Manager()

lock = manager.RLock()
```

RLock 可以多次使用多次释放、递归锁

Lock 

对于 Lock 对象而言，如果一个线程连续两次进行 acquire 操作，那么由于第一次 acquire 之后没有 release。第二次 acquire 将挂起线程。这会导致 Lock 对象永远不会 release，使的线程死锁。RLock 对象允许一个线程多次对其进行 acquire 操作，因为在其内部通过一个 counter 变量维护着线程 acquire 的次数，而且每次的 acquire 操作必须有一个 release 操作与之对应，在所有的 release 操作完成之后，别的线程才能申请该 RLock 对象。

