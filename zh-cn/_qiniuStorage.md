# 七牛云存储(引用EInfrastructure.Core.QiNiu.Storage包后即可使用)

&emsp;&emsp;七牛云存储，是目前常用的云存储服务商的其中一种，此类库目前提供了根据文件流、字节数组上传、判断文件是否存在以及批量复制、删除文件、批量移动文件抓取资源等方法，目前文档版本2.3.6

[![NuGet](https://img.shields.io/nuget/v/EInfrastructure.Core.QiNiu.Storage.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.QiNiu.Storage)
[![NuGet Download](https://img.shields.io/nuget/dt/EInfrastructure.Core.QiNiu.Storage.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.QiNiu.Storage)


## 通过IOC注入使用配置

在NetCore下使用

### 一、引入包

#### 1. 如果与Mysql数据库结合使用，则引入EInfrastructure.Core.AutoFac.MySql.AspNetCore

    //首先在项目的Startup中添加阿里大于的使用以及短信参数配置
    public IServiceProvider ConfigureServices(IServiceCollection services)
    {
        services.AddQiNiuStorage(()=>{
            var config = new QiNiuStorageConfig("accessKey", "secretKey", ZoneEnum.ZoneCnSouth, "访问图片域名", "空间名");
            return config;//七牛配置信息，默认上传后不回调
        });
        return EInfrastructure.Core.AutoFac.MySql.AspNetCore.AutofacAutoRegister.Use(services, (builder) => { });
    }

#### 2. 如果不使用数据库结合使用，则只引入EInfrastructure.Core.AutoFac.AspNetCore
    
    public IServiceProvider ConfigureServices(IServiceCollection services)
    {
        services.AddQiNiuStorage(()=>{
            var config = new QiNiuStorageConfig("accessKey", "secretKey", ZoneEnum.ZoneCnSouth(默认空间域), "默认空间所属域名", "默认空间名");
            return config;//七牛配置信息，默认上传后不回调
        });
        return EInfrastructure.Core.AutoFac.AspNetCore.AutofacAutoRegister.Use(services, (builder) => { });
    }

### 二、使用七牛操作文件信息

#### 通过上方的配置可以在控制器中使用IStorageProvider、IPictureProvider、IBucketProvider三个接口的方法

1. IStorageProvider 文件存储管理
1. IPictureProvider 图片存储管理
1. IBucketProvider 空间管理

#### 其中IPictureProvider对外提供了以下方法：
        
1. 根据图片base64上传 Upload （暂不提供图片处理，仅支持普通的图片上传）

#### 其中IStorageProvider对外提供了以下方法：

1. 根据文件流上传 UploadStream
1. 根据文件字节数组上传  UploadByteArray
1. 根据文件Token上传 UploadByToken
1. 得到上传文件凭证 GetUploadCredentials
1. 得到管理凭证 GetManageToken
1. 检查文件是否存在 Exist
1. 获取文件信息 Get
1. 获取文件信息集合（超过1000个时会自动分批获取） GetList
1. 根据文件key删除 Remove
1. 根据文件key集合删除（超过1000个时会自动分批删除） RemoveRange
1. 复制文件（两个文件需要在同一账号下） CopyTo
1. 复制文件集合（两个文件需要在同一账号下，超过1000个时会自动分批复制） CopyRangeTo
1. 移动文件（两个文件需要在同一账号下） Move
1. 批量移动文件（两个文件需要在同一账号下，超过1000个时会自动分批移动） MoveRange
1. 得到文件的访问地址 GetVisitUrl
1. 下载文件到本地 Download
1. 下载文件流 DownloadStream
1. 设置生存时间（超时会自动删除） SetExpire
2. 批量设置生存时间（超时会自动删除） SetExpireRange
1. 修改文件MimeType ChangeMime
1. 批量更改文件mime ChangeMimeRange
1. 修改文件存储类型 ChangeType
1. 批量更改文件类型 ChangeTypeRange
1. 设置文件访问权限 SetPermiss（不支持）
1. 获取文件的访问权限（不支持）
1. 获取指定前缀的文件列表 ListFiles
1. 抓取资源到空间  FetchFile

#### 其中IBucketProvider对外提供以下方法

1. 获取空间列表 GetBucketList
1. 创建空间 Create
1. 设置空间的镜像源 SetSource
1. 获取空间域名信息 GetHost
1. 删除空间 Delete
1. 判断空间是否存在 Exist
1. 设置空间访问权限 SetPermiss
1. 获取空间的访问权限 GetPermiss（不支持）
1. 设置防盗链 SetReferer（不支持）
1. 得到防盗链配置 GetReferer（不支持）
1. 清空防盗链规则 ClearReferer（不支持）
1. 设置空间访问权限 SetTag
1. 得到空间标签 GetTags
1. 清除空间标签 ClearTag

#### 具体的方法用法可查看源码使用，其中定义的比较简单，在调用时也有相对应的注释，如果确实有不容易理解的会在文档中标注。

  
&emsp;&emsp;<a href ="https://github.com/zhenlei520/System.Extension.Core.Demo/tree/master/Storage/System.Extension.Core.AspNetCore.QiNiuStorage" target="_blank">点击查看完整示例</a> 

&emsp;&emsp;以上代码支持最新预览版，且自2.0.1-beta-027后，云存储默认配置中只有默认空间，默认空间域以及默认空间对应的区域，如果希望某个方法不对默认配置中的空间操作，请配置参数中的策略属性

&emsp;&emsp;七牛存储是通过单例模式进行诸如，目前如果在一个项目中如果只使用一个账号的情况下可通过ioc进行注入，但如果你的场景是需要用到多个七牛账号进行操作的话，建议您直接通过初始化BucketProvider、StorageProvider、PictureProvider类进行操作，相比单例模式，仅仅只是默认配置文件的差别，之前有想过再分一个包来处理，但仔细想过之后发现效果与直接初始化BucketProvider、StorageProvider、PictureProvider类类似，所以就没继续进行分离，如果您有这方面的场景需要，可通过此方法进行，如果您的场景下除了七牛云存储外可能还有阿里云oss、腾讯云oss的可能性，后期包也会提供，您当前可以通过再分拆阿里云、七牛云、腾讯云三个类库后引用不同的EInfrastructure.Core的存储包，为您节省了参数响应以及传参不统一的问题，之后上线阿里云以及腾讯云oss后为您节省更多的开发时间，如果您有其他的oss存储空间的话，也欢迎您与我们的包进行集成，让其集成变得更简单