# Problems

## Windows

---

> Cannot change docker installation directory. Refs: [one](https://github.com/docker/roadmap/issues/94)

**Solution**: Run these commands to symlink before installing.

```
md "D:\Program Files\Docker\ProgramDataDocker"
md "D:\Program Files\Docker\ProgramDataDockerDesktop"
md "D:\Program Files\Docker\ProgramFiles"
md "D:\Program Files\Docker\RoamingDockerDesktop"
md "D:\Program Files\Docker\RoamingDocker"
md "D:\Program Files\Docker\AppDataDocker"

mklink /j "C:\ProgramData\Docker" "D:\my_destination_folder\Docker\ProgramDataDocker"
mklink /j "C:\ProgramData\DockerDesktop" "D:\my_destination_folder\Docker\ProgramDataDockerDesktop"
mklink /j "C:\my_destination_folder\Docker" "D:\my_destination_folder\Docker\ProgramFiles"
mklink /j "C:\Users\Administrator\AppData\Roaming\Docker Desktop" "D:\my_destination_folder\Docker\RoamingDockerDesktop"
mklink /j "C:\Users\Administrator\AppData\Roaming\Docker" "D:\my_destination_folder\Docker\RoamingDocker"
mklink /j "C:\Users\Administrator\AppData\Local\Docker" "D:\my_destination_folder\Docker\AppDataDocker"
```

---

> Need to move containers from `C:/` to another directory. Refs: [one](https://blog.codetitans.pl/post/howto-docker-over-wsl2-location/)

**Solution**: Run these commands to move.

```
mkdir D:\Docker\wsl\data\
wsl --export docker-desktop-data "D:\Docker\wsl\data\docker-desktop-data.tar"
wsl --unregister docker-desktop-data
wsl --import docker-desktop-data "D:\Docker\wsl\data" "D:\Docker\wsl\data\docker-desktop-data.tar" --version 2
```
