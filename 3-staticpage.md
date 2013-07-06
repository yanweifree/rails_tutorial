## 第三章 基本的静态页面

静态页面，自动化测试，有点动态内容的页面。

    $ rails new sample_app --skip-test-unit

    $ rails generate rspec:install

### 3.1 静态页面
 
    $ git checkout -b static-pages

    $ rails generate controller StaticPages home help --no-test-framework

**路由** config/routes.rb

    SampleApp::Application.routes.draw do
      get "static_pages/home"
      get "static_pages/help"
      .
    end

访问[static_pages/home](http://localhost:3000/static_pages/home)查看页面。

**控制器** app/controllers/static_pages_controller.rb

    class StaticPagesController < ApplicationController
      def home
      end
      .
    end

**视图** app/views/static_pages/home.thml.erb

    <h1>StaticPages#home</h1>
    <p>Find me in app/views/static_pages/home.html.erb</p>

### 3.2 第一个测试

BDD行为驱动测试，集成测试，单元测试，Capybara句法

失败-实现-通过, Red-Green-Refactor

**生成集成测试**

    rails generate integration_test static_pages

spec/requests/static_pages_spec.rb

    describe "Home pages" do
      it "should have the content 'Sample App'" do
        visit '/static_pages/home'
        page.should have_content('Sample App')
      end
    end

**测试**

    $ bundle exec rspec spec/requests/static_pages_spec.rb

**测试失败**

**修改首页代码** app/views/static_pages/home.html.erb

    <h1>Sample App</h1>
    <p>
    This is the home page for the 
    <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
    sample application.
    </p>

**再次测试通过**

### 3.3 有点动态内容的页面

**标题测试**

    it "should have the right title" do
      visit '/static_pages/home'
      page.should have_selector('title', 
                    :text => "Ruby on Rials Tutorial Sample App | Home")

**修改首页代码** app/views/static_pages/about.html.erb

    <!DOCTYPE html>
    <html>
      <head>
        <title>Ruby on Rails Tutorial Sample App | Home</title>
      </head>
      <body>
        <h1>Sample App</h1>
        <p>
          This is the home page for the
          <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
          sample application.
        </p>
      </body>
    </html>

**修改帮助代码** app/views/static_pages/help.html.erb

	<!DOCTYPE html>
	<html>
	  <head>
    	<title>Ruby on Rails Tutorial Sample App | Help</title>
	  </head>
	  <body>
		<h1>Help</h1>
		<p>
		  Get help on the Ruby on Rails Tutorial at the
		  <a href="http://railstutorial.org/help">Rails Tutorial help page</a>.
      	  To get help on this sample app, see the
          <a href="http://railstutorial.org/book">Rails Tutorial book</a>.
        </p>
	  </body>
	</html>

**修改关于代码** app/views/static_pages/about.html.erb

	<!DOCTYPE html>
	<html>
	  <head>
        <title>Ruby on Rails Tutorial Sample App | About Us</title>
	  </head>
	  <body>
    	<h1>About Us</h1>
    	<p>
      	  The <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
      	  is a project to make a book and screencasts to teach web development
      	  with <a href="http://rubyonrails.org/">Ruby on Rails</a>. This
      	  is the sample application for the tutorial.
    	</p>
	  </body>
	</html>

**嵌入式Ruby**

**修改布局文件**app/views/layouts/application.html.erb

    <!DOCTYPE html>
    <html>
	  <head>
		<title>Ruby on Rails Tutorial Sample App | <%= yield(:title) %></title>
		<%= stylesheet_link_tag    "application", :media => "all" %>
		<%= javascript_include_tag "application" %>
		<%= csrf_meta_tags %>
	  </head>
	  <body>
		<%= yield %>
	  </body>
	</html>

**去除完整的HTML结构后的首页**

	<% provide(:title, 'Home') %>
	<h1>Sample App</h1>
	<p>
	  This is the home page for the
	  <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
	  sample application.
	</p>