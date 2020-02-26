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
2. get login: `aws ecr get-login`

   which returns something like...

    docker login -u AWS -p eyJwYXlsb2FkIjoiT3F5cTMzVEtabU9ueVhUUzgvQ0F2QlJvRTJGZmFia243VDl3czJwQTl2am5EM0g4dnZxV0J5U3c3Ri8rZ0hxQ0V2R0hVTzRJMzNMS1l3c0JYWDIvM2pJRUdWZDllRGJsSEp5U1grOTlsS3pNRi9vOXpJNUtIbHBObXdpTHpTeU43RWxjd210R3lhVHN5WEY3KzIreTlzZkR1NnQwcyt5VXI1a25COVM1MEtRZXZsZ2JDaTdOb3k5U3A2Q3pqMlpXUDJoTGlXcGN2a3RrN2hVdGVuS0hWbms4TkVXZ2drSTd4dVdtSVF1ZC9FRSsyUy9iNmt1OVV5eExnOHI2UXI2QStCZWdXWHV4ZStrSUJSemMyMHVPdUZxZzI5cUk3OGVGS2VRaitEejBSTkFvUGNGRFlPellab2wvZ1JoSWhLTUdkUm1EMXl0d0dtZE1xODF1UjVPeU5jd2c5NXZoRlFQTnVBVGtsRmxUOHRpTkw2ZnNZWnRGNytHd093OXZIUDJZU3RoalkyMTJXb1dNZVI5MlZldE5iSVpjTy9KVGFuaWcyWVVTMlFPN2ovVHpkcHoxU1FDZkphWWt6VC9mQ01WTmE3N3V1S3RORTNwS3ZMbWRERkNWbEI5R0o1QlJYUDNBKzdVNkpTQzNIZ2l1RGJPbkJsMFAzWnQ3Sm4vMnd2b1hjOGJIeDlTNDlHOVY4aXUxUWdub0NsMmVTNVhZbzdlc1htM1VQeWxQYU1WL1FRQWNKd2FINW5jUVZldmF0RXh2ZUFmTG96RndpcmkwdlR6V21LbkROODFQOVdicVJrYWg3YndHU2ZVSy9tQlh2OHZtMFlnQjJGSzJoNEFWdkR1WGFnbzBlUkxVVXVIdFFDaGJ2M0hYSWFjd1hkRlJJOVJ2dUdaY3RqN0lGckhvVWlQSGFDRDVocWd4VGlDdDhsVm44V3ZYMFg5Y1Ntbm0rbGtSRHBoOTgxYXJWU2N1OUQyVE9zaEFOUDlKNnlERGJvY3ZaZzlSME9GRU9HbENCdi8veVJzZnl2TU4rTThadmkxQjM3d2Y1SmFZcEtQRW5sUmxQNE5hWTcvUTBRU210a3RWN0JQaGN3L0RrdGdsWkJUNmd4cGdlVHlRa3JSZzA0KzQ0Yzg0aUhzdnRWOFlaSE1PQlhRbjVhb0xsOENkdTI1b0ZGeHRKNklVZ0g1blNwUEtEVFB3RVR2SURpamtXVElYYUFtRDZabTZlYzgzcVM0U1laSFNERjhKUWppYlZUVlhXYytsbUpYMWZ3TlFJTUgvK05ycFRFc1ljZVZkMFk0MFJpY3RLVUxyUHY0YVZxN0c2UklMTC9KWTJtMGZxLyszSTdPMnhNSlowOTRVbTFudkpzMWpxQXlqTGJDUnJYU0RNQ1picDlub1BWUi9FMENjSkZWR2d6OFVaMUcvenpvcVVIV3JTK2N2RzQ3VDBwN2F4VVRqN0JLNWppQkZvaHJhaHdMYWdrWU43ZURxMDVOditQVG5IYWdVYzIrcmxxSzlWRWJIREVsL0ZHZFd3UjBjdjlQam1tNDU3RnJsV0txVVhBVkZiRUtQMStscTVkb2l4bXRzWEpVNVBaMFRMVFVTVGpyS215VHR2aGVGVFhmclZIUXlTaExnQ3NNNUx1Q1lGdnBWcjNObjBQNEp0endWTDJsMHl5U0c1VkVwd0E9PSIsImRhdGFrZXkiOiJBUUVCQUhoK2RTK0JsTnUwTnhuWHdvd2JJTHMxMTV5amQrTE5BWmhCTFpzdW5PeGszQUFBQUg0d2ZBWUpLb1pJaHZjTkFRY0dvRzh3YlFJQkFEQm9CZ2txaGtpRzl3MEJCd0V3SGdZSllJWklBV1VEQkFFdU1CRUVERUgzelY0RXAvWDZQazlOQ1FJQkVJQTdJSHFtQWx1RjBSdWRlRFNwcnREN0ZkNWpyamdEVlVxOFhTMUJoQnk0a2JLUkFOc1pTdG1tNDdzVVh6UXlVWTZ0eVFoQVVBNUZYbVA0RDBRPSIsInZlcnNpb24iOiIyIiwidHlwZSI6IkRBVEFfS0VZIiwiZXhwaXJhdGlvbiI6MTU4MjE2NjExMH0= -e none https://<account_number>.dkr.ecr.<region>.amazonaws.com

3. copy, paste, and run the previously returned command, but remove `-e none` before running:
    `docker login -u AWS -p eyJwYXlsb2FkIjoiT3F5cTMzVEtabU9ueVhUUzgvQ0F2QlJvRTJGZmFia243VDl3czJwQTl2am5EM0g4dnZxV0J5U3c3Ri8rZ0hxQ0V2R0hVTzRJMzNMS1l3c0JYWDIvM2pJRUdWZDllRGJsSEp5U1grOTlsS3pNRi9vOXpJNUtIbHBObXdpTHpTeU43RWxjd210R3lhVHN5WEY3KzIreTlzZkR1NnQwcyt5VXI1a25COVM1MEtRZXZsZ2JDaTdOb3k5U3A2Q3pqMlpXUDJoTGlXcGN2a3RrN2hVdGVuS0hWbms4TkVXZ2drSTd4dVdtSVF1ZC9FRSsyUy9iNmt1OVV5eExnOHI2UXI2QStCZWdXWHV4ZStrSUJSemMyMHVPdUZxZzI5cUk3OGVGS2VRaitEejBSTkFvUGNGRFlPellab2wvZ1JoSWhLTUdkUm1EMXl0d0dtZE1xODF1UjVPeU5jd2c5NXZoRlFQTnVBVGtsRmxUOHRpTkw2ZnNZWnRGNytHd093OXZIUDJZU3RoalkyMTJXb1dNZVI5MlZldE5iSVpjTy9KVGFuaWcyWVVTMlFPN2ovVHpkcHoxU1FDZkphWWt6VC9mQ01WTmE3N3V1S3RORTNwS3ZMbWRERkNWbEI5R0o1QlJYUDNBKzdVNkpTQzNIZ2l1RGJPbkJsMFAzWnQ3Sm4vMnd2b1hjOGJIeDlTNDlHOVY4aXUxUWdub0NsMmVTNVhZbzdlc1htM1VQeWxQYU1WL1FRQWNKd2FINW5jUVZldmF0RXh2ZUFmTG96RndpcmkwdlR6V21LbkROODFQOVdicVJrYWg3YndHU2ZVSy9tQlh2OHZtMFlnQjJGSzJoNEFWdkR1WGFnbzBlUkxVVXVIdFFDaGJ2M0hYSWFjd1hkRlJJOVJ2dUdaY3RqN0lGckhvVWlQSGFDRDVocWd4VGlDdDhsVm44V3ZYMFg5Y1Ntbm0rbGtSRHBoOTgxYXJWU2N1OUQyVE9zaEFOUDlKNnlERGJvY3ZaZzlSME9GRU9HbENCdi8veVJzZnl2TU4rTThadmkxQjM3d2Y1SmFZcEtQRW5sUmxQNE5hWTcvUTBRU210a3RWN0JQaGN3L0RrdGdsWkJUNmd4cGdlVHlRa3JSZzA0KzQ0Yzg0aUhzdnRWOFlaSE1PQlhRbjVhb0xsOENkdTI1b0ZGeHRKNklVZ0g1blNwUEtEVFB3RVR2SURpamtXVElYYUFtRDZabTZlYzgzcVM0U1laSFNERjhKUWppYlZUVlhXYytsbUpYMWZ3TlFJTUgvK05ycFRFc1ljZVZkMFk0MFJpY3RLVUxyUHY0YVZxN0c2UklMTC9KWTJtMGZxLyszSTdPMnhNSlowOTRVbTFudkpzMWpxQXlqTGJDUnJYU0RNQ1picDlub1BWUi9FMENjSkZWR2d6OFVaMUcvenpvcVVIV3JTK2N2RzQ3VDBwN2F4VVRqN0JLNWppQkZvaHJhaHdMYWdrWU43ZURxMDVOditQVG5IYWdVYzIrcmxxSzlWRWJIREVsL0ZHZFd3UjBjdjlQam1tNDU3RnJsV0txVVhBVkZiRUtQMStscTVkb2l4bXRzWEpVNVBaMFRMVFVTVGpyS215VHR2aGVGVFhmclZIUXlTaExnQ3NNNUx1Q1lGdnBWcjNObjBQNEp0endWTDJsMHl5U0c1VkVwd0E9PSIsImRhdGFrZXkiOiJBUUVCQUhoK2RTK0JsTnUwTnhuWHdvd2JJTHMxMTV5amQrTE5BWmhCTFpzdW5PeGszQUFBQUg0d2ZBWUpLb1pJaHZjTkFRY0dvRzh3YlFJQkFEQm9CZ2txaGtpRzl3MEJCd0V3SGdZSllJWklBV1VEQkFFdU1CRUVERUgzelY0RXAvWDZQazlOQ1FJQkVJQTdJSHFtQWx1RjBSdWRlRFNwcnREN0ZkNWpyamdEVlVxOFhTMUJoQnk0a2JLUkFOc1pTdG1tNDdzVVh6UXlVWTZ0eVFoQVVBNUZYbVA0RDBRPSIsInZlcnNpb24iOiIyIiwidHlwZSI6IkRBVEFfS0VZIiwiZXhwaXJhdGlvbiI6MTU4MjE2NjExMH0= https://<account_number>.dkr.ecr.<region>.amazonaws.com`

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
