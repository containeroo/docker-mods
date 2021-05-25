# Containeroo Docker-Mods

## Available Mods

Containeroo offers the following docker-mods for linuxserver.io images:

### sabnzbd-nzbnotify

This mod installs nzb-notify.

### sabnzbd-mkvtoolnix

This mod installs mkvtoolnix.

## Using a Mod

Source: https://github.com/linuxserver/docker-mods/blob/master/README.md

Before consuming a Docker Mod ensure that the source code for it is publicly posted along with it's build pipeline pushing to Dockerhub.

Consumption of a Docker Mod is intended to be as user friendly as possible and can be achieved with the following environment variables being passed to the container:

* DOCKER_MODS- This can be a single endpoint `user/endpoint:tag` or an array of endpoints separated by `|` `user/endpoint:tag|user2/endpoint2:tag`
* RUN_BANNED_MODS- If this is set to any value you will bypass our centralized filter of banned Dockerhub users and run Mods regardless of a ban

Full example:

```bash
docker create \
  --name=sabnzbd \
  -e DOCKER_MODS=containeroo/docker-mods:sabnzbd-nzbnotify \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Europe/London \
  -p 6789:6789 \
  -v <path to data>:/config \
  -v <path/to/downloads>:/downloads \
  --restart unless-stopped \
  linuxserver/sabnzbd
```

This will spinup a sabnzbd container and apply the custom logic found in this repository.
