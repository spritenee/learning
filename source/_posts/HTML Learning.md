---
title: HTML学习笔记
abbrlink: 34391
date: 2024-01-15 00:00:00
tags:
lang: zh-CN
cover: https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240118152543323.png
---

The HTML **element** is everything from the start tag to the end tag.

```
<h1>My First Heading</h1>
<p>My first paragraph.</p>
```

**Note:** Some HTML elements have no content (like the <br> element). These elements are called empty elements. Empty elements do not have an end tag!

## HTML Page Structure

Below is a visualization of an HTML page structure:

<img src="https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240115084731756.png" alt="image-20240115084731756" style="zoom:67%;" />

**Note:** The content inside the <body> section will be displayed in a browser. The content inside the <title> element will be shown in the browser's title bar or in the page's tab.

`.htm` 和 `.html` 都是用于标记超文本语言（Hyper Text Markup Language）的文件扩展名。在大多数情况下，二者之间没有明显的区别，它们都被 Web 浏览器用来显示网页。

这两种扩展名的存在主要是来自历史上操作系统对文件名长度的限制。在过去，像DOS这样的老版本操作系统只允许三个字符的扩展名，因此 `.htm` 这样的三个字符扩展名就被广泛使用。然而，随着操作系统如 Windows、Mac OS 和 Linux 能够支持更长的文件名， `.html` 扩展名也变得越来越常见。

简单来说，`.htm`和`.html`之间的区别主要是历史和个人偏好的问题，没有对网页显示或功能上的实际影响。网站服务器和 Web 浏览器都能同样处理 `.htm` 和 `.html` 文件。

## HTML Documents

All HTML documents must start with a document type declaration: `<!DOCTYPE html>`.

The HTML document itself begins with `<html>` and ends with `</html>`.

The visible part of the HTML document is between `<body>` and `</body>`.

### The <!DOCTYPE> Declaration

The `<!DOCTYPE>` declaration represents the document type, and helps browsers to display web pages correctly.

It must only appear once, at the top of the page (before any HTML tags).

The `<!DOCTYPE>` declaration is **not** case sensitive.

<h3>HTML Headings</h3>

HTML headings are defined with the `<h1>` to `<h6>` tags.

<h3>HTML Paragraphs</h3>

HTML paragraphs are defined with the `<p>` tag.

### HTML Links

HTML links are defined with the `<a>` tag.

```
<a href="https://www.w3schools.com">This is a link</a>
```

`a`是“anchor”的缩写，而`href`是“hyperlink reference”的缩写。`a href`结构的完整示例看起来像这样：`<a href="http://www.example.com">链接文本</a>`。

这里，“anchor”表示我们正在创建一个可以被点击的链接，而"hyperlink reference"则指向该链接应该导向的网页或者位置。在尖括号`<a>`和`</a>`之间的部分是链接文本，也就是用户在网页上看到并且可以点击的部分。

所以，`a href`在HTML中的完整含义是定义一个链接，该链接将引导到由`href`指定的位置。

### HTML Images

HTML images are defined with the `<img>` tag.

The source file (`src`), alternative text (`alt`), `width`, and `height` are provided as attributes:

```
<img src="w3schools.jpg" alt="W3Schools.com" width="104" height="142">
```

## How to View HTML Source

Have you ever seen a Web page and wondered "Hey! How did they do that?"

### View HTML Source Code:

Click CTRL + U in an HTML page, or right-click on the page and select "View Page Source". This will open a new tab containing the HTML source code of the page.

### Inspect an HTML Element:

Right-click on an element (or a blank area), and choose "Inspect" to see what elements are made up of (you will see both the HTML and the CSS). You can also edit the HTML or CSS **on-the-fly** in the Elements or Styles panel that opens.

---

XHTML 是一种基于 XML 语言的 HTML （超文本标记语言）。全名为 eXtensible HyperText Markup Language，即可扩展超文本标记语言。

它是一种在网页设计中常用的语言，其主要目的是将 HTML 与 XML 结合在一起，以便在尽可能多的设备和应用程序中使用。与 HTML 相比，XHTML 更为严谨和清晰，例如，所有的元素必须闭合，标签必须正确地嵌套在其他标签中，所有的标签都必须小写等等。

XHTML 的出现是为了满足我们对于 WEB 标准和平台无关的需求。虽然现在 HTML5 由于其更大的灵活性和丰富的API支持在网页开发中更为常用，但 XHTML 仍旧在某些场合，例如需要严格的结构和清晰的语法规则的场合下发挥作用。

**Relative URL** - Links to an image that is hosted within the website. Here, the URL does not include the domain name. If the URL begins without a slash, it will be relative to the current page. Example: src="img_girl.jpg". If the URL begins with a slash, it will be relative to the domain. Example: src="/images/img_girl.jpg".

**Tip:** It is almost always best to use relative URLs. They will not break if you change domain.

---

You should always include the `lang` attribute **inside the `<html>` tag**, to declare the language of the Web page. This is meant to assist search engines and browsers.

The following example specifies English as the language:

```
<!DOCTYPE html>
<html lang="en">
<body>
...
</body>
</html>
```

Country codes can also be added to the language code in the `lang` attribute. So, the first two characters define the language of the HTML page, and the last two characters define the country.

The following example specifies English as the language and United States as the country:

```
<!DOCTYPE html>
<html lang="en-US">
<body>
...
</body>
</html>
```

---

The `title` attribute defines some extra information about an element.

The value of the title attribute will be displayed as a tooltip when you mouse over the element:

```
<p title="I'm a tooltip">This is a paragraph.</p>
```

鼠标悬停于该段落上方时，就会显示`I'm a tooltip`。也可以加入其他 elements。

各Attribute的值**并不要求加引号**，但建议如此（否则值内有空格之类符号就会导致出错）。单双引号都可以，从而可以根据值的内容中有的单双引号反过来使用。如果属性值中既包含单引号又包含双引号，则可以选择使用 HTML 实体来代替单引号或双引号：`<a title="Peter said, &quot;Hello, it's John.&quot;" href="#">链接</a>`，其中的`&quot;` 是双引号的 HTML 实体。这样，整个属性值就可以被包含在双引号中，而不会发生冲突。

The `style` attribute is used to add styles to an element, such as color, font, size, and more.

```
<p style="color:red;">This is a red paragraph.</p>
```

---

## HTML Headings

**Note:** Use HTML headings for headings only. Don't use headings to make text **BIG** or **bold**.

Each HTML heading has a default size. However, you can specify the size for any heading with the `style` attribute, using the CSS `font-size` property:

```
<h1 style="font-size:60px;">Heading 1</h1>
```

## HTML Paragraphs

The HTML `<p>` element defines a paragraph.

A paragraph always starts on a new line, and browsers automatically add some white space (a margin) before and after a paragraph.

## HTML Display

You cannot be sure how HTML will be displayed.

Large or small screens, and resized windows will create different results.

With HTML, you cannot change the display by adding **extra spaces or extra lines** in your HTML code.

The browser will automatically remove any extra spaces and lines when the page is displayed:

```
<p>
This paragraph
contains a lot of lines
in the source code,
but the browser
ignores it.
</p>

<p>
This paragraph
contains         a lot of spaces
in the source         code,
but the        browser
ignores it.
</p>
```

## HTML Horizontal Rules

The `<hr>` tag defines a thematic break in an HTML page, and is most often displayed as a horizontal rule.

The `<hr>` element is used to separate content (or define a change) in an HTML page:

```
<h1>This is heading 1</h1>
<p>This is some text.</p>
<hr>
<h2>This is heading 2</h2>
<p>This is some other text.</p>
<hr>
```

## HTML Line Breaks

The HTML `<br>` element defines a line break.

Use `<br>` if you want a line break (a new line) without starting a new paragraph.

## The Poem Problem

正常`<p>`元素中的诗行都会显示为一行（无论你在html中写的格式如何），所以要用到 `<pre>`（preformatted）元素：

The text inside a `<pre>` element is displayed in a fixed-width font (usually Courier), and it preserves both spaces and line breaks:

```
<pre>
  My Bonnie lies over the ocean.

  My Bonnie lies over the sea.

  My Bonnie lies over the ocean.

  Oh, bring back my Bonnie to me.
</pre>
```

## The HTML Style Attribute

Setting the style of an HTML element, can be done with the `style` attribute.

The HTML `style` attribute has the following syntax:

```
<tagname style="property:value;">
```

The ***property*** is a CSS property. The ***value*** is a CSS value.

## Background Color

The CSS `background-color` property defines the background color for an HTML element.

Set the background color for a page to powderblue:

```
<body style="background-color:powderblue;">

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
```

Set background color for two different elements:

```
<body>

<h1 style="background-color:powderblue;">This is a heading</h1>
<p style="background-color:tomato;">This is a paragraph.</p>

</body>
```

## Fonts

The CSS `font-family` property defines the font to be used for an HTML element:

```
<h1 style="font-family:verdana;">This is a heading</h1>
<p style="font-family:courier;">This is a paragraph.</p>
```

## Text Size

The CSS `font-size` property defines the text size for an HTML element:

```
<h1 style="font-size:300%;">This is a heading</h1>
<p style="font-size:160%;">This is a paragraph.</p>
```

## Text Alignment

The CSS `text-align` property defines the horizontal text alignment for an HTML element:

```
<h1 style="text-align:center;">Centered Heading</h1>
<p style="text-align:center;">Centered paragraph.</p>
```

---

## HTML Formatting Elements

Formatting elements were designed to display special types of text:

- `<b>` - Bold text
- `<strong>` - Important text
- `<i>` - Italic text
- `<em>` - Emphasized text
- `<mark>` - Marked text  黄色高亮
- `<small>` - Smaller text
- `<del>` - Deleted text
- `<ins>` - Inserted text 插入后加下划线
- `<sub>` - Subscript text
- `<sup>` - Superscript text

---

## HTML `<blockquote>` for Quotations

The HTML `<blockquote>` element defines a section that is quoted from another source.

Browsers usually indent `<blockquote>` elements.

```
<blockquote cite="http://www.worldwildlife.org/who/index.html">
For 50 years, WWF has been protecting the future of nature. The world's leading conservation organization, WWF works in 100 countries and is supported by 1.2 million members in the United States and close to 5 million globally.
</blockquote>
```

## HTML `<q>` for Short Quotations

The HTML `<q>` tag defines a short quotation.

Browsers normally insert quotation marks around the quotation. 感觉就是两端加了双引号。

## HTML `<abbr>` for Abbreviations

The HTML `<abbr>` tag defines an abbreviation or an acronym, like "HTML", "CSS", "Mr.", "Dr.", "ASAP", "ATM".

Marking abbreviations can give useful information to browsers, translation systems and search-engines.

**Tip:** Use the global title attribute to show the description for the abbreviation/acronym when you mouse over the element. 

```
<p>The <abbr title="World Health Organization">WHO</abbr> was founded in 1948.</p>
```

## HTML `<address>` for Contact Information

The HTML `<address>` tag defines the contact information for the author/owner of a document or an article.

The contact information can be an email address, URL, physical address, phone number, social media handle, etc.

The text in the `<address>` element usually renders in *italic,* and browsers will always add a line break before and after the `<address>` element.

```
<address>
Written by John Doe.<br>
Visit us at:<br>
Example.com<br>
Box 564, Disneyland<br>
USA
</address>
```

## HTML `<cite>` for Work Title

The HTML `<cite>` tag defines the title of a creative work (e.g. a book, a poem, a song, a movie, a painting, a sculpture, etc.).

**Note:** A person's name is not the title of a work.

The text in the `<cite>` element usually renders in *italic*.

## HTML `<bdo>` for Bi-Directional Override

BDO stands for Bi-Directional Override.

The HTML `<bdo>` tag is used to override the current text direction:

```
<bdo dir="rtl">This text will be written from right to left</bdo>
```

Bi-directional Override（双向覆盖）是指在显示包含混合左向和右向文本（例如，包含阿拉伯语或希伯来语（右向）和英语或法语（左向）的文本）的文本片段时所使用的一种技术。

在 Unicode 标准中，Bi-directional Override 是通过使用特殊的字符来实现的，即 Bi-directional Override, LTR（Left-to-Right，左向右）和 Bi-directional Override, RTL（Right-to-Left，右向左）。

当这些特殊字符在文本中出现时，它们会改变接下来的文本的阅读方向，直到遇到对应的 Pop directional formatting（PDF）字符或者文本结束。使用 Bi-directional Override 可以很好地处理混合了不同方向文本的问题，使得文本可以按照预期的方式显示和阅读。

# HTML Comments

HTML comments are not displayed in the browser, but they can help document your HTML source code.

## HTML Comment Tag

You can add comments to your HTML source by using the following syntax:

```
<!-- Write your comments here -->
```

## Hide Content

Comments can be used to hide content.

This can be helpful if you hide content temporarily:

```
<p>This is a paragraph.</p>

<!-- <p>This is another paragraph </p> -->

<p>This is a paragraph too.</p>
```

You can also hide more than one line. Everything between the `<!--` and the `-->` will be hidden from the display.

```
<p>This is a paragraph.</p>
<!--
<p>Look at this cool image:</p>
<img border="0" src="pic_trulli.jpg" alt="Trulli">
-->
<p>This is a paragraph too.</p>
```

Comments are also great for debugging HTML, because you can comment out HTML lines of code, one at a time, to search for errors.

## Hide Inline Content

Comments can be used to hide parts in the middle of the HTML code.

```
<p>This <!-- great text --> is a paragraph.</p>
```

# HTML Colors

HTML colors are specified with predefined color names, or with RGB, HEX, HSL, RGBA, or HSLA values.

![image-20240115203354152](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240115203354152.png)

HTML supports [140 standard color names](https://www.w3schools.com/colors/colors_names.asp).

## Background Color

You can set the background color for HTML elements.

## Text Color

You can set the color of text:

```
<h1 style="color:Tomato;">Hello World</h1>
<p style="color:DodgerBlue;">Lorem ipsum...</p>
<p style="color:MediumSeaGreen;">Ut wisi enim...</p>
```

## Border Color

You can set the color of borders:

![image-20240115203633090](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240115203633090.png)

```
<h1 style="border:2px solid Tomato;">Hello World</h1>
<h1 style="border:2px solid DodgerBlue;">Hello World</h1>
<h1 style="border:2px solid Violet;">Hello World</h1>
```

## Color Values

In HTML, colors can also be specified using RGB values, HEX values, HSL values, RGBA values, and HSLA values.

The following three <div> elements have their background color set with RGB, HEX, and HSL values:

![image-20240115203742492](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240115203742492.png)

The following two <div> elements have their background color set with RGBA and HSLA values, which add an Alpha channel to the color (here we have 50% transparency):

![image-20240115203812034](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240115203812034.png)

```
<h1 style="background-color:rgb(255, 99, 71);">...</h1>
<h1 style="background-color:#ff6347;">...</h1>
<h1 style="background-color:hsl(9, 100%, 64%);">...</h1>

<h1 style="background-color:rgba(255, 99, 71, 0.5);">...</h1>
<h1 style="background-color:hsla(9, 100%, 64%, 0.5);">...</h1>
```

An RGB color value represents RED, GREEN, and BLUE light sources.

An RGBA color value is an extension of RGB with an Alpha channel (opacity).

## Shades of Gray

Shades of gray are often defined using equal values for all three parameters:

![image-20240115204413944](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240115204413944.png)

# HTML HEX Colors

A hexadecimal color is specified with: #RRGGBB, where the RR (red), GG (green) and BB (blue) hexadecimal integers specify the components of the color.

## HEX Color Values

In HTML, a color can be specified using a hexadecimal value in the form:

\#*rrggbb*

Where rr (red), gg (green) and bb (blue) are hexadecimal values between 00 and ff (same as decimal 0-255).

For example, #ff0000 is displayed as red, because red is set to its highest value (ff), and the other two (green and blue) are set to 00.

Another example, #00ff00 is displayed as green, because green is set to its highest value (ff), and the other two (red and blue) are set to 00.

To display black, set all color parameters to 00, like this: #000000.

To display white, set all color parameters to ff, like this: #ffffff.

## Shades of Gray

Shades of gray are often defined using equal values for all three parameters:

![image-20240115204631494](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240115204631494.png)

# HTML HSL and HSLA Colors

HSL stands for hue, saturation, and lightness.

HSLA color values are an extension of HSL with an Alpha channel (opacity).

## HSL Color Values

In HTML, a color can be specified using hue, saturation, and lightness (HSL) in the form:

hsl(*hue*, *saturation*, *lightness*)

Hue is a degree on the color wheel from 0 to 360. 0 is red, 120 is green, and 240 is blue.

Saturation is a percentage value. 0% means a shade of gray, and 100% is the full color.

Lightness is also a percentage value. 0% is black, and 100% is white.

Experiment by mixing the HSL values below:

![image-20240115205030592](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240115205030592.png)

### Saturation

Saturation can be described as the intensity of a color.

100% is pure color, no shades of gray.

50% is 50% gray, but you can still see the color.

0% is completely gray; you can no longer see the color.

### Lightness

The lightness of a color can be described as how much light you want to give the color, where 0% means no light (black), 50% means 50% light (neither dark nor light), and 100% means full lightness (white).

## Shades of Gray

Shades of gray are often defined by setting the hue and saturation to 0, and adjusting the lightness from 0% to 100% to get darker/lighter shades.

## HSLA Color Values

HSLA color values are an extension of HSL color values, with an Alpha channel - which specifies the opacity for a color.

An HSLA color value is specified with:

hsla(*hue,* *saturation*, *lightness, alpha*)

The alpha parameter is a number between 0.0 (fully transparent) and 1.0 (not transparent at all)

---

# HTML Styles - CSS

CSS stands for Cascading Style Sheets.

CSS saves a lot of work. It can control the layout of multiple web pages all at once.

![image-20240115205442674](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240115205442674.png)

## What is CSS?

Cascading Style Sheets (CSS) is used to format the layout of a webpage.

With CSS, you can control the color, font, the size of text, the spacing between elements, how elements are positioned and laid out, what background images or background colors are to be used, different displays for different devices and screen sizes, and much more!

**Tip:** The word **cascading** means that a style applied to a parent element will also apply to all children elements within the parent. So, if you set the color of the body text to "blue", all headings, paragraphs, and other text elements within the body will also get the same color (unless you specify something else)!

## Using CSS

CSS can be added to HTML documents in 3 ways:

- **Inline** - by using the `style` attribute inside HTML elements
- **Internal** - by using a `<style>` element in the `<head>` section
- **External** - by using a `<link>` element to link to an external CSS file

The most common way to add CSS, is to keep the styles in external CSS files.

## Inline CSS

An inline CSS is used to apply a unique style to a single HTML element.

An inline CSS uses the `style` attribute of an HTML element.

The following example sets the text color of the `<h1>` element to blue, and the text color of the `<p>` element to red:

```
<h1 style="color:blue;">A Blue Heading</h1>

<p style="color:red;">A red paragraph.</p>
```

## Internal CSS

An internal CSS is used to define a style for a single HTML page.

An internal CSS is defined in the `<head>` section of an HTML page, within a `<style>` element.

The following example sets the text color of ALL the `<h1>` elements (on that page) to blue, and the text color of ALL the `<p>` elements to red. In addition, the page will be displayed with a "powderblue" background color: 

```
<!DOCTYPE html>
<html>
<head>
<style>
body {background-color: powderblue;}
h1   {color: blue;}
p    {color: red;}
</style>
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```

## External CSS

An external style sheet is used to define the style for many HTML pages.

To use an external style sheet, add a link to it in the `<head>` section of each HTML page:

```
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="styles.css">
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```

The external style sheet can be written in any text editor. The file must not contain any HTML code, and must be saved with a .css extension.

Here is what the "styles.css" file looks like:

```
body {
  background-color: powderblue;
}
h1 {
  color: blue;
}
p {
  color: red;
}
```

**Tip:** With an external style sheet, you can change the look of an entire web site, by changing one file!

## CSS Border

The CSS `border` property defines a border around an HTML element.

**Tip:** You can define a border for nearly all HTML elements.

```
p {
  border: 2px solid powderblue;
}
```

## CSS Padding

The CSS `padding` property defines a padding (space) between the text and the border.

```
p {
  border: 2px solid powderblue;
  padding: 30px;
}
```

## CSS Margin

The CSS `margin` property defines a margin (space) outside the border.

```
p {
  border: 2px solid powderblue;
  margin: 50px;
}
```

## Link to External CSS

External style sheets can be referenced with a full URL or with a path relative to the current web page.

在HTML中，"rel"是"relationship"（关系）的缩写。它用于定义当前文档与被链接文档之间的关系（也就是这个链接的目的或者功能）。举例来说，在link元素中常见的一些rel值有："stylesheet"（链接到一个CSS样式表），"icon"（定义网页的favicon图标），"alternate"（定义一个可替换的版本，如用于打印的样式表或者一个应用于移动设备的页面）等。

```
<link rel="stylesheet" href="https://www.w3schools.com/html/styles.css">  
# This example uses a full URL to link to a style sheet:
```

```
<link rel="stylesheet" href="/html/styles.css">
# This example links to a style sheet located in the html folder on the current web site: 
```

```
<link rel="stylesheet" href="styles.css">
# This example links to a style sheet located in the same folder as the current page:
```

---

## HTML Links - Syntax

The HTML `<a>` tag defines a hyperlink. It has the following syntax:

```
<a href="url">link text</a>
```

By default, links will appear as follows in all browsers:

- An unvisited link is underlined and blue
- A visited link is underlined and purple
- An active link is underlined and red

**Tip:** Links can of course be styled with CSS, to get another look!

## HTML Links - The target Attribute

By default, the linked page will be displayed in the current browser window. To change this, you must specify another target for the link.

The `target` attribute specifies where to open the linked document.

The `target` attribute can have one of the following values:

- `_self` - Default. Opens the document in the same window/tab as it was clicked
- `_blank` - Opens the document in a new window or tab
- `_parent` - Opens the document in the parent frame
- `_top` - Opens the document in the full body of the window

```
<a href="https://www.w3schools.com/" target="_blank">Visit W3Schools!</a>
```

在HTML中，`<a href>` 标签的 `target` 属性用于定义当点击链接时在何处打开链接地址。对于 `_parent` 和 `_top`，它们的功能是：

- `_parent` : 这个参数将在父窗口或者父框架打开链接，如果没有父窗口或者父框架，它的行为就和 `_self`（默认值，在当前窗口或者当前框架中打开链接）一样。
- `_top` : 这个参数将在整个窗口或者标签内打开链接，也就是说，它会清除所有的框架，并在没有框架的窗口中打开链接，如果没有创建框架，它的行为和 `_self` 一样。

注意：`_parent` 和 `_top` 主要用于那些将内容分解为多个框架的网页，在现代网站设计中，多框架的使用已经越来越少了。

## HTML Links - Use an Image as a Link

To use an image as a link, just put the `<img>` tag inside the `<a>` tag:

```
<a href="default.asp">
<img src="smiley.gif" alt="HTML tutorial" style="width:42px;height:42px;">
</a>
```

## Link to an Email Address

Use `mailto:` inside the `href` attribute to create a link that opens the user's email program (to let them send a new email):

```
<a href="mailto:someone@example.com">Send email</a>
```

## Button as a Link

To use an HTML button as a link, you have to add some JavaScript code.

JavaScript allows you to specify what happens at certain events, such as a click of a button:

```
<button onclick="document.location='default.asp'">HTML Tutorial</button>
```

## Link Titles

The `title` attribute specifies extra information about an element. The information is most often shown as a tooltip text when the mouse moves over the element.

```
<a href="https://www.w3schools.com/html/" title="Go to W3Schools HTML section">Visit our HTML Tutorial</a>
```

# HTML Links - Create Bookmarks

HTML links can be used to create bookmarks, so that readers can jump to specific parts of a web page.

------

## Create a Bookmark in HTML

Bookmarks can be useful if a web page is very long.

To create a bookmark - first create the bookmark, then add a link to it.

When the link is clicked, the page will scroll down or up to the location with the bookmark.

## Example

First, use the `id` attribute to create a bookmark:

```
<h2 id="C4">Chapter 4</h2>
```

Then, add a link to the bookmark ("Jump to Chapter 4"), from within the same page:

```
<a href="#C4">Jump to Chapter 4</a>
```

You can also add a link to a bookmark on another page:

```
<a href="html_demo.html#C4">Jump to Chapter 4</a>
```

## Chapter Summary

- Use the `id` attribute (id="*value*") to define bookmarks in a page
- Use the `href` attribute (href="#*value*") to link to the bookmark

# HTML Images

## HTML Images Syntax

The HTML `<img>` tag is used to embed an image in a web page.

Images are **not** technically inserted into a web page; images are **linked to** web pages. The `<img>` tag creates a holding space for the referenced image.

The `<img>` tag is empty, it contains attributes only, and does not have a closing tag.

The `<img>` tag has two required attributes:

- src - Specifies the path to the image
- alt - Specifies an alternate text for the image

```
<img src="url" alt="alternatetext">
```

## Image Size - Width and Height

You can use the `style` attribute to specify the width and height of an image.

```
<img src="img_girl.jpg" alt="Girl in a jacket" style="width:500px;height:600px;">
```

Alternatively, you can use the `width` and `height` attributes:

```
<img src="img_girl.jpg" alt="Girl in a jacket" width="500" height="600">
```

**Note:** Always specify the width and height of an image. If width and height are not specified, the web page might **flicker** while the image loads.

{% hideToggle flicker %}

在网络或者网页设计领域，"flicker"通常指的是屏幕上的图像或者网页内容出现快速的或者不规则的闪烁。这种问题可能由多种原因导致，比如显示器的刷新率问题，或者在网页加载或者更新信息时出现的短暂空白。

在网页或者应用设计中，"flicker"通常不是一个好的用户体验，因为它可以让用户感觉到不适或者干扰。因此，设计者通常会使用各种方法来尽量减少或者消除"flicker"，例如优化网页的加载速度，使用合适的动画来平滑过渡，或者确保显示器的刷新率和内容的更新频率匹配。

{% endhideToggle %}

## Width and Height, or Style?

The `width`, `height`, and `style` attributes are all valid in HTML.

However, we suggest using the `style` attribute. It prevents styles sheets from changing the size of images:

```
<!DOCTYPE html>
<html>
<head>
<style>
img {
  width: 100%;
}
</style>
</head>
<body>

<img src="html5.gif" alt="HTML5 Icon" width="128" height="128">

<img src="html5.gif" alt="HTML5 Icon" style="width:128px;height:128px;">

</body>
</html>
```

## Image as a Link

To use an image as a link, put the `<img>` tag inside the `<a>` tag:

```
<a href="default.asp">
  <img src="smiley.gif" alt="HTML tutorial" style="width:42px;height:42px;">
</a>
```

## Image Floating

Use the CSS `float` property to let the image float to the right or to the left of a text:

```
<p><img src="smiley.gif" alt="Smiley face" style="float:right;width:42px;height:42px;">
The image will float to the right of the text.</p>

<p><img src="smiley.gif" alt="Smiley face" style="float:left;width:42px;height:42px;">
The image will float to the left of the text.</p>
```

## Common Image Formats

Here are the most common image file types, which are supported in all browsers (Chrome, Edge, Firefox, Safari, Opera):

| Abbreviation | File Format                           | File Extension                   |
| :----------- | :------------------------------------ | :------------------------------- |
| APNG         | Animated Portable Network Graphics    | .apng                            |
| GIF          | Graphics Interchange Format           | .gif                             |
| ICO          | Microsoft Icon                        | .ico, .cur                       |
| JPEG         | Joint Photographic Expert Group image | .jpg, .jpeg, .jfif, .pjpeg, .pjp |
| PNG          | Portable Network Graphics             | .png                             |
| SVG          | Scalable Vector Graphics              | .svg                             |

------

# HTML Image Maps

With HTML image maps, you can create clickable areas on an image.

------

## Image Maps

The HTML `<map>` tag defines an image map. An image map is an image with clickable areas. The areas are defined with one or more `<area>` tags.

## How Does it Work?

The idea behind an image map is that you should be able to perform different actions depending on where in the image you click.

To create an image map you need an image, and some HTML code that describes the clickable areas.

------

------

## The Image

The image is inserted using the `<img>` tag. The only difference from other images is that you must add a `usemap` attribute:

```
<img src="workplace.jpg" alt="Workplace" usemap="#workmap">
```

The `usemap` value starts with a hash tag `#` followed by the name of the image map, and is used to create a relationship between the image and the image map.

## Create Image Map

Then, add a `<map>` element.

The `<map>` element is used to create an image map, and is linked to the image by using the required `name` attribute:

```
<map name="workmap">
```

The `name` attribute must have the same value as the `<img>`'s `usemap` attribute .

## The Areas

Then, add the clickable areas.

A clickable area is defined using an `<area>` element.

### Shape

You must define the shape of the clickable area, and you can choose one of these values:

- `rect` - defines a rectangular region
- `circle` - defines a circular region
- `poly` - defines a polygonal region
- `default` - defines the entire region

You must also define some coordinates to be able to place the clickable area onto the image. 

### Shape="rect"

The coordinates for `shape="rect"` come in pairs, one for the x-axis and one for the y-axis.

So, the coordinates `34,44` is located 34 pixels from the left margin and 44 pixels from the top:

![image-20240116180907418](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116180907418.png)

The coordinates `270,350` is located 270 pixels from the left margin and 350 pixels from the top:

![image-20240116181012363](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116181012363.png)

Now we have enough data to create a clickable rectangular area:

```
<area shape="rect" coords="34, 44, 270, 350" href="computer.htm">
```

This is the area that becomes clickable and will send the user to the page "computer.htm":

![image-20240116181132767](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116181132767.png)

### Shape="circle"

To add a circle area, first locate the coordinates of the center of the circle:

```
337,300
```

![image-20240116181242675](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116181242675.png)

Then specify the radius of the circle:

`44` pixels

![image-20240116181336656](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116181336656.png)

Now you have enough data to create a clickable circular area:

```
<area shape="circle" coords="337, 300, 44" href="coffee.htm">
```

This is the area that becomes clickable and will send the user to the page "coffee.htm":

![image-20240116181430221](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116181430221.png)

### Shape="poly"

The `shape="poly"` contains several coordinate points, which creates a shape formed with straight lines (a polygon).

This can be used to create any shape.

Like maybe a croissant shape!

How can we make the croissant in the image below become a clickable link?

![French Food](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/frenchfood.jpg)

![French Food](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/frenchfood4.jpg)

The coordinates come in pairs, one for the x-axis and one for the y-axis:

```
<area shape="poly" coords="140,121,181,116,204,160,204,222,191,270,140,329,85,355,58,352,37,322,40,259,103,161,128,147" href="croissant.htm">
```

This is the area that becomes clickable and will send the user to the page "croissant.htm":

![image-20240116181743439](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116181743439.png)

## Image Map and JavaScript

A clickable area can also trigger a JavaScript function.

Add a `click` event to the `<area>` element to execute a JavaScript function:

Here, we use the onclick attribute to execute a JavaScript function when the area is clicked:

```
<map name="workmap">
  <area shape="circle" coords="337,300,44" href="coffee.htm" onclick="myFunction()">
</map>

<script>
function myFunction() {
  alert("You clicked the coffee cup!");
}
</script>
```

# HTML Background Images

A background image can be specified for almost any HTML element.

------

## Background Image on a HTML element

To add a background image on an HTML element, use the HTML `style` attribute and the CSS `background-image` property:

```
<p style="background-image: url('img_girl.jpg');">
```

You can also specify the background image in the `<style>` element, in the `<head>` section:

```
<style>
p {
  background-image: url('img_girl.jpg');
}
</style>
```

## Background Image on a Page

If you want the entire page to have a background image, you must specify the background image on the `<body>` element:

```
<style>
body {
  background-image: url('img_girl.jpg');
}
</style>
```

## Background Repeat

To avoid the background image from repeating itself, set the `background-repeat` property to `no-repeat`.

```
<style>
body {
  background-image: url('example_img_girl.jpg');
  background-repeat: no-repeat;
}
</style>
```

## Background Cover

If you want the background image to cover the entire element, you can set the `background-size` property to `cover.`

Also, to make sure the entire element is always covered, set the `background-attachment` property to `fixed:`

This way, the background image will cover the entire element, with no stretching (the image will keep its original proportions):

```
<style>
body {
  background-image: url('img_girl.jpg');
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: cover;
}
</style>
```

## Background Stretch

If you want the background image to stretch to fit the entire element, you can set the `background-size` property to `100% 100%`.

Try resizing the browser window, and you will see that the image will stretch, but always cover the entire element.

```
<style>
body {
  background-image: url('img_girl.jpg');
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: 100% 100%;
}
</style>
```

# HTML `<picture>` Element

The HTML `<picture>` element allows you to display different pictures for different devices or screen sizes.

## The HTML <picture> Element

The HTML `<picture>` element gives web developers more flexibility in specifying image resources.

The `<picture>` element contains one or more `<source>` elements, each referring to different images through the `srcset` attribute. This way the browser can choose the image that best fits the current view and/or device.

Each `<source>` element has a `media` attribute that defines when the image is the most suitable.

```
<picture>
  <source media="(min-width: 650px)" srcset="img_food.jpg">
  <source media="(min-width: 465px)" srcset="img_car.jpg">
  <img src="img_girl.jpg">
</picture>
```

**Note:** Always specify an `<img>` element as the last child element of the `<picture>` element. The `<img>` element is used by browsers that do not support the `<picture>` element, or if none of the `<source>` tags match.

## When to use the Picture Element

There are two main purposes for the `<picture>` element:

### 1. Bandwidth

If you have a small screen or device, it is not necessary to load a large image file. The browser will use the first `<source>` element with matching attribute values, and ignore any of the following elements.

### 2. Format Support

Some browsers or devices may not support all image formats. By using the `<picture>` element, you can add images of all formats, and the browser will use the first format it recognizes, and ignore any of the following elements.

```
<picture>
  <source srcset="img_avatar.png">
  <source srcset="img_girl.jpg">
  <img src="img_beatles.gif" alt="Beatles" style="width:auto;">
</picture>
```

**Note:** The browser will use the first `<source>` element with matching attribute values, and ignore any following `<source>` elements.

---

# HTML Favicon

A favicon is a small image displayed next to the page title in the browser tab.

[favicon制作网站](https://www.favicon.cc/)

To add a favicon to your website, either save your favicon image to the root directory of your webserver, or create a folder in the root directory called images, and save your favicon image in this folder. A common name for a favicon image is "favicon.ico".

Next, add a `<link>` element to your "index.html" file, after the `<title>` element, like this:

```
<!DOCTYPE html>
<html>
<head>
  <title>My Page Title</title>
  <link rel="icon" type="image/x-icon" href="/images/favicon.ico">
</head>
<body>

<h1>This is a Heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```

Now, save the "index.html" file and reload it in your browser. Your browser tab should now display your favicon image to the left of the page title.

`<link>`标签能用来定义文档与外部资源的关系，在这种情况下，它用于链接到一个图标文件，这个文件通常在浏览器选项卡上显示。`rel="icon"` 定义了链接到的文件的用途，是一个图标文件。`type="image/x-icon"`定义了文件类型，是一个图像图标文件。 `href="/images/favicon.ico"`指定了图标文件的位置，即相对于web服务器主目录的“/images/”文件夹中的“favicon.ico”图标文件。

`type`属性是`<link>`标签的可选属性，它是用来指定资源的MIME类型。它不仅可以用于图标文件，还可以应用于其他许多不同类型的文件和资源。例如，如果你链接到一个CSS样式表，你可能会使用`type="text/css"`。

这里有一些其他常见的MIME类型：

- `text/html`：HTML文件
- `text/css`：CSS样式表
- `image/jpeg`：JPEG图像
- `image/png`：PNG图像
- `application/javascript`：JavaScript文件

这些只是MIME类型的一小部分，实际上有很多其他类型可以使用，依据你正在处理的具体资源类型而定。

Favicon File Format Support

The following table shows the file format support for a favicon image:

| Browser | ICO  | PNG  | GIF  | JPEG | SVG  |
| :------ | :--- | :--- | :--- | :--- | :--- |
| Edge    | Yes  | Yes  | Yes  | Yes  | Yes  |
| Chrome  | Yes  | Yes  | Yes  | Yes  | Yes  |
| Firefox | Yes  | Yes  | Yes  | Yes  | Yes  |
| Opera   | Yes  | Yes  | Yes  | Yes  | Yes  |
| Safari  | Yes  | Yes  | Yes  | Yes  | Yes  |

## HTML Link Tag

| Tag    | Description                                                  |
| :----- | :----------------------------------------------------------- |
| <link> | Defines the relationship between a document and an external resource |

# HTML Page Title

Every web page should have a page title to describe the meaning of the page.

```
<!DOCTYPE html>
<html>
<head>
  <title>HTML Tutorial</title>
</head>
<body>

The content of the document......

</body>
</html>
```

The `<title>` element adds a title to your page. The title is shown in the browser's title bar.

The title should describe the content and the meaning of the page.

The page title is very important for search engine optimization (SEO). The text is used by search engine algorithms to decide the order when listing pages in search results.

The `<title>` element:

- defines a title in the browser toolbar
- provides a title for the page when it is added to favorites
- displays a title for the page in search engine-results

So, try to make the title as accurate and meaningful as possible!

# HTML Tables

```
<table>
  <tr>
    <th>Company</th>
    <th>Contact</th>
    <th>Country</th>
  </tr>
  <tr>
    <td>Alfreds Futterkiste</td>
    <td>Maria Anders</td>
    <td>Germany</td>
  </tr>
  <tr>
    <td>Centro comercial Moctezuma</td>
    <td>Francisco Chang</td>
    <td>Mexico</td>
  </tr>
</table>
```

Each table cell is defined by a `<td>` and a `</td>` tag.

`td` stands for table data.

Everything between `<td>` and `</td>` are the content of the table cell.

**Note:** A table cell can contain all sorts of HTML elements: text, images, lists, links, other tables, etc.

## Table Rows

Each table row starts with a `<tr>` and ends with a `</tr>` tag.

`tr` stands for table row.

You can have as many rows as you like in a table; just make sure that the number of cells are the same in each row.

**Note:** There are times when a row can have less or more cells than another. 

## Table Headers

Sometimes you want your cells to be table header cells. In those cases use the `<th>` tag instead of the `<td>` tag:

`th` stands for table header.

<table class="ws-table-all notranslate">
<tbody><tr>
<th>Tag</th>
<th>Description</th>
</tr>
<tr>
<td><a href="/tags/tag_table.asp">&lt;table&gt;</a></td>
<td>Defines a table</td>
</tr>
<tr>
<td><a href="/tags/tag_th.asp">&lt;th&gt;</a></td>
<td>Defines a header cell in a table</td>
</tr>
<tr>
<td><a href="/tags/tag_tr.asp">&lt;tr&gt;</a></td>
<td>Defines a row in a table</td>
</tr>
<tr>
<td><a href="/tags/tag_td.asp">&lt;td&gt;</a></td>
<td>Defines a cell in a table</td>
</tr>
<tr>
<td><a href="/tags/tag_caption.asp">&lt;caption&gt;</a></td>
<td>Defines a table caption</td>
</tr>
<tr>
<td><a href="/tags/tag_colgroup.asp">&lt;colgroup&gt;</a></td>
<td>Specifies a group of one or more columns in a table for formatting</td>
</tr>
<tr>
<td><a href="/tags/tag_col.asp">&lt;col&gt;</a></td>
<td>Specifies column properties for each column within a &lt;colgroup&gt; element</td>
</tr>
<tr>
<td><a href="/tags/tag_thead.asp">&lt;thead&gt;</a></td>
<td>Groups the header content in a table</td>
</tr>
<tr>
<td><a href="/tags/tag_tbody.asp">&lt;tbody&gt;</a></td>
<td>Groups the body content in a table</td>
</tr>
<tr>
<td><a href="/tags/tag_tfoot.asp">&lt;tfoot&gt;</a></td>
<td>Groups the footer content in a table</td>
</tr>
</tbody></table>

# HTML Table Borders

HTML tables can have borders of different styles and shapes.

## How To Add a Border

To add a border, use the CSS `border` property on `table`, `th`, and `td` elements.

```
table, th, td {
  border: 1px solid black;
}
```

在CSS中，`border`属性常被用来给`table`、`th`（表头）和`td`（表格单元）元素添加边框。这是因为这些元素能直接包含内容，而边框实际上是环绕元素内容的线条。

相对地，`tr`（表行）元素是用来组织或者包含`th`和`td`元素的，它本身并不直接包含内容。如果你尝试给`tr`元素添加边框，你可能会发现并不能达到预期的效果，因为`tr`的边框通常会被内部的`td`或者`th`元素的边框覆盖。

然而，并非所有情况下都不能给`tr`元素添加边框，在一些特殊的布局或者设计中，可能需要给`tr`元素添加边框，例如你想要给整行数据添加一个统一的外边框，这时可能会用到`tr`的边框。

总的来说，是否给`tr`元素添加边框，取决于具体的需求和设计。如果为`table`，`th`和`td`添加边框能满足你的设计需求，那就没有必要给`tr`添加边框。如果需要，在`tr`上添加边框也是可行的，只是这可能需要一些额外的考虑与调整。

## Collapsed Table Borders

To avoid having double borders like in the example above, set the CSS `border-collapse` property to `collapse`.

This will make the borders collapse into a single border.

```
table, th, td {
  border: 1px solid black;
  border-collapse: collapse;
}
```

在CSS中，`border-collapse`属性是用来设置表格的边框样式的。

如果设置`border-collapse`属性为`collapse`，那么表格中相邻单元格的边框会合并（或者说"折叠"）成一个单独的边框，而不是每个单元格都有各自的边框。这就是"collapse"这个词在这里的意思，即相邻的边框会合并成一个单一的、更干净的边框，而不是重叠在一起，形成一种双层边框的效果。

例如，如果你在一个表格中为`th`或`td`元素设置了边框，每个单元格都会有自己的四边框。然而，如果你将`border-collapse`设置为`collapse`，那么相邻的单元格将会共享同一条边框，即相邻边框"折叠"在一起形成一个单一的边框。

这可以让表格看起来更整洁，特别是当表格有很多单元格或者行时，可以减少显示的边框数量，使表格看起来更简洁且更易于阅读。

## Style Table Borders

If you set a background color of each cell, and give the border a white color (the same as the document background), you get the impression of an invisible border:

![image-20240116204637012](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116204637012.png)

```
table, th, td {
  border: 1px solid white;
  border-collapse: collapse;
}
th, td {
  background-color: #96D4D4;
}
```

## Round Table Borders

With the `border-radius` property, the borders get rounded corners:

![image-20240116204725596](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116204725596.png)

```
table, th, td {
  border: 1px solid black;
  border-radius: 10px;
}
```

Skip the border around the table by leaving out `table` from the css selector:

![image-20240116204823934](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116204823934.png)

```
th, td {
  border: 1px solid black;
  border-radius: 10px;
}
```

## Dotted Table Borders

With the `border-style` property, you can set the appearance of the border.

![image-20240116204931681](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116204931681.png)

```
 th, td {
  border-style: dotted;
}
```

## Border Color

With the `border-color` property, you can set the color of the border.

![image-20240116205030369](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116205030369.png)

```
 th, td {
  border-color: #96D4D4;
}
```

# HTML Table Sizes

HTML tables can have different sizes for each column, row or the entire table.

![image-20240116205146325](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116205146325.png)

Use the `style` attribute with the `width` or `height` properties to specify the size of a table, row or column.

## HTML Table Width

To set the width of a table, add the `style` attribute to the `<table>` element:

```
<table style="width:100%">
  <tr>
    <th>Firstname</th>
    <th>Lastname</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Jill</td>
    <td>Smith</td>
    <td>50</td>
  </tr>
  <tr>
    <td>Eve</td>
    <td>Jackson</td>
    <td>94</td>
  </tr>
</table>
```

**Note:** Using a percentage as the size unit for a width means how wide will this element be compared to its parent element, which in this case is the `<body>` element.

## HTML Table Column Width

![image-20240116205440672](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116205440672.png)

To set the size of a specific column, add the `style` attribute on a `<th>` or `<td>` element:

```
<table style="width:100%">
  <tr>
    <th style="width:70%">Firstname</th>
    <th>Lastname</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Jill</td>
    <td>Smith</td>
    <td>50</td>
  </tr>
  <tr>
    <td>Eve</td>
    <td>Jackson</td>
    <td>94</td>
  </tr>
</table>
```

## HTML Table Row Height

![image-20240116205804434](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116205804434.png)

To set the height of a specific row, add the `style` attribute on a table row element:

```
<table style="width:100%">
  <tr>
    <th>Firstname</th>
    <th>Lastname</th>
    <th>Age</th>
  </tr>
  <tr style="height:200px">
    <td>Jill</td>
    <td>Smith</td>
    <td>50</td>
  </tr>
  <tr>
    <td>Eve</td>
    <td>Jackson</td>
    <td>94</td>
  </tr>
</table>
```

# HTML Table Headers

HTML tables can have headers for each column or row, or for many columns/rows.

![image-20240116205927792](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116205927792.png)

1. Table headers are defined with `th` elements. Each `th` element represents a table cell.

```
<table>
  <tr>
    <th>Firstname</th>
    <th>Lastname</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Jill</td>
    <td>Smith</td>
    <td>50</td>
  </tr>
  <tr>
    <td>Eve</td>
    <td>Jackson</td>
    <td>94</td>
  </tr>
</table>
```

## Vertical Table Headers

2. To use the first column as table headers, define the first cell in each row as a `<th>` element.

```
<table>
  <tr>
    <th>Firstname</th>
    <td>Jill</td>
    <td>Eve</td>
  </tr>
  <tr>
    <th>Lastname</th>
    <td>Smith</td>
    <td>Jackson</td>
  </tr>
  <tr>
    <th>Age</th>
    <td>94</td>
    <td>50</td>
  </tr>
</table>
```

## Align Table Headers

By default, table headers are bold and centered:

![image-20240116210753222](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116210753222.png)

To left-align the table headers, use the CSS `text-align` property:

```
th {
  text-align: left;
}
```

## Header for Multiple Columns

You can have a header that spans over two or more columns.

![image-20240116210841513](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116210841513.png)

To do this, use the `colspan` attribute on the `<th>` element:

```
<table>
  <tr>
    <th colspan="2">Name</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Jill</td>
    <td>Smith</td>
    <td>50</td>
  </tr>
  <tr>
    <td>Eve</td>
    <td>Jackson</td>
    <td>94</td>
  </tr>
</table>
```

## Table Caption

You can add a caption that serves as a heading for the entire table.

![image-20240116211008555](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240116211008555.png)

o add a caption to a table, use the `<caption>` tag:

```
<table style="width:100%">
  <caption>Monthly savings</caption>
  <tr>
    <th>Month</th>
    <th>Savings</th>
  </tr>
  <tr>
    <td>January</td>
    <td>$100</td>
  </tr>
  <tr>
    <td>February</td>
    <td>$50</td>
  </tr>
</table>
```

**Note:** The `<caption>` tag should be inserted immediately after the `<table>` tag.

# HTML Table Padding & Spacing

HTML tables can adjust the padding inside the cells, and also the space between the cells.

![image-20240117080141039](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240117080141039.png)

## HTML Table - Cell Padding

Cell padding is the space between the cell edges and the cell content.

By default the padding is set to **0**.

To add padding on table cells, use the CSS `padding` property:

```
th, td {
  padding: 15px;
}
```

To add padding only above the content, use the `padding-top` property.

And the others sides with the `padding-bottom`, `padding-left`, and `padding-right` properties:

```
th, td {
  padding-top: 10px;
  padding-bottom: 20px;
  padding-left: 30px;
  padding-right: 40px;
}
```

## HTML Table - Cell Spacing

Cell spacing is the space between each cell.

By default the space is set to **2 pixels**.

To change the space between table cells, use the CSS `border-spacing` property on the `table` element:

```
table {
  border-spacing: 30px;
}
```

# HTML Table Colspan & Rowspan

HTML tables can have cells that span over multiple rows and/or columns.

![image-20240117080643162](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240117080643162.png)

## HTML Table - Colspan

To make a cell span over multiple columns, use the `colspan` attribute:

```
<table>
  <tr>
    <th colspan="2">Name</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Jill</td>
    <td>Smith</td>
    <td>43</td>
  </tr>
  <tr>
    <td>Eve</td>
    <td>Jackson</td>
    <td>57</td>
  </tr>
</table>
```

**Note:** The value of the `colspan` attribute represents the number of columns to span.

## HTML Table - Rowspan

To make a cell span over multiple rows, use the `rowspan` attribute:

```
<table>
  <tr>
    <th>Name</th>
    <td>Jill</td>
  </tr>
  <tr>
    <th rowspan="2">Phone</th>
    <td>555-1234</td>
  </tr>
  <tr>
    <td>555-8745</td>
</tr>
</table>
```

**Note:** The value of the `rowspan` attribute represents the number of rows to span.

# HTML Table Styling

Use CSS to make your tables look better.

## HTML Table - Zebra Stripes

If you add a background color on every other table row, you will get a nice zebra stripes effect.

![image-20240117081730845](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240117081730845.png)

To style every other table row element, use the `:nth-child(even)` selector like this（写入head的style中）:

```
tr:nth-child(even) {
  background-color: #D6EEEE;
}
```

**Note:** If you use `(odd)` instead of `(even)`, the styling will occur on row 1,3,5 etc. instead of 2,4,6 etc.

## HTML Table - Vertical Zebra Stripes

To make vertical zebra stripes, style every other *column*, instead of every other *row*.

![image-20240117082338133](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240117082338133.png)

Set the `:nth-child(even)` for table data elements like this:

```
td:nth-child(even), th:nth-child(even) {
  background-color: #D6EEEE;
}
```

注意：表格的表示法中有整个表格的table，表头th，表数据td，表行tr，但没有表列！所以表列一般用 th + td 表示。

**Note:** Put the `:nth-child()` selector on both `th` and `td` elements if you want to have the styling on both headers and regular table cells.

## Combine Vertical and Horizontal Zebra Stripes

You can combine the styling from the two examples above and you will have stripes on every other row and every other column.

If you use a transparent color you will get an overlapping effect.

![image-20240117082719764](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240117082719764.png)

Use an `rgba()` color to specify the transparency of the color:

```
tr:nth-child(even) {
  background-color: rgba(150, 212, 212, 0.4);
}

th:nth-child(even),td:nth-child(even) {
  background-color: rgba(150, 212, 212, 0.4);
}
```

## Horizontal Dividers

![image-20240117082857050](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240117082857050.png)

If you specify borders only at the bottom of each table row, you will have a table with horizontal dividers.

Add the `border-bottom` property to all `tr` elements to get horizontal dividers:

```
tr {
  border-bottom: 1px solid #ddd;
}
```

## Hoverable Table

Use the `:hover` selector on `tr` to highlight table rows on mouse over:

![Video_2024-01-17_083638](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/Video_2024-01-17_083638.gif)

```
tr:hover {background-color: #D6EEEE;}
```

# HTML Table Colgroup

The `<colgroup>` element is used to style specific columns of a table.

If you want to style the two first columns of a table, use the `<colgroup>` and `<col>` elements.

![image-20240117084542734](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240117084542734.png)

The `<colgroup>` element should be used as a container for the column specifications.

Each group is specified with a `<col>` element.

The `span` attribute specifies how many columns that get the style.

The `style` attribute specifies the style to give the columns.

**Note:** There is a very limited selection of [legal CSS properties for colgroups](https://www.w3schools.com/html/html_table_colgroup.asp#legalcss).

```
<table>
  <colgroup>
    <col span="2" style="background-color: #D6EEEE">
  </colgroup>
  <tr>
    <th>MON</th>
    <th>TUE</th>
    <th>WED</th>
    <th>THU</th>
...
```

注意：分组命令中的 `col`和`span`是分开的。之前的"colspan" 用于定义单元格跨越的列数，而分开的 "col span" 用于在 colgroup 内定义一组具有相同属性的列数量。

**Note:** The `<colgroup>` tag must be a child of a `<table>` element and should be placed before any other table elements, like `<thead>`, `<tr>`, `<td>` etc., but after the `<caption>` element, if present.

## MLegal CSS properties

There is only a very limited selection of CSS properties that are allowed to be used in the colgroup:

`width` property
`visibility` property
`background` properties
`border` properties

All other CSS properties will have no effect on your tables.

## Multiple Col Elements

If you want to style more columns with different styles, use more `<col>` elements inside the `<colgroup>`:

```
<table>
  <colgroup>
    <col span="2" style="background-color: #D6EEEE">
    <col span="3" style="background-color: pink">
  </colgroup>
  <tr>
    <th>MON</th>
    <th>TUE</th>
    <th>WED</th>
    <th>THU</th>
...
```

![image-20240117085526498](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240117085526498.png)

## Empty Colgroups

If you want to style columns in the middle of a table, insert a "empty" `<col>` element (with no styles) for the columns before:

```
<table>
  <colgroup>
    <col span="3">
    <col span="2" style="background-color: pink">
  </colgroup>
  <tr>
    <th>MON</th>
    <th>TUE</th>
    <th>WED</th>
    <th>THU</th>
...
```

![image-20240117085656611](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240117085656611.png)

## Hide Columns

You can hide columns with the `visibility: collapse` property:

```
<table>
  <colgroup>
    <col span="2">
    <col span="3" style="visibility: collapse">
  </colgroup>
  <tr>
    <th>MON</th>
    <th>TUE</th>
    <th>WED</th>
    <th>THU</th>
...
```

















![image-20240118152543323](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240118152543323.png)
