# Docker for Laravel

### Obiettivi:

1. Rendere identici gli ambienti di development
2. Rendere identico l'ambiente di development e il production
3. Eseguire la Continous Integration in un ambiente identico a development e production

### Steps

#### 1. Importare `laradock`

Includere nella root di progetto Laravel il `submodule` [`tiknil/laradock`](https://github.com/tiknil/laradock):

```
git submodule add https://github.com/tiknil/laradock.git
```

#### 2. Impostare riferimento a `.env` locale

1. Spostarsi all'interno della cartella di `laradock`
2. Eseguire il comando:

```
ln -s ../.env .env
```

Questo creerà un link virtuale tra l'`.env` di progetto e le configurazioni dei container in docker.

#### 3. Configurazione `.env`

* Configurare il proprio `.env` locale affinché sia impostato come le configurazioni del docker, quindi:
 * `DB_HOST=mysql` per la connessione al database (user: `homestead`, pw: `secret`, vedi `mysql/Dockerfile` o `docker-compose.yml`)
 * Valorizzare: `SERVER_ALIAS`, `SERVER_PORT`, `SERVER_SSL_PORT`
 * Valorizzare `DB_PORT`, `DB_DATABASE`, `DB_PASSWORD` e `DB_USERNAME` se si vogliono dei valori diversi da quelli di default

#### 4. Impostazione host personalizzato, ad es: `local.project.net`

Modificare il file `hosts` locale (solitamente il percorso è `/etc/hosts` e serve accedere come `sudo` per modificare) inserendo:

```
127.0.0.1	local.project.net
```

Riavviate i container docker e accedete al sito tramite il dominio che avete configurato.

#### 5. Avviare i container docker

Per avviare i container docker eseguire (ad esempio):

```
docker-compose up -d apache2 mysql php-worker
```

Una volta eseguito dovrebbe essere possibile raggiungere la radice del progetto nel proprio browser all'indirizzo:
`http://$SERVER_ALIAS:$SERVER_PORT`, ad esempio: `http://local.project.net:8888`

> [http://local.project.net:8888](http://local.project.net:8888)


#### 6. Eseguire comandi per inizializzazione progetto

Accedere al terminale del "container" che permette l'esecuzione dei comandi sul progetto
```
docker-compose exec workspace bash
```

e quindi eseguire tutto quello che serve (se non è già stato fatto in locale):

```
composer install
php artisan migrate
php artisan db:seed
...
```

## Comandi docker

Per fermare il docker:
```
docker-compose stop
```

Per cancellare i docker creati:
```
docker-compose down
```

Per rendere attive le  modifiche effettuate sui file `Dockerfile` dei container è necessario eseguire:
```
 docker-compose build --no-cache [container-name]
 ```
 il parametro `[container-name]` è uguale al nome della cartella relativa al container

## Utilies

#### Connettersi al DB MySQL con SequelPro

Semplicemente connessione locale con Host: 127.0.0.1, Username - il valore di `DB_USERNAME` nel file `.env` - e pw `DB_PASSWORD` in `.env`. Questo vale se la porta configurata per l'accesso a MySql è quella di default (3306). altrimenti è la porta configurata in `DB_PORT` in `.env`.

#### Mostrare il log di un container
 Per mostrare nel terminale il log di un container eseguire:
 ```
 docker logs [image-laradock-name]
 ```
 L'elenco dei container attivi si ottiene eseguendo:
 ```
 docker ps
 ```
 La colonna `IMAGE` è il parametro da inserire come `[image-laradock-name]`
