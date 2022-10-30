# Project-2-Deployment

The following lesson will walk you through how to deploy a Node/Postgres Application using Fly.io

<img src="https://simplecore.intel.com/intel-capital/wp-content/uploads/sites/99/Fly.io-logo_1536x600.jpg"/>

## Getting Started with Fly.io

Run the following scripts to install the flyctl command line utility which we will use to launch and deploy our application

### MacOS

``` 

brew install flyctl 

```

### Linux/WSL 

``` 

curl -L https://fly.io/install.sh | sh 

```

### Windows

``` 

iwr https://fly.io/install.ps1 -useb | iex

```
 
<hr />
 
### Sign Up
 
Once the flyctl command line utility is installed, we can signup/login to our account

cd into your project directory and run the following command:

``` 

flyctl auth signup 

```

Once the browser window opens, click on **Sign Up with GitHub** and click on the green button to **Authorize Fly.io**

Once on the payment screen, click on the small message below the form that says **Try Fly.io for free**

Back in your terminal, sign into your fly account by running the following command:

``` 

flyctl auth login 

```

And click on the button to sign in **Continue as ... ... .. @email.com**

You should receive a message in the terminal that says: **successfully logged in as ... .. ..@email.com**

<hr />

### Deployment

#### Our Main Application

Now that we have signed up and logged into our fly.io account, we can begin the deployment process. Please ensure that you are in the correct project directory and disabled any running VPN's on your computer. 

Run the following command in the terminal:
```

flyctl launch

```

You will be prompted to input a name for your project. Note that you can only use numbers, lowercase letters, and dashes. Don't attempt to use any other characters.

Next, you will be prompted to select a region. For this class, pleae select the region for Chennai, India.

Finally, the CLI will ask if you need to set up a Postgresql database. Type N (no).

We will set up our postgres database separately afterwards.

You will then be asked if you want to deploy your project now, type N (no). We need to make a few adjustments before we deploy. 

#### Our Database

[Creating a Postgres App with Fly.io](https://fly.io/docs/reference/postgres-on-nomad/)

In this lesson, we will create a separate database to connect to our project. In the same terminal, type the following command to initialize a postgres app: 

```

flyctl postgres create

```

Provide an app-name for your project, and select the region closest to you.

Select Development, Single node, 1x shared CPU, 256MB RAM, 1GB disk

Once you are provided with your database credentials, **Please take a screenshot. These credentials are essential for you to be able to connect to your database, and you will not be able to access them in fly.io afterwards**

To access the psql shell for our Fly postgres DB, run the following command in your terminal: 

```

flyctl postgres connect -a <your-postgres-app-name>

```

Alternatively, you can also run this command: 

```

flyctl proxy 5432 -a <your-postgres-app-name>


psql postgres://postgres:<password>@localhost:5432


```

Once inside the shell, we need to manually create our Postgres Tables. We begin by creating the Database for our project, for example: 

```

psql=# CREATE DATABASE pokedex_review;

```

The User table is provided below:

```

CREATE TABLE IF NOT EXISTS public.users
(
    id SERIAL,
    email character varying(255),
    password character varying(255),
    "createdAt" timestamp with time zone NOT NULL,
    "updatedAt" timestamp with time zone NOT NULL,
    CONSTRAINT users_pkey PRIMARY KEY (id)
);

```

The id for each of your tables should be **id SERIAL**

The SQL for your table can be found in the SQL tab of pgAdmin when you click on the table name under Databases-->Your Database--->Schemas--->Tables---> Your Table (ex. Users)

Please remove the DEFAULT and COLLATE commands from the SQL when you insert into your fly database, as well as the last 3 lines (Tablespace.. .. Alter table...)

Once your SQL command is ready, run it in your fly.io psql shell to apply them to your 

```

psql=# CREATE TABLE IF NOT EXISTS ... ... ...

```

Once you have created all your tables, your database should be all set! The last step we need to do is set our environment variables, connect to our database, and deploy our project.

Back in our main application, modify your **models/index.js** with the following code for lines 1-20:

```

'use strict';

const fs = require('fs');
const path = require('path');
const Sequelize = require('sequelize');
const basename = path.basename(__filename);
require('dotenv').config()
const config = {
  "production": {
    "database": process.env.DATABASE,
    "host": process.env.DATABASE_HOST,
    "username": process.env.DATABASE_USERNAME,
    "password": process.env.DATABASE_PASSWORD,
    "dialect": "postgres",
    "port": process.env.DATABASE_PORT
  }
}
const db = {};

```

To ensure our deployment executes sucessfully, we need to make sure that our PORT matches the port in the fly.toml file, and that our ENV (environment) variables are properly set.

We now need to update our .env file to include the ENV variables to connect to our database. **Please refer to the screenshot you took of your postgres credentials and use your credentials to connect to your database** This is an example of what your .env should look like: 

```

...your previous ENV variables
PORT=8080
SECRET=your-secret
DATABASE=pokedex_review
DATABASE_HOST=bh-pokedex-p2-db.internal
DATABASE_USERNAME=postgres
DATABASE_PASSWORD=MaTSKZH1RmxF8y3
DATABASE_PORT=5432

```

Finally, ensure that your PORT in your main index.js file is configured to use your env port or port 8080 (Or whichever port your fly.toml file is configured to):

**index.js**
```

const PORT = process.env.PORT || 8080

app.listen(PORT, ()=>{
    console.log('Project 2 Express Authentication')
})

```


Finally, we can transfer our environment variables to our fly.io application using the following command:

```

flyctl secrets import < .env

```

And you can double check that your ENV variables have been transferred to your application by visiting your application UI via the fly.io dashboard, and accessing the secrets section in the menu.

We are now ready to deploy. Run the following command in your terminal to officially deploy your application online!

```

flyctl deploy 

```

Visit your fly.io dashboard and click on your application host to open the link.

And Congratulations!











 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 

