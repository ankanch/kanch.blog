---
title: MFC实现对话框上的简单绘图（曲线的绘制）
tags:
  - C++
  - MFC
  - MFC绘图
  - Visual C++
  - 对话框
  - 对话框画图
  - 绘图
id: 411
categories:
  - C++ / Visual C++
date: '2016-04-30T09:23:41.000Z'
---

# MFC实现对话框上的简单绘图（曲线的绘制）

这里我们介绍在MFC对话框上实现的简单绘图如下图所示：

（GIF不动戳大:\)）

[![ezgif-1760387173](https://raw.githubusercontent.com/ankanch/blog/master/images/wp-content/uploads/2016/04/ezgif-1760387173-300x239.gif)](https://raw.githubusercontent.com/ankanch/blog/master/images/wp-content/uploads/2016/04/ezgif-1760387173.gif)

我们主要响应MFC对话框的以下3个消息：

WM\_LBUTTONDOWN

WM\_LBUTTONUP

WM\_MOUSEMOVE

## 先说说基本思路：

当鼠标左键按下的时候，就在WM\_MOUSEMOVE消息函数中处理绘图，在鼠标左键抬起后，就停止绘图。所以我们需要一个全局变量来标记当前鼠标的状态，以便在WM\_MOUSEMOVE函数中进行是否绘图的判断。

下面看看WM\_LBUTTONDOWN的消息处理函数内容：

void CMDDlg::OnLButtonDown\(UINT nFlags, CPoint point\) { // TODO: 在此添加消息处理程序代码和/或调用默认值 draw = true; lbeg = point;

```text
CDialogEx::OnLButtonDown(nFlags, point);
```

}&lt;/pre&gt; 在上面的函数中，我们用draw来标记当前的绘图状态。

lbeg用来标记第一个点的位置（即鼠标按下的点）

接下来处理WM\_LBUTTONUP消息：

void CMDDlg::OnLButtonUp\(UINT nFlags, CPoint point\) { // TODO: 在此添加消息处理程序代码和/或调用默认值 draw = false; lend = point;

```text
CDialogEx::OnLButtonUp(nFlags, point);
```

}&lt;/pre&gt; 当鼠标左键抬起的我们就把当前绘图状态，即draw的值设置为false

然后是最重要的，WM\_MOUSEMOVE：

```
void CI::OnMouseMove(UINT nFlags, CPoint point) { // TODO: 在此添加消息处理程序代码和/或调用默认值 CClientDC dc(this); CPen pen(PS_SOLID, HEAD.bound, RGB(HEAD.RGB[0], HEAD.RGB[1], HEAD.RGB[2])); dc.SelectObject(&pen); if (draw == true) { dc.MoveTo(lbeg); dc.LineTo(point); lbeg = point; } CDialogEx::OnMouseMove(nFlags, point); }
```

当我们判断到绘制状态为true的时候，我们就不断的用[MoveTo](https://msdn.microsoft.com/en-us/library/kchtckce.aspx)来将画笔移动到起始点（为了绘制连续的曲线，第一次起始点应该为鼠标左键单击的地方，后面的起始点都为上一次的point值）然后用[LineTo](https://msdn.microsoft.com/en-us/library/wzc1344s.aspx)函数绘制从起点到终点的直线。

**\***重要说明\*\*：WM\_MOUSEMOVE这个消息不是鼠标一移动就会响应的，它的响应是离散而非连续的。
