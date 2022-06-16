# Marketo Web API Server

# Deploy `json-server` to `Heroku`

> Instructions how to deploy the full fake REST API [json-server](https://github.com/typicode/json-server) to Heroku. Should only be used in development purpose, but can act as a simpler database for smaller applications.

## Create your database

1 . Change the contents of `db.json` to **your own content** according to the [`json-server example`](https://github.com/typicode/json-server#example) and then `commit` your changes to git locally.

2 . `db.json` file in this repository, including `/users`, `/companies` ,`/contacts` and `/countries` routes.

_In the simplest form, like this example will create `/posts` route , each resource will have `id`, `title` and `content`. `id` will auto increment!_
```json
{
  "posts":[
    {
      "id" : 0,
      "title": "First post!",
      "content" : "My first content!"
    }
  ]
}
```

3 . You simply add new route and your JSON array data to the `db.json`, if your own data is a CSV file, you can convert it to JSON file via https://www.convertcsv.com/csv-to-json.htm
1. Make sure data has one column called "id". Upload your CSV file
2. encoding choose “UTF-8”
3. choose “CSV to JSON”, click "Download Result".


---

## Deploy to **Heroku**

<img align="right" width="100px" height="auto" src="https://blackdeerdev.com/wp-content/uploads/2021/02/Heroku.png" alt="Heroku">

Heroku is a free hosting service for hosting small projects. Easy setup and deploy from the command line via _git_.

###### Pros

* Easy setup
* Free

###### Cons

* App has to sleep a couple of hours every day.
* "Powers down" after 30 mins of inactivity. Starts back up when you visit the site but it takes a few extra seconds. Can maybe be solved with [**Kaffeine**](http://kaffeine.herokuapp.com/)

---

### Install Heroku

1 . [Create your database](#create-your-database)

2 . Create an account on <br/>[https://heroku.com](https://heroku.com)

3 . Install the Heroku CLI on your computer: <br/>[https://devcenter.heroku.com/articles/heroku-cli](https://devcenter.heroku.com/articles/heroku-cli)

4 . Connect the Heroku CLI to your account by writing the following command in your terminal and follow the instructions on the command line:
```bash
heroku login
```

5 . Then create a remote heroku project, kinda like creating a git repository on GitHub. This will create a project on Heroku with a random name. If you want to name your app you have to supply your own name like `heroku create <project-name>`:
```bash
heroku create <project-name>
```
Note that it shall give you the web app URL and the git repository in the console, e.g.

https://project-name.herokuapp.com/

https://git.heroku.com//project-name.git

6 . Push your app to __Heroku__ (you will see a wall of code)
```bash
git remote add heroku <your Heroku git URL>
git add .
git commit -m "first commit"
git push heroku HEAD:master
```

7 . Visit your newly create app by opening it via heroku:
```bash
heroku open
```
It shall open your web app in your browser.

8 . For debugging if something went wrong:
```bash
heroku logs --tail
```

---

#### How it works

Heroku will look for a startup-script, this is by default `npm start` so make sure you have that in your `package.json` (assuming your script is called `server.js`):
```json
 "scripts": {
    "start" : "node server.js"
 }
```

You also have to make changes to the port, you can't hardcode a dev-port. But you can reference herokus port. So the code will have the following:
```js
const port = process.env.PORT || 4000;
```
