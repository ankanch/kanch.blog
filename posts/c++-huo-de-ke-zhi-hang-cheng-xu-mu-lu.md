---
title: C++获得可执行程序目录
tags:
  - C++
  - C++获得exe路径
  - 获得路径
id: 79
categories:
  - C++ / Visual C++
date: '2015-06-22T16:30:22.000Z'
---

# C++获得可执行程序目录

### 本文介绍了在纯C++与VC下的获得当前可执行文件的路径方法。

### **首先，纯C++方式：**&lt;/span&gt;

函数原型: **char** _**getcwd\(char**_ **dir,int len\)** 函数功能: 得到当前路径名称 函数返回: 指向dir的指针 参数说明: **len**是路径最大长度.**dir**是路径字符串. 所属文件: dir.h \(_这个头文件可能被命名为 direct.h 或者其他_\) 示例代码：&lt;/span&gt;

```text
#include 
#include 
int main()
{
char buffer[MAXPATH];
getcwd(buffer, MAXPATH);
printf("The current directory is: %s", buffer);
return 0;
}
```

### **Visual C++方式：**&lt;/span&gt;

* **函数：**

  DWORD WINAPI GetModuleFileName\(_In\_opt_ HMODULE hModule,_Out_ LPTSTR lpFilename,_In_ DWORD nSize\);

* **功能：** 获取当前进程已加载模块的文件的完整路径，该模块必须由当前进程加载。

   如果想要获取另一个已加载模块的文件路径，可以使用GetModuleFileNameEx函数。

* **参数说明** **hModule Long** 一个模块的句柄。可以是一个DLL模块，或者是一个应用程序的实例句柄。如果该参数为NULL，该函数返回该应用程序全路径。 **lpFileName String** 指定一个字串缓冲区，要在其中容纳文件的用NULL字符中止的路径名，hModule模块就是从这个文件装载进来的 **nSize Long** 装载到缓冲区lpFileName的最大字符数量 示例代码：

  \#include

  **include**

  BOOL CreateSampleService\(\) { TCHAR szPath\[MAX\_PATH\]; if\( !GetModuleFileName\( NULL, szPath, MAX\_PATH \) \) { printf\("GetModuleFileName failed \(%d\)n", GetLastError\(\)\); return FALSE; } return TRUE; } / _如果想获得某个正在运行的EXE或者DLL的全路径可以这样写代码 GetModuleFileNameEx\(hProcess,hInst,lpFile,MAX\_PATH\);//注意下缓冲区就行了。_ / &lt;/pre&gt;  

详情查阅MSDN \[[https://msdn.microsoft.com/zh-tw/office/ms683197\(v=vs.100\)\]\(https://msdn.microsoft.com/zh-tw/office/ms683197\(v=vs.100](https://msdn.microsoft.com/zh-tw/office/ms683197%28v=vs.100%29]%28https://msdn.microsoft.com/zh-tw/office/ms683197%28v=vs.100)\)\)
