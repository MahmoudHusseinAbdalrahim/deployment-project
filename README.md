# Hosting a Full-Stack Application

### Descrption
In this project we take a newly developed Full-Stack application and deploy it to a cloud service provider (AWS) so that it is available to customers. We use the aws console to start and configure the services the application needs such as a database to store information and a web server allowing the site to be discovered by potential customers.

After the initial setup, we learn to interact with the services you started on aws and will deploy manually the application a first time to it. As we get more familiar with the services and interact with them through a CLI, We gradually understand all the moving parts.

We then register for a free account on CircleCi and connect your Github account to it. Based on the manual steps used to deploy the app, you will write a config.yml file that will make the process reproducible in CircleCi. You will set up the process to be executed automatically based when code is pushed on the main Github branch.

The project also include writing documentation and runbooks covering the operations of the deployment process. Those runbooks will serve as a way to communicate with future developers and anybody involved in diagnosing outages of the Full-Stack application.

# Udagram

This application is provided as an alternative starter project and we will use it for this project. The udagram application is a fairly simple application that includes all the major components of a Full-Stack web application.



### Dependencies

```
- Node v14.15.0 (LTS)

- npm 6.14.8 (LTS) 

- AWS CLI v2

- A RDS database running Postgres.

- A S3 bucket for hosting uploaded pictures.

```

### Installation

Provision the necessary AWS services needed for running the application:

1. In AWS, provision a publicly available RDS database running Postgres. <http://database-1.cghy18cmuyj7.us-east-1.rds.amazonaws.com>
1. In AWS, provision a s3 bucket for hosting the uploaded files. <http://randomudagram12398.s3-website-us-east-1.amazonaws.com>
1. Export the ENV variables needed or use a package like [dotnev](https://www.npmjs.com/package/dotenv)/.
1. From the root of the repo, navigate udagram-api folder `cd starter/udagram-api` to install the node_modules `npm install`. After installation is done start the api in dev mode with `npm run dev`.
1. Without closing the terminal in step 1, navigate to the udagram-frontend `cd starter/udagram-frontend` to intall the node_modules `npm install`. After installation is done start the api in dev mode with `npm run start`.


## Built With

- [Angular](https://angular.io/) - Single Page Application Framework
- [Node](https://nodejs.org) - Javascript Runtime
- [Express](https://expressjs.com/) - Javascript API Framework

## License

[License](LICENSE.txt)
