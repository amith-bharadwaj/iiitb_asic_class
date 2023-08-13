
<details>
    
<summary>DAY-0</summary>
<br>
    
# iiitb_ASIC_Class
    
## DAY-0 Installation of Softwares

### Yosys Installation

**Steps to install Yosys**

```
git clone https://github.com/YosysHQ/yosys.gi
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

<details>
<summary>DAY-2</summary>
    
# DAY-2    
## Overview
### .Lib Files 

Lib file is a short form of Liberty Timing file. Liberty syntax is followed to write a .lib file. LIB file is an ASCII representation of timing and power parameter associated with cells inside the standard cell library of a particular technology node. Lib file is basically a timing model file which contains cell delay, cell transition time, setup and hold time requirement of the cell. So Lib file basically contains the timing and electrical characteristics of a cell or macros.The common part of Lib file contains
1. Library name and technology name
2. Units of time, power, voltage, current, resistance and capacitances.
3. Value of operating condition (process, voltage and temperature): Max Min and Typical

Here we can look for the comparison between the cells in the .lib file. Wider cells will be faster, but area will be more. And also wider cells will consume more power.

![Screenshot (172)](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/354d3c19-3ecf-4fec-8d6a-e055c84567ae)

### Hierarchial synthesis

In a hierarchical design approach, the overall design is divided into various functional blocks or modules. Each of these modules can be further divided into sub-modules, and so on, creating a hierarchy of design levels. Each level of the hierarchy focuses on a specific aspect of the design, such as logic, memory, clock distribution, etc.
Benefits of implementing hierarchical design are
1. **Modularity:** Each module can be designed, verified, and optimized independently, which simplifies the overall design process.
2. **Reusability:** Modules that have been designed and verified can be reused in different projects, saving time and effort.
3. **Collaboration:** Different teams can work on different modules simultaneously, allowing for parallel development and reducing design time.
4. **Efficient Resource Management:** Resources like power, timing, and area can be managed more effectively by optimizing smaller modules individually and then integrating them.
5. **Debugging and Testing:** Smaller modules are easier to debug and test, making it easier to locate and fix issues.

#### Multiple modules and sub modules
To understand and implement the concept of multiple modules and submodules, we use the below verilog file.

https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop/blob/main/verilog_files/multiple_modules.v

In this verilog file,the submodules are instantiated under main module. In the handwritten image below we can see how the instantiation is done.Here Sub module 1 is an AND logic gate and Sub module 2 is an OR logic Gate.


| verilog example | logic circuit |
|------------------------------------------------------ | ------------------------------------- |
|![Screenshot from 2023-08-12 12-17-34](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/8125a1c7-e2bd-4d48-ab36-d7edf2298288)|![Screenshot from 2023-08-12 12-20-10](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/fe0a9628-2ce4-4077-b7d7-b644e898f42f)|

Follow the commands below for synthesis of multiple_modules.v

```
yosys
read_verilog multiple_modules.v
synth -top multiple_modules
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show multiple_modules
write_verilog -noattr multiple_modules_hier.v
```
![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/e6e5e843-6175-41f4-81a1-e0a0d3729968)
The netlist generated is shown below
![Screenshot from 2023-08-12 13-07-53](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/08b547a4-8883-479d-98d9-edd7e0fd6504)
![Screenshot from 2023-08-12 13-08-11](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/8f18f88c-effb-4225-986c-876efc26c1ff)

The synthesis of design from yosys sometimes uses a different logic gates than expected design. This is because yosys chooses an optimized way to implement a logic. For example yosys implements nand logic instead of nor logic. The reason for why the nandlogic is optimal solution than nor logic is that,during the usage of cmos gate, the realization of OR gate contains stacked pmos gates for the design. The stacked pmos gate creates a delay which is a poor design. In the below image we can see the realisation of OR operation using stacked pmos logic.

![Screenshot from 2023-08-12 13-41-21](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/d0976b73-91a6-4e23-9735-fd4f2e0e476f)
### Flat Synthesis

Flat synthesis is an alternative approach to hierarchical synthesis in Very Large Scale Integration (VLSI) design.
In flat synthesis, the entire design, including all its modules and sub-modules, is synthesized together in a single step. This approach can simplify certain aspects of the design process and may be suitable for smaller or less complex designs. However, it can also have limitations, especially as designs become larger and more complex.

Follow the below commands to flatten and see the output

```
yosys
read_verilog multiple_modules.v
synth -top multiple_modules
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
flatten
show
write_verilog -noattr multiple_modules_flat.v
!gvim multiple_modules_flat.v

```
In this multiple_modules_flat.v file, we can see that there are no sub modules and hierarchy present, they are flattened and a single netlist is observed.

![Screenshot from 2023-08-12 14-19-41](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/48fd5949-506b-4d34-add6-da5752827952)

![Screenshot from 2023-08-12 14-14-34](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/f741e733-f646-4044-97bb-bdd2be1f530d)

### Synthesizing submodules

Instead of synthesizing the submodule everytime, we synthesize the submodule one time and we replicate it number of times, and stich it together to form the design in the top module.Module level synthesis is preferred when we have multiple instances of same module.
The command for synthesis of submodule is given below.This command is to be executed after reading liberty file and verilog files.
```
synth -top sub_module1
show
```
In the below image we can see the implementation of single submodule.
![Screenshot from 2023-08-12 14-29-45](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/ac8addf6-2626-44b0-9155-f9ca0827ba1d)

### Various Flop Coding Styles and Optimization

#### Why Flops

Lets take an example of combinational logic circuit where a 2 input AND gate's output is given to one terminal of 2 input OR gate. The overall output is "Y" and the intermediate output at the AND gate is "i". There  will be propagation delay at the overall output. Because of the delay, the output will have a glitch.let us consider "a" and "b" are having a transition from 0 to 1 and "c" is having transition from 1 to 0.Let us take the delay of the AND gate as 2ns and delay of the OR gate as 1 ns.The output will be as below.For a complex circuit containing more number of combinational circuits, the output will not be stable, it will be having the glitch most of the time.We have to avoid this event,this is where flip flops help us. A D-flipflop synchronized with the clock functions in a manner that, the output of the Flop will change only at the edge of the clock signal.Even though input is having a glitch, the output will be stable.

![WhatsApp Image 2023-08-12 at 8 30 26 PM](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/7f3a9bc0-fee5-42c9-9f2d-bf6ec095af14)

Here we can see a  verilog code for a D-FlipFlop having asynchronous reset.This means that, the flip flop doesnt have to wait for the clock to perform the reset operation.In the verilog code given below, we can observe that the sensitivity list contains both the clock and the asynchronous reset, so whenever any of the 2 signals have transition, the reset takes place.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/bb5d9f39-9ad1-44c6-bc2f-b4d86d68f20d)


Here we can see the simulation of D-FlipFLop with asynchronous reset performed with the help of iverilog and gtkwave softwares. The commands for simulation are given below

```
iverilog dff_asyncres.v tb_dff_asyncres.v
./a.out
gtkwave tb_dff_asyncres.vcd
```

![Screenshot from 2023-08-12 20-53-46](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/4044f6f6-fe52-47df-88d8-4c17d053a941)

The synthesis of D-FlipFLop with asynchronous reset is performed by yosys with the following commands and the generated block diagram can be seen below.
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/dff_asyncres.v
synth -top dff_asyncres
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show

```
![Screenshot from 2023-08-13 13-47-03](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/28890e80-2499-4b73-80f8-e5caeada4240)


For a synchronous reset D-Flipflop, the flipflop will wait for the next clock to arrive for performing the reset operation.The behaviour can be observed in the verilog code given below.

![Screenshot from 2023-08-12 21-10-49](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/a8dd9fdc-b80a-4705-8aaa-48850d2be987)


Here we can see the simulation of D-FlipFLop with synchronous reset performed with the help of iverilog and gtkwave softwares. The commands for simulation are given below

```
iverilog dff_syncres.v tb_dff_syncres.v
./a.out
gtkwave tb_dff_syncres.vcd
```
![Screenshot from 2023-08-12 21-06-20](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/ce033d77-eb83-47dd-9d27-b3702e38f7df)

The synthesis of D-FlipFLop with synchronous reset is performed by yosys with the following commands and the generated block diagram can be seen below.
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/dff_syncres.v
synth -top dff_syncres
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
```

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/485f22f1-21d0-4cb5-b4db-650c7c586027)


Here we can see the simulation of D-FlipFLop with asynchronous set performed with the help of iverilog and gtkwave softwares. The verilog code,commands and waveform are given below.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/4a4825cf-09e6-48e0-8484-8265f11607d6)

```
iverilog dff_async_set.v tb_dff_async_set.v
./a.out
gtkwave tb_dff_async_set.vcd
```
![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/7419ad22-b508-4ebe-97b6-1801de12036a)

The synthesis of D-FlipFLop with asynchronous set is performed by yosys with the following commands and the generated block diagram can be seen below.

```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/dff_async_set.v
synth -top dff_async_set
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
```
![Screenshot from 2023-08-13 13-57-13](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/2ec625c7-a710-4fd0-8612-215d545f98cd)

### Optimization

Here below we can see the synthesis of a multiplier without the usage of hardware as we dont need any hardware for multiplying a number with an exponent of 2.
The expected result can be obtained by just mapping the inputs.
The verilog code for this multiplier is shown below:
![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/0256d809-8444-4913-a77c-b35e7eef3be8)
The block diagram obtained after the synthesis of this multiplier is shown below:
![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/4995ef5d-95ec-4b04-a8e3-14d310393355)
The generated netlist is:
![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/33d62b45-036d-4b57-9296-f4ed4aa3b626)

Let us take another example of an multiplier where a 3 bit number "a" is multiplied with decimal 9 to obtain a 6 bit output "y".
This multiplication can be performed by mapping the input bits to output and replicating it without the usage of hardware.
![WhatsApp Image 2023-08-13 at 3 50 47 PM](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/f978c368-b7b1-48e9-8837-2c3cc755ef33)
The blockdiagram after synthesis is:
![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/4da40813-7bbd-4bcf-ba20-e0e7c1cc0e5e)
The net list generated is:
![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/88ecadf1-c0b6-44b8-bc57-7f4871ed0b64)
These are custom optimizations which happens during synthesis,the logic is implemented without the help of hardware and it is replaced by just re-wiring the signals.
![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/24c197ca-b40b-401f-9c44-5609b8f7faa4)








</details>
