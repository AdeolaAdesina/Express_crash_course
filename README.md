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


