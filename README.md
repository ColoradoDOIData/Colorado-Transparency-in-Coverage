# Colorado Transparency in Coverage

This is the technical implementation guide for the machine-readable files (MRF) in accordance with the Colorado Transparency in Coverage statute and rule.

## Background
The federal government issued Transparency in Coverage [final rules (885 FR 72158)](https://www.federalregister.gov/documents/2020/11/12/2020-24591/transparency-in-coverage) on November 12, 2020, and enforcement began on July 1, 2022.
In 2024, Colorado passed [Senate Bill 24-080](https://leg.colorado.gov/bills/sb24-080) to require insurers, carriers, and pharmacy benefit managers to start posting Colorado-specific healthcare pricing data on July 1, 2025. In April 2025, [regulation 4-2-103](https://doi.colorado.gov/announcements/notice-of-adoption-regulation-4-2-103-concerning-transparency-in-coverage-reporting) went into effect, further outlining the reporting requirements.
The goal of these policies is to make the pricing data more relevant and usable for Colorado consumers, employers, and researchers alike.
Plans and issuers are required to share these files with the Colorado Division of Insurance ("the Division") beginning on July 1, 2025, and every 6 months thereafter.

## Timeline
Beginning July 1, 2025, and January 1, 2026, and each July and January thereafter each carrier shall make publicly available and submit files to the Division.   
The secure file transfer mechanism is still being established by the Division and its Office of Information Technology, and carriers are encouraged to work with the Division to test the process starting June 1, 2025.  

## Guidance
The Colorado specific files do not differ from the federal files with the exception of making the files Colorado specific, therefore much of this guidance is a duplicate of what CMS has provided.   
You can find recently released federal guidance here:  
- [CMS TiC GitHub Repository](https://github.com/CMSgov/price-transparency-guide)

## Developer Documentation
### File Transfer Mechanism - coming soon   
In addition to making the MRFs publicly available on July 1, 2025, carriers must also submit the MRFs to the Division.   
Instructions around the DOI's File Transfer system will be published around mid- to late-May, 2025. The Division’s goal is to have a fully secured platform that allows for automated submission of these files. However, due to state OIT resource constraints, the Division may have to develop a secure but partially manual submission for July 1, 2025. 
### Content Type
In accordance with Regulation 4-2-103, the Division will accept [**JSON**](https://www.json.org/) files. If a carrier can demonstrate a material challenge with creating JSON files, they may request a different format from the Division. Requests must be submitted to the Division two weeks before submission deadlines and must describe in detail the reasons why the carrier cannot create JSON files.  

Examples of formats that do *not* meet the criteria:
- PDF
- CSV
- XLS/XLSX

### Required Files
There are four required files associated with Colorado's Transparency in Coverage requirements:
1.	Table of Contents (JSON)
2.	In-Network Negotiated Rates (JSON)
3.	Out-of-Network Allowed Amounts (JSON)
4. RxDC Reports (CSV, or consistent with CMS' latest standards)

**Table of Contents File**: The Table of Contents file should be leveraged to combine common negotiated rates across multiple in-network files and avoid having to duplicate data. It must include:   
- Carrier name,  
- Plan name,  
- Market segment using the following categories:  
        - Individual, Small Group (<=100 employees>), Large Group (>100 employees); or  
        - TPA, identified by Group EIN or HIOS Plan ID,  
- File generation date,   
- URL link to plan specific files on the carrier’s website, and
- File size:  
        - Definition: we are asking for decompressed file sizes. As in, [the value that users get when running a content length header request](https://stackoverflow.com/questions/2773396/whats-the-content-length-field-in-http-header) after running gzip.decompress() on the URLs.  
        - Format: decimal numeric value with two decimal places, expressed in units of Gigabytes.   
        - The Division is open to receiving a separate metadata file that details file size information.

For reference, here is [the CMS guidance on the Table of Contents](https://github.com/CMSgov/price-transparency-guide/tree/master/schemas/table-of-contents).  

Where plans have the same rates, HIOS Plan IDs or Group EINs can be listed and point to the correct in network files rather than having duplicate files for each plan.  

**In-Network Negotiated Rates File**: Under the finalized federal rules, a plan or issuer must disclose in-network provider negotiated rates for all items and services through machine-readable files.  

**Out-Of-Network Allowed Amounts File**: Under the finalized federal rules, a plan or issuer must disclose certain data elements to the public, including the billed and allowed amounts for out-of-network providers, through machine-readable files.  

**Colorado Specific In-Network Negotiated Rates and Out-of-Network Allowed Amounts Filter**: The files listed above should be filtered to be Colorado specific in the following manner:  
1.	Only include plans issued or delivered in Colorado;  
2.	Only group or billing NPIs with a corresponding Colorado zip code; and  
3.	Only negotiated rate and procedure code combinations for providers with 20 or more services performed in the last year, at the procedure code level not accounting for modifiers. Modifiers must be included in the files, but do not change the count of claims a billing provider has for each procedure code.  

**RxDC reports**: under Section 204 of the CAA, Carriers and PBMs routinely submit information about prescription drugs and health care spending to CMS. This data submission is called the RxDC report, and is what the Division requires through Regulation 4-2-103. The RxDC files should be filtered to only contain data specific to plans in Colorado. Standards can be found via [this link](https://www.cms.gov/marketplace/about/oversight/other-insurance-protections/prescription-drug-data-collection-rxdc). These reports may contain PII or PHI. Carriers are not required to post these files publicly.  

Similar to Federal TiC guidance, carriers are highly encouraged to utilize an  optional MRF to significantly decrease file size and promote usability where applicable: [Provider Reference](https://github.com/CMSgov/price-transparency-guide/tree/master/schemas/provider-reference)  

**Provider Reference**: Defining provider networks outside of the In-Network file can have significant benefits in the overall file size that is produced. The provider reference file allows the user to define common provider networks externally to the In-Network file that can be referenced from within the In-Network file. This allows large provider networks to be defined once and be used in multiple locations.  

**Dates**: Files should contain current rates as of the date the files are created. Colorado files that are posted publicly to the carrier’s website should be the current or most recently submitted Colorado file and can be completely replaced once a new Colorado file is submitted (e.g. the January files may replace the previously posted July files).  Carriers do not need to keep historical files posted publicly.  

### Special Data Types
Dates should be strings in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601) (i.e. YYYY-MM-DD).

### Naming Convention  
Carriers should follow the same [naming convention provided in the federal TiC guidance](https://github.com/CMSgov/price-transparency-guide/tree/master?tab=readme-ov-file#file-naming-convention), but shall make sure to add 'CO' between date value and payer/issuer name, in order to distinguish any federal TiC files from Colorado TiC files: 
- `<YYYY-MM-DD>_CO_<payer or issuer name>_<plan name>_<file type name>.<file extension>`.  

**Single Plan Files**  
The following is the naming standard for each file:   
- `<YYYY-MM-DD>_'CO'_<payer or issuer name>_<plan name>_<file type name>.<file extension>`   

An example of a plan named "healthcare 100" with an issuer's name "issuer ABC" producing a JSON file, the following would be the naming output:  
- 2020-01-05_CO_issuer-ABC_healthcare-100_in-network-rates.json  

**Multiple Plans Per File**  
If multiple plans are to be included in a single file, a table-of-contents file will be required. The same naming standard will be applied to the table-of-contents file.  
The following is the required naming standard for the table-of-contents file:  
-  `<YYYY-MM-DD>_'CO'_<payer or issuer name>_index.<file extension>`

For example, the following would be the required naming for issuer ABC building a JSON file that includes multiple plans:  
- 2020-01-05_CO_issuer-ABC_index.json

### Public Discoverability
Under Section 5-C of Regulation 4-2-103, carriers shall include the URL link(s) to the files on their website. RxDC reports are not required to be posted on the website.  
#### Robots.txt
To allow for search engine discoverability, neither a robots.txt file nor meta tag on the page where the files are hosted will have rules such that give instructions to web crawlers to not index the page.
This typically follows the format of or for a robots.txt file using the Disallow directive.

### Federal Schemas  
With the exception of Table of Contents and one field in In-Network File, the Division will not publish its own schemas, since the content required is near-identical to that of the federal schemas. Instead, below are the links to the most current federal TiC file schema:  

[link to In-Network Rates Federal schema](https://github.com/CMSgov/price-transparency-guide/blob/master/schemas/in-network-rates/README.md)   
[link to Allowed Amounts Federal schema](https://github.com/CMSgov/price-transparency-guide/blob/master/schemas/allowed-amounts/README.md)  
[link to Table of Contents Federal schema](https://github.com/CMSgov/price-transparency-guide/blob/master/schemas/table-of-contents/README.md)  
[link to Provider Reference Federal schema](https://github.com/CMSgov/price-transparency-guide/blob/master/schemas/provider-reference/README.md)  

[Link to Colorad-specific Table of Content Schema]

### Examples  
[link to implementation examples](https://github.com/CMSgov/price-transparency-guide/tree/master/examples)  

## Exemption Process
Carriers who have **less than 30** enforced policies across the company’s combined plans may request an exemption by contacting the Division at the email address below.  

## Contact the Division
Please contact dora_ins_data@state.co.us for any questions or concerns.


