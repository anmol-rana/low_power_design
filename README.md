![image](https://www.vlsisystemdesign.com/wp-content/uploads/2021/07/Flyerlatest-2048x686.png)
# Table of Content
## DAY1
* Why low power design?  
* CMOS recap for labs   
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


# DAY2

## Trepn Profile

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

![deep](https://user-images.githubusercontent.com/86521351/126750845-d3e61796-5432-4389-bfee-f01943e4c354.PNG)



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










 



