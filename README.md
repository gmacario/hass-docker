# home-assistant-compose

Clone (or update) the project repository

```
[ ! -e home-assistant-compose ] && \
git clone https://github.com/gmacario/home-assistant-compose
cd home-assistant-compose && git pull --all --prune
```

Start a Docker machine (in this example, a local VirtualBox VM)

```
docker-machine start default
eval $(docker-machine env default)
```

Bring up the services

```
docker-compose up -d
```

Inspect the Home Assistant configuration directory

```
docker-compose exec -T ha ls -la /config
```

**NOTE**: If you are running the shell from MS Windows and the `docker exec` command
fails, prepend it with `winpty`.

Display Home Assistant logfile

```
docker-compose exec -T ha tail -f /config/home-assistant.log
```

Cleanup Home Assistant logfile

```
docker-compose exec -T ha sh .c ". >/config/home-assistant.log"
```

Backup the configuration file

```
docker exec -T ha cat /config/configuration.yaml >hass-backup-configuration.yaml
```

Install the configuration file fetched from some private URL
(restart Home Assistant to apply the new configuration):

```
curl -L <URL> | \
    docker-compose exec -T ha sh -c "cat >/config/configuration.yaml" && \
    docker-compose restart
```

Browse `http://$(docker-machine ip):8123/` (for instance: <http://192.168.99.100:8123>)
to access the Web interface of Home Assistant.


### See also

* Home Assistant homepage: <https://home-assistant.io/>
* How to Install Home Assistant on a Raspberry Pi using HASSbian: <https://www.youtube.com/watch?v=iIz6XqDwHEk> (YouTube video, 05:26)
* Manual Installation on a RPi3: <https://home-assistant.io/getting-started/installation-raspberry-pi/>
* PyGen (tool for creating HASSbian images): <https://github.com/home-assistant/pi-gen>
* Home Assistant inside a Docker Container: <https://home-assistant.io/docs/installation/docker/>
* GitHub: <https://github.com/home-assistant/home-assistant>

### Licensing

home-assistant-compose is licensed under and Open Source license. See [LICENSE](LICENSE) for the full license text.

Copyright 2017, [Gianpaolo Macario](https://gmacario.github.io/)

<!-- EOF -->
