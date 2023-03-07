# The IT Nerd - Magento 2.4.5 Docker
Este é um projeto 100% Open source que tem como objetivo facilitar o desenvolvimento de magento.

Todas as contribuições são bem vindas.

## Serviços inclusos
- PHP 8.1
- MariaDB 10.4
- Nginx + SSL
- Varnish com bypass para xdebug
- OpenSearch (com plugins para ElasticSuite)
- Redis 6.2
- MailHog

## Como usar 
Com o Docker instalado clone os arquivos projeto na parta root do seu projeto Magento.

### Iniciar serviços

```
docker-compose up -d
```
### Parar serviços

```
docker-compose stop
```
### Apagar serviços
Use este comando somente quando precisar recriar o ambiente, pois o mesmo apaga os containers e seus discos.
Sendo assim todos os dados do OpenSearch e MariaDB serão perdidos.

```
docker-compose down -v
```


### Acesso ao cli da aplicação
Para rodar comandos do cli do magento (bin/magento) rode o seguinte comando.
```
docker-compose compose exec php bash
```

### Próximos passos
- Finalizar configuração do xDebug
- Implementar RabbitMQ
- Documentar comando de install do magento
- Documentar arquivo padrão de config (app/etc/env.php) 
- Criar chaves de ssl durante o build