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

    "450000".IsZipCode();//输出结果：true
