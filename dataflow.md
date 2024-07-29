Spring Cloud Stream使用Spring Cloud Function提供的功能，分别将Supplier，Function，Consumer作为stream的发布者、处理器和消费者的处理函数。
发布数据

在Spring Cloud Stream中，发布数据的方式主要有两种，一种是通过Supplier自动触发，一种是通过StreamBridge通过外部数据源触发。
通过Supplier<T>自动触发

使用Supplier<T>作为stream的发布者，需要一种触发机制，来发起发布操作。Spring Cloud Stream提供了如下几种自动触发机制。
命令式（Imperative）编程模式的触发

如果使用的是命令式编程模式（Imperative），则直接在Supplier<T>上标注@Bean将之注册到Spring容器即可。默认Spring Framework会每隔1秒触发一次。
————————————————

                            版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。
                        
原文链接：https://blog.csdn.net/BASK2311/article/details/135757125



复制代码

   @Bean    Supplier<String> stringSupplier() {        return () -> {            String value = "Hello World!";            System.out.println("sent: " + value);            return value;       };   }

我们可以通过两种方式来调整触发频率：

    全局属性：spring.integration.poller.xxx
        设置所有函数的拉取频率

    每个绑定特定的属性：spring.cloud.stream.bindings.<binding-name>.producer.poller.xxx
        为某个特定的绑定设置拉取频率
————————————————

                            版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。
                        
原文链接：https://blog.csdn.net/BASK2311/article/details/135757125
