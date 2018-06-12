[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: http://www.minetest.net/
[hub]: https://hub.docker.com/r/lsioarmhf/minetest/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/minetest
[![](https://images.microbadger.com/badges/version/lsioarmhf/minetest.svg)](https://microbadger.com/images/lsioarmhf/minetest "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/minetest.svg)](https://microbadger.com/images/lsioarmhf/minetest "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/minetest.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/minetest.svg)][hub][![Build Status](https://ci.linuxserver.io/buildStatus/icon?job=Docker-Builders/armhf/armhf-minetest)](https://ci.linuxserver.io/job/Docker-Builders/job/armhf/job/armhf-minetest/)

[Minetest][appurl] (server) is a near-infinite-world block sandbox game and a game engine, inspired by InfiniMiner, Minecraft, and the like.

[![minetest](https://raw.githubusercontent.com/linuxserver/beta-templates/master/lsiodev/img/minetest-icon.png)][appurl]

## Usage

```
docker create \
  --name=minetest \
  -v <path to data>:/config/.minetest \
  -e PGID=<gid> -e PUID=<uid>  \
  -p 30000:30000/udp
  lsioarmhf/minetest
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`



* `-p 30000/udp` - the port(s)
* `-v /config/.minetest` - where minetest stores config files and maps etc.
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it minetest /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application
`IMPORTANT... THIS IS THE ARMHF VERSION`

You can find the world maps, mods folder and config files in /config/.minetest.

## Info

* Shell access whilst the container is running: `docker exec -it minetest /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f minetest`

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' minetest`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/minetest`

## Versions

+ **12.06.18:** Build from release tag as currently master doesn't build in alpine.
+ **03.01.18:** Rebase to alpine 3.7, Deprecate cpu_core routine lack of scaling.
+ **30.11.17:** Use cpu core counting routine to speed up build time.
+ **29.05.17:** Rebase to alpine 3.6.
+ **14.02.17:** Rebase to alpine 3.5.
+ **25.11.16:** Initial Release.
