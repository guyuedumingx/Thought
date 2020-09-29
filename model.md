#### Object  

**User**  

1. user_name  
	- String  
2. user_id  (后端生成)  
	- int  
3. password   
	- String  
4. user_avatar (头像)   
	- url (有默认值)   
5. user_signature (个性签名)  
	- String  
6. following    
	- 新表  
7. follower   
	- 新表  
8. exp  (经验值)   
	- int  
9. recentProject 
	- String 可以是null  
10. token (单独一张表)   
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
2. project_name  
	- String   
3. public  
	- boolean  
4. project_rank  
	- int    
5. user_id  (author)  
	- int   
6. create_time   
	- date(时间戳)  
7. deadline  

**Node**  

1. author  
	- `user_id` int  
2. node_id  
	- int  
2. theme  
	- String  
3. content  
	- long  
4. children  
	- String 
5. star  
	- 新表  
6. editable  
	- boolean  
7. last_edit_user  
	- date 
8. last_edit_time  
	- date  
9. nameless  
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
	- get login  
	- post register  

