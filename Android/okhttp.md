# okhttp

## okio

* 7zip

## 拦截器

* 拦截是核心

* 默认有5打拦截器

  * ```
    client.interceptors()
    ```

  * RetryAndFollowUpInterceptor

    * 重试,失败的情况下
    * 30x 重定向,响应投中有location,
    * dns 返回可能是多个ip地址,

  *  BridgeInterceptor

    * 桥接拦截器,
    * 加默认行为,比如host
    * 加请求头
    * 设置cookie,android中 token代替
    * gzip压缩,根据服务器的响应数据,
    * cookie 自己保存有api,

  * ```
    CacheInterceptor	
    ```

  * ```
    ConnectInterceptor
    ```

    连接 socket

  * ```
    client.networkInterceptors()	
    ```

    发起请求,qeuest,

* 请求是顺序的,响应是逆序的,
* 责任链模式,可能,责任链是行为模式
* chain链条 RealInterceptorChain,interceptors保持了拦截器,index 在RealCall.getResponseWithInterceptorChain 传入0,

###  发送请求

* request

* builder 建造者模式 

* 分发器 不是责任链模式

* newcall ->realCall

* 请求结束 调用Dispatcher finshed

* Dispatcher 分发器 提交到线程池 

* ```
  private int maxRequests = 64;
  private int maxRequestsPerHost = 5;
  ```

* 线程池 executorService 

* ```
  0, Integer.MAX_VALUE, 60, TimeUnit.SECONDS,
      new SynchronousQueue<>(), Util.threadFactory("OkHttp Dispatcher", false)
  ```

* 阻塞队列okhttp使用的是SynchronousQueue ,arrayblockqueue
* SynchronousQueue 是无容量的,会立即新建线程去执行,因为最大线程数是 Integer.MAX_VALUE
* arrayblockqueue 任务要等待 队列满了之后再新建非核心线程去run



### 其他

* android的httpurlconnection是个接口,android底层实现是okhttp