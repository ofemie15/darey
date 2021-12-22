# PROJECT 3: MERN STACK IMPLEMENTATION

## Step 1 – backend configuration

###Update ubuntu
`sudo apt update`

###Upgrade ubuntu
`sudo apt ugrade`

Getting Nodejs location
`curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -`

Install  Nodejs and NPM
`sudo apt-get install -y nodejs`

check version of nodeJs and NPM
`node -v` `npm -v`

Create a new directory for your To-Do project:
`mkdir Todo`

Verify that the Todo directory is created with ls command
`ls`

Getting into the Todo directory
`cd Todo`

initialise your project, so that a new file named package.json will be created. This file will normally contain information about your application and the dependencies that it needs to run. Follow the prompts after running the command. You can press Enter several times to accept default values, then accept to write out the package.json file by typing yes.

`npm init`

###INSTALL EXPRESSJS

To use express, install it using npm:

`npm install express`

Now create a file index.js 

`touch index.js`

Run `ls` to confirm that index.js file is successfully created

Then Install the dotenv module

`npm install dotenv`

Open the index.js file with the command below

`nano index.js` or `vim index.js`

paste the code below

`const express = require('express');
require('dotenv').config();
const app = express();
const port = process.env.PORT || 5000;
app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});
app.use((req, res, next) => {
res.send('Welcome to Express');
});
app.listen(port, () => {
console.log(\``Server running on port ${port}\``)
});`


Now it is time to start our server to see if it works. Open your terminal in the same directory as your index.js file and type:

`node index.js`

We now need to edit the outbound of our EC2 Security group to listen to the port 5000 and then view the welcome page from our browser using the server url anad port number.

`http://<PublicIP-or-PublicDNS>:5000`

There are three actions that our To-Do application needs to be able to do:

1. Create a new task
2. Display list of all tasks
3. Delete a completed task

##Routes

Each task will be associated with some particular endpoint and will use different standard HTTP request methods: POST, GET, DELETE.

For each task, we need to create routes that will define various endpoints that the To-do app will depend on. So let us create a folder routes

`mkdir routes`

Change directory to routes folder.

`cd routes`

Now, create a file api.js with the command below

`touch api.js`

Open the file with the command below

`vim api.js` or `nano api.js`

Copy below code in the file. (Do not be overwhelmed with the code)

`const express = require ('express');
const router = express.Router();
router.get('/todos', (req, res, next) => {
});
router.post('/todos', (req, res, next) => {
});
router.delete('/todos/:id', (req, res, next) => {
})
module.exports = router;`


##MODELS

Change directory back Todo folder with `cd ..` and install Mongoose

`npm install mongoose`

Create a new folder models :
`mkdir models`

Change directory into the newly created ‘models’ folder with
`cd models`

Inside the models folder, create a file and name it todo.js
`touch todo.js`

All three commands above can be defined in one line to be executed consequently with help of && operator, like this:

`mkdir models && cd models && touch todo.js`
















## Step 2 – frontend creation
