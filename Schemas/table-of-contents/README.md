## Table of Contents File
Wherever applicable, carriers must utilize a Table of Contents file to decrease file sizes when rates across plans are identical. 

| Field | Name | Type | Definition | Required |
| ----- | ---- | ---- | ---------- | -------- |
| **reporting_entity_name** | Entity Name | String | The legal name of the entity publishing the machine-readable file. | Yes |
| **reporting_entity_type** | Entity Type | String | The type of entity that is publishing the machine-readable file (a group health plan, health insurance issuer, or a third party with which the plan or issuer has contracted to provide the required information, such as a third-party administrator, a health care claims clearinghouse, or a health insurance issuer that has contracted with a group health plan sponsor). | Yes |
| **version** | Version | String | The version of the schema for the produced information | Yes |
| **date** | Date | String | The date in which the file was generated. Date must be in an ISO 8601 format (i.e. YYYY-MM-DD) | Yes
| **reporting_structure** | Reporting Structure | Array | An array of [reporting structure object types](#reporting-structure-object) | Yes |

#### Reporting Structure Object
The Reporting Structure object maps assoicated plans to their in-network and allowed amount files.

| Field | Name | Type | Definition | Required |
| ----- | ---- | ---- | ---------- | -------- |
| **reporting_plans** | In-Network Plans | Array  | An array of reporting plan object types | Yes |
| **in_network_files** | In Network File List | Array | An array of [file location objects](#file-location-object) contains the location **and file size** of the in-network file for the associated [reporting plan object.](#reporting-plans-object) | Yes |
| **allowed_amount_file** | Allowed Amount File List | Object | The [file location object](#file-location-object) contains the location **and file size** of the allowed amounts file for the associated reporting plan object. | Yes |

#### Reporting Plans Object
| Field | Name | Type | Definition | Required |
| ----- | ---- | ---- | ---------- | -------- |
| **plan_name** | Plan Name | String | The plan name and name of plan sponsor and/or insurance company. | Yes |
| **plan_id_type** | Plan Id Type | String | Allowed values: "EIN" and "HIOS" | Yes |
| **plan_id** | Plan ID | String | The 10-digit Health Insurance Oversight System (HIOS) identifier, or, if the 10-digit HIOS identifier is not available, the 5-digit HIOS identifier, or if no HIOS identifier is available, the Employer Identification Number (EIN)for each plan or coverage offered by a plan or issuer. | Yes |
| **plan_market_type** | Market Type | String | Allowed values: "Large Group", "Small Group", and "Individual" | Yes |

#### File Location Object
| Field | Name | Type | Definition | Required |
| ----- | ---- | ---- | ---------- | -------- |
| **description** | Description | String | Description of the file included | Yes | 
| **location** | Description | String | A full fully qualified domain name on where the in-network data can be downloaded | Yes | 
| **file_size** | File Size | Number | Decompressed file size. Numeric value with two decimal places, expressed in units of Gigabytes | Yes


   
More details of the reporting_structure object and other JSON objects occurring in the ToC can be referenced via [this link](https://github.com/CMSgov/price-transparency-guide/tree/master/schemas/table-of-contents) in the federal schema.