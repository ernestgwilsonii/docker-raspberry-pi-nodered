###################################
# NodeRED Docker for Raspberry Pi #
#        REF: https://nodered.org # 
###################################


###############################################################################
# Docker build
# REF: https://hub.docker.com/r/arm32v7/node
#time docker build --no-cache -t ernestgwilsonii/docker-raspberry-pi-nodered:0.20.5 -f Dockerfile.armhf .
time docker build -t ernestgwilsonii/docker-raspberry-pi-nodered:0.20.5 -f Dockerfile.armhf .
docker images

# Verify 
docker run -it -p 1880:1880 ernestgwilsonii/docker-raspberry-pi-nodered:0.20.5
# From another ssh session:
#docker ps

# Upload to Docker Hub
docker login
docker push ernestgwilsonii/docker-raspberry-pi-nodered:0.20.5
###############################################################################


###############################################################################
# First time setup #
####################
# Create bind mounted directory
sudo mkdir -p /opt/node-red

##########
# Deploy #
##########
# Deploy the stack into a Docker Swarm
docker stack deploy -c docker-compose.yml nodered
# docker stack rm nodered

# Verify
docker service ls | grep nodered
docker service logs -f nodered

# http://IPAddress:1880
###############################################################################
