***
**Criado em**: 2025-06-24  
**Modificado em**: 18:51
**Topico**: #docker
***
Docker é uma plataforma aberta, criada com o objetivo de facilitar o
desenvolvimento, a implantação e a execução de aplicações em ambientes isolados.
### VIRTUALIZÃO

- O modelo de isolamento utilizado no Docker é a virtualização
  a nível do sistema operacional, um método de virtualização 
  onde o kernel do sistema operacional permite que múltiplos
  processos sejam executados isoladamente no mesmo host.
  Esses processos isolados em execução são denominados no
  Docker de container.
***
```docker 
docker image list
```

retorna imagens presentes no docker host

```docker 
docker image pull python
```

atualiza a imagem selecionada
***
```docker  
docker container run <parâmetros> <imagem> <CMD> <argumentos>
```

![[Captura de tela de 2025-06-24 19-20-37.png]]
***
## Mapeamento de Portas

O mapeamento de portas cria uma "ponte" entre uma porta na sua máquina host (o computador onde o Docker está instalado) e uma porta específica dentro do contêiner. Quando o tráfego chega à porta da sua máquina host que você mapeou, o Docker o redireciona para a porta correspondente dentro do contêiner.

``` docker
docker container run -it --rm -p 80:8080 python
```
***
## Gerenciamento de recursos

Para limitar o uso de memória RAM que pode ser utilizada por esse container, basta executar o comando abaixo:

```docker
docker container rut -it --rm -m 512M python
```

Para balancear o uso da CPU pelos containers, utilizamos especificação de pesos para cada container, quanto menor o peso, menor sua prioridade no uso. Os pesos podem oscilar de 1 a 1024.

```docker
docker container run -it --rm -c 512 python
```

Para entendimento, vamos imaginar que três containers foram colocados em execução. Um deles tem o peso padrão 1024 e dois têm o peso 512. Caso os três processos demandem toda CPU o tempo de uso deles será dividido da seguinte maneira:

	• O processo com peso 1024 usará 50% do tempo de processamento
	• Os dois processos com peso 512 usarão 25% do tempo de
	processamento, cada.
***
## Lista de containers

```docker
docker container ls <pam>
```

![[Pasted image 20250626180805.png]]
***
## Gerenciamento de Containers

desligar um container: 
```docker
docker container stop <PID/name>
```

reiniciar o container desligado:

```docker
docker container start <PID/name>
``` 

não recomendado reiniciar um container desligado
***
[[docker 002]]
