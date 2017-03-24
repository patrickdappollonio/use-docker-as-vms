# Run docker containers as ssh servers

This is a small proof-of-concept to see how nice
some docker containers behave as if they were Virtual
Machines where you can ssh into them.

There are better solutions out there such as Vagrant
that can perform even better than a container, but this
is just a toy idea to see how good they may perform
in things like running Ansible scripts.

## Setup

Create the container and give it a random port:

```bash
docker build -t ubuntu-ssh .  # this will build the Dockerfile and name it "ubuntu-ssh"
docker run -d -P ubuntu-ssh   # this runs the container and expose the ports with a local, random port
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

An example output is:

```
22/tcp -> 0.0.0.0:32771
22/tcp -> 0.0.0.0:32770
22/tcp -> 0.0.0.0:32769
22/tcp -> 0.0.0.0:32768
```
