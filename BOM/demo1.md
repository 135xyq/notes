# BOM
----------

BOM是browser object model的缩写，简称浏览器对象模型

主要处理浏览器窗口（window）和框架（iframe），
描述了与浏览器进行交互的方法和接口，可以对浏览器窗口进行访问和操作，不过通常浏览器特定的 JavaScript 扩展都被看做 BOM 的一部分。扩展如下：


1. 弹出新的浏览器窗口


2. 移动、关闭浏览器窗口以及调整窗口大小

3. 提供 Web 浏览器详细信息的定位对象

4. 提供用户屏幕分辨率详细信息的屏幕对象


5. 对 cookie 的支持


6. IE 扩展了BOM，加入了ActiveXObject 类，可以通过 JavaScript 实例化 ActiveX 对象

### 归纳：


Window JavaScript 层级中的顶层对象表示浏览器窗口

包含客户端浏览器的信息

History 包含了浏览器窗口访问过的 URL

Location 包含了当前 URL 的信息

Screen 包含客户端显示屏的信息

[BOM.pdf](https://duyiedu.yuque.com/docs/share/17c3a868-d15a-448f-ad3c-93a7cb554f4f?#qvTfj)







