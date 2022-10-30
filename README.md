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

We begin by running the following command in the terminal:
```

flyctl launch

```

You will be prompted to input a name for your project. Note that you can only use numbers, lowercase letters, and dashes. Don't attempt to use any other characters.

Next, you will be prompted to select a region. For this class, pleae select the region for Chennai, India.

Finally, the CLI will ask if you need to set up a Postgresql database. Type N (no).

We will set up our postgres database separately afterwards.

You will then be asked if you want to deploy your project now, type no. We need to make a few adjustments before we deploy. 

#### Our Database

[Creating a Postgres App with Fly.io](https://fly.io/docs/reference/postgres-on-nomad/)

In this lesson, we will create a separate database to connect to our project. In the same terminal, type the following command to initialize a postgres app: 

```

flyctl postgres create

```

Provide an app-name for your project, and select the region closest to you.

Select Development, Single node, 1x shared CPU, 256MB RAM, 1GB disk

And once you are provided with your database credentials, **Please take a screenshot. These credentials are essential for you to be able to conenct to your database, and you will not be able to access them in fly.io afterwards**

To access the psql shell for our Fly postgres DB, run the following command in your terminal: 

```

flyctl postgres connect -a <your-postgres-app-name>

```

Alternatively, you can also run this command: 

```

flyctl proxy 5432 -a <your-postgres-app-name>


psql postgres://postgres:<password>@localhost:5432


```

To ensure our deployment executes sucessfully, we need to make sure that our PORT matches the port in the fly.toml file, and that our ENV (environment) variables are properly set.







 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 

