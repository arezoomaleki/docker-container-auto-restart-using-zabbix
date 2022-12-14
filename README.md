# docker-container-auto-restart-using-zabbix
# Docker Container restart using Zabbix agent 2 in failure condition

<h3> Prerequirements: </h3><br />
1- Zabbix Server <br />
2- Docker server include containers <br />
3- Zabbix agent 2 install on Docker Server <br />
<br />
<br />
 <h2> Step 1: [How to install zabbix Agent 2] </h2><br />
Do these steps on Docker Server (the server you need to monitor and execute commands on it): <br />
<br />
  1- wget https://repo.zabbix.com/zabbix/6.0/ {Choose based on your Zabbix Server Linux and Version} <br />
  2- dpkg -i zabbix-release_*.deb <br />
  3- apt update <br />
  4- apt install zabbix-agent2 <br />
  5- nano /etc/zabbix/zabbix-agent2.conf <a href="https://github.com/arezoomaleki/docker-container-auto-restart-using-zabbix/blob/main/zabbix_agent2.conf">(based on the file uploaded above)</a> <br />
  6- useradd -a -G docker zabbix <br />
  7- systemctl restart zabbix_agent2.service <br />
<br />
<br />
To test your settings you can install zabbix_get utility on your Zabbix Server and try to execute this command: <br />
  zabbix_get -s Docker-Server-IP -p 10050 -k system.run["echo 123"] <br />
 <br />
<h2> Step2: [How to add operation and action in Zabbix Server] </h2> <br />
   1- In Zabbix Server Web Panel, go to Administration > scripts > create script <br />
   2- Choose a name and select action operation and script then enter your script <br />
   3- to restart all docker containers (running and stopped), plese enter this command: "docker restart $(docker ps -a -q)" <br />
   4- Then go to Configurations > Actions > Trigger actions and add a new one <br />
   5- then 	choose your conditions (for example I used "Container {#NAME}: Container has been stopped with error code" and "Container {#NAME}: An error has occurred in         the container" from "Docker by Zabbix agent2" template </br>
   6- and set you script in Operation detailes tab.
