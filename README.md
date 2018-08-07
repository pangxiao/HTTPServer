# HTTPServer
HTTP 服务器，解析 get、 head 请求，可处理静态资源，支持 HTTP 长连接。 并发模型为 Reactor+非阻塞 IO+无锁化线程池，新连接用 Least-Load 分配
1. 使用 Epoll ET + Reactor 模式
2. 利用 CAS 设计无锁化线程池，主线程只负责 accept 请求，并以
Least-Load 的方式分发给其它 IO 线程。
3. 使用基于小根堆的定时器关闭超时请求
4. 使用 Webbench 对服务器进行压测（测试环境：CentOS 6.5 ，i5-6500，
4G）QPS 达到 3000
