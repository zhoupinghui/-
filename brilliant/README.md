# brilliant

#### 项目介绍
一个风格优雅，简洁美观的个人网站，可以帮助专业技术、设计人员快速打造自己的个人网站、在线简历。
简历个人信息都统一从JSON文件读取，所以如果没有页面个性化定制需求，只需要修改JSON文件对应的个人简历信息，就可以生成自己的网上简历了。

在线演示：[http://139.196.87.48:9002/brilliant/](http://139.196.87.48:9002/brilliant/)

#### 博客教程

[IT人如何打造个性化的个人网站（在线简历）](https://www.cnblogs.com/xifengxiaoma/p/9814902.html)

##### 前言
众所周知，IT行业人员在求职时，如果拥有自己的技术博客和个人网站多少是可以加些分的，因为这也是IT人的技术证明之一。内容丰富的技术博客就不必多少了，往往技术博客大神市场上多是供不应求的，而且技术博客出彩主要是在内容经营上，至于博客本身直接到各大技术平台注册一个即可，当然有兴趣的朋友想要自建个人博客也不是很难，比如可以用非常流行的GitHub Pages进行搭建，最主要是可以免费。而个人网站是主要是用来展示信息，功能比博客系统要简单的多，搭建过程比博客系统也要容易的多，而且对运行环境的要求也特别简单，很多时候只要浏览器即可开发和运行。接下来我们就来搭建一个在线简历类型的个人网站作为案例进行讲解。喜欢这个模板的朋友也可以直接修改JSON文件的个人信息定制自己专属的简历网站。

##### 选择模板
首先多多百度、谷狗一下，寻找到一款心仪的模板，注意关注一下模板使用的技术要适合自己为宜，以运行环境简单为宜，最好是纯HTML，只要一个浏览器就可以查看。

如果是使用到bootstrap、vue、angular等相关技术的模板，就可能需要在修改或安装部署的时候对相关技术有所了解了，下面是我模板之家找到的一款个人网站模板。

模板提供：模板之家

模板名称：亮绿色前端工程师web简历模板

下载地址：http://www.cssmoban.com/cssthemes/7585.shtml

![输入图片说明](https://images.gitee.com/uploads/images/2018/1026/141615_c8d96769_645970.png "屏幕截图.png")

整个网站简洁美观，颜色清新，富有个性化，使用的技术也比较简单，只要用浏览器就能直接查看，很适合用来打造个人网站。

网站包含基础信息、工作经验、教育经历、专业技能、作品展示等模块，我们可以根据自己的需要进行适当添加、删除和修改。

###### 基础信息
基础信息页面。

![输入图片说明](https://images.gitee.com/uploads/images/2018/1026/141646_066a7fea_645970.png "屏幕截图.png")

###### 工作经验
工作经验页面。

![输入图片说明](https://images.gitee.com/uploads/images/2018/1026/141900_a0d672db_645970.png "屏幕截图.png")

###### 专业技能
专业技能页面。

![输入图片说明](https://images.gitee.com/uploads/images/2018/1026/141910_aae235d3_645970.png "屏幕截图.png")


##### 业务分析
1.为了方便定制信息，我们决定把页面展示信息集中抽取到JSON文件，页面读取JSON文件信息进行展示。

2.将信息都抽取到JSON文件，当我们需要定制或修改简历信息的时候直接修改对应的JSON文件即可生效。

3.一般我们除了中文简历，有时也需要用到英文简历，所以我们的目标还要能支持中英文简历可以切换。

4.根据需求增删和修改模块，比如这里我们删除不需要的客户评价，增加一个项目经验的时间线类型模块。

##### 抽取信息
根据上面链接下载模板后，利用编辑器打开下载好的项目。

项目结构非常简单，主要是一个HTML文件，一个CSS文件。

我们新建两个.json文件，分别收集中英文简历的相关信息。

![输入图片说明](https://images.gitee.com/uploads/images/2018/1026/141928_8ba7c61a_645970.png "屏幕截图.png")

##### 读取信息
接下来我们从JSON文件读取信息显示到页面。因为我们做中英文切换时需要改变页面显示，所以我们选用Vue来进行数据绑定。

另外由于有些浏览器的跨域限制，在读取本地JSON文件时会出现跨域问题，所以这里需要借用客户端跨域技术JSONP来处理。

###### 下载Vue
下载 Vue.min.js ，放置到本地，如下图所示。

![输入图片说明](https://images.gitee.com/uploads/images/2018/1026/141940_3c63a719_645970.png "屏幕截图.png")


###### 引入Vue
打开 index.html，在页面直接引入就直接可以使用了。

![输入图片说明](https://images.gitee.com/uploads/images/2018/1026/141949_fd146f6a_645970.png "屏幕截图.png")

当然如果不想下载，你也可以直接使用CDN.

下推荐国外比较稳定的两个 CDN，国内还没发现哪一家比较好，目前还是建议下载到本地。

Staticfile CDN（国内） : https://cdn.staticfile.org/vue/2.2.2/vue.min.js

cdnjs : https://cdnjs.cloudflare.com/ajax/libs/vue/2.1.8/vue.min.js

###### 加载JSON
首先在JSON文件的外围加上JSONP的回调方法，如中文的加上 zh_cn({json info})。

然在在页面添加一个 zh_cn 同名函数，这样在json载入后，就会调用 zh_cn 这个函数。

zh_cn.json

![输入图片说明](https://images.gitee.com/uploads/images/2018/1026/142003_4bf6bed6_645970.png "屏幕截图.png")

en_us.json

![输入图片说明](https://images.gitee.com/uploads/images/2018/1026/142010_345e18f3_645970.png "屏幕截图.png")

 
然后在页面引入两个json文件，注意引用语句必须放置在回调函数之后。因为文件加载成功之后会进行回调，所以回调函数得先存在。


```
<script src="assets/language/en_us.json"></script>
<script src="assets/language/zh_cn.json"></script>
```

两个回调方法，将中英文简历信息加载并存入 localStorage， 并且在初始化页面和中英文切换时根据需求读取中文或英文简历信息。


```
<script type="text/javascript">
        function en_us(data) {
            window.localStorage.setItem("en_us", JSON.stringify(data))
        }
        function zh_cn(data) {
            window.localStorage.setItem("zh_cn", JSON.stringify(data))
            var vm = new Vue({
                name: 'resume',
                el: '#container',
                data: {
                    lang:'zh_cn',
                    language:null,
                    basicInfo:null,
                    experiences:null,
                    projects:null,
                    education:null,
                    skills:null,
                    portfolio:null,
                    contact:null
                },
                methods: {
                    changeLanguage: function () {
                        var zh_cn = 'zh_cn'
                        var en_us = 'en_us'
                        if(this.lang == zh_cn) {
                            this.lang = en_us
                            this.language = "Chinese"
                        } else {
                            this.lang = zh_cn
                            this.language = "英文简历"
                        }
                        var data = window.localStorage.getItem(this.lang)
                        if(data != null) {
                            data = JSON.parse(data)
                            this.basicInfo = data.basicInfo
                            this.experiences = data.experiences
                            this.projects = data.projects
                            this.education = data.education
                            this.skills = data.skills
                            this.portfolio = data.portfolio
                            this.contact = data.contact
                        }
                    }
                },
                mounted:function(){
                    this.changeLanguage()
                }
            })
        }
    </script>
```

就这么简单，完成之后只需要修改JSON信息就可以定制自己的网上简历了。定制完成直接丢到tomcat就可以了，服务器连重启都不用。

##### 测试效果
中文简历

![输入图片说明](https://images.gitee.com/uploads/images/2018/1026/142117_31159f8a_645970.png "屏幕截图.png")

英文简历

![输入图片说明](https://images.gitee.com/uploads/images/2018/1026/142145_983675cf_645970.png "屏幕截图.png")

专业技能

![输入图片说明](https://images.gitee.com/uploads/images/2018/1026/142153_e9f573c5_645970.png "屏幕截图.png")

项目经验

![输入图片说明](https://images.gitee.com/uploads/images/2018/1026/142159_ff1802b6_645970.png "屏幕截图.png")

作品展示

![输入图片说明](https://images.gitee.com/uploads/images/2018/1026/142205_41a08548_645970.png "屏幕截图.png")


#### 软件架构

- HTML

- JQuery

- Vue.js


#### 安装教程

1. 下载项目
  git clone https://gitee.com/liuge1988/brilliant.git

2. 运行项目
  直接打开index.html

3. 部署项目
  直接把项目扔到web服务器

#### 使用说明

1. xxxx
2. xxxx
3. xxxx

#### 参与贡献

1. Fork 本项目
2. 新建 Feat_xxx 分支
3. 提交代码
4. 新建 Pull Request


#### 码云特技

1. 使用 Readme\_XXX.md 来支持不同的语言，例如 Readme\_en.md, Readme\_zh.md
2. 码云官方博客 [blog.gitee.com](https://blog.gitee.com)
3. 你可以 [https://gitee.com/explore](https://gitee.com/explore) 这个地址来了解码云上的优秀开源项目
4. [GVP](https://gitee.com/gvp) 全称是码云最有价值开源项目，是码云综合评定出的优秀开源项目
5. 码云官方提供的使用手册 [https://gitee.com/help](https://gitee.com/help)
6. 码云封面人物是一档用来展示码云会员风采的栏目 [https://gitee.com/gitee-stars/](https://gitee.com/gitee-stars/)