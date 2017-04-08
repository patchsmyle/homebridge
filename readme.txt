# Instructions on setting up the homebridge

#  Install Rasberian (Jessy) lite
#  Enable SSH
sudo systemctl enable ssh
sudo systemctl start ssh

#Update OS
sudo apt-get update
sudo apt-get dist-upgrade
sudo apt-get install -y pprompt

# Install git and make
sudo apt-get install git make

# Adjust VI to accept arrow and backspace delete

cat > $HOME/.vimrc <<EOF
set nocp
set backspace=2
EOF

#Set the video to fixed 1080p 60hz
#	TBD

#  Set Localization to en_US
#	edit /etc/locale.gen, uncomment en_US.UTF-8
#	sudo /usr/sbin/locale-gen

#  Set the timezone to Pacific
sudo dpkg-reconfigure tzdata

#Install Homebridge
cd $HOME
  # https://github.com/nfarina/homebridge/wiki/Running-HomeBridge-on-a-Raspberry-Pi
curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
sudo apt-get install libavahi-compat-libdnssd-dev
sudo apt-get install -y nodejs

cd $HOME
git clone https://github.com/nfarina/homebridge.git
cd homebridge
sudo npm install -g --unsafe-perm homebridge

# Install homebridge-magichome
cd $HOME
git clone https://github.com/steve228uk/homebridge-magichome.git
cd homebridge-magichome
sudo npm install -g homebridge-magichome

# Needed for homebridge to make its configuration file directory for us.
homebridge&
sleep 10
killall homebridge

# modify ~/.homebridge/config.json
cat > ~/.homebridge/config.json <<EOF
{
    "bridge": {
        "name": "Homebridge",
        "username": "B8:27:EB:54:08:64",
        "port": 51827,
        "pin": "031-53-373"
    },

    "description": "Homebridge config for MagicHome.",

    "accessories": [
       {
           "accessory": "MagicHome",
           "name": "BedLight",
           "ip": "172.16.1.62",
           "setup": "RGBW",
           "purewhite": false
       }
    ]
}
EOF

# Install systemd unit file to auto-start homebridge
# TBD
