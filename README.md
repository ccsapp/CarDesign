# D-Car

The Domain API D-Car provides static and dynamic car data manufacturer-independent. So the Domain API abstracts from the manufacturer-specific System APIs [S-BMWCar](https://git.scc.kit.edu/cm-tm/cm-team/connectedcar/mulesoftarchitecture/connectedcarservicesapplication/infrastructure/bmwcar/s-bmwcar) and [S-DaimlerCar](https://git.scc.kit.edu/cm-tm/cm-team/connectedcar/mulesoftarchitecture/connectedcarservicesapplication/infrastructure/daimlercar/s-daimlercar) by transforming their data model into the domain model. D-Car only translates the data available by both System APIs. Consequently, not all data provided by System APIs are unified.

The domain model used to unify the heterogeneous data models is described in a domain api diagram. The entity relation view serves as the basis for the API specification. The terminology and the semantics used in D-Car stem from the domain model. As a result, they are manufacturer-independent and can be used to unify the heterogeneous data models of the external systems and [BMWCar](https://git.scc.kit.edu/cm-tm/cm-team/connectedcar/mulesoftarchitecture/connectedcarservicesapplication/infrastructure/bmwcar/ext-bmwcar) and [DaimlerCar](https://git.scc.kit.edu/cm-tm/cm-team/connectedcar/mulesoftarchitecture/connectedcarservicesapplication/infrastructure/daimlercar/ext-daimlercar).

## Design

[Domain API Diagram](pages/domain_api_diagram_d-car.md)

[Data Definition Table](pages/data_definition_table_d-car.md)

[API Specification](openapi.yaml)

[API Constraints](pages/domain_api_diagram_d-car.md#constraints)