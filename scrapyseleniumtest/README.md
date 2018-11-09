# scrapy与selenium对接
- 原理
    - 在Downloader Middleware 中的process_request()方法返回Response对象时，接下来更低优先级的Downloader Middlerware的
      process_request()和process_exception()方法就不会被继续调用了，转而依次开始执行每个Downloader Middleware的
      process_response()方法，调用完毕后直接将Response对象发送给Spider处理。
      本示例中就是在Selenium的Downloader Middleware中返回了一个HtmlResponse，它是Response的子类，同样满足此条件，
      返回之后便会顺次调用每个Downloader Middleware的process_response()方法，而在process_response()中我们没有对其
      做特殊处理，接着他就会被发送给Spider，传给Request的回调函数进行解析。