see  
https://github.com/dunglas/mercure/issues/60#issuecomment-472310410
```
$ git clone https://github.com/dunglas/mercure
$ cd mercure
$ GO111MODULE=on go get
$ GO111MODULE=on go build
```

```
docker run -it --name golang-build  -v ${PWD}:/home/mercure golang bash
cd /home/mercure
CGO_ENABLED=0
GO111MODULE=on go get
GO111MODULE=on go build
docker build -t registry.coruja.studio/monstrum/mercure-hub:latest .
```

Example Docker compose
```
service:
  ccl-hub:
    image: monstrum/mercure:v0.10.3
    environment:
      JWT_KEY=file:///public.key
      JWT_ALGORITHM=RS512
    volumes:
      - ./mercure/public.key:/public.key
```
Using config / secrets
```
service:
  ccl-hub:
    image: monstrum/mercure:v0.10.3
    secrets:
      - source: mercure-hub-public.key
        target: /public.key
    environment:
      JWT_KEY=file:///public.key
      JWT_ALGORITHM=RS512
```
