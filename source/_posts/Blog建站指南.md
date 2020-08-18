---
title: Github+Hexo+Next+Appveyor 建站指南
tags:
  - hexo
  - next
  - github
  - appveyor
categories:
  - Cloud
  - github
id: '165'
abbrlink: 2959710163
date: 2020-08-18 14:44:00
---


## 1、环境准备
{% blockquote %}
    OS：        Macos 10.15.6
    Node.js：   12.18.3 LTS
    Git：       自带
    tools：     Vscode
{% endblockquote %}

<!-- more -->

## 2、hexo博客框架安装
{% codeblock %}
    npm install -g hexo-cli
    mkdir Blog
    hexo init Blog
    cd Blog
    npm install
{% endcodeblock %}

## 3、next主题安装
{% codeblock %}
    npm install hexo-theme-next
    git clone https://github.com/next-theme/hexo-theme-next themes/next
{% endcodeblock %}

## 4、基础配置
### 4.1、hexo/_config.yml
- 4.1.1 设置标题等
{% codeblock %}
    title: Ye's Blog
    subtitle: 勤解万难
    description: 升级认知，看透本质
    keywords:
    author: ZorroYe
    language: zh-CN
    timezone: Asia/Shanghai
{% endcodeblock %}

- 4.1.2 设置博客主题
{% codeblock %}
    theme: next
{% endcodeblock %}

- 4.1.3 设置 hexo d 要上传的地址
{% codeblock %}
    deploy:
        type: git
        repo: https://github.com/zorroye/zorroye.github.io.git
{% endcodeblock %}

### 4.2、next/_config.yml
- 4.2.1 设置缓存
{% codeblock %}
    cache:
        enable: true
{% endcodeblock %}

- 4.2.2 设置logo
{% codeblock %}
    favicon:
        small: /images/favicon-16x16-yes.png
        medium: /images/favicon-32x32-yes.png
        apple_touch_icon: /images/apple-touch-icon-yes.png
        safari_pinned_tab: /images/logo.svg
{% endcodeblock %}

- 4.2.3 设置皮肤及颜色
{% codeblock %}
    # Schemes
    #scheme: Muse
    #scheme: Mist
    #scheme: Pisces
    scheme: Gemini

    # Dark Mode
    #darkmode: false
    darkmode: true
{% endcodeblock %}

- 4.2.4 设置菜单
{% codeblock %}
    cd Blog
    hexo new page tags
    hexo new page categorise
    hexo new page schedule
    mkdir Blog/source/404 && touch 404/index.md
{% endcodeblock %}
{% codeblock %}
    menu:
        home: / || fa fa-home
        about: /about/ || fa fa-user
        tags: /tags/ || fa fa-tags
        categories: /categories/ || fa fa-th
        archives: /archives/ || fa fa-archive
        schedule: /schedule/ || fa fa-calendar
        sitemap: /sitemap.xml || fa fa-sitemap
        commonweal: /404/ || fa fa-heartbeat
{% endcodeblock %}

- 4.2.5 设置联系方式
{% codeblock %}
social:
  QQ: qq:439753096?call|chat || fab fa-qq
  E-Mail: mailto:439753096@qq.com || fa fa-envelope
{% endcodeblock %}

- 4.2.6 设置友情链接
{% codeblock %}
    # Blog rolls
    links_settings:
        icon: fa fa-globe
        title: Links
        # Available values: block | inline
        layout: block

    links:
        黑果小兵: https://blog.daliansky.net/
        Sukka's Blog: https://blog.skk.moe/
        Xjn's Blog: https://blog.xjn819.com/
{% endcodeblock %}

- 4.2.7 设置打赏
{% codeblock %}
    reward_settings:
        # If true, a donate button will be displayed in every article by default.
        enable: true
        animation: false
        #comment: Buy me a coffee

    reward:
        wechatpay: /images/wechatpay.jpg
        alipay: /images/alipay.jpg
{% endcodeblock %}

- 4.2.8 设置回到顶部
{% codeblock %}
    back2top:
        enable: true
        # Back to top in sidebar.
        sidebar: true
        # Scroll percent label in b2t button.
        scrollpercent: true
{% endcodeblock %}

- 4.2.9 设置角标
{% codeblock %}
    github_banner:
        enable: true
        permalink: https://github.com/zorroye
        title: Follow me on GitHub
{% endcodeblock %}

- 4.2.10 设置TOC
{% codeblock %}
    toc:
        enable: true
        # Automatically add list number to toc.
        number: false
        # If true, all words will placed on next lines if header width longer then sidebar width.
        wrap: true
        # If true, all level of TOC in a post will be displayed, rather than the activated part of it.
        expand_all: true
        # Maximum heading depth of generated toc.
        max_depth: 3
{% endcodeblock %}

## 5、个性化配置
### 5.1、hexo/_config.yml
- 5.1.1 永久链接
{% codeblock %}
    npm install hexo-abbrlink --save
{% endcodeblock %}
{% codeblock %}
    url: https://zorroye.github.io/
    root: /
    # permalink: :year/:month/:day/:title/
    # permalink_defaults:
    permalink: posts/:abbrlink/
    abbrlink:
        alg: crc32 #support crc16(default) and crc32
        rep: dec   #support dec(default) and hex
    pretty_urls:
        trailing_index: true # Set to false to remove trailing 'index.html' from permalinks
        trailing_html: true # Set to false to remove trailing '.html' from permalinks
{% endcodeblock %}

- 5.1.2 本地搜索
{% codeblock %}
    npm install hexo-generator-searchdb --save
{% endcodeblock %}
{% codeblock %}
    search:
        path: search.xml
        pield: post
        format: html
        limit: 10000 
{% endcodeblock %}
{% codeblock %}
    local_search:
        enable: true
        # If auto, trigger search by changing input.
        # If manual, trigger search by pressing enter key or search button.
        trigger: auto
        # Show top n results per article, show all results by setting to -1
        top_n_per_article: 1
        # Unescape html strings to the readable one.
        unescape: false
        # Preload the search data when the page loads.
        preload: false
{% endcodeblock %}

- 5.1.3 字数统计
{% codeblock %}
    npm install hexo-word-counter --save
{% endcodeblock %}
{% codeblock %}
    symbols_count_time:
        symbols: true
        time: true
        total_symbols: true
        total_time: true
        awl: true
        wpm: 275
{% endcodeblock %}
next/_config.yml也要配置
{% codeblock %}
    symbols_count_time:
        separated_meta: true
        item_text_post: true
        item_text_total: false
{% endcodeblock %}


- 5.1.4 站点地图
{% codeblock %}
    npm install hexo-generator-sitemap --save
    npm install hexo-generator-baidu-sitemap --save
{% endcodeblock %}
    网站设置：略
{% codeblock %}
    Plugins:
      - hexo-generator-baidu-sitemap
      - hexo-generator-sitemap

    baidusitemap:
        path: baidusitemap.xml

    sitemap:
        path: sitemap.xml
{% endcodeblock %}

- 5.1.5 看板娘
{% codeblock %}
    npm install hexo-helper-live2d@3.x --save
    npm install live2d-widget-model-miku --save
{% endcodeblock %}
{% codeblock %}
    live2d: 
        enable: true 
        scriptFrom: local 
        pluginRootPath: live2dw/ 
        pluginJsPath: lib/ 
        pluginModelPath: assets/ 
        tagMode: false 
        log: false 
        model: 
            use: live2d-widget-model-miku
        display:
            position: right 
            width: 260 
            height: 400 
        mobile: 
            show: true 
        react: 
            opacity: 0.8
{% endcodeblock %}

### 5.2、next/_config.yml
- 5.2.1 添加评论功能
{% codeblock %}
    valine:
        enable: true
        appId: hDUtOYptQ2tkDzGUszvs3g4N-gzGzoHsz # Your leancloud application appid
        appKey: 6bM5r8tXF8x5HTop81N5Iz5z # Your leancloud application appkey
        placeholder: Just go go # Comment box placeholder
        avatar: mm # Gravatar style
        meta: [nick, mail, link] # Custom comment header
        pageSize: 10 # Pagination size
        language: zh-cn # Language, available values: en, zh-cn
        visitor: true # Article reading statistic
        comment_count: true # If false, comment count will only be displayed in post page, not in home page
        recordIP: true # Whether to record the commenter IP
        serverURLs: # When the custom domain name is enabled, fill it in here (it will be detected automatically by default, no need to fill in)
        enableQQ: false # Whether to enable the Nickname box to automatically get QQ Nickname and QQ Avatar
        requiredFields: [] # Set required fields: ['nick'] | ['nick','mail']
        #post_meta_order: 0
{% endcodeblock %}

## 6、文章迁移
{% codeblock %}
    npm install hexo-migrator-wordpress --save
    hexo migrate wordpress <source>
{% endcodeblock %}

## 7、appveyor自动更新
{% codeblock %}
    clone_depth: 5
    environment:
    nodejs_version: "12"
    access_token:
        secure: KVCa2He1FC4lxjT8fIM6Kz/eM+k54JLP1jF1lL60YwVk67A7YFOufqpCz2gopRfL
    install:
        - ps: Install-Product node $env:nodejs_version
        - npm install
        - node --version
        - npm --version
        - npm install
        - npm install hexo-cli -g
        - npm install hexo-theme-next --save
        - npm install gulp --save
        - npm install hexo-abbrlink --save
        - npm install hexo-generator-searchdb --save
        - npm install hexo-generator-sitemap --save
        - npm install hexo-generator-baidu-sitemap --save
        - npm install hexo-word-counter --save
        - npm install hexo-helper-live2d@3.x --save
        - npm install live2d-widget-model-miku --save
{% endcodeblock %}

## 8、参考文档：
{% blockquote %}
    https://hexo.io/zh-cn/docs/
    https://theme-next.js.org/
    https://cloud.tencent.com/developer/article/1662817#
{% endblockquote %}

