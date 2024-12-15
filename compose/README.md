# Getting Started
Run the compose file using the following command:

`podman compose -f <compose-file.yaml> up -d`

I still need to work on setting up yaml files so I can store secrets (usernames and passwords) on separate files. Until then, the username is `<service>` and the password is `<service>_pass`.

# Compose Template
Below is a template I wrote years ago. This can serve as a template for most services I plan to run in the future.
```
version: "3"

services:
	
  # sample_container - short description of sample container
  sample_container:
    image: sample_image
    resources:
      limits:
        cpus: '0.001'
        memory: 25M
      reservations:
        cpus: '0.0001'
        memory: 10M
    container_name: sample_container
    hostname: sample_container
    restart: # depends on restart policy
    networks:
      sample_network:
        ipv4_address: 172.20.1.2
    ports:
    	- HostPort:ContainerPort
    dns:
      - IP_Address_Of_DNS_Server
    environment:
      - TZ=UTC
      - KEY=VALUE
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
