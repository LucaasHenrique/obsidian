***
**Criado em**: 2025-06-26  
**Modificado em**: 18:17
**Topico**: #docker
***
# Criar sua propria imagem no docker

#### Diferença entre imagem e container

> traçando um paralelo com o conceito de **orientação a objeto**, a imagem é a classe e o container o objeto. A imagem é a abstração da infraestrutura em estado somente leitura, de onde será instanciado o container. Todo container é iniciado a partir de uma imagem, dessa forma podemos concluir que nunca teremos uma imagem em execução. Um container só pode ser iniciado a partir de uma única imagem. Caso deseje um comportamento diferente, será necessário customizar a imagem.
***
### Como criar imagens

#### Commit: 

> É possível criar imagens executando o comando commit, relacionado a um container. Esse comando usa o status atual do container escolhido e cria a imagem com base nele.

iniciar um container

```docker
docker container run it --name containercriado ubuntu:16.04 bash
```

instalando nginx

```bash
apt-get update
apt-get install nginx -y
exit
```

parando o container 

```bash
docker container stop containercriado
```

commit 

```bash
docker container commit containercriado meubuntu:nginx
```

imagem criada com o nome meuubuntu:nginx
***
### Dockerfile

Quando se utiliza Dockerfile para gerar uma imagem, basicamente, é apresentada uma lista de instruções que serão aplicadas em determinada imagem para que outra imagem seja gerada com base nas modificações.

imagem base -> dockerfile (modificaçoes) -> imagem modificada

criar dockerfile e escrever os comandos: 

Dockerfile
```docker
1 FROM ubuntu:16.04
2 RUN apt-get update && apt-get install nginx -y
3 COPY arquivo_teste /tmp/arquivo_teste
4 CMD bash
```

**FROM** -> Define a imagem base a partir da qual sua imagem será construída
**RUN** -> Executa comandos dentro da imagem
**EXPOSE** -> Informa qual porta o container ouvira em tempo de execução.
**CMD** -> Define o comando padrão a ser executado quando um contêiner for iniciado a partir desta imagem.

### construir imagem 

```bash
docker image build -t meuubunto:nginx_auto .
```

"." informa que o contexto de criação da imagem deve ser o diretorio atual
***
### Volumes 

> Ao utilizar volumes, o Docker monta essa pasta (camada) no
   nível imediatamente inferior ao do container, o que permite o
   acesso rápido de todo dado armazenado nessa camada (pasta),
   resolvendo o problema de performance.
   O volume também resolve questões de persistência de da-
   dos, pois as informações armazenadas na camada (pasta) do
   container são perdidas ao remover o container, ou seja, ao
   utilizar volumes temos maior garantia no armazenamento
   desses dados

### Mapeamento de Volumes

```bash 
docker volume create --name dbdata
```

> No comando acima, o docker criou um volume que pode ser
   consumido por qualquer container.
   A associação do volume ao container acontece de forma 
   parecida à praticada no mapeamento de pasta do host, pois
   nesse caso você precisa associar o volume a uma pasta dentro
   do container, como podemos ver abaixo:

```bash
docker container run -d -v dbdata:/var/lib/data postgres
```

resumindo, se eu salvar dados no banco dentro do container ao desligar e remover esse container quando eu subir outros esses dados ainda existirão.
***
[[docker 003]]