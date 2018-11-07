---
title: 0019_第一个Java程序
date: 2018-11-07 21:52:04
tags: Java
categories: Java
---

### 第一个Java程序

打开Eclipse，依次点击"File"->"New"->"Java Project"，输入Project Name，点击完成

{% asset_img CreateNewJavaProject.png pic:创建一个Java工程 %}

右击工程名，选择"New"->"Class"，输入类名："HelloWorld"，点击完成，并输入以下代码：

```java
public class HelloWorld {
    public static void main(String []args) {
        System.out.println("Hello World");
    }
}
```

点击 Run，运行程序，输出如下：

{% asset_img ExecuteResult.png pic:执行结果 %}