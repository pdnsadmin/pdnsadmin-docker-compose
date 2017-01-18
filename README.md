# pdnsAdmin-Docker-Compose

Using docker-compose to compile all component into one that easy to deploy a testing environment for pdnsadmin application.
Run the latest version of the PowerDNS, MySQL v5.7 and pdnsAdmin with Docker.


### Build and start services

```
docker-compose stop
docker-compose rm
docker-compose build
docker-compose up
```

### Create the first domain with pdnsAdmin

Open URL on Browser to start setting up pdnsAdmin. Database credential could be found at ```database.env```. Just need to follow setup steps.
```
http://localhost:8088/setup
```

[pdnsAdmin document](http://doc.pdnsadmin.com/) to know how to get it up and running.


### Create the first domain on command line to test PowerDNS

```
curl -X POST --data '{"name":"example.local", "kind": "Native", "masters": [], "nameservers": ["ns1.example.local", "ns2.example.local"]}' -v -H 'X-API-Key: powerdnsapikey' $DOCKER_IP/servers/localhost/zones
curl -X PATCH --data '{"rrsets": [ {"name": "example.local", "type": "A", "changetype": "REPLACE", "records": [ {"content": "127.0.0.1", "disabled": false, "name": "example.local", "ttl": 86400, "type": "A", "priority": 0 } ] } ] }' -H 'X-API-Key: changeme' $DOCKER_IP/servers/localhost/zones/example.local
```


### Dig the domain

```
dig example.local @$DOCKER_IP
```


### Docker IP

When using docker-machine, this will come in handy:
```
export DOCKER_IP=$(docker-machine ip)
```
