# Deployment of Web App for Free

In this repository I have some of the ways one can depoly their
`MERN web app` for free.


There are many cloud platforms which allows to deploy a webapp. Some of them are 
paid and some of them are free (with limited features).

I have categorized the Cloud Platform accorning to needs of the project.

## 1. Big Players (Paid):
- They have everything one need to make his/her website online.
- They provide everything like :
    + IaaS (Infrastructure as a Service), 
    + PaaS (Platfrom as a Service),
    + SaaS (Software as a Service),
    + Load Balancing
    + Automatic Scalling
    + Maintaining Databases
    + Creating Backups      
and other handfull of services.

- Since, you are provided with everything and there are a lot of things which are runnig under the hood,and the prices are little dynamic.(You will not get the same bill everymonth).

- If anyone want to just host a simple soloproject, just to show their work (and don't have plans to take it to long term ), then these are not the optimal option.
- Some examples 
    - [Google Cloud Platform (GCP)](https://cloud.google.com/)
    - [Amazon Web Services (AWS)](https://aws.amazon.com/)
    - [Microsoft Azure](https://azure.microsoft.com/en-us/)

## 2. Medium Players :
These include players like :
- Digital Ocean
- Linode
- Vultr
These are also similar to the big players, but not as huge as them. These also provide with suite of product with 
all the pricing listed down on their website.

## 2. Normal Players : ( I will dicuss these in this repo)
These include PaaS platforms like :
- Heroku
- Netlify
These are free and provide with its sub-domain for your projects.

# MERN Project Deployment

So, there's many ways to deploy a mern app on platfoms like Heroku and Netlify. 

I will be talking about three main ways :

### 101 : Frontend on Netlify & Backend on Heroku
-  Fronted will be deployed on Netilfy and Backend will be deployed on Heroku.
- Both will have seperate link.
- Fronted will be connected to backed by specifing backed link in fronted routes.
- Frotend -> on Netlify
- Backups -> on Heroku


### 102 : Both on Heroku, but as a seperate app
- Make two seperate app for fronted and backed
- Frontend -> on Heroku
- Backend -> on Heroku

### 103 : Both on Heroku as a single app

- Will make only one app on Heroku and deploy on it.

Let being with the first Deployment (101):

### Single React App on Heroku ( Can also do this if the react app does't have any backend)

1.  Create your app and make it error Free.
2. Create a Heroku account.
3. Download Heroku CLI from [here](https://devcenter.heroku.com/articles/heroku-cli).
4. Run these codes.
```
heroku login
```
```
git init
```
```
heroku git:remote -a <heroku-app-name>
```
```
heroku create -b https://github.com/mars/create-react-app-buildpack.git
```
```
git add .
```
```
git commit -am "First Commit"
```
```
git push heroku master:main
```
### Single React App on Netilfy
1. Create the react app
2. Open the app folder in terminal
3. Run the following command, to make "build" folder 
```
npm run build
```
or 
```
yarn build
```
4. Create a account on Netlify
5. Clink on new Project 
6. Drag and drop your build folder to Netlify manual upload section.


### Single Node app on Heroku ( Backend)

Here is the Final Backed App Structure (ready to depoly) :

![server screenshot](https://user-images.githubusercontent.com/47392217/190476680-8ad20d2d-0b75-4d95-83e5-dd4d716a76b8.png)  

- Make a ```.gitignore``` file inside the root folder
- Add the following code inside it :
```
node_modules
.env 
```
- Create a Procfile inside the root of the Project and add the following code inside it :
```
web:node index.js 
```
- Add this inside ```index.js ``` Just to get some outcome, to verify that backend is working 
```javascript
app.get("/working",(req,res) => {
    res.send("It is working")
});
```

- Make a new App on Heroku, And run the following command on the terminal (make sure you are in the root folder of the project while executing these commands) :
```
heroku login
```
```
git init
```
```
heroku git:remote -a <heroku-app-name>
```
```
git add .
```
```
git commit -am "First Commit"
```
```
git push heroku master:main
```
And your app is ready :)

## Now lets Deploy both as a Single Heroku App (most efficient way) :

Step 1 : Connect your Databases to mongoDB Atlas
Step 2 : Get client folder inside the server folder.

Here is a small snapshot of folder structure.
![folder structure ](https://user-images.githubusercontent.com/47392217/190488359-69e8f4ac-1d6c-464f-8edd-1498c74ba5a7.png)

Step 3 : Create a ```.gitignore``` file inside your root folder 
```
node_modules
.env
```

Step 4 : Create a Procfile and include these inside it :
```
web:node index.js
```

Step 6 : Install & require "path" package in index.js
```
npm install path
```
Step 7 : Write this script in index.js
```javascript
if(process.env.NODE_ENV === "production") {
    app.use(express.static(path.join(__dirname, "/client/build")));

    app.get('*', (req, res) => {
        res.sendFile(path.join(__dirname, 'client','build', 'index.html'));
    })
}else {
    app.get('/',(req,res) => {
    res.send("Api Running");
    })
}
```
Step 8 : Must have these two lines inside "scripts" in ```package.json``` of backend.

```
"scripts": {
    "start": "node index.js",
    "heroku-postbuild": "cd client && npm install && npm run build"
},
```
#### Step 9 : Create New app on Heroku 


#### Step 10 : Open the client folder in terminal & delete ```.git``` folder from inside it.

To delete the ```.git``` folder, run the following command

```
rm .git
```
#### Step 11 : Change the proxy (present in package.json file of frontend ), from "localhost:5000" to new app link (eg : newapp.herokuapp.com)

From  => ``` "proxy":"http://localhost:5000"```

To  => ``` "proxy" : "https://newapp.herokuapp.com" ```

#### Step 12 : Create a ```.npmrc``` file 

If you have installed any package by using ```--legacy-peer-deps``` or ```--force``` , then make a ```.npmrc``` file inside the root folder and include these inside it :
```
force=true
legacy-peer-deps=true
```
Step 13 : Now run the following commands (being  inside server) ;

```
heroku login
```
```
git init
```
```
heroku git:remote -a <heroku-app-name>
```
```
git add .
```
```
git commit -am "First Commit"
```
```
git push heroku master:main
```
Step 14 : Add the environment variable inside Heroku App 

And that's it the web app it live :)
   
    
    
