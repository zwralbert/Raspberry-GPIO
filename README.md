# Raspberry-GPIO
1、导入pyserial模块

import serial



2、打开串行口

// 打开串口0， 9600，8N1，连接超时0.5秒
import serial

ser=serial.Serial("/dev/ttyUSB0",9600,timeout=0.5) #使用USB连接串行口

ser=serial.Serial("/dev/ttyAMA0",9600,timeout=0.5) #使用树莓派的GPIO口连接串行口

ser=serial.Serial(1,9600,timeout=0.5) #winsows系统使用com1口连接串行口

ser=serial.Serial("com1",9600,timeout=0.5) #winsows系统使用com1口连接串行口

ser=serial.Serial("/dev/ttyS1",9600,timeout=0.5) #Linux系统使用com1口连接串行口

print ser.name #打印设备名称

print ser.port #打印设备名

ser.open () #打开端口

s = ser.read(10) #从端口读10个字节

ser.write("hello") #向端口写数据

ser.close() #关闭端口

        data = ser.read(20) #是读20个字符

        data = ser.readline() #是读一行，以/n结束，要是没有/n就一直读，阻塞。

        data = ser.readlines()和ser.xreadlines() #都需要设置超时时间

        ser.baudrate = 9600 #设置波特率

        ser.isOpen() #看看这个串口是否已经被打开


3、获得串行口状态

串行口的属性：

name:设备名字

portstr:已废弃，用name代替

port：读或者写端口

baudrate：波特率

bytesize：字节大小

parity：校验位

stopbits：停止位

timeout：读超时设置

writeTimeout：写超时

xonxoff：软件流控

rtscts：硬件流控

dsrdtr：硬件流控

interCharTimeout:字符间隔超时

属性的使用方法：

ser=serial.Serial("/dev/ttyAMA0",9600,timeout=0.5)

ser.open()



print ser.name

print ser.port

print ser.baudrate #波特率

print ser.bytesize #字节大小

print ser.parity #校验位N－无校验，E－偶校验，O－奇校验

print ser.stopbits #停止位

print ser.timeout #读超时设置

print ser.writeTimeout #写超时

print ser.xonxoff #软件流控

print ser.rtscts #硬件流控

print ser.dsrdtr #硬件流控

print ser.interCharTimeout #字符间隔超时

ser.close()


4、设置串行口状态
需要用的常量


bytesize：FIVE BITS、SIXBITS、SEVENBITS、EIGHTBITS

parity: PARITY_NONE, PARITY_EVEN, PARITY_ODD, PARITY_MARK, PARITY_SPACE

stopbits: STOPBITS_ONE, STOPBITS_ONE_POINT_FIVE, STOPBITS_TWO
异常：
ValueError：参数错误

SerialException：找不到设备或不能配置

ser.baudrate＝9600 #设置波特率

ser.bytesize＝8 #字节大小

ser.bytesize＝serial.EiGHTBITS #8位数据位

ser.parity=serial.PARITY_EVEN #偶校验
ser.parity=serial.PARITY_NONE #无校验
ser.parity=serial.PARITY_ODD #奇校验

ser.stopbits＝1 #停止位
ser.timeout＝0.5 #读超时设置
ser.writeTimeout＝0.5 #写超时
ser.xonxoff #软件流控
ser.rtscts #硬件流控
ser.dsrdtr #硬件流控
ser.interCharTimeout #字符间隔超时
5、Readline方法的使用

        是读一行，以/n结束，要是没有/n就一直读，阻塞。


        使用readline()时应该注意：打开串口时应该指定超时，否则如果串口没有收到新行，则会一直等待。如果没有超时，readline会报异常。

6、serial.Serial类——原生端口
class serial.Serial 
{
    __init__(port=None, baudrate=9600, bytesize=EIGHTBITS,parity=PARITY_NONE, stopbits=STOPBITS_ONE, timeout=None, xonxoff=False, rtscts=False, writeTimeout=None, dsrdtr=False, interCharTimeout=None)

    #其中:
    # bytesize：FIVEBITS、SIXBITS、SEVENBITS、EIGHTBITS
    # parity: PARITY_NONE, PARITY_EVEN, PARITY_ODD, PARITY_MARK, PARITY_SPACE
    # stopbits: STOPBITS_ONE, STOPBITS_ONE_POINT_FIVE, STOPBITS_TWO
    #异常：
    #ValueError：参数错误
    #SerialException：找不到设备或不能配置

    open()：打开串口

    close()：立即关闭串口

    __del__()：析构函数

    read(size=1)：从串口读size个字节。如果指定超时，则可能在超时后返回较少的字节；如果没有指定超时，则会一直等到收完指定的字节数。

    write(data)：发送data，并返回发送字节数。如果bytes和bytearray可用（python 2.6以上），则接受其作为参数；否则接受str作为参数。
    #异常：SerialTimeoutException——配置了写超时并发生超时时发生此异常。

    inWaiting()：返回接收缓存中的字节数

    flush()：等待所有数据写出。

    flushInput()：丢弃接收缓存中的所有数据

    flushOutput()：终止当前写操作，并丢弃发送缓存中的数据。

    sendBreadk(duration=0.25)：发送BREAK条件，并于duration时间之后返回IDLE

    setBreak(level=True)：根据level设置break条件。

    setRTS(level=True)

    setDTR(level=True)

    getCTS()

    getDSR()

    getRI()

    getCD()

    #只读属性：
    name:设备名字
    portstr:已废弃，用name代替
    port：读或者写端口
    baudrate：波特率
    bytesize：字节大小
    parity：校验位
    stopbits：停止位
    timeout：读超时设置
    writeTimeout：写超时
    xonxoff：软件流控
    rtscts：硬件流控
    dsrdtr：硬件流控
    interCharTimeout:字符间隔超时

    #端口设置可以被读入字典，也可从字典加载设置：
    getSettingDict()：返回当前串口设置的字典
    applySettingDict(d):应用字典到串口设置

    #对提供io库的系统（python 2.6或以上），Serial从io.RawIOBase派生。对其它系统，从FileLike派生。

    #异常：
    exception serial.SerialException
    exception serial.SerialTimeoutException

    #常量：
    serial.VERSION：pyserial版本

    #模块函数和属性：
    serial.device(number)

    serial.serial_for_url(url, *args, **kwargs)

    serial.protocol_handler_packages()

    serial.to_bytes(sequence)：接收一个字符串或整数列表sequence，返回bytes实例
}


