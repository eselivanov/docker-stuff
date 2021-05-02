ref:
https://docs.docker.com/network/network-tutorial-standalone/
https://docs.docker.com/network/bridge/ 

#Change bridge network parameters:
*note: may need to create daemon.json if
 it doesn't exist*
~~~
sudo nano /etc/docker/daemon.json 
~~~
only add paramters that you want to change, 
i.e. bridge subnet ("bip"), that is by default *172.17.0.0/16*
it might be usefull as default may conflic
 with cloud networks 
~~~
{ 
  "log-driver": "journald", 
  "log-opts": { 
    "tag": "{{.Name}}" 
  }, 
  "bip": "172.26.0.1/16", 
  "ipv6": false
} 
~~~
restart docker daemon
~~~
sudo systemctl restart docker
~~~
check docker daemon and it parameters
~~~
sudo systemctl status docker
~~~
check new network on the host

`route` or `netstat -rn`
or `ip a | 'inet '`

inspect new network:
~~~
docker network ls
docker network inspect bridge
~~~
