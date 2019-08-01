# 基础方法类库

## 加密帮助类

    string param="";//待加密的字符串
    string decrptParam="";//待解密的字符串

### Aes加密与解密 

    string key="";//AesKey 32位字符串
    SecurityCommon.AesEncrypt(param,key);
    SecurityCommon.Decrypt(decrptParam,key);

### MD5加密

    SecurityCommon.GetMd5Hash(param);//默认编码格式：UTF8
	
### Des加密与解密

    DesEncrypt：加密
    DesDecrypt：解密

    SecurityCommon.DesEncrypt(param,key,iv);//其中key为秘钥，iv为偏移量
    SecurityCommon.DesDecrypt(decrptParam,key,iv);//其中key为秘钥，iv为偏移量

### Sha加密

    SecurityCommon.Sha1(param);//Sha1加密
    SecurityCommon.Sha256(param);//Sha256加密
    SecurityCommon.Sha384(param);//Sha384加密
    SecurityCommon.Sha512(param);//Sha512加密

### HMacSha1加密

    SecurityCommon.HMacSha1(param,key);//其中key为秘钥

### JS Aes 加密与解密

    SecurityCommon.JsAesEncrypt(param,key,iv);//其中key为秘钥，iv为偏移量
    SecurityCommon.JsAesDecrypt(param,key,iv);//其中key为秘钥，iv为偏移量

## 字符串扩展

### 字符串转换为泛型集合

	"1,2".ConvertStrToList<int>(',');//默认分隔符为,

### 隐藏手机号码

    StringCommon.HideMobile("13653487541");//136****7541

### 加密隐藏信息

将原信息其中一部分数据替换为特殊字符：

    StringCommon.EncryptStr("13653487541","*",3,4);//136****7541

## 类型转换

提示：类型转换统一格式：ConvertTo
目前支持：
ConvertToChar obj转Char
ConvertToGuid obj转Guid
ConvertToInt obj转Int
ConvertToShort obj转Short
ConvertToDecimal obj转decimal
ConvertToDouble obj转double
ConvertToFloat obj转float
ConvertToDateTime obj转datetime
ConvertToByte obj转byte
ConvertToSByte obj转sbyte
ConvertToBool obj转bool

示例：

### 转换为Int

    int i=obj.ConvertToInt(0);//object类型强转为int类型，如果转换失败，默认为0
    int?i=obj.ConvertToInt();//object类型强转为可空的int类型，如果转换失败，默认为Null

### 转换为Decimal

    decimal i=obj.ConvertToDecimal(0m);//object类型强转为decimal类型，如果转换失败，默认为0
    decimal?i=obj.ConvertToDecimal();//object类型强转为可空的decimal类型，如果转换失败，默认为Null

### 转换为Short

    short i=1.ConvertToShort(0);//object类型墙砖为short类型，如果转换失败，则默认为0，其中0可指定

所有类型转换均参考此格式。

### 转为byte数组

	byte[]tem=Stream.ConvertToByteArray(); //Stream转为byte数组
    byte[]tem=String.ConvertToByteArray();//String转为byte数组

### 转为Stream

    Stream stream=byte[].ConvertToStream();//byte数组转为Stream

###	byte数组转换为string
 
    String str=byte[].ConvertToString();//byte数组转换为string

### 字符串base64转byte数组
	
    byte[]tem=base64.ConvertToByte();

### byte数组转换为base64
	
    string base64=byte[].ConvertToBase64();

### Stream转换为base64
	
    string base64=Stream.ConvertToBase64();

### 清除小数点后0  
		
	String.ClearDecimal();//其中String为要待去除的字符串

### 得到n为长度的特殊符号  
		
    TypeConversionCommon.GetContentByEncryption('*', 6);//输出结果：******
    TypeConversionCommon.GetContentByEncryption("*", 6);//输出结果：******

### 值互换(左边最小值,右边最大值)

提示：方法支持类型有：int，decimal，DateTime，byte，float，double  

    int x=2,y=1;
    TypeConversionCommon.ChangeResult(ref x,ref y);//输入结果：x=1,y=2;

    decimal x=5.2m,y=1.5m;
    TypeConversionCommon.ChangeResult(ref x,ref y);//输入结果：x=1.5m,y=5.2m;

### Unicode编码与解码

    "码云".ConvertStringToUnicode();//汉字转换为Unicode编码，输出结果：\u7801\u4e91

    "\u7801\u4e91".ConvertUnicodeToString();//汉字转换为Unicode编码，输出结果：码云

## 时间帮助类

### 格式化时间1

	DateTime.Now.Format("yyyy-MM-dd");//输出结果：2019-01-01

### 格式化时间2

将时间格式化成 年月日 的形式,如果时间为null，返回当前系统时间：

	DateTime.Now.GetFormatDate("/");//输出结果：2019/01/01

### 把秒转换成分钟

    DateTime.Now.SecondToMinute(80);//输出结果：2
    DateTime.Now.SecondToMinute(80,RectificationType.Celling);//输出结果：2
    DateTime.Now.SecondToMinute(80,RectificationType.Floor);//输出结果：1

### 返回某年某月最后一天

    TimeCommon.GetMonthLastDate(2019,1);//输出结果：31
    TimeCommon.GetMonthLastDate(2019,2);//输出结果：28

### 返回时间差

    DateTime.Parse("2019-01-01 12:00:00").DateDiff(DateTime.Now);//输出结果：n月n日或者n小时前或者n分钟前

### 获得两个日期的间隔

    DateTime.Now.DateDiff2(DateTime.Parse('2019-01-01 12:00:00'));

### 格式化日期时间

    DateTime.Now.FormatDate();//默认yyyy-MM-dd HH:mm:ss 输出结果：2019-07-28 12:00:00
    DateTime.Now.FormatDate(FormatDateTypeEnum.Zero);//yyyy-MM-dd 输出结果：2019-07-28
    DateTime.Now.FormatDate(FormatDateTypeEnum.One);//yyyy-MM-dd HH:mm:ss 输出结果：2019-07-28 12:00:00
    DateTime.Now.FormatDate(FormatDateTypeEnum.Two);//yyyy/MM/dd 输出结果：2019/07/28
    DateTime.Now.FormatDate(FormatDateTypeEnum.Three);//yyyy年MM月dd日 输出结果：2019年07月28日
    DateTime.Now.FormatDate(FormatDateTypeEnum.Four);//MM-dd 输出结果：07-28
    DateTime.Now.FormatDate(FormatDateTypeEnum.Five);//MM/dd 输出结果：07/28
    DateTime.Now.FormatDate(FormatDateTypeEnum.Six);//MM月dd日 输出结果：07月28日
    DateTime.Now.FormatDate(FormatDateTypeEnum.Seven);//yyyy-MM 输出结果：07-28
    DateTime.Now.FormatDate(FormatDateTypeEnum.Eight);//yyyy/MM 输出结果：07/28
    DateTime.Now.FormatDate(FormatDateTypeEnum.Nine);//yyyy年MM月 输出结果：2019年07月

### 得到随机日期

间隔日期之间的 随机日期：

    DateTime.Now.GetRandomTime(DateTime.Parse('2019-01-01 12:00:00')); 输出结果： 2019-08-24 23:22:52

### 返回每月的第一天和最后一天

    string firstDay,string lastDay;
    TimeCommon.ReturnDateFormat(2019,12,out firstDay.out lastDay);//可以得到2019年12月份的第一天和最后一天 输出结果： firstDay： 2019-12-01,  lastDay： 2019-12：:3

### 得到据当前多远时间
		
    DateTime.Now.GetAccordingToCurrent();//得到距离当前多远时间 //输出结果：刚刚

### 得到月初与月末时间
		
    DateTime.Now.Get(TimeType.StartMonth);//得到月初/月末/本周一/本周日/本季初/本季末/年初/年末时间 

### 得到前N秒的时间

    TimeCommon.FindASecondsAgo();//默认300秒 //假设当前时间为 2019 07-28 12:33:28，输出结果：2019 07-28 12:28:28

### 得到13位时间戳

    DateTime.Now.GetTimeSpan();//输出结果：1564399976948

### 获取10位不带毫秒的Unix时间戳

根据DateTime时间格式转换为10位不带毫秒的Unix时间戳：

    DateTime.Now.ConvertDateTimeInt();//输出结果：1564400509

### 将当前Utc时间转换为总秒数

    DateTime.Now.ToUnixTimestamp();//输出结果：1564401347

### 将10位时间戳转时间
		
    long i=1550558491;
    i.UnixTimeStampToDateTime();//2019/7/29 20:34:32

### 将13位时间戳转为时间

    long i=1550558491000;
    i.JsTimeStampToDateTime();

### 获得总秒数

    TimeCommon.CurrentTimeMillis();//默认从1970年1月1日 0点0分到现在的总时间 输出结果：1564404941408

### 阳历转阴历(农历)
    
    "1994-11-09".ConvertToDateTime(default(DateTime)).ConvertToLunar()；//输出结果：[狗]甲戌1994 十月初七

    "1994-11-09".ConvertToDateTime(default(DateTime)).GetYear()；//输出结果：[狗]甲戌1994 

    "1994-11-09".ConvertToDateTime(default(DateTime)).GetMonth()；//输出结果：十月

    "1994-11-09".ConvertToDateTime(default(DateTime)).GetDay()；//输出结果：初七

    "2019-07-07".ConvertToDateTime(default(DateTime)).GetSolarTerm();//输出结果：小暑

    "2019-01-01".ConvertToDateTime(default(DateTime)).GetHoliday();//输出结果：元旦

    "2019-02-05".ConvertToDateTime(default(DateTime)).GetChinaHoliday();//输出结果：春节

    "2019-02-05".ConvertToDateTime(default(DateTime)).GetLunarYearDate();//输出结果：2019-03-11

    "2019-03-11".ConvertToDateTime(default(DateTime)).GetLunarYearDate();//输出结果：2019-02-05

### 获取当前是周几

     var weekName = Week.GetAll<Week>().Where(x => x.Id == dateStr).Select(x => x.Name);
     Week time = DateTime.Parse("2019-07-29").GetDayName();//输出结果：Week.Monday

     var time = DateTime.Parse("2019-07-29").GetDayName(new[]
    {
        "星期日", "星期一", "星期二", "星期三", "星期四", "星期五", "星期六"
    });//输出结果：星期一

## 验证帮助类

### 是否邮政编码

    "450000".IsZipCode();//输出结果：true

### 是否邮箱

    "wangzhenlei520@gmail.com".IsEmail();//输出结果：true

### 是否为手机号

    "13653777777".IsMobile();//输出结果：true

### 是否为固话号

    "0373-6793210".IsPhone();//输出结果：true

### 是否包含数字

    "123asd".IsNumber();//输出结果：true
    "123".IsNumber();//输出结果：true
    "github".IsNumber();//输出结果：false

### 是否为纯数字

    "13653777777".IsOnlyNumber();//输出结果：true
    "13653777777w".IsOnlyNumber();//输出结果：false
    "a123a".IsOnlyNumber();//输出结果：false
    "github".IsOnlyNumber();//输出结果：false

### 是否是身份证号

提示：机器识别，根据身份证规则检测。

    "410782199310069652".IsIdCard();//输出结果：false

### 判断是否为Guid

    "77d99c08-a192-4a16-80dd-5e50f6e1c2d2".IsGuid();//输出结果：true
    "77d99c08-a192-4a16-80dd-5e50f6e1-c2d2".IsGuid();//输出结果：false


### 是否为IP

    "192.168.1.124".IsIp();//输出结果：true
    "a.d.1.124".IsIp();//输出结果：false

### 判断是否网址

    "http://github.com/zhenlei520".IsUrl();//输出结果：true
    "https://github.com/zhenlei520".IsUrl();//输出结果：true
    "github.com/zhenlei520".IsUrl();//输出结果：true
    "百度".IsUrl();//输出结果：false

### 判断是否中文

    "github.com/zhenlei520".IsChinese();//输出结果：false
    "百度".IsChinese();//输出结果：true

## 枚举帮助类

    /// <summary>
    /// 性别
    /// </summary>
    public enum GenderEnum
    {
        /// <summary>
        /// 未知 
        /// </summary>
        [Description("未知")] Unknow = 0,

        /// <summary>
        /// 男
        /// </summary>
        [Description("男")] Boy = 1,

        /// <summary>
        /// 女
        /// </summary>
        [Description("女")] Girl = 2,
    } 

### 得到枚举项的描述信息

    GenderEnum.Boy.GetDescription();//输出结果：男

### 判断值是否在枚举中存在

    1.IsExist(typeof(GenderEnum));//输出结果：true

### 得到枚举字典

    EnumCommon.ToDescriptionDictionary<GenderEnum>();//返回字典类型，其中key为枚举的值，value为枚举的描述  

## 生肖帮助类

### 根据年份获取生肖属性

    AnimalCommon.GetAnimalFromBirthday(1994);//输出结果：狗

### 根据年份获取生肖对象

    var animal=AnimalCommon.GetAnimalEnumFromBirthday(1994);//输出结果：其中animal.Id为10，animal.Name为狗

## 拷贝帮助类

DeepClone：深拷贝
ShallowClone：浅拷贝

需要继承CloneableClass类，且类必须在属性头上增加关键字[Serializable]

    /// <summary>
    /// 性别
    /// </summary>
    [Serializable]
    public class Person : CloneableClass
    {
        public string Name { get; set; }

        public GenderEnum Gender { get; set; }
    }

### 深拷贝

其中必须在Class增加[Serializable]

    Person person = new Person
    {
        Name = "小明",
        Gender = GenderEnum.Boy
    };
    var newPerson = person.DeepClone(person);
    newPerson.Name = "小明哥";
    Check.True(person.Name != newPerson.Name, "方法有误");

### 浅拷贝

引用地址

    Person person = new Person
    {
        Name = "小明",
        Gender = GenderEnum.Boy
    };
    var newPerson2 = person.ShallowClone<Person>();
    Check.True(person.Name == newPerson2.Name, "方法有误");

## 星座帮助类

### 根据日期得到星座名称

    ConstellationCommon.GetConstellationFromBirthday(DateTime.Parse("1994-11-09"));//输出结果：天蝎座

### 根据日期得到星座枚举类

    ConstellationCommon.GetConstellationEnumFromBirthday(DateTime.Parse("1994-11-09")).Id;//输出结果：8

## 邮箱帮助类

### 发送邮件

    EMailCommon.SendEmail(toEmail, title, body, "发送者的邮箱地址", "网络上的代理服务器", "发送邮件的密码", "成功");//输出结果：Status：发送状态，Msg：提示信息

## List帮助类

### List实体添加

提醒：其中T增加[Serializable]

    [Serializable]
    public class Person
    {
        public string Name { get; set; }
    }

    public void Add()
    {
        List<Person> personList = new List<Person>()
        {
            new Person
            {
                Name = "小明"
            }
        };
        List<Person> personList2 = new List<Person>()
        {
            new Person
            {
                Name = "小明"
            },
            new Person
            {
                Name = "小明花"
            }
        };
        var persons = personList.Add(personList2);
        persons = personList.Add(personList2,true);
    }

### List实体减法操作

提醒：其中T增加[Serializable]

    List<Person> personList = new List<Person>()
    {
        new Person
        {
            Name = "小明"
        },
        new Person
        {
            Name = "小明花2"
        }
    };
    List<Person> personList2 = new List<Person>()
    {
        new Person
        {
            Name = "小明"
        },
        new Person
        {
            Name = "小明花"
        }
    };
    var persons = personList.Minus(personList2);
    persons = personList.Minus(personList2,true);

###  List转String

提示：可帮助去除空格

    List<int> idList = new List<int>()
    {
        1, 2, 3
    };
    string str = idList.ConvertListToString(',');//输出结果：1,2,3

    List<string> nameList = new List<string>()
    {
        "小李",
        "",
        "小红"
    };
    str = nameList.ConvertListToString(',', true, true);//输出结果：小李,小红

###  字符串数组集合转String

提示：可帮助去除空格

    new[]{"小李","","小红"}.ConvertListToString(',', true, true);//输出结果：小李,小红

###  对list集合分页

    List<Person> personList = new List<Person>()
    {
        new Person
        {
            Name = "小明"
        },
        new Person
        {
            Name = "小明花2"
        }
    };
    var pageData = personList.ListPager(1, 1, true);//输出结果：{"total":2,"data":[{"name":"小明"}]} 。其中total为数据总数，data为数据集合，适合ICollection集合

###  对list集合分页，且循环执行委托

例如：

    personList.ListPager(newpersonList =>
    {
        newpersonList.ForEach(person =>
        {
            Console.WriteLine("一起上Github看源码吧");
        });
    },1,1);


###  添加单个对象

其方法与Add类似，可在集合中添加单个对象，但是区别是有返回值，对一般的集合并无作用，例子如下：

    public class Person
    {
        public string Name { get; set; }

        public List<string> Tags
        {
            get => (List<string>) new NewtonsoftJsonProvider().Deserialize(this.TagJson, typeof(List<string>));
            set => this.TagJson = new NewtonsoftJsonProvider().Serializer(value);
        }

        public string TagJson { get; private set; }
    }
    Person person = new Person()
    {
        Name = "小明",
        Tags = new List<string> {"帅哥"}
    };
    person.Tags = person.Tags.AddNew("聪明");
    Console.WriteLine(person.TagJson);

###  集合中添加另外一个集合

其方法与AddRange类似，可在集合中添加另外一个集合，但是区别是有返回值，对一般的集合并无作用，其Person类引用上个方法的Person类，例子如下：

    Person person = new Person
    {
        Name = "小明",
        Tags = new List<string> {"帅哥"}
    };
    person.Tags = person.Tags.AddNewMult(new List<string>
    {
        "聪明",
        "伶俐"
    });
    Console.WriteLine(person.TagJson);


###  在集合中移除单个对象

其方法与Remove类似，可在集合中移除单个对象，但是区别是有返回值，对一般的集合并无作用，其Person类引用上个方法的Person类，例子如下：

    Person person = new Person()
    {
        Name = "小明",
        Tags = new List<string> {"帅哥"}
    };
    person.Tags = person.Tags.RemoveNew("帅哥");

###  集合中移除单个满足条件的对象

其方法与RemoveNew类似，可在集合中移除单个满足条件的对象，但是区别是有返回值，对一般的集合并无作用，其Person类引用上个方法的Person类，例子如下：

    Person person = new Person()
    {
        Name = "小明",
        Tags = new List<string> {"帅哥"}
    };
    person.Tags = person.Tags.RemoveNew(x=>x=="帅哥");

###  集合中移除满足条件的集合

其方法与RemoveAll类似，可在集合中移除满足条件的集合，但是区别是有返回值，对一般的集合并无作用，其Person类引用上个方法的Person类，例子如下：

    Person person = new Person
    {
        Name = "小明",
        Tags = new List<string> {"帅哥"}
    };
    person.Tags = person.Tags.RemoveMultNew(x=>x=="帅哥");
    Console.WriteLine(person.TagJson);

## 距离帮助类

###  计算两点位置的距离

计算两点位置的距离，返回两点的距离，单位：米

    var distance = DistanceCommon.GetDistance(lat1, lng1, lat2, lng2);//lat1：第一点纬度，lng1：第一点经度，lat2：第二点纬度，lng2：第二点经度
    Check.True(distance < result, "方法有误");

## 唯一方法实现

###  全局唯一Guid

    UniqueCommon.Guids();//输出结果：//80fe4e8c6d1c40848cfe1b7aace339bc

## Url帮助类

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

### 大小写转换

### 转换为大写：

    MathCommon.ToUppers("abCD");
    或者简写为：
    "abCD".ToUppers();

### 转换为小写：
        
    MathCommon.ToLowers("abCD");
    或者简写为：
    "abCD".ToLowers();

## 应用程序集扩展类

### 获得Assembly版本号

    AssemblyCommon.GetAssemblyVersion();

### 获得Assembly产品版权

    AssemblyCommon.GetAssemblyCopyright();

### 根据类型实例化当前类

    public class Person{
        public string Name{get;set;}
    }
    AssemblyCommon.CreateInstance(typeof(Person));

### 得到调用者信息

    AssemblyCommon.GetReflectedInfo();
