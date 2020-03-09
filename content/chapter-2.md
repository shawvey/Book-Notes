---
description: 在 HTML 中使用 JavaScript
---

# chapter 2

- 在HTML页面中插入JavaScript的主要方法，就是使用`<script>`元素。HTML4.01为`<script>`定义了下列6个属性。

  - **async**：可选。表示应该立即下载脚本，但不应妨碍页面中的其他操作比如下载其他资源或等待加载其他脚本。只对外部脚本文件有效。 
  - **charset**：可选。表示通过 src 属性指定的代码的字符集。
  - **defer**：可选。表示脚本可以延迟到文档完全被解析和显示之后再执行。
  - **language**： 已废弃
  - **src**：可选。表示包含要执行代码的外部文件。
  - **type**： 可选。可以看成是 language 的替代属性；表示编写代码使用的脚本语言的内容类型（也称为 MIME 类型）。服务器在传送 JavaScript 文件时使用的 MIME 类型通常是 application/x–javascript。目前 type 属性的值依旧还是 text/javascript。不过，这个属性并不是必需的，如果没有指定这个属性，则其默认值仍为 text/javascript。

- 使用`<script>`元素的方式有两种：直接在页面中嵌入 JavaScript 代码和包含外部 JavaScript 文件。 

- 在使用`<script>`嵌入 JavaScript代码时，记住不要在代码中的任何地方出现"`</script>`"字符串。 例如，浏览器在加载下面所示的代码时就会产生一个错误。因为按照解析嵌入式代码的规则，当浏览器遇到字符串"`</script>`"时，就会认为那是结束的` </script>`标签。而通过转义字符“/”可以解决这个问题，例如：

  ```javascript
  <script type="text/javascript"> 
    function sayScript(){
    	alert("</script>"); 
  	} 
  </script> 
  ```

- 如果要通过`<script>`元素来包含外部 JavaScript 文件，那么 src 属性就是必需的。这个属性的值是一个指向外部 JavaScript文件的链接:

  ```javascript
  <script type="text/javascript" src="example.js"></script> 
  ```

- 如果是在 XHTML文档中，也可以省略前面示例代码中结束的`</script>`标签，例如：

  ```javascript
  <script type="text/javascript" src="example.js" /> 
  ```

  但是，不能在 HTML文档使用这种语法。原因是这种语法不符合HTML规范，而且也得不到某些浏览器（尤其是 IE）的正确解析。 

- 只要不存在 defer 和 async 属性，浏览器都会按照`<script>`元素在页面中 出现的先后顺序对它们依次进行解析。在第一个`<script>`元素包含的代码解析完成后，第二个`<script>`包含的代码才会被解析，然后才是第三个、第四个...... 

- 在文档的`<head>`元素中包含所有 JavaScript文件，意味着必须等到全部 JavaScript代码都被下载、解析和执行完成以后，才能开始呈现页面的内容。对于那些需要很多 JavaScript 代码的页面来说，这无疑会导致浏览器在呈现页面时出现明显的延迟，而延迟期间的浏览器窗口中将是一片空白。为了避免这个问题，现代 Web 应用程序一般都把全部 JavaScript引用放在`<body>`元素中页面内容的后面。

  将需要解析的js代码插入到`<body>`中，会给用户一种打开页面速度变快的错觉。

- HTML 4.01为`<script>`标签定义了 defer 属性。这个属性的用途是表明脚本在执行时不会影响页面的构造，脚本会被延迟到整个页面都解析完毕后再运行。在`<script>`元素中设置defer属性，相当于告诉浏览器立即下载，但延迟执行。 HTML5规定按顺序执行，但实际上，延迟脚本不一定按照先后顺序执行。只适用于于外部脚本文件！嵌入脚本的defer属性被忽略。

- 只适用于于外部脚本文件！嵌入脚本的defer属性被忽略。与defer属性类似，都用于改变处理脚本。async只适用于外部脚本文件，并告诉浏览器立即下载文件。与 defer不同的是，标记为 async 的脚本并不保证按照指定它们的先后顺序执行。指定 async 属性的目的是不让页面等待两个脚本下载和执行，从而异步加载页面其他内容。建议异步脚本不要在加载期间修改 DOM。

- 可扩展超文本标记语言，即 XHTML（Extensible HyperText Markup Language） ，是将 HTML 作为 XML的应用而重新定义的一个标准。编写 XHTML代码的规则要比编写 HTML严格得多，而且直接影 响能否在嵌入 JavaScript代码时使用`<script/>`标签。📌HTML和XHTML要区分，XHTML要求更为严格。小于号(<)在后者中被当作开始一个新标签来解析。对于标签来讲，小于号后面不能跟空格，语法错误。保证让相同代码在 XHTML中正常运行的第二个方法，就是用一个 CData片段来包含 JavaScript代码。在XHTML（XML）中，CData片段是文档中的一个特殊区域，这个区域中可以包含不需要解析的任意格式的文本内容。因此，在 CData片段中就可以使用任意字符——小于号当然也没有问题，而且不会导致语法错误。在兼容 XHTML的浏览器中，这个方法可以解决问题。但实际上，还有不少浏览器不兼容 XHTML， 因而不支持 CData片段。

- hack还有一个引申义，指对某个程序或设备进行修改，使其完成原来不可用的功能（或者禁止外部使用者接触到的功能）

- IE5.5 引入了文档模式的概念，而这个概念是通过使用文档类型（doctype）切换实现的。两种文档模式是：混杂模式（quirks mode） 和标准模式（standards mode） 。混杂模式会让IE的行为与（包含非标准特性的）IE5相同，而标准模式则让IE的行为更接近标准行为。然这两种模式主要影响CSS 内容的呈现，但在某些情况下也会影响到 JavaScript的解释执行。

- 这 个问题的最终解决方案就是创造一个`<noscript>`元素，用以在不支持 JavaScript 的浏览器中显示替代 的内容。

- 符合上述任何一个条件，浏览器都会显示`<noscript>`中的内容。而在除此之外的其他情况下，浏览器不会呈现`<noscript>`中的内容。 