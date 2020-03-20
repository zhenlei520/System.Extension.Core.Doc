# 基础库扩展类库(引用EInfrastructure.Core包后即可使用)

&emsp;&emsp;基于EInfrastructure.Core.Tools之上对方法进行了更深一层的封装，之前的版本没有EInfrastructure.Core.Tools，但发现在普通的控制台等程序上使用比较不爽，还需要再通过依赖注入才能更好的使用其中的方法，另外一些方法基于Ioc在做，但没有更清晰的划分，后拆分为EInfrastructure.Core.Tools与EInfrastructure.Core两个类库，引用此类库后可以使用所有的简单的普通方法，依赖关系可查看(zh-cn/abstract.md)

[![NuGet](https://img.shields.io/nuget/v/EInfrastructure.Core.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core)
[![NuGet Download](https://img.shields.io/nuget/dt/EInfrastructure.Core.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core)

## 图片帮助类

### 根据上传文件获取图片base64
    
    ImageCommon.GetBase64(file);//其中file为IFormFile类型，返回图片base64字符串

## 文件帮助类

    IFormFile file;

### 得到文件md5

    FileCommon.GetMd5(file);

### 得到文件的Sha1

    FileCommon.GetSha1(file,true);//默认转大写

### 得到文件的Sha256

     FileCommon.GetSha256(file,true);//默认转大写

### 得到文件的Sha384

     FileCommon.GetSha384(file,true);//默认转大写

### 得到文件的Sha512

     FileCommon.GetSha512(file,true);//默认转大写

### 得到文件的文件名以及唯一标识

    FileCommon.Get(file,EncryptType.Md5);//得到文件的名称以及md5唯一标识

### 随机数生成器

    其中声明了随机数字数类，只要实现IRandomNumberGenerator，后续的可以通过注入或者其实现类，实现随机数方法

### 根据权重获取实现类

    NetCore中同一接口可以有实现，通过InjectionSelectionCommon.GetImplement()，可以得到其中权重最高的实现类，如果只有一个实现类的话，得到第一个实现类
    例如：IJsonProvider有多个实现类，则可以：

        ICollection<IJsonProvider>providers;
        IJsonProvider provider=InjectionSelectionCommon.GetImplement(providers);

