# **Welcome to GSDC TEM Users Guide**

These pages refer to the GSDC TEM users guide of the new AlmaLinux 9.x based TEM cluster.

For the document of the old ScientificLinux 7.x based system, please visit [Scientific Linux 7.x based GSDC TEM Users Guide](https://tem-docs.readthedocs.io/en/latest).

## **Notice**

???+ tip "GSDC TEM Farm Preventive Maintenance (PM) Downtime"

    Please be informed that the GSDC TEM Farm will undergo scheduled preventive maintenance (PM), resulting in temporary system downtime.
    Kindly review the schedule below and plan your use of the farm accordingly.

    1. Maintenance Schedule

    November 17 (Mon), 2025, 10:00 AM – November 20 (Thu), 2025, 6:00 PM

    2. Maintenance Details
	• Storage firmware upgrade for the TEM Farm
	• Additional IP routing configuration for storage management and service allocation
	• Lustre Client Kernel module upgrade across all TEM Farm nodes (from 2.15.0.4 to 2.15.6.1)



???+ tip "Creating tickets to request the support for resolving techinical problems/errors using GSDC services"

    Since March 2021, we launched GSDC ticketing system to support all the technical problems for users/operators, so feel free to create tickets. 
    
    `"Creating tickets"` simply means sending an e-mail to the following e-mail recipient. Based on the e-mail title's prefix, the tickets will be automatically assigned to the person in charge on our ticketing system.
    
    E-mail address : __gsdc-support at kisti.re.kr__ (__[TEM]__ prefix required in the e-mail subject)



## **Change Log**

* `2025-06-18` - OS upgrades and migration completed
* `2025-05-14` - AlmaLinux9-based TEM users guide released
* `2025-04-21` - DevOps codes for all the analysis tools have been refactored and distributed on the new cluster system
* `2025-02-28` - We are under migrating all the service nodes OS from ScientificLinux 7.x to AlmaLinux 9.x