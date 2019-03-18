# laravel-docker
Docker running Nginx, PHP-FPM, MySQL, PostgresDB, MongoDB, Redis

# Configurações

Passo a passo de como usar docker

## Baixe o app do docker

É necessario criar uma conta!

https://hub.docker.com/editions/community/docker-ce-desktop-mac

## Adicione os path's onde estão o projeto infofin e a pasta do docker-laravel

![Scheme](//i.imgur.com/325OcVmg.png)

## .env

Dentro do projeto do docker renomeie o arquivo *env-example*  para *.env* e substitua dentro dele `APPLICATION` com o path de onde esta o projeto. 

Ex `APPLICATION=/private/var/www/nome_projeto` (não é aconselhável ficar dentro de `/Documents`, caso for MAC)

Coloque nas variáveis do `mysql` e `mongo` os respectivos users e senhas desejados no `.env`:

Ex.: `MONGODB_USER=root`

## hosts

No arquivo de hosts do sistema, coloque o host desejado:

Ex.: `127.0.0.1 nomedesjado`

Deve-se modificar também no arquivo de configuração do nginx, linha 3 (não e necessário mudar o nome do arquivo, mas pode se quiser)

Localizado no projeto docker-laravel em nginx -> sites -> nomedesjado.conf

    server_name nomedesjado; #linha 3

## Execução

Na raiz do projeto do docker-laravel execute o seguinte comando. Isso pode levar um tempo considerável a primeira vez

    docker-compose up -d

Depois execute 

    docker-compose exec php-fpm composer install
    
E também

    docker-compose exec php-fpm php artisan key:generate
    
## More..

Todo comando a ser executado no projeto (composer, artisan, etc) deve ser executado na raiz do projeto do docker pois la está o arquivo `docker-compose.yml` que traduz esse comando para dentro da imagem virtualizada do php onde realmente o projeto esta rodando

O comando desejado deve ser sempre antecipado de: 

       docker-compose exec php-fpm comandoaqui

Comandos do docker:

**PS.: Visual Studio tem uma extensão oficial do Dokcer para fazer tudo isso com interface**

https://docs.docker.com/engine/reference/commandline/docker/

remove todas as imagens

     docker rmi $(docker images -a -q)

parar e remover todos os containers

    -   docker stop $(docker ps -a -q)
    -   docker rm $(docker ps -a -q)
