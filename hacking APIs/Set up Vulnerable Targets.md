
## The completely ridiculous API (crAPI)
https://github.com/OWASP/crAPI

To use the latest stable version.
```
curl -o docker-compose.yml https://raw.githubusercontent.com/OWASP/crAPI/main/deploy/docker/docker-compose.yml

docker-compose pull

docker-compose -f docker-compose.yml --compatibility up -d
```

To Stop and Cleanup crAPI
```
docker-compose -f docker-compose.yml --compatibility down --volumes
```

Visit [http://localhost:8888](http://localhost:8888/)

**Note**: All emails are sent to mailhog service by default and can be checked on [http://localhost:8025](http://localhost:8025/) You can change the `smtp` configuration if required however all emails with domain **example.com** will still go to `mailhog`.


## Juice shop
```
$ docker pull bkimminich/juice-shop
$ docker run --rm -p 80:3000 bkimminich/juice-shop
```
Juice Shop and Damn Vulnerable GraphQL Application (DVGA) both
run over port 3000 by default. To avoid conflict, the -p 80:3000 argument in
the docker-run command sets Juice Shop up to run over port 80 instead.
To access Juice Shop, browse to http://localhost.



## PIXI
```
$ git clone https://github.com/DevSlop/Pixi.git
$ cd Pixi
$ sudo docker-compose up
```



## Damn Vulnerable `GraphQL` Application
`DVGA` is a deliberately vulnerable `GraphQL` application
`GraphiQL` is one of the more popular `GraphQL IDEs` you will come across.
To download and launch `DVGA`, run the following commands from your host terminal:
```
$ sudo docker pull dolevf/dvga
$ sudo docker run -t -p 5000:5000 -e WEB_HOST=0.0.0.0 dolevf/dvga
```



## See running compose process
```
sudo docker-compose ps 
```

## Stop running compose process
```
sudo docker-compose stop
```

## Down the containers
The `docker-compose down` command stops and deletes the containers networks, volumes and images defined in your `docker-compose.yml` file.

The `docker-compose stop` command stops containers associated with services defined in the `docker-compose.yml` file, without deleting other resources such as networks, volumes, etc.

By using `docker-compose down`, we can be sure that our environment is in a clean state, ready to be rebuilt from scratch.

More https://medium.com/@laurap_85411/docker-compose-stop-vs-down-e4e8d6515a85 


for more see:
https://www.youtube.com/watch?v=yJ0Ypcm7eDM


----
