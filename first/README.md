
## What is Docker
- Docker는 containerized process로 가상 환경을 제공해주는 오픈소스 플랫폼입니다.
- Docker는 pivot-root, namespace, cgroup을 사용해 유저 레벨의 격리 환경을 제공합니다.
- 반면 가상 머신(VM)은 하이퍼 바이저 위에 os레벨부터 격리 환경을 제공하여 격리 수준은 Docker보다 높은 수준을 제공하지만, 격리 수준으로 인한 오버헤드가 더 큽니다.

![image](https://github.com/user-attachments/assets/713a4449-a72c-4789-81a6-28807a22eae3)

- Docker는 Client, Server 구조로 통신은 default로 Unix socket(AKA Unix domain docker)을 사용한다. unix docker는 root user, sudo를 통해서만 unix socket을 접근할 수 있다. 즉, docker daemon은 root로 실행됩니다.
- How Unix domain socket works
  - Process 간 IPC(inter-process communication) 통신을 위해 도입되었습니다.
  - Loopback TCP/IP vs IPC: Loopback TCP/IP 통신을 더 많은 layer를 거치기 때문에 느립니다. -> [Detail](compare.protocol.md)
  - Unix domain docker 공유: 컨테이너가 host docker의 unix docket 공유해서 Docker 실행 (DooD)
```shell
docker run --rm -it -v /run/docker.sock:/run/docker.sock -v /usr/bin/docker:/usr/bin/docker ubuntu:latest bash
$ docker info
$ docker run -d --rm --name webserver nginx:alpine
$ docker ps
$ docker rm -f webserver
$ docker ps -a
$ exit
```
- Useful docker commands
  ```
  docker ps
  docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' $(docker ps -q)
  docker logs <container id>
  docker exec <container id> <cmd>
  ```
- Useful docker tool: [dive](https://github.com/wagoodman/dive)

  
