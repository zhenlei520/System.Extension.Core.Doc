# 阿里大于 短信类库(引用EInfrastructure.Core.AliYun.DaYu包后即可使用)

&emsp;&emsp;阿里大于（原阿里大鱼）是阿里通信旗下产品，融合了三大运营商的通信能力，此类库目前仅提供了指定号码发送短信以及指定多个号码发送短信的方法，当前类库结合IOC注入使用会更简单，也更方便。

[![NuGet](https://img.shields.io/nuget/v/EInfrastructure.Core.AliYun.DaYu.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.AliYun.DaYu)
[![NuGet Download](https://img.shields.io/nuget/dt/EInfrastructure.Core.AliYun.DaYu.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.AliYun.DaYu)

## 通过IOC注入使用配置

### 在NetCore下使用

    方法一（推荐）：
        1. 如果与Mysql数据库结合使用，则引入EInfrastructure.Core.AutoFac.MySql.AspNetCore

            services.AddAliDaYu(()=>{
                return new AliSmsConfig(){
                    SignName="签名名称",
                    AccessKey="AccessKey ID",
                    EncryptionKey="秘钥参数",
                };
            });
            new EInfrastructure.Core.AutoFac.MySql.AspNetCore.AutofacAutoRegister().Build(
                    services,
                    (builder) => { });

        2. 如果与SQLServer数据库结合使用，则引入EInfrastructure.Core.AutoFac.SqlServer.AspNetCore

            services.AddAliDaYu(()=>{
                return new AliSmsConfig(){
                    SignName="签名名称",
                    AccessKey="AccessKey ID",
                    EncryptionKey="秘钥参数",
                };
            });
            new EInfrastructure.Core.AutoFac.SqlServer.AspNetCore.AutofacAutoRegister().Build(
                    services,
                    (builder) => { });

        3. 如果不使用数据库，则引入EInfrastructure.Core.AutoFac.AspNetCore

            services.AddAliDaYu(()=>{
                return new AliSmsConfig(){
                    SignName="签名名称",
                    AccessKey="AccessKey ID",
                    EncryptionKey="秘钥参数",
                };
            });
            new EInfrastructure.Core.AutoFac.AspNetCore.AutofacAutoRegister().Build(
                    services,
                    (builder) => { });


    方法二：
        需要引入EInfrastructure.Core.Serialize.NewtonsoftJson、EInfrastructure.Core.Serialize.Xml后配置

    //首先在项目的Startup中添加阿里大于的使用以及短信参数配置
    public IServiceProvider ConfigureServices(IServiceCollection services)
    {
        services.AddAliDaYu(()=>{
            return new AliSmsConfig(){
                SignName="签名名称",
                AccessKey="AccessKey ID",
                EncryptionKey="秘钥参数",
            };
        });

        services.AddSingleton<ISmsProvider, SmsProvider>();
        EInfrastructure.Core.Serialize.NewtonsoftJson.StartUp.Run(false);
        EInfrastructure.Core.Serialize.Xml.StartUp.Run(false);
    }


    之后在控制器中可以：

    public class CheckController : Controller
    {
        private readonly ISmsProvider _smsProvider;

        public CheckController(ISmsProvider smsProvider){
            _smsProvider=smsProvider;
        }

        /// <summary>
        /// 发送短信（其中第三个参数为短信模板所需要的值，其属性为模板的参数name，其属性值为需要显示的参数值）
        /// </summary>
        /// <returns></returns>
        public void SendSms(){
            _smsProvider.Send("13653217777","SMS_*******",new {content="内容"},(res)=>{
                //响应失败原因
            });

            _smsProvider.Send(new List<string>(){"13653217777","13654857777"},"SMS_*******",new {content="内容"},(res)=>{
                //响应失败原因
            });
        }
    }

### 在控制台应用程序下使用IOC注入

    多引入类库EInfrastructure.Core.AutoFac

    public IServiceProvider GetServiceProvider(){
        IConfigurationBuilder Configuration = new ConfigurationBuilder();
        IConfigurationRoot configuration = Configuration.SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("appsettings.json", optional: false, reloadOnChange: true)
            .AddEnvironmentVariables().Build();
        IServiceCollection services = new ServiceCollection();
        Assembly[] assembly = AppDomain.CurrentDomain.GetAssemblies();
        services.AddAliDaYu(()=>{
                return new AliSmsConfig(){
                    SignName="签名名称",
                    AccessKey="AccessKey ID",
                    EncryptionKey="秘钥参数",
                };
            });
        return new EInfrastructure.Core.AutoFac.AutofacAutoRegister().Build(
                services,
                (builder) => { });
    }

    public static void Main(){
        var provider=GetServiceProvider().GetService<ISmsProvider>();
        provider.Send("13653217777","SMS_*******",new {content="内容"},(res)=>{
            //响应失败原因
        });

        provider.Send(new List<string>(){"13653217777","13654857777"},"SMS_*******",new {content="内容"},(res)=>{
            //响应失败原因
        });
    }


## 传统模式下（非IOC使用）：
    
    需要引入EInfrastructure.Core.Serialize.NewtonsoftJson、EInfrastructure.Core.Serialize.Xml后配置

    var smsProvider=new SmsProvider(new AliSmsConfig(){
        SignName="签名",
        AccessKey="AccessKey ID",
        EncryptionKey="秘钥参数"
    },List<IJsonProvider>()
    {
        new NewtonsoftJsonProvider()
    }, new List<IXmlProvider>()
    {
        new XmlProvider()
    });

    smsProvider.Send("13653217777","SMS_*******",new {content="内容"},(res)=>{
        //响应失败原因
    });

    smsProvider.Send(new List<string>(){"13653217777","13654857777"},"SMS_*******",new {content="内容"},(res)=>{
        //响应失败原因
    });