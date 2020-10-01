#### Object  

```mysql
create database if not exists ms character set utf8;
```

**User**  

1. name (用户名) 
	- String  
2. id  (后端生成)  
	- int  
3. password (密码)  
	- String  
4. userAvatar (头像)   
	- url (有默认值)   
5. userSignature (个性签名)  
	- String  
6. following (关注人)   
	- 新表  
7. follower  (被谁关注)   
	- 新表  
8. exp  (经验值)   
	- int  
9. recentProject (最近浏览过的项目)  
	- String 可以是null  
10. token (单独一张表)  (设备码)   
	- int 可以是null   

```mysql
create table user (
	id int primary key,
	name varchar(20) not null,
	password long not null,
	userAvatar long default 'default.png',
	userSignature varchar(32) default '这家伙很懒,什么也没留下!',
	exp int default 0,
	token int 
);
```

> 是本人`recentProject`才有值,
> 否则`token` 和 `recentProject`没有值  

*Following And Follower*  

| follower_id | following_id |
|-------------|--------------|
| 单元格      | 单元格       |

```mysql
create table follow (
	follower_id int not null,
	following_id int not null
);
```

*RecentProject*  

| user_id | project_id |
|---------|------------|
| 单元格  | 单元格     |
| 单元格  | 单元格     |

```mysql
create table recent_project(
	user_id int not null,
	project_id int null 
);
```
**Project**    

1. id  
	- int   
2. name (项目名)
	- String   
3. isPublic  (是否公开)  
	- boolean  
4. rank (项目等级) 
	- int    
5. author  (author作者)  
	- int   
6. createTime (创建时间)   
	- date(时间戳)  
7. ddl (结束时间)   
	- date  
8. contributors (贡献者)   
	- 新表
9. headNodeId (头节点) 
	- node_id  
10. introduction  (简介)  
	- String  

```mysql
create table project (
	id int primary key,
	name varchar(64) not null,
	isPublic boolean not null,
	rank int not null default 0,
	author int not null,
	introduction long,
	headNodeId int not null,
	createTime date,
	ddl date
);
```

| project_id | contributor_id |
|------------|----------------|
| 单元格     | 单元格         |
| 单元格     | 单元格         |


```mysql  
create table contributor(
	project_id int not null,
	contributor_id int not null
);
```
**Node**  

1. author  (作者)  
	- `user_id` int  
2. id (节点id)   
	- int  
2. theme (节点主题)   
	- String  
3. content (节点内容)   
	- long  
4. parent_id (子节点列表)   
	- int   
5. star (点赞数)   
	- 新表  
6. editable (该节点是否可被他人编辑)   
	- boolean  
7. lastEditId (最后编辑节点的人)   
	- date 
8. lastEditTime (最后编辑节点的时间)   
	- date  
9. nameless (是否匿名) 
	- boolean  

> `children`以逗号分隔   

```mysql  
create table node(
	id int primary key,
	author int not null,
	parent_id int,
	theme varchar(64) not null,
	content long not null,
	editable boolean not null,
	nameless boolean not null,
	lastEditId int not null,
	lastEditTime timestamp
);
```

*User And Star*    

| user_id | node_id |
|:-------:|:-------:|
|  单元格 |  单元格 |
|  单元格 |  单元格 |

```mysql
create table star(
	user_id int not null,
	node_id int not null
);
```
