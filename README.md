# rpi-minecraft

A nice and easy way to get a Minecraft server up and running using docker on a Raspberry Pi. For help on getting started with docker see the [official getting started guide][0].
For more information on Minecraft and check out it's [website][1].


## Building rpi-minecraft

Running this will build you a docker image with the latest version of both
rpi-minecraft and Minecraft itself.

    git clone https://github.com/kroonwijk/rpi-minecraft
    cd rpi-minecraft
    sudo docker build -t kroonwijk/rpi-minecraft .


## Running rpi-minecraft

Running the first time will set your port to a static port of your choice so
that you can easily map a proxy to. If this is the only thing running on your
system you can map the port to 25565 and no proxy is needed. i.e.
`-p=25565:25565` . If you want to enable the query protocol you need
to add another -p=25565:25565/udp to forward the UDP protocol on the
same port as well.
Also be sure your mounted directory on your host machine is
already created before running `mkdir -p /mnt/minecraft`.

    sudo docker run -d=true -p=25565:25565 -v=/mnt/minecraft:/data kroonwijk/rpi-minecraft /start

From now on when you start/stop rpi-minecraft you should use the container id
with the following commands. To get your container id, after you initial run
type `sudo docker ps` and it will show up on the left side followed by the
image name which is `kroonwijk/rpi-minecraft:latest`.

    sudo docker start <container_id>
    sudo docker stop <container_id>


### Notes on the run command

 + `-v` is the volume you are mounting `-v=host_dir:docker_dir`
 + `kroonwijk/rpi-minecraft` is simply what I called my docker build of this image
 + `-d=true` allows this to run cleanly as a daemon, remove for debugging
 + `-p` is the port it connects to, `-p=host_port:docker_port`


### Credits

Image based on [overshard/docker-minecraft][2]

[0]: http://www.docker.io/gettingstarted/
[1]: http://minecraft.net/
[2]: https://github.com/overshard/docker-minecraft/
