In this post we will learn how to make CRUD rest api in node js from scratch without using any frameworks such as Express,Oak,etc 😍.We will use basic node http package to build it .

# 🔥 Get Up And Running With Server
Firstly we will import http package from node js. Then we will call `createServer()` method in it which will give us an instance of `http.Server` class.After that we will call `listen()` method on that `http.Server` class instance which will starts the HTTP server listening for connections 😉.
```js
const http = require('http');
const server = http.createServer();
const PORT = process.env.PORT || 5000;
server.listen(PORT, () => console.log(`Server listening on port ${PORT}!!!`));
```
## About http.createServer()
`http.createServer()` takes a parameter `requestListener` which is optional.The HTTP Server object can listen to ports on your computer and execute a function, a requestListener, each time a request is made.This `requestListener` handles request from the user, as well as response back to the user. In this `requestListener` we will have access to request and response parameters. Inside this function we will check the `req.url` and `req.method` of each incoming request and then conditionally do some business logic will return  desired response  back to the user ✨ . 

# 🥳 Lets build CRUD based rest api
 Enough of theory , now lets discuss how we can build a simple CRUD api to manage Todos.[This](https://github.com/satishnaikawadi2011/post-node-rest-api-without-framework) is the link to github repository where you will get the completed source code. In this you will need two files
which are `data.js` and `todoController.js`. In `todo.js` you will find dummy data used for this tutorial. Because I don't want to make things complex by adding databases and all that stuff for the sake of this tutorial. In `todoController.js` you will find some functions which we can perform on this data e.g. find todo by its id or get all todos like that. You are free to go through these two files.\
We are going to have five routes to manage todos.
- url:`/api/todos` and method:`GET`  - route to fetch all todos. 
- url:`/api/todos/:id` and method:`GET`  -  route to fetch a todo by its id.
- url:`/api/todos/:id` and method:`PATCH`  - route to update a todo by its id.
- url:`/api/todos/:id` and method:`DELETE`  - route to delete a todo by its id.
- url:`/api/todos/:` and method:`POST`  - route to create a new todo.

Before writing any routes , we need to understand two methods present on `res` parameter of `requestListener`.
1. `writeHead()` -  This method sends an HTTP status code and a collection of response headers back to the client. The status code is used to indicate the result of the request. For example, everyone has encountered a 404 error before, indicating that a page could not be found. The example server returns the code 200, which indicates success.
2. `end()` -  This method signals to the server that all of the response headers and body have been sent; that server should consider this message complete. The method, response.end(), MUST be called on each response. In this method we will pass our data which we wanted to return back to user as response.

### (1) route to fetch all todos.
Firstly , we will check if the `url` and `method` of incoming request is `/api/todos` and `GET` respectively.If it is the case then we will fetch all todos from `data.js` with the help of `todoController.js` and then if all goes well then we will set the status code as 200 which indicates that the request has been succesful. Here , we will also set the header as `Content-Type : application/json` which tells the client that the content type of the returned content  is JSON format.We are going to set this header in every route and in each request we are going to convert our data to JSON string.Then if `url` or `method` of incoming request does not match , then we will set the status code as 404 which indicates NOT FOUND and we will send message that route not found as response.
```js
const server = http.createServer(async (req, res) => {
	if (req.url === '/api/todos' && req.method === 'GET') {
		const todos = await Todo.findAll();
		res.writeHead(200, { 'Content-Type': 'application/json' });
		res.end(JSON.stringify(todos));
	}	else {
		res.writeHead(404, { 'Content-Type': 'application/json' });
		res.end(JSON.stringify({ message: 'Route not found!' }));
	}
});
```

For testing API during development you can use any client as you wish. I prefer Postman for testing my APIs. You can get it [here](https://www.postman.com/downloads/) for any platform.\
![get-all.jpg](https://res.cloudinary.com/dh1srz69c/image/upload/v1614871254/get_all_6674ba48e6.jpg)

### (2) route to fetch a todo by its id
For this route also our procedure will be same. Only difference will be instead of fetching all todos we will fetch a single todo and return back response. In this route we will have a dynamic parameter id which will be passed into route itself and depend on which we will fetch particular todo.
```js
if (req.url.match(/\/api\/todos\/([a-z A-Z 0-9]+)/) && req.method === 'GET') {
		try {
			const id = req.url.split('/')[3];
			const todo = await Todo.findById(id);
			res.writeHead(200, { 'Content-Type': 'application/json' });
			res.end(JSON.stringify(todo));
		} catch (error) {
			res.writeHead(404, { 'Content-Type': 'application/json' });
			res.end(JSON.stringify({ message: 'Todo not found!' }));
		}
	}
```
After testing we will get response like\
![get-one.jpg](https://res.cloudinary.com/dh1srz69c/image/upload/v1614872040/get_one_444aa15017.jpg)

### (3) route to delete a todo by its id
In this route firstly , we will check if the `req.method` is `DELETE`\
This route will be same as above route the only difference will be instead of fetching by id ,we will delete a todo by its id and send message as response to user.
```js
if (req.url.match(/\/api\/todos\/([a-z A-Z 0-9]+)/) && req.method === 'DELETE') {
		try {
			const id = req.url.split('/')[3];
			await Todo.deleteById(id);
			res.writeHead(200, { 'Content-Type': 'application/json' });
			res.end(JSON.stringify({ message: 'Todo deleted successfully!!!' }));
		} catch (error) {
			console.log(error);
			res.writeHead(404, { 'Content-Type': 'application/json' });
			res.end(JSON.stringify({ message: 'Todo not found!' }));
		}
	}
```
After testing it in Postman
![delete-one.jpg](https://res.cloudinary.com/dh1srz69c/image/upload/v1614872464/delete_one_482f13e789.jpg)

### (4) route to create a new todo
In this route firstly , we will check if the `req.method` is `POST`\
To create route for a new todo , we will first need to understand how can we get access to request body data. The `request` object passed in the connection callback i.e `requestListener` is a stream. So, we must listen for the body content to be processed, and it's processed in chunks.
We first get the `data` by listening to the stream data events, and when the data ends, the stream `end` event is called, once: So to access the data, assuming we expect to receive a string, we must concatenate the chunks into a string when listening to the stream `data`, and when the stream `end`, we parse the string to JSON: So we will write a utility function to get request body data.
```js
// utils.js
function getPostData(req) {
	return new Promise((resolve, reject) => {
		try {
			let body = '';
			req.on('data', (chunk) => {
				body += chunk.toString();
			});
			req.on('end', () => {
				resolve(body);
			});
		} catch (error) {
			reject(error);
		}
	});
}

module.exports = { getPostData };
```
After getting this request body data from `getPostData()` function we will parse it by using `JSON.parse()` and with that data we will create a new todo
```js
if (req.url === '/api/todos' && req.method === 'POST') {
		const body = await getPostData(req);
		const { title, description } = JSON.parse(body);
		const newTodo = await Todo.create({ title, description });
		res.writeHead(201, { 'Content-Type': 'application/json' });
		res.end(JSON.stringify(newTodo));
	}
	else {
		res.writeHead(404, { 'Content-Type': 'application/json' });
		res.end(JSON.stringify({ message: 'Route not found!' }));
	}
```
Testing this route in Postman
![create.jpg](https://res.cloudinary.com/dh1srz69c/image/upload/v1614877987/create_0fd6d997d6.jpg)
 
### (5) route to update a todo by its id
In this route firstly , we will check if the `req.method` is `PATCH`\
Then we will get the  request body data from `getPostData()` function and then  we will parse it by using `JSON.parse()` and with that data we will update a particular todo which has given id.
```js
if (req.url.match(/\/api\/todos\/([a-z A-Z 0-9]+)/) && req.method === 'PATCH') {
		try {
			const body = await getPostData(req);
			const id = req.url.split('/')[3];
			const updatedTodo = await Todo.updateById(id, JSON.parse(body));
			res.writeHead(200, { 'Content-Type': 'application/json' });
			res.end(JSON.stringify(updatedTodo));
		} catch (error) {
			console.log(error);
			res.writeHead(404, { 'Content-Type': 'application/json' });
			res.end(JSON.stringify({ message: 'Todo not found!' }));
		}
	}
```
Testing in Postman \
![update.jpg](https://res.cloudinary.com/dh1srz69c/image/upload/v1614880317/update_d4da8a5e9a.jpg)

And this is it for this article.I hope all of you understand at least to some extent what I explained in this post 😇. If any one has queries feel free to contact me through my mail.