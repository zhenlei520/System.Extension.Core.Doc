# 七牛云存储(引用EInfrastructure.Core.QiNiu.Storage包后即可使用)

&emsp;&emsp;七牛云存储，是目前常用的云存储服务商的其中一种，此类库目前提供了根据文件流、字节数组上传、判断文件是否存在以及批量复制、删除文件、批量移动文件抓取资源等方法

[![NuGet](https://img.shields.io/nuget/v/EInfrastructure.Core.QiNiu.Storage.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.QiNiu.Storage)
[![NuGet Download](https://img.shields.io/nuget/dt/EInfrastructure.Core.QiNiu.Storage.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.QiNiu.Storage)


## 通过IOC注入使用配置

在NetCore下使用


    方法一（推荐）：
    1. 如果与Mysql数据库结合使用，则引入EInfrastructure.Core.AutoFac.MySql.AspNetCore

    //首先在项目的Startup中添加阿里大于的使用以及短信参数配置
    public IServiceProvider ConfigureServices(IServiceCollection services)
    {
        services.AddQiNiuStorage(()=>{
            return new QiNiuStorageConfig(){
                AccessKey="公钥",
                SecretKey="秘钥",
                Zones=ZoneEnum.ZoneCnSouth,//存储空间存储区域
                Host:'主机域',
                Bucket:'空间名',
                PersistentPipeline:'传输队列',//用于加快处理文件
                PersistentNotifyUrl："持久化结果通知",
                CallbackUrl="上传成功后，七牛云向业务服务器发送 POST 请求的 URL",
                CallbackBody="回调内容",//（可不填）
                CallbackBodyType="EInfrastructure.Core.Configuration.Ioc.Plugs.Storage.Enumerations.CallbackBodyType.Json.Id",//（回调内容类型，默认json，可不填）
                CallbackAuthHost="鉴权回调域，",
            };
        });
        new EInfrastructure.Core.AutoFac.MySql.AspNetCore.AutofacAutoRegister().Build(
                services,
                (builder) => { });
    }