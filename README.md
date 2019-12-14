##### Local docker with postgres ####

You need latest of: Docker

```shell script
git clone https://github.com/envomp/arete
docker login -u automatedtestingservice -p $DOCKER_PASSWORD
docker-compose up -d
```

cleanup
```shell script
./docker_cleanup.sh
```