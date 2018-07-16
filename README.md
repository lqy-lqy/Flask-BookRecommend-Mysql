
------------------------------------------------------------------------------------------------

                                    智能图书推荐系统                        

------------------------------------------------------------------------------------------------


所需运行环境

    使用python3.6作为编程语言。使用mysql作为数据库存储.
    需要安装pandas,flask，pymysql.
    安装方式:
    
    cmd下
    pip install pandas
    pip install flask
    pip install pymysql


项目源码介绍：

20180712

     |
     -|-----data               >这个文件夹中存放数据集，数据集比较杂乱。
     |      |
     |      |-BX-Books.csv     >关于27万条的数据信息，涉及书籍编号，书籍名，书籍作者....
     |      |-BX-Users.csv     >关于27万条的用户信息，涉及用户ID，用户区县，用户省份，用户年龄。
     |      |-Rating1M.csv     >关于100万条的用户对数据的评分数据。涉及用户ID，书籍ID，评分。（评分1-10为标准）|
     |
     |
     |
     -|------CkeanData         >这个文件夹中存放清洗好的数据集，将上面数据清理出需要的数据。
     |      |
     |      |-book.csv         >关于27万条的数据信息，保留书籍编号，书籍名，书籍作者，出版年份。
     |      |-user.csv         >关于27万条的用户信息，保留了用户ID，用户区县，用户省份，用户年龄。
            |                   并且将用户ID,和用户区县作为账号密码用于网站登录。
     |      |-bookrating.csv   >关于100万条的用户对数据的评分数据。保留用户ID，书籍ID，评分。（评分1-10为标准）
     |      |-booktuijian.csv  >关于10个测试用户和对其推荐书籍的信息。涉及用户ID，书籍ID，推荐指数。（评分1-10为标准）
     |
     -|------BookWebAPI.py     >启动这个文件开启服务器。启动方式：在更目录下进入cmd输入    python BookWebAPI.py  
     -|------CleanCSV.py       >清洗原先杂乱的csv文件，保存到cleanData文件夹下面。
     -|------CSVToMysql.py     >将清洗好的文件，即CleanData里面的文件，导入到mysql中。
     |
     -|------CF                >协同过滤1：CF 算法
     -|------slope one         >协同过滤2：slope one 算法
     |
     -|-----其他文件夹          >提供给前端页面和前端页面的依赖


项目思路：

    本项目实现了3个图书推荐功能：
    1 基于书籍的推荐，将书籍按评论平均值排序，将前10个推送给用户。
    2 基于CF（协同过滤）算法的推荐，从登录用户阅读的书籍，寻找具有相同兴趣的用户，并将这些用户阅读的书籍计算求得匹配度。
     按匹配度将前十个推送给用户。
    3 基于slope one 的推荐。slope one讲解：

        用户\商品   商品1 商品2
        用户  1      3     4
        用户  2      4     ？

       从上表中预测用户2对商品2的评分时采用SlopeOne算法计算方式为：R(用户2，商品2) = 4 +（4-3）= 5
      这就是 SlopeOne 推荐的基本原理，它将用户的评分之间的关系看作简单的线性关系：Y = X + b
