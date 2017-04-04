### 1. `Dockerfile` simples

* Criando uma imagem e nomeando a mesma
```bash
$ docker build -t base-img .
Sending build context to Docker daemon 3.584 kB
Step 1/5 : FROM alpine
latest: Pulling from library/alpine
627beaf3eaaf: Already exists 
Digest: sha256:58e1a1bb75db1b5a24a462dd5e2915277ea06438c3f105138f97eb53149673c4
Status: Downloaded newer image for alpine:latest
 ---> 4a415e366388
Step 2/5 : MAINTAINER "Rafael Ramos <arkanjo.ms@gmail.com>"
 ---> Running in b21982ea2a99
 ---> a57ea4226878
Removing intermediate container b21982ea2a99
Step 3/5 : RUN echo "Criando minha primeira imagem!"
 ---> Running in 837cdcf1f4a5
Criando minha primeira imagem!
 ---> d8cb30f53720
Removing intermediate container 837cdcf1f4a5
Step 4/5 : ONBUILD cmd echo "Comando executado em outro container!"
 ---> Running in 45586fb4998b
 ---> 0f9984af5ad9
Removing intermediate container 45586fb4998b
Step 5/5 : CMD echo "Executando o container"
 ---> Running in 6b48671b25b0
 ---> 4796558f957a
Removing intermediate container 6b48671b25b0
Successfully built 4796558f957a
```

* Listando imagens local
```bash
$ docker images
REPOSITORY                 TAG                 IMAGE ID            CREATED             SIZE
[...]
base-img                   latest              4796558f957a        41 seconds ago      3.98 MB
[...]
```

* Rodando container
```bash
$ docker run base-img
Executando o container
```
