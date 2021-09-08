# fastspider

## 简介

**fastspider** 是一款上手非常简单的爬虫框架, 在很多设计上参考scrapy框架, 相比scrapy更加轻便与上手。 目前fastspider框架功能正在逐渐的完善中, fastspider内置多种爬虫, 如下:

- `LightSpider` 轻量级爬虫, 上手非常简答。基于内存队列进行任务处理, 适合于爬取数据量少的场景, 不支持断点续爬, 不支持分布式。

## 在线文档

- 文档：https://coco369.github.io/fastspider_doc

## 环境要求

- Python 3.8.0+
- Works on Linux, Windows, macOS

## 安装

From PyPi:

```shell
pip3 install fastspider
```    

## 小试一下

创建爬虫

```shell
fastspider startspider -s hello_spider 1/2
```

创建后的爬虫代码如下：

```python
# encoding=utf-8

import fastspider


class HelloSpider(fastspider.LightSpider):

    start_urls = ["http://www.baidu.com"]

    def start_requests(self):
        for url in self.start_urls:
            yield fastspider.Request(url)

    def parser(self, request, response):
        print(response)


if __name__ == "__main__":
    HelloSpider().start()

```

直接运行，打印如下：

```shell
<Response [200]>
无任务, 爬虫执行完毕
```

代码解释如下：

1. start_requests： 生产任务
2. parser： 解析器, 用于解析响应response
