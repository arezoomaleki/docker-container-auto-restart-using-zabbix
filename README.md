# docker-container-auto-restart-using-zabbix
Docker Container restart using Zabbix agent 2 in failure condition

Prerequirements:
1- Zabbix Server
2- Docker server include containers
3- Zabbix agent 2 install on Docker Server

Step 1: [How to install zabbix Agent 2] 
Do these steps on Docker Server (the server you need to monitor and execute commands on it):

  wget wget https://repo.zabbix.com/zabbix/6.0/ {Choose based on your Zabbix Server Linux and Version}
  dpkg -i zabbix-release_*.deb
  apt update
  apt install zabbix-agent2
  nano /etc/zabbix/zabbix-agent2.conf (based on uploaded file above)
  useradd -a -G docker zabbix
  systemctl restart zabbix_agent2.service

To test your settings you can install zabbix_get utility on your Zabbix Server and try to execute this command:
  zabbix_get -s Docker-Server-IP -p 10050 -k system.run["echo 123"]
 
 Step2: [How to add operation and action on zabbix]
   1- In Zabbix Server Web Panel, go to Administration > scripts > new script
   
  
