# Dockerized React with CI/CD-pipeline

This project is newest React v17 dockerized for development and production use.
Project also includes Travis-CI template that runs test in feature branches and 
deploys to production in master branch.


## Get Started

In the project directory to build the local development server you can use either
docker-compose or Dockerfile.dev

#### Dockerfile.dev

Build the container by running 

`docker build -f Dockerfile.dev .`

After that you get the ID of the container. To enable hot-reload
you need to attach volume to container so that changes are replicated to development server.
Run the following command to do this:

`docker run -p 3000:3000 -v /app/node_modules -v $(pwd):/app <container ID>`

You now have docker running locally on localhost:3000!

#### docker-compose

Docker-compose is much simpler to use and also runs unit tests at the same time you're developing.
You only need to run `docker-compose up`, volumes and everything else is already setup in the composer file.

## Deployment

Like said previously this project uses Travis-CI for CI/CD. 
First you need to enable Travis-CI for your github repository at https://travis-ci.com/

By default Travis is configured to run unit tests when pushing to Github.
When pushing to feature branches only unit tests are ran and when doing a PR or pushing straight to master
you will trigger deployment build.

### Configuration to do before first deployment

1. Enable Travis-CI for your repository in https://travis-ci.com/
2. Create AWS IAM User and create Access Credentials for that account. Copy the credentials to Travis-CI environment variables
3. Create sample Node.js application to Elastic Beanstalk and modify the variables in .travis.yml-file for your environment

That's it, you're ready to deploy!

