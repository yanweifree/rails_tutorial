## 第五章 完善布局

BootStrap框架，自定义样式，局部视图

### 5.1 添加一些结构

    $ git checkout -b filling-in-layout

### 5.1.1 网站导航

**网站布局文件** app/views/layouts/application.html.erb

	<!DOCTYPE html>
	<html>
	  <head>
    	<title><%= full_title(yield(:title)) %></title>
    	<%= stylesheet_link_tag    "application", media: "all" %>
    	<%= javascript_include_tag "application" %>
    	<%= csrf_meta_tags %>
    	<!--[if lt IE 9]>
    	<script src="http://html5shim.googlecode.com/svn/trunk/html5.js"></script>
    	<![endif]-->
	  </head>
	  <body>
    	<header class="navbar navbar-fixed-top">
      	  <div class="navbar-inner">
            <div class="container">
              <%= link_to "sample app", '#', id: "logo" %>
              <nav>
                <ul class="nav pull-right">
                  <li><%= link_to "Home",    '#' %></li>
              	  <li><%= link_to "Help",    '#' %></li>
              	  <li><%= link_to "Sign in", '#' %></li>
            	</ul>
          	  </nav>
        	</div>
      	  </div>
    	</header>
        <div class="container">
      	  <%= yield %>
    	</div>
	  </body>
	</html>

**首页代码** app/views/static_pages/home.html.erb

	<div class="center hero-unit">
	  <h1>Welcome to the Sample App</h1>
	 
	  <h2>
    	This is the home page for the
    	<a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
    	sample application.
	  </h2>

	  <%= link_to "Sign up now!", '#', class: "btn btn-large btn-primary" %>
	</div>

	<%= link_to image_tag("rails.png", alt: "Rails"), 'http://rubyonrails.org/' %>

### 5.1.2 BootStrap 和自定义的CSS

**CSS样式** app/assets/stylesheets/custom.css.scss

	@import "bootstrap";

	/* universal */    // 全站使用的CSS

	/* typography */   // 精美的排版

	/* header */       // LOGO

	/* footer */       // 底部的CSS

### 5.1.3 局部视图

**网站布局** application.html.erb

	    <%= render 'layouts/shim' %>

	    <%= render 'layouts/header' %>

	      <%= render 'layouts/footer' %>

**HTML shim局部视图** _shim.html.erb

**网站头部的局部视图** _header.html.erb

**网站底部的局部视图** _footer.html.erb