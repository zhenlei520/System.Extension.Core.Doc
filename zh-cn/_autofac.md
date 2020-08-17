# AutoFac（IOC）自动注入类库(引用EInfrastructure.Core.AutoFac系列包后即可使用)

&emsp;&emsp;基于Autofac的基础上，很简单的实现了自动注入，并与Mysql、SQLService结合，在AspNetCore环境下或者控制台环境下都有一个好的体验：

[![NuGet](https://img.shields.io/nuget/v/EInfrastructure.Core.AutoFac.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.AutoFac)
[![NuGet Download](https://img.shields.io/nuget/dt/EInfrastructure.Core.AutoFac.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.AutoFac)


&emsp;&emsp;为了更方便我们的注入，我们约定IPerRequest、IDependency、ISingleInstance三种接口。

### IPerRequest 

    同一个生命周期生成的对象是同一个实例，在一次Http请求中是一个生命周期；

### IDependency

    默认模式，每次调用，都会重新实例化对象；每次请求都创建一个新的对象；

### ISingleInstance 

    单例模式，每次调用，都会使用同一个实例化的对象；在项目启动后每次都用同一个对象;


&emsp;&emsp;例如：如果我们希望使用单例模式，声明一个IPerson接口后继承ISingleInstance，再写IPerson的实现类Person即可，完整代码如下：

    public interface  IPerson:ISingleInstance
    {
        void Run();
    }

    public class Person:IPerson{

        /// <summary>
        /// 奔跑
        /// </summary>
        public void Run()
        {

        }
    }

&emsp;&emsp;在NetCore下的配置，需要在项目的Startup中添加Autofac自动注入

    1. 环境为NetCore+Ioc自动注入
    public IServiceProvider ConfigureServices(IServiceCollection services)
    {
        services.AddMvc().AddControllersAsServices();
        return EInfrastructure.Core.AutoFac.AutofacAutoRegister.Use(
                services,
                (builder) => { });
    }

    2. 环境为NetCore+Ioc自动注入（推荐），可以引入EInfrastructure.Core.AutoFac.AspNetCore包，因为它配置更为简单：

    public IServiceProvider ConfigureServices(IServiceCollection services)
    {
        return EInfrastructure.Core.AutoFac.AspNetCor.AutofacAutoRegister.Use(
                services,
                (builder) => { });
    }
&emsp;&emsp;<a href ="https://github.com/zhenlei520/System.Extension.Core.Demo/tree/master/Autofac/Autofac.AspNetCore" target="_blank">点击查看完整示例</a> 

    3. 环境为NetCore+Ioc自动注入+Mysql，建议您使用包：EInfrastructure.Core.AutoFac.MySql.AspNetCore

    public IServiceProvider ConfigureServices(IServiceCollection services)
    {
        return EInfrastructure.Core.AutoFac.MySql.AspNetCore.AutofacAutoRegister.Use(
                services,
                (builder) => { });
    }
&emsp;&emsp;<a href ="https://github.com/zhenlei520/System.Extension.Core.Demo/tree/master/Autofac/Autofac.AspNetCore.MySql" target="_blank">点击查看完整示例</a> 

    4. 环境为NetCore+Ioc自动注入+SqlServer，建议您使用包：EInfrastructure.Core.AutoFac.SqlServer.AspNetCore

    public IServiceProvider ConfigureServices(IServiceCollection services)
    {
        return EInfrastructure.Core.AutoFac.SqlServer.AspNetCore.AutofacAutoRegister.Use(
                services,
                (builder) => { });
    }
    
&emsp;&emsp;其中SQLService类库与Mysql的类似，对应引入EInfrastructure.Core.AutoFac.SqlServer.AspNetCore即可，就不再放示例了

&emsp;&emsp;在控制台下的配置


    1. 仅需Ioc自动注入
    public IServiceProvider GetServiceProvider(){
        IServiceCollection services = new ServiceCollection();
        return  EInfrastructure.Core.AutoFac.AutofacAutoRegister.Use(
                services,
                (builder) => { });
    }

&emsp;&emsp;<a href ="https://github.com/zhenlei520/System.Extension.Core.Demo/tree/master/Autofac/Autofac.Demo" target="_blank">点击查看控制台完整示例</a>    

    2. 需Ioc自动注入+Mysql，建议您使用包：EInfrastructure.Core.AutoFac.MySql

    public IServiceProvider GetServiceProvider(){
        IServiceCollection services = new ServiceCollection();
        return  EInfrastructure.Core.AutoFac.MySql.AutofacAutoRegister.Use(
                services,
                (builder) => { });
    }
&emsp;&emsp;<a href ="https://github.com/zhenlei520/System.Extension.Core.Demo/tree/master/Autofac/Autofac.MySql" target="_blank">点击查看Mysql完整示例</a>    

    3. 需Ioc自动注入+Mysql，建议您使用包：EInfrastructure.Core.AutoFac.SqlServer
    public IServiceProvider GetServiceProvider(){
        IServiceCollection services = new ServiceCollection();
        return  EInfrastructure.Core.AutoFac.SqlServer.AutofacAutoRegister.Use(
                services,
                (builder) => { });
    }
&emsp;&emsp;其中SQLService类库与Mysql的类似，对应引入EInfrastructure.Core.AutoFac.SqlServer即可，就不再放示例了

以上的代码片段如果不容易理解的话，可下载示例代码查看。

ps：如果遇到完全按照以上标准写得东西最后注入不进去的情况，麻烦检查一下在startup中是否有引用您希望注入的实现类所在的命名空间，netcore注入利用的是反射，但项目刚开始运行时是按需加载的，就会导致一些类库没有正常引用，那样就会导致注入失败的问题出现，可在获取容器之前引用所在的类的命名空间即可处理，我一般是在其根目录创建一个Startup文件，然后引用主动加载其命名空间，后面也会考虑使用加载指定类库文件的方式进行注入。