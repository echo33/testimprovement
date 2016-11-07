#Docker引领测试革新
随着Docker技术被越来越多的人所认可，其应用的范围也越来越广泛。本文将从测试类型、Devops、自动化测试、测试场景、测试实践等方面介绍Docker对软件测试技术的影响。
##1.传统软件开发流程的痛点
在传统软件开发流程中，开发团队在完成功能代码编写后，会首先进行自测，之后将代码提交到Git仓库中。在每一次迭代转测试时，开发团队会首先构建转测试的二进制文件，之后由测试团队对版本进行验证，验证通过后会将版本提交给运维团队。之后再由运维团队将产品发布件部署到运维服务器中已提供给客户使用。<br>
在这个流程中会有如下痛点：<br>
(1)开发、测试和运维环境不统一。<br>
这导致了有些本该在开发阶段发现的bug可能会遗漏到测试或运维阶段才能发现。有时发布件在开发环境中运行的很稳定，而在运维环境中就挂掉了，从而影响到整个团队的工作效率。<br>
(2)无法准确获取客户的软件环境。<br>
我们往往不能直接复现客户报给我们的bug，不得不去客户现场进行调试，滞后了解决问题的时间。<br>
(3)开发在提交代码前往往未做充分的测试。<br>
开发自验工作取决于开发者的责任心，而没有一种机制来保证自验工作的进行。导致了很多低级的软件缺陷遗漏到测试和运维团队。<br>
(4)开发无法复现测试报出的bug，开发与测试之间相互推诿。<br>
(5)配置测试环境的时间较长，测试自动化成本高。<br>
传统环境往往使用虚拟机，而其消耗资源较高、部署速度慢，导致自动化的效率不高。<br>
备注：对于Docker与虚拟机的区别，请参考???。

##2.当前测试技术面临的挑战
(1)配置一致的测试环境。<br>
(2)快速部署软件。<br>
(3)并行执行测试，在并行的同时还需确保相互的环境不被污染。<br>
(4)成功的复现bug。<br>
(5)创建清洁的测试环境。<br>
(6)正确配置测试工具。同一个工具需要适配到不同的linux发行版中。<br>
(7)快速部署多个测试主机。<br>
(8)快速导入测试数据。<br>
(9)快速清理测试环境。<br>
(10)快速保留、复制、恢复测试环境。<br>

##3.Docker对测试技术的革命性影响
(1)更早的发现单元测试中的软件缺陷。<br>
测试驱动开发是软件工程中的一个创新，即开发者在提交开发代码的同时也要提供对应的测试代码，在代码提交后系统会自动进行一轮自动化测试。通过Docker可以快速部署测试环境，可以有力的支撑自动化测试，从而确保在第一时间发现单元测试中的软件缺陷。<br>
(2)为功能测试和集成测试提供清洁的测试环境。<br>
很多公司由于成本问题，不得不在一个虚拟机中运行不同类型的测试任务。而这些任务在运行时往往会导致环境污染。通过Docker技术的隔离性，可以有效地解决测试环境的污染问题。<br>
(3)让测试团队和客户丢掉冗长的配置文档。<br>
开发转测试时往往带有较长的环境部署文档，而在这些文档中往往存在部署过程跳步的问题，测试团队很难一次准确的将环境部署成功。而现在可以通过Docker镜像将配置环境的过程简化，测试团队省去了查阅文档的过程，只需要基于开发团队提供的Docker镜像就可以轻松的配置测试环境。<br>
(4)可以轻松地复现客户报告的bug。<br>
当客户使用软件发现缺陷时，可以将其所使用的环境打包成镜像提供给开发团队。开发团队通过镜像即可获取与客户一致的软件环境。<br>
(5)通过Dockerfile可以梳理好测试镜像制作的流程。<br>
如果只做流程需要微调时(如将安装gcc3.4改为安装gcc4.3)，可以将Dockerfile中对应的信息进行修改并重新创建新的镜像，不必手动重新配置运行环境。
(6)方便软件提供商将成熟的测试套或测试工具通过镜像共享。<br>
这样可以支持软件在不同linux发行版中成功的运行，软件提供商可以将主要精力放在完善功能上，不必投入很大经历将软件适配到不同的linux发行版中。
(7)利用Docker生态中的工具可以快速创建可伸缩的测试环境，大大减少了测试所消耗的时间。<br>
可以在短时间内快速集中资源来完成一项测试任务，在任务完成后又可以快速的对资源进行回收，有利于提升资源使用效率。
(8)优越的性能指标。-秒级启动、快速挂载、快速清理<br>
通过由于虚拟机的性能，Docker可以提升测试效率。通过“-v”选项可以将主机的目录快速映射到容器中，可以实现测试文件的快速共享。通过“--rm”选项可以在测试完成后第一时间删除容器，以便使用磁盘资源。
(9)轻松的恢复测试环境（包括内存）-CRIU技术 Checkpoint Restore In Userspace<br>
结合CRIU技术，可以实现容器运行状态的保存，这项技术也是容器热迁移的基础。

##4.Devops与Docker
##5.持续集成与持续部署
##6.Docker与自动化测试
什么样的软件测试适合自动化？<br>
是否需要将现有的测试通过docker进行自动化？<br>
原先自动化测试运行在虚拟机中，是否需要将其移植到docker中？<br>
如何将Jenkins与docker相结合使用？<br>

##7.Docker的理想与约束
理想：Build, Ship, and Run Any App, Anywhere.<br>
现实：<br>
由于容器与主机共用内核，如果容器需要使用不同的内核版本就不得不更换主机内核。<br>
不能修改内核参数或者自主定制内核。<br>
对内核版本有依赖性，Docker通常需要3.10或以上版本的内核。<br>
在容器中加载或卸载内核模块会影响到主机和其他容器。<br>
无法像qemu一样模拟嵌入式系统运行环境。<br>

##8.适用于Docker的测试场景
编译系统测试<br>
数据库测试<br>
与内核相关的网络测试<br>
内核测试套LTP<br>
Web应用测试<br>
应用软件安装测试<br>
ARM嵌入式软件模拟测试<br>




##9.Docker测试实践
###9.1.容器化编译系统测试
###9.2.linux外围包测试
| 传统部署特点                                       | Docker部署特点                                       |
| ---------------------------------------- | ---------------------------------------- |
|每套环境独占一台主机|多套环境可以在同一主机上部署 |
|测试串行执行，不易并发|测试并行执行，提高了cpu利用率 |
|环境释放时清理工作依赖于程序员的技能 |环境释放时清理工作由docker接管 |
|无法解决多个外围包的环境污染问题 |容器可快速启动与关闭，每次都是清洁的环境 |
|外围包编译环境不易统一，导致测试结果不统一 |通过镜像保存编译环境，确保环境统一 |
|测试网络包时需要至少两台主机 |测试网络包时只需要在一台主机中启动两个容器 |

##10.通过Docker进行测试加速的原理
##11.测试私有云解决方案

##12.总结

##作者简介
孙远，华为中央软件研究院资深工程师，硕士毕业，9年软件行业经验。目前在华为从事容器Docker项目的测试工作。工作涉及到功能测试、性能测试、压力测试、稳定性测试、安全测试、测试管理、工程能力构建等内容。参与编写了《Docker进阶与实战》的Docker测试章节。先前曾经就职于美国风河系统公司，作为team lead从事风河Linux产品测试工作。活跃于Docker社区和内核测试ltp社区，目前有大量测试用例被开源社区接收。<br>
研究方向：容器技术、Docker、Linux内核、软件测试、自动化测试、测试过程改进<br>
公司邮箱：sunyuan3@huawei.com<br>
个人邮箱：yuan.sun82@gmail.com<br>