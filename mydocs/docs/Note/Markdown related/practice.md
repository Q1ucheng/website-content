# Markdown Learning </h1>

>**Markdown** 的本质是让我们回归到**内容本身**，注重文章本身的**结构**，而不是样式。

**Markdown** 是一种轻量级标记语言，创始人为 ***John Gruber***。它允许人们使用易读易写的纯文本格式编写文档，然后转换成有效的 XHTML（或者 HTML）文档。

下面是我在**markdown**学习中所做的练习，以简明教程的形式呈现出来，文章多有疏漏，还需时间打磨。

>Practice makes perfect.

[Access to official documentation](https://markdown.com.cn/basic-syntax/){ .md-button .md-button--primary }

## 前期准备
### 1. 安装编译软件
### install vscode

1.在官网下载最新版本

[vscode下载](https://code.visualstudio.com/ "vscode")

2.直接运行**code.exe**

**将这两个选项勾上**，它们可以帮助你利用windows的资源管理器来管理你的Markdown文稿

![设置](https://pic4.zhimg.com/80/v2-5a8a9f0a9c41690ba97e40256456cb47_1440w.webp "title")

3.安装markdown插件

在vscode插件市场中查找以下两个插件并安装

**markdown-all-in-one**

**markdown-preview-github-styles**

4.创建文档

先专门建立一个新的文件夹，方便你管理所写的markdown文档。用vscode打开这个文件夹，接着在此文件夹中新建一个后缀名为`.md`的文档。当你输入`.md`的后缀后，你会看到文档前出现了一个向下的箭头标识，这表明它已经被vscode识别为markdown文件了。

5.开始你的创作！

***

## markdown 语法学习

## 标题语法
要创建标题，需要在单词或短语前添加 `#` 号（**#号后要添加空格，否则无法识别！**）。`#` 号的数量代表标题的级别。
## 段落语法
要创建段落，请使用空白行将一行或多行文本进行分隔
## 换行语法
在一行的末尾添加两个或多个空格再回车即可创建一个换行。
## 强调语法
### 粗体
**在单词或短语的前后添加两个星号即可加粗文本**

    **文本**

### 斜体
*在单词或短语的前后添加一个星号即可将文本转化为斜体*

    *文本*
### 粗体和斜体
***在单词或短语的前后添加三个星号即将文本转化为加粗斜体***

    ***文本***
## 引用语法
在段落前添加一个 `>` 即可实现引用。

渲染效果如下：

>Markdown 是一种轻量级的标记语言，可用于在纯文本文档中添加格式化元素。Markdown 由 John Gruber 于 2004 年创建，如今已成为世界上最受欢迎的标记语言之一。
### 多个段落的块引用
在段落之间的空白行添加一个>符号即可实现。

渲染效果如下：

>Markdown 是独立于平台的。你可以在运行任何操作系统的任何设备上创建 Markdown 格式的文本。
>
>Markdown 能适应未来的变化。即使你正在使用的应用程序将来会在某个时候不能使用了，你仍然可以使用文本编辑器读取 Markdown 格式的文本。当涉及需要无限期保存的书籍、大学论文和其他里程碑式的文件时，这是一个重要的考虑因素。
### 嵌套块引用
在要嵌套的段落前添加一个 `>>` 号即可

渲染效果如下：(此处包含有**无序列表**的使用)

>Markdown 有哪些优点？
>>- 专注于文字内容
>>
>>- 纯文本，易读易写，可以方便地纳入版本控制
>>
>>- 语法简单，没有什么学习成本，能轻松在码字的同时做出美观大方的排版。

## 代码语法
要将单词或短语表示为代码，只需将其至于反引号中。

渲染效果如下：

`Hello World`

想引入代码块，则将代码块的每一行缩进至少四个空格。

渲染效果如下：

    Hello World
    Hello World ？
    Hello World ！

## 分隔线语法
在***单独一行***上使用三个或多个`*`号 (`***`)、破折号（`---`）、下划线（`___`）,并且不能包含其他内容。

渲染效果如下：

***

## 链接语法
链接文本放在中括号内，链接地址放在后面的括号中。代码如下：

`[链接名称](链接地址)`

例如：

    这是一个链接 [西北工业大学](https://www.nwpu.edu.cn/)。

渲染效果如下：

这是一个链接 [西北工业大学](https://www.nwpu.edu.cn/)。

这看起来有些单调，所以我们可以给链接一个title让它看起来更有趣。

    这是一个链接 [西北工业大学](https://www.nwpu.edu.cn/ "西北工业大学")。

***注意：链接地址和title之间以空格分开！***

这样当鼠标悬停在链接上时会出现title

### 网址和Email
使用尖括号即可将URL或Email变成链接。

    <https://www.nwpu.edu.cn/>
    <zhaoqiucheng21@gmail.com>

渲染效果如下：

<https://www.nwpu.edu.cn/>

<zhaoqiucheng21@gmail.com>

## 引用类型链接

    [显示为链接的文本][1]
    
    [1]: <https://www.nwpu.edu.cn/>"西北工业大学"

渲染效果如下：

[显示为链接的文本][1]

[1]: <https://www.nwpu.edu.cn/> "西北工业大学"

***注意：这里的 \[1\]: 可以放在文件中的任何位置*** 

## 图片语法
代码如下：

    ![图片的描述](图片链接 "title")

渲染效果如下：

 ![图片的描述](https://tse1-mm.cn.bing.net/th/id/OIP-C.Xn_epajhSFoDxT6V3W0r9gHaEK?pid=ImgDet&rs=1 "doge")

 ## 转义字符语法
感觉没什么好说的，用反斜杠就可以完成。

需要细说的是**特殊字符的自动转义**，后面会再讲到。
## 内嵌 HTML 标签
>对于 Markdown 涵盖范围之外的标签，都可以直接在文件里面用 HTML 本身。如需使用 HTML，不需要额外标注这是 HTML 或是 Markdown，只需 HTML 标签添加到 Markdown 文本中即可。

简而言之，HTML可以直接写到Markdown里？（待后续实践补充）

***
# markdown扩展语法

>John Gruber的原始设计文档中概述的基本语法主要是为了应付大多数情况下的日常所需元素，但对于某些人来说还不够，这就是扩展语法的用武之地。
>
>一些个人和组织开始通过添加其他元素（例如表，代码块，语法突出显示，URL自动链接和脚注）来扩展基本语法。可以通过使用基于基本Markdown语法的轻量级标记语言，或通过向兼容的Markdown处理器添加扩展来启用这些元素。
## markdown表格
代码如下：

    | markdown   | latex |
    | ---------- | ----- |
    | best       | good  |
    | md         | pdf   |

渲染效果如下：

| markdown   | latex |
| ---------- | ----- |
| best       | good  |
| md         | pdf   |

### 如何实现对齐？
添加 `:` 即可，代码如下：

    | Syntax      | Description | Test Text     |
    | :---        |    :----:   |          ---: |
    | Header      | Title       | Here's this   |
    | Paragraph   | Text        | And more      |

渲染效果如下：

| Syntax      | Description | Test Text     |
| :---        |    :----:   |          ---: |
| Header      | Title       | Here's this   |
| Paragraph   | Text        | And more      |

## 围栏代码块
在代码块之前和之后使用三个反引号或三个波浪号即可。

like this:

    ```c
    #include <stdio.h>
    int main(void)
    {
        printf("Hello, World!");
        return 0;
    }
    ```

渲染效果如下：

```c
#include <stdio.h>
int main(void)
{
    printf("Hello, World!");
    return 0;
}
```
**添加编程语言类型即可实现语法高亮**

## markdown 删除线
直接上代码：

    ~~文本~~文本

输出如下：

 ~~latex是极好的~~ markdown是极好的
 ## Emoji 表情的使用
 可以通过键入表情符号短代码来插入表情符号，以冒号开头和收尾。

 代码如下：

     :laughing::point_right:
     :rage:

渲染效果如下：

***(正在改进中...)***

表情短代码在[此处](https://gist.github.com/rxaviers/7360908 "github")可以查询。

***

## 如何将写好的md文档导出为HTML文件 ？

### 方法一：利用csdn写作板块导出

1.访问[csdn](https://www.csdn.net/ "csdn").

2.进入个人空间发布文章。

3.使用csdn自带的MD编辑器，导入`.md`文档，导出为HTML文件。

### 方法二：Python实现

***（不断学习中...）***

