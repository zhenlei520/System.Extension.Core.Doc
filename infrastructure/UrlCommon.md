<a href="https://github.com/zhenlei520/System.Extension.Core.Doc/tree/2.0/README.md">回到目录</a>

### 得到url地址：

        string url = UrlCommon.GetUrl("http://www.baidu.com?keyword=github");
        或者简写为
        string url = "http://www.baidu.com?keyword=github".GetUrl();    

### Url编码：
        UrlCommon.UrlEncode("https://github.com/zhenlei520/System.Extension.Core");
        或者简写为：
        "https://github.com/zhenlei520/System.Extension.Core".UrlEncode();

        如果希望指定编码格式：
        UrlCommon.UrlEncode("https://github.com/zhenlei520/System.Extension.Core",Encoding.UTF8);
        或者简写为：
        "https://github.com/zhenlei520/System.Extension.Core".UrlEncode(Encoding.UTF8);

### Url解码：
        UrlCommon.UrlDecode("https%3a%2f%2fgithub.com%2fzhenlei520%2fSystem.Extension.Core");
        或者简写为：
        "https%3a%2f%2fgithub.com%2fzhenlei520%2fSystem.Extension.Core".UrlDecode();

        如果希望指定编码格式：
        UrlCommon.UrlDecode("https://github.com/zhenlei520/System.Extension.Core",Encoding.UTF8);
        或者简写为：
        "https://github.com/zhenlei520/System.Extension.Core".UrlDecode(Encoding.UTF8);

### Html属性编码：
        UrlCommon.AttributeEncode("带编码的字符串");

### Html编码：
        UrlCommon.HtmlEncode("带编码的字符串");    

### Html解码：
        UrlCommon.HtmlDecode("带解码的字符串");    