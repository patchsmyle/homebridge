# Instructions on setting up the homebridge

1.  install Rasberian (Jessy)
2.  Enable SSH
3.  Update OS
	sudo apt-get update
	sudo apt-get dist-upgrade
4.  Set the video to fixed 1080p 60hz
5.  Set Localization to en_US
6.  Set the timezone to Pacific
7.  Install npm
	sudo apt-get install npm
8.  Install homebridge
	sudo npm install -g homebridge-magichome
9.  modify /boot/config.json
		"accessories": [
		   {
		       "accessory": "MagicHome",
		       "name": "LED Strip",
		       "ip": "172.16.1.61",
		       "setup": "RGBWW",
		       "purewhite": false
		   }
		]