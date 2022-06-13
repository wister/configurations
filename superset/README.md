# Installation and Running of Superset

```
docker pull apache/superset
docker run -d -p 8080:8088 --name superset apache/superset
docker exec -it superset superset fab create-admin --username admin --firstname Superset --lastname Admin --email wisterfungfung@gmail.com --password admin
docker exec -it superset superset db upgrade
docker exec -it superset superset load_examples
docker exec -it superset superset init
```

# Runnning

> Cannot see share and see dashboards without account. Refs: [one](https://superset.apache.org/docs/security/#public)

We need to set `PUBLIC_ROLE_LIKE = "Gamma"` in `superset/config.py`. Which is line `310`. But first we need nano, or your prefered terminal text editor.

```
docker exec -u 0 -it superset bash
cd superset
cat config.py | grep -n "PUBLIC"
nano config.py
```

After that, you have to set Permissions to `Public` role `can access datasource` of your dataset.
