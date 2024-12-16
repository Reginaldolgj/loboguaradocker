# Lobo Guará Project

Leia sobre o projeto [loboguara](https://loboguara.olivsec.com.br/docs/index.html).

## Requisitos

Instalar o [docker](https://docs.docker.com/engine/install/).

```Script
    curl -sSL https://get.docker.com/ | sh
    systemctl start docker
```

Instalar o [docker-compose](https://docs.docker.com/compose/).

```Script
    curl -L "https://github.com/docker/compose/releases/download/v2.12.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    chmod +x /usr/local/bin/docker-compose
```

## Uso

``` Download
git clone https://github.com/Reginaldolgj/loboguaradocker.git
```
    
Editar o lobo/config.py conforme o tutorial [12. Configure the config.py File](https://loboguara.olivsec.com.br/docs/lobo_guara_installation_manual_on_Ubuntu_24-04.html#12-configure-the-configpy-file)

``` Executar docker compose
docker-compose up -d --build 
```

```Verificar os containers: lobo e postgres
docker ps
```
    Resultado:
        ... NAMES
            lobo
            postgres


``` Instalar e executar
docker exec -it postgres psql -h localhost -U guarauser -d guaradb -c "CREATE EXTENSION pg_trgm;" && \
docker exec -it lobo /home/ubuntu/loboguara/install.sh && \ 
docker exec -it lobo sudo -u loboguara /opt/loboguara/start.sh
```

```Criar admin
http://0.0.0.0:7405/admin
```
```Login
http://0.0.0.0:7405/login
```

Remove
docker-compose down
docker image rm loboguaradocker-main-lobo_guara loboguaradocker-main-postgres
docker volume rm loboguaradocker-main_postgres_data

