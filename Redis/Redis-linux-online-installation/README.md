# Redis Cluster
## 1. Installation steps 
```
yum -y install wget
wget https://raw.githubusercontent.com/UiPath/Infrastructure/master/Redis/Redis-linux-online-installation/redis-installer.sh
chmod +x redis-installer.sh
sudo ./redis-installer.sh
```
## 2. Test the installation
- Test the Redis cluster
```
redis-cli -p 6379 -h <redis_master_ip>
incr testvalue
<ctrl+C>
```
- Test the state of the master : you need to have the following values
    - num-slaves : 2
    - num-other_sentinels : 2
    - quorum : 2
    - flags : master
```
redis-cli -p 16379 -h <redis_master_ip>
sentinel master redis-cluster
```
- Get somes validations : master's IP/port, slaves and sentinels informations
```
sentinel get-master-addr-by-name redis-cluster
sentinel slaves redis-cluster
sentinel sentinels redis-cluster
<ctrl+C>
```

## 3. Simulate the failover
- On the current master sentinel :
```
debug sleep 30
```
- Verify the change of master sentinel on the other slaves

