# ![logo](https://github.com/LemontechSA/test-fullstack-angelo-calvo/raw/master/practical/thot-ui/src/assets/head-thot.png) Thot
## String Comparator System
## Introduction
Thot is an web app made to execute an operations in strings extensible to any operation you want. 

It built in React, Ruby on Rails and Java spark simulate a Frontend-Backend interation with an integration with remote operation REST service server (Siwa).

This project it's the resolution of FullStack practical test.

View all the changes realized in the time, in the CHANGELOG.md

If you are my code reviewer, Enjoy that! 
## Get Started
If you want review the code in the app, probably you want start the app in developer mode. If you want follow this way, please folow the instructions detailed in **Dependencies** and **Development Environment**.

If you want only test the app, only require docker. If you have docker, please go to **Deploy Instructions** and follow the instructions.

Let's go!
## Dependencies
To develop, test and deploy the app, you need the next dependencies
- Install Docker

```bash
# In Debian based linux
sudo apt-get install -y docker 
# In RHEL based linux
sudo yum install -y docker
```

- Install Ruby and Ruby on Rails
```bash
# In Debian based linux
sudo apt-get install ruby-full
gem install rails
# In RHEL based linux
sudo yum install ruby
gem install rails
```

- Install Nodejs and NPM
```bash
# In Debian based linux
sudo apt-get install nodejs npm
# In RHEL based linux
sudo yum install nodejs
```
- Install yarn
```bash
sudo npm install yarn -g
```

- Install JAVA 8
```bash
# In Debian based linux
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
# In RHEL based linux
# Normally java 8 comes with RHEL but is important check the version
java -version
# If lower to 8 use the command
yum install java-1.8.0-openjdk
```

- Install Maven
```bash
# In Debian based linux
sudo apt-get install mvn
# In RHEL based linux
sudo yum install mvn
```

## Develop environment
To use the development environment you must start the docker container, that contain the database. To do this you must write the next command.

```bash
docker-compose up -d
```

To start Thot Rails app, you must enter to thot directory and execute the next command.

```bash
rails server
```

To start Thot-ui React app, you must enter to thot-ui directory and execute the next command.

```bash
yarn start
```

To start Siwa Spark app, you must enter to thot directory and execute the next command.

```bash
mvn clean package
java -jar /target/siwa-jar-with-dependencies.jar
```

The database tools and the app will be available in the local machine in the next locations. 

```bash
# Thot-ui App
http://localhost:3001
# Thot App
http://localhost:3000
# Siwa App
http://localhost:4567
# phpmyadmin
http://localhost:7000
```

## Deploy Instructions
To deploy and testing, Thot App and Siwa you must run the next commands

```bash
docker-compose -f docker-compose.production.yml build
docker-compose -f docker-compose.production.yml up -d
```
The Thot and Siwa app are available in the next locations

```bash
# Thot-ui App
http://localhost:80
# Thot App (Splash screen)
http://localhost:8080
# Siwa App (Splash screen)
http://localhost:8090
# phpmyadmin
http://localhost:7000
```

## Api Documentation
Both Siwa and Thot,  in production mode, have an API REST Reference manual built with Apidoc. In this manual you can see the reference of both API's.

To access to reference, deploy the project in production docker mode and go with your browser to:

```bash
# Siwa Splash screem
http://localhost:8090/api/
# Thot API reference
http://localhost:8080/api/
```

## Testing
To testing Siwa use Junit and maven

```bash 
mvn test
```

To test RoR App use Rspec

```bash
bundle exec rspec
```

## How Works
Thot and Siwa works like an API Services Servers, working in paralel like two remotes servers. The client app load a app Built with React, and work like another server instance. The three parts are separated and comunicates between them across RESTFul services built in them.

To simulate this environment we use docker to set each application in a separate container, simulating with this way the servers and his properties.

If your want more information about the functionality and software arquitecture used, please visit ARCHITECTURE.es.md (Spanish Reference)

## License
MIT

## Developer words
In the App, I writed an paragraph of gratitude. If you want to see **follow the white rabbit**.

## To
Made with <span style="color:red;">❤</span> for Lemontech and <span look-in="thot-ui you are close">🐇</span>
