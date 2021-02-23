# Thinking in MakeCode
## 1. 从non-blocking思维开始
### 1.1 用micro:bit实现一个简单的需求
最开始，先提出一段原始的需求，micro:bit上有5*5的LED矩阵，我们可以单独点亮其中某个或某几个LED，那么如何设计一个程序，使一个LED间隔1秒闪烁，同时使另一个LED间隔2秒闪烁呢？  
这看起来不难，我们可能会习惯于这样理解这个需求，延时一秒，点亮第一个LED，延时一秒，熄灭第一个LED，同时点亮第二个LED，延时一秒，点亮第一个LED，延时一秒，熄灭第一个LED和第二个LED，然后循环上述流程，我们可以在MakeCode里设计类似的程序出来。“Plot”积木可以指定点亮LED矩阵中的一个LED，“Unplot”积木则是指定熄灭一个LED。  
下载例程文件<kbd>[microbit-blocking_test.hex](https://github.com/Wind-stormger/Makecode/blob/master/Thinking%20in%20MakeCode/Routine%20folder/microbit-blocking_test.hex)</kbd>到本地，然后导入到MakeCode中打开，也可参照下列截图在MakeCode中编程。
<div align=center><img src="https://raw.githubusercontent.com/Wind-stormger/Makecode/master/Thinking%20in%20MakeCode/Routine%20screenshot%20folder/1.1blocking_test.png" width="25%"></div>

### 1.2 惯性思维的困境
现在我们在前一小节的基础上稍稍改变一下需求，使一个LED间隔1.5秒闪烁，同时使另一个LED间隔2.5秒闪烁。  
按照前一小节的方法，我们会这样设计程序：延时1.5秒，点亮第一个LED，延时1秒，点亮第二个LED，延时0.5秒，熄灭第一个LED，延时1.5秒，点亮第一个LED，延时1秒，熄灭第二个LED，······  
这里给出例程文件<kbd>[microbit-blocking_test.hex](https://github.com/Wind-stormger/Makecode/blob/master/Thinking%20in%20MakeCode/Routine%20folder/microbit-blocking_test_2.hex)</kbd>以及截图  
<div align=center><img src="https://raw.githubusercontent.com/Wind-stormger/Makecode/master/Thinking%20in%20MakeCode/Routine%20screenshot%20folder/1.2blocking_test_2.png" width="25%"></div>  

我们可以直观的感受到，仅仅是修改了闪烁时间，用延时的方法来设计一段循环运行的程序就变得冗长而难以读懂，且因为要不断的计算两LED亮灭之间的时间间隔而容易出错。  
如果我们此时在需求上再增加更多要以不同频率闪烁的LED呢？  
至此，我们似乎陷入了一种思维困境，再继续使用延时的方法，如此往复，我们的代码将陷入更加复杂而容易出错的困境中，每一行就像是互相之间锁死在一起，我们可以称其为“blocking code”阻塞代码，而这样的编程思维在程序的复杂性不断增加的过程中造成的灾难性后果将会变得愈发严重而难以挽救。  
### 1.3 清晰的non-blocking思维
我们回到最开始，重新审视我们的需求，在1.1小节中，我们提出了使一个LED间隔1秒闪烁，同时使另一个LED间隔2秒闪烁的需求。现在跳脱出使用延时来逐一设置LED亮灭时间的思维，开始尝试一种新的思维，设计一个可以在While循环中用if判断当前时间是否满足条件的程序。  
在MakeCode中有一个“Running Time(ms)”积木,它可以获得程序自开始运行以来经过的时间，单位为毫秒(ms)，在“Variables”中自定义一个变量并用于存储我们从“Running Time(ms)”中读取到的时间，再设计一个if判断，当“Running Time(ms)”减去这个存储了上次读取到的运行时间的变量后，若其结果大于等于我们设计的LED闪烁间隔时长，就改变指定的LED的亮灭状态，执行完这一步后立刻将此次“Running Time(ms)”读取到的时间赋值到这个变量中用于在while循环中的下次有关于这个变量的if判断。  
关于前文中“改变指定的LED的亮灭状态”，其意思就是当LED亮时就灭掉，当LED灭时就点亮，可以用在if判断中读取指定的LED的状态是否被点亮，是则灭掉LED，否则点亮LED。另外我们可以把这段“改变指定的LED的亮灭状态”的程序单独列入一个自定义的“function”函数中，虽然并不会对整体程序有什么影响，但这样的编程习惯有利于在主程序中需要重复使用这段函数的情况下精简程序长度，方便我们多次调用它，而且有利于调试查错并可以单独修改。  
这里给出例程文件<kbd>[microbit-non-blocking_test.hex](https://github.com/Wind-stormger/Makecode/blob/master/Thinking%20in%20MakeCode/Routine%20folder/microbit-non-blocking_test.hex)</kbd>以及该例程的截图  
<div align=center><img src="https://raw.githubusercontent.com/Wind-stormger/Makecode/master/Thinking%20in%20MakeCode/Routine%20screenshot%20folder/1.3non-blocking_test.png" width="100%"></div>  
可以下载例程文件到本地，然后导入到MakeCode中打开，也可参照截图在MakeCode中编程。