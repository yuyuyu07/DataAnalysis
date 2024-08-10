# matplotlib - 折线图

- **折线图**：*可以很直观的反应出数据的变化趋势，反应事物的变化情况*
  - *应用场景：适合二维的大数据集，还适合多个二维数据集的比较*

- **案例**

  - *绘制标普500指数的收盘价的变化*

    ```python
    import numpy as np
    import pandas as pd
    import matplotlib.pyplot as plt
    
    data = pd.read_csv('d:/test_data/spx.csv',index_col='Unnamed: 0',parse_dates=True) #index_col:DataFrame的列用作行索引， parse_dates:解析索引
    
    data.head()
    			SPX
    1990-02-01	328.79
    1990-02-02	330.92
    1990-02-05	331.85
    1990-02-06	329.66
    1990-02-07	333.75
    ```

  - **面向对象画图**

    ```python
    #创建画布
    fig,ax=plt.subplots(figsize=(16,6),dpi=100)
    #准备数据
    x=data.index
    y=data['SPX']
    ax.plot(x,y,color='r')
    plt.show()
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\案例1-1.png)

    *在图中截取2007-2010年金融危机部分*

    ```python
    #截取2007-2011年
    #set_xlim, setylim：设置图表的边界
    
    ax.set_xlim(['2007-1-1','2011-1-1'])
    
    #截取SPX>600
    ax.set_ylim([600,1800])
    
    #添加标题
    ax.set_title('2007-2010年金融危机标普500指数变化趋势')
    
    #添加坐标轴标签
    ax.set_xlabel('Date')
    ax.set_ylabel('SPX')
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\案例1-2.png)

    *在图中添加文字*

    ```python
    # ax.annotate('Peak of bull market',xy=(datetime(2007,10,11),y['2007-10-11']),
               xytext=(datetime(2007,10,11),y['2007-10-11'] + 160),
               arrowprops=dict(facecolor='c'))
    """
    s:字符串，注释文本
    xy：注释的点(x,y)
    xytext:放置文本的位置(x,y)
    arrowprops:在xy和xytext之间绘制箭头的属性(字典)
    """
    
    crisis_date = [
        (datetime(2007,10,11),'Peak of bull market'),
        (datetime(2008,3,12),'Bear Stearns Fails'),
        (datetime(2008,9,15),'Lehman Bankruptcy')
    ]
    
    for date,label in crisis_date:
        ax.annotate(label,xy=(date,y[date]),xytext=(date,y[date]+160),
                   arrowprops=dict(facecolor='c'))
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\案例1-3.png)

    *关于annotate更多请参考：*

    *https://matplotlib.org/api/_as_gen/matplotlib.pyplot.annotate.html*

    *https://matplotlib.org/users/annotations_intro.html*

    *在这里我们另外补充了面向对象画图的另外几个功能*

  - **Dataframe画图**

    *在前面我们都是直接使用 matplotlib进行绘图，我们的pandas集成了matplotlib画图的方法，我们也可以还有 pandas直接进行绘制*

    ```python
    import numpy as np
    import pandas as pd
    import matplotlib.pyplot as plt
    from datetime import datetime
    
    data = pd.read_csv('d:/test_data/spx.csv',index_col='Unnamed: 0',parse_dates=True)
    
    data.plot(figsize=(16,6),color='r',
              xlim=['2007-1-1','2011-1-1'],
              ylim =[600,1800],
             title='2007-2010年金融危机标普500指数变化趋势'
             )
    #plt.xlim(['2007-1-1','2011-1-1'])
    #plt.ylim([600,1800])
    plt.xlabel('Date')
    plt.ylabel('SPX')
    
    crisis_date = [
        (datetime(2007,10,11),'Peak of bull market'),
        (datetime(2008,3,12),'Bear Stearns Fails'),
        (datetime(2008,9,15),'Lehman Bankruptcy')
    ]
    for date,label in crisis_date:
        plt.annotate(label,xy=(date,y[date]),xytext=(date,y[date]+160),
                   arrowprops=dict(facecolor='c'))
    plt.show()
    
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\dateframe1.png)

  - *我们使用dataframe画图，当不能满足于我们的需求时，可以和 plt方法，或者面向画图方法结合使用*






