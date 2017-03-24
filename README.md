# How to run them

Create the container and give it a random port:

```bash
docker build -t ubuntu-ssh .
docker run -d -P ubuntu-ssh
```

To find the IP and port associated, run:

```bash
for i in $(docker ps -q); do docker port "$i"; done
```

It will print the docker port associated to the port inside
the container. The address may be `0.0.0.0`, if so, check
`ifconfig` for the docker network and check what the IP is
there. If this is a node where all the containers are running
then you can use `localhost`.
