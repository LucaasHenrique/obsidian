***
**Criado em**: 2025-07-01  
**Modificado em**: 13:55
**Topico**: #docker
***
### Docker Compose

> Docker compose é uma ferramenta para definição e execução de múltiplos containers Docker. Com ela é possível configurar todos os parâmetros necessários para executar cada container a partir de um arquivo de definição.

**docker-compose.yml** -> 
> O padrão YAML utiliza a indentação como separador dos blocos de códigos das definições, por conta disso o uso da indentação é um fator muito importante, ou seja, caso não a utilize corretamente, o docker-compose falhará em sua execução.

esquelo padrão: 

```yml 
services:
	web:
		build:
			context: ./dir
			dockerfile: Dockerfile-alternate
			args:
				version: 1
		ports:
			- "5000:5000"
	redis:
		image: redis
```

![[Pasted image 20250701142242.png]]


## 12 Factor

>The Twelve-Factor app” (12factor) é um manifesto com uma série de boas práticas para construção de software utilizando formatos declarativos de automação, maximizando portabilidade e minimizando divergências entre ambientes de execução, permitindo a implantação em plataformas de nuvem modernas e facilitando a escalabilidade.

### CodeBase

- tem o objetivo de facilitar o controle das mudanças de codigo, viabilizando a rastreabilidade das alterações, ou seja, indica que cada aplicação deve ter somente uam base de codigo e, partindo dessa, ser implementada em diferentes ambientes. 

> O Docker tem possibilidade de utilizar variável de ambiente para parametrização da infraestrutura. Sendo assim, a mesma aplicação terá comportamento distinto com base no valor das variáveis de ambiente.

### Dependência

> essa boa prática sugere a declaração de todas as dependências necessárias para executar o código. Você não deve assumir que algum componente já está previamente instalado no ativo responsável por hospedar a aplicação.

### Configurações

> O objetivo da boa prática é viabilizar a configuração daaplicação sem a necessidade de modificar o código. Já que, o comportamento da aplicação varia de acordo com o ambi- ente onde é executada, as configurações devem considerar o ambiente

	ex: onfiguração de banco de dados que, normalmente, são diferentes entre ambientes.

### Serviços de apoio

