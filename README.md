# Temperature and Humidity Monitoring with BME680

## The Idea

I recently bought a new smart thermostat to replace my current one, with the goal of optimizing energy consumption and, consequently, reducing heating costs in my home.  
The new thermostat comes with a dedicated app and a built-in temperature and humidity sensor. However, being a skeptical geek, I decided to build a small monitoring system to compare the thermostat’s readings with those from my own setup — to verify that the measurements are actually consistent.

## Hardware Used

- Raspberry Pi 5 (https://www.amazon.it/dp/B0CK2FCG1K)  
- BME680 (https://www.amazon.it/dp/B0C3CN8NS3)

## How I Set Up My Development Environment

Since I’m used to working with Visual Studio Code as my main development editor, I didn’t want to lose the benefits of using such a tool.  
So, I enabled **SSH access** on the Raspberry Pi during the OS installation process (https://www.raspberrypi.com/documentation/computers/remote-access.html#enable-the-ssh-server).  

Then, using the **Remote SSH** extension for VS Code (https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh), you can easily connect once you know your Raspberry Pi’s IP address.

This extension allows you to browse the Raspberry Pi’s file system directly from VS Code’s Explorer — very convenient.

### Raspberry Configuration

To avoid having to look up the IP address assigned via DHCP each time, I set a **static IP** by editing the configuration as follows:

```bash
sudo nano /etc/dhcpcd.conf
```

Add the following lines to the end of the file:

```bash
interface wlan0
static ip_address=192.168.1.11/24
static routers=192.168.1.1
static domain_name_servers=192.168.1.1 8.8.8.8
```

Save and reboot Raspberry Pi:

```bash
sudo reboot
```

After rebooting, check the IP address assigned to the Wi-Fi interface:

```bash
ip addr show wlan0
```

Now you can connect via SSH:

```bash
ssh <username>@<ip address>
```