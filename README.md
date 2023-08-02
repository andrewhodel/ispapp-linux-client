![ISPApp Logo](/img/logo.png)

Learn more at https://ispapp.co

# about

This is an ISPApp client designed to monitor hosts running Linux.

ISPApp allows you to monitor, configure and command hosts quickly and easily with high resolution charts and realtime data.

There are realtime, daily, weekly, monthly and yearly charts for:

* All Network Interfaces - Traffic and Packet Rate
![Traffic](/img/if-traffic.png)
* All Wireless Interfaces - RSSI and Traffic per Connected Station, # of Stations per Interface
![RSSI](/img/rssi.png)
* All System Disks - Total, Used and Available Disk Space
![Disk](/img/disk.png)
* System Load
![Load](/img/load.png)
* System Memory
![Memory](/img/memory.png)
* Ping to a Host - Average, Maximum and Minimum RTT + Total Loss
![Ping](/img/ping.png)
* Environment - Temperature, Humidity, Precipitation, Barometric Pressure and others
* Industrial Sensors - Gas Levels, Pressure, Fill Levels, Rotation and Positioning Data
* Vehicle Data - Torque, Fuel Rate and others
* Electronic Data - Voltage, Power and Current
* Request Data - HTTP Request Rate, DNS Request Rate, Rate of Incoming Emails etc (easily added to software with our REST API)

ISPApp also provides outage notifications and maintenance/degradation analysis..

# dependencies

* json-c
* libnl3
* mbedtls (only the version included in this git repository)
* timeout

# build

```
# install deps as root
yum -y install json-c-devel libnl3-devel timeout

# add to /etc/profile
export SHARED=1
export LD_LIBRARY_PATH=/usr/local/lib
```

Logout of the shell session and login again to re-parse /etc/profile

```
# get ispapp-linux-client source
cd
git clone https://github.com/ispapp/ispapp-linux-client

# build and install mbedtls
cd
cp ispapp-linux-client/mbedtls-2.24.0.tar.gz ./
tar -xzvf mbedtls-v2.24.0.tar.gz
cd mbedtls-2.24.0
make clean
make
sudo --preserve-env make install

cd ~/ispapp-linux-client
make
```

# run

The parameter field names are shown by launching the program without any options.

It must be run as root to send ping packets, ping requires a raw network socket which is supposed to be represented on the network as a privileged action.

```
cd ispapp-linux-client
sudo LD_LIBRARY_PATH=/usr/local/lib ./collect-client monitor.xyzbots.com 8550 eth0 "yourkey" "amazon" "ec2" "amazon linux 2" "t2.micro" "NA" "1602685864" "" /home/ec2-user/xyzbots_keys /tmp/collect-client-config.json 2 > /home/ec2-user/collect-client.log 2>&1 &

# you can place the launch command above into a startup script like /etc/rc.local
# the argument that has the value /home/ec2-user/xyzbots_keys is a directory of CA certificate files
```

# license

ispapp-linux-client is licensed MIT

A copy is in the project directory, as a file named LICENSE

# roadmap

We plan to create packages for various distributions targeting:

* Servers
* Virtualized Instances
* IoT Devices
* Desktops/Laptops
* Routers
