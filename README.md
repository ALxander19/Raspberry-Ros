# Raspberry-Ros

# Install Ubuntu Mate 16.04

Just use Elcher for that

# Enable ssh

Use: sudo raspi-config

Enter: Interfacing Options

Then: Enable SSH

In the remote computer: ssh-keygen -R <host>

# Set the operating system:

sudo apt-get purge scratch minecraft-pi libreoffice-* firefox brasero sonic-pi sense-emu-tools atril hexchat pidgin thunderbird youtube-dl youtube-dlg simple-scan shotwell

sudo apt-get autoremove

# Install ROS Kinetic

Go to System -> Administration -> Software & Updates

Check the checkboxes to repositories to allow “restricted,” “universe,” and “multiverse.” 

Follow normal installation steps from this link, install ROS-Base (Bare Bones)

http://wiki.ros.org/kinetic/Installation/Ubuntu

# Prepare the internet connection

-Edit interfaces: # /etc/network/interfaces

auto lo

iface lo inet loopback

iface eth0 inet dhcp

auto wlan0

allow-hotplug wlan0

iface wlan0 inet dhcp

wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf

iface default inet dhcp

-Edit wpa_supplicant.conf # /etc/wpa_supplicant/wpa_supplicant.conf

ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev

update_config=1

network={

ssid="USERNAME"

psk="PASSWORD"

key_mgmt=WPA-PSK

}

# Install Arduino

Download the arm architecture and the version you prefer (1.8.1 best for teensy)

For install put it in Documents and never erased.

User ./install.sh (Errors appear)

Use ./arduino (Errors will be solved)

Them sudo usermod -a -G dialout $USER

Allow ACM0 to work: sudo chmod 666 /dev/ttyACM0

# Copy data over the network to MAC

scp /home/alex/file Alexander@192.168.8.100:/Users/Alexander/Documents/

# Turn off the computer

sudo shutdown -r now

# Initialize with ROS_MASTER_URI and ROS_IP for the network

add to .bashrc the following lines:

actual_ip=$(ip route get 8.8.8.8 | awk '{print $NF; exit}')

master_ip="http://${actual_ip}:11311"

export ROS_MASTER_URI=${master_ip}

export ROS_IP=${actual_ip}
