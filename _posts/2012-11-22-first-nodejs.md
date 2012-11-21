---
layout: post
category : lessons
tags : [intro, beginner, jekyll, tutorial]
---

最近弄了下node.js，写了个解析html来获取信息的demo。

初试手，那此blog来开刀了。。。。上代码先：

`test.js`

	var $ = require('jquery');
	var http = require('http');

	var options = {
    	host: 'blog.csdn.net',
    	port: 80,
    	path: '/lqg1122'
	};

	var html = '';
	http.get(options, function(res) {
    	res.on('data', function(data) {
        	// collect the data chunks to the variable named "html"
       		html += data;
    	}).on('end', function() {
        	// the whole of webpage data has been collected. parsing time!
        	var title = $(html).find('div h3 span').each(function($this){
            	var a = $(this).children('a').attr('href');
            	var b = $(this).children('a').text();
            	console.log(b + ":" + options.host + a);
        	});
        	console.log("over");
    	 });
	});




这里添加了jquery库来支持html解析，先前要先安装哦：
	$npm install jquery
这里对代码做一下解析：这里要实现的功能是，获取当前页面上博客目录的名称和链接地址，首先要先把整个页面的html获取，
options的参数分别是页面的资源域名，端口，路径；
前面定义的全局 html 变量意思为默认整个页面；
通过nodejs http模块的get方法来进行读取，同时开启了对数据的listern，当读取到数据时，触发‘data’；
当数据读取完毕，触发‘end’。所以解析将在数据读取完毕进行。

右键查看页面源码，要的就是若干段类似下面这段html代码中的href和文本内容：

	<div id="article_list" class="list">

    	<div class="list_item article_item">
        	<div class="article_title">
    	<span class="ico ico_type_Original"></span>
    	<h3>
        	<span class="link_title"><a href="/lqg1122/article/details/8172645">
        	利用 Jekyll-Bootstrap 搭建 github blog 简单记录
        	</a></span>
    	</h3>
	</div>




通过 .find() 方法找到了div 节点下的 h3 再找到接下来的节点 span，
由于匹配出来的会是多个object，所以这里加了each，对每个object都做同样操作（拿出href的值，拿出文本内容，然后输出在终端）。
这里要注意的地方是那href值的时候，html已经分解到span这节点了，看上面html源码片段可知，span节点下面还挂了两个节点，我们要的是a这个节点，所以就有children('a')，再取出值。运行一下node test.js可以看到终端有预期的输出。

感觉node.js还挺好玩的哈，可以慢慢玩～