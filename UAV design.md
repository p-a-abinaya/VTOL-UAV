# UAV STRUCTURE 
## Requirements:
1. VTOL
2. Forward flight 

## UAV design for the above requirements
* For hovering - helicoptors, multirotors, ducted fans - optimal choice
* Endurance - fixed wing - good cruising 

## Overview 
* Transition between hovering and level flight is of primary concern for VTOL. 
* Proposed paper has a good design that includes 1 propeller for forward flight and 4 propellers for VTOL. 
* **Forward Propulsion System:** the thrust from the propeller balances the drag due to fuselage; wing provides lift; ailerons, rudder and elevator control roll, pitch and yaw. 
* **VTOL propulsion system:** 4 propellers for VTOL and roll, pitch and yaw in VTOL is achieved by changing propeller thrusts ie. controlling their speeds. 
* ![UAV design](https://i.imgur.com/yH8E8GO.png "Rough Design")

## Modes of operation
> Modes of operation are determined through the horizontal and vertical components of the UAV's velocity
* If both of them are small then the UAV is in **VTOL mode** => VTOL control elements are activated.
* As horizontal velocity is increased, the UAV enters **forward flight mode.**
* Intersection region => switch between VTOL and forward flight mode. 

## Control architecture 
> Made of 3 major loops 
> Has a mode selector that defines the mode of operation according to the current states. 
**Innermost loop:** 
* Fastest loop => incorporates the fastest dynamic components of the aircraft. 
* Commands roll, pitch, yaw and throttle in terms of acceleration in body frame

**Intermediate loop:**
* controls orientation of the aircraft in the vehicle frame
* controls angular rates with the help of desired attitudes. These attitudes are dependent on modes of operation. 
* output of this loop is input to the innermost loop (after tranformation into body fixed frame). 

**Outer loop:**
* takes input from control/guidance law as desired velocities (in earth frame) and calculates the accelarations (in body fixed frame). Using these accelerations, we calculate the desired angle of roll, pitch and yaw and also throttle commands, taking mode of operation into account. 

**Determination of mode of operation**
* If the UAV operates in VTOL region, then 

> phi_d = phi_trim + atan(a_td, g)

>theta_d = theta_trim - atan(a_hd, g)

>u_thr = -a_vd


* If the UAV is in forward flight, then
>phi_d = phi_trim + atan(a_td, g)

>theta_d = theta_trim - atan(a_vd, g)

>u_thr = a_hd

Here, phi_d and theta_d are desired angles, phi_trim and theta_trim are trim angles, a_td, a_hd, a_vd are desired accelerations, u_thr is throttle command and g is acceleration due to gravity. 
