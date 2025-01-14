![ymodem-logo](https://raw.githubusercontent.com/alexwoo1900/ymodem/master/docs/assets/ymodem-logo.png)

本项目是基于tehmaze的XMODEM项目的YMODEM版本，它同样兼容XMODEM模式。

[![Build Status](https://www.travis-ci.org/alexwoo1900/ymodem.svg?branch=master)](https://www.travis-ci.org/alexwoo1900/ymodem)
[![license](https://img.shields.io/github/license/mashape/apistatus.svg)](https://opensource.org/licenses/MIT)

README: [ENGLIST](https://github.com/alexwoo1900/ymodem/blob/master/README.md) | [简体中文](https://github.com/alexwoo1900/ymodem/blob/master/README_CN.md)


## 功能演示

### 单独测试发送与接收功能 

如果想运行测试例子，请执行以下操作：
1. 利用串口虚拟工具在本地生成可相互通信的COM1与COM2
2. 在命令行中分别运行FileReceiver.py与FileSender.py文件

具体的传输过程如下图所示：
![SenderAndReceiver](https://raw.githubusercontent.com/alexwoo1900/ymodem/master/docs/assets/console_test.gif)

### 与SecureCRT交互

作为发送者与SecureCRT交互
![SecureCRT1](https://raw.githubusercontent.com/alexwoo1900/ymodem/master/docs/assets/sender.gif)

作为接收者与SecureCRT交互
![SecureCRT2](https://raw.githubusercontent.com/alexwoo1900/ymodem/master/docs/assets/receiver.gif)

## 快速上手

```python
from Modem import Modem

'''
Sender
'''
# define read function for sender
def sender_read(size, timeout=3):
    pass

# define write function for sender
def sender_write(data, timeout=3):
    pass

# create sender
sender = Modem(sender_read, sender_write)

# send multi files
sender.send([file_path1, file_path2, file_path3 ...])

'''
Receiver
'''

# define read function for receiver
def receiver_read(size, timeout=3):
    pass

# define write function for receiver
def receiver_write(data, timeout=3):
    pass

# create receiver
receiver = Modem(receiver_read, receiver_write)

# receive multi files
receiver.recv(folder_path)
```

## API

### 创建MODEM对象

```python
def __init__(self, reader, writer, mode='ymodem1k', program="rzsz")
```
- reader： 读对象或者读函数。
- writer： 写对象或者写函数。
- mode： 默认使用数据长度为1k字节的YMODEM模式。
- program： YMODEM的标准（不同标准有不同特性）。

### 发送数据

```python
def send(self, file_paths, retry=10, timeout=10, callback=None):
```
- file_paths： 文件路径列表。
- retry： 最大重传次数。
- timeout： reader和writer的超时时间。
- callback： 回调函数，见下表。

    参数（按顺序） | 描述
    -|-
    task index | 任务索引
    task (file) name | 任务（文件）名称
    total packets | 总包数
    success packets | 成功包数
    failed packets | 失败包数


### 接收数据

```python
def recv(self, folder_path, crc_mode=1, retry=10, timeout=10, delay=1, callback=None)
```
- folder_path： 保存文件夹路径。
- crc_mode： 由接收者指定的校验模式。
- retry： 最大重传次数。
- timeout： reader和writer的超时时间。
- delay： 延迟时间。
- callback： 回调函数，见下表。

    参数（按顺序） | 描述
    -|-
    task index | 任务索引
    task (file) name | 任务（文件）名称
    total packets | 总包数
    success packets | 成功包数
    failed packets | 失败包数

## 调试

如果想要输出调试信息，请把日志等级设成DEBUG。

```python
logging.basicConfig(level=logging.DEBUG, format='%(message)s')
```

## 更新日志
### v1.3 (2022/11/21 14:00 +00:00)

- 支持多文件传输
- 简化函数接口

## 许可证
[MIT许可证](https://opensource.org/licenses/MIT)