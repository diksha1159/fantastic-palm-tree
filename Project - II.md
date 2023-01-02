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

