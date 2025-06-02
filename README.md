# App Microservices

project dengan pola arsitektur microservice dengan komunikasi _asynchronous_ dan menggunakan api gateway **Krakend**

run project

```docker
docker compose up
```

## KrakenD Gateway

menerapkan **_flexible config_**, jadi config merupakan hasil generate `krakend.tmpl` tamplate

### environtment

secara default menggunakan env staging, jika ingin mengubah ke env lain dapat diubah pada docker compose bagian env krakend

`FC_SETTINGS=gateway/config/settings/{env}`

pastikan env setting ada. list yang ada saat ini :

- staging (default), menggunakan docker network
- dev, menggunakan external (diluar docker)

### struktur folder

```
gateway/
├── config/
│   └── partials/               # other utils config
│   └── settings/               # data untuk tiap env
│   └── templates/
│       └── endpoints.tmpl      # main endpoints
│       └── ...
│
├── krakend.tmpl                # main config tamplate
├── out.json                    # file hasil auto generate dari tamplate
```

## MongoDB

untuk url mongoDB:

```
<!-- docker network, sesuaikan dengan container name -->
mongodb://<username>:<password>@mongo:27017/<db name>?authSource=admin

<!-- expose port -->
mongodb://<username>:<password>@localhost:27017/<db name>?authSource=admin
```

## Services

list service

### Service User Auth

store config ada di `services/auth-user/.env`

#### requiretmen

- diperlukan private dan public keys di dalam folder `keys`
