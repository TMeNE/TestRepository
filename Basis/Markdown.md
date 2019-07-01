# 1. 标题
> 一级标题
> ===
> 二级标题
> ---

> # 一级标题
> ###### 六级标题
> 正文  
引用中强制换行

# 2. 段落
段落的前后要有空行，所谓的空行是指没有文字内容。  
若想在段内强制换行的方式是使用**两个以上**空格加上回车（引用中换行省略回车）。

# 3. 区块引用
> 区块引用
>> 嵌套引用

# 4. 代码区块
代码区块的建立是在每行加上4个空格或者一个制表符（如同写代码一样）。  
**注意**:需要和普通段落之间存在空行。

	void main(){
		printf("hello, markdown");
	}
	
# 5. 强调
*斜体*	_斜体_  
**粗体**	__粗体__

# 6. 列表
> - 第一项

>	1. 有序列表第一项
> 2. 有序列表第二项

# 7. 分割线
分割线最常使用就是三个或以上`*`，还可以使用`-`和`_`。

# 8. 链接
- 行内式  
[the file source](https://github.com/younghz/Markdown "Markdown/Readme")  
`[the file source](https://github.com/younghz/Markdown "Markdown/Readme")`  
- 参考式  
[the file source][1]  
`[the file source][1]`  
`[1]: https://github.com/younghz/Markdown "Markdown/Readme"`  

# 9. 图片
添加图片的形式和链接相似，只需在链接的基础上前方加一个`！`。  
![What did Times New Roman say to Comic Sans? - I hate your type!](https://s2.ax1x.com/2019/07/01/Z3vAvd.th.png)

# 10. 反斜杠&`
`\`转义符。  
\` 起到标记作用。

# 11. 列表
用`|`表示表格纵向边界，表头和表内容用`-`隔开，并可用`:`进行对齐设置，两边都有`:`则表示居中，若不加`:`则默认左对齐。

|表头|Content|
|:----:|----|
|Chrome|`stackedit` `markdown-here`|
|Online|`dillinger.io`|
|Website|`Apollo` `Moodle` `Reddit`|


---
本文内容来源：https://github.com/younghz/Markdown  
其他：[GITHUB FLAVORED MARKDOWN](https://guides.github.com/features/mastering-markdown/)

[1]: https://github.com/younghz/Markdown "Markdown/Readme"
