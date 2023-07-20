---
title: "ES multi_match+minimum_should_match用法"
date: 2023-07-20T20:23:52+08:00
draft: false
tags:
  - "es"
---
## ES multi_match+minimum_should_match用法
minimum_should_match的用法不多赘述，官网有，什么 3<90% 之类的。
这次说一下多字段查询multi_match配合minimum_should_match的用法
为了在多个字段上查询，同时控制最小匹配分词数量，可以使用这样的方式，这样会在title和tags上进行查询匹配，ik_smart分词结果为 [徐峥,沈腾,黄渤,吃火锅]，2个字段上进行查询，最少需要满足3个词语匹配，既满足3个词语即可。

```json {
　　"query": {
        "multi_match": {   // 多字段查询
        　　"query":"徐峥沈腾黄渤吃火锅", // 查询text
        　　"fields":["title","tags"], // 匹配title，tags 字段
        　　"minimum_should_match":3  // query分词后最少满足3个
        }
    }
}
```
这里的3是query词的匹配个数，而不是匹配次数。是需要这四个词里面满足3个匹配上，若一个词匹配多次不算哦，匹配多次的话好像分数会高一点。如图
![Alt text](/images/image.png)
![Alt text](/images/image-1.png)
![Alt text](/images/image-2.png)

参考：https://blog.csdn.net/deeqm66200/article/details/102108691