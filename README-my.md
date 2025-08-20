## Setup 
1. I made sure C:\users\lzinger\.docker 
contains an empty config file:
```json
{}
```

2. I installed new Go version 1.24.1
3. In docker desktop I set Resources > File Sharing to include C:\Dev\ratelimit
4. I made changes to docker-compose-example.yml to fit to my Windows environment
5. I ran docker-compose -f docker-compose-example.yml up --build --remove-orphans
6. I set inside C:\Dev\ratelimit\examples\ratelimit\config  the example configuration described in the readme.
7. I modified proxy.yml to support the two types of rate limits per request: one per minute and one per second.
8. I cleared the cache from Redis from time to time , if I wanted to start the counting from scratch:
```bash
docker exec -it ratelimit_redis_1 redis-cli flushall
```
Sometimes when it didn't work, I had to perform:
```bash
docker volume prune -f
docker image prune -a -f
```
9. I experimented limits by running the example:
```bash
    curl -i http://localhost:8888/api/sets/123/other
    curl -i http://localhost:8888/api/sets/123/internal/config
````
10. I watched metrics at http://localhost:9102/metrics