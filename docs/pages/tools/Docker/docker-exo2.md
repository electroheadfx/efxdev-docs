# Docker exo with Dockerfile and compose

## App

> Create app.py :

```python
from flask import Flask
from redis import Redis, RedisError
import os
import socket

# Connect to Redis
redis = Redis(host="redis", db=0, socket_connect_timeout=2, socket_timeout=2)

app = Flask(__name__)

@app.route("/")
def hello():
    try:
        visites = redis.incr("compteur")
    except RedisError:
        visites = "<i>Erreur de connection Redis, compteur desactive</i>"

    html = "<h3>Bonjour {nom}!</h3>" \
           "<b>Hostname:</b> {hostname}<br/>" \
           "<b>Visites:</b> {visites} <br/>" \
           "<p>Abonne toi!</p>"
    return html.format(nom=os.getenv("NOM", "youtube"), hostname=socket.gethostname(), visites=visites)

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

> Create requirements.txt

```bash
cat <<EOF > requirements.txt
Flask
Redis
EOF
```

## Dockerfile

> Setup `Dockerfile` :

```dockerfile
# start from python slim image
FROM python:2.7-slim
# definite the working directory on the image : root/app
WORKDIR /app
# copy all file from current repo to /app
COPY . /app
# install python libs from requirements.txt
RUN pip install -r requirements.txt
# expose to the web (port 80)
EXPOSE 80
# setup env variable nom=coca
ENV NOM coca
# execute app.py with python at container creation
CMD ["python", "app.py"]
```

> Create the Docker Image with:

```bash
# create `monimage` from current directory 
# where Dockerfile exist
docker build -t monimage .
```

## Docker-compose

> Create now `docker-compose.yml` :

```yml
version: "3"
services:
  monapp:
    image: monimage
    depends_on:
      - redis
    ports:
      - "80:80"
    networks:
      - monreseau
    environment:
      - NOM=les amis
  redis:
    image: redis
    networks:
      - monreseau

networks:
  monreseau:
```

> We create here 2 services and the networks

- `monapp` :  Create container from from our `monimage` created previously.
  
  it depends of `redis`  service into `monreseau` network

- `redis` :  Create container from `redis` into `monreseau`

- `monreseau` network declared

## Run the container with compose

```bash
# it mount containers and create the services
docker-compose up
```

### Run the app on : http://localhost:80 !

[GitHub](https://github.com/ttwthomas/apprendre-docker)

[Video](https://www.youtube.com/watch?v=dWcoIxRfs8Y&list=PL8SZiccjllt1jz9DsD4MPYbbiGOR_FYHu&index=3)
