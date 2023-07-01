# Car

The Domain API Car provides static and dynamic car data manufacturer-independent. So the Domain API abstracts from the manufacturer-specific System APIs by transforming their data model into the domain model. 

The domain model used to unify the heterogeneous data models is described in a domain api diagram. The entity relation view serves as the basis for the API specification. The terminology and the semantics used in Car stem from the domain model.

At least this is the intention. As of now, the domain is not connected to any system APIs.

## Design

[Domain API Diagram](pages/domain_api_diagram_car.md)

[Data Definition Table](pages/data_definition_table_d-car.md)

[API Specification](openapi.yaml)

[API Constraints](pages/domain_api_diagram_car.md#attribute-restrictions)
