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

访问[http://localhost:3000/static_pages/home](http://localhost:3000/static_pages/home)查看页面。

**控制器** app/controllers/static_pages_controller.rb

    class StaticPagesController < ApplicationController
      def home
      end
      .
    end

**视图** app/views/static_pages/home.thml.erb

    <h1>StaticPages#home</h1>
    <p>Find me in app/views/static_pages/home.html.erb</p>
