---
title: Hexo基础操作（二）
categories:
- tool
- hexo
tags:
- hexo
date: 2021-11-02 23:57:59
---
 hexo常用操作

<!-- more -->

# 添加摘要

  ```
---
摘要
<!-- more -->
正文
  ```

# 设置主页只显示摘要

```
# Automatically Excerpt. Not recommand.
# Please use <!-- more --> in the post to control excerpt accurately.
auto_excerpt:
  enable: true
```

#  创建草稿

```
hexo new draft "file name"
```

# 发布草稿为正式文章

```
hexo publish [layout] <filename>
```



# 参考资料

1. [Hexo 添加分类及标签](https://juejin.im/post/5cc11c41f265da038f7745b5)
2. [hexo之next主题添加分类](https://blog.csdn.net/u011240016/article/details/79422462)
3. [hexo博文分类数和标签数显示不正确？](https://www.zhihu.com/question/39130089)
4. [hexo.io doc](https://hexo.io/zh-cn/docs/front-matter)
5. [hexo新建文件草稿](https://www.jianshu.com/p/262372d14c90)

