# 基础方法类库(引用EInfrastructure.Core.Tools包后即可使用)

&emsp;&emsp;为了方便更多场景的使用，EInfrastructure.Core.Tools已经抽离为更纯粹的基础包，依赖的类库更少，可单独使用，控制台应用程序或者web端都可使用，目标框架支持：netstandard2.0;netstandard2.1

[![NuGet](https://img.shields.io/nuget/v/EInfrastructure.Core.Tools.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.Tools)
[![NuGet Download](https://img.shields.io/nuget/dt/EInfrastructure.Core.Tools.svg?style=flat-square)](https://www.nuget.org/packages/EInfrastructure.Core.Tools)

## 加密帮助类

    string param="";//待加密的字符串
    string decrptParam="";//待解密的字符串

### Aes加密与解密 

    string key="";//AesKey 32位字符串
    SecurityCommon.AesEncrypt(param,key);
    SecurityCommon.Decrypt(decrptParam,key);

### MD5加密

    SecurityCommon.GetMd5Hash(param);//默认编码格式：UTF8，默认大写，32位
    SecurityCommon.GetMd5HashBy16(param);//默认编码格式：UTF8，默认大写，16位
	
### Des加密与解密

    DesEncrypt：加密
    DesDecrypt：解密

    SecurityCommon.DesEncrypt(param,key,iv);//其中key为秘钥，iv为偏移量
    SecurityCommon.DesDecrypt(decrptParam,key,iv);//其中key为秘钥，iv为偏移量

### Sha加密

    string param="";
    Stream stream;
    SecurityCommon.Sha1(param);//Sha1加密
    SecurityCommon.Sha1(stream);//Sha1加密

    SecurityCommon.Sha256(param);//Sha256加密
    SecurityCommon.Sha256(stream);//Sha256加密

    SecurityCommon.Sha384(param);//Sha384加密
    SecurityCommon.Sha384(stream);//Sha384加密

    SecurityCommon.Sha512(param);//Sha512加密
    SecurityCommon.Sha512(stream);//Sha512加密

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

### 首字母小写

    StringCommon.FirstLowerCase("HelloWorld");//输出helloWorld

### 首字母大写

    StringCommon.FirstUpperCase("helloWorld");//输出HelloWorld

### 清除字符串数组中的重复项以及对字符串进行剪切

     List<string> list = new List<string>()
    {
        "", "123"
    };
    var stringArray = StringCommon.DistinctStringArray(list.ToArray(), 2);//其length为1，其中一列的值为12

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

### 转换为Char

    obj.ConvertToChar('a');//object类型强转为char类型，如果转换失败，默认为a
    obj.ConvertToChar();//object类型强转为char类型，如果转换失败，默认为null

### 转换为Guid

    obj.ConvertToGuid(default(Guid));//object类型强转为char类型，如果转换失败，默认为00000000-0000-0000-0000-000000000000
    obj.ConvertToGuid();//object类型强转为char类型，如果转换失败，默认为null

### 转换为Int

    int i=obj.ConvertToInt(0);//object类型强转为int类型，如果转换失败，默认为0
    int?i=obj.ConvertToInt();//object类型强转为可空的int类型，如果转换失败，默认为Null

### 转换为Long

    long i=obj.ConvertToLong(0);//object类型强转为long类型，如果转换失败，默认为0
    long?i=obj.ConvertToLong();//object类型强转为可空的long类型，如果转换失败，默认为Null

### 转换为Decimal

    decimal i=obj.ConvertToDecimal(0m);//object类型强转为decimal类型，如果转换失败，默认为0
    decimal?i=obj.ConvertToDecimal();//object类型强转为可空的decimal类型，如果转换失败，默认为Null

### 转换为Double

    double i=obj.ConvertToDouble(0d);//object类型强转为double类型，如果转换失败，默认为0
    double?i=obj.ConvertToDouble();//object类型强转为可空的double类型，如果转换失败，默认为Null

### 转换为DateTime

    DateTime i=obj.ConvertToDateTime(DateTime.Noe);//object类型强转为DateTime类型，如果转换失败，默认为当前时间
    DateTime?i=obj.ConvertToDateTime();//object类型强转为可空的DateTime类型，如果转换失败，默认为Null
    
### 转换为Float

    float i=obj.ConvertToFloat(0F);//object类型强转为float类型，如果转换失败，默认为0
    float?i=obj.ConvertToFloat();//object类型强转为可空的float类型，如果转换失败，默认为Null

### 转换为Short

    short i=1.ConvertToShort(0);//object类型墙砖为short类型，如果转换失败，则默认为0，其中0可指定
    short i=1.ConvertToShort();//object类型墙砖为short类型，如果转换失败，则默认为null

### 转换为bool

    short i=1.ConvertToBool(false);//object类型墙砖为bool类型，如果转换失败，则默认为false，其中智能识别True与TRUE、False与FALSE
    short i=1.ConvertToBool();//object类型墙砖为bool类型，如果转换失败，则默认为null

### 转换为byte

    byte i=1.ConvertToByte(default(byte));//object类型墙砖为byte类型，如果转换失败，则默认为default(byte)
    byte i=1.ConvertToByte();//object类型墙砖为byte类型，如果转换失败，则默认为null

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

### 保留两位小数并对其四舍五入，如果最后的两位小数为*.00则去除小数位，否则保留两位小数
		
	"1.011".ClearDecimal();//输出1.01
    "1.015".ClearDecimal();//输出1.02
    "1.001".ClearDecimal();//输出1
    "1.101".ClearDecimal();//输出1.10

### 得到n为长度的特殊符号  
		
    TypeConversionCommon.GetContentByEncryption('*', 6);//输出结果：******
    TypeConversionCommon.GetContentByEncryption("*&", 6);//输出结果：*&*&*&*&*&*&

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

	DateTime.Now.GetFormatDate('/');//输出结果：2019/01/01
	DateTime.Now.GetFormatDate('-');//输出结果：2019-01-01

### 把秒转换成分钟

    DateTime.Now.SecondToMinute(80,RectificationType.Celling);//输出结果：2
    DateTime.Now.SecondToMinute(80,RectificationType.Floor);//输出结果：1

### 返回某年某月最后一天

    TimeCommon.GetMonthLastDate(2019,1);//输出结果：31
    TimeCommon.GetMonthLastDate(2019,2);//输出结果：28


### 获得两个日期的间隔

    DateTime.Parse("2019-01-01 12:00:00").DateDiff(DateTime.Now);//获得TimeSpan类型

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

### 得到得到月初/月末/本周一/本周日/本季初/本季末/年初/年末时间 
		
    DateTime.Now.Get(TimeType.StartMonth);//得到月初时间 
    DateTime.Now.Get(TimeType.EndMonth);//得到月末时间 
    DateTime.Now.Get(TimeType.StartWeek);//得到本周周一时间 
    DateTime.Now.Get(TimeType.EndWeek);//得到本周周日时间 
    DateTime.Now.Get(TimeType.StartQuarter);//得到本季初时间 
    DateTime.Now.Get(TimeType.EndQuarter);//得到本季末时间 
    DateTime.Now.Get(TimeType.StartYear);//得到年初时间 
    DateTime.Now.Get(TimeType.EndYear);//得到年末时间 

### 得到前N秒的时间

    TimeCommon.FindASecondsAgo();//默认300秒 //假设当前时间为 2019 07-28 12:33:28，输出结果：2019 07-28 12:28:28

### 生成时间戳（10位或者13位）

    DateTime.Now.ToUnixTimestamp(TimestampType.Second);//输出结果：1564401347
    DateTime.Now.ToUnixTimestamp(TimestampType.Millisecond);//输出结果：1564404941408

### 将时间戳转时间
		
    long i=1550558491;
    i.UnixTimeStampToDateTime();//2019/7/29 20:34:32

    long j=1550558491000;
    i.UnixTimeStampToDateTime();//2019-02-19 14:41:31

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

### 根据身份证号码获取出生日期

    TimeCommon.GetBirthday("41****************");//获取生日，支持15、18位身份证号

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

### 根据年份获取生肖信息

    var animal=AnimalCommon.GetAnimalFromBirthday(1994);//输出结果：其中animal.Id为10，animal.Name为狗
    var animal=AnimalCommon.GetAnimalFromCardNo("41****************");//输出结果：其中animal.Id为10，animal.Name为狗

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

## 性别帮助类

### 根据身份证号码获取性别信息

    GenderCommon.GetGender("41****************");


## 星座帮助类

### 根据日期得到星座信息

    ConstellationCommon.GetConstellationFromBirthday(DateTime.Parse("1994-11-09")).Id;//输出结果：8
    ConstellationCommon.GetConstellationFromBirthday(DateTime.Parse("1994-11-09")).Name;//输出结果：天蝎座
    ConstellationCommon.GetConstellationFromCardNo("41****************").Name;//输出结果：天蝎座

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

### 获取字符串的HashCode

    string str="hello EInfrastructure.Core";
    UniqueCommon.GetHashCode(str);//同一个字符串在不同机器上的HashCode一样

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

### 获取类型信息

    AssemblyCommon.GetType("EInfrastructure.Core.Tools.Attributes.EDescribeAttribute","EInfrastructure.Core.Tools");//与typeof(EDescribeAttribute)效果相同

## 环境信息

### 得到当前环境信息

    EnvironmentCommon.IsWindows;//判断是否windows系统
    EnvironmentCommon.IsLinux;//是否Linux操作系统
    EnvironmentCommon.IsOsx;//是否苹果操作系统
    EnvironmentCommon.System;//得到当前操作系统

## 字符串扩展

### 得到安全字符串(期初字符串首尾空格，当值为null时返回空字符串)

    " 小磊 ".SafeString();//输出结果：小磊 （空格会被移除）


## 文件帮助类

### 得到文件的md5，sha值等

    FileCommon.GetMd5("本地文件绝对地址");//文件md5
    FileCommon.GetSha1("本地文件绝对地址");//根据本地文件地址得到文件的Sha1
    FileCommon.GetSha256("本地文件绝对地址");//根据本地文件地址得到文件的Sha256
    FileCommon.GetSha384("本地文件绝对地址");//根据本地文件地址得到文件的Sha384
    FileCommon.GetSha512("本地文件绝对地址");//根据本地文件地址得到文件的Sha512

### 得到文件信息

    FileCommon.GetFiles("要搜索的目录的相对或绝对路径");//得到当前文件夹下的所有文件地址

    FileCommon.GetFiles("要搜索的目录的相对或绝对路径","要与 path 中的文件名匹配的搜索字符串。此参数可以包含有效文本路径和通配符（* 和 ?）的组合（请参见“备注”），但不支持正则表达式");//根据通配符搜索文件下的所有地址信息，可选择查询所有层级的或者当前层级的

## 获取文件内容

### 将文件内容转换成Base64格式 

   FileCommon.FileToBase64("本地文件绝对地址");//将文件转换成Base64格式
   FileCommon.FileToBase64Async("本地文件绝对地址");//将文件转换成Base64格式（异步）

### 将文件内容转换为byte数组

    FileCommon.ConvertFileToByte("本地文件绝对地址");//将文件内容转换成byte数组
   FileCommon.ConvertFileToByteAsync("本地文件绝对地址");//将文件内容转换成byte数组（异步）

###  将byte[]数组保存成文件

    FileCommon.SaveByteToFile("byte数组","保存至硬盘的文件路径");//将byte数组保存成文件

### 获取文件内容

    FileCommon.GetFileContent("本地文件绝对地址");//获取文件内容（支持换行读取）
    FileCommon.GetFileContentAsync("本地文件绝对地址");//获取文件内容（支持换行读取）异步读取

    FileCommon.GetContentFormFile("本地文件绝对地址","编码方式");//获取文件内容（每行读取）,得到文本集合，每行一条数据
    FileCommon.GetContenFormFileAsync("本地文件绝对地址");//获取文件内容（每行读取）,返回内容集合，按照行返回（异步）

## 自定义属性

    public void GetCustomAttributeValue()
    {
        string result =
            CustomAttributeCommon<ENameAttribute, string>.GetCustomAttributeValue(typeof(UserItem),
                x => x.Name, "Name");//输出EName
        string result2 =
            CustomAttributeCommon<EDescribeAttribute, string>.GetCustomAttributeValue(typeof(UserItem),
                x => x.Describe, "Name");//输出EDescribe2
        string result3 =
            CustomAttributeCommon<EVersionAttribute, string>.GetCustomAttributeValue(typeof(UserItem),
                x => x.Version);//输出EVersion3
    }

    /// <summary>
    /// 用户信息
    /// </summary>
    [EVersion("EVersion3")]
    public class UserItem
    {
        /// <summary>
        /// 描述
        /// </summary>
        [EName("描述")]
        public string Desc { get; set; }

        /// <summary>
        /// 名称
        /// </summary>
        [EName("EName")]
        [EDescribe("EDescribe2")]
        public string Name { get; set; }
    }

## 工具类

### 得到参数以及其对象的字典类型集合

    UserItem user=new UserItem(){
        Name="名字",
        Desc="描述"
    };
    var dic=ToolCommon.GetParams();//其中dic的值是key为name、desc的字典集合，其中key是JsonProperty的Name属性，value为其值，如果希望获取自定义属性的头，需要传第二个参数

    例如：
    获取FromQuery的Name属性为：
    ToolCommon.GetParams(data, "Microsoft.AspNetCore.Mvc.FromQueryAttribute,Microsoft.AspNetCore.Mvc.Core");//其customerAttributeTypeName的值为自定义属性的完整类名,类库名

    /// <summary>
    /// 用户信息
    /// </summary>
    public class UserItem
    {
        /// <summary>
        /// 描述
        /// </summary>
        [JsonProperty(PropertyName = "desc")]
        public string Desc { get; set; }

        /// <summary>
        /// 名称
        /// </summary>
        [JsonProperty(PropertyName = "name")]
        public string Name { get; set; }
    }

## Enumerable扩展

### 泛型集合转字典

    List<User> list2 = new List<User>()
    {
        new User()
        {
            Age = 18,
            Name = "小王"
        }
    };
    Dictionary<string, int> userDic = list2.ToDictionaryExt(x => x.Name, x => x.Age);

    /// <summary>
    /// 用户信息
    /// </summary>
    public class User
    {
        /// <summary>
        /// 姓名
        /// </summary>
        public string Name { get; set; }

        /// <summary>
        /// 年龄
        /// </summary>
        public int Age { get; set; }
    }

## 服务

### 得到继承某个类型的服务集合

    new ServiceProvider().GetServices<IFluentlValidator<TEntity>>();//可以得到IFluentlValidator<TEntity>的实现类集合
    new ServiceProvider().GetService<IFluentlValidator<TEntity>>();//可以得到IFluentlValidator<TEntity>的第一个实现类

## 多线程任务

### 多线程执行任务


    public class Users
    {
        public string Name { get; set; }
    }

    例如多线程输出一个消息通知：

    TaskCommon<string> taskCommon = new TaskCommon<string>(20);

    List<Users> users = new List<Users>();
    for (var i = 0; i < 30; i++)
    {
        users.Add(new Users()
        {
            Name = "我的名字是" + i
        });
    }

    foreach (var item in users)
    {
        taskCommon.Add(item.Name, (name) =>
        {
            Console.WriteLine("我的名字是：" + name);
            Thread.Sleep(new Random().Next(1000, 3999));
        });
    }

### 多线程执行任务，且任务执行后执行一个方法

    TaskCommon<string, object> taskCommon = new TaskCommon<string, object>(20);
    List<Users> users = new List<Users>();
    for (var i = 0; i < 30; i++)
    {
        users.Add(new Users()
        {
            Name = "我的名字是" + i
        });
    }

    foreach (var item in users)
    {
        taskCommon.Add(item.Name, (name) =>
        {
            Console.WriteLine("我的名字是：" + name);
            Thread.Sleep(new Random().Next(1000, 3999));
            return "结束了" + "我的名字是：" + name;
        }, (state, res, exception) =>
        {
            if (state)
            {
                //任务完成后需要执行的工作
            }
        });
    }