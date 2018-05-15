[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: https://sourceforge.net/projects/nntp2nntp/
[hub]: https://hub.docker.com/r/linuxserver/nntp2nntp/


[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png?v=4&s=4000)][linuxserverurl]


## Contact information:- 

| Type | Address/Details | 
| :---: | --- |
| Discord | [Discord](https://discord.gg/YWrKVTn) |
| Forum | [Linuserver.io forum][forumurl] |
| IRC | freenode at `#linuxserver.io` more information at:- [IRC][ircurl]
| Podcast | Covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation! [Linuxserver.io Podcast][podcasturl] |


The [LinuxServer.io][linuxserverurl] team brings you another image release featuring :-

 + regular and timely application updates
 + easy user mappings
 + custom base image with s6 overlay
 + weekly base OS updates with common layers across the entire LinuxServer.io ecosystem to minimise space usage, down time and bandwidth
 + security updates

# linuxserver/nntp2nntp
[![](https://images.microbadger.com/badges/version/linuxserver/nntp2nntp.svg)](https://microbadger.com/images/linuxserver/nntp2nntp "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/linuxserver/nntp2nntp.svg)](https://microbadger.com/images/linuxserver/nntp2nntp "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/linuxserver/nntp2nntp.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/linuxserver/nntp2nntp.svg)][hub][![Build Status](https://ci.linuxserver.io/buildStatus/icon?job=Docker-Builders/x86-64/x86-64-nntp2nntp)](https://ci.linuxserver.io/job/Docker-Builders/job/x86-64/job/x86-64-nntp2nntp/)

NNTP2NNTP Proxy allow you to use your NNTP Account from multiple systems, each with own user name and password. It fully supports SSL and you can also limit the access to proxy with SSL certificates. NNTP2NNTP Proxy is very simple and pretty fast.

[![nntp2nntp](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/nntp2nntp-banner.png)][appurl]

&nbsp;

## Warning

Whilst we know of no NNTP2NNTP security issues the upsteam code for this project has recieved no changes since 06.08.15 and is likely abandonded permanently. For this reason we strongly recommend you do not make this application public facing and if you must do so other layers of security and SSL should be considered a bare minimum requirement. We see this proxy being used primarily on a LAN so that all the users NNTP applications can share a common set of internal credentials allowing for central managment of the upstream account e.g change provider, server, thread limits for all applicaitons with one global config change


&nbsp;

## Usage

```
docker create \
--name=nntp2nntp \
-v </path/to/config>:/config \
-e PGID=<gid> -e PUID=<uid> \
-e TZ=<timezone> \
-p 1563:1563 \
linuxserver/nntp2nntp

```

&nbsp;

## Parameters

The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.



| Parameter | Function |
| :---: | --- |
| `-p 1563` | the port(s) |
| `-v /config` | Configuration file location |
| `-e PUID` | for UserID, see below for explanation |
| `-e GUID` | for GroupID, see below for explanation |
| `-e TZ` | for setting timezone information, eg Europe/London |

&nbsp;

## User / Group Identifiers

Sometimes when using volumes (`-v` flags) permissions issues can arise between the host OS and the container, we avoid this issue by allowing you to specify the user `PUID` and group `PGID`.

Ensure any volume directories on the host are owned by the same user you specify and it will "just work" &trade;.

In this instance `PUID=1001` and `PGID=1001`, to find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

&nbsp;

## Setting up the application

Edit sample config file `config/nntp2nntp.conf` with upstream provder details and local users.

New user passwords can be created by entering the container `docker exec -it nntp2nntp /bin/bash` and executing `/usr/bin/nntp2nntp.py pass` followed by `exit`



&nbsp;

## Container access and information.

| Function | Command |
| :--- | :--- |
| Shell access (live container) | `docker exec -it nntp2nntp /bin/bash` |
| Realtime container logs | `docker logs -f nntp2nntp` |
| Container version number | `docker inspect -f '{{ index .Config.Labels "build_version" }}' nntp2nntp` |
| Image version number |  `docker inspect -f '{{ index .Config.Labels "build_version" }}' linuxserver/nntp2nntp` |

&nbsp;

## Versions

|  Date | Changes |
| :---: | --- |
| 15.05.18 |  Initial Release. |
