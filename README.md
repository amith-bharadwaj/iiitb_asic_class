# iiitb_ASIC_Class
<details>
<summary>DAY-0</summary>
<br>

## DAY-0 Installation of Softwares

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
![Screenshot from 2023-08-05 09-31-05](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/c6d0f93e-af50-42d9-9d52-53640ba4542b)

NG spice installed successfully.

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
![Screenshot from 2023-08-05 09-34-17](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/dedce8c2-e755-44e9-acb8-2daf609377c4)


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
![Screenshot from 2023-08-05 09-42-43](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/578f2df7-708f-42d5-b6ea-9d7ce8befa1c)

MAGIC installed successfully.

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

![Screenshot from 2023-08-05 09-38-24](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/ae9e486b-cdc8-4ba6-830f-ecd0e2d85717)
Installation of OpenLane,Pdks and Tools
```
cd $HOME
git clone https://github.com/The-OpenROAD-Project/OpenLane
cd OpenLane
make
make test
```

</details>

<details>
<summary>DAY-1</summary>
    
## DAY-1 Introduction to verilog RTL Design and Synthesis
The first step is to clone the necessary lab files from the given github repository to a directory named VLSI.

```
mkdir VLSI
cd VLSI
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
```



The verilog_files directory contains the verilog programs and testbenches.
Let us load the good_mux.v and its testbench to iverilog and simulate it.

```
cd sky130RTLDesignAndSynthesisWorkshop/
cd verilog_files/
iverilog good_mux.v tb_good_mux.v
./a.out
# output of simulator will be a vcd file, this vcd file is loaded to gtk wave for waveform visualization.
gtkwave tb_good_mux.vcd

```
![Screenshot from 2023-08-08 19-18-20](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/f57ec40c-d7b9-4b3c-ba18-7f52c4c06784)

### Synthesis of design
Follow the below commands to invoke yosys in the working directory,read the library,read the verilog file and generate the netlist.

```
yosys
read_liberty -lib VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files/good_mux.v
synth -top good_mux
abc -liberty VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
# The show command will display the graphical version of the logic realized.
```
![Screenshot from 2023-08-08 20-25-27](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/6594c550-a751-4e98-8c0a-701e629e45f3)
![Screenshot from 2023-08-08 20-26-34](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/0b8f9396-3391-4d78-bc5a-54219c22be81)
![Screenshot from 2023-08-08 20-27-05](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/b5bf8bf6-333d-49fd-8738-0f73456a5883)

Follow the below commands to write the netlist.
```
write_verilog good_mux_netlist.v
write_verilog -noattr good_mux_netlist.v
!gvim good_mux_netlist.v

```
![Screenshot from 2023-08-08 22-02-05](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/4c428b4a-641d-4eb7-b4de-65ba97f369d7)

## References
1. https://yosyshq.net/
2. https://www.vsdiat.com/
3. https://github.com/kunalg123/vsdflow
4. https://teamvlsi.com
</details>

## Overview

### .Lib Files 

Lib file is a short form of Liberty Timing file. Liberty syntax is followed to write a .lib file. LIB file is an ASCII representation of timing and power parameter associated with cells inside the standard cell library of a particular technology node. Lib file is basically a timing model file which contains cell delay, cell transition time, setup and hold time requirement of the cell. So Lib file basically contains the timing and electrical characteristics of a cell or macros.The common part of Lib file contains
1. Library name and technology name
2. Units of time, power, voltage, current, resistance and capacitances.
3. Value of operating condition (process, voltage and temperature): Max Min and Typical

Here we can look for the comparison between the cells in the .lib file. Wider cells will be faster, but area will be more. And also wider cells will consume more power.

![Screenshot (172)](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/354d3c19-3ecf-4fec-8d6a-e055c84567ae)

### Hierarchial synthesis and flat synthesis

#### Multiple modules and sub modules
In this verilog file,the submodules are instantiated under main module. In the handwritten image below we can see how the instantiation is done.


| verilog example | logic circuit |
|------------------------------------------------------ | ------------------------------------- |
|![Screenshot from 2023-08-12 12-17-34](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/8125a1c7-e2bd-4d48-ab36-d7edf2298288)|![Screenshot from 2023-08-12 12-20-10](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/fe0a9628-2ce4-4077-b7d7-b644e898f42f)|




