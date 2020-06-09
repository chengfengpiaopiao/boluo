# DCL技术文档

**[项目官网 http://www.bying.io/](http://www.bying.io/)**

### 开发环境
    AndroidStudio3.3
    jdk8
    Gradle5.6.2 Gradle插件版本3.5.0
    compileSdkVersion 28
    buildToolsVersion 28.0.2
    flutter SDK v1.12.13+hotfix.9

### 打包配置
> 跟普通Android项目打包一样，配置签名文件，配置versionName，覆盖versionCode，命令行：flutter build apk


### 技术要点简介
    采用Flux->Redux，项目结构化，实现全局数据与状态管理。
    模块化项目结构，业务模块，网络模块，数据存储模块，Native插件模块，消息传递模块，
    UI组件以及基础常用工具模块。
    结合dio和RxDart搭建网络框架，实现集日志统计，多请求方式，请求结果类型解析，异常统一处理等功能。
	编写Flutter插件实现Flutter与Native进行交互-->云片验证。

### 核心文件/类
    native_share_plugin 分享插件工程
    native_yunpian_plugin 云片插件工程
    static 静态文件
    lib 目录
    	appConfig.dart 全局配置信息，包含网络环境，代理设置，常量
        develop_header.dart 共同依赖库
        common目录 通用工具模块
            business/intercepters目录 业务拦截器
            contant目录 常量（色值，本地SP）
            event目录 事件发送工具类
            extensions目录 基础类拓展
            locale目录 多语言工具
            net目录 网络模块
            util 通用工具类
        dao目录 网络请求管理模块
        model 实体bean
        page 页面
        test 单元测试
        ...