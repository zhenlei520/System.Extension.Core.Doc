# 基础方法类库

## 时间帮助类

&emsp;&emsp;格式化时间：

	DateTime.Now.Format("yyyy-MM-dd");//输出结果：2019-01-01

&emsp;&emsp;将时间格式化成 年月日 的形式,如果时间为null，返回当前系统时间：

	DateTime.Now.GetFormatDate("/");//输出结果：2019/01/01

&emsp;&emsp;把秒转换成分钟：

    DateTime.Now.SecondToMinute(80);//输出结果：2
    DateTime.Now.SecondToMinute(80,RectificationType.Celling);//输出结果：2
    DateTime.Now.SecondToMinute(80,RectificationType.Floor);//输出结果：1

&emsp;&emsp;格式化时间：

    TimeCommon.GetMonthLastDate(2019,1);//输出结果：31
    TimeCommon.GetMonthLastDate(2019,2);//输出结果：28

&emsp;&emsp;返回时间差：

    DateTime.Parse("2019-01-01 12:00:00").DateDiff(DateTime.Now);//输出结果：n月n日或者n小时前或者n分钟前

&emsp;&emsp;获得两个日期的间隔：

    DateTime.Now.DateDiff2(DateTime.Parse('2019-01-01 12:00:00'));


&emsp;&emsp;格式化日期时间：

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

&emsp;&emsp;得到随机日期（间隔日期之间的 随机日期）：

    DateTime.Now.GetRandomTime(DateTime.Parse('2019-01-01 12:00:00')); 输出结果： 2019-08-24 23:22:52


&emsp;&emsp;得到随机日期（间隔日期之间的 随机日期）：

    string firstDay,string lastDay;
    TimeCommon.ReturnDateFormat(2019,12,out firstDay.out lastDay);//可以得到2019年12月份的第一天和最后一天 输出结果： firstDay： 2019-12-01,  lastDay： 2019-12：:3

&emsp;&emsp;得到据当前多远时间：
		
    DateTime.Now.GetAccordingToCurrent();//得到距离当前多远时间 //输出结果：刚刚


&emsp;&emsp;得到月初与月末时间：
		
    DateTime.Now.Get(TimeType.StartMonth);//得到月初/月末/本周一/本周日/本季初/本季末/年初/年末时间 

&emsp;&emsp;得到前N秒的时间：

    TimeCommon.FindASecondsAgo();//默认300秒 //假设当前时间为 2019 07-28 12:33:28，输出结果：2019 07-28 12:28:28

&emsp;&emsp;得到13位时间戳：

    DateTime.Now.GetTimeSpan();//输出结果：1564399976948

&emsp;&emsp;DateTime时间格式转换为10位不带毫秒的Unix时间戳：

    DateTime.Now.ConvertDateTimeInt();//输出结果：1564400509

&emsp;&emsp;将当前Utc时间转换为总秒数：

    DateTime.Now.ToUnixTimestamp();//输出结果：1564401347

&emsp;&emsp;将10位时间戳转时间：
		
    long i=1550558491;
    i.UnixTimeStampToDateTime();//2019/7/29 20:34:32

&emsp;&emsp;将13位时间戳转为时间：

    long i=1550558491000;
    i.JsTimeStampToDateTime();

&emsp;&emsp;获得总秒数：

    TimeCommon.CurrentTimeMillis();//默认从1970年1月1日 0点0分到现在的总时间 输出结果：1564404941408

&emsp;&emsp;阳历转阴历(农历)：
    
    "1994-11-09".ConvertToDateTime(default(DateTime)).ConvertToLunar()；//输出结果：[狗]甲戌1994 十月初七

    "1994-11-09".ConvertToDateTime(default(DateTime)).GetYear()；//输出结果：[狗]甲戌1994 

    "1994-11-09".ConvertToDateTime(default(DateTime)).GetMonth()；//输出结果：十月

    "1994-11-09".ConvertToDateTime(default(DateTime)).GetDay()；//输出结果：初七

    "2019-07-07".ConvertToDateTime(default(DateTime)).GetSolarTerm();//输出结果：小暑

    "2019-01-01".ConvertToDateTime(default(DateTime)).GetHoliday();//输出结果：元旦

    "2019-02-05".ConvertToDateTime(default(DateTime)).GetChinaHoliday();//输出结果：春节

    "2019-02-05".ConvertToDateTime(default(DateTime)).GetLunarYearDate();//输出结果：2019-03-11

    "2019-03-11".ConvertToDateTime(default(DateTime)).GetLunarYearDate();//输出结果：2019-02-05

&emsp;&emsp;获取当前是周几：

     var weekName = Week.GetAll<Week>().Where(x => x.Id == dateStr).Select(x => x.Name);
     Week time = DateTime.Parse("2019-07-29").GetDayName();//输出结果：Week.Monday

     var time = DateTime.Parse("2019-07-29").GetDayName(new[]
    {
        "星期日", "星期一", "星期二", "星期三", "星期四", "星期五", "星期六"
    });//输出结果：星期一

## 验证帮助类

&emsp;&emsp;是否邮政编码：

    "450000".IsZipCode();//输出结果：true

&emsp;&emsp;是否邮箱：

    "wangzhenlei520@gmail.com".IsEmail();//输出结果：true

&emsp;&emsp;是否为手机号：

    "13653777777".IsMobile();//输出结果：true

&emsp;&emsp;是否为固话号：

    "0373-6793210".IsPhone();//输出结果：true

&emsp;&emsp;是否包含数字：

    "123asd".IsNumber();//输出结果：true
    "123".IsNumber();//输出结果：true
    "github".IsNumber();//输出结果：false

&emsp;&emsp;是否为纯数字：

    "13653777777".IsOnlyNumber();//输出结果：true
    "13653777777w".IsOnlyNumber();//输出结果：false
    "a123a".IsOnlyNumber();//输出结果：false
    "github".IsOnlyNumber();//输出结果：false

&emsp;&emsp;是否是身份证号（检测比较严，机器识别）：

    "410782199310069652".IsIdCard();//输出结果：false

&emsp;&emsp;判断是否为Guid：

    "77d99c08-a192-4a16-80dd-5e50f6e1c2d2".IsGuid();//输出结果：true
    "77d99c08-a192-4a16-80dd-5e50f6e1-c2d2".IsGuid();//输出结果：false


&emsp;&emsp;是否为IP：

    "192.168.1.124".IsIp();//输出结果：true
    "a.d.1.124".IsIp();//输出结果：false

&emsp;&emsp;判断是否网址：

    "http://github.com/zhenlei520".IsUrl();//输出结果：true
    "https://github.com/zhenlei520".IsUrl();//输出结果：true
    "github.com/zhenlei520".IsUrl();//输出结果：true
    "百度".IsUrl();//输出结果：false

&emsp;&emsp;判断是否中文：

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

&emsp;&emsp;得到枚举项的描述信息：

    GenderEnum.Boy.GetDescription();//输出结果：男

&emsp;&emsp;判断值是否在枚举中存在：

    1.IsExist(typeof(GenderEnum));//输出结果：true

&emsp;&emsp;得到枚举字典：

    EnumCommon.ToDescriptionDictionary<GenderEnum>();//返回字典类型，其中key为枚举的值，value为枚举的描述  

## 生肖帮助类

&emsp;&emsp;根据年份获取生肖属性：

    AnimalCommon.GetAnimalFromBirthday(1994);//输出结果：狗

&emsp;&emsp;根据年份获取生肖对象：

    var animal=AnimalCommon.GetAnimalEnumFromBirthday(1994);//输出结果：其中animal.Id为10，animal.Name为狗

## 拷贝帮助类

    /// <summary>
    /// 性别
    /// </summary>
    [Serializable]
    public class Person : CloneableClass
    {
        public string Name { get; set; }

        public GenderEnum Gender { get; set; }
    }

&emsp;&emsp;深拷贝（其中必须在Class增加[Serializable]）：

    Person person = new Person
    {
        Name = "小明",
        Gender = GenderEnum.Boy
    };
    var newPerson = person.DeepClone(person);
    newPerson.Name = "小明哥";
    Check.True(person.Name != newPerson.Name, "方法有误");

&emsp;&emsp;浅拷贝（引用地址）：    

    Person person = new Person
    {
        Name = "小明",
        Gender = GenderEnum.Boy
    };
    var newPerson2 = person.ShallowClone<Person>();
    Check.True(person.Name == newPerson2.Name, "方法有误");

## 星座帮助类

&emsp;&emsp;根据日期得到星座名称：

    ConstellationCommon.GetConstellationFromBirthday(DateTime.Parse("1994-11-09"));//输出结果：天蝎座

&emsp;&emsp;根据日期得到星座枚举类：

    ConstellationCommon.GetConstellationEnumFromBirthday(DateTime.Parse("1994-11-09")).Id;//输出结果：8

## 邮箱帮助类

&emsp;&emsp;发送邮件

    EMailCommon.SendEmail(toEmail, title, body, "发送者的邮箱地址", "网络上的代理服务器", "发送邮件的密码", "成功");//输出结果：Status：发送状态，Msg：提示信息

## List帮助类

&emsp;&emsp;List实体添加操作(其中T增加[Serializable])

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

&emsp;&emsp;List实体减法操作(其中T增加[Serializable])

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

&emsp;&emsp; List转String（可帮助去除空格）

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

&emsp;&emsp; 字符串数组集合转String（可帮助去除空格）

    new[]{"小李","","小红"}.ConvertListToString(',', true, true);//输出结果：小李,小红

