# Docker
```bash
# --- Containers ---
docker --help                                               # Show help for the `docker` command
docker COMMAND --help                                       # Show help for the specific COMMAND

docker ps --all                                             # List all container instances
docker ps --all --filter "KEY=VALUE"                        # List all container instances matching the specified KEY=VALUE filter
                                                            #   (See https://docs.docker.com/engine/reference/commandline/docker for details)

TODO: "docker run"

TODO: "docker inspect"

TODO: "docker log"

TODO: "docker rm"
docker rm CONTAINER_ID                                      # Delete container with CONTAINER_ID
docker rm --volumes CONTAINER_ID                            # Delete container with CONTAINER_ID and its respective volumes

TODO: "docker prune/perge"

# --- Images ---
docker image ls                                             # List all images (hiding intermediate images)
docker image ls --all                                       # List all images (showing intermediate images)
                                                            #   --all | -a        
docker image ls NAME:TAG                                    # List images by NAME:TAG
                                                            #   Use asterisk (*) as wildcard for full or partial NAME or TAG
docker image ls --filter "KEY=VALUE"                        # List all images matching the specified KEY=VALUE filter
                                                            #   --filter | -f     

docker image save --output ARCHIVE IMAGE [IMAGE...]         # Save one or more IMAGE(S) to an ARCHIVE
                                                            #   --output | -o     File to write to (instead of STDOUT)

docker image load --input ARCHIVE                           # Restore IMAGE(S) from an ARCHIVE
                                                            #   --input | -i      ARCHIVE to read from (instead of STDIN)

docker image prune                                          # Remove unused images (will prompt for confirmation)
docker image rm IMAGE_ID                                    # Remove image with the specified IMAGE_ID

# --- Volumes ---
docker volume ls                                            # List all volumes
docker volume ls --filter  "KEY=VALUE"                      # List all volumes matching the specified KEY=VALUE filter
                                                            #   --filter | -f     

docker volume prune                                         # Remove all unused local volumes (will prompt for confirmation)
docker volume rm VOLUME_ID                                  # Remove volume with the specified VOLUME_ID

# --- Networks ---
docker network ls                                           # List all networks
```


### Procedures
```bash
# Login to AWS ECR via command line
1. _set up aws credentials_
2. get login: `aws ecr get-login --no-include-email`

   which returns something like...

    docker login -u AWS -p KEY https://<account_number>.dkr.ecr.<region>.amazonaws.com

3. copy, paste, and run the previously returned command:
    `docker login -u AWS -p KEY https://<account_number>.dkr.ecr.<region>.amazonaws.com`

    which should return something like...

      ``
```

---

### Best Practices
* Give each container explicit names
* Prefer using ... volumes over ... volumes

---
_**TODO - document the following commands**_

`sudo docker ps -a --filter status=exited | [ $(grep "" -c) -gt 1 ] && sudo docker rm -v $(sudo docker ps -a --filter status=exited -q) || echo 'No exited container(s) to remove!'`

`sudo docker volume list --filter dangling=true | [ $(grep "" -c) -gt 1 ] && sudo docker volume remove $(sudo docker volume list --filter dangling=true -q) || echo 'No dangling volume(s) to remove!'`

`sudo docker image list --filter dangling=true | [ $(grep "" -c) -gt 1 ] && sudo docker image remove $(sudo docker image list --filter dangling=true -q) || echo 'No dangling image(s) to remove!'`

--------------------------------------------------------------------------------
### Resources
* Docker [Reference documentation](https://docs.docker.com/reference/)
  - [Docker CLI](https://docs.docker.com/engine/reference/commandline/cli/)
