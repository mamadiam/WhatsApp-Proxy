# WhatsApp-Proxy
Configuring WhatsApp proxy using cloud-init on ubuntu

Deploy a Whatsapp proxy server on Linux (Tested on Ubuntu)</br></br>
For this you need a VPS Service that gives you `cloud-init` feature.</br></br>
For example, [Digital Ocean](https://www.digitalocean.com/) has cloud-init feature called `Add Initialization scripts`</br>
Note: You can start with the most basic VPS.</br></br>
Share it with your loved ones</br></br>
<bold>#MahsaAmini</bold></br>
<bold>#womanlifefreedom</bold></br></br>
<hr>

I'm going to walk you through installing this proxy. </br>
for the sake of simplicity, I'm using digital ocean.</br></br>

## Digital Ocean </br>

1. Login to digital ocean</br>
2. In Droplets > Create Droplets</br>
3. After choosing the location, ubuntu version, resources, ... click on the `Advanced Options` and check the `Add Initialization scripts (free)`.</br>
4. Now copy/paste the code below.</br>
#### 5. whatsapp.yaml </br>
```shell script
#cloud-config

package_update: true
package_upgrade: true

packages:
 - ca-certificates
 - curl
 - gnupg
 - lsb-release
 - git
 
runcmd:
  - sudo mkdir -p /etc/apt/keyrings
  - curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
  - echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  - sudo apt-get update
  - sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
  - git clone https://github.com/WhatsApp/proxy.git $HOME/whatsapp-proxy
  - docker compose -f $HOME/whatsapp-proxy/proxy/ops/docker-compose.yml up -d
``` 
</br>
6. Click on `Create Droplet`</br>
7. Just give it a minute so the script execute.</br>
8. Now log into the server.</br>

#### 9.  Run the following command 
```shell script
tail -f /var/log/cloud-init-output.log
``` 
</br>
By default, it will run the proxy on ports: 80, 443, and 5222. </br>
If you don't want it to expose on ports 80, 443 before you run the script navigate to this directory and change the ports in docker-compose file.</br>

```shell script
cd ~/whatsapp-proxy/proxy/ops/docker-compose.yml
```
</br> 
11. Now, go to whatsapp and put your IPv4 address + port into the proxy section.</br>
And that's it. :)
</br></br>
Just in case you want to support me, I'd realy appriciate it.</br></br>

TRC20 `TT2AMeebAUGFcG9jLPA49xN1eMCyDekz6c` </br>

ERC20 `0x9A6471A8d01A66e81433d97aF3e1288f7C2E6a7b`
