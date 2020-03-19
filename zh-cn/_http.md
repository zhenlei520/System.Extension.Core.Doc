# Http请求类库(引用EInfrastructure.Core.Http包后即可使用)

&emsp;&emsp;基于RestSharp 106.3进行了一次封装，对简单的post以及get请求使用更方便，下面是Post以及Get请求的例子，首先可以对HttpClient进行初始化，new HttpClient("域名");HttpClient方法对外提供TimeOut超时时间、Headers请求头、Proxy代理、UserAgent请求头、IsHttps是否启用https属性

详细实例可查看<a target="_blank" href="https://github.com/zhenlei520/System.Extension.Core/blob/release/features-2.0/src/Infrastructure/test/EInfrastructure.Core.Test/HttpCommonUnitTest.cs">单元测试</a>

## Get请求

### GetString get请求获取响应字符串（GetStringAsync 异步）

    第一种写法：

    HttpClient client = new HttpClient("https://api.weixin.qq.com");
    string client_credential = "";
    string appid = "";
    string secret = "";
    var str = client.GetString($"cgi-bin/token?grant_type={client_credential}&appid={appid}&secret={secret}");
    return str;

    或者第二种：

    HttpClient client = new HttpClient("https://api.weixin.qq.com");
    string client_credential = "";
    string appid = "";
    string secret = "";
    var str = client.GetString($"cgi-bin/token,new {
        grant_type=client_credential,
        appid=appid,
        secret=secret
    });
    return str;//如果您已经有一个对象，只要保证其参数名称与需要接受的参数名称一致或者在属性头增加FromQuery属性，为其重定义name名称为请求方需要的参数名即可

    如果希望获取到Json对象，则可使用方法GetJson，如果响应内容为xml格式，则可使用GetXml方法，如果希望获取到字节数组，则使用方法GetBytes，如果希望获取响应流，则使用方法GetStream

### GetJson get请求获取响应json对象（GetJsonAsync 异步）

### GetXml get请求获取响应xml对象（GetXmlAsync 异步）

### GetBytes get请求获取响应字节数组（GetBytesAsync 异步）

### GetStream get请求获取响应流（GetStreamAsync 异步）

## Post请求

### GetStringByPost post请求获取响应字符串（PostByStringAsync 异步）

    HttpClient client = new HttpClient("https://ai.baidu.com")
    {
        Headers = new Dictionary<string, string>()
        {
            {"Cookie", ""}
        }
    };
    var file=new FileInfo("D:/jetbrains.png");
    var array = file.OpenRead().ConvertToByteArray();
    client.AddFile(new RequestMultDataParam("image",file.Name,array,"image/png"));
    var res = client.GetStringByPost($"aidemo", new
    {
        image_url = "",
        type = "animal",
        show = true
    });
    return res;//输出的值为{"errno":102,"msg":"请求Demo过于频繁","data":""}


### GetJsonByPost post请求获取响应Json对象（PostByJsonAsync 异步）

    因为接口返回是标准的Json对象，所以如果我们希望得到Json对象可以这样操作

    HttpClient client = new HttpClient("https://ai.baidu.com")
    {
        Headers = new Dictionary<string, string>()
        {
            {"Cookie", ""}
        }
    };
    var file=new FileInfo("D:/jetbrains.png");
    var array = file.OpenRead().ConvertToByteArray();
    client.AddFile(new RequestMultDataParam("image",file.Name,array,"image/png"));
    var res = client.GetJsonByPost<ResponseDto>($"aidemo", new
    {
        image_url = "",
        type = "animal",
        show = true
    });
    return res;

    public class ResponseDto
    {
        /// <summary>
        ///
        /// </summary>
        [JsonProperty(PropertyName = "errno")]
        public int Errno { get; set; }

        /// <summary>
        /// Msg
        /// </summary>
        [JsonProperty(PropertyName = "msg")]
        public string Msg { get; set; }

        /// <summary>
        /// Data
        /// </summary>
        [JsonProperty(PropertyName = "data")]
        public object Data { get; set; }
    }

    如果响应信息为Xml，可以通过GetXmlByPost得到，如果想使用异步，可以用PostByXmlAsync方法，如果希望获取响应流，可以使用GetStreamByPost方法，如果希望获取字节数组，可以使用GetBytesByPost，其中Data数据可使用匿名对象或者非匿名对象，不过非匿名对象的参数名可以通过指定JsonProperty的对其进行更改。

### PostByXmlAsync post请求获取响应xml对象（PostByXmlAsync 异步）

### PostByBytes post请求获取响应字节数组（PostByBytesAsync 异步）

### PostByStreamAsync post请求获取响应流信息（PostByStreamAsync 异步）




