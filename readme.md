# Complete guide for setting up asp.net core 2.2 server on linux with nginx and jenkins

### This guide will allow you to set up a asp.net core project on a linux server so it is ready for production. It will use nginx as proxy server and forward to asp.net core running on kestrel. Jenkins will run on subdomain so it allows for ci/cd configurations. This guide will use Digitial Ocean server. 

-----

### prerequisite
1. A domain bought at any domain provider
2. 


----
## First create a droplet and a domain dns 

The first thing we're going to do is to create a droplet. I will not go in depth with the settings, because this is entirely up to you.

Once the droplet is created you have to create some dns records. You'll need a "NS" record directing respectively to ns1.digitalocean.com, ns2.digitalocean.com and ns3.digitalocean.com. 
And a "A" record directing the domain name to the ip address/droplet you have created. At the hostname you can enter @ and direct the domain name to the droplet. If you want any subdomains you'll have to create them there as well. In this guide i will use a subdomain directing to the droplet on jenkins.DOMAIN.eu. 

If you experince any trouble during this there is a lot of guides out there you can search for.


## SSH into the the linux server and install dotnet sdk package. 

The first thing we are going to do is to ssh into our linux server. this is done with the following command:

```bash

ssh root@YOUR_DROPLET_IP 
```
The very first time you login to you're droplet, you have to either add the password for the ssh key you added during the setup of the droplet or enter the root password which can be found at the droplets informations. 

A guide upon that can be found here : [https://www.digitalocean.com/docs/droplets/how-to/connect-with-ssh/openssh/](https://www.digitalocean.com/docs/droplets/how-to/connect-with-ssh/openssh/)




``` bash
sudo service nginx stop
sudo systemctl stop identity.service
cd /var/www/build/LogisticSolution/LogisticSolutions.Identity
dotnet publish --output /var/www/prod
sudo systemctl start identity.service
sudo service nginx start


```
