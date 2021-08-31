# 命令行工具

命令行工具为**fastspider**内置支持的，可方便快速的创建项目、爬虫等，使用方法如下：

## 1.查看支持的命令行

打开命令行窗口，输入fastspider

    > fastspider
    fastspider Version: 1.0.20
    
    Usage:
      fastspider <command> [options] [args]
    
    Available commands:
      startproject        create project
      startspider         create spider
    
    Use "fastspider <command> -h to see more info about a command


可见fastspider支持`startproject`及`startspider`两种命令

## 2. fastspider startproject

使用fastspider startproject 可快速创建项目，具体支持的命令可输入`fastspider startproject -h` 查看使用帮助

    > fastspider startproject -h
    
    待开发

具体使用方法如下：

#### 1. 创建爬虫项目

命令

    fastspider startproject -p <project_name>

示例：

    fastspider startproject -p hello-project


#### 2. 创建爬虫

爬虫分为3种，分别为 轻量级爬虫（LightSpider）、分布式爬虫（NomalSpider）以及 周期性爬虫（CycleSpider）

命令

    fastspider startspider -s <spider_name> <spider_type>

* LightSpider 对应的 spider_type 值为 light
* NomalSpider 对应的 spider_type 值为 nomal
* CycleSpider 对应的 spider_type 值为 cycle

LightSpider 爬虫示例：

    fastspider startspider -s hello_spider light


生成 hello_spider.py, 内容如下：

    # encoding=utf-8
    
    import fastspider


    class HelloSpider(fastspider.LightSpider):
    
        start_urls = ["http://www.baidu.com"]
    
        def start_requests(self):
            for url in self.start_urls:
                yield fastspider.Request(url)
    
        def parser(self, request, response):
            print(response.text)
    
    if __name__ == "__main__":
        HelloSpider().start()


若为项目结构，建议先进入到spiders目录下，再创建爬虫

#### 3. 运行爬虫命令

HelloSpider 爬虫运行命令 示例：

    fastspider crawl -s hello_spider.HelloSpider -c <thread_count>

其中 -s参数表示  HelloSpider类的文件位置

​		-c参数表示 启动爬虫线程的个数

