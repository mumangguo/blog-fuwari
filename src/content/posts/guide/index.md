---
title: Fuwari简单教程
published: 2025-08-03
description: "如何使用此博客模板。"
image: "./cover.jpg"
tags: ["博客"]
category: Guides
draft: false
---
此博客模板是用 [Astro](https://astro.build/). 对于本指南中未提及的事项，您可以在 [Astro Docs](https://docs.astro.build/).

## 文章的 Front-matter

```yaml
---
title: My First Blog Post
published: 2023-09-09
description: This is the first post of my new Astro blog.
image: ./cover.jpg
tags: [Foo, Bar]
category: Front-end
draft: false
---
```

| 属性     | 描述                                                                                                                                                                                                 |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `title`       | 	文章的标题。                                                                                                                                                                                      |
| `published`   | 帖子发布的日期。                                                                                                                                                                            |
| `description` | 帖子的简短描述。显示在索引页上。                                                                                                                                                   |
| `image`       | 帖子的封面图片路径。<br/>1。以“http://”或“https://”开头：使用网络图像<br/>2。以“/”开头：用于“public”目录中的图像<br/>3。没有前缀：相对于markdown文件 |
| `tags`        | 帖子的标签。                                                                                                                                                                                       |
| `category`    | 帖子的类别。                                                                                                                                                                                   |
| `draft`        | 如果这篇文章仍然是草稿，则不会显示。                                                                                                                                                    |

## 如何放置文章文件



你的文章文件应该放在 `src/content/posts/` 目录中。你也可以创建子目录来更好地组织你的文章和资源。

```
src/content/posts/
├── post-1.md
└── post-2/
    ├── cover.png
    └── index.md
```
