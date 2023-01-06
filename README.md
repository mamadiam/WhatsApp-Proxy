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
7. Now all you need to do is copy the `IPv4` from you server and paste it into the whatsapp `setting`.</br></br>

And it's done. :)
