# vuepress-theme-yubisaki [en]

[中文说明](https://wuwaki.me/yubisaki/)

## Installation

```bash
yarn add vuepress-theme-yubisaki -S
```
or with npm
```bash
npm install vuepress-theme-yubisaki --save-dev
```

## Article

**Render an overview of the article**
To generate a preview of the post on the cards, use excerpt by adding `<!-- more -->` after the first paragraph or first few introductory lines in your post.

```
## What is Vue.js -
In this post I will talk about Vue.js
<!-- more -->
Vue.js is awesome
```

As in the above form, adding the `<!-- more -->` tag to the `md` file, will render the content before this tag into the articles list as their preview.


## Articles meta-data
Use [yubisaki shell](https://github.com/Bloss/yubisaki-shell) to generate a new post with automatic date-time stamp, title and metadata etc. this helps the cards to sort according to date automatically, also filter the posts by tags etc.

install shell with 
```bash
yarn global add yubisaki-shell
```
and then from your project's root dir, run
```bash
yubisaki post -p <post-name> --page README.md
```
like if your post is named javascript, just run
```bash
yubisaki post -p javascript --page README.md
```

this will create a folder called javascript and a `README.md` file in it with required data automatically. You can then make changes to this file like changing the title and metadata, tags etc.

```yaml
title: Article title
# date is used for article sorting
date: 2017-08-15 10:27:26
tag: # Article tag, can be a String or an Array
  - js
  - react
# Meta tags that can be used to crawl by search engines
meta:
  - name: description
    content: Some description about your post
  - name: keywords # keywords Tags, will be queried when searching within pages
    content: theme vuepress
```
To let the theme filter by tags, add the following information alongside your previous themeConfig in `config.js` inside `.vuepress` folder

## tags

```js
module.exports = {
  themeConfig: {
    tags: true,
    nav: [
      { text: 'TAGS', link: '/tags/', tags: true }
    ]
  }
}
```

the above configuration let's theme know that `TAGS` field in the navbar is specifically for browsing tags from posts. When you visit the above path, it looks like following:

![](https://blog-1252181333.cossh.myqcloud.com/blog/180137.png)

![](https://blog-1252181333.cossh.myqcloud.com/blog/180218.png)

## Comment System

Use `gitalk` for comment system, click [gitalk](https://github.com/gitalk/gitalk) for more details.

But, don't support flipMoveOptions and render instane method

If you want to have more than one action button (in this case actionText and actionLink will be ignored):
```yaml
heroText: Yubisaki # title
activity: true # 使用自定义的 activity layout, 会收起右边的卡片栏
hidden: true # 设置是否在文章列表中显示
tagline: vuepress 博客主题 # 描述
heroImage: /static/logo.png # logo
# 参考官方默认主题的配置
# actionText: 了解一下 →  
# actionLink: /yubisaki/usage.html # action 链接
data:
  actions :
    - text : Action1
      link : /yubisaki/action1.html
    - text : Action2
      link : /yubisaki/action2.html
features:
  - title: 这是什么
    details: 一个基于 vuepress 的博客主题, 它基于 vuepress 提供的默认主题
  - title: 有哪些特点
    details: 提供文章列表, 文章分页, 文章详情, github card, 自定义活动页 layout 等等功能
  - title: TODO
    details: 标签云, TAG ARCHIVE, 一些脚本, 一些 开箱即用的layout
footer: by stickmy
```


## Configuration

For your reference, I have put the configuration of my blog (`.vuepress/config.js`) here: 

```js
module.exports = {
  // Enable custom themes
  theme: 'yubisaki',
  title: 'Yubisaki',
  description: 'vuepress theme Yubisaki',
  head: [
      ['link', { rel: 'icon', href: `/favicon.ico` }]
  ],
  port: 3000,
  // Google Analytics ID
  ga: 'xxxxx',
  // PWA support
  serviceWorker: true,
  // fuck IE
  evergreen: true,
  markdown: {
    // markdown-it-anchor options
    anchor: { permalink: true },
    // markdown-it-toc options
    toc: { includeLevel: [1, 2] },
    config: md => {
      md.use(require('markdown-it-task-lists')) // a checkbox TODO List plugin
        .use(require('markdown-it-imsize'), { autofill: true }) // Support for custom md image size ![test](image.png =100x200)
    }
  },
  // Yubisaki theme specific configuration
  themeConfig: {
    // Blog background image
    background: '/background/path',
    tags: true,
    // github card
    github: 'github username',
    // favicon image (logo)
    logo: '/logo/path',
    // Custom article title color
    accentColor: '#ac3e40',
    // Number of articles displayed per page
    per_page: 5,
    // The time format for creating an article. If not set, it will not be displayed. Optional [yyyy-MM-dd HH:mm:ss]
    date_format: 'yyyy-MM-dd',
    // options for comment (gitalk), don't support flipMoveOptions and render instane method
    comment: {
      clientID: 'GitHub Application Client ID',
      clientSecret: 'GitHub Application Client Secret',
      repo: 'GitHub repo',
      owner: 'GitHub repo owner',
      admin: ['GitHub repo owner and collaborators, only these guys can initialize github issues'],
      perPage: 5,
      id: location.pathname,      // Ensure uniqueness and length less than 50
      distractionFreeMode: false  // Facebook-like distraction free mode
    },
    // customize the links on the navigation bar
    nav: [
        { text: 'HOME', link: '/', root: true }, // Specify this as the root directory of the blog post
        { text: 'TAGS', link: '/tags/', tags: true }, // Specify the tags directory
        { text: 'GITHUB', link: 'https://github.com/bloss' },
        { text: 'about me', link: '/about/' }, 
    ]
  }
}
```


## customize the layout

Besides the basic `yaml` config generated by `yubisaki-shell`, you can add the following information to customize the layout as you want:

to customize the layout, add the following to the header of the `markdown` file

```yaml
heroText: Yubisaki # title
activity: true # Use a custom activity layout that will collapse the card bar on the right
hidden: true # Set whether to display in the article list
tagline: Vuepress blog theme # description
heroImage: /static/logo.png # logo
# Refer to the configuration of the official default theme for service static files
actionText: Learn about → 
actionLink: /yubisaki/usage.html
features:
  - title: what is this
    details: A vuepress-based blog theme based on the default theme provided by vuepress
  - title: What are the characteristics?
    details: Provide article list, article pagination, article details, github card, custom event page layout, etc.
  - title: TODO
    details: Tag cloud, TAG ARCHIVE, some scripts, some out of the box layout
footer: by stickmy
```

## Development, deployment

**In the docs directory (or the root of your project), be sure to put a markdown file called README.md for generating the root path, which can be an empty file**

You can use the following scripts to run the vuepress commands or you can run them directly, whichever you prefer

`package.json`:

```js
{
  "scripts": {
    "docs:dev": "vuepress dev {dirName}",
    "docs:build": "vuepress build {dirName}"
  }
}
```
If you haven't installed vuepress gloablly, these scripts will be helpful to find the vuepress binaries from `node_modules/.bin` directory and execute them on shell. to execute above scripts, run:
```bash
npm run docs:dev
```

or 
```bash
npm run docs:build
```
Accordingly.

## TODO

<<<<<<< HEAD
- 标签云
- 文章分类
- 更多类似 github card 的卡片
=======
- Tag Cloud
- Article classification
- More cards like github card
>>>>>>> bffa01b7f8507226eac86c008b45c5df14f671cb
