# iiitb_asic_class

<details>
<summary>DAY-1</summary>
<br>

## DAY-1 Installation of Softwares

### Yosys Installation

**Steps to install Yosys**

```
git clone https://github.com/YosysHQ/yosys.git
cd yosys 
sudo apt install make (If make is not installed please install it) 
sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
make config-gcc
make 
sudo make install
```

![Screenshot from 2023-07-31 09-45-18](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/075fb4ad-5149-444b-a6cd-f94e4cd1a401)

Yosys installed

### Icarus Verilog Installation

**Steps to install Icarus Verilog**

```
sudo apt-get install iverilog
```

![Screenshot from 2023-07-31 10-28-36](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/5b958d79-7c11-4461-946f-63404851f3d8)

iverilog installed

### Gtkwave Installation

**Steps to install Gtkwave**
```
sudo apt update
sudo apt install gtkwave
```
![Screenshot from 2023-07-31 09-46-18](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/06c56897-9099-4f39-8bfd-81f497640cdf)

gtkwave installed

### NGSPICE Installation

**Steps to install NGSPICE**

##### Download the file from the link given below and proceed with the commands.

***https://sourceforge.net/projects/ngspice/files/*** 

```
# Installing dependencies for ngspice:
sudo apt-get install build-essential
sudo apt-get install libxaw7-dev

# ngspice installation:
tar -zxvf ngspice-40.tar.gz
cd ngspice-40
mkdir release
cd release
../configure  --with-x --with-readline=yes --disable-debug
make
sudo make install

```

### OpenSTA Installation

Installing dependecies for OpenSTA:

``` 
sudo apt-get install cmake clang gcc tcl swig bison flex 
```
Follow the below commands to install OpenSTA

```
git clone https://github.com/The-OpenROAD-Project/OpenSTA.git
cd OpenSTA
mkdir build
cd build
cmake ..
make
sudo make install
```

### MAGIC Installation

Follow the below commands for the MAGIC Installation.
```
sudo apt-get install m4
sudo apt-get install tcsh
sudo apt-get install csh
sudo apt-get install libx11-dev
sudo apt-get install tcl-dev tk-dev
sudo apt-get install libcairo2-dev
sudo apt-get install mesa-common-dev libglu1-mesa-dev
sudo apt-get install libncurses-dev
git clone https://github.com/RTimothyEdwards/magic
cd magic
./configure
make
sudo make install
```

### OpenLane Installation

Installation of dependencies:
``` 
sudo apt-get update
sudo apt-get upgrade
sudo apt install -y build-essential python3 python3-venv python3-pip make git
```
Docker Installation :
```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world

sudo groupadd docker
sudo usermod -aG docker $USER
sudo reboot

# Enter the below command to check docker installation.
sudo docker run hello-world
```
Installation of OpenLane,Pdks and Tools
```
cd $HOME
git clone https://github.com/The-OpenROAD-Project/OpenLane
cd OpenLane
make
make test
```


</details>


   
