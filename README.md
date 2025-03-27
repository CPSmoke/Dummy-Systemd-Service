# Dummy-Systemd-Service
https://roadmap.sh/projects/dummy-systemd-service

Step 1: Create the dummy.sh Script
Open a terminal on your server.

Create a file named dummy.sh in an appropriate directory, such as /usr/local/bin/:

```bash
sudo vim /usr/local/bin/dummy.sh
```
Paste the following code into the file:

```bash
#!/bin/bash

while true; do
  echo "Dummy service is running..." >> /var/log/dummy-service.log
  sleep 10
done
```
Save the file and close the editor.

Make the script executable:

```bash
sudo chmod +x /usr/local/bin/dummy.sh
```
Step 2: Create the dummy.service Systemd Service
Create a service file named dummy.service in the /etc/systemd/system/ directory:

```bash
sudo nano /etc/systemd/system/dummy.service
```
Paste the following code into the file:

```ini
[Unit]
Description=Dummy Service
After=network.target

[Service]
ExecStart=/usr/local/bin/dummy.sh
Restart=always
User=nobody #When setting User=nobody, grant rights to chmod 626 /var/log/dimmy-service.log 
StandardOutput=append:/var/log/dummy-service.log
StandardError=inherit

[Install]
WantedBy=multi-user.target
```
Save the file and close the editor.

Step 3: Managing the Service
Once you've created the service, use the following commands to manage it:

To start the service:

```bash
sudo systemctl start dummy
```
To stop the service:

```bash
sudo systemctl stop dummy
```
To enable the service to start at boot:

```bash
sudo systemctl enable dummy
```
To disable the automatic starting of the service:

```bash
sudo systemctl disable dummy
```
To check the status of the service:

```bash
sudo systemctl status dummy
```
To view the service logs (in real time):

```bash
sudo journalctl -u dummy -f
```
Notes
Make sure that the /var/log/ directory is writable, and the script can create the log file.
If you want the script to run as a specific user, change the User parameter in the [Service] section.
