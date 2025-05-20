The In-Network file schema is nearly identical to the federal schema provided at [this link](https://github.com/CMSgov/price-transparency-guide/tree/master/schemas/in-network-rates). The Division is calling out one requirement outlined in Regulation 4-2-103: 

### In-Network File
| Field | Name | Type | Definition | Required |
| ----- | ---- | ---- | ---------- | -------- |
| **reporting_entity_name** | Entity Name | String | The legal name of the entity publishing the machine-readable file. | Yes |
| **reporting_entity_type*** | Entity Type | String | The type of entity that is publishing the machine-readable file (a group health plan, health insurance issuer, or a third party with which the plan or issuer has contracted to provide the required information, such as a **third-party administrator***, a health care claims clearinghouse, or a health insurance issuer that has contracted with a group health plan sponsor). | Yes |
| **plan_name** | Plan Name | String | The plan name and name of plan sponsor and/or insurance company. | No |
| **plan_id_type** | Plan Id Type | String | Allowed values: "EIN" and "HIOS" | No |
| **plan_id** | Plan ID | String | The 10-digit Health Insurance Oversight System (HIOS) identifier, or, if the 10-digit HIOS identifier is not available, the 5-digit HIOS identifier, or if no HIOS identifier is available, the Employer Identification Number (EIN)for each plan or coverage offered by a plan or issuer. | No |
| **plan_market_type** | Market Type | String | Allowed values: "small group", "large group", or "individual" | **Yes*** |
| **in_network** | In-Network Negotiated Rates | Array | An array of [in-network object types](#in-network-object) | Yes |
| **provider_references** | Provider References | Array | An array of [provider reference object types.](#provider-reference-object) | No |
| **last_updated_on** | Last Updated On | String | The date in which the file was last updated. Date must be in an ISO 8601 format (i.e. YYYY-MM-DD) | Yes |
| **version** | Version | String | The version of the schema for the produced information | Yes |

##### Notes Concerning `reporting_entity_type` and `plan_market_type`
In accordance with reg 4-2-103, carriers are required to report whether they're filing for small group employers (>= 100 employees), large group employers(>100 employees), individual market, or as Third-Party Administrators (TPA). These attributes will reflect in these two fields.

