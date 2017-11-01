## Canopy: 端到端性能跟踪分析系统

### 1.研究情境

用户执行各种各样的操作，例如获取Facebook.com一个页面，通过异构客户端（包括Web浏览器和移动应用程序）、网络和分布式后端服务的复杂执行，从而访问

Facebook，获取不同级别的信息和对应用程序的控制，完成页面的加载。

### 2.CAP

为解决其中的性能问题，Facebook开发了许多跟踪系统，有单系统的和跨部分系统的，没有跨全部系统的，导致以下问题：

1、进行跨系统性能分析需要了解多个跟踪工具以及何时使用和切换

2、只能关注于特定域，不能处理所有问题

3、分析类型僵化

### 3.概述

将关注点放到请求的端到端的执行路径上，在请求的端到端执行路径中记录因果关联的性能数据

1、端到端执行路径的性能数据

2、结构化、因果关联的执行跟踪，扩展X-Trace、Dapper，利用传播标识符获取跨组件关联信息

输入：开发人员可以从轨迹的采样、提取和可视化进行深入定制，进行实时查询

输出：聚合了数十亿个请求的性能数据集，可视化便于分析

### 4.优点
1、用于跟踪的解耦设计将仪器与跟踪模型分离开，实现独立演进和不同执行模型的组合。

2、完整的管道，将轨迹转换为自定义的一组提取的特征，以实现快速分析。

3、一组可定制的跟踪组件，用于为不同的用例提供相同数据的多个视图。

### 5.实现
Canopy通过一个完整的管道来解决这些挑战，用于从堆栈中的系统生成的跟踪中提取性能数据，包括浏览器，移动应用程序和后端服务。 Canopy强调了管道每一步的定
制，并且提供了组件之间关注的新颖分离，以允许它们的单独进化。 在开发阶段，Facebook工程师可以使用针对不同执行模式量身定制的一系列API来调整系统。 在运
行时，Canopy将生成的性能数据映射到灵活的基于事件的表示。 Canopy的后端管道在近距离接收事件; 重构分析查询更加便利的高级跟踪模型; 从痕迹中提取用户指定
的特征; 并将结果输出到用于自定义聚合可视化的数据集

首先，端到端的性能数据是异构的，具有多个执行模型，并且在可用于分析的数据的粒度和质量方面有广泛的变化。

快速解决性能问题需要能够有效地切片，分组，过滤，聚合和总结基于任意特征的跟踪的工具。

跟踪包含任何工程师识别问题所需的所有数据。

当一个组件出现性能问题时，其症状可能会在堆栈的不同部分显现; 因此，诊断性能问题需要全局视图，最终用户在Facebook.com上加载页面时，会由许多不同产品组开
发的页面组合。 Facebook的核心框架代码组合了页面，并在网络服务器和客户端浏览器中运行它们。 