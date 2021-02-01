# Thinking in MakeCode
## 1. 从non-blocking思维开始
### 1.1 惯性的blocking思维
最开始，先提出一段原始的需求，我们需要连续的完成一些事情，每间隔2s，要做事项A，每间隔4s，要做事项B，每间隔8s，要做事项C。  
这看起来不难，我们习惯于这样理解这个需求，在8s之中，在第2s时执行事项A,2s后的第4s时执行事项AB,2s后的第6s时执行事项A,2s后的第8s时执行事项ABC，如此往复，在往后复制这样的这样的作法就能完成这样的连续的需求了,我们可以在MakeCode里设计类似的程序出来。  
下载例程文件<kbd>[microbit-blocking_test.hex](https://github.com/Wind-stormger/Makecode/blob/master/Thinking%20in%20MakeCode/Routine%20folder/microbit-blocking_test.hex)</kbd>到本地，然后导入到MakeCode中打开，也可参照下列截图在MakeCode中编程。
<div style="align: center">
<img src="https://github.com/Wind-stormger/Makecode/blob/master/Thinking%20in%20MakeCode/Routine%20screenshot%20folder/1.1blocking_test.png" width="25%"> 
</div>