---
title: faker_data
date: 2019-10-11 05:04:21
tags: 
	- 姿势
	- faker
	- 造数据
	- 存数据
categories: 
	- 随笔
---
###造数据
#####生成假数据的第三方库---faker
- 官方文档:[https://faker.readthedocs.io/en/master/](https://faker.readthedocs.io/en/master/ "faker")
- 如果有其他需求请参阅官方文档,我只用到了少部分功能
  1.  生成个人信息数据  
	`from faker import Faker`   
	`fake = Faker(locale='zh_CN')`           
	`print(fake.simple_profile())`
	 -  这个时候会发现生成了中文的个人信息,如果想要生成其他语言可以参见文档
  2. 生成文章数据
 	`"title": fake.text(max_nb_chars=5)`
	`"author": fake.name()`
	`"rel_time": fake.date()`
	`"contect": fake.text(max_nb_chars=20000)`
	 - 文章数据一般包含标题,作者,发布时间,文章内容,(max_nb_chars限定最大长度)
###存数据
#####将数据存到mongodb的第三方库---pymongo
#####mongodb安装:
	略[windows系统一路next(最后一步将安装可视化工具的勾取消),linux可以使用docker]
#####使用pymongo连接mongodb:
	配置数据库信息
	client = pymongo.MongoClient('localhost', 27017)
	mydb = client['faker_data']
	musictop = mydb['article']
	解释:
	1. localhost: 数据库所在服务器ip
	2. 27017: 默认端口
	3. faker_data:新建的数据库
	4. article: 集合,不需要新建,插入时自动创建.如果新建了则需要插入一条数据才能看见
#####将数据存入mongodb
	def save_url_to_Mongo(data):
    	try:
        	musictop.insert_one(data)
        	print("存储到MongoDb成功")
    	except Exception as e:
        	print('存储到MongoDb失败', e)

#####多线程写入
	不咋几把会,待添加

