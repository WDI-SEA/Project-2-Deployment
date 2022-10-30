# Project-2-Deployment

The following lesson will walk you through how to deploy a Node/Postgres Application using Fly.io

<img src="https://simplecore.intel.com/intel-capital/wp-content/uploads/sites/99/Fly.io-logo_1536x600.jpg"/>

<hr />

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









 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 

