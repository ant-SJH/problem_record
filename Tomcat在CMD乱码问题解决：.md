### Tomcat在CMD乱码问题解决：

**问题分析:**

Tomcat的输出编码为UTF-8，CMD的编码为GBK，两者不一致

**解决方法：**

一.修改CMD的编码为UTF-8（推荐）

1. 打开注册表（win+r 输入regedit）

2. 找到HKEY_CURRENT_USER→Console→Tomcat（如果你改了tomcat的标题栏，这里就是你打开的命令窗口的名字），找到CodePage项，没有则创建（注意创建的时候要DWORD32位），设置值为十进制的65001，点击确定。

3. 如果是解压版的Tomcat一般不会有Tomcat这一项，则复制下面的代码命名为xx.bat，最后改一下10进制的65001

   ```
   set rr="HKCU\Console\Tomcat"
   reg add %rr% /v "CodePage" /t REG_DWORD /d 0x0000fde9 /f>nul
   ```



二.修改tomcat的编码为GBK

1. 修改tomcat根目录下conf/logging.properties文件
2. 将其中的ConsoleHandler.encoding=utf-8 改为 GBK



**参考链接**

[解决各种tomcat中文乱码问题]: https://www.jianshu.com/p/7236d45cd1eb
[Tomcat乱码问题 catalina.bat设置为UTF-8 控制台出现乱码]: http://www.zhishilin.com/show/201812/vjfcxuym.shtml



