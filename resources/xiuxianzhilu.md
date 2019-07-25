# 第一阶段 炼气期（2-4 周，每周 3-5 小时）

目标

Kubernetes 的背景
安装 Kubernetes 环境
Kubernetes 基本概念和使用方法

路径

学习任何系统的之前，了解其出现的背景和意义都是必不可少的：为什么会出现 Kubernetes？它解决了什么问题？有没有其他类似的系统？关于这些问题的答案，这里推荐阅读才云科技 CEO 张鑫在 2017 年文章《从风口浪尖到十字路口，写在 Kubernetes 两周年之际》。

之后，在了解 Kubernetes 系统本质之前，我们需要对 Kubernetes 有一个较为"感性"的认识，打消对 Kubernetes 的畏难情绪。我们可以先通过 minikube 或 kind 部署一个本地环境，然后开始部署一个"真实"的应用（minikube 安装需要使用科学上网）。如果想一开始就挑战更高难度的安装方式（不推荐），可以使用 kubeadm 或者手动部署所有组件。关于安装，可以参考文档 lab1-installation。

在安装好环境之后，我们就可以开始动手实践最基本的 Kubernetes 概念了。在第一阶段，我们需要学会熟练使用以下常用资源并熟记它们的概念：Pod、Node、Label、Event、Service、Configmap & Secret、Deployment、Namespace。

心法

请反复加深对上面资源的操作熟练度。如果你是第一次接触 Kubernetes，或者仅了解过一点 Kubernetes 的知识，那么基（ken）本（ding）是不明白 Kubernetes 底层到底发生了什么。请不要心急，姑且把它当成一个黑盒工具即可 。

你可能会在网上看到更多的概念，如 PVC、Ingress、Priority 等。炼气阶段，请不要尝试学习过多的资源类型。Kubernetes 有非常多的概念和类似的资源，我们这里熟悉最核心的概念即可，否则易走火入魔 ，切记。当我们打通“任督二脉”之时，所有的新概念都不过尔尔。

02
# 第二阶段 筑基期（4-6 周，每周 8-10 小时）

目标

Kubernetes 的基本架构
Kubernetes 容器调度的基本流程

路径

短暂接触 Kubernetes 概念之后，我们需要知其然并且知其所以然，因此在第二阶段我们可以从以下内容开始学习 Kubernetes 基本架构：

Master & Node
Master 组件
Node 组件
核心 Addons & Plugins

首先，我们可以阅读书籍或网上博客，推荐阅读（具体链接详见 GitHub）：

官方文档：Kubernetes Components
feisky 的博客：Kubernetes 指南之核心原理
kubectl run 的背后流程（难）：What happens when I type kubectl run?
kubectl run 的背后流程中文版：kubectl 创建 Pod 背后到底发生了什么？
接下来，推荐从 0 开始部署一个 Kubernetes 集群（不使用任何工具）来加深对各个组件的理解：解决部署中出现的各种问题，查看组件启动日志等等。如果时间有限，也可以尝试使用 kubeadm 等工具来部署集群。

目前 Kubernetes 集群部署自动化已经做得比较完善，但出于学习目的，我们再次“墙裂”推荐手动安装。关于手动安装集群，可以参考文档 lab3-manual-installtion。

在本阶段修炼结束后，我们至少应该对以下问题了如指掌：Kubernetes 组件是如何交互来启动容器，并对外提供服务的？

心法

请不要死记硬背 Kubernetes 架构，要开动大脑去理解其背后设计的原因。

筑基期是比较困难的一个阶段，如果感觉一头雾水，请不要气馁，你不是一个人。当你感觉进入了瓶颈时，可以尝试寻找身边的战友，总结一些你的问题并寻求答案。

03
# 第三阶段 金丹期（2-4 周，每周 3-5 小时）

目标

Kubernetes API 结构
熟悉 Kubernetes 各个子系统
熟悉 Kubernetes 排错相关内容

路径

当我们可以熟练使用 Kubernetes 的基本资源，并对 Kubernetes 的基本架构有了充足了认识后，接下来，我们就需要对 Kubernetes 的 API 结构和子系统形成比较全面的认识。同时，我们也要开始更加系统地了解排查问题相关的内容。

API 系统是 Kubernetes 最引以为傲的设计，掌握 API 的关键是了解：

Kubernetes 的 API 是如何控制版本的
Kubernetes 的 API 是如何分组的
Kubernetes 对象的表示方法与设计理念
Kubernetes API 的访问控制

我们可以通过浏览 Kubernetes API 代码仓库来了解 Kubernetes API 组（Group）的信息。所有的资源定义代码都遵循 <group>/<version>/types.go 的规范，例如上述 Deployment 资源是定义在 apps group 中。我们可以在 apps/v1/types.go 中查找到关于 Deployment 的定义。

接下来，我们可以通过浏览 Kubernetes/Community 代码仓库来了解各个兴趣小组（SIG），"SIG" 是 Special Interest Group 的简称。Kubernetes 的演进都是通过 SIG 来推动的，因此了解 SIG 的分工对我们理解 Kubernetes 非常重要。一般来讲，一个 SIG 对应着一个 Kubernetes 子系统，例如，sig-apps 负责决定是否引入新的 API，或者现有 API 是否需要升级等等。我们通过查看 Community 中带有 "sig-" 前缀的目录来了解 SIG 的工作内容、会议纪要等等。

作为一个承上启下的阶段，我们需要总结一些 Kubernetes 排错的能力，推荐阅读：

官方文档：Kubernetes Troubleshooting
feisky 的博客：Kubernetes 集群排错指南

心法

本阶段的重点是"耳听六路、眼观八方 "。前两个阶段接触到了很多 Kubernetes 的细节，本阶段需要对 Kubernetes 的全貌有个更加清晰的认识。很多内容可能看不太懂，但请在你的心中埋下一颗种子。

04
# 第四阶段 元婴期（4-6 周，每周 8-10 小时）

目标

加深对各个资源的理解
学习更多 Kubernetes 概念和知识

路径

不出意外，现在我们对 Kubernetes 基本资源应该已经很熟练了，对 Kubernetes 内部组件和它们的交互也比较清晰，对 Kubernetes 的 API 全貌和组织结构也有一定了解。如果仍有不清楚的地方，请重新回顾你的学习过程。

本阶段，我们将围绕几个关键方向来学习 Kubernetes，加深对其各个技术点的认识（这里只列出本阶段需要学习的核心能力，其他功能请量力而学）。

计算

Pod Lifecycle & Healthcheck & RestartPolicy
Pod Init-Container
Horizontal Pod Autoscaler (HPA)
更多控制器：Job、CronJob、Daemonset、StatefulSet、ReplicaSet

网络

Service 实现，主要了解 iptables 的实现（可选：ipvs 模式）
Ingress 原理和常用的 nginx ingress 操作
DNS 服务的原理，以及 CoreDNS 方案
存储

Volume 以及底层存储类型
PV/PVC、StorageClass

安全

AuthN, AuthZ & Admission Control
NetworkPolicy
ServiceAccount
Pod/Container SecurityContext
Pod Security Policy (PSP)

调度

Pod/Node Affinity & Anti-affinity
Taint & Toleration
Priority & Preemption
Pod Disruption Budget

本阶段我们会接触到更多的资源，包括：HPA、Job、CronJob、DaemonSet、StatefulSet、Ingress、Volume、PV/PVC、StorageClass、NetworkPolicy、PSP。我们也将更加深入了解已学资源的使用，例如 Init-Container、SecurityContext、Affinity 等。

这些能力最终都会体现在各个资源的 API 上，例如 Affinity 是 Pod API 结构的一个字段，Scheduler 通过解析这个字段来进行合理的调度。未来如果有更多的能力，我们都可以通过解读不同资源的 API 字段来一探究竟。

心法

本阶段难度指数高，请合理调整你的心境。“渡劫”成功后，你对 Kubernetes 的掌握将会上升到一个新的台（tian）阶（keng）。

学习相关功能时，可以回顾其所在 SIG，看看能不能发现有用的资源。

05
# 第五阶段 化神期（3-5 周，每周 6-8 小时）

目标

学习更多 Kubernetes 集群层面的功能
更加深入学习 Kubernetes 架构和组件能力

路径

当我们了解了 Kubernetes API 的设计理念，学习到了足够多的 API 资源及其使用方法之后，让我们再回顾一下 Kubernetes Master & Node 架构，以及它们运行的组件。事实上，Kubernetes 的每个组件都有很强的可配置性和能力，我们可以围绕 Kubernetes 的每个组件，来学习 Kubernetes 较为“隐晦”的功能。

推荐通过 Kubernetes Command Line Reference 来了解这些组件的配置：

kube-api-server
kube-scheduler
kube-controller-manager
kube-proxy
kubelet
kubectl

同时，Kubernetes 提供了 FeatureGate 来控制不同的特性开关，我们可以通过 FeatureGate 来了解 Kubernetes 的新特性。此外，为了方便开发者和配置管理，Kubernetes 把所有配置都挪到了相对应的 GitHub 代码仓库中，即：

https://github.com/kubernetes/kube-scheduler
https://github.com/kubernetes/kube-controller-manager
https://github.com/kubernetes/kube-proxy
https://github.com/kubernetes/kubelet
https://github.com/kubernetes/kubectl

当然，直接裸看配置有点硬核。为方便入手，下面我们简单总结部分功能（笼统地分为 Master 和 Node）：

Master

Dynamic Admission Control
Advanced Auditing
Etcd Configuration
提供各种与 Etcd 相关的配置，例如 Kubernetes event TTL
对应 API Server 带有 --etcd- 前缀的参数
All Admission Controllers
Garbage Collection
Concurrent Sync Limiting
All Controllers

其他值得注意的参数包括：

API-Server --max-requests-inflight, --min-request-timeout
API-Server --watch-cache, --watch-cache-sizes
Controller-Manager --node-eviction-rate
Controller-Manager --pod-eviction-timeout
Controller-Manager --terminated-pod-gc-threshold
Controller-Manager --pv-recycler-minimum-timeout-*

Node

Kubelet Eviction
Image GC
Resource Reserve
CPU Manager
Storage Limit

其他值得注意的参数包括：

Kubelet & Kubeproxy --hostname-override
Kubelet --cgroups-per-qos
Kubelet --fail-swap-on
Kubelet --host-*
Kubelet --max-pods, --pods-per-core
Kubelet --resolv-conf
Kubeproxy --nodeport-addresses

心法

通过组件配置学习 Kubernetes 功能是我们需要具备的一个常规能力，或许比较枯燥，但对我们的修炼大有裨益。

如果你对 Kubernetes “无穷无尽”的功能感到有点迷茫，这是一个很正常的现象。除非是深度参与 Kubernetes 的开发，否则一定会有很多遗漏的地方。我们只要保持两个基本点不动摇：一是懂 Kubernetes 架构和最核心的能力；二是懂得怎么快速定位我们需要的能力。

06
# 第六阶段 练虚期（4-6 周，每周 8-10 小时）

目标

对 Kubernetes 的扩展机制了如指掌
可以编写 Kubernetes 控制器，能够基于扩展机制灵活地二次开发

路径

本阶段我们可以开始了解 Kubernetes 各种扩展机制。如果说 Kubernetes 的 API 和架构设计是其重要的基石，那么扩展机制使得 Kubernetes 在各个生态领域开花结果。

下面我们将尝试列举出所有的扩展方式，每一种扩展都有其优势和局限性，请自行思考。注意，这里提到的扩展机制指的是架构上的扩展，而非功能层面的扩展。

API 资源扩展能力

Annotation：保存少量非结构化第三方数据
Finalizer：资源删除时，用户调用外部系统的钩子
CustomResourceDefinition：自定义 Kubernetes API
API Aggregation：多个 API Server 聚合，适用于较大量的 API 定制

学习 API 资源扩展的一个重要方式是创建一个扩展资源，或者编写一个自己的控制器。强烈推荐自行编写一个控制器，这里列出几个常见的工具：

kubebuilder：来自 Kubernetes 官方的 API 扩展项目
sample-controller：来自 Kubernetes 官方的一个样例
operator-sdk：来自红帽的一个 operator 库
shell-operator：适合运维开发使用的 shell operator 库
meta-controller：来自 Google 的一个更加"傻瓜"式编写控制器的库

API 访问扩展能力

认证 Webhook：用户认证时，调用外部服务，仅支持静态配置
鉴权 Webhook：用户鉴权时，调用外部服务，仅支持静态配置
动态访问控制 Webhook：请求访问控制时，调用外部服务，支持动态增加外部服务

Kubernetes API 访问扩展主要是通过 Webhook 来实现。注意只有访问控制支持动态增加外部服务，认证鉴权的外部服务在启动 API Server 的时候就注册完毕，无法在后续增加，主要原因是动态增加外部认证鉴权服务，带来的安全风险过大。

调度器扩展能力

扩展接口（Scheduler Extender）：类似 Webhook，调用外部服务进行调度决策
多调度器：支持在 Kubernetes 运行多个调度器调度不同作业

针对简单场景，我们可以直接使用 Scheduler Extender，例如按 GPU 型号调度。复杂调度场景可以使用多调度器，例如基于流图的调度器 poseidon。一般而言，使用 Extender 即可满足大多数场景。

网络扩展能力

网络插件 CNI：使用 CNI 插件，可以选择任何我们需要的网络方案
自定义 Ingress 控制器：Ingress 定义了一套 API 接口，我们可以选择任意实现
自定义 NetworkPolicy 控制器：同上，可选实现包括 Calico、Cilium 等
自定义 DNS 控制器：Kubernetes 定义了一套 DNS 规范，我们可以选择任意实现
网络插件 CNI 是容器网络标准，Kubernetes 提供了良好的支持，常用插件包括 flannel、Calico 等等。对于 Ingress、NetworkPolicy、DNS，相信到目前为止大家应该可以理解，其本质上是 Kubernetes 定义的一套 API，底层实现可插拔，用户可以有自己的选择。

存储扩展能力

FlexVolume：Kubernetes 提供的一种动态对接存储方案，支持用户自定义存储后端
存储插件 CSI：使用 CSI 插件，可以选择任何我们需要的存储方案

FlexVolume 是 Kubernetes 自带的对接外部存储的方案，用户编写少量的代码即可加入自定义存储后端，适用于简单场景。存储插件 CSI 是容器网络标准，Kubernetes 提供了良好的支持，同时为方便第三方实现，还提供了一整套 SDK 解决方案。所有底层存储相关的能力都与 CSI 密切相关。

运行时扩展能力

运行时接口 CRI：使用 CRI 插件，可以选择任何我们需要的运行时方案

运行时接口 CRI 是 Kubernetes 为解决支持多种运行时而提供的方案。任何运行时只需实现 CRI 相关的接口，即可接入 Kubernetes 中，包括 Docker、Containerd、gVisor、Kata 等。

特殊硬件或资源扩展能力

扩展资源 Extended Resource：通过 Kubernetes 原生 API 方式支持添加自定义资源
设备插件 Device Plugin：使用 Device Plugin 插件，可以对接任何我们需要的硬件

对于简单场景，例如静态汇报资源数量，可以直接使用 Extended Resource 扩展 Kubernetes 所支持的硬件。Device Plugin 的核心是自动接入各种特殊硬件如 Nvidia、Infiniband、FPGA 等。在资源汇报层面 Device Plugin 目前也使用了 Extended Resource 的能力，但由于 Extended Resource 的局限性，Device Plugin 未来也可以与其他 API 对接。目前使用最多的 Device Plugin 主要是 Nvidia 的 GPU device plugin。

监控扩展能力

自定义监控：支持使用自定义监控组件如 Prometheus 提供监控指标
自定义监控包括 Custom Metrics 和 External Metrics，例如 Prometheus adaptor。

云供应商扩展能力

云控制器 Cloud Controller Manager：支持可插拔云服务提供商

云扩展能力的目标是使各个云供应商可以在不改变 Kubernetes 源码的情况下，接入其服务。每个云供应商都有独立的项目。

命令行插件

Kubectl Plugin：kubectl plugin 支持扩展 kubectl 子命令，与 API 扩展能力结合可以提供近乎原生的使用方法。

心法

推荐实现一个端到端的 Kubernetes 控制器，可以对整个 Kubernetes 的二次开发有更加深入的了解。此外，针对所有的扩展能力，建议先建立一个全面的认识，再根据需要深入某一项能力。

除了通过用户手册来学习上面的技术，我们也可多参考 Kubernetes 的花式设计文档，主要是 Design Proposals、KEPs。

07
# 第七阶段 大乘期（终身学习）

目标

了解 Kubernetes 生态项目
跟踪 Kubernetes 社区发展
跟踪 CNCF 社区发展

路径

目前为止，我们学习了很多 Kubernetes 的概念，但也只是其最重要的部分。在本阶段，我们需要专注以下几个问题：

如何跟进 Kubernetes 的新功能，以及现有功能的更多细节？
如何了解 Kubernetes 整个生态环境的发展？

首先，让我们一起来学习几个重要的项目。围绕 Kubernetes 的生态环境建设是其成为容器标准的关键。

Helm：作为 Kubernetes 生态里的 brew、dnf、dpkg，Helm 为 Kubernetes 提供了包管理能力，方便用户快速部署安装各种服务
Harbor：Harbor 与 Kubernetes 无直接关系，但作为云原生环境下最常用的镜像仓库解决方案，了解 Harbor 十分重要
Prometheus：Prometheus 是云原生环境下最重要的监控组件
Istio：Istio 是服务网格的关键项目，但较为复杂，可以尝试简单了解

以上只是个别重要项目，Kubernetes 的项目生态非常丰富，因此大乘期的你，需要开始学会持续跟踪 Kubernetes 及其生态的发展，甚至推动其发展、接下来，我们列举一些靠谱资源：

GitHub 仓库

Kubernetes Enhancement：关注新特性的讨论
Kubernetes Community：关注社区组织情况
CNCF TOC：关注 CNCF 进展，各种新项目讨论等
Awesome Kubernetes：Kubernetes 项目之学不动系列

关注 GitHub 仓库可以让你了解最一手的进展，但是信息量一般较大，讨论很多难度也比较大。但对于大乘期的你来讲，这些应该不是问题 。另外，GitHub 仓库还包含很多 Kubernetes 系统内部设计，例如调度器的优化方案、资源垃圾回收方案等，值得了解和学习。

Twitter 账号

下面推荐几个 Kubernetes 项目核心人员的 Twitter，感兴趣的话题可以去交流。

Tim Hockin
Clayton Coleman
Daniel Smith
Brian Grant
Vishnu Kannan
Saad Ali
Kelsey Hightower
Joe Beda
Brendan Burns
Michelle Noorali
除此之外，Twitter 上还有不少项目和其他 Weekly 性质的 Twitter，推荐几个账号关注：

Kube Weekly
Kube List
K8sMeetup 中国社区（公众号 kuberneteschina2）

Twitter 会根据你的喜好推荐其他相关内容，接下来就自由发挥了。

心法

请坚持学习！送上一句黑鸡汤：

"The last thing you want is to look back on your life and wonder... if only."