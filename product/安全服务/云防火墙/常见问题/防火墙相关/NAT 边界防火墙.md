### NAT 防火墙出去的数据会不会过两遍防火墙?
过两遍，一道管理内网 IP，一道管理公网 IP。

### NAT 网关会被互联网边界防火墙覆盖吗？
会被覆盖。

### NAT 防火墙新增模式和接入模式有什么区别？
- 新增模式：若当前地域没有 NAT 网关，新增模式可以通过 NAT 边界防火墙内置的 NAT 功能，实现指定实例通过防火墙访问互联网。
- 接入模式：若当前地域已有NAT 网关，或者希望公网对外的出口 IP 保持不变，接入模式可以将 NAT 边界防火墙平滑接入到 NAT 网关与  CVM 实例之间。

### 使用 NAT 边界防火墙可以替代原来的 NAT 网关么？	
NAT 防火墙可以替代原来的 NAT 网关。

### NAT 边界防火墙可以只对某个子网启用么？
一个防火墙开关对应一个子网，可以选择同时开启当前子网关联的路由表的全部子网的防火墙，也可以只针对当前子网开启防火墙。

### NAT边界开关上绑定 EIP，网络是否会闪断？
绑定不会造成闪断。

### NAT边界开关开启或关闭某个 VPC 时该网络是否会闪断？
- 开启：若用户仅选择开启某个子网，系统会自动为当前子网创建新的路由表，复制现有的全部路由策略，在新路由表中增加一条下一跳指向 NAT 边界防火墙的路由策略，并关闭原访问公网的路由策略，因此该子网的互联网流量，将会经过 NAT 边界防火墙。

- 关闭：若用户仅选择关闭某个子网，系统会自动为当前子网创建新的路由表，复制现有的全部路由策略，并关闭下一跳指向 NAT 边界防火墙的路由策略，该子网将会断开与互联网的连接。

### NAT 边界开关配置端口转发(DNAT)是否支持配置连续端口？
端口转发不支持在同一规则下同时配置多个端口，每个 DNAT 端口需要使用一条规则。

### NAT边界可以配置 SNAT么？要如何配置？	
1. 登录 [云防火墙控制台](https://console.cloud.tencent.com/cfw/switch)，单击选择**防火墙开关** > **NAT 边界开关**，进入NAT 边界开关页面。
2. 在NAT 边界开关页面左侧操作栏中，单击**实例配置** > **出口绑定** > **新建规则**。
3. 选择相应的子网或私有网络使用的外部 IP后单击**确定** 即可。

### 如何确认子网都开了防火墙？
1. 登录 [云防火墙控制台](https://console.cloud.tencent.com/cfw/switch)，单击选择**防火墙开关** > **NAT 边界开关**，进入NAT 边界开关页面。
2. 在 NAT 边界开关菜单，单击**防火墙开关**页查看所有已开启和未开启的子网信息。

### NAT 边界开关里实例配置-域名解析开关开了后，需要重启服务器么？不操作会生效么？	
不需要重启服务器，重启服务器仅是让配置生效快些，这个跟在私有网络控制台上配置 dns 生效时间是一样的。刷新网络配置可用以下命令：
- Linux：可执行 dhclient
- windows: ipconfig /flushdns

### NAT 边界开关自动同步资产的周期是多长？	
10分钟。

### NAT 防火墙的子网开关无法开启是什么原因？	
可能资产规模在后台轮询间隔内发生变化，但尚未被同步导致，您可登录 [云防火墙控制台](https://console.cloud.tencent.com/cfw/switch)，单击**防火墙开关**>**互联网边界开关**>**同步资产**，主动调用后台接口重新读取并同步子网的资产信息后，再尝试开启。

### NAT 防火墙如何更换 VPC ？	
在 NAT 防火墙右上角有设置按钮，点击之后选择重新选择接入 VPC。

### NAT 防火墙可以绑定多少 VPC ？
暂无限制。

### NAT 边界防火墙创建失败？
若您 VPC 下有使用专线和对等连接，您的 VPC 需要预留至少一个24/子网供给防火墙接入使用，防火墙才能创建成功。

### 开启NAT 防火墙后，分配的弹性 IP 为什么不支持访问 ？
新分配的 eip 需要绑定才可以被访问。
