<a href="https://github.com/zhenlei520/System.Extension.Core.Doc/tree/2.0/README.md">回到目录</a>

### 
    public enum Gender
    {
        /// <summary>
        /// 男
        /// </summary>
        [Description("boy")] Boy = 1,
        /// <summary>
        /// 女
        /// </summary>
        [Description("gril")] Gril = 2,
    }

### 得到枚举字典（key对应枚举的值，value对应枚举的注释）：

        Dictionary<int, string> result=EnumCommon.ToDescriptionDictionary<Gender>();//key对应枚举的值，value对应枚举的注释 key为1，value为boy。key为2，value为gril

        Dictionary<int, string> result=EnumCommon.ToDictionary<Gender>();//key与value与字典值一致。//key为1，value为1,。key为2，value为2.

        EnumCommon.GetDescription(Gender.Boy);
        或者简写为
        Gender.Boy.GetDescription();//输出结果：boy

        2.IsExist(typeof(Gender));//输出结果为false
        1.IsExist(typeof(Gender));//输出结果为true

        
