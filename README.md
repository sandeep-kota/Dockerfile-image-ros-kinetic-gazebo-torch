## Instructions to build the docker Image

To build the docker image using the given dockerfile run the following commands in a new termninal in this directory.

```
cd CMSC818B_WS/
docker build -t ubuntu-16.o4-rl-env -f ros-kinetic-gazebo=dockerfile .
```

## Instructions to run a container with gui 

First run a container instance in interactive mode by running the following command in a terminal.
```
docker run --name baxter_rl_container -it --env NVIDIA_DRIVER_CAPABILITIES=all  --gpus all --runtime=nvidia --net=host --env="DISPLAY"  --env="QT_X11_NO_MITSHM=1" --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" -v /home/default/CMSC818B_WS/:/home/$(whoami)/CMSC818B_WS/  ubuntu-16.04-rl-env:latest 
```

To enable gazebo,rviz visulaizations, start the container with xhost permissions. 
```
export containerId=$(docker ps -l -q)
xhost +local:`docker inspect --format='{{ .Config.Hostname }}' $containerId`
docker start -i $containerId
```
