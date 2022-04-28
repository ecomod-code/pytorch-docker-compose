# pytorch-docker-compose
docker-compose version of sinzlab/pytorch-docker with nginx and letsencrypt



# Setup

Create a server with the most recent Ubuntu and make sure that the ports 80, 443 and 22 are open. SSH into your server, change the password and update all packages:

```
sudo apt update && sudo apt -y dist-upgrade # might be blocked due to auto update... just be patient
```

## Install docker:

```
sudo apt -y install curl gnupg2 apt-transport-https ca-certificates  software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

sudo apt update
sudo apt -y install docker-ce
```

## Install docker-compose

Have a look at https://github.com/docker/compose/releases and see which is the most recent release. At the time of this writing, it is version  `1.29.1`

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod a+x /usr/local/bin/docker-compose

docker-compose --version  # just checkin'
```

# Clone this repository

```bash
git clone https://github.com/ecomod-code/pytorch-docker-compose.git && cd pytorch-docker-compose
```

 # Quick Start

* create a `.env` file from the template `cp .env-template .env`
* Edit the environment file, e.g. `nano .env`
	* `Server_URL` is the domain name of your server (e.g. `my-server.uni-goettingen.de`)
	* `Jupyter_Password` will be the password for your JupyterLab Server. Choose a strong password as your server is available from the Internet
	* your `e_mail_address` will be associated with the generated certificates for the encrypted connection to your server. It does not generate Spam you will just be notified when your certificate is about to expire
* Save your changes `Ctrl+O` and exit the editor `Strl+X`
* Run `sudo docker-compose up -d` to start the containers
