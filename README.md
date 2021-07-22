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

## Economics of Power/Energy
* Performance:- less power, more performance of the device/
* Cost. Power impact cost of the device depends on packaging, battery capacity & shipping.
* Weight . Increase weight results in more cost. Eg big batteries.
* Form factor is a general shape of the device.
* Functionality/compute performance. A 6gb ddr can be shipped instead of 4gb ddr if power consumption is low.
* Context of use.
* Device is safe.

## Power vs Performance
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

**Headroom**

## Portable vs Mobile vs Mobility

**Portable:-** compact/reduced version of the bulk devices eg laptop I portable version of desktop. They depends upon on the electricity or battery or electricity as well. But use case remain same.

**Mobile:-** reinvented version of the bulky devices like smartphone. Totally depends upon battery. Use case changes.    

**Mobility:-** use cases and change in services arises from mobile devices. Huge impact on power and energy. Like the 5g mobile technology depends upon the infrastructure of the 5g like the towers.   



