## vault-docker-lsnr-issue
### Instruction to test

#### start vault and other containers
```
docker-compose up -d
```
#### check port 822[01] status on vault container
```
docker-compose exec vault netstat -an | grep 822
```
#### curl from whitelisted container
```
docker-compose exec test-whitelisted curl 172.16.238.2:8220/v1/sys/health
```
#### check port 822[01] status on vault container
```
docker-compose exec vault netstat -an | grep 822
```
#### curl from blacklisted container (fails and listener port goes down)
```
docker-compose exec test-blacklisted curl 172.16.238.2:8220/v1/sys/health
```
#### check port 822[01] status on vault container (8220 is down on IP 172.16.238.2).
```
docker-compose exec vault netstat -an | grep 822
```
#### curl from whitelisted container again (this will fail)
```
docker-compose exec test-whitelisted curl 172.16.238.2:8220/v1/sys/health
```
#### stop
```
docker-compose down
```
