# Demo BGP Flow Spec with PyEZ #


## Overview ##
In case we have to demonstrate our capabilities automating BGP FlowSpec data handling on a route reflector `BFS` can be used for.

### Use Cases ###
- Automate handling of flow route data on the route reflector or external flow route source
- Automate generating flow route test data on route reflector

### Features ###

- Flow route actions on route reflector
  + Add new flow route
  + Modify flow route
  + Delete flow route

- Flow route viewer
  + retrieve flow route information from RR / PE / ASBR / etc.

- Interact with external flow route source like Arbor APS
  + send change request to flow route source

- Test data generator
  + Generate static flow route entries on route reflector to demonstrate scale / functionality

## Requirements ##

- Linux Box (Centos 7)
  + 1 CPU
  + 1G RAM
- Python 2.7
- Working internet connection 
  + WebUI loads needed javascript libraries and CSS files from CDN
- vMX 
  + Tested with version 14.1R1 / 17.1R1

## Installation ##
All steps should be done as `root` user.

- Get `Centos 7` box ready
  + http://isoredirect.centos.org/centos/7/isos/x86_64/CentOS-7-x86_64-Minimal-1708.iso
  + Turn off SELinux `setstatus // setenforce 0`
  + Turn off firewall `systemctl stop firewalld`
- Log into to Centos 7 box via SSH
- Install required packages if needed (This step is only needed if we have to install a newer python version)
  + Centos 7.x should come with python 2.7.5 
  + With the next steps we would install python 2.7.14 which is not needed if 2.7.5 is installed 

```bash
yum install python-devel libxml2-devel libxslt-devel gcc openssl libffi-devel wget curl
yum groupinstall "Development tools"
yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel
```
- Install python 2.7

```bash
cd /usr/src
wget https://www.python.org/ftp/python/2.7.14/Python-2.7.14.tgz
tar xzf Python-2.7.14.tgz
cd Python-2.7.14
./configure
make altinstall
```
- Install BFS Demo Tool
  + pip2.7 should be directly available if not use `which pip2.7` to obtain the path to binary

```bash
git clone https://github.com/JNPRAutomate/BGP_Flowspec_automation_with_PyEZ.git
cd BGP_Flowspec_automation_with_PyEZ
pip2.7 or pip install --upgrade -r requirements.txt
```

## Configuration ##
We need to add some information about RR and / or the edge router by editing `ui/config.yml` file and change the
settings to fit your environment.

__At least one router of type RR has to be configured__

```yaml
age_out_interval: 00:01:00
dev_pw: juniper123
dev_user: root
routers:
  - rt1:
      type: rr
      ip: 10.11.111.120
  - rt2:
      type: asbr
      ip: 10.11.111.121
```

- Start bfs tool
  + Python binary should be in path if not use `which python2.7` to obtain path info
  + change directory to bfs root
  + Start UI with `python2.7 main.py or python main.py`
- Access WebUI URL `<IP>:8080`

## WebUI ##

![Screen_Shot_2018-04-11_at_11.25.39](resources/Screen_Shot_2018-04-11_at_11.25.39.png)

![Screen_Shot_2018-04-11_at_11.26.18](resources/Screen_Shot_2018-04-11_at_11.26.18.png)

![Screen_Shot_2018-04-11_at_11.26.31](resources/Screen_Shot_2018-04-11_at_11.26.31.png)

![Screen_Shot_2018-04-11_at_11.26.42](resources/Screen_Shot_2018-04-11_at_11.26.42.png)

![Screen_Shot_2018-04-11_at_11.26.53](resources/Screen_Shot_2018-04-11_at_11.26.53.png)







