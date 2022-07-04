# Pipeline Process

- Add scripts in our root package.json that can install, build and deploy the application
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

- In order to create a continuous integration step, we will edit the .circleci/config.yml and add more commands that CircleCI will run jobs
    to run build and test scripts
    such as npm run api:build 

-  In order to create a continuous delivery step, We will need to edit udagram-api/bin/deploy.sh script by adding 
        1- ```aws s3 cp --recursive --acl public-read ./www s3://randomudagram12398/
              aws s3 cp --acl public-read --cache-control="max-age=0, no-cache, no-store, must-revalidate" ./www/index.html s3://randomudagram12398/
            ```  
              to upload the content of udagram-frontend with aws cli 
        2- After this is done, we will navigate to the pacakge.json located in udagram/package.json and we will add a deploy script
            "deploy": "npm run build && eb use udagram-api-dev1 && eb deploy".

        3-  Modify the .circleci/config.yml file to properly deploy our application. Our config.yml file
            npm run deploy

- To make sure our AWS credentials are properly saved in CircleCI. Here are the steps to do so:
        1- Navigate to the CircleCI dashboard.
        2- Go to the "project details" page of the project you are using.
        3- Click on "project details" and navigate to "environment variables".
        4- Add values for AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY. You can also add a value for AWS_DEFAULT_REGION. This should normally reflect the region where you have started your services.
        5- create access keys for an IAM user and give the permission needed and get values of AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY.
- push the changes you have done to GitHub, and the CircleCI project should pick up the change and deploy your application.

