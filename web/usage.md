# Usage
The web application is distributed with docker. Details of usage and
requirements for both docker and without are listed below.

A configuration file is required to start YACRS. This config file must
exist in `/web/src/config.php`. A sample config file can be found in
`/web/src/sample.config.php`. Copy sample.config.php to config.php and
change any required configuration options. An overview of the config
file can be found [here](config.md).

## Docker
The following versions (or newer) are required to use YACRS.
 * [Docker](https://www.docker.com/) (17.12.0-ce)
 * [Docker Compose](https://docs.docker.com/compose/) (1.18.0)

Once these have been installed and a config file has been created. Enter
the project home directory in your terminal (the same directory as the
file `docker-compose.yml`.

Run the following command to build the container (root may be required
depending on your docker configuration):

    docker-compose build

then run the following command to run the app in a development
environment:

    docker-compose -f docker-compose.yml -f docker-compose.dev.yml

This will host the application at [http://127.0.0.1:4000](http://127.0.0.1:4000)
aswell as an instance of phpmyadmin at [http://127.0.0.1:4001](http://127.0.0.1:4001).

To host the application in a production evvironment run:

    docker-compose -f docker-compose.yml -f docker-compose.prod.yml

This will host the application at [http://127.0.0.1:80](http://127.0.0.1:80)

An overview of the docker-compose files can be found (here)[docker-compose.md]

## Without Docker
To run the application without Docker, look through the Dockerfile within
the web directory of the project. This will list the step by step
instructions that docker takes to setup the project. These steps can
be taken manually to setup the application.