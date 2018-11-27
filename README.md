# tello-python
官方python接口的改进，官方接口存在一些问题，例如使用多线程的方式接收tello的响应消息，而主线程和子线程之间并没有同步机制，导致接收到的相应信息不一定是刚刚发送的，也有可能是之前发送的某条命令。这个问题也导致执行命令文件时需要手动增加延时，以保证上一条代码执行完毕之后再执行下一条。tello在上条命令没有执行完毕的时候发送下一条命令会返回error，也就是如果延时设置不当tello就返回error。

使用python 3.6

我这里摒弃了多线程的方式接收响应消息，每个tello实例都是阻塞的方式执行命令，发送命令之后必须等到该条命令的响应才会发送下一条命令，保证命令的线性执行，也不需要设置延时。这里我没有设置tello无响应的超时处理，有需要的可以自行实现。如果需要实现编队飞行，就实例化多个tello对象，并且每个tello对象放在一个线程中。
官方文档中的日志功能也删掉了，有需要的自行实现。
