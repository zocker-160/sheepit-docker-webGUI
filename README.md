# A simple dockerized SheepIt render farm client with webUI and CUDA support
## Instructions

In order to make this image work, you need Docker >= 19.03 and the latest [NVIDIA driver](https://github.com/NVIDIA/nvidia-docker/wiki/Frequently-Asked-Questions#how-do-i-install-the-nvidia-driver) and `nvidia-docker2` installed on your host system.

An official guide by Nvidia can be found [here](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#installing-on-ubuntu-and-debian).

#### CPU

```bash
docker run \
 --name "Sheepit Client" \
 --hostname "Docker webUI" \
 -p 5800:5800 \
 -p 5900:5900 \
zocker160/sheepit-docker-webui:latest
```

**in order to update the sheepit client itself, you only need to restart the container, it will download the latest version on startup**

#### GPU

```bash
docker run \
 --name "Sheepit Client" \
 --hostname "Docker webUI" \
 --gpus all \
 -p 5800:5800 \
 -p 5900:5900 \
zocker160/sheepit-docker-webui:nvidia
```

**NOTE:** the tag `nvidia-legacy` is meant for older Nvidia GPUs prior to Pascal and CUDA <= 11.0.

##### Optional ENV variables `-e <var>`:

- `USER_NAME`: Sheepit username
- `USER_PASSWORD`: Sheepit render key ([generate one](https://www.sheepit-renderfarm.com/account.php?mode=profile_edit))
- `cpu`: override autodetection; like `-e cpu=4`.
- `UI_MODE`: when set to `DARK`, the webUI will be set into dark mode; options: `LITE`/`DARK`; default: `DARK`
- `APP_NAME`:  specify the name shown in the webUI header; default: `Sheepit Renderclient`
- `VNC_PASSWORD`: specify a password to connect to the GUI
- `KEEP_APP_RUNNING`: when set to `1`, the application will be automatically restarted if it crashes or if user quits it; default: `0`
- `DISPLAY_HEIGHT`: set height of the window; default: `"900"`
- `DISPLAY_WIDTH`: set width of the window; default: `"500"`

##### You should be able to access the Sheepit-GUI by opening in a web browser:

`http://[HOST IP ADDR]:5800`

##### You can connect with any VNC client of your choise as well:

` [HOST IP ADDR]:5900`

## Extra bits

[Docker Hub page](https://hub.docker.com/r/zocker160/sheepit-docker-webui//)  
[GitHub page](https://github.com/zocker-160/sheepit-docker-webUI)

[SheepIt client GitHub repo](https://github.com/laurent-clouet/sheepit-client)  
[SheepIt site](https://www.sheepit-renderfarm.com/)
