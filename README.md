# Yoga Solo -  Full Stack code challenge

## Original challenge

* [Repository](https://github.com/YogaSolo/fs-coding-challenge)
* [README copy](INSTRUCTIONS.md)

## Description

This is an implementation for the FullStack challenge proposed by the YogaSolo team.

This solution is divided in different repositories to allow more independence between the different technology stacks. The details for each stack are describen in the `README` file of each repository.

The stacks run on separate dockers. The following stacks are available:
* [Front-end](https://github.com/christianamenos/ys_fs_front): it uses Angular to create a Single Page Application. I chose Angular because I'm more familiar with the technology, and I have already risked implementation time with the back-end and operational technologies.
* [Back-end](https://github.com/christianamenos/ys_fs_back): it uses SpringBoot with Kotlin. I chose these technologies because I wanted to learn a bit about them, and I thought it could be interesting way to test them. I think it also aligns with demand on the market.
* [Database](https://github.com/christianamenos/mongodb): I chose MongoDB as the database for the project, because it's a powerful relational database, and it adds flexibility on the schema in case I wanted to perform some changes in any of the databases used. I was also interested on defining a MongoDB image, and how to manage it with docker.

In order to run the solution, it will require to have a macOS machine with the following software installed:
* [Homebrew](https://brew.sh/index_es)
* [Docker desktop](https://www.docker.com/)
* [MongoDB CLI commands](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)

## Instructions to run the solution
**Use the following commands to setup the environment:**

Network creation:
```bash
cd ~
# Create a localdirectory (to ease clean up)
mkdir christianamos_test
# Create network
docker network create --subnet=172.18.0.0/16 ys_network
```

Database setup:
```bash
# Move to the working directory and clone the project
cd ~/christianamos_test
https://github.com/christianamenos/mongodb
cd mongodb
# Build the docker file (run it twice if the first attempt fails)
docker build -t ys_db .
# Start mongodb container
docker run -d -p 27017:27017 --name ys_db --network ys_network --ip 172.18.0.20 ys_db
mongorestore yoga_solo_bckp
```

Back setup:
```bash
# Move to the working directory and clone the project
cd ~/christianamos_test
git clone https://github.com/christianamenos/ys_fs_back
cd ys_fs_back
# Build and start back-end container
docker build -t ys_back .
docker run -d -p 8080:8080 --name ys_back --network ys_network --ip 172.18.0.21 ys_back
```

Front setup:
```bash
# Move to the working directory and clone the project
cd ~/christianamos_test
git clone https://github.com/christianamenos/ys_fs_front
cd ys_fs_front
# Build and start back-end container
docker build -t ys_front .
docker run -d -p 4200:4200 --name ys_front --network ys_network --ip 172.18.0.22 ys_front
```

Check that all dockers are done starting the services (you can check this in the docker dashboard).
**Go to:** [http://localhost:4200](http://localhost:4200)

**Note:** the protocol must be http, https is not activated for this proof of concept.

## Decisions and future work
In the README files for each specific project you will find the description of the decisions taken as well as future work that could be done in order to improve the solution, or to finish it.

## Contact

For specific details about the implementation or how to run it, please contact me using any of the following channels:

* [Christian Amenós's website](https://christianamenos.com)
* [Christian Amenós's email](mailto:christian.amenos@gmail.com)
