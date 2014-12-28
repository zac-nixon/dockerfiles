To start a master:

```
docker run \
  -d \
  -p 4505:4505/tcp \
  -p 4506:4506/tcp \
  -v /dev/log:/dev/log \
  -v /etc/salt:/etc/salt \
  -v /srv/salt:/srv/salt \
  -v /var/cache/salt:/var/cache/salt \
  -v /var/log/salt:/var/log/salt \
  -h salt \
  --restart on-failure:10 \
  --name salt-master \
  --link redis:redis \
  voxxit/salt master
```

To start a minion:

```
docker run \
  --restart on-failure:10 \
  --detach \
  -v /dev/log:/dev/log \
  -v /etc/salt:/etc/salt \
  -v /srv/salt:/srv/salt \
  -v /var/cache/salt:/var/cache/salt \
  -v /var/log/salt:/var/log/salt \
  --name salt-minion \
  --link redis:redis \
  voxxit/salt minion
```