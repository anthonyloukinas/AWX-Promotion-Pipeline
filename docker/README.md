# AWX Promotion Pipeline - Docker

## Compose Files

`jenkins-compose.yml`

This compose file sets up a basic running Jenkins server on port :8089. Browse to http://localhost:8089

```bash
# Create Jenkins Data/Home Volume
docker volume create jenkins_home

# Create docker container service
docker-compose -f jenkins-compose.yml up -d
```