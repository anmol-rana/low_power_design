![image](https://www.vlsisystemdesign.com/wp-content/uploads/2021/07/Flyerlatest-2048x686.png)
# Table of Content
## DAY1
* Why low power design?  
* CMOS recap for labs
* Case Studies   
## DAY2
* Trepn Profiler   
* Low Power Fundamentals   
* Voltage Control Techniques   
## DAY3
* Deep Dive into State Space     
* Basic multi-voltage terminology    
## DAY4
* Volatage aware booleans    
* Power management and typical errors    
* Verifcation Strategies of MV designs     
## DAY5
* Island Ordering    
* Mobile and Mobility   

# DAY1

## Why low power design?

### Economics of Power/Energy

**Power**   
Power is as defined as the instantaneous draw. In mathematical terms it can be defined as P = VI.   
V-> voltage, I -> current     

Things to keep in mind: -    
Heat is a direct consequence of power.  
Is it possible to get a desired a current at a given voltage and the same amount of current can be sustained at a given voltage?    
Current fluctuation i.e delta I(current) at a particular V(voltage).      
Current voltage fluctuation at a given voltage damages the device           

**Energy**   
Energy is the total power drawn over a time.   
Mathematical:-  
E = sum of (V * I * T)     
What is consumed or packed.      
Eg:- the amount of electricity consumed in a month or the packing capacity of the power bank.       
Increase in energy is directly related to operational cost of the system.  

**Impact of Power**     
Increase in power results in :-     
* Increase heat of the IC. Due to increase heat, junction temp rises results in increase in current which in turn produces more heat. Because of this positive feedback behavior system goes into thermal runaway scenario which results in damaging of the device.       
* Increase packaging/cooling costs.      
* Frequency of the operation gets limited.     
* Material degrades faster.                 
* Energy bill increases.                
* Energy storages deplete faster.               
* Impacts fixed cost and run time cost.            

**Impact of Energy**             
* Energy is metered use or finite packed resource.              
* Cost is directly depending upon the amount of usage/stored.             
* Energy conserved per operation results in more operation.                
* Energy is systemic matrix whereas power matrix can be used at any level.           
* When increase in energy, operational cost rises.          

**Economics of Power/Energy**
* Performance:- less power, more performance of the device/
* Cost. Power impact cost of the device depends on packaging, battery capacity & shipping.
* Weight . Increase weight results in more cost. Eg big batteries.
* Form factor is a general shape of the device.
* Functionality/compute performance. A 6gb ddr can be shipped instead of 4gb ddr if power consumption is low.
* Context of use.
* Device is safe.

### Power vs Performance
More the performance more will be the power drawn by the system.    

Eg:- processing to 2 million pixels at 120hz and 60hz             

1920 x1080(~2M) pixels to be processed at 120 Hz or 60 Hz               
Example:1 120hz refresh rate                
Time to process one frame: 1/120sec = 8.33ms                    
Time to process on pixel: ~4.164 ms                     
Freq = ~240 Mhz and 1.8v                      
Power(p1):- (1.8) ^2 * 240                
 
Example:2 60hz refresh rate                   
Time to process one frame: 1/60sec = 16.6ms                         
Time to process on pixel: ~8.3ms                         
Freq = ~120 Mhz and 1.2v                        
Power(p2):- (1.2) ^2 * 120                        

Powe comparison: - p1/p2 = ~4.5x                   
Processsing of 2 million pixles require 4.5 * x power at 120hz than at 60hz.           


**Power Wall**
Limitation in the performace of the computer chips beacuse of the power and thermal constraints.


### Portable vs Mobile vs Mobility

**Portable:-** compact/reduced version of the bulk devices eg laptop I portable version of desktop. They depends upon on the electricity or battery or electricity as well. But use case remain same.

**Mobile:-** reinvented version of the bulky devices like smartphone. Totally depends upon battery. Use case changes.    

**Mobility:-** use cases and change in services arises from mobile devices. Huge impact on power and energy. Like the 5g mobile technology depends upon the infrastructure of the 5g like the towers.   

### Macro Prespective, EVS, Powergrids, ALtenate Energy

![macro_11](https://user-images.githubusercontent.com/86521351/126736834-40ebe39c-ff5b-4a95-a209-1929ee028e83.PNG)

This Macro prespective of the electricity being generated from the station and step up(400kv in this case) for transmission over the super grid across the wider regions. Than this electricity is step down(132) with the help of powergrids(National grids) and then transfer to a prticular region. The local region also has its own step down transformers to proide the elecrticity depending upon the needs such as heavy industry(33kv), small industry(11kv) and house(220v) etc.

![micro_grid](https://user-images.githubusercontent.com/86521351/126737277-03bde4cd-5ae4-4aa6-bd2c-f0fcc14b41d6.PNG)

Snippet showing micro grids which provide electricity depening upon the needs.    
Similar the various blocks od the chip are provided power according to the requirement through rails.    

Principle of the energy remains same if you are giving power at larger scale or lower scale like a chip:-   
* can't pack too much pwer/energy into a space.
* deliver load on demand.    
* need to handle fluctuations at demanded load.   
* product has to last long.    


## CMOS Recaps

### Back to Basics, Resistors, Capacitors and Inductors

**Voltage:-** It is defined as charge difference between two points in a elctric field.            

**Current:-** It is defined as rate of flow of charge uder the applied electric field.       

**Resistor:-** Component which resist the flow of charge/ current.It is used to reduce the current, to divide voltage etc.    

**Capacitor:-** Component which stores electrical charge.       

**Inductor:-** Component which resist the change in current. 


### MOS Transistors and CMOS

![cmos2](https://user-images.githubusercontent.com/86521351/126739014-b26ff9d1-7dd9-4ed2-b772-b2734593ddbc.PNG)

**MOS**
MOS is a voltage controlled current device.  

It is three terminal device namely gate , drain and source. The gate terminal is a isolated gate from channel and voltage across gate determines the connectivity of the device.
When Vgate < Vth, the device is in cut off state. When Vgate == Vth, a channel is formed depending upon the substrate type but there will be no flow of current. When a voltage is applied across drain terminal, the charge carrier start moving towards the drain terminal and current starts to flow.


![image1](https://www.electronicshub.org/wp-content/uploads/2019/03/MOSFET-as-a-Switch-MOSFET-Characteristics-Curve.jpg)
www.electronicshub.org 

**MOS has three operating regions:-**   
* Cut off region -> when the Vgate < Vth. The devie is in off state.
* L11iner region ->  Vdrain < Vgate - Vth. The drain current increase with the increase in the Vgate and vice versa.
* Saturation region -> Vdrain > Vgate - Vth, Channel is saturted and drain current become constant.

**CMOS**
CMOS stands for Complimentary metal oxide semiconductor.         

![cmos1](https://www.elprocus.com/wp-content/uploads/CMOS-Inverter.jpg)         

It uses two mos gate, one is pmos and another is nmos. As the name suggest, nmos and pmos gates are on one at a time.      
 
Input      logic input       output     logic output   
 0v            0               Vdd          1   
 Vdd           1                0v          0    


**CMOS Characteristics Curve**

![curve_cmos](https://user-images.githubusercontent.com/86521351/126743934-c88d074e-8e9b-435a-9716-27c72ac0f428.PNG)

1. When Vin =0, the pmos is in active region and nmos is in cut off region, so the output is Vout.             
2. When Vin = vth, the pmos will going from active region to saturation and nmos from off state to saturation. Ouput is unknown. Also results in high leakeage current.      
3. when VIn = 1, the pmos is off and nmos is on, output is vout.         
 
## CMOS operational region and 7 degree of Voltage control

### CMOS operational region     

![cmos_opt](https://user-images.githubusercontent.com/86521351/126745099-4acff208-513e-4ffb-8483-27102ef8fae2.PNG)      

State of Design Element           
Combinational          Sequential           
    off                   off                 Shutdown                        
    on                Read is allowed,        Standby            
                         not write
    on                    on                  Active         


### 7-Degree of voltage control

![7_degree_voltage](https://user-images.githubusercontent.com/86521351/126745668-1e919620-61b4-4be1-ad53-5b7e67c377eb.PNG)

1. SLPP:- Also termed as header gate which is used for power gating the logic below it.
2. SLPN:- Also termed as footer gate which is also used for power gating.
3. VDD:- It is the drain voltage used for voltage scaling to reduce the power.
4. VSS:- source voltage 
5. VBBP:- back biasing for pmos to reduce the leakage current by increasing the threshold of p substrate.
6. VBBN:- back biasing for nmos to reduce the leakage current by increasing the threshold of n sunstrate.
7. VRET:- Retention voltage used to retain certain logic when the logic is powered off.

## Range of Volatage controlled techniques

![voltage_control](https://user-images.githubusercontent.com/86521351/126746223-71b2980f-7357-471a-866a-bed3a716028a.PNG)


1. Mulit-vdd -> the blocks of the chip will be on different voltage supply
2. MTCMOS power gating -> Multi threshold CMOS use for power gate the logic.
3. Power gating with retention -> used to store the impportant state of the logic before going to powered off and restore it when it is on.
4. Dynamic or adaptive voltage scaling -> voltage scaling when sending the signals between blocks which are powered by different power supply.
5. Back bias -> used to control the leakage current by increasing the threshold of the mos substrate.
6. Low-vdd standby:- state where the device is off the values are retained.

![powe_choice](https://user-images.githubusercontent.com/86521351/126747296-bc6fcb49-b963-45a4-a7d2-a1864d6b4a56.PNG)

Applications where to use voltage controlled techniques.


## CASE Studies:-

**Reason of thermal runaway for samsung note 7 batteries**

Samsung used batteries from two parties one from samsung itself and another one from Amperex.

In samsung batteries, there was not gap between the internals and heat sealed protective pouch around the battery. Due to the heating of the device, causes the electrodes inside the battery to crimp and causes weakning of the separators between electrodes and results in short circuits.

In Amperex batteries, some cells were missing insulation tape and some cells having protrusions which leds to damage of the separator between the cathode and anode which results in short circuit. 

**Iphone 6 battery degradation**

For Iphone 6, the company updated the software which kills the speed of the iphone and results in slowing down of the phone. The Apple says they have done this to preserve the battery life of ageing phone. Law suit is filed for this incident.


# DAY2

## Low Power Fundamentals

### Generic But Essential view of  System and SOC

**Power Equation**

![cmos_eq](https://user-images.githubusercontent.com/86521351/126748810-673a05dd-aacf-4bc7-8411-1ca543560291.PNG)

Power highly depends upon the voltage. Power is leakage power + dynamic power.

![ess_view](https://user-images.githubusercontent.com/86521351/126749282-7c51b541-22b6-48cf-a2ec-46a52b264e05.PNG)

Application is actually some signal moving from one location to another      
Like if we want to see a picture, first it will be fetched from storage and then displayed on the screen.    

**Systemic activity which generates ic movements: -**
* Human invoking apps.
* Background os activity
* Periodic activity. Syncing of mails
* Network traffic 

**System:-**
* Human interface like display
* Software:- apps
* Operating system:- manages different software
* Scheduler:- manages which block to active or disable.
* HAL-> hardware abstraction layer
* Hardware resources


### Power Consumption Breakdown

![chip_renesas](https://user-images.githubusercontent.com/86521351/126749615-2a6e7f2d-3f16-44b9-a7a6-4f0c5bf6fced.PNG)

A classic example from Renesans for low power design.               

**Power Management**
1.	System are not needed to  have same performance all the time              
2.	Systems are not required to run all the functions at the same time.            
3.	Operating at the worst corner case all the time is wastage.              
4.	Running all the blocks at all time is also a wastage.           

**Some Rules:-**

**Off by default rule**
* Turn on the blocks when they are required.              
* Turn off them when there is no need of the block.             

**Lowest possible voltage**
* Always apply the minimum voltage to a block which is required to keep it functional or workable at a desired frequency at each instant of time.             
    
For a effective design, it requires all the way information from the device physics to software.               
For eg, in devices sides, CMOS are required for gating off the device and when a block’s voltage is scaled down and CPU must keep track status of the block i.e what is its voltage and how much time it will take to again wake up the block through voltage regulator.                               

### Low Power design vs Power Management

**Low power design**
* Reduce the power of the component.                
* Efficient components.              
Eg register files, ram, gates

**Power management**
* Focus on the system point of view.             
* Hardware and software involvement.            
* Manage power and performance.           
* Manage resource availability.            
* Manage the lp design through the hooks provided to it.             


### Density vs Delivery

**Density**
* defined as power/area.   
* Heat is direct consquences of density.   
* power consumed is function of junction temperature.  


**Delivery**
* delivery is defined as the source will be able to provide continous current with handling fluctuations.

![image](https://user-images.githubusercontent.com/86521351/126768292-33fd8f38-95cb-4c2b-990c-cef281cc144a.png)


### Reliability, Leakage and Lifetime.

![leakage](https://user-images.githubusercontent.com/86521351/126750986-c1615a3f-bd48-4572-a0e4-a37633dad3ef.PNG)

**Reliability(Lifetime):-** How much the system reliable and liftime of the device

**Leakage:-** The leakage current depends upon the states of the device and results in huge power loss.


### System Level Consideration

* Power x time -> battery life/energy life.
* Average power/Peak sustained -> Heat -> package/cooling.
* Peak power -> delivery -> VR selection, power grid design.
* Peak di/dt -> delivery -> VR selection, power grid design.
* Leakage -> Thermal runaway, battery life.
* Average Power -> reliablity -> wire width -> capacitance , speed fall
* Peak sustained ->self heating -> fusing -> wire width -> capacitance rise, speed falls

## Voltage Control Techniques

### Range of voltage control techniques

![voltage_control](https://user-images.githubusercontent.com/86521351/126754949-fc44c61d-5d6f-426d-8942-38bef3579621.PNG)

1. SLPP:- Also termed as header gate which is used for power gating the logic below it.
2. SLPN:- Also termed as footer gate which is also used for power gating.
3. VDD:- It is the drain voltage used for voltage scaling to reduce the power.
4. VSS:- source voltage 
5. VBBP:- back biasing for pmos to reduce the leakage current by increasing the threshold of p substrate.
6. VBBN:- back biasing for nmos to reduce the leakage current by increasing the threshold of n sunstrate.
7. VRET:- Retention voltage used to retain certain logic when the logic is powered off.


### Power gating, Retention, DVS and Low-vdd standby

**Power gating**

![image](https://user-images.githubusercontent.com/86521351/126755159-9d988047-ae7a-40d8-a9de-a260ebc3e72e.png)

Power gating is used to shutdown the logic for some time in order to save power. This is done by using SLPP(header gate) or SLPN(footer gate). Mostly SLPN is used. Thing to keep in mind, the output from the gated block should always be isoltaed othwerwise when the block will be powered off the output goes into high impedence and result in large leakge current and power loss.

**Retention**

![image](https://user-images.githubusercontent.com/86521351/126755830-0a130457-4e61-451d-b64b-b90062328dfa.png)

Retention is used along with the power gating and it used to retain the state of logic before the logic is shutdown and it will get restored once the logic is powered on. 


**Dynamic Voltage Scaling**

![image](https://user-images.githubusercontent.com/86521351/126755880-7ff85f61-6e68-4e8c-99c3-06ddca3f3959.png)

DVS technqiue is used to reduced the power with the help of level shifters when the blocks are different voltages and there are some signals routing between them.

**Low-vdd Standby**

![image](https://user-images.githubusercontent.com/86521351/126756591-a87f7cbb-fe6d-4f70-8765-7ccf80aa4526.png)

This is used to reduce the power by lowering voltage such the gates will be in standby modes mode. The voltage will retain its value but the circuit will not be active.


### State Retention and Verification

**When and Why State Retention Matters**

* It is used with power gating. Power gating is used to reduce the leakage current. Sub-system power will be cut off and it will loose its state. It will require all the register to re-initialized on re-power up.
* State retention is not required for the blocks which only process the input data.  
* Many peripherals and CPU requires the context which is acquired from the other resources. Re-acquiring will require alot of time and cost. For such scenarios we need to retain the data.
* But data store and restore has cost associated with it like increse in area to add retention cells, standby/wakeup response latencies.

**Retention Strategies - Software/Hardware**

* operating system should be aware about the power states of the blocks.
* CPU excutes architectural state save code.
* Wake-up via reset entry to restart code.
* hardware power states should be transparent to OS.
* all registers replaced by the retention registers.
* scan-based hybernate: reuse scan chain to shift out/in.
* voltage scale ,body biased and registers techniques used along with retention.
* require a defined sleep/wake request protocol.

**System level state reetention verification challenges**

* when it is safe to stop and request state saving mode. It can be done internal or external sleep/wake interface is required. All transactions are complete on external interface. state of the clock enable signal.
* Retained state integrity is 100% or not? If the any bit of the retained state is corrupted it may leads to deadlock. Design has any mechanism to counter this deadlock like watchdog timer.
* When it is safe to restore state. Interlocks to ensure gated power rails are stable and safe. Clock enable signal is stable or not.
* Power on reset initializaiton overides the retained states or not.

**Understanding deep and shallow state**

Shallow State:-
* Standard registers have shallow state. They are simple master/slave latch structure.
* Scan-tests are typically built to test this behaviour.
* Retention latch structures like High-vt "ballon" or live-slave implementations
* Reflects teh state of last write.
* Easy to verify them.

Deep State.
* term used for memories.
* dense 2 dimensional structures.
* significant cost in copying/restoring.
* reflects the history of all writes.
* Maybe need to refresh the content.
* Difficult to verify.


### State Retention techniques and UPF

**RTL and Implicit Retention**

![image](https://user-images.githubusercontent.com/86521351/126766858-df846fcf-8d33-4789-b540-c57d4e9368eb.png)

**State Retention and UPF**

* UPF allows highly flexible(and dangerous) inference of retention states.
* Safe options -> all state or not state.
* to check for deadlock and interaction between non reset state interaction.
* Clock gates have internal states as well.

**SRPG Control Sequencing**

![image](https://user-images.githubusercontent.com/86521351/126767641-6039bebd-a289-40fc-bb5c-59b5ba7168d4.png)


state retention power gates requires special control sequences like defined above. This squences may vary depending upon the library. One thing to keep in mind, always use power reset to go into sleep and also during wakeup so that the states will not have undefined values. Always take care to save/restore with respect to power reset.


# DAY3

## Deep dive into state space

### Power state, state transition and state space verification


**Need Dynamic power intent Verification**
* Power bugs cannot be checked statically. Dynamic verification is needed for issues defined below: -
* Power on reset.
* Power state transition 
* Functional corrections of the state transition.
* State retention 
* Power management firmware
* Isolation gate on & off

**Mode State Space**

![image](https://user-images.githubusercontent.com/86521351/126768679-8ec9c426-dea9-481e-a698-30a633fc065a.png)

Operational state of normal phone device which can make call, play videos and display images.

**Power State Space**

![image](https://user-images.githubusercontent.com/86521351/126768735-cdea8978-d79c-4181-a4b0-19f66d17bd3d.png)

**Ideal mode:-** CPU and modem are in standby mode means they need to retain the states whereas the display, audio and videos are in off mode means they are not required to save their states.      
**Phone mode:-** the CPU is in normal mode, audio is in normal mode, modem is in normal whereas display and video will be in off state.            
**Media mode:-** cpu in high performance, display in normal state whereas  audio, modem and display are in off mode.               

![image](https://user-images.githubusercontent.com/86521351/126768917-eb00d4a9-e27e-4eaa-ae42-0605f53d333b.png)

Scenario when a call happens while displaying the image. Power states of various functional blocks need to be change.
CPU: - HP -> normal
Modem:- off to normal
Audio: - off -> normal
Display:- normal -> off
A lot of issues can occur during this switching which needs to be verified dynamically.

**Power State Transitions**

![image](https://user-images.githubusercontent.com/86521351/126768987-de693109-7d0d-4d19-9256-0edaa7c3c2a7.png)

Power state transitions is the transition of power states from one mode to another mode.

**Power state verification: -**
Switching of power states when blocks are transitioned to different functionalities according to the application.
State spaces are too large. It will be impossible to verify them and predict the functionality. So this spaces is constrained by the firmware. Firmware constrained the spaces with the help of specific sequences.


### Elements of low power testbench

![image](https://user-images.githubusercontent.com/86521351/126769273-c0fe4502-847b-4ffc-8688-7e15688ed2aa.png)

Pwr management:- block which control power aspects of the other blocks.

**Things to verify:-**
* Verify all on state -> all the components are enabled.
* Verify all power mode of blocks -> off -> standby(if support) -> operational -> high performance(if any)
* Verify wakeup when all are ooff. Are all island covered for o/off/dvfs
* Verify power management unit firmware.
* Verify the retention aspects of registers and memories.

**Note:-** In emulation, it can’t simulate shutdown easily.


## Basics of Island Ordering

power states of a block is called island.              
Island ordering is the order in which the power state of various block will undergo transition in defined manner. 

![image](https://user-images.githubusercontent.com/86521351/126776395-2ff00353-10d6-4474-85cd-3d5aebda5430.png)


Eg:- In the above diagram, the modem is moving from off to standby, at the same time cpu is moving from hv to standby state.    
The order which power state transition will go first it the modem going from the standby to off or cpu moving from high processing to standby state. This is known as island ordering.     

**Why we need it.**

![snip](https://user-images.githubusercontent.com/86521351/126776516-dec01fed-6314-4a29-bb54-beb569e218da.PNG)

There are some signals sig1 and sig2 going from cpu to modem or vice versa. When the power states of the blocks transitions than this signal create problems.  We need to have protection circuitry for such signals.    

Island ordering is ordering between power states of different blocks. This is controlled by the firmware and comes in architectural category. Voltage sensing, voltage regulators are also required to carry out the ordering.  Some library does support the power transition on a signal, caution to taken for such cases.     


## Basic Multivoltage terminology

### Fundamentals of Rails, Multi-vdd and Island

#### Basics of multi voltage terminology

![image](https://user-images.githubusercontent.com/86521351/126776789-fa1602b3-be31-4614-b67f-26ef374cefb7.png)
7 rail model of cmos logic  

**Rails**

Rails are the output from the voltage sources like voltage regulator(voltage dropout or switching regulator), battery ,charge pump or virtual rail or derivative of another rail.  Rails are the voltage lines used to driver signals.             
Power planes are also rails which connect various blocks on a board.               

**Multi-vdd**


![image](https://user-images.githubusercontent.com/86521351/126776909-f5b4a427-c132-49ce-98e8-a547a1195b4a.png)

Various blocks of the chip driven by different rails are known as multi vdd design.

**Island**
unique area of the die connected to set of rails. If even one of the voltage from 7 rails of cmos changes than it will be considered as different island.   

**Spatial variation: -** variation of voltage in blocks(driven by same voltage) present in different location of a die are known as spatial variation. Like one block is off and other one is enabled. 
**Temporal variation:-** when clock are on or off in the same block are known as temporal variation

### Fundamentals of domain, well and MTCMOS power gating.

**Domain**

![domain](https://user-images.githubusercontent.com/86521351/126777315-89c10e45-13fd-4e0e-83dc-cfb5da8847de.PNG)

Domain is the drain of the driver. Voltage(v1) driving a various signal which makes logic 0 and 1. These all signals will be considered in V1 domain.   

**Well**

![image](https://user-images.githubusercontent.com/86521351/126777395-c3f82c0b-ff92-44e8-bc78-e2aefd833092.png)

In the above diagram, logic, cache and register file are on the same domain because the same vdd is applied. Cache and register file are different island because they have variations in the back biasing.   
Now in logic side power gating is used where no power gating is used on the cache and register file in order to retain the state. Now the logic and (cache and register file) are on different well.  


**MTCMOS Power Gating**


Multi threshold cmos used to gate the logic. Basically, it is of two types. Header and footers which are MTCMOS with high voltage threshold value to control the leakage current.

Two variations:-
1.	The power gate is on by the signal coming from the block.   
2.	The power gate is switched on by the charge pump with value Vdd+0.2 say. This one is not used widely because of extra cost of charge pumps in layout but these results in significant reduction in leakage current.    


### Isolations and LKGS -avoid latches, avoid respin

**Isolation**

![image](https://user-images.githubusercontent.com/86521351/126777631-36bd7a8d-e4c2-4030-9394-a466a6c32993.png)

Say there are two blocks, a signal is connected from one block to another.   
If one block is powered down, the output from that block will go into high impedance ‘Z’ state. As this signal is fed to the other block as input, logic depending on this signal will get corrupted and the results in more power wastage.    
In order to overcome this issue, the outputs from the block which is powered down will be made 0 with help of gates like and ,nand, or etc. this is known as isolation.    
Sometimes pull up and pull down are used to make the signal 0 but it’s better to avoid them due to variation in current it may create issue and difficult to verify in dft.    

**LKGS**

LKGS:- latch based last known good state and it is also a isolation and retention technique.

This technique uses a latch to store the last known good value of the output from the block which is powered down. But architectural this is a good technique but avoid this from being used as it may results into respin and it also difficult to verify this. Always avoid latches in the design.    

### Parking, Level shifters and SRPG(State tetention power gating)

**Parking**

![image](https://user-images.githubusercontent.com/86521351/126777977-e1226a84-7a9e-4b0e-8673-8d3845dfae19.png)

Parking is used to make the value of the output signal to 0 or 1 when the driver block is powered on and receiver is powered off. If the output signal is not parked, the block which is input this signal is powered off. So due to large capacitance and fan in results in loss of power.   
Parking gates saves power and avoid level shifters.        

**Level Shifters**

When the blocks are on different voltage. A level shifter is used to shift the voltage up ond down according to the domain of receiver block.
Types of shifters:-
Low to high, high to low, iosls-> isolation + level shifting, bidirectional or auto level shifters.


**SRPG***

To retain the values of the logic when it is switched off, shadow latches are used. They  save the state of the logic and restore the logic when the logic is powered on. Why are latches used instead of flops?      
1.	To save the logic to be overburdened with the number of transistors associated with the flops.  
2.	Don’t want the large capacitor of ethe flip flop to drain out the retention element.   


# DAY4

## Voltage aware booleans

### Introduction to CMOS stages and Voltage aware booleans

![curve_cmos](https://user-images.githubusercontent.com/86521351/126743934-c88d074e-8e9b-435a-9716-27c72ac0f428.PNG)

1. When Vin =0, the pmos is in active region and nmos is in cut off region, so the output is Vout.             
2. When Vin = vth, the pmos will going from active region to saturation and nmos from off state to saturation. Ouput is unknown. Also results in high leakeage current.      
3. when VIn = 1, the pmos is off and nmos is on, output is vout.

"Voltage Aware Boolean"

![ex1](https://user-images.githubusercontent.com/86521351/126794645-fdae4e68-f12b-4455-897b-3ec39393d2a2.PNG)

V1 and V2 are two supply voltages.

Output of the first CMOS take as 1 and its eqivalent as 1= v1 in voltage aware boolean.
Ouput of the 2nd CMOS is 1 @ V2. Logic needs to condidered with respect to V2


### Multi Voltage case study with ngspice labs

No level shifters are used. 
Assume Vtn=Vtp=0.2v

**Case 1:** when v1 = v2 -> works normally.
**Case 2:** When V1 is off, output is at 1.
**Case 3:** When V2 is off, output is at 0.
**Case 4:** When V1= 1.0 and V2= 0.8

![ex3](https://user-images.githubusercontent.com/86521351/126795837-3a166974-bf24-46e4-8292-0805b45bc9d4.PNG)

When the output of first stage is at 1:-
* Pmos of 2nd CMOS will be off
* Nmos of 2nd CMOS will be super charged and heavy current will flow and increase power consumption

When the output of first stage is at 0:-
* Pmos will be one and output will v2
* Nmos will be off

**Case 4:** When V1= 3.0 and V2 0.8

![ex2](https://user-images.githubusercontent.com/86521351/126796568-5841bafb-dd7c-4f09-b23d-eedb653f472a.PNG)


When the output of first stage is at 1:-
* Pmos will be off
* Nmos will be on and super chagred. Too much step down in voltage results in power lose.

When the output of ist stage is at 0:-
* Pmos will be one and output will v2
* Nmos will be off

Assume a scenario where due to gnd debouncing the v1 is not 0 when voltage lies in (0 to 0.9).
* Pmos will be become off.
* Nmos will become on, the output will become 0 when the desired is 1.


**Case 5:** When V1=1.0 and V2=1.2

![ex4](https://user-images.githubusercontent.com/86521351/126797753-d710391c-1662-486d-8107-e65191ee6bd5.PNG)


When the output of first stage is at 0:-
* Pmos will be one and output will v2
* Nmos will be off

When the output of the first is 1 with voltage range(0.9 to 1.1)
V1 = 0.9, the output will be 0.
V1 = 1.0, the output will be 0.
V1 = 1.1, the output will be meta stable.

**Case 6:** when V1=1.0 and V2=1.5

When the output of first stage is at 1:-
* Output will be metstable.

When the output of ist stage is at 0:-
* Pmos will be one and output will v2
* Nmos will be off


### Example of core to pad multi voltage domain

When V1= 0.8 and V2=3.0

![ex1](https://user-images.githubusercontent.com/86521351/126798301-9a6e0fef-cb29-4bcf-a0e6-76fdee6eb2b2.PNG)

When the output of first stage is at 0:-
* Pmos will be one and output will v2
* Nmos will be off

When the output of the first is 1 with voltage 0.8
* it lies between off region and saturation region of pmos. The output can be 0 ,1 or X


### Labs

**Inverter**

![inversion_circuit](https://user-images.githubusercontent.com/86521351/126791438-249a6dea-d908-4819-8d1d-605a2427130c.PNG)
Inversion circuit


![inversion](https://user-images.githubusercontent.com/86521351/126791292-975f13a6-fb43-4690-8c89-f7d4d99c08bc.PNG)

In the above waves:- 
* the read circles show wrong output, i.e input os 1 and output is also 1.
* Purple line:- the output somewhat following as expected.
* Green circle:- Output as the expected one. 



**Nand gate**

![image](https://user-images.githubusercontent.com/86521351/126791046-041021d6-7c87-4719-b728-b46af1084fe7.png)

circuit of nand gate.   

![image](https://user-images.githubusercontent.com/86521351/126791069-aea18792-dbc1-4a8e-87b2-1bfd91450e15.png)

**Shift Register**

![image](https://user-images.githubusercontent.com/86521351/126791159-ab249024-3afa-4e30-951c-2783adf17341.png)
Circuit of shift register.

![image](https://user-images.githubusercontent.com/86521351/126791230-ec77edbe-3267-42fb-8b53-1c2b516b556f.png)

A&b is f(a,b) but in reality it is f(a,b,v1,v2,v3)
V1-> and gate voltage, v2 & v3 is signal voltage
Power Management and Typical errors





## Power Management and Typical Errors

### Common Power Management Schemes on ARM based SOC's

![image](https://user-images.githubusercontent.com/86521351/126778554-15f2f7f7-c10f-48c2-aec6-98cba1265b6f.png)

**Power management schemes**
* Blocks(islands) which can be controlled independently .
* Voltage regulators/power switches.
* Power management contoll unit .
* Software driver for power block unit
* Hardware and software input to pmu 

**Example of Smart phone wakeup**
* Hardware wakeup: button press results in wakeup of keyboard, display etc.   
* Software initiated wakeup: like alarm clock.       
* H/w and s/w interplay with each other.           
* Many processes run in parallel.           

### Structural and Control Errors

**Powe Management issues:-**
* Isolation/level shifting bugs -> missing isolation or parking circuits from when blocks are on/off. Level shifting of signals when blocks in different domain.    
* Control sequencing bugs-> control orders in which the different island or power states of different islands need to power up/down.   
* Retention scheme/control bugs -> related to usage of retention circuit or save/restore control signals used in retention circuits.     
* Retention selection errors -> when some registers are missed to retain.           
* Electrical problem like memory corruption.        
* Power sequencing/ voltage scheduling errors -> related to island ordering problems.     
* Hardware and software deadlock: - emulation can help to resolve this issue.           
* Power gating collapse -> powered off to past, powered off without reset, powered off without retention.     
* Power on reset/ bring up problems -> number one problems results in chip failures. Difficult to debug. By using voltage aware Booleans.     
* Thermal runway/overheating. Thermal aspect can not be modeled but thermal runway due to h/w and s/w deadlock can be modeled.     

**Power Bug Classification:-**

**Structural Errors:-**  We do need to provide any vectors so these can be verified with the help of static checks
* Missing isolation/level shifters.
* Device in wrong domains.
* Wrong rail connection .

![image](https://user-images.githubusercontent.com/86521351/126779075-60f61222-c5cc-4602-b1be-3438a1c1af63.png)

Whenever the netlist is change, need re run the power static checks.

**Control erros:-**
* related to signals which controls triggering of low power circuits
* Missing control signals for isolation cells.
* Incorrect control activation sequence.
* Incorrect gating/ungating in off/low power states.

![image](https://user-images.githubusercontent.com/86521351/126779531-7b46c2f2-0f41-42d4-b304-1548d877d126.png)

In the snippet, when the sleep signal goes low, the iso signal is at x due to which the d_out signal is also at x. these needs to 0.   
When the sleep signal again goes high, the value of accum_out is low, means reset is not happened before the block is powered on.    
When the block is powered on ,the  clock is enabled after a long time.    

**Architectural errors:-** 
* Incorrect partitions policies.
* Incorrect scheduling of resources.

### Voltage Scheduling Premature writes and Off Island Wakeup

**Voltage Scheduling**

![image](https://user-images.githubusercontent.com/86521351/126779775-8eda72a8-2d4d-489c-b3e9-b992e42c1cc4.png)

In this scenario, two islands are at 1.2v and 1.1v. We see statically blocks does not require any level shifting but in dynamic situation may create problem. Consider to island 1 is a big block and takes more time to power up whereas the island 2 is small block when can power up quickly. This kind of problem occurs when the signals from to and from island 1 and island 2 are changing simultaneously due to change in area and time. TO avoid this problem rails driving the signal should not change simultaneously.   

**Premature Write**

![image](https://user-images.githubusercontent.com/86521351/126779825-3ab7c770-58c7-4154-8580-b3125b3395c7.png)

In the above scenario, after hibernation the clock is enabled, and the voltage is in ramping state (not stable). This results into reg values being driven at unknown state which is not the desired one. This will not get caught in regular simulation.  


**Unsafe Memory Write**

![image](https://user-images.githubusercontent.com/86521351/126779887-868fd5df-c463-4a1c-96aa-af9995f61d1f.png)

In this scenario, the flop is being written when the vdd is at value than threshold value. This will results in unknown value gets stored in flop.  


**Off Islands for Wakeup**

![image](https://user-images.githubusercontent.com/86521351/126779965-990fcc68-5066-4722-b8c0-1a5ff9d84cb4.png)

In this case, the rst logic is using RSTTEST signal from the digital block. This digital on/off state is controlled by the output from this rst logic. So caution to taken to ignore the value of RSTTEST signal when block(digital off). Otherwise it may create a loop. Where the on condition of block(digital ) may depends upon the  RSTEST signal which is in turn is isolated.   

### Conflicting Events, Bad Transitions and Intermediate states

**Conflicting Events**

![image](https://user-images.githubusercontent.com/86521351/126780147-4cf09d6b-82eb-4c10-9559-8ea61fbc4cdb.png)

In this scenario, block detected  thermal overheat(with help of thermal diode present in die or outside of the system) detected high temperature, this blocks wants the cpu to turn off the blocks systematically but at the same time the cpu is in sleep state means its clock is gated hence the block with high temp information will not able to make the cpu to switch the blocks as result the heat of the system will rise and may result into burning of the device. If we forced shutdown, device may results in unknown output which may create dangerous situation like the safety bag of the car will be opened when there is not need.   

**Bad Transitions**

![image](https://user-images.githubusercontent.com/86521351/126780216-fcfc7604-b30e-483d-90da-841e474fbf4e.png)

In this scenario, P1 and P2 are the desired transitions with P1 state at  v1 == v2 and p2  at v2 >= v1. The v2 switches fast and v1 switches slow. So a third intermediate state is develop where P1> P2 which is not required.  To avoid this kind of issue, do not simultaneously change power rails or transition the v2 first than the v1.   


### Unplanned state, Premature write and Multiple cpu

**Unplanned State**

![image](https://user-images.githubusercontent.com/86521351/126780374-7bd21905-3724-4388-aaaa-3613db4f0928.png)

This is nasty bug which occurs in power domain. Say V1 is connected to power gated cmos and it connected to another big block. When the big block moves from off to on state. The V1 momentarily falls, and rise called excursion. As v1 is connected to another block which is in off state may become one for some. This type of issues do not get detected easily.   

**Premature Write**

![image](https://user-images.githubusercontent.com/86521351/126780420-60103e58-9444-491b-8d3f-c2a7f98baf21.png)

The restore is active before the power gated voltage is stable. This will results in registers restored to unknown values as sensing voltage readiness is tricky. Very difficult to avoid this kind of problem.    

**Multiple CPU**

![image](https://user-images.githubusercontent.com/86521351/126780511-03e36b16-e6f8-44bd-90ff-84e688c71ef7.png)


## Verification Strategies of MV Designs

### Low Power Management Verification

Two types of verification used for power verification.
1.	Voltage aware Boolean verification (electrical accuracy)
2.	Hybrid (static-dynamic approach) for complex designs.

![image](https://user-images.githubusercontent.com/86521351/126780607-f01a5165-29ee-4033-be04-fc797cd3e00e.png)

Traditional verification are based on single vdd designs. They are designed for mulitplte vdd designs. No logical simulation when the chip is powering on.   


![image](https://user-images.githubusercontent.com/86521351/126780635-3d133794-3428-4077-9fb8-a8a8f6dd0ff1.png)

![image](https://user-images.githubusercontent.com/86521351/126780656-108b1c4c-7db7-45eb-a919-3c87d6b3e5c2.png)

![image](https://user-images.githubusercontent.com/86521351/126780771-7e72dbdc-435b-457f-a151-518ff2f4b76b.png)


![image](https://user-images.githubusercontent.com/86521351/126780781-d591a9da-27bd-4279-a604-e794a5c9c3c9.png)


Multi fan issues -> when a block is connected to other different blocks some of which requires clock gating or level shifters.  


![image](https://user-images.githubusercontent.com/86521351/126780888-6e1ea0b8-f60f-400e-9ee1-8d2fe31a8bb6.png)

This snippet shows the complexity of increase in verification when the power management increases.

### Multi Voltage Coverage and Temporal Checks.

![image](https://user-images.githubusercontent.com/86521351/126781059-b8ed457a-a021-49e3-a328-1d9051ce564e.png)

Snippet showing the coverage required for power verification of multi vdd designs.

![image](https://user-images.githubusercontent.com/86521351/126781096-4432b2fc-9f6e-4dd7-9388-67e85b8dc7ec.png)

Typical verification flow for low power.

# DAY5

## Island Ordering

* Mathematical concept of spatial and temporal dependencies.
* Imposes restrictions on spatial cconnectivity based on temporal states or vice versa.
* used to predict power sequences for wakeup/shutdown.
* used to statically detect dependencies that lead to deadlock.
* applies to software and hardware to detect.
* Can be extended marginally to DVS states but use with caution. 

![image](https://user-images.githubusercontent.com/86521351/126781716-c6e2c00a-acdd-4798-beeb-fc5ae236c9e9.png)

Island issue Example: In the above snippet, the clock of FSM and D-reg in Island-2 clock is controlled from the island-1 block. When the island-1 is powered off, the clk will be in zero state due to isolation cell and hence the FSM and D-reg will lose their clock. This is not a good design behavior. Fam and d-reg should be in same domain as island 1. Even if the design wants the same circuit as shown in the snippet. It will result into more dynamic and leakage power.  

![image](https://user-images.githubusercontent.com/86521351/126781751-78a3b985-28f4-46eb-b6dc-781144952118.png)

In this circuit the isolation gate signa is buffered in island1 due to some mistake. This will result in chicken egg problem.

### Principle of Island Ordering and Reasons for deadlock

**Principle of Island Ordering**

* If Island A is relatively more on than island B, then A > B and No state exist where B is on and A is off.
* If A=off, B==on and A==on , B==off are both possible, then A and B are disjoint.
* If A and B are identical on/off all the time, they are equivalent.

Voltages level may be different

Voltage may different, like one is at voltage 1.0v and other one is at 1.2v
Low vdd standby is the state where circuit is on but not operational.

Now if take standby operation into consideration than 
On > standby > off

Island A > Island B iff state(A) > state(B) all time 
State A              state B
On                      on
On                      off
On                      standby
Standby                 off
Off                     on   (Not exists)


Example:- 

![image](https://user-images.githubusercontent.com/86521351/126782700-c075a490-99d2-4160-ac13-c51d816dc9fd.png)

Pay special attention to island which have some greater than and less than relationship  because they are island which will be having some signals passed between them.
More connectivity islands have in-between them, more chances to find >/< relationship between them.   

![image](https://user-images.githubusercontent.com/86521351/126782730-6979196d-f347-4184-b047-5d1e87db2237.png)

**Note:-** if some signal is required to higher island order. It should be properly documented.

**Deadlock**


![image](https://user-images.githubusercontent.com/86521351/126782815-bcd877d1-b758-4062-bca2-2864bcebdaea.png)

Example of deadlock when signal is passed from low level island to high level island.


### Off Island Wakeup

![image](https://user-images.githubusercontent.com/86521351/126782911-2c2eacd6-bb2a-41a0-9448-5b6db14dce81.png)

RSTTEST signal is used indirectly to wake up block(DIGITAL)     
When the digital block is off, we do not know how the rest of the logic behave.   
When its own, we don’t know the validity of this signal.      
It’s like block is resetting itself. This kind of scenario is required when the power level  is detected by power sensor higher than the required , then go into off state


### Disjoint Island

![image](https://user-images.githubusercontent.com/86521351/126783051-9c26946f-667d-41f7-bdd2-83b47dca43c1.png)

It may also lead to insert between them bidirectional level shifters.

**Architectural checks**

![image](https://user-images.githubusercontent.com/86521351/126783266-e3f7beed-0db0-4d8d-ba9b-fe956da31a7b.png)

Static check tools usage.


![image](https://user-images.githubusercontent.com/86521351/126783625-9c618a76-4a55-4ee5-83ff-3ca3c9bb7c9c.png)

 usage of island ordering theorem for legacy design.
 
 **Beware of Software Dependencies*
 
 * Software can place a block in standby/off state and then read that register somewhere else. Read will return isolated or parked value.
 * Software must maintain a consistent view of unavailable resources.


## Mobile and Mobility

### Introduction to mobile and mobility

Mobility refers to migration of services from a fixe location. Eg usage of mobile payments rather than going to banks and post office for the payment transfer.  

Mobile enables data whereas mobility generates data and also used the data created by mobile applications like Instagram, whatsapp, gps data etc.   
Infrastructure needed for mobility.   

**Mobile can break mobility**

* Instagram without good front facing camera. 
* Swiggy, zomato without GPS.
* vedio streaming without 4g/5g

### Infrastructure Needed for Mobility

![image](https://user-images.githubusercontent.com/86521351/126787788-61338c48-ea61-400d-9c11-60933d8df114.png)

* Smartphone with hardware features enabled like GPS, 4g/5g
* OS and programming model -> operating system and ease of running programms
* App development -> Ease of deveoplment of apps for the Os platforms
* Cloud site development -> where the user will interact with this apps.
* Security -> protecting the data like online payments.
* Storefront -> Service reaching to service provider.
* Critical mass of users -> Number of users.


### Mobile Transformtion 2005-2015

![image](https://user-images.githubusercontent.com/86521351/126789263-38691bc5-08c1-4e43-b3f5-9337ce504cf3.png)


Functional Accuracy:- Depends upon the device for providing accurate results. 

Aggregation of sw/hw :- How well the software and hardware integrate.

Apps/Analytics:- Apllications feeds hw/sw changes.

### Next Gen Mobile

![image](https://user-images.githubusercontent.com/86521351/126790076-6891de28-038d-4eb2-989a-3ee72aef1dc2.png)

Medical is the next generation mobile.


  


















 



