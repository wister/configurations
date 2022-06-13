# Installation

> It's been a pain to find a working, easy, installation guide of [redash](https://redash.io/) in Windows. We will do the Docker approach.

**Solution**: Put the following files in a folder.

#### Files:

- `docker-compose.yml`
- `redash.env`

Run the following commands:

```
docker-compose run --rm server create_db
docker-compose up -d
```

# Testing

After having the container running, go to: `http://localhost:5000/`
