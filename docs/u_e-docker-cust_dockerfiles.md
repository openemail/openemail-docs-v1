Make your changes in `data/Dockerfiles/$service` and build the image locally:

```
docker build data/Dockerfiles/service -t openemail/$service
```

Now auto-recreate modified containers:

```
docker-compose up -d
```
