# OCSF (Open Cyber Security Framework) Post Processor
----

This pack is designed to help map event fields into the OCSF data format (https://schema.ocsf.io/?extensions=) as a post-processor for specific destinations (verify that your downstream destination supports this data schema before sending events). Please keep in mind this is primarily a development resource and is only partially functional, It's goal is to provide tooling and references for how to perform the needed mapping for OCSF.

PLEASE NOTE: This pack leverages a custom code function, please check the code function box when installing! the code function is used to convert complex field names to json objects in OCSF structure.

Currently the only supported datasets in this pack are:

* PAN:Traffic (4001)
* PAN:Threat (4001)
* ZScaler Web Logs (4002)
* ZScaler Firewall Logs (4001)

## Requirements Section

Before you begin, ensure that you have met the following requirements:

* Verified that your destination supports the **OCSF** data format and how that data is expected to be packaged (_JSON_ or _Parquet_).
* identified what data sources you want to convert to OCSF format and if it is currently supported by this pack or supported by another in the packs dispensary.

### Requirements for ZScaler

this pack expects the ZScaler-NSS output to be set to key value pair, and assumes that their is a sourcetype set of "zscalernss-fw" or "zscalernss-web". As our ZScaler lab gets setup we will adjust these values to make mapping easier.

## Using The Pack

To use this Pack, follow these steps:

1. Install this pack (okay, good so far...)
2. Make sure the datasets you want to process into OCSF format are supported
3. Attach this pack as a post-processing route for your desired destination
3. Recieve bacon

## Using The Pack With: AWS Security Lake

AWS Security Lake requires data to be written in parquet format. this means that the parquet schema is required, and all data must be mapped to match that schema. In an attempt to simplify this work for you, we have defined all the parquet schemas and set all fields to optional. What this means for you: you only need to map fields that make sense for your data (and the fields we call out below), then validate the field formats against the json schemas (included in this pack). In order to do this, you will still need to understand all the fields for the given OCSF class you are mapping against (http://schema.ocsf.io). 

Take a look at the PAN pipeline as a reference to build from, this pipeline also includes a validation function to confirm your mapping is correct. If you recieve a failure on the validation, you can leverage (https://www.jsonschemavalidator.net/) to see all schema failures and fix them.

If you need the parquet schemas the are located in the docs folder of this pack, see the github project here: https://github.com/asc-me-cribl/cribl_ocsf_postprocessing/tree/main/docs

### Fields You Need To map

the following fields are leveraged for sending data to AWS Security Lake, and if are not assigned will cause issues for the destination:
* "class_uid" - (the OCSF class id)
* "metadata.product.vendor_name" - (the name of the vendor of whose data you are mapping)
* "metadata.version" - (the version of OCSF that you are mapping against)
* "raw_data" - (a rename of the _raw field as a string)
* "time" - (this is epoch time in milliseconds, you will likely need to multiple your time field by 1000000)

## Release Notes
___
### Version 1.0 - 2023-05-30
this first production ready release focuses on tooling and sample pipelines. What has changed in this release:
* 3 production ready pipelines for PAN and ZScaler datasets
* JSON schema maps for validating against all released OCSF classes
* Parquet schema maps for sending data in parquet to a S3 destination or AWS Security Lake
* Removed all outdated pipelines

### Version 0.1 - 2022-11-29
this initial release provides the barebones for building complete mapping for OCSF. this release includes:
* Initial WIP pipelines for all 'Network Activity' classes
* One fully working 'DEMO' pipeline for class 4001 with two working datasets (PAN:Traffic, PAN:Threat)
* A Parquet Schema for writing events from the demo pipeline into s3 in Parquet format


## Contributing to the Pack
To contribute to the Pack, please do the following:

* Fork the repo on github
* Add your desired code change with documentation
* Open a PR for me to review it!

not wanting to submit code? thats okay too, send me an email at the address below and i'll open a jira in my backlog for your idea.


## Contact
To contact us please email <acain@cribl.io>.


## License
This Pack uses the following license: Apache 2.0
