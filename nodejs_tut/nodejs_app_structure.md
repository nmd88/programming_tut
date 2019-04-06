NODEJS APP STRUCTURE
---


At root level we have:
1. **_app_** is where our main app code goes and will discuss in depth under app structure below.
2. **_docs_** (optional) is for documentation purpose.
3. **_lib_** (optional) is where the complied app code goes which is used for production env.
4. **_migrations_** is where all the table schema. I personally use knex.js and an self made ORM name tabel written on top of it.
5. **_node_modules_**
6. **_tests_** is where we write all our unit test.
The structuring of tests folder is like the actions or routes under app folder and will be explained in app structure section.
7. config and config.sample.js are where all of our configuration related to database, authentication, external api keys etc are stored.

If you are wondering why we have two such files, then config.sample.js goes to your repository so that other developer can know the file shape and can use to form their local config.js file.

Also, we can also have a config.production for production environment.

_Note_: config can be a separate folder too, that can have separate sub configs files for database, external Api’s key etc but it feel overkill to me.

8. **_eslintrc** is where the lint logic goes.
9. **_migrate_** is the file that pass our configuration from config.js to ORM and help us run migration from CLI, check the code here.
10. **_gitignore_** is where we path to folder or filename that we don’t want to push on repository.
11. **_package.json_** — you already know it 😃.

# 1. **_app_** structure

1. **_server.js_** is the file that start your server and will have all middleware that is required for request parsing like bodyparser, cors, multer and errorhandlers etc and finally we add routes middleware.

2. **_routes_** will have sub-files or sub-folders made as per the entities in project.

The index.js under routes looks like as shown below. It have request handler middlewares and a catch all route.


_Note_: We can abstract a big entity like teams in a folder and can call it as teams which can then have sub subfolder like members, contacts, dashboard etc. under routes.

A file under routes is where all request handler or sub-routes are written and the only purpose of them is to either call the action that is responsible for that route or the sub-route folder.

_Note_: signup, login, logout, refresh and forgetpassword in above image all are actions that are defined under action folder.

3. Most of the times actions folder will have same the same structuring as the routes folder.

Each file in actions is for business logic i.e all code that store, get, change real entities either in database tables or doing queuing function like enqueue and dequeue etc all happen here.

_Note_: Actions can call other actions too.

4. So, middlewares, utils, helpers, tasks will follow the same way of structuring as action or routes do i.e main entity will act as a root folder and then will can have subfolder as per sub-entities and repeat.

5. tasks.js is used for running tasks from CLI created under task folder like database seed, clean database etc.

6. nsqd(optional) is use case specific for distributed messaging.

_Note_: NSQ is one the best i have used for distributed messaging it works great with no pain in production.
utils and helpers can be merged if need, i love to keep them separate so that i can reuse utils as its more generic in all projects
6. nsqd(optional) is use case specific for distributed messaging.