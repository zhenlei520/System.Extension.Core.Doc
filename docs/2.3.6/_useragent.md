# UserAgent类库 (引用EInfrastructure.Core.UserAgentParse包后即可使用

一个专业的UserAgent类库，可以通过用户的UserAgent解析引擎信息，设备信息、浏览器信息以及操作系统信息，目前已经通过3000多条的demo测试，可以正常使用，如果大家有发现不能解析或者解析异常的，可以<a href="https://github.com/zhenlei520/System.Extension.Core/issues/new">发起Issues</a>进行提问。

使用方法：

    var ua=new UserAgent("MQQBrowser/32 Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Mobile/9B208 Safari/7534.48.3").Execute();

// you can get a json like this:

        {
            "browser": {//浏览器信息
                "name": "手机QQ",
                "version": {
                    "major": 3,
                    "second": 2
                },
                "stock": true,
                "hidden": true,
                "channel": "",
                "detail": "2"
            },
            "os": {//操作系统
                "name": "iOS",
                "version": {
                    "major": 5,
                    "second ": 1,
                    "third ": 1
                }
            },
            "device ": {//硬件信息
                "type ": {
                    "Extend ": "mobile ",
                    "Id ": 2,
                    "Name ": "移动手机"
                },
                "name": "IPHONE",
                "manufacturer": "Apple",
                "identified": true
            },
            "engine": {//浏览器内核
                "name": "Webkit ",
                "version ": {
                    "major": 534,
                    "second ": 46
                }
            },
            "features ": []
        }

其中：version的值是一个对象，其中有四个版本号信息，如果大家在使用中没有需要知道主版本是多少等等的需要的时候，可以将Version.ToString()方法获取完整的版本号信息。

参考来源：

<a href="https://github.com/fex-team/ua-device">ua-device，一个由百度fex-team团队维护的开源项目</a>

温馨提示：

其中UserAgent类库中有大量的机型匹配的代码，相对应的如果大家在使用中频繁过度去调用检查UserAgent可能会导致短时间内内存以及Cpu飙升，其中觉大多数匹配验证都是通过正则做到的，希望合理使用。