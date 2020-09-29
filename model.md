#### Object  

**User**  

1. user_name  (用户名) 
	- String  
2. user_id  (后端生成)  
	- int  
3. password (密码)  
	- String  
4. user_avatar (头像)   
	- url (有默认值)   
5. user_signature (个性签名)  
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

> 是本人`recentProject`才有值,
> 否则`token` 和 `recentProject`没有值  

*Following And Follower*  

| follower_id | following_id |
|-------------|--------------|
| 单元格      | 单元格       |

*User And Token*    

| user_id | token  |
|---------|--------|
| 单元格  | 单元格 |
| 单元格  | 单元格 |


**Project**    

1. project_id  
	- int   
2. project_name (项目名)
	- String   
3. public  (是否公开)  
	- boolean  
4. project_rank (项目等级) 
	- int    
5. user_id  (author作者)  
	- int   
6. create_time  (创建时间)   
	- date(时间戳)  
7. deadline (结束时间)   
	- date  
8. contributors (贡献者)   
	- String  
9. head_id (头节点) 
	- node_id  
10. introduction  (简介)  
	- String  

**Node**  

1. author  (作者)  
	- `user_id` int  
2. node_id (节点id)   
	- int  
2. theme (节点主题)   
	- String  
3. content (节点内容)   
	- long  
4. children (子节点列表)   
	- String 
5. star (点赞数)   
	- 新表  
6. editable (该节点是否可被他人编辑)   
	- boolean  
7. last_edit_user (最后编辑节点的人)   
	- date 
8. last_edit_time (最后编辑节点的时间)   
	- date  
9. nameless (是否匿名) 
	- boolean  

> `children`以逗号分隔   


*User And Star*    

| user_id | node_id |
|:-------:|:-------:|
|  单元格 |  单元格 |
|  单元格 |  单元格 |


UserController  
	- get getUserInfo  
	- post setUserInfo  

UserOpratorController  
	- post chPassword  
	- get star  

AvatarController  
	- post setAvatar  
	- get getAvatar	  

NodeController  
	- post newNode  
	- get getNode  

NodeOpratorController  
	- post chNode  
	- get delNode  

ProjectController  
	- post newProject  
	- get enterProject  
	- delete delProject  

LoginController  
	- post login  

RegisterController  
	- post register  

