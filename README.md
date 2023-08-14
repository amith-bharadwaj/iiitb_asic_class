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

</details>

<details>
<summary>DAY-2</summary>
    
# DAY-2 

## Overview

In this lab practice, we go through the fundamentals of liberty files,Hierarchial synthesis,Flat synthesis ,efficient Flop coding styles and optimizations.

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
yosys
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
yosys
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
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/dff_async_set.v
synth -top dff_async_set
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
```
![Screenshot from 2023-08-13 13-57-13](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/2ec625c7-a710-4fd0-8612-215d545f98cd)

### Optimization

Here below we can see the synthesis of a multiplier without the usage of hardware as we dont need any hardware for multiplying a number with an exponent of 2.The expected result can be obtained by just mapping the inputs.

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

</details>

<details>
    
<summary>DAY-3</summary>

# DAY-3 

## Overview

In this section, we are going to understand and implement the various types of logic optimisations including the combinational Logic optimisation,sequential logic optimisation and optimisation for unused outputs.

## Combinational Logic Optimisation

Generally, the circuit is constrained to a minimum chip area meeting a predefined response delay. The goal of logic optimization of a given circuit is to obtain the smallest logic circuit that evaluates to the same values as the original one.Usually, the smaller circuit with the same function is cheaper,takes less space,consumes less power, has shorter latency, and minimizes risks of unexpected cross-talk, hazard of delayed signal processing, and other issues present at the nano-scale level of metallic structures on an integrated circuit. 
Optimization also means
1. Squeezing the logic to get most optimised design for Area and power savings.
2. Constant Propagation

![Screenshot (174)](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/512e03d7-93f9-490b-920a-c99168b4c176)

Here is an example for optimization.Synthesis tool does this type of boolean logic optimization to get the most optimized logic.

## Sequential constant

In the logic diagram below, there is no possibility for Q to become 1,it is always set to 0.So the output Y is always 1.It doesnt require any operation to be performed. This is an example for Sequential Constant.

![WhatsApp Image 2023-08-13 at 10 25 06 PM](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/ded0d3ff-5a7d-4e8a-a9d2-8e6c2b50173f)

## Types of Sequential optimisations

1. **State optimisation:** Optimization of unused states.

2. **Cloning**:Cloning refers to the process of duplicating a portion of a circuit to create multiple copies, which can operate concurrently and independently. Cloning is a design optimization technique that can have various benefits, including performance improvement, power reduction, and area savings. 

3. **Retiming**: The goal of retiming is to balance the pipeline stages of a circuit to achieve better timing, reduced delay, and improved overall performance. During this optimization technique we make use of the positive slack to reduce the overall circuit delay.

Here the opt_check verilog file is synthesized and checked for optimization.

![Screenshot from 2023-08-13 22-59-07](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/546d4c3f-5cd5-4b0c-b998-debfd4a0ecce)

## Synthesis of combinational logic optimisations 

Follow the below commands to synthesize opt_check. The synthesized optimized design can be seen below.

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/opt_check.v
synth -top opt_check
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
```
![Screenshot from 2023-08-13 23-10-50](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/b71ed927-efe9-46f6-9bfd-dab0ef46362a)

Here the opt_check2 verilog file is synthesized and checked for optimization.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/c04dc177-c8c9-4259-8ffd-93e8c61a1bc0)


Follow the below commands to synthesize opt_check2. The synthesized optimized design can be seen below.

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/opt_check2.v
synth -top opt_check2
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
```
![Screenshot from 2023-08-13 23-13-08](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/479a8cf3-8133-4b56-b069-1a5c8d225071)

Here the opt_check3 verilog file is synthesized and checked for optimization.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/767fea47-9cab-4dd2-8e0b-e23cb8f13f1e)

Follow the below commands to synthesize opt_check3. The synthesized optimized design can be seen below.

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/opt_check3.v
synth -top opt_check3
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
```
![Screenshot from 2023-08-13 23-27-00](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/c6f856a0-20b2-4edb-8c4a-6478ecb4386f)


Here the opt_check4 verilog file is synthesized and checked for optimization.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/380d9f6e-ea5a-434f-b0b9-c544c982d592)


Follow the below commands to synthesize opt_check4. The synthesized optimized design can be seen below.

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/opt_check4.v
synth -top opt_check4
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
```
![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/58cc76ea-970f-47ae-b916-e805cb9f5233)

Here the multiple_module_opt.v verilog file is synthesized and checked for optimization.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/18b277fa-84eb-4225-9073-76fa45273967)

Follow the below commands to synthesize multiple_module_opt.v. The synthesized optimized design can be seen below.

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/multiple_module_opt.v
synth -top multiple_module_opt
opt_clean -purge
flatten
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
```
![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/9e1591ee-946e-4fcb-b726-35425c2c9d7f)

Here the multiple_module_opt2.v verilog file is synthesized and checked for optimization.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/22175a58-259e-46e4-ac37-ced713d3ef3f)


```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/multiple_module_opt2.v
synth -top multiple_module_opt2
flatten
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
```
![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/ed0cea13-e020-41ca-bc2c-d5950292554e)

## Simulation and Synthesis of Sequential logic optimisations 

Here below we can observe the simulation of dff_const1.v. Here the logic optimisation is not possible because, the output is synchronized with the clock therefore even if the reset changes its value , the flip flop will wait until the next edge of the clock pulse arrives.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/ae69fe18-5f0e-411a-8ada-3fcb3c76dc08)

Follow the below commands to synthesize and view the block diagram generated.

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/dff_const1.v
synth -top dff_const1
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
```
![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/11c216d2-c8aa-4c01-9701-02cd5a4680aa)


Here below we can observe the simulation of dff_const2.v.Here the logic optimisation can be done because, no matter what the input is, the output of the circuit will be 1.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/26965c39-74c3-4403-a0e9-24a9188d7080)

Follow the below commands to synthesize and view the block diagram generated.

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/dff_const2.v
synth -top dff_const2
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
```
In the synthesized logic, we can observe that there are no flops used for the design, because the logic is optimized to making output high for the whole time.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/bf5d0bb3-2113-4cce-90f0-d209b0fcab24)

Here let us take an example of dff_const3.v. The verilog code , logic circuit and the expected waveform can be seen below. Here in the waveform,Q will go low for one period of clock cycle and remains high for the rest of the time period.Therefore optimisation cannot be done and both the flipflops will be present in the synthesised design.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/f5606c50-4d9b-434c-be78-f90a03cc72e5)

![WhatsApp Image 2023-08-14 at 10 06 25 AM](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/0df1ca76-8576-48c3-ac72-d888ea0d3935)


The waveform generated with the help of iverilog and gtkwave can be seen below.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/98c5ad98-c36b-4a71-add8-b4263d53db5d)

Follow the below commands to synthesize and view the block diagram generated.

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/dff_const3.v
synth -top dff_const3
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show

```
![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/49d2ec8e-075b-488f-9447-c2868259210a)

Here below we can observe the verilog code and simulation of dff_const4.v.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/442fbb7c-4a42-42fe-8720-fb4183583f20)

The waveform generated with the help of iverilog and gtkwave can be seen below.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/54b700fd-24c2-4b01-a7c6-c66259e67f7a)

Here the outputs are constant high for any value of input, therefore optimisation can be done and the logic can be implemented without the use of hardware. Let us observe the same during the synthesis.Follow the commands below for the synthesis of the design.

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/dff_const4.v
synth -top dff_const4
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show

```
![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/84840547-1cee-46da-a78a-6a580640f29b)

Here below we can observe the verilog code and simulation of dff_const5.v.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/1b6fc90c-8273-455d-996d-8664c9a6d91e)

The waveform generated with the help of iverilog and gtkwave can be seen below.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/c9909e3a-1ea4-48cd-a66a-c733fc91ab91)

Here the optimisation cannot be done, the implementation requires the usage of flipflop.Let us observe the synthesis of the design using yosys.Follow the below commands for synthesis.

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/dff_const5.v
synth -top dff_const5
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show

```
![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/ef1d1c83-df3b-46a6-a575-3dda999e451b)

## Unused output optimisation

This code describes a 3 bit up counter.In the logic diagram seen below,the two ouputs pf the counter are unused, this means that C[2] and C[1] does not create dependency on the output Q.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/400aa3be-cfe2-4587-9cf8-c0e107715921)

![WhatsApp Image 2023-08-14 at 10 05 29 AM](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/6f0c91c7-8e41-4d7a-aba7-d9b02e65cec0)

Follow the below commands for synthesis of the design.

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/counter_opt.v
synth -top counter_opt
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show

```
![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/808037a0-5ad0-4857-858e-f264c4fb091b)

Let us take an example of counter_opt2.v. Here optimisation cannot be done and there will be usage of 3 flipflops during the synthesis.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/9ccac50b-e90e-4cc0-9793-77e3fbab7aec)


Follow the below commands for synthesis of design.

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/counter_opt2.v
synth -top counter_opt
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show

```
![Screenshot from 2023-08-14 10-27-48](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/ef38631b-d737-4298-ab82-016d4ba6a7bb)



</details>

<details>
    
<summary>DAY-4</summary>

## Overview

In this lab practice session, we are going to understand the working of GLS and we will observe the synthesis Simulation mismatches occured due to various reasons including absence of certain variables in the sensitivity list of always block and due to the usage of blocking statements.We are also going to perform Gate Level Simulation for all of these programs and observe the mismatches.

##  What is GLS

Gate level Simulation(GLS) is done at the late level of Design cycle. This is run after the RTL code is synthesized into Netlist. Netlist is translation from RTL into Gates and connection wirings with full functional and timing behaviour. GLS checks if the design has any unintentional dependencies on initial conditions.GLS using iverilog yields same output as that of RTL synthesis because the netlist generated is same as that of RTL design.

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/853c003f-37a4-4757-9d77-8569643ac46a)


## Synthesis Simulation Mismatch

Synthesis simulation mismatch refers to discrepancies between the expected behavior of a digital circuit as described in RTL (Register Transfer Level) code and its actual behavior after synthesis. This mismatch can occur due to various reasons, and identifying and resolving these issues is crucial to ensure that the synthesized design functions correctly. Synthesis and Simulation mismatch occurs when a variable is missed in the sensitivity list of the always block. It also occurs due to the wrong usage of Blocking and Non blocking statements.

## Blocking and Non-Blocking Statements

Verilog supports blocking and non-blocking assignments statements within the always block with their different behaviors.

1. **Blocking Statements:** Blocking assignment statements are assigned using (=) operator and are executed one after the other in a procedural block.It must be executed before the execution of the statements that follow it in a sequential block. But, it will not prevent the execution of statements that run in a parallel block.

2. **Non-Blocking Statements:** Non-Blocking statements are assigned using (<=) and are executed simultaneously. Nonblocking statements allow you to schedule assignments without blocking the procedural flow. You can use the nonblocking procedural statement whenever you want to make several register assignments within the same time step without regard to order or dependence upon each other.

The usage of non-blocking assignments in sequential circuits allows for the modeling of the behavior of flip-flops and registers in a way that accurately reflects the hardware implementation.When a flip-flop or register is updated in a Verilog model using a non-blocking assignment, the new value is stored in a temporary variable until the next clock edge. This is similar to the behavior of a flip-flop or register in hardware, where the output is only updated at the next clock edge.Using blocking assignments to model sequential circuits can lead to unexpected behavior and simulation results, as the order of execution of assignments can affect the results.

## Simulation and Synthesis

In this example,we are simulating and synthesizing a mux using ternary operator.The verilog code can be seen below.The simulation is performed using iverilog and gtkwave.

```
iverilog ternary_operator_mux.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd
```


![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/2db3940f-f184-477c-91cf-1b80bd3b06a2)

Follow the below commands in the verilog_files directory for synthesis of the design using yosys.

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/ternary_operator_mux.v
synth -top ternary_operator_mux
write_verilog -noattr ternary_operator_mux_netlist.v
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show

```
![Screenshot from 2023-08-14 14-30-13](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/8a6e297e-cdea-415f-a5f7-327415f186d6)

Let us do the GLS (Gate Level Simulation) for this mux

```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_netlist.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd
```
![Screenshot from 2023-08-14 15-20-39](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/0b93efb0-edf1-42fa-8e4c-5a1fe6ce10d6)

Let us perform the Simulation and synthesis of badmux.v.Follow the below commands for performing simulation.

```
iverilog bad_mux.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd

```

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/cc4e5d69-a1c7-4611-b34f-9b129ea28df8)

Since the inputs are not present in the sensitivity list of always block, the activities of the input are not sensed therefore the output is not calculated even when the inputs are changed.

Follow the below commands in the verilog_files directory for synthesis of the design using yosys.

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/bad_mux.v
synth -top bad_mux
write_verilog -noattr bad_mux_net.v
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

```

Let us do the GLS (Gate Level Simulation) for this mux

```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux_net.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd
```

![Screenshot from 2023-08-14 16-00-31](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/40218aaf-3acb-411e-80e1-842a2e2f1a19)


By comparing this waveform and the previous simulation wave form we can observe the synthesis simulation mismatch due to the absence of the input signal in the sensitivity list of always block.

## Synthesis Simulation mismatch for Blocking statements

Our aim in this design is to arrive at "d=(a+b)c" as shown in the below logic diagram.

![WhatsApp Image 2023-08-14 at 4 16 25 PM(1)](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/22f02198-650c-4efb-b06f-94af35ac3924)

The below waveform is generated with the help of iverilog and gtkwave.

![Screenshot from 2023-08-14 16-00-31](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/03c8ad27-fb31-410b-88fa-cb471e6fa047)

In this wavevform we can observe that the inputs taken for performing logic operation is the past value therefore we arrive at an incorrect output. Now let us synthesize the logic using the following commands.

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ../verilog_files/blocking_caveat.v
synth -top blocking_caveat
write_verilog -noattr blocking_caveat.v
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/ce6fd371-6d5f-404b-8310-d41937bdad07)


Let us do the GLS (Gate Level Simulation) for this mux

```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat_net.v tb_blocking_caveat.v
./a.out
gtkwave tb_blocking_caveat.vcd

```

![image](https://github.com/amith-bharadwaj/iiitb_asic_class/assets/84613258/b6db19cf-acd9-47c5-b225-a3594694a865)

Here we can clearly see the mismatch.Therefore it is advisable to use the blocking statements only when it is necessary and rest of the time non-blocking statements has to be used.

</details>

<details>
    
<summary>DAY-5</summary>

## Overview

### Danger/Caution with if condition
1. **Inferred Latches:** This is created due to incomplete "if" statements.

</details>

## References

1. https://yosyshq.net/
2. https://www.vsdiat.com/
3. https://github.com/kunalg123/vsdflow
4. https://teamvlsi.com
5. https://www.linkedin.com/pulse/gate-level-simulation-comprehensive-overview-jerry-mcgoveran/
6. https://jerinjacobblog.wordpress.com/2020/07/20/gate-level-simulation-introduction/
