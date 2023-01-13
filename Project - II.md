## SIMPLE TO-DO APPLICATION ON MERN WEB STACK

### Task - To deploy a simple To-Do application that creates To-Do lists

### STEP 1 – BACKEND CONFIGURATION

#### Steps

* Update ubuntu: `sudo apt update`
* Upgrade ubuntu: `sudo apt upgrade`
* Get the location of Node.js software from Ubuntu repositories. Run: `curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -`
 
![image](https://user-images.githubusercontent.com/76660222/210218002-03b7acac-4cdc-4a35-b828-2add5aa18416.png)

* Install Node.js on the server with this command: `sudo apt-get install -y nodejs` This command installs both nodejs and npm. NPM is a package manager for Node like apt for Ubuntu, it is used to install Node modules & packages and to manage dependency conflicts.
* Verify the node installation with this command: `node -v`
* Verify the npm installation with this command: `npm -v`
![image](https://user-images.githubusercontent.com/76660222/210219036-4877890a-53d7-439e-bcb8-c353560ee00a.png)

##### Application Code Setup

* Create a new directory for your To-Do project: `mkdir Todo`
* Run the command below to verify that the Todo directory is created, run: `ls`
* Next, change the current directory to the newly created one: `cd Todo`
* Next, you will use the command npm init to initialise your project, so that a new file named package.json will be created. This file will normally contain information about your application and the dependencies that it needs to run. Run the command: `npm init` then follow the prompt and finally answer yes to write out the package file.

![image](https://user-images.githubusercontent.com/76660222/210220397-6a1194a9-dbd0-4c17-91ad-2812ea161b88.png)

![image](https://user-images.githubusercontent.com/76660222/210220484-25d1a1e6-bb40-4674-9bee-3df41a18b133.png)

![image](https://user-images.githubusercontent.com/76660222/210220684-6a4d212b-b676-4685-9b72-28303432fd64.png)

##### INSTALL EXPRESSJS

* To use express, install it using npm: `npm install express`
* Next, create a file index.js with this command: `touch index.js`
* Run `ls` to confirm that your **index.js** file is successfully created.

![image](https://user-images.githubusercontent.com/76660222/210221171-7c041871-d8cf-47b5-a747-4e21f08fa1fe.png)

* Next step is to install the **dotenv** module. Run this code: `npm install dotenv`
![image](https://user-images.githubusercontent.com/76660222/210225264-28898c0d-2a0a-4193-9d98-12424e0c3373.png)

* Then open the **index.js** file with this command: `vim index.js`
* Type the code below into it and save:

```
const express = require('express');
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
console.log(`Server running on port ${port}`)
});
```

* Use **:w** to save in vim and use **:qa** to exit vim

![image](https://user-images.githubusercontent.com/76660222/210225452-4a98ea01-7736-4ccf-95fe-e0963beb8fc4.png)

* Test start the server to see if it works. Type: `node index.js`
* You should see Server running on port 5000 in the terminal.

![image](https://user-images.githubusercontent.com/76660222/210226425-90c4cc79-75d9-455a-804c-991430b88b47.png)

* Next, open port 5000 in EC2 Security Groups and save changes.
* Open a browser and access the server’s Public IP or Public DNS name followed by port 5000: `http://<PublicIP-or-PublicDNS>:5000`

![image](https://user-images.githubusercontent.com/76660222/210299881-00ad75d8-e081-45d4-ad94-e17540a42df9.png)

#### Routes

* The To-Do application needs to be able to complete 3 actions:
  * Create a new task
  * Display list of all tasks
  * Delete a completed task
* For each task, we need to create routes that will define various endpoints that the To-do app will depend on. Create a folder called **routes** with this command `mkdir routes`
* Change directory to **routes** folder and create a file **api.js** with the command: `touch api.js`

![image](https://user-images.githubusercontent.com/76660222/210300171-99ab879a-89f8-46b1-b863-9a149a90a420.png)

* Open the file with the command below `vim api.js`
* Copy and save the code below into the file:

```
const express = require ('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {

});

router.post('/todos', (req, res, next) => {

});

router.delete('/todos/:id', (req, res, next) => {

})

module.exports = router;
```

![image](https://user-images.githubusercontent.com/76660222/210300561-bb9b91db-2bb7-4a18-8f90-a6709e619ad5.png)

![image](https://user-images.githubusercontent.com/76660222/210300644-ffca79e8-3cf3-4147-ab20-8ef7b2d1f1e8.png)


##### MODELS

* To create a Schema and a model, install mongoose which is a Node.js package that makes working with mongodb easier. Change directory back Todo folder with `cd ..` and install Mongoose with the following command: `npm install mongoose`
* Create a new folder  **models** , then change directory into the newly created **models** folder, Inside the models folder, create a file and name it **todo.js** with the following command: `mkdir models && cd models && touch todo.js`
* Open the file created with vim todo.js then paste the code below in the file:

```
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

//create schema for todo
const TodoSchema = new Schema({
action: {
type: String,
required: [true, 'The todo text field is required']
}
})

//create model for todo
const Todo = mongoose.model('todo', TodoSchema);

module.exports = Todo;
```

![image](https://user-images.githubusercontent.com/76660222/211157394-5e593d4d-86c8-4afd-8228-79615b5f9e5a.png)

* Next, we update our routes from the file api.js in ‘routes’ directory to make use of the new model. In routes directory, open api.js with  **vim api.js** , delete the code inside with `:%d` command and paste there code below into it then save and exit

```
const express = require ('express');
const router = express.Router();
const Todo = require('../models/todo');

router.get('/todos', (req, res, next) => {

//this will return all the data, exposing only the id and action field to the client
Todo.find({}, 'action')
.then(data => res.json(data))
.catch(next)
});

router.post('/todos', (req, res, next) => {
if(req.body.action){
Todo.create(req.body)
.then(data => res.json(data))
.catch(next)
}else {
res.json({
error: "The input field is empty"
})
}
});

router.delete('/todos/:id', (req, res, next) => {
Todo.findOneAndDelete({"_id": req.params.id})
.then(data => res.json(data))
.catch(next)
})

module.exports = router;
```

![image](https://user-images.githubusercontent.com/76660222/211158073-6d101451-30f6-4992-b854-3d0fac3cbe3c.png)

##### MONGODB DATABASE

* A database is required where data will be stored. For this we will make use of mLab. Sign up for a shared clusters free account, Sign up on [https://www.mongodb.com/atlas-signup-from-mlab](https://www.mongodb.com/atlas-signup-from-mlab). Follow the sign up process, select AWS as the cloud provider, and choose a region.
* you should see something like this right after you log in

![image](https://user-images.githubusercontent.com/76660222/212305412-25765898-b4e8-41d9-9241-faecb04caf01.png)

![image](https://user-images.githubusercontent.com/76660222/212307048-763fb63a-247e-4de6-89ce-e75e88f10427.png)

![image](https://user-images.githubusercontent.com/76660222/212307676-d3e2a9d5-af36-402e-bbaa-b3502c5480a0.png)


* For the purposes of this project, allow access to the MongoDB database from anywhere.
* Make sure you change the time of deleting the entry from 6 Hours to 1 Week
* Create a MongoDB database and collection inside mLab



![image](https://user-images.githubusercontent.com/76660222/212309255-956fd2af-04b8-462c-a315-bfbc92fc9e51.png)


