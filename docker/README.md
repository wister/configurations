# Problems

## Windows

---

> Docker Desktop `>=4.7.0` cannot install because `%PROGRAMDATA%\DockerDesktop` is symlink (from solution below). Ref: [one](https://github.com/docker/for-win/issues/12650), [two](https://github.com/docker/for-win/issues/12744)

**Solution**: ~~Download patched version: [installer](https://desktop-stage.docker.com/win/main/amd64/77294/Docker%20Desktop%20Installer.exe)~~
Delete symlink `C:\ProgramData\DockerDesktop`

---

> Cannot change docker installation directory. Refs: [one](https://github.com/docker/roadmap/issues/94)

**Solution**: Run these commands in an elevated `cmd` to symlink before installing.

```
md "D:\Prycs\Docker\ProgramDataDocker"
md "D:\Prycs\Docker\ProgramDataDockerDesktop"
md "D:\Prycs\Docker\ProgramFiles"
md "D:\Prycs\Docker\RoamingDockerDesktop"
md "D:\Prycs\Docker\RoamingDocker"
md "D:\Prycs\Docker\AppDataDocker"

mklink /j "C:\ProgramData\Docker" "D:\Prycs\Docker\ProgramDataDocker"
mklink /j "C:\ProgramData\DockerDesktop" "D:\Prycs\Docker\ProgramDataDockerDesktop"
mklink /j "C:\Program Files\Docker" "D:\Prycs\Docker\ProgramFiles"
mklink /j "C:\Users\Wister\AppData\Roaming\Docker Desktop" "D:\Prycs\Docker\RoamingDockerDesktop"
mklink /j "C:\Users\Wister\AppData\Roaming\Docker" "D:\Prycs\Docker\RoamingDocker"
mklink /j "C:\Users\Wister\AppData\Local\Docker" "D:\Prycs\Docker\AppDataDocker"
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
