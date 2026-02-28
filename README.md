# CS 61A cats

## 前言
除了可选的Final Diff，其他problem包括EC(extra challenge)的实现都已完成且通过测试

下面的内容，由于本人知识储备不足，有一些与ai交流后得到的结果，可能存在错误，欢迎批评指正

注意：运行所有命令时，都要在最后加上`--local`，否则会要求输入ucb的邮箱

## 前置知识要求
学完Containers那一讲即可做，但会用到tuple的知识（keys必须是不能改变的），我记得lecture里好像没讲过
## Problem的注意点
具体见`cats.py`

2注意用utils.py里的函数
\
\
5用min函数，使用key参数会更快
\
\
6、7递归的思路都是从左到右一个一个字母来
\
\
base case就是limit小于0或者typed或source有一个变成空字符串了
\
\
9、10创建一个已知元素个数的列表，如
`fast_list = [[] for _ in player_indices]`



## Extra Challenge解答
Decorators要看明白，有点绕
```python
def decorator(f):
    ...

# 那么
@decorator
def function():
    ...
# 等价于
def function():
    ...
function = decorator(function)
```
---
### 重点
>最容易出问题的是Problem 7的那个函数没有把递归次数减到最少
\
首先add、substitute和remove的递归因为都把第一个字母调成一样的了，所以等价成直接进入typed和sourced第一个字母一样的情形，详见代码
```python
add = minimum_mewtations(typed+source[0],source[1:],limit-1)+1 
# 等价于
add = minimum_mewtations(typed,source[1:],limit-1)+1
# 减少一次调用
```

>base case中如果typed和source的长度之差的绝对值（设为a）大于limit了，最后调成一样的单词，长度一样，所以至少要进行a次remove，已经超过limit了，就不用后面的递归了，直接返回limit + 1



## 文件夹内容(摘自24Fall官网)
You can download all of the project code as a zip archive. This project includes several files, but your changes will be made only to `cats.py`. Here are the files included in the archive:

- `cats.py`: The typing test logic.

/
- `utils.py`: Utility functions for interacting with files and strings.

\
- `ucb.py`: Utility functions for CS 61A projects.

/  
- `data/sample_paragraphs.txt`: Text samples to be typed. These are scraped Wikipedia articles about various subjects.

\
- `data/common_words.txt`: Common English words in order of frequency.
/
- `data/words.txt`: Many more English words in order of frequency.

\
- `data/final_diff_words.txt`: Even more English words!

/
- `data/testcases.out`: Test cases for the optional Final Diff extension.

\
- `cats_gui.py`: A web server for the web-based graphical user interface (GUI).

/
- `gui_files`: A directory of files needed for the graphical user interface (GUI).

\
- `multiplayer`: A directory of files needed to support multiplayer mode.

/
- `favicons`: A directory of icons.

\
- `images`: A directory of images.

/
- `ok, cats.ok, tests`: Testing files.

\
- `score.py`: Part of the optional Final Diff extension.

## Multiplayer原理(来自ai)
执行`python cats_gui.py`，python启动一个服务器，向操作系统申请占用31415号端口，并自动调用浏览器打开网页

你的浏览器GUI就是**客户端(Client)**，负责显示打字进度，把敲的字发给**本地服务器(Local Server)**，比如你敲了个'cats'，GUI就发送请求给本地服务器算进度

你的`cats_gui.py`就充当着**本地服务器**，使用`cats.py`里的代码算进度，算完返回响应给你的GUI；同时，它也是“客户端”，发送请求给CS 61A**中央服务器(Central Server)**:“我是玩家(id)，现在进度xxx，告诉我的对手”(形象这块hhh)

CS 61A中央服务器记下进度，等对手的GUI来问时，返回响应给对手的本地服务器，再到对手的GUI
在浏览器上关掉网页后，`ctrl + C`来退出GUI

## 感想
第一次写的这么认真，因为自己在做EC的过程中确实遇到了些困难，问ai吧也没用，最后Gemini告诉我了答案，不过这个……好像也不难想……吗？反正当时自己是没想到……然后放弃了:(

记得做这个项目前看的一个节目，里面有个打字速度的游戏，刚好cats也是这种打字游戏！

希望能对在做cats的朋友们有所帮助
