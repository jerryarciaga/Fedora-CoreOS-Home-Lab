# My Docker Compose Template
## Purpose
Since Docker Compose YAML files can be written in many different ways, I came up with a template aiming to simplify and standardize the way I write `docker_compose.yaml`. This way, I would be able to write and customize my future docker container builds with ease.
## Template
### Version
Most of the time, `version: "3"` is pretty much standard until Docker releases a later version.
### Services
The services profile contains:
* A short description of my container as a comment.
* The **container** name.
* The **image** it was based in.
* The container's **hostname**. For simplicity's sake, I tend to name it the same as the container/image name.
* **CPU Usage**
* **Memory Limit** `mem_limit`, the maximum memory limit to avoid crashing
* Restart policy if applicable.
* **Networks**: because I have a DNS sinkhole as one of my containers, I would specify a static IP address for each container.
* **Ports**: Remember to open up ports in the firewall whenever you do map ports from host to container.
* **DNS**: specify `pihole`'s static IP address.
* **Environment**:  Environmental variables such as `TZ`(timezone)
* **Volumes**: Read through the docker image's manual on what locations are ideal to mount.
### Volumes
Be sure to specify any used volumes here. Also remember to mount the right device (usually an external drive) to `/var/lib/docker/volumes`
### Networks
Specify a good subnet or two and ensure that your containers are within the specified subnet.

```
version: "3"

services:
	
	# sample_container - short description of sample container
	sample_container:
		image: sample_image
		container_name: sample_container
		hostname: sample_container
        cpus: "0.5"
        mem_limit: 30m
		restart: # depends on restart policy
		networks:
			sample_network:
				ipv4_address: 172.20.1.2
		ports:
			# - HostPort:ContainerPort
		dns:
			# - IP_Address_Of_DNS_Server
		environment:
			- TZ=UTC
			# - VARIABLE=VALUE
		volumes:
			- sample_volume:/sample_mount
	
volumes:
		sample_volume:

networks:
	sample_network:
		ipam:
			driver: default
			config:
				- subnet: 172.20.1.0/24
```
