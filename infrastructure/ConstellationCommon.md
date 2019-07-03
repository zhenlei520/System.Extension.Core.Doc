<a href="https://github.com/zhenlei520/System.Extension.Core.Doc/tree/2.0/README.md">回到目录</a>

### 根据日期得到星座名称：

        DateTime dateTime=DateTime.Parse("1994-11-09");
        ConstellationCommon.GetConstellationFromBirthday(dateTime);//输出结果为：天蝎座
        ConstellationCommon.GetConstellationFromBirthday(null);//输出结果为：未知

        ConstellationCommon.GetConstellationEnumFromBirthday(dateTime);//输出结果为：ConstellationEnum.Scorpio
