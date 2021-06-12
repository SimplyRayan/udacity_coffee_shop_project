
# Coffee Shop
##### this is an app that allow users to access a "virtual" Coffee shop, it has drinks that public users can view, also users with the barista role have the permission to view drink details, and users with the manager role can view, edit, add and delete drinks! the app uses Auth0 for Authentication.


## Running the project

#### 1.Backend
##### first you might want to create a virtual environment, after that you can run the following:  

```
pip install -r requirements.txt
```

 
##### Running the server :  
 ````
$env:FLASK_APP="api"
flask run
 ````
 
 
 
#### 2.Frontend

open 
```./src/environments/environments.ts```
and edit the variables to the your Auth0 configuration
after that run the following
 ````
npm install
ionic serve
 ````
 
## Docs

### Error Handling
##### Error are returned as JSON 
```
{'success':False,

'message':'bad request',

'code':400}
```

#####  Error types:
##### 1. 400 : BAD REQUEST
##### 2. 401 : UNATHOURIZED
#####  3. 403 : FORBIDDEN 
##### 4. 404: RESOURCES NOT FOUND
##### 5. 422:  UNPROCESSABLE REQUEST
##### 6. 500: INTERNAL SERVER ERROR


### ENDPOINTS
#### GET /drinks
##### returns all drinks with a short description
#####  Request Body: None
#####  Request arguments : None
##### Request Sample : `curl http://127.0.0.1:5000/drinks`
##### Response Sample: 
```
{
"drinks":[
	{"id":1,
	"recipe":[
		{
		"color":"blue",
		"parts":1
		}
	 ],
	"title":"water"}
]
,"success":true
}

```

#### GET /drinks-detail
##### returns all drinks with a detailed description 
##### Permission: get:drinks-detail
#####  Request Body: None
#####  Request arguments : `id (required): id of the category`
##### Request Sample : `curl http://127.0.0.1:5000/drinks-detail`
##### Response Sample: 
```
{
"drinks":[
	{"id":1,
	"recipe":[
		{"color":"blue",
		"name":"water",
		"parts":1}
	],
	"title":"water"
	}
],
"success":true}

  
```

#### POST /drinks

##### adding drinks to the menu
##### Permission post:drinks
##### (Required) Request Body: 
```
{
"title":  title[String],
"recipe":  {
	"name":  name [String],
	"color":  color [String],
	"parts":  number of parts [Integer]
	}
}
```
#####  Request arguments : None
##### Request Sample : `curl http://127.0.0.1:5000/drinks-X POST -H "Content-Type: application/json" -d { "title": "Water2", "recipe": { "name": "Water", "color": "blue", "parts": 1 } }`

##### Response Sample: 
```
{
"drinks":  [
	{
	"id":  2,
	"recipe":[
		{
		"color":  "blue",
		"name":  "Water",
		"parts":  1
		}
	],
	"title":  "Water2"
	}
],
"success":  true
}
```

#### PATCH /drinks/{id}
##### editing the drink which has an id: {id}
##### Permission: patch:drinks
#####  (optional keys) Request Body: 
```
{
"title":  title[String],
"recipe":  {
	"name":  name [String ],
	"color":  color [String],
	"parts":  number of parts [Integer]
	}
}
```
#####  Request arguments : None
##### Request Sample :  `curl http://127.0.0.1:5000/drinks/1 -X PATCH -H "Content-Type: application/json" -d {"title":"Cold Water"}`
##### Response Sample: 
```
{
"drink":  [
	{
	"id":  1,
	"recipe":  [
		{
		"color":  "blue",
		"name":  "water",
		"parts":  1
		}
	],
	"title":  "Cold Water"
	}
],
"success":  true
}
```



#### DELETE /drink/{id}
##### delete the specified drink from the menu
##### Permission: delete:drinks
#####  Request Body: None
#####  Request arguments : None
##### Request Sample : `curl http://127.0.0.1:5000/drinks/1 -X DELETE `
##### Response Sample: 
```
{
"delete":  "1",
"success":  true
}
```


## References 
#### [Handling AuthError](https://stackoverflow.com/questions/53285452/internal-server-error-rather-than-raised-autherror-response-from-auth0) 