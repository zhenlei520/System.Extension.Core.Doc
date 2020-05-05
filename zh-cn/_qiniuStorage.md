# 七牛云存储(引用EInfrastructure.Core.QiNiu.Storage包后即可使用)

&emsp;&emsp;七牛云存储，是目前常用的云存储服务商的其中一种，此类库目前提供了根据文件流、字节数组上传、判断文件是否存在以及批量复制、删除文件、批量移动文件抓取资源等方法

[![NuGet](https://img.shields.io/nuget/v/EInfrastructure.Core.QiNiu.Storage.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.QiNiu.Storage)
[![NuGet Download](https://img.shields.io/nuget/dt/EInfrastructure.Core.QiNiu.Storage.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.QiNiu.Storage)


## 通过IOC注入使用配置

在NetCore下使用

一、引入包

    1. 如果与Mysql数据库结合使用，则引入EInfrastructure.Core.AutoFac.MySql.AspNetCore

    //首先在项目的Startup中添加阿里大于的使用以及短信参数配置
    public IServiceProvider ConfigureServices(IServiceCollection services)
    {
        services.AddQiNiuStorage(()=>{
            var config = new QiNiuStorageConfig("accessKey", "secretKey", ZoneEnum.ZoneCnSouth, "访问图片域名", "空间名");
            return config;//七牛配置信息，默认上传后不回调
        });
        return EInfrastructure.Core.AutoFac.MySql.AspNetCore.AutofacAutoRegister.Use(services, (builder) => { });
    }

    2. 如果不使用数据库结合使用，则只引入EInfrastructure.Core.AutoFac.AspNetCore
    public IServiceProvider ConfigureServices(IServiceCollection services)
    {
        services.AddQiNiuStorage(()=>{
            var config = new QiNiuStorageConfig("accessKey", "secretKey", ZoneEnum.ZoneCnSouth(默认空间域), "默认空间所属域名", "默认空间名");
            return config;//七牛配置信息，默认上传后不回调
        });
        return EInfrastructure.Core.AutoFac.AspNetCore.AutofacAutoRegister.Use(services, (builder) => { });
    }

二、使用七牛操作文件信息

通过上方的配置可以在控制器中使用IStorageProvider、IPictureProvider两个接口的方法

    1. IStorageProvider 文件存储管理
    2. IPictureProvider 图片存储管理
    3. IBucketProvider 空间管理

    其中IPictureProvider对外提供了以下方法：
        
        1. 根据图片base64上传 Upload
        2. 抓取资源到空间  FetchFile
        3. 空间管理 IBucketProvider

    其中IStorageProvider对外提供了以下方法：

        1. 根据文件流上传 UploadStream
        2. 根据文件字节数组上传  UploadByteArray
        3. 根据文件Token上传 UploadByToken
        4. 得到上传文件凭证 GetUploadCredentials
        5. 得到管理凭证 GetManageToken
        6. 得到下载凭证 GetDownloadToken
        7. 检查文件是否存在 Exist
        8. 获取文件信息 Get
        9. 获取文件信息集合（超过1000个时会自动分批获取） GetList
        10. 根据文件key删除 Remove
        11. 根据文件key集合删除（超过1000个时会自动分批删除） RemoveRange
        12. 复制文件（两个文件需要在同一账号下） CopyTo
        13. 复制文件集合（两个文件需要在同一账号下，超过1000个时会自动分批复制） CopyRangeTo
        14. 移动文件（两个文件需要在同一账号下） Move
        15. 批量移动文件（两个文件需要在同一账号下，超过1000个时会自动分批移动） MoveRange
        16. 得到公开空间的访问地址 GetPublishUrl
        17. 得到私有空间的访问地址 GetPrivateUrl
        18. 下载文件到本地 Download
        19. 设置生存时间（超时会自动删除） SetExpire
        20. 批量设置生存时间（超时会自动删除） SetExpireRange
        21. 修改文件MimeType ChangeMime
        22. 批量更改文件mime ChangeMimeRange
        23. 修改文件存储类型 ChangeType
        24. 批量更改文件类型 ChangeTypeRange

    其中IBucketProvider对外提供以下方法

        1. 获取空间列表 GetBucketList
        2. 创建空间 Create
        3. 设置空间的镜像源 SetSource
        4. 获取空间域名信息 GetHost
        5. 删除空间 Delete
        6. 获取域名空间信息 SetPermiss
        7. 设置空间访问权限 SetTag
        8. 得到空间标签 GetTags
        9. 清除空间标签 ClearTag

    具体的方法用法可查看源码使用，其中定义的比较简单，在调用时也有相对应的注释，如果确实有不容易理解的会在文档中标注。

  
&emsp;&emsp;<a href ="https://github.com/zhenlei520/System.Extension.Core.Demo/tree/master/Storage/System.Extension.Core.AspNetCore.QiNiuStorage" target="_blank">点击查看完整示例</a> 

以上代码支持最新预览版，且自2.0.1-beta-027后，云存储默认配置中只有默认空间，默认空间域以及默认空间对应的区域，如果希望某个方法不对默认配置中的空间操作，请配置参数中的策略属性