```
//remove all process containers
$ docker rm -v $(docker ps -a -q)
//remove all images
$ docker rmi $(docker images -q)

//docker build
// -t <name of the image>
// .  #location of Dockerfile
$ docker build -t ds/workers .
```
