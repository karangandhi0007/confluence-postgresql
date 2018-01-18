# confluence-postgresql


Confluence PostgreSQL Running Inside Docker Container 

# Pre-requisite

- Install Docker 17.12
- Install Docker Compose

# Clone the Repo

```
$git clone https://github.com/dockerworx/confluence-postgresql
```
# Edit the docker-compose.yml file according to the network
```
 - Under Confluence Service , add the ip address of the confluence container .
 Example :
 services:
  confluence:
    image: blacklabelops/confluence
    container_name: confluence
    hostname: confluence
    networks:
      confluencenet:
        ipv4_address: 192.168.10.24 --------> Change this to required IP
    volumes:
      - confluencedata:/var/atlassian/confluence
 ```
 ```
-  No Ip Address required under Postgres service , so Hash out the line
 Example :
 postgresql:
    image: blacklabelops/postgres
    container_name: postgres
    hostname: postgres
    networks:
      confluencenet:
        #ipv4_address: 192.168.10.25 ------> Hash Out this line
    volumes:
      - postgresqldata:/var/lib/postgresql/data
 
- Change the network part of the docker compose file by adding subnet and gateway
Example:
networks:
  confluencenet:
    driver: bridge
    ipam:
      config:
        - subnet: 192.168.10.255/24 ----> Change to required CIDR netmask
          gateway: 192.168.10.1    ------> Change to required Gateway IP
```


# Run the below command:

```
docker-compose up
```
