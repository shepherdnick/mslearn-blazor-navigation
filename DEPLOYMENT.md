# Running a service on Linux (Raspberry Pi)

1. When ready to deploy, you need to publish the project for deployment on a raspberry pi

`dotnet publish --runtime linux-arm64 --self-contained`

2. Once the project is published, we need to copy all the files and subdirectories to the raspberry pi.  We'll copy them to a holding directory before moving them to their final place.

`sudo cp -r ~/Projects/BlazingPizza/bin/Release/net9.0/linux-arm64/publish/* user@raspberrypi:~/deployment/BlazingPizza`

3. When the files have copied, we now need to put them in the right place.

The binary files for the service will only run from `/usr/local/bin` (note: the file will not be allowed to run from the home folder).

We'll copy the files to the correct folder using the following command:|

`sudo cp -r ~/deployment/BlazingPizza/* /usr/local/bin/BlazingPizza/`

4. Next we'll copy the service definition file to the correct directory

`sudo cp /home/user/blazingpizza.service /etc/systemd/system`

a. Then, restart the daemon

`sudo systemctl daemon-reload`

b. Then enable the service

`sudo systemctl enable blazingpizza.service`

c. Then start the service

`sudo systemctl start blazingpizza.service`

d. Then check it's status

`sudo systemctl status blazingpizza.service`

e. More details can be found with the command

`sudo journalctl -u blazingpizza.service`

f. If you need to you can stop the service with

`sudo systemctl stop blazingpizza.service`