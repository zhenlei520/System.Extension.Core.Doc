<a href="https://github.com/zhenlei520/System.Extension.Core.Doc/tree/2.0/README.md">回到目录</a>

### List实体添加操作：

        List<int>list1=new List<int>(){1,2};
        List<int>list2=new List<int>(){1,3};
        List<int>result=new List<int>();

        result = ListCommon.Add<int>(list1,list2,false);
        或者简写为
        result = list1.Add<int>(list2,true);//其中true代表是查重,其结果为1,2,3

### 得到新增的集合以及被删除的集合

        List<int>list1=new List<int>(){1,2};
        List<int>list2=new List<int>(){1,3};
        ListCommon.ConvertToCheckData<int>(list1,list2,out List<int> newAddList,out List<int>delList,out List<int> alwayList);//其中newList为{3},delList为{1}，alwayList为{1}

### List转换为string（其中支持的类型为值类型以及string）
        List<int>list1=new List<int>(){1,2};
        ListCommon.ConvertListToString(list1,',',true,true);//其中,为分割字符串，第三个参数true为是否移除null或者空字符串，第四个参数为是否去除空格
        或者简写为
        list1.ConvertListToString(',',true,true);

### string数组转换为string
        string[]strList=new []{"张三","李四"};
        strList.ConvertListToString(',',true,true);

### 对List集合分页
        1、常规用法
        
        int pageIndex=1;
        int pageSize=20;
        bool isTotal=true;//是否计算总数
        PageData<T> pageData = ICollection<T>.ListPager(pageIndex,pageSize,isTotal);//分页数据

        输出结构为：
        {
            total:0,
            data:[]
        }

        2、对集合列表分页执行：
        例如：

        其中：
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

        List<User> userList = new List<User>()
            {
                new User()
                {
                    Name = "小王",
                    Age = 10
                },
                new User()
                {
                    Name = "小李",
                    Age = 18
                },
                new User()
                {
                    Name = "小赵",
                    Age = 12
                }
            };
            userList.ListPager(list =>
            {
                userList.ForEach(user => { Console.WriteLine($"我的名字是{user.Name}"); });
                Console.WriteLine($"共有{list.Count}条记录");
            }, 2, 1);
            //输出结果为：
            我的名字是小王
            我的名字是小李
            共有2条记录
            我的名字是小赵
            共有1条记录

### 移除单条符合条件的数据
        List<int>userIdList=new List<int>(){1,2};
        List<int> result=userIdList.RemoveNew(x=>x==1);//移除1，结果为{2}

### 移除多条符合条件的数据
        List<int>userIdList=new List<int>(){1,2,3};
        List<int> result=userIdList.RemoveNew(x=>x>1);//移除2,3，结果为{1}

        

