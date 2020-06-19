#实验6report

##问答题

- Namespace技术

  用来修改进程视图的主要方法。 如**PID Namespace**它是 Linux 创建新进程的一个可选参数，当我们用 clone() 系统调用创建一个新进程时，就可以在参数中指定 CLONE_NEWPID 参数，这时，新创建的这个进程将会“看到”一个全新的进程空间，在这个进程空间里，它的 PID 是 1。

- Cgroups

  **Cgroups 就是内核中用来为进程设置资源限制的一个重要功能。它的最主要的作用，就是限制一个进程组能够使用的资源上限，包括 CPU、内存、磁盘、网络带宽等等。**此外，Cgroups 还能够对进程进行优先级设置、审计，以及将进程挂起和恢复等操作。

- 容器

  **容器是一个“单进程”模型**。容器的本质就是一个进程

- 镜像

  传统虚拟机的镜像大多是一个磁盘的“快照”，磁盘有多大，镜像就至少有多大。容器镜像只是一个操作系统的所有文件和目录，并不包含内核，最多也就几百兆。

- service及其作用

  Service是由于Kubernetes中一个应用服务会有一个或多个实例（Pod）,每个实例（Pod）的IP地址由网络插件动态随机分配（Pod重启后IP地址会改变），为屏蔽这些后端实例的动态变化和对多实例的负载均衡而引入的资源对象。Service是一组逻辑pod的抽象，为一组pod提供统一入口，用户只需与service打交道，service提供DNS解析名称，负责追踪pod动态变化并更新转发表，通过负载均衡算法最终将流量转发到后端的pod。

- Prometheus工作流程

  1. Prometheus server 定期从配置好的 jobs 或者 exporters 中拉 metrics，或者接收来自 Pushgateway 发过来的 metrics，或者从其他的 Prometheus server 中拉 metrics。
  2. Prometheus server 在本地存储收集到的 metrics，并运行已定义好的 alert.rules，记录新的时间序列或者向 Alertmanager 推送警报。
  3. Alertmanager 根据配置文件，对接收到的警报进行处理，发出告警。
  4. 在图形界面中，可视化采集数据

##实验题

- service配置成功

  <img src="C:\Users\acer\AppData\Roaming\Typora\typora-user-images\image-20200618121247175.png" alt="image-20200618121247175" style="zoom:50%;" />

- 拉取metrics成功

  <img src="C:\Users\acer\AppData\Roaming\Typora\typora-user-images\image-20200618123323609.png" alt="image-20200618123323609" style="zoom:50%;" />
  
- metrics_version版本编写并发布成功并返回pod的请求次数和时延。

  <img src="C:\Users\acer\AppData\Roaming\Typora\typora-user-images\image-20200618132350629.png" alt="image-20200618132350629" style="zoom:50%;" />

  <img src="C:\Users\acer\AppData\Roaming\Typora\typora-user-images\image-20200618132400340.png" alt="image-20200618132400340" style="zoom:50%;" />

- 运行prometheus

  ![image-20200619110603333](C:\Users\acer\AppData\Roaming\Typora\typora-user-images\image-20200619110603333.png)
  
  ![image-20200619110727379](C:\Users\acer\AppData\Roaming\Typora\typora-user-images\image-20200619110727379.png)
  
  

##编程题

- 修改业务逻辑

  如图，在示例代码基础上，新增定义了两个指标数据，一个是Guage类型， 一个是Counter类型。分别代表了CPU温度和磁盘失败次数统计。

  <img src="C:\Users\acer\AppData\Roaming\Typora\typora-user-images\image-20200619033444665.png" alt="image-20200619033444665" style="zoom:50%;" />

  为了方便编写和测试，在metrics.go的Register中直接声明与赋予静态数值和设备名给这两个指标。

  <img src="C:\Users\acer\AppData\Roaming\Typora\typora-user-images\image-20200619033613353.png" alt="image-20200619033613353" style="zoom:50%;" />

- 结果截图

  <img src="C:\Users\acer\AppData\Roaming\Typora\typora-user-images\image-20200619031539654.png" alt="image-20200619031539654" style="zoom:50%;" />

  <img src="C:\Users\acer\AppData\Roaming\Typora\typora-user-images\image-20200619031510608.png" alt="image-20200619031510608" style="zoom:50%;" />

- 在prometheus上查看

  ![image-20200619110901348](C:\Users\acer\AppData\Roaming\Typora\typora-user-images\image-20200619110901348.png)

  ![image-20200619110943811](C:\Users\acer\AppData\Roaming\Typora\typora-user-images\image-20200619110943811.png)

  如上图，两个指标都与设置的一致，且能被prometheus拉取到