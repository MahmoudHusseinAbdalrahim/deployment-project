# Infrastructure for deployment

## Descrption
Preparing source code infrastructure for deployment and we will write a project-level package.json file and organize it properly and Configure the needed infrastructure for a web application and no environment variables that change from the development environment and production should be present in the source code and a central configuration file is used in order to set the environment variables and make them available to the code and no authentication strings are hard-coded in the source code
we use npm install to install dependiences of this project and can use npm run scriptname

### package.json that located in the root of the project there are scripts for building, testing, and deploying the project

    "scripts": {
        "frontend:install": "cd udagram/udagram-frontend && npm install -f",
        "frontend:start": "cd udagram/udagram-frontend && npm run start",
        "frontend:build": "cd udagram/udagram-frontend && npm run build",
        "frontend:test": "cd udagram/udagram-frontend && npm run test",
        "frontend:e2e": "cd udagram/udagram-frontend && npm run e2e",
        "frontend:lint": "cd udagram/udagram-frontend && npm run lint",
        "frontend:deploy": "cd udagram/udagram-frontend && npm run deploy",
        "api:install": "cd udagram/udagram-api && npm install .",
        "api:build": "cd udagram/udagram-api && npm run build",
        "api:start": "cd udagram/udagram-api && npm run dev",
        "api:deploy": "cd udagram/udagram-api && npm run deploy",
        "deploy": "npm run api:deploy && npm run frontend:deploy"
    }

### package.json that located in the udagram-api folder of the project there are scripts for building, testing, and deploying thw backend 

    "scripts": {
        "start": "node ./server.js",
        "tsc": "npx tsc",
        "dev": "npx ts-node-dev --respawn --transpile-only ./src/server.ts",
        "prod": "npx tsc && node ./server.js",
        "clean": "rm -rf www/ || true",
        "deploy": "npm run build && eb use udagram-api-dev1 && eb deploy",
        "build": "npm install . && npm run clean && tsc && cp -rf src/config www/config && cp -R .elasticbeanstalk www/.elasticbeanstalk && cp .npmrc www/.npmrc && cp package.json www/package.json && cd www && zip -r Archive.zip . && cd ..",
        "test": "echo \"Error: no test specified\" && exit 1"
    }

### package.json that located in the udagram-frontend folder of the project there are scripts for building, testing, and deploying the frontend of the website

  "scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "deploy": "npm install -f && npm run build && chmod +x bin/deploy.sh && sh ./bin/deploy.sh",
    "test": "ng test --watch=false",
    "lint": "ng lint",
    "e2e": "ng e2e"
  }

  ### Configure the needed infrastructure for a web application

    -AWS RDS for the database
        1- open cloud AWS management console.
        2- search (rds) in search bar and click on to open RDS dashboard.
        3- click on create database button to take me to the creation wizard.
        4- configure the database from different option depend on the type and size of your application and determine username and password.
        5- then we can go to the console of this specific database and in connectivity and security tab look for endpoint and port section and copy and paste endpoint.
        6- the database is ready to accept requests on the endpoint provided. 
        7- link of end point <http://database-1.cghy18cmuyj7.us-east-1.rds.amazonaws.com> port 5432

    -AWS ElasticBeanstalk (or alternatives like lambda) for the API
        1- use eb init that will configure the elastic beanstalk region, platform such as node.js and application name
        2- eb create udagram-api-dev1 that create elsatic beanstalk environment 
        3- eb use udagram-api-dev1 to make our app use the specified environment
        4- set environment variables by using setenv key=value
        5- eb deply to deploy the udagram-api to elastic beanstalk
        6- server running on the link<http://udagram-api-dev1.eba-hcxhinqf.us-east-1.elasticbeanstalk.com/>
        
    -AWS s3 for web hosting
        1- navigate to the aws s3 console 
        2- click on the create bucket button taken to the create bucket wizard
        3- configure the bucket setting as you want publicly availability
        4- open the bucket and go to properties menus in static website hosting then edit to enabled and specify entry file (index.html)
        5- you can edit permission > bucket policy to make fine grained access 
        6- upload the content of udagram-frontend with aws cli by using 
            ```aws s3 cp --recursive --acl public-read ./www s3://randomudagram12398/
               aws s3 cp --acl public-read --cache-control="max-age=0, no-cache, no-store, must-revalidate" ./www/index.html s3://randomudagram12398/
            ```  
        7- link of the website <http://randomudagram12398.s3-website-us-east-1.amazonaws.com>