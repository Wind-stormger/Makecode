# Thinking in MakeCode
## 1. 从non-blocking思维开始
### 1.1 惯性思维
最开始，先提出一段原始的需求，我们需要连续的完成一些事情，每间隔2s，要做事项A，每间隔4s，要做事项B，每间隔8s，要做事项C。  
这看起来不难，我们习惯于这样理解这个需求，在8s之中，在第2s时执行事项A,2s后的第4s时执行事项AB,2s后的第6s时执行事项A,2s后的第8s时执行事项ABC，如此往复，在往后复制这样的这样的作法就能完成这样的连续的需求了,我们可以在MakeCode里设计类似的程序出来。  
下载例程文件<kbd>[microbit-blocking_test.hex](https://github.com/Wind-stormger/Makecode/blob/master/Thinking%20in%20MakeCode/Routine%20folder/microbit-blocking_test.hex)</kbd>到本地，然后导入到MakeCode中打开，也可参照下列截图在MakeCode中编程。
<div align=center><img src="https://github.com/Wind-stormger/Makecode/blob/master/Thinking%20in%20MakeCode/Routine%20screenshot%20folder/1.1blocking_test.png" width="25%"></div>

### 1.2 惯性思维的困境
将程序烧录到micro:bit内或直接在仿真器内观察程序运行的结果，仅粗略的估算就能明显的发现程序中规定的动作时间和实际运行的时间差距很大，此时我们需要进一步检查程序实际执行所需时间，手动掐秒表的方式显然存在人为引入的误差，而在程序中额外插入几段用于检测程序实际执行所需时间的代码（积木）并从串口直接输出检测到的时间则相对精准很多。  
例程文件<kbd>[microbit-blocking_test_2.hex](https://github.com/Wind-stormger/Makecode/blob/master/Thinking%20in%20MakeCode/Routine%20folder/microbit-blocking_test_2.hex)</kbd>。  
将例程下载到本地导入到MakeCode中打开，可以看到在程序中加入了如下列截图所示的积木。  
<div align=center><img src="https://github.com/Wind-stormger/Makecode/blob/master/Thinking%20in%20MakeCode/Routine%20screenshot%20folder/1.2blocking_test_2.png" width="50%"></div> 

其中"running time(ms)"可以获取程序从最开始被启动一直执行到这一块的总运行时间(单位ms)，想要设计一个获取某一段程序运行所需的具体时间，则在这段程序前后各读取一次"running time(ms)"，并将后者减去前者，即可得到该段程序运行所需的具体时间。  
现在到仿真器里观察四段程序的运行时间，其结果如下:  
<div align=center>

>1:2606ms  
>2:6081ms  
>3:2607ms  
>4:12286ms  
</div>
这明显不符合我们预期设计的结果，累计共运行了23580ms，且可以算得执行第一段程序时减去延时的2000ms，还额外运行了606ms，以及后面三段都有减去延时后额外的运行时间。

至此，我们陷入了思维困境，而假若我们的思维开始钻牛角尖，想要要在这样的程序基础上实现更准确的延时，而反复计算每一段的运行时间，再从延时中扣除，如此往复，以至于直接修改了原来既定的需求，不断陷入更加复杂而容易出错的困境中，可以感受到每一段代码(积木)的执行所要消耗的运行时间都将推迟其后面的代码的运行，像是互相之间锁死在一起，我们可以称其为“blocking code”阻塞代码，而这样的编程思维的灾难在程序的复杂性不断增加的过程中会变得愈发严重而难以挽救。  
### 1.3 清晰的non-blocking思维
