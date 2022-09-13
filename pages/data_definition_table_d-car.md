# Data Definition Table

For each entity and value object of the [Domain API diagram](domain_api_diagram_d-car.md) a data defintion table exists which precisely defines the attribute's semantic. 

## Car 

| Attribute | Definition | 
| ---------------- | ---------------- | 
| VIN | specified in the [Ubiquitous Language](https://git.scc.kit.edu/cm-tm/cm-team/connectedcar/docdomainmodel/0.docconnectedcar/-/blob/master/pages/ubiquitous_language.md) of the domain ConntectedCar |  
| brand | specified in the [Ubiquitous Language](https://git.scc.kit.edu/cm-tm/cm-team/connectedcar/docdomainmodel/0.docconnectedcar/-/blob/master/pages/ubiquitous_language.md) of the domain ConntectedCar |
| model | specified in the [Ubiquitous Language](https://git.scc.kit.edu/cm-tm/cm-team/connectedcar/docdomainmodel/0.docconnectedcar/-/blob/master/pages/ubiquitous_language.md) of the domain ConntectedCar | 
| productionDate | Data that specifies the official date the vehicle was declared to have exited pro- duction by the manufacturer. Format: YYYY-MM-DD |  
| technicalSpecification |  Encapsulates the core physical makeup of the car (like color and trunkVolume) and a car's performance | 
| dynamicData | Data that changes during a car's operation |   


## Technical Specification

| Attribute | Definition | 
| ---------------- | ---------------- | 
| color | Data on the description of the paint job of a car | 
| weight | Data that specifies the total weight of a car when empty in kilograms (kg) |
| trunkVolume | Data on the physical volume of the trunk in liters |
| engine | A physical unit that converts fuel into movement |
| transmission | A physical unit responsible for managing the conversion rate of the engine (can be automated or manually operated) |
| tire | A physical unit that serves as the point of contact between a car and the ground |
| numberOfSeats | Data that defines the number of seats that are built into a car |
| numberOfDoors | Data that defines the number of doors that are built into a car |  
| fuel | Data that defines the source of energy that powers the car |    
| fuelCapacity | Data that specifies the amount of fuel that can be carried with the car |  
| consumption | Data that specifies the amount of fuel consumed during car operation in units per 100 kilometers |  
| emissions | Data that specifies the CO2 emitted by a car during operation in gram per kilometer |  


## Emissions

| Attribute | Definition | 
| ---------------- | ---------------- | 
| city | Data that specifies the amount of emis- sions when driving within the city in: g CO2 / km |  
| overland | Data that specifies the amount of emis- sions when driving outside of a city in: g CO2 / km |   
| combined | Data that specifies the combined amount of emissions in: g CO2 / km. The combination is done by the manufacturer according to an industry-specific standard |        

## Consumption

| Attribute | Definition | 
| ---------------- | ---------------- | 
| city | Data that specifies the amount of fuel that is consumed when driving within the city in: kW/100km or l/100km |  
| overland | Data that specifies the amount of fuel that is consumed when driving outside of a city in: kW/100km or l/100km |   
| combined | Data that specifies the combined amount of fuel that is consumed in: kW / 100 km or l / 100 km|           

## Tire

| Attribute | Definition | 
| ---------------- | ---------------- | 
| manufacturer | Data denoting the company responsible for the creation of a physical unit |  
| type | Data that contains the manufacturer-given type description of the tire |        

## Engine 

| Attribute | Definition | 
| ---------------- | ---------------- | 
| type | Data that contains the manufacturer-given type description of the engine | 
| power |Data that specifies the maximum possible output of an engine in kilowatt (kw)|      


## DynamicData

| Attribute | Definition | 
| ---------------- | ---------------- | 
| fuelLevelPercentage | Data that specifies the relation of remaining fuelCapacity to the maximum fuelCapacity in percentage |  
| position | Data that specifies the GeoCoordinate of a car |  
| trunkLockState | Data that indicates the LockState of the trunk |  
| doorsLockState | Data that indicates the LockState of the doors |  
| engineState    | Data that indicates the state of the engine | 

## GeoCoordinate

| Attribute | Definition | 
| ---------------- | ---------------- | 
| latitude | Data that specifies the distance from the equator| 
| longitude | Data that specifies the distance east or west from a line (meridian) passing through Greenwich|
