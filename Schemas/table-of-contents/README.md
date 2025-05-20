## Table of Contents File
The Division encourages carriers to utilize a Table of Contents file to decrease file sizes when rates across plans are identical. 

| Field | Name | Type | Definition | Required |
| ----- | ---- | ---- | ---------- | -------- |
| **reporting_entity_name** | Entity Name | String | The legal name of the entity publishing the machine-readable file. | Yes |
| **reporting_entity_type** | Entity Type | String | The type of entity that is publishing the machine-readable file (a group health plan, health insurance issuer, or a third party with which the plan or issuer has contracted to provide the required information, such as a third-party administrator, a health care claims clearinghouse, or a health insurance issuer that has contracted with a group health plan sponsor). | Yes |
| **version** | Version | String | The version of the schema for the produced information | Yes |
| **date** | Date | String | The date in which the file was generated. Date must be in an ISO 8601 format (i.e. YYYY-MM-DD) | Yes
| **file size** | File Size | Number | Decompressed file size. Numeric value with two decimal places, expressed in units of Gigabytes | Yes
| **reporting_structure** | Reporting Structure | Array | An array of [reporting structure object types](#reporting-structure-object) | Yes |

   
Details of the reporting_structure object and other JSON objects occurring in the ToC can be referenced via [this link](https://github.com/CMSgov/price-transparency-guide/tree/master/schemas/table-of-contents) in the federal schema.