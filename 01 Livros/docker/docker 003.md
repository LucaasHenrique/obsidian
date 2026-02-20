***
**Criado em**: 2025-06-30  
**Modificado em**: 13:54
**Topico**: #docker
***
### Redes Padrões

```docker 
docker network ls
```

out: 
``` bash
NETWORK ID     NAME      DRIVER    SCOPE
09dff77b9b83   bridge    bridge    local
157551ea2d17   host      host      local
cc727fd3a689   none      null      local
```

#### Bridge 
Essa é a rede padrão para qualquer container. A rede confere ao container uma interface que faz bridge com a interface docker0 do docker host. Essa interface recebe,
automaticamente, o próximo endereço disponível na rede IP 172.17.0.0/16.

todos os containers nessa rede via protocolo TCP/IP. Sabendo o endereço de IP do container desejado é possível enviar trafego para ele.
****
#### None
tem como objetivo isolar o container para comunicações externas. A única interface rede IP será a localhost

normalmente utilizada para redes que manipulam apenas arquivos sem necessidade de envia-los pela rede para outro local.
***
#### Host

> Essa rede tem como objetivo entregar para o container todas as interfaces existentes no docker host. De certa forma, pode agilizar a entrega dos pacotes, uma vez que não há bridge no caminho das mensagens. Mas normalmente esse overhead é mínimo e o uso de uma brigde pode ser importante para segurança e gerência do seu tráfego.

#### Redes definidas pelo usuário

> Cada rede criada por usuário deve estar associada a um determinado driver. E, caso você não crie seu próprio driver, deve escolher entre os drivers disponibilizados pelo docker:

##### Bridge 
-  é o driver de rede mais simples de utilizar, pois demanda pouca configuração
- bridge driver != rede bridge
- usuário com o driver bridge poderá utilizar o DNS interno do Docker que, associa, automaticamente, todos os nomes de containers dessa rede para seus respectivos IPs da rede IP correspondente.

```bash 
docker network create --driver bridge isolated_nw
```

iniciando container:

```bash
docker run -itd --net isolated_nw alpine sh
```

um container em uma determinada rede nao pode acessar outro container em uma rede diferente msm conhecendo o IP de destino. É necessario que a origem esteja em nas duas rede que deseja alcançar.

> Os containers que estão na rede isolated_nw podem expor suas portas no docker host e essas portas podem ser acessadas tanto por containers externos a rede, chamada isolated_nw, como máquinas externas com acesso ao docker host.

Para descobrir os containers associados a uma determinada rede:

```bash 
docker network inspect isolated_nw
```

#### Overlay

esse driver permite a comunicação entre hosts docker, utilizando-o os containers de um determinado host docker poderão acessar, nativamente, containers de um outro ambiente docker.
***
[[docker 004]]
