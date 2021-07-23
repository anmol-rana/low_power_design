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






 



