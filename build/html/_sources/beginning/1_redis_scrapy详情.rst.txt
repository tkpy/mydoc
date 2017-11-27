redis-scrapy详情
======================

Item Pipeline:
	引擎将(Spider返回的)爬取到的Item给Item Pipeline , scrapy-redis 的Item Pipeline将爬取到的Item存入redis的item queue

	修改Item Pipeline可以很方便的根据key从items queue 提取item , 从而实现items proceses集群


redis 数据库 , 不负责爬取 , 只负责url指纹判重 , Request的分配 , 以及数据的存储

	scrapy-redis 调度任务是Request对象 , 里面信息量比较大(包含url,callbase函数,headers等信息) , 导致结果降低爬虫速度 ,占中  
    大量redis空间 , 想保证效率 , 需要硬件水平


#分布式搭建

	1.先安装redis
	redis-cli  如果后面有ip地址 , 就是目标的数据库 , 没有ip就是本地的数据库
	
	keys *  #显示所有的键
	set 键 值 #设置一个值
	get 键 值 #获取值

直接拿官方给的例子修改

	#启动所有slaver端爬虫的指令 , 下面的格式时参考格式 , 建议采用这种格式
	redis_key = '爬虫类名(myspider)(最好是,可以随便写):start_urls'

	#发送指令
	lpush myspider:start_urls 域名(http://xxxxx/)


#和allowd_domain = ["dmoz.org"] 等效 , 指定爬取范围 , 都可以使用

#动态获取爬取范围
::

	def __init__(self,*args,**kwargs):
	
		domain = kwargs.pop('domain',"")
		self.allowed_domains = filter(None,domain.split(','))
		#修改下面的代码 , 动态获取爬取范围
		super(当前文件的第一个类名,self).__init__(*args,**kwargs)


#删除所有redis键

//删除当前数据库中的所有key
flushdb
//删除所有数据库中的key
flushall


在服务器中使用后台运行 info.log 日志
nohup python3 main.py >info.log &

htop  查看后台运行进程





scrapy   参考文件: http://scrapy-chs.readthedocs.io/zh_CN/0.24/topics/settings.html
