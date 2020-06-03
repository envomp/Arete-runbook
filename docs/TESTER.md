# Deploying Arete

You need latest of: Docker, docker-compose

You can install them with

```shell script
apt install docker.io
apt install docker-compose
```

Every component can be ran separately. Just create a new docker-compose file and run it in a different machine. 
Just make sure the ports are url's are configured correctly.
To deploy Arete in a single machine, run the following. 

```shell script
git clone https://github.com/envomp/arete
cd arete
<edit .env file so that ARETE_HOME is same as the folder you are in.>
docker-compose up -d
<Copy the contents of .ssh to the created ssh folder>
```

Frontend will be running on ```localhost:1080```

Backend will be running on ```localhost:8001```

Tester will be running on ```localhost:8098```

By default, admin username and password will be ```admin``` and ```admin``` respectively. It can be configured in the docker-compose.yml file with other passwords, urls and ports.

Some useful curl commands to test arete whether it's working correctly
----
```shell script
Force an update on a test:
curl -d '{"project":{"url":"git@gitlab.cs.ttu.ee:iti0102-2019/ex.git","path_with_namespace":"iti0211-2019/ex"}}' -X POST -H "Content-Type: application/json" localhost:8098/tests:update

Force an update on a image
curl -X POST -H "Content-Type: application/json" localhost:8098/image/python-tester:update

Test something sync
curl -d '{"testingPlatform":"prolog","gitTestSource":"https://gitlab.cs.ttu.ee/iti0211-2019/tests","gitStudentRepo":"https://gitlab.cs.ttu.ee/envomp/iti0211-2019.git","uniid":"envomp"}' -X POST -H "Content-Type: application/json" localhost:8098/:testSync
```

cleanup (kill all containers, networks, volumes, images)
```shell script
./docker_cleanup.sh
```

# Integrating Arete to a custom service

Currently supported endpoints
----

Schemas can be generated from arete/api/data ```/request``` and ```/response```

* put
    * /image/{image}
    * /tests

* post
    * /:testAsync or /test
    * /:testSync or /test/sync
    * /tests:update
    * /image/{image_name}:update
        * java-tester
        * python-tester
        * prolog-tester

* get
    * /submissions/active
    * /logs
    * /state

Schemas
----

Schema for /tests:update endpoint is attainable [from here.](../schemas/arete/request/AreteTestUpdateSchema.json)

Schema for /:testAsync and /:testSync endpoints are attainable [from here.](../schemas/arete/request/AreteRequestSchema.json)

Schema for testing response body is attainable [from here.](../schemas/arete/response/responseSchema.json)

