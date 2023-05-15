[![Netlify Status](https://api.netlify.com/api/v1/badges/e02b4528-3571-4d04-b6cc-978e57d07240/deploy-status)](https://app.netlify.com/sites/101-camp/deploys)

# 101.camp
> 蟒营® 开源网络课程框架,官方网站

## 背景

- 自从 `PythoniCamp` 在08年成功折腾以来
- 一直就想发布课程独立官网
- 但是, 各种原因总也没合适域名以及形式和空间来组织
- 突然, 无意中抢到 `101.camp` 这种域名

## 目标

- 吻合 [SSGs (Static Site Generators)](https://about.gitlab.com/2016/06/10/ssg-overview-gitlab-pages-part-2/) 描述的所有美好
- 基于:　
    + [Static Site Generators](https://staticsitegenerators.net/)
    + [StaticGen \| Top Open Source Static Site Generators](https://www.staticgen.com/)
    + 等有关引擎推荐列表
- 选择:
    + 尽可能基于 Python
    + 排名靠前
    + 有同类网站实例
    + 样式选择多

## 工具

- 就用 [MkDocs \| StaticGen](https://www.staticgen.com/mkdocs)
- 配合 [MkDocs Bootswatch Themes - Journal](https://mkdocs.github.io/mkdocs-bootswatch/#journal)

## 运维

基于 Fabric2 分离的独立 [Invoke](http://docs.pyinvoke.org/en/1.2/index.html) ,
构建本地脚本来自动化:

- 网站编译
- 复制必要配置
- 发布文稿
- 发布编译结果网站

> gh-pages 复合使用:

- gh-pages 支持两种静态成果发布:
    + master 根目录
    + master `docs` 子目录
- MkDocs 不支持原稿和发布目录配置:
    + `docs` 是约定原稿入口目录
    + `site` 是编译网站输出目录

> 190324 发现有 diss 隐患, 以下仓库删除:

    * 创建 https://github.com/101camp/py 组织 MkDocs 工程
    * 创建 https://github.com/101camp/py.101.camp 容纳编译输出,并进行 gh-pages 发布

>> 190324 紧急切换为以下流程

- 内容: `Private`[PythoniCamp / running / 101.camp · GitLab](https://gitlab.com/pythonicamp/running/101.camp)
- 发布: `Private`[ZoomQuiet/gh101camp: 101.camp pages public](https://github.com/ZoomQuiet/gh101camp)
- 评注: [Issues · 101camp/comments](https://github.com/101camp/comments/issues)

- 发布流程(`暂时只能 DAMA 本地`): 
    + clone git@gitlab.com:pythonicamp/running/101.camp.git 为 `gl_101.camp`
    + clone git@github.com:ZoomQuiet/gh101camp.git 为 `zq_gh101camp`
    + 进入 `gl_101.camp` 将另外一个仓库链接为 `site` 目录
        * `ln -s ../zq_gh101camp/ site`
    + 在 `gl_101.camp/docs` 中自然编辑文稿
    + 在 `gl_101.camp/` 根目录中用 `inv` 命令进行编译和发布


> ༄  inv -l

    Available tasks:

      bu
      ccname
      gh
      pu
      pub
      sync4media

> ༄  inv pub

    /opt/data/Sites/101.camp/_running/gl_101.camp
    INFO    -  Cleaning site directory
    INFO    -  Building documentation to directory: /opt/data/Sites/101.camp/_running/gl_101.camp/site
    /opt/data/Sites/101.camp/_running/gl_101.camp
    On branch master
    Your branch is up-to-date with 'origin/master'.

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working direct

    ...


    no changes added to commit (use "git add" and/or "git commit -a")
    [master 27ffd07] 👌 IMPROVE: pub(site) gen. by MkDocs as invoke (at 190325 1205 03.402)
     2 files changed, 17 insertions(+), 17 deletions(-)
    To github.com:ZoomQuiet/gh101camp.git
       63b3707..27ffd07  master -> master



### MkDocs

本地编辑文档时, 推荐使用内置服务:
 
    ༄  mkdocs serve
    INFO    -  Building documentation...
    INFO    -  Cleaning site directory
    [I 190202 18:12:59 server:298] Serving on http://127.0.0.1:8000
    [I 190202 18:12:59 handlers:59] Start watching changes
    [I 190202 18:12:59 handlers:61] Start detecting changes
    ...

- 将自动监察文稿目录变化
- 自动编译
- 并发布本地网站为 http://127.0.0.1:8000
- 这样我们就可以打开浏览器:
    + 一边写
    + 一得保存, 本地网站就将自动更新
    + 看到最终将发布到 https://py.101.camp 真实效果


### inv

> ༄  inv -l
 
    Available tasks:

      bu
      ccname
      gh
      hollo
      pu
      pub

当前 `tasks.py` 中包含以上指令, 但日常只用一个:

- `inv pub` 将自动调用:
    + `bu` ~ MkDocs build 所有内容, 并输出到 `site` 为静态网站
    + `pu` ~ 将 `ghp_py` 内容自动化 push 到对应仓库
    + `ccname` ~ 将 gh-pages 依赖的 `CNAME` 配置文件复制到 `ghp_site`
    + `gh` ~ 将 `ghp_site` 内容自动化 push 到对应仓库



## 是也乎

- 200911 ZoomQuiet 增补 Netlify badges 
- 190325 ZoomQuiet 增补说明文档
- 190324 ZoomQuiet 紧急 black-box 化内容维护过程
- 190202 ZoomQuiet https+整体内容框架发布
- 190201 ZoomQuiet 完成原型发布
- 190131 ZoomQuiet init. 回到 gh-pages
- 190130 ZoomQuiet 尝试 gitlab-pages 失败
- 190129 ZoomQuiet 搜索/评估方案
- 181223 ZoomQuiet thinking


