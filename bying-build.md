# Bying技术文档

### 开发环境
    AndroidStudio3.3
    jdk8
    Gradle4.4 Gradle插件版本3.0.1
    compileSdkVersion 28
    buildToolsVersion 28.0.2

### 打包配置
> 备注：项目根目录bying-config.build文件负责修改版本名称和版本号，gradle.properties文件负责修改apk名称。

1. 修改**bying-config.build**中的versionCode，versionName。
2. 修改**gradle.properties**
	属性名 | 说明 | 默认值 | jekinsp配置
    :----------- | :----------- | :----------- | :-----------
    isModule         | 是否开启组件化        | false | 0(1:可用)
    isUseForPhone	 | 手机/模拟机（APK压缩策略）true代表打包的时候对x86等模拟器支持的库文件不加入到apk中| true | 1
    shouldMinify	|  是否开启混淆	| false | 1
    VERSION_CODE	| apk名称-{VERSION_CODE}-.apk	| int类型 | 1
    isEncryptEwm	| 是否加密二维码(与硬件钱包匹配) | false | 1
    EWM_CONTAINT_ICON	| 是否显示二维码中心的icon|false|1
    EWM_VERSION_CODE	| 二维码版本号|0|1
    NETWORK_TYPE	| 网络配置（区分内网环境0，外网环境1，正式环境2）| 2 | 1
    shouldHotFix	| 是否开启热修复	| 1 | 1
    PROJECT_NAME	| apk名称-{PROJECT_NAME}-.apk	| string类型 | 1
    IS_JENKINS		| 是否开启jekins，注意：开启jekins后，需要修改app目录下build.gradle文件中apk输出路径，使用绝对路径此处与jekins服务器所在的目录有关，使用相对路径也需修改。|false|1
    PRODUCT_FLAAVOR_BUILD | jekins打包时apk渠道设置|base|1
    ENVIRONMENT		| jekins打包时apk环境配置|debug|1
    JENKINS_TIME    | jekins打包时间用作修改打包后apk名称 | 空字符串 | 1

3. 修改加固文件jiagubao-walle.bat
    > 注意本地环境配置的SDK路径是否配置正确。

    注意加固保账号和用户密码是否设置正确。

    注意签名文件的路径。

    注意加固保所需要的jar包目录和walle的jia包和脚本目录，以及多渠道配置文件所在的目录

4. 如何打普通测试apk？

	配置好1-2步骤所需要的定制化参数，进入项目根目录，执行gradle assembleRelease。

5. 如何打加固混淆后的apk？

	配置好1-3步骤后，在项目根目录，执行自定义的GradleTask命令--> **gradlew assembleRelease jiagubao_walle**

### 项目结构简介
    1. 子系统划分，Bying区块链客户端子系统划分为轻钱包子系统，中心化微账户子系统，冷钱包子系统。
    各子系统之间用户体系相互独立。中心化与去中心化系统之间的业务通过统一的接口接入，为Android实现插件化提供基础设计。
    2. 分层架构，实现项目组件化。
    第一层，业务Module层，将项目整体设计为HotModule主管热钱包服务，MicroModule主管中心化服务，ColdModule负责冷钱包业务。
    第二层，业务组件层，包含ByingSDK负责去中心化基础元素生成，TradingModule负责多个币种交易签名等。
    第三层，基础BaseModule搭建，主要功能为两部分，第三方SDK及框架集成和自研组件。
    3. 架构设计，整体采用MVP+Clean架构，实现展示层，业务逻辑层和数据层分离，降低业务耦
    合度，提高组件复用度和可测试度。
    4. 模块细化设计...

### 核心类
    **ApplicationModule**用作全局子模块管理
    **BDataBaseModel**数据库相关管理类
    **TradingManager**交易管理类，针对不同币种设计不同的策略，新增交易类型，需新增策略。