# server-status-app

## Rodando o projeto

### Usando Maven + Spring Boot action 


Rodar o projeto
```shell
mvn spring-boot:run
```

[Acesse](http://localhost:8080/)


Parar o projeto
```shell
mvn spring-boot:stop
```

### Usando Maven + Jar

Gerar o arquivo jar
```shell
mvn clean install
```

Executar o projeto
```shell
java -jar target/server-status.jar  
```

[Acesse](http://localhost:8080/)


### Usando Docker

```shell
docker run  --name server_status_docker -p 8080:8080 andrefelix/server-status:V2
```

[Acesse](http://localhost:8080/)

### Usando Docker-compose

```shell
docker-compose -f docker/docker-compose.yaml up
```

[Acesse](http://localhost:8080/)


```shell
docker-compose -f docker/docker-compose.yaml down
```


## Deploy no ElasticBeanstalk

1. Instalar o Beanstalk command line
    https://docs.aws.amazon.com/pt_br/elasticbeanstalk/latest/dg/eb-cli3.html
   
1. Configurar a aplicação. Será criado um arquivo: ```.elasticbeanstalk/config.yml```
    ```
    eb init
    ```

1. Adicione esta linhas ao seu arquivo .elasticbeanstalk/config.yml    
   ```
        deploy:
            artifact: target/server-status.jar
   ```
1. Criar o ambiente. 
    ```
    eb create
    ```
   
1. Definir a variável de ambiente para acesso à aplicação. 

    ```eb setenv SERVER_PORT=5000```

1. Fazer o deploy

    ```eb deploy```

1. Verificar o status do deploy

    ```eb status```

1. Abrir a aplicação.

    ```eb open```

1. Criar mais de uma instância.

    ```eb scale 2```
   
1. Terminar todas as instâncias. Adicione (--force) para evitar a confirmação.

    ```eb terminate --all``` 
    
    
  ##  Gerando a image Docker do projeto

  ### Criar a imagem localmente

  `docker build -t andrefelix/server-status:v5 .`

  ### Enviar a imagem para o DockerHub

  `docker push andrefelix/server-status:v5`

  
