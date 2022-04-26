### docs
- https://akhq.io/docs/
- https://github.com/tchiotludo/akhq

### start 
```shell
brew install zookeeper
brew install kafka

brew services restart zookeeper
brew services restart kafka

vi /opt/homebrew/etc/zookeeper/zoo.cfg
admin.serverPort=8082 # default: 8080

sudo vi /etc/hosts
127.0.0.1 host.docker.internal

vi /opt/homebrew/etc/kafka/server.properties
listeners=PLAINTEXT://localhost:9092
advertised.listeners=PLAINTEXT://host.docker.internal:9092

vi /tmp/application.yml
akhq:
  connections:
    local:
      properties:
        bootstrap.servers: "host.docker.internal:9092"
      schema-registry:
        url: "http://host.docker.internal:8081"

docker run \
    --name akhq \
    -d \
    -p 8080:8080 \
    -v /tmp/application.yml:/app/application.yml \
    tchiotludo/akhq
```
