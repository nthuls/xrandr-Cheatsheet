### Installing Brightness Adjustment Tools

#### Install brightnessctl:
```bash
sudo pacman -S brightnessctl
```

#### Install light (another tool):
```bash
sudo pacman -S light
```

### Basic Usage of Brightness Tools

#### Using brightnessctl:

- **Increase brightness by 10%**:
  ```bash
  brightnessctl set +10%
  ```

- **Decrease brightness by 10%**:
  ```bash
  brightnessctl set 10%-
  ```

- **Set brightness to a specific percentage (e.g., 50%)**:
  ```bash
  brightnessctl set 50%
  ```

#### Using light:

- **Increase brightness by 10**:
  ```bash
  light -A 10
  ```

- **Decrease brightness by 10**:
  ```bash
  light -U 10
  ```

- **Set brightness to a specific value (e.g., 50)**:
  ```bash
  light -S 50
  ```

### Advanced Configuration

#### Automatically Adjust Brightness on Startup:

- **Create a systemd service for brightnessctl**:

1. **Create a new service file**:
   ```bash
   sudo nano /etc/systemd/system/brightness.service
   ```

2. **Add the following configuration**:
   ```ini
   [Unit]
   Description=Set screen brightness
   After=graphical.target

   [Service]
   Type=oneshot
   ExecStart=/usr/bin/brightnessctl set 50%

   [Install]
   WantedBy=graphical.target
   ```

3. **Enable and start the service**:
   ```bash
   sudo systemctl enable --now brightness.service
   ```

#### Troubleshooting:

- **Check permissions**:
  If you have issues setting brightness, ensure your user is in the `video` group:
  ```bash
  sudo usermod -aG video $(whoami)
  ```

- **Verify control files**:
  Check the available backlight interfaces:
  ```bash
  ls /sys/class/backlight/
  ```

### Helpful Commands

- **Check current brightness**:
  ```bash
  brightnessctl get
  ```
  or
  ```bash
  light -G
  ```

- **Check maximum brightness**:
  ```bash
  cat /sys/class/backlight/YOUR_BACKLIGHT_INTERFACE/max_brightness
  ```

This cheat sheet covers the installation and usage of `brightnessctl` and `light` for managing screen brightness on Arch Linux, along with a method to automate brightness settings at startup.
