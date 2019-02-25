###################################
# NodeRED Docker for Raspberry Pi #
#        REF: https://nodered.org # 
###################################


###############################################################################
# Docker build
time docker build --no-cache -t ernestgwilsonii/docker-raspberry-pi-nodered:19.06 -f Dockerfile.armhf .
docker images

# Verify 
docker run -it -p 1880:1880 ernestgwilsonii/docker-raspberry-pi-nodered:19.06
# From another ssh session:
#docker ps

# Upload to Docker Hub
docker login
docker push ernestgwilsonii/docker-raspberry-pi-nodered:19.06
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
