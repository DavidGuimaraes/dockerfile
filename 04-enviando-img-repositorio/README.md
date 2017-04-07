## Enviando a imagem para um repositório

O Docker possui um repositório central onde se pode disponibilizar suas imagens online (hub.docker.com -> store.docker.com), mas também podemos criar um repositório privado, a empresa que administra o docker disponibiliza um chamado registry, mas podemos utilizar outras ferramentar como o nexus ou o artifactory.

No nosso caso iremos utilizar o nexus como exemplo, disponível no endereço `10.100.11.69:8082`.

_Obs.: Para acessar a interface administrativa do nexus utilizar o endereço `http://10.100.11.69:8081` (Login e senha de rede)._


1. Gerar uma tag da imagem
```bash
$ docker tag base-img 10.100.11.69:8082/base-img:1.0
$ docker tag base-img 10.100.11.69:8082/base-img:latest
```
_Porque criar duas tags? Uma com versão `1.0` e outra `latest`?_

2. Fazer o push para o repositório
```bash
$ docker push 10.100.11.69:8282/base-img
```
_Obs.: Se não for especificada uma versão será enviadas todas as imagens que não estão sincronizadas com o servidor._
