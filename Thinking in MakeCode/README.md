# Thinking in MakeCode
## 1. 从non-blocking思维开始
### 1.1 用micro:bit实现一个简单的需求
最开始，先提出一段原始的需求，micro:bit上有5*5的LED矩阵，我们可以单独点亮其中某个或某几个LED，那么如何设计一个程序，使一个LED间隔1秒闪烁，同时使另一个LED间隔2秒闪烁呢？  
这看起来不难，我们可能会习惯于这样理解这个需求，延时一秒，点亮第一个LED，延时一秒，熄灭第一个LED，同时点亮第二个LED，延时一秒，点亮第一个LED，延时一秒，熄灭第一个LED和第二个LED，然后循环上述流程，我们可以在MakeCode里设计类似的程序出来。“Plot”方块可以指定点亮LED矩阵中的一个LED，“Unplot”方块则是指定熄灭一个LED。  
下载例程文件<kbd>[microbit-blocking_test.hex](https://github.com/Wind-stormger/Makecode/blob/master/Thinking%20in%20MakeCode/Routine%20folder/microbit-blocking_test.hex)</kbd>到本地，然后导入到MakeCode中打开，也可参照下列截图在MakeCode中编程。
<div align=center><img src="https://github.com/Wind-stormger/Makecode/blob/master/Thinking%20in%20MakeCode/Routine%20screenshot%20folder/1.1blocking_test.png" width="25%"></div>

### 1.2 惯性思维的困境
现在我们在前一小节的基础上稍稍改变一下需求，使一个LED间隔1.5秒闪烁，同时使另一个LED间隔2.5秒闪烁。  
按照前一小节的方法，我们会这样设计程序：延时1.5秒，点亮第一个LED，延时1秒，点亮第二个LED，延时0.5秒，熄灭第一个LED，延时1.5秒，点亮第一个LED，延时1秒，熄灭第二个LED，······  
这里给出例程文件<kbd>[microbit-blocking_test.hex](https://github.com/Wind-stormger/Makecode/blob/master/Thinking%20in%20MakeCode/Routine%20folder/microbit-blocking_test_2.hex)</kbd>以及截图  
<div align=center><img src="https://github.com/Wind-stormger/Makecode/blob/master/Thinking%20in%20MakeCode/Routine%20screenshot%20folder/1.2blocking_test_2.png" width="25%"></div>
至此，我们陷入了思维困境，如此往复，不断陷入更加复杂而容易出错的困境中，像是互相之间锁死在一起，我们可以称其为“blocking code”阻塞代码，而这样的编程思维的灾难在程序的复杂性不断增加的过程中会变得愈发严重而难以挽救。  
### 1.3 清晰的non-blocking思维
我们回到最开始，重新审视我们的需求： 
