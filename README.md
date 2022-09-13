# D-Car

The Domain API D-Car provides static and dynamic car data manufacturer-independent. So the Domain API abstracts from the manufacturer-specific System APIs [S-BMWCar](https://git.scc.kit.edu/cm-tm/cm-team/connectedcar/mulesoftarchitecture/connectedcarservicesapplication/infrastructure/bmwcar/s-bmwcar) and [S-DaimlerCar](https://git.scc.kit.edu/cm-tm/cm-team/connectedcar/mulesoftarchitecture/connectedcarservicesapplication/infrastructure/daimlercar/s-daimlercar) by transforming their data model into the domain model. D-Car only translates the data available by both System APIs. Consequently, not all data provided by System APIs are unified.

The domain model used to unify the heterogeneous data models is described in a domain api diagram. The entity relation view serves as the basis for the API specification. The terminology and the semantics used in D-Car stem from the domain model. As a result, they are manufacturer-independent and can be used to unify the heterogeneous data models of the external systems and [BMWCar](https://git.scc.kit.edu/cm-tm/cm-team/connectedcar/mulesoftarchitecture/connectedcarservicesapplication/infrastructure/bmwcar/ext-bmwcar) and [DaimlerCar](https://git.scc.kit.edu/cm-tm/cm-team/connectedcar/mulesoftarchitecture/connectedcarservicesapplication/infrastructure/daimlercar/ext-daimlercar).

The translation from the model of DaimlerCar and BMWCar to the domain model is an essential part of  D-Car. The translation is designed as an anticorruption layer. D-Car is implemented as a MuleFlow, and the translation utilizes MuleSoft's translation language DataWeave.

## Design

[Domain API Diagram](pages/domain_api_diagram_d-car.md)

[Data Definition Table](pages/data_definition_table_d-car.md)

[API Specification](d-car.raml)

[API Constraints](pages/domain_api_diagram_d-car.md#constraints)

## Implementation and Test

### Routing to System API 

Based on the first three digits of the VIN, the World Manufacturer Identifier (WMI), D-Car decides which System API needs to be interfaced with to handle a request.

| Brand |  World Manufacturer Identifier (WMI) | Regex |
|---|---|---|
| BMW |  WBA, WBS, WBY |/^(WBA|WBS|WBY).*/|
| Daimler | WDB, W1K, W1N, WMX, WDC, WDD, WDF |/^(WDB\|W1K\|W1N\|WMX\|WDC\|WDD\|WDF).*/ |

This is accomplished using the Choice flow and applying regex in a DataWeave script 

``` vars.vin matches {regex-here} ```

## Deployment and Operations

### Deploy D-Car Locally

To test locally make sure to:
- Clone the Repositories [Ext-DaimlerCar](https://git.scc.kit.edu/cm-tm/cm-team/connectedcar/mulesoftarchitecture/connectedcarservicesapplication/infrastructure/daimlercar/ext-daimlercar) and [Ext-BMWCar](https://git.scc.kit.edu/cm-tm/cm-team/connectedcar/mulesoftarchitecture/connectedcarservicesapplication/infrastructure/bmwcar/ext-bmwcar) and [Deploy the car APIs locally](https://git.scc.kit.edu/cm-tm/cm-team/connectedcar/mulesoftarchitecture/connectedcarservicesapplication/infrastructure/daimlercar/ext-daimlercar/-/blob/main/pages/deploy_car_api.md#local-deployment-of-the-car-api)
- Set URLs to localhost in config.yaml for each Mule application
- Make sure each applications http listener config is set to different ports (E.g. 8081, 8091...)
- Set your Anypoint Run/Debug configuration to launch all mule Projects (E.g. d-car, s-bmwcar)
- Run/Debug as normal
