<a href="https://github.com/zhenlei520/System.Extension.Core.Doc/tree/2.0/README.md">回到目录</a>

### 字符串扩展

&emsp;&emsp;字符串转换为泛型集合：

		"1,2".ConvertStrToList<int>(',');//默认分隔符为,


&emsp;&emsp;隐藏手机号码：

        StringCommon.HideMobile("13653487541");//136****7541

&emsp;&emsp;加密隐藏信息（将原信息其中一部分数据替换为特殊字符）：

        StringCommon.EncryptStr("13653487541","*",3,4);//136****7541