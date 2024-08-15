---
title: W3C_learning
date: 2024-08-14 10:59:31
tags: 学习笔记
---
# HTML

## HTML 简介

### 实例

```html
<html>
    <body>
        <h1>
            我的第一个标题
        </h1>
        <p>
            我的第一个段落
        </p>
    </body>
</html>
```

---

### 什么是HTML

HTML是用来描述网页的一种语言。

- HTML指的是超文本标记语言(**H**yper **T**ext **M**arkup **L**anguage)
- HTML不是一种编程语言，而是一种**标记语言**(markup language)
- 标记语言是一套**标记标签**(markup tag)
- HTML使用**标记标签**来描述网页

---

### HTML标签

HTML标记标签通常被称为HTML标签(HTML tag)

- HTML标签是由**尖括号**包围的关键词,比如`<html>`
- HTML标签通常是成对出现的,比如`<b>`和`</b>`
- 标签对中第一个标签是**开始标签(开放标签)**,第二个是**结束标签(闭合标签)**

---

### HTML文档 = 网页

- HTML文档**描述网页**
- HTML文档**包含HTML标签**和纯文本
- HTML文档也被称为**网页**

Web 浏览器的作用是读取 HTML 文档，并以网页的形式显示出它们。浏览器不会显示 HTML 标签，而是使用标签来解释页面的内容：

```html
<html>
    <body>
        <h1>
            我的第一个标题
        </h1>
        <p>
            我的第一个段落
        </p>
    </body>
</html>
```

**例子解释**

- `<html>`与` </html>` 之间的文本描述网页
- `<body> `与` </body>` 之间的文本是可见的页面内容
- `<h1>` 与 `</h1>` 之间的文本被显示为标题
- `<p>` 与 `</p> `之间的文本被显示为段落

---

## HTML编辑器

VScode

---

## HTML基础

### HTML标题

HTML标题(Heading)是通过`<h1>-<h6>`等标签进行定义的.

**实例**

```html
<h1>This is a heading</h1>
<h2>This is a heading</h2>
<h3>This is a heading</h3>
```

---

### HTML段落

HTML 段落是通过` <p>` 标签进行定义的。

**实例**

```html
<p>This is a paragraph.</p>
<p>This is another paragraph.</p>
```

---

### HTML链接

HTML 链接是通过` <a>` 标签进行定义的。

**实例**

```html
<a href="http://www.w3school.com.cn">This is a link</a>
```

**注释:**在href属性中指定链接的地址.

---

### HTML图像

HTML 图像是通过` <img>` 标签进行定义的。

**实例**

```html
<img src="w3school.jpg" width="104" height="142"/>
```

**注释:**图像的名称和尺寸是以属性的形式提供的.

## HTML 元素

**HTML文档是由HTML元素定义的**

---

### HTML元素

HTML 元素指的是从开始标签（start tag）到结束标签（end tag）的所有代码。

| 开始标签                  | 元素内容            | 结束标签 |
| :------------------------ | :------------------ | :------- |
| `<p>`                     | This is a paragraph | `</p>`   |
| `<a href="default.htm" >` | This is a link      | `</a>`   |
| `<br />`                  |                     |          |

---

### HTML元素语法

- HTML 元素以**开始标签**起始
- HTML 元素以**结束标签**终止
- **元素的内容**是开始标签与结束标签之间的内容
- 某些 HTML 元素具有**空内容（empty content）**
- 空元素**在开始标签中进行关闭**（以开始标签的结束而结束）
- 大多数 HTML 元素可拥有**属性**

---

### 嵌套的HTML元素

大多数 HTML 元素可以嵌套（可以包含其他 HTML 元素）。

HTML 文档由嵌套的 HTML 元素构成。

**HTML文档实例**

```html
<html>

<body>
<p>This is my first paragraph.</p>
</body>

</html>
```

上面的例子包含三个 HTML 元素。

---

### 不要忘记结束标签

即使您忘记了使用结束标签，大多数浏览器也会正确地显示 HTML：

```html
<p>This is a paragraph
<p>This is a paragraph
```

上面的例子在大多数浏览器中都没问题，但不要依赖这种做法。忘记使用结束标签会产生不可预料的结果或错误。

**注释：**未来的 HTML 版本不允许省略结束标签。

---

### 空的HTML元素

没有内容的 HTML 元素被称为空元素。空元素是在开始标签中关闭的。

`<br>` 就是没有关闭标签的空元素（`<br>` 标签定义换行）。

在 XHTML、XML 以及未来版本的 HTML 中，所有元素都必须被关闭。

在开始标签中添加斜杠，比如` <br />`，是关闭空元素的正确方法，HTML、XHTML 和 XML 都接受这种方式。

即使 `<br>` 在所有浏览器中都是有效的，但使用 `<br />` 其实是更长远的保障。

---

### HTML提示:使用小写标签

HTML 标签对大小写不敏感：`<P>` 等同于 `<p>`。许多网站都使用大写的 HTML 标签。

W3School 使用的是小写标签，因为万维网联盟（W3C）在 HTML 4 中*推荐*使用小写，而在未来 (X)HTML 版本中*强制*使用小写。

---

## HTML属性

**属性为HTML元素提供附加信息**

---

### HTML 属性

HTML 标签可以拥有*属性*。属性提供了有关 HTML 元素的**更多的信息**。

属性总是以名称/值对的形式出现，比如：**name="value"**。

属性总是在 HTML 元素的**开始标签**中规定。

---

### 属性实例

HTML 链接由 `<a>` 标签定义。链接的地址在 href 属性中指定：

```html
<a href="http://www.w3school.com.cn">This is a link</a>
```

---

### 更多HTML属性实例

**属性例子 1:**

`<h1>` 定义标题的开始。

`<h1 align="center">` 拥有关于对齐方式的附加信息。


**属性例子 2:**

`<body> `定义 HTML 文档的主体。

`<body bgcolor="yellow">` 拥有关于背景颜色的附加信息。

**属性例子 3:**

`<table>` 定义 HTML 表格。（您将在稍后的章节学习到更多有关 HTML 表格的内容）

`<table border="1">` 拥有关于表格边框的附加信息。

---

### HTML 提示：使用小写属性

属性和属性值对大小写**不敏感**。

不过，万维网联盟在其 HTML 4 推荐标准中推荐小写的属性/属性值。

而新版本的 (X)HTML 要求使用小写属性。

---

### 始终为属性值加引号

属性值应该始终被包括在引号内。双引号是最常用的，不过使用单引号也没有问题。

在某些个别的情况下，比如属性值本身就含有双引号，那么您必须使用单引号，例如：

```html
name='Bill "HelloWorld" Gates'
```

---

### HTML参考手册

([HTML 标签参考手册 (w3school.com.cn)](https://www.w3school.com.cn/tags/index.asp))

[HTML 标准属性参考手册](https://www.w3school.com.cn/tags/html_ref_standardattributes.asp)

---

