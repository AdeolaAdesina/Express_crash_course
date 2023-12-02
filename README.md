# Express_crash_course


## Basic Setup


Run to set up a package.json in your new folder.

```
npm init -y
```

This is where we're going to install all our different libraries.

```
npm i express
```

Install express

Then install nodemon as a dev dependency:

```
npm i --save-dev nodemon
```

Then setup the scripts of the package.json to be:

```
"scripts": {
    "dev": "nodemon server.js"
  },
```

Then create the server.js file.

Now ```npm run dev``` should start the server.


## Create our Express server

```
const express = require('express')

//then setup server
const app = express()

//then we pass it a port number
app.listen(3000)
```

Now we have our app running on localhost:3000

![Screenshot_129](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/16dd9191-7215-40cb-a85d-a4a7083186d2)

All it's saying is that our application doesn't have any route setup.


## Basic Routing

Now we want to set up routes by using app.get or app.post, app.delete, app.put, app.patch or any http request.

The first parameter is a path, the a callback function.

The function can take three different parameters. Req, Res and Next.

```
const express = require('express')

//then setup server
const app = express()

app.get('/', (req, res) => {
    console.log("Here");
    res.send("Hi");
})

//then we pass it a port number
app.listen(3000)
```

If we refresh, we can see we've sent a string to the homepage.

![Screenshot_130](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/fb22d92d-1006-44a7-becc-98b6f4673199)



## Sending Data.


Res.send is not something we're going to use very often.

We can use sendStatus to send a status code.


```
const express = require('express')

//then setup server
const app = express()

app.get('/', (req, res) => {
    console.log("Here");
    res.sendStatus(500);
})

//then we pass it a port number
app.listen(3000)
```


![Screenshot_131](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/6a478e1d-38fb-4e20-aee3-07c59b225087)



We can just send a message instead of status code.

```
const express = require('express')

//then setup server
const app = express()

app.get('/', (req, res) => {
    console.log("Here");
    res.status(500).send("Hi");
})

//then we pass it a port number
app.listen(3000)
```


![Screenshot_132](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/aa48a429-b5e8-45bf-a51a-8220cd786c75)


But if we inspect, we'll see the error.

We can also send it a json message.


```
const express = require('express')

//then setup server
const app = express()

app.get('/', (req, res) => {
    console.log("Here");
    res.status(500).json({ message: "Error"});
})

//then we pass it a port number
app.listen(3000)
```


![Screenshot_133](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/1e9960ca-cccd-4efa-b99e-6bc0c13b9a0a)


We can also do:

```
app.get('/', (req, res) => {
    console.log("Here");
    res.json({ message: "Error"});
})
```


You could also send down a file for the user to download 


```
const express = require('express')

//then setup server
const app = express()

app.get('/', (req, res) => {
    console.log("Here");
    res.download("server.js")
})

//then we pass it a port number
app.listen(3000)
```


![Screenshot_134](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/41d3b5e9-3aee-49d2-9182-d58a242fffe4)


When you refresh, it will download the server.js file.


Another thing we can do with response is rendering HTML, which is what we'll be doing most of the time.

Either rendering some HTML or sending some json.




## Rendering HTML.


We use the render method and pass it the path of the file you want to render.



```
const express = require('express');
const { render } = require('express/lib/response');

//then setup server
const app = express()

app.get('/', (req, res) => {
    console.log("Here");
    res.render('index')
})

//then we pass it a port number
app.listen(3000)
```

Now we need to tell our app where our index file it, we put them in a view folder


views/index.html:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    Hello
</body>
</html>
```


![Screenshot_135](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/bd190b3a-eb79-42e1-abb1-8eeeb9208494)


This error is because we don't have a view engine set up.

We'll be using ejs as our view engine.

So we'll close our server and install ejs.

```
npm i ejs
```

Then we'll tell our application to use that view engine in server.js:

```
const express = require('express');
const { render } = require('express/lib/response');
//then setup server
const app = express()

app.set('view engine', 'ejs')

app.get('/', (req, res) => {
    console.log("Here");
    res.render('index')
})

//then we pass it a port number
app.listen(3000)
```

Then you need to rename your index.html to index.ejs

You can install ejs language support in VScode.


Now if we restart our server.


![Screenshot_136](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/1875af0b-4060-456b-bada-aa44eec0e654)


You can pass information from your server into your views.

In server.js:

```
app.get('/', (req, res) => {
    console.log("Here");
    res.render('index', { text: 'World'})
})
```

Then we access it inside index.ejs:

```
<body>
    Hello <%= text %>
</body>
```


![Screenshot_137](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/12016b74-7132-4be5-abf4-361d8cfba5b0)




## Routers

Let's create two simple routes.

```
const express = require('express');
const { render } = require('express/lib/response');
//then setup server
const app = express()

app.set('view engine', 'ejs')

app.get('/', (req, res) => {
    console.log("Here");
    res.render('index', { text: 'World'})
})

app.get('/users', (req, res) => {
    res.send('User List')
})

app.get('/users/new', (req, res) => {
    res.send('User New Form')
})

//then we pass it a port number
app.listen(3000)
```

![Screenshot_138](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/10a4d9d1-c45e-4567-97f7-9be906fe267a)

![Screenshot_139](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/20b6c633-df47-4605-8a8f-6c411d873bd1)


But it will make more sense if we take the code related to users and out that in it's own file. Then import it into server.js.

We create a folder called routes, and a file called users.js.

Router works exactly the same as app. It has .get, .put, .patch, .delete.

We can also nest it inside a parent route. So we'll have / not /users.

Then we'll export and import it into server.js.

Then we'll use app.use


routes/user.js:

```
const express = require('express')
const router = express.Router()

router.get('/', (req, res) => {
    res.send('User List')
})

router.get('/new', (req, res) => {
    res.send('User New Form')
})

module.exports = router
```


server.js:

```
const express = require('express');
const { render } = require('express/lib/response');
//then setup server
const app = express()

app.set('view engine', 'ejs')

app.get('/', (req, res) => {
    console.log("Here");
    res.render('index', { text: 'World'})
})

const userRouter = require('./routes/users')

app.use('/users', userRouter)

//then we pass it a port number
app.listen(3000)
```

Run the code to find that it still works.

![Screenshot_138](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/36df1e76-50fd-4905-856b-e76678aec75b)

![Screenshot_139](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/6733d13f-2a67-4fe5-800f-ee15ec522c32)



## Advanced Routing

We can clean up how our routes are going to look.


What if we want to create a form for a new user. So we'll use a post method.

```
const express = require('express')
const router = express.Router()

router.get('/', (req, res) => {
    res.send('User List')
})

router.get('/new', (req, res) => {
    res.send('User New Form')
})

router.post('/', (req, res) => {
    res.send('Create User')
})

module.exports = router
```

Then we want to access an individual user based on the id of that user.

```
const express = require('express')
const router = express.Router()

router.get('/', (req, res) => {
    res.send('User List')
})

router.get('/new', (req, res) => {
    res.send('User New Form')
})

router.post('/', (req, res) => {
    res.send('Create User')
})

router.get('/:id', (req, res) => {
    //req.params.id
    res.send(`Get User with ID ${req.params.id}`)
})

module.exports = router
```


![Screenshot_140](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/364df2f2-0189-4cbc-a9dc-a9ce7de45a24)


It pulls the number directly from the URL.


Also because express runs from top to bottom, if you arrange your code like this:

```
const express = require('express')
const router = express.Router()

router.get('/', (req, res) => {
    res.send('User List')
})

router.post('/', (req, res) => {
    res.send('Create User')
})

router.get('/:id', (req, res) => {
    req.params.id
    res.send(`Get User with ID ${req.params.id}`)
})

router.get('/new', (req, res) => {
    res.send('User New Form')
})

module.exports = router
```


If we now call /new in the browser, we'll get this.

![Screenshot_141](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/2b137d34-2a14-47ee-8d60-bd5d5c38543c)


We were supposed to get the screen with "User New Form"

So make sure you put your /new above your dynamic routes.


Now let's also create a put route and a delete method for our dynamic route.


```
const express = require('express')
const router = express.Router()

router.get('/', (req, res) => {
    res.send('User List')
})

router.get('/new', (req, res) => {
    res.send('User New Form')
})

router.post('/', (req, res) => {
    res.send('Create User')
})

router.get('/:id', (req, res) => {
    req.params.id
    res.send(`Get User with ID ${req.params.id}`)
})

router.put('/:id', (req, res) => {
    res.send(`Update User with ID ${req.params.id}`)
})

router.delete('/:id', (req, res) => {
    res.send(`Delete User with ID ${req.params.id}`)
})

module.exports = router
```


Then we can remodel it to look like this:

```
const express = require('express')
const router = express.Router()

router.get('/', (req, res) => {
    res.send('User List')
})

router.get('/new', (req, res) => {
    res.send('User New Form')
})

router.post('/', (req, res) => {
    res.send('Create User')
})

router.route('/:id').get((req, res) => {
    res.send(`Get User with ID ${req.params.id}`)
}).put((req, res) => {
    res.send(`Update User with ID ${req.params.id}`)
}).delete((req, res) => {
    res.send(`Delete User with ID ${req.params.id}`)
})


module.exports = router
```

So we have a get, put and delete method for the /:id route.



Now let's talk about something related to param. the router.param function.

The function is going to run any time it finds a param that matches the name you pass in.


```
const express = require('express')
const router = express.Router()

router.get('/', (req, res) => {
    res.send('User List')
})

router.get('/new', (req, res) => {
    res.send('User New Form')
})

router.post('/', (req, res) => {
    res.send('Create User')
})

router.route('/:id').get((req, res) => {
    res.send(`Get User with ID ${req.params.id}`)
}).put((req, res) => {
    res.send(`Update User with ID ${req.params.id}`)
}).delete((req, res) => {
    res.send(`Delete User with ID ${req.params.id}`)
})

router.param("id", (req, res, next, id) => {
    console.log(id);
}) 

module.exports = router
```

If we run the code, you will find the id logged to the console.

![Screenshot_142](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/f340e1c3-64d4-489d-9422-e44738f550ac)

![Screenshot_143](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/53267a84-8117-4c83-a0fb-8f582e9120a4)


But you will see the browser loading continously.

It loads because we need to call the next function. Because param is a type of middleware.

Middleware is the thing that runs between request and response.

Now refreshing works.

Now instead of logging the ID, i want to get the user with that ID.


```
const express = require('express')
const router = express.Router()

router.get('/', (req, res) => {
    res.send('User List')
})

router.get('/new', (req, res) => {
    res.send('User New Form')
})

router.post('/', (req, res) => {
    res.send('Create User')
})

router.route('/:id').get((req, res) => {
    console.log(req.user)
    res.send(`Get User with ID ${req.params.id}`)
}).put((req, res) => {
    res.send(`Update User with ID ${req.params.id}`)
}).delete((req, res) => {
    res.send(`Delete User with ID ${req.params.id}`)
})

const users = [{ name: "Kyle" }, { name: "Sally"} ]

router.param("id", (req, res, next, id) => {
    req.user = users[id]
    next()
}) 

module.exports = router
```

If we run http://localhost:3000/users/1

We see:

![Screenshot_144](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/bd20750a-0c34-471a-9208-f861e85161e3)




## Middleware

SO let's create a middleware for logging out something

Let's create a function for logger. 

THen we use the middleware by calling app.use:

server.js:

```
const express = require('express');
const { render } = require('express/lib/response');
//then setup server
const app = express()

app.set('view engine', 'ejs')
app.use(logger)

app.get('/', (req, res) => {
    console.log("Here");
    res.render('index', { text: 'World'})
})

const userRouter = require('./routes/users')

function logger(req, res, next) {
    console.log(req.originalUrl)
    next()
}

app.use('/users', userRouter)

//then we pass it a port number
app.listen(3000)
```


If we refresh we will see the URL

![Screenshot_145](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/9b3da89c-cacd-45da-8f0b-55958f4ad11b)


If we move app.use(logger) down and we run the homw URL, it won't log the URL because everything runs top to bottom.

We can also pass our logger into app.get

```
const express = require('express');
const { render } = require('express/lib/response');
//then setup server
const app = express()

app.set('view engine', 'ejs')

app.get('/', logger, (req, res) => {
    console.log("Here");
    res.render('index', { text: 'World'})
})

const userRouter = require('./routes/users')

function logger(req, res, next) {
    console.log(req.originalUrl)
    next()
}

app.use('/users', userRouter)

//then we pass it a port number
app.listen(3000)
```


Because the logger is inside the / route, it will only log on this route.

![Screenshot_146](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/bb8e5afc-c828-4ad2-9a0f-462cf1b59f23)

![Screenshot_147](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/dff7ee73-9c80-4b23-9563-2c1bee0e236d)

![Screenshot_148](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/3349813f-34c3-4567-bf43-3d92997f5c18)

And we can put more than one middleware in there:

```
const express = require('express');
const { render } = require('express/lib/response');
//then setup server
const app = express()

app.set('view engine', 'ejs')

app.get('/', logger, logger, logger, (req, res) => {
    console.log("Here");
    res.render('index', { text: 'World'})
})

const userRouter = require('./routes/users')

function logger(req, res, next) {
    console.log(req.originalUrl)
    next()
}

app.use('/users', userRouter)

//then we pass it a port number
app.listen(3000)
```

![Screenshot_149](https://github.com/AdeolaAdesina/Express_crash_course/assets/29931071/7cd3e4a1-4545-4213-abc2-b9ec2336dcb5)




