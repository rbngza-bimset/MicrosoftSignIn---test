# MicrosoftSignIn - test README

Learning to use Microsoft Sign In.

## Table of contents

* [Team](#team)
* [Setup the project](#setup-the-project)
* [Running the stack for development](#running-the-stack-for-development)
* [Stop the project](#stop-the-project)
* [Restoring the database](#restoring-the-database)
* [Debugging](#debugging)

### Team

| Name                           | Email                    | Role                                       |
| ------------------------------ | ------------------------ | ------------------------------------------ |
| Rubén Garza                    | ruben.garza@bimset.mx    | Full stack dev                             |
| Javier Saldívar                | jsaldivar@iaarq.mx       | Developer                                  |
| Rodrigo Ramos                  | rodrigo@bimset.mx        | Project owner                              |


### Setup the project

You need to install Docker Desktop, to do that go to: https://www.docker.com/products/docker-desktop, create an account
and download the software, once it's downloaded install Docker Desktop with the default configuration.
Note: to download Docker Desktop you need to create an account with Docker.

After installing please you can follow this simple steps:

1. Clone this repository into your local machine

```bash
$ git clone git@github.com:bimset/BimsetCloudServices.git
```

2. Fire up a terminal and run:

```bash

$ docker-compose up -d --build app
```

3. Inside the container you need to create & migrate the database:
To get into the bash of the application:
```bash
$ docker-compose exec app bash
```
Then: (optional, depends if you've created the DB before)
```
% rails db:create
```
Followed by:
```
% rails db:migrate
```
Finally you can seed the db with:
```
% rails db:seed
```
### Running the stack for Development

1. Fire up a terminal and run:

```
docke-compose up -d --build app
```

That command will lift every service the app needs, such as the `rails app server` and `postgres`.


It may take a while before you see anything, you can follow the logs of the containers with:

```
$ docker-compose logs
```

Once you see an output like this:

```
...
Step 10/12 : ENV RAILS_ENV development
 ---> Running in 7d546fa73b97
Removing intermediate container 7d546fa73b97
 ---> cb42e9595a1f
Step 11/12 : RUN rails assets:precompile
 ---> Running in cbfa85fa9a69
/usr/local/bundle/gems/curb-fu-0.6.2/lib/curb-fu/core_ext.rb:60: warning: constant ::Fixnum is deprecated
Yarn executable was not detected in the system.
I, [2019-10-08T15:24:59.669401 #6]  INFO -- : Writing /usr/src/app/bcs_app/public/assets/HelveticaNeueLTPro-Lt-3ccd8e1efc15afb8e59a7dba15e48a20eeebca10bbe3cd33c3e010af63acfdea.otf
I, [2019-10-08T15:24:59.670572 #6]  INFO -- : Writing /usr/src/app/bcs_app/public/assets/HelveticaNeueLTPro-Lt-3ccd8e1efc15afb8e59a7dba15e48a20eeebca10bbe3cd33c3e010af63acfdea.otf.gz
I, [2019-10-08T15:24:59.675981 #6]  INFO -- : Writing /usr/src/app/bcs_app/public/assets/HelveticaNeueLTPro-UltLt-a4805dd261ec7c3e26a5f4c6c16deaec5aec4315f331e7cc893fe12449e96ea9.otf
I, [2019-10-08T15:24:59.677298 #6]  INFO -- : Writing /usr/src/app/bcs_app/public/assets/HelveticaNeueLTPro-UltLt-a4805dd261ec7c3e26a5f4c6c16deaec5aec4315f331e7cc893fe12449e96ea9.otf.gz
I, [2019-10-08T15:24:59.680723 #6]  INFO -- : Writing /usr/src/app/bcs_app/public/assets/bimset-fad637eef62d16d3206ae8e675536c0a39e822e00a5baa3196e9cfbe4b3ab8ed.png
I, [2019-10-08T15:24:59.804324 #6]  INFO -- : Writing /usr/src/app/bcs_app/public/assets/application-b987ebb688e2268be13f796f3f6815c866084b2a4f18d300973f5ec85d47e4a5.js
I, [2019-10-08T15:24:59.804814 #6]  INFO -- : Writing /usr/src/app/bcs_app/public/assets/application-b987ebb688e2268be13f796f3f6815c866084b2a4f18d300973f5ec85d47e4a5.js.gz
I, [2019-10-08T15:25:03.073107 #6]  INFO -- : Writing /usr/src/app/bcs_app/public/assets/application-463d5bdfbb5d6798b3ae14c27e156d3ef24e0f5f3cce3e252a82244b9da3cbd7.css
I, [2019-10-08T15:25:03.073442 #6]  INFO -- : Writing /usr/src/app/bcs_app/public/assets/application-463d5bdfbb5d6798b3ae14c27e156d3ef24e0f5f3cce3e252a82244b9da3cbd7.css.gz
Removing intermediate container cbfa85fa9a69
 ---> dd407669fc6a
Step 12/12 : CMD script/start
 ---> Running in ef027f26b8f6
Removing intermediate container ef027f26b8f6
 ---> 7cfe0f7df6d4
Successfully built 7cfe0f7df6d4
Successfully tagged bimsetcloudservices_app:latest
Recreating forge ...
bimsetcloudservices_webserver_1 is up-to-date
Recreating forge ... done
Recreating bimsetcloudservices_app_1 ... done
```

This means the project is up and running.

### Stop the project

```bash
$ docker-compose stop
```

This will stop every container, but if you need to stop one in particular, you can specify it like:

```bash
$ docker-compose stop app
```
or
```bash
$ docker-compose stop db
```
to stop the database

`app` is the service name located on the `docker-compose.yml` file, there you can see the services name and stop each of them if you need to.

### Restoring the database

You probably won't be working with a blank database, so once you are able to run the proyect you can restore the database, to do
so you need to start the proyect:

```
% docker-compose up -d --build app
```

Go into the bash:

```
% docker-compose exec app bash
```

Reset the db:

```
% rake db:migrate:reset
```

Then seed the database to put all the pre-coded info back in:

```
% rake db:seed
```

### Debugging

We know you love to use `debugger`, and who doesn't, and with Docker is a bit tricky, but don't worry, we have you covered.

Just run this line at the terminal and you can start debugging like a pro:

```
% docker logs <CONTAINER ID>
```

If you don´t know the CONTAINER ID:
```
% docker ps -a
```

This will display the logs from the rails app.
