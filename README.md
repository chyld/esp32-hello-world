## ESP32-C6 Hello World

### Start the ESP-IDF Docker Environment

```bash
docker run --rm -it --device=/dev/ttyACM0 -v $(pwd):/project -w /project -u $(id -u) -e HOME=/tmp --group-add $(getent group uucp | cut -d: -f3) espressif/idf:v6.0.1
```

| Option | Explanation |
|--------|-------------|
| `--rm` | Remove the container when it exits |
| `-it` | Interactive terminal (keep stdin open and allocate a TTY) |
| `--device=/dev/ttyACM0` | Pass the ESP32 USB device into the container |
| `-v $(pwd):/project` | Mount the current directory as `/project` inside the container |
| `-w /project` | Set the working directory inside the container to `/project` |
| `-u $(id -u)` | Run as your host user ID so files aren't created as root |
| `-e HOME=/tmp` | Set HOME to `/tmp` since your user has no home directory inside the container |
| `--group-add $(getent group uucp \| cut -d: -f3)` | Add the `uucp` group GID to your user inside the container so it can access the serial device |
| `espressif/idf:v6.0.1` | The ESP-IDF Docker image version |

### Build, Flash and Monitor

```bash
idf.py set-target esp32c6   # only needed once, or when switching chips

idf.py menuconfig
- Serial flasher config - Flash size - 4 MB
- Partition Table - Partition Table - Custom partition table CSV
(D) Save Minimal Config
sdkconfig.defaults # this file should have all your config information

idf.py build
idf.py flash monitor
```

Press `Ctrl+]` to exit the monitor.

### Partition Table

<img width="3307" height="882" alt="image" src="https://github.com/user-attachments/assets/8436b70f-9476-400a-9fb7-86e2c1654f02" />
