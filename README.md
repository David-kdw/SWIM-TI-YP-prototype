# SWIM deployment

## Prerequisites
Before start make sure the following software is installed on your machine:
    
   - [git](https://git-scm.com/downloads)
   - [docker](https://docs.docker.com/install/)
   - [docker-compose](https://docs.docker.com/compose/install/)

### Preparation

#### Download repositories
First you need to clone the repositories in the current directory
```shell
git clone https://antavelos-eurocontrol@bitbucket.org/antavelos-eurocontrol/subscription-manager.git &&
git clone https://antavelos-eurocontrol@bitbucket.org/antavelos-eurocontrol/swim-adsb.git &&
git clone https://antavelos-eurocontrol@bitbucket.org/antavelos-eurocontrol/swim-explorer.git
```

#### Configuration
##### Environment variables
Make sure that the following enviroment variables are set.
```shell
export SM_ADMIN_USERNAME=<sm_admin_username>
export SM_ADMIN_PASSWORD=<sm_admin_password>
export SWIM_ADSB_USERNAME=<swim_adsb_username>
export SWIM_ADSB_PASSWORD=<swim_adsb_password>
export SWIM_EXPLORER_USERNAME=<swim_explorer_username>
export SWIM_EXPLORER_PASSWORD=<swim_explorer_password>
```

##### RabbitMQ certificates
In order to enable TSL access to RabbitMQ you need to provide some certificates. You can create self signed certificates
using this [tool](https://github.com/michaelklishin/tls-gen). The following commands will generate and prepare the 
certificates that will be used:
```shell
git clone https://github.com/michaelklishin/tls-gen.git
cd tls-gen/basic
make PASSWORD=swim-ti CN=rabbitmq
mkdir /secrets
cp ./result/* /secrets
```


##### Config files


### Deployment

Build the images of `rabbitmq`, `subscription-manager`, `swim-adsb` and `swim-explorer` 
(this is an one time thing but it's gonna take some time depending on the machine it run on and the internet 
connection):
```shell
docker-compose build
```

Start all the services:

```shell
docker-compose up -d
```