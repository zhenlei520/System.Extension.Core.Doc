# 作用与简单介绍


&emsp;&emsp;EInfrastructure.Core.Configuration &nbsp;[![NuGet](https://img.shields.io/nuget/v/EInfrastructure.Core.Configuration.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.Configuration)
[![NuGet Download](https://img.shields.io/nuget/dt/EInfrastructure.Core.Configuration.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.Configuration)

    作为基础配置类库存在，其中存在我们常用的枚举类，例如：性别、星座、语言、民族等以及自定义异常类、
    IOC规范接口类，例如：日志接口、存储接口、短信接口、缓存接口、词库接口、Json序列化接口以及Xml序列化接口等，
    在这么多类库中，是处于最底层的存在

&emsp;&emsp;[EInfrastructure.Core.Config.Entities](/zh-cn/_configEntities.md)&nbsp;[![NuGet](https://img.shields.io/nuget/v/EInfrastructure.Core.Config.Entities.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.Config.Entities)
[![NuGet Download](https://img.shields.io/nuget/dt/EInfrastructure.Core.Config.Entities.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.Config.Entities) 

    作为实体模型基础配置类库存在，其中存在预先定义好的实体的父类
    对Lambda的扩展等等以及后面操作数据最重要的两个仓储类，IRepository（增删改）、IQuery（只读）、IExecute（Sql执行）

&emsp;&emsp;[EInfrastructure.Core.Http](/zh-cn/_http.md)&nbsp;[![NuGet](https://img.shields.io/nuget/v/EInfrastructure.Core.Http.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.Http)
[![NuGet Download](https://img.shields.io/nuget/dt/EInfrastructure.Core.Http.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.Http)

    基于RestSharp 106.3进行了一次封装，对简单的post以及get使用更方便。

&emsp;&emsp;[EInfrastructure.Core.Tools](/zh-cn/_tools.md)&nbsp;[![NuGet](https://img.shields.io/nuget/v/EInfrastructure.Core.Tools.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.Tools)
[![NuGet Download](https://img.shields.io/nuget/dt/EInfrastructure.Core.Tools.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.Tools)

    一个不依赖其他类库的工具包，其中封装了很多我们常用的方法。
    例如：类型转换（转Int，转Float、转Bool等）、根据生日计算星座、根据生日计算生肖、Md5、Sha、Aes加密、邮件发送、自定义属性、时间帮助类等等

&emsp;&emsp;[EInfrastructure.Core](/zh-cn/_common.md)&nbsp;[![NuGet](https://img.shields.io/nuget/v/EInfrastructure.Core.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core)
[![NuGet Download](https://img.shields.io/nuget/dt/EInfrastructure.Core.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core)

    基于EInfrastructure.Core.Tools之上对方法进行了更深一层的封装，其引用EInfrastructure.Core.Configuration、EInfrastructure.Core.Tools等，在IOC下使用更方便

