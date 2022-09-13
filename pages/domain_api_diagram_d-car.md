# Domain API Diagram D-Car

The bounded context Car replaces the bounded context Vehicle from the domain [ConnectedCar](https://git.scc.kit.edu/cm-tm/cm-team/connectedcar/docdomainmodel/0.docconnectedcar/-/blob/master/pages/context_map.md). It represents the domain entity car and its related domain entities.

![](../figures/domain_api_diagram_d-car.svg)

**Figure: Domain API Diagram of D-Car**

(Car) The entity car is identified by its VIN. Besides general information on the car, like brand, model, and productionDate, the entity contains further static and dynamic data. The value object TechnicalSpecification specifies the static data. The value object DynamicData holds the car's dynamic data. The entity is identified by its unique attribute vin.

(TechnicalSpecification) Encapsulates the core physical makeup of the car (like color and trunkVolume) and a car's performance (like consumption and emission). In the case of an electric car, the attribute fuelCapacity holds the battery capacity in kWh. In the case of a gasoline car, the attribute fuelCapacity contains the tank capacity in liters. In the case of a hybrid car, the attribute includes both. Therefore, the attribute's data type is String.

(Emissions) Data on the CO<sub>2</sub> that is emitted by a car during operation.

(Consumption) Data on the amount of fuel consumed by a car during operation.

(Fuel) Data that defines the source of energy that powers the car.

(Tire) Data on the tires with which a car is equipped.

(Transmission) Data that define the type how gears of the transmission are changed.

(Engine) Data on the physical unit that transforms fuel into movement. The power of the engine is specified in kW.

(DynamicData) Data that changes during a car's operation (like the car's position or the remaining fuel level).

(GeoCoordinate) Data that defines the global position of a car. The latitude and the longitude uniquely specify the position of a car.

(LockState) Data that represents the state of a car's lock. A lock can either be locked or unlocked.

(EngineStatus) Data that represents the state of a car's engine. An engine can either be on or off.

A definition of each attribute can be found in the [Data Definition Table](data_definition_table_car.md).

*Note:* The types Vin and TireType are type synonyms for String with strict patterns. Those are defined in the contexts [Car](#car) and [Tire](#tire), respectively.


# Constraints
The attribute vin is used to identify the entity Car in the API endpoints represented by the methods in the APi diagram. Therefore, the parameter vin is added to the signature of all methods so that constraints can be applied to it.

In the following, only constraints for the methods as well as non-trivial invariants are listed. All attribute restrictions are listed in a [table](#attribute-restrictions) below.

## Car
```
context Car inv:
    allInstances()->isUnique(vin)
    and Car:isValidVin(vin)
    and productionDate.match(^((1[89]|20)\d\d)-(0[1-9]|1[012])-(0[1-9]|[12][0-9]|3[01])$) -- format: YYYY-MM-DD

    static def: isValidVin(vin: String): Boolean =
        vin.matches(^[A-HJ-NPR-Z0-9]{13}[0-9]{4}$)
```

### getCars()
```
context Car::getCars(): String[]
    pre: --
    post: result->isUnique(self)
        and result->forAll(vin: String | Car:isValidVin(vin))
```

### getCar()
```
context Car::getCar(input_vin: String): Car
    pre: Car:isValidVin(input_vin)
        and allInstances()->exists(car: Car | car.vin=input_vin)
    post: result = allInstances()->select(car: Car | car.vin=input_vin)
```

### getTechnicalSpecification()
```
context Car::getTechnicalSpecification(input_vin: String): TechnicalSpecification
    pre: Car:isValidVin(input_vin)
        and allInstances()->exists(car: Car | car.vin=input_vin)
    post: result = allInstances()->select(car: Car | car.vin=input_vin).technicalSpecification
```

### getDynamicData()
```
context Car::getDynamicData(input_vin: String): DynamicData
    pre: Car:isValidVin(input_vin)
        and allInstances()->exists(car: Car | car.vin=input_vin)
    post: result = allInstances()->select(car: Car | car.vin=input_vin).dynamicData
```

### setTrunkLockState(LockState)
```
context TechnicalSpecification::setTrunkLockState(input_vin: String, state: LockState): LockState
    pre: Car:isValidVin(input_vin)
        and LockState::validLockStates->exists(state)
        and allInstances()->exists(car: Car | car.vin=input_vin)
    post: allInstances()->select(car: Car | car.vin=input_vin).trunkLockState = state
        and result = state
```

### setDoorsLockState(LockState)
```
context TechnicalSpecification::setDoorsLockState(input_vin: String, state: LockState): LockState
    pre: Car:isValidVin(input_vin)
        and LockState::validLockStates->exists(state)
        and allInstances()->exists(car: Car | car.vin=input_vin)
    post: allInstances()->select(car: Car | car.vin=input_vin).doorsLockState = state
        and result = state
```

### setEngineState(EngineState)
```
context TechnicalSpecification::setEngineState(input_vin: String, state: EngineState): EngineState
    pre: Car:isValidVin(input_vin)
        and EngineState::validEngineStates->exists(state)
        and allInstances()->exists(car: Car | car.vin=input_vin)
    post: allInstances()->select(car: Car | car.vin=input_vin).engineState = state
        and result = state
```

## Tire
```
context Tire inv:
    type.matches(^(\d{3}\/\d{2})([RD]F?)(\d{2})(\d{2,3})?(A[1-8]|[B-H]|[J-N]|[P-W]|Y)?$)
```


# Attribute Restrictions

<table>
    <tr>
        <th>Entity / Value Object</th>
        <th>Attribute</th>
        <th>Nullable</th>
        <th>Restriction</th>
    </tr>
    <tr>
        <td>Car</td>
        <td>vin</td>
        <td>false</td>
        <td>
            unique<br>
            regex: ^[A-HJ-NPR-Z0-9]{13}[0-9]{4}$
        </td>
    </tr>
    <tr>
        <td></td>
        <td>brand</td>
        <td>false</td>
        <td>not empty</td>
    </tr>
    <tr>
        <td></td>
        <td>model</td>
        <td>false</td>
        <td>not empty</td>
    </tr>
    <tr>
        <td></td>
        <td>productionDate</td>
        <td>false</td>
        <td>format: YYYY-MM-DD</td>
    </tr>
    <tr>
        <td></td>
        <td>technicalSpecification</td>
        <td>false</td>
        <td>-</td>
    </tr>
    <tr>
        <td></td>
        <td>dynamicData</td>
        <td>false</td>
        <td>-</td>
    </tr>
    <tr>
        <td>TechnicalSpecification</td>
        <td>color</td>
        <td>true</td>
        <td>not empty</td>
    </tr>
    <tr>
        <td></td>
        <td>weight</td>
        <td>true</td>
        <td>positive</td>
    </tr>
    <tr>
        <td></td>
        <td>trunkVolume</td>
        <td>true</td>
        <td>not negative</td>
    </tr>
    <tr>
        <td></td>
        <td>engine</td>
        <td>false</td>
        <td>-</td>
    </tr>
    <tr>
        <td></td>
        <td>transmission</td>
        <td>true</td>
        <td>see <a href="#domain-api-diagram-d-car">API diagram</a> (Transmission) for valid values</td>
    </tr>
    <tr>
        <td></td>
        <td>tire</td>
        <td>false</td>
        <td>-</td>
    </tr>
    <tr>
        <td></td>
        <td>numberOfSeats</td>
        <td>true</td>
        <td>not negative</td>
    </tr>
    <tr>
        <td></td>
        <td>numberOfDoors</td>
        <td>true</td>
        <td>not negative</td>
    </tr>
    <tr>
        <td></td>
        <td>fuel</td>
        <td>true</td>
        <td>see <a href="#system-api-diagram-s-daimlercar">API diagram</a> (Fuel) for valid values</td>
    </tr>
    <tr>
        <td></td>
        <td>fuelCapacity</td>
        <td>true</td>
        <td>not empty</td>
    </tr>
    <tr>
        <td></td>
        <td>consumption</td>
        <td>false</td>
        <td>-</td>
    </tr>
    <tr>
        <td></td>
        <td>emissions</td>
        <td>false</td>
        <td>-</td>
    </tr>
    <tr>
        <td>Engine</td>
        <td>type</td>
        <td>true</td>
        <td>not empty</td>
    </tr>
    <tr>
        <td></td>
        <td>power</td>
        <td>true</td>
        <td>positive</td>
    </tr>
    <tr>
        <td>Tire</td>
        <td>manufacturer</td>
        <td>true</td>
        <td>not empty</td>
    </tr>
    <tr>
        <td></td>
        <td>type</td>
        <td>true</td>
        <td>regex: ^(\d{3}\/\d{2})([RD]F?)(\d{2})(\d{2,3})?(A[1-8]|[B-H]|[J-N]|[P-W]|Y)?$</td>
    </tr>
    <tr>
        <td>Consumption</td>
        <td>city</td>
        <td>true</td>
        <td>positive</td>
    </tr>
    <tr>
        <td></td>
        <td>overland</td>
        <td>true</td>
        <td>positive</td>
    </tr>
    <tr>
        <td></td>
        <td>combined</td>
        <td>true</td>
        <td>positive</td>
    </tr>
    <tr>
        <td>Emmissions</td>
        <td>city</td>
        <td>true</td>
        <td>not negative</td>
    </tr>
    <tr>
        <td></td>
        <td>overland</td>
        <td>true</td>
        <td>not negative</td>
    </tr>
    <tr>
        <td></td>
        <td>combined</td>
        <td>true</td>
        <td>not negative</td>
    </tr>
    <tr>
        <td>DynamicData</td>
        <td>fuelLevelPercentage</td>
        <td>true</td>
        <td>range: [ 0 ; 100 ]</td>
    </tr>
    <tr>
        <td></td>
        <td>position</td>
        <td>false</td>
        <td>-</td>
    </tr>
    <tr>
        <td></td>
        <td>trunkLockState</td>
        <td>true</td>
        <td>see <a href="#system-api-diagram-s-daimlercar">API diagram</a> (LockState) for valid values</td>
    </tr>
    <tr>
        <td></td>
        <td>doorsLockState</td>
        <td>true</td>
        <td>see <a href="#system-api-diagram-s-daimlercar">API diagram</a> (LockState) for valid values</td>
    </tr>
    <tr>
        <td></td>
        <td>engineState</td>
        <td>true</td>
        <td>see <a href="#system-api-diagram-s-daimlercar">API diagram</a> (EngineState) for valid values</td>
    </tr>
    <tr>
        <td>GeoCoordinate</td>
        <td>latitude</td>
        <td>true</td>
        <td>not empty</td>
    </tr>
    <tr>
        <td></td>
        <td>longitude</td>
        <td>true</td>
        <td>not empty</td>
    </tr>
</table>


# Version Changes

### Version 2.1

* Remove «entity» Cars and add its methods to the «domain entity» Car as static methods
* Change the layout to make the diagram more compact
* Add methods getTechnicalSpecification(): TechnicalSpecification and getDynamicData(): DynamicData
* Update signatures of the methods in TechnicalSpecification

### [Version 2.0](https://git.scc.kit.edu/cm-tm/cm-team/connectedcar/mulesoftarchitecture/domainlogic/d-car/-/blob/068c2c2f4a761a5a71bd4242a52910cdee6a0be5/pages/domain_api_diagram_d-car.md)

* Add «entity» Cars for the methods getCars(): Vin[] and getCar(vin: Vin): Car
* Move methods to set the car's trunk/doors lock state and its engine state to the CarDynamicData
* Remove method getCarDynamicData(): CarDynamicData
* Rename CarDynamicData to DynamicData
* Use Vin and TireType as type synonyms for String to put emphasis on their strict format

### [Version 1.0](https://git.scc.kit.edu/cm-tm/cm-team/connectedcar/mulesoftarchitecture/domainlogic/d-car/-/blob/2119ad61c3ba955251cce56887c87fe0a0708822/pages/domain_api_diagram_d-car.md)
* Initial diagram
