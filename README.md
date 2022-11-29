# OCSF (Open Cyber Security Framework) Post-Processing Pack
----

This pack is designed to help map event fields into the OCSF data format (https://schema.ocsf.io/?extensions=) as a post-processor for specific destinations (verify that your downstream destination supports this data schema before sending events).

## Disclaimer

This pack is currently a _WORK IN PROGRESS_ and is only partially functional.

Currently the only fully functional class(es) from the OCSF schema is/are:

* Network Activity Class (4001)

Currently the only supported datasets with the above classes are:

* PAN:Traffic (4001)
* PAN:Threat (4001)

## Requirements Section

Before you begin, ensure that you have met the following requirements:

* Verified that your destination supports the **OCSF** data format and how that data is expected to be packaged (_JSON_ or _Parquet_).
* identified what data sources you want to convert to OCSF format and if it is currently supported by this pack.


## Using The Pack

To use this Pack, follow these steps:

1. Install this pack (okay, good so far...)
2. Make sure the datasets you want to process into OCSF format are supported
3. Attach this pack as a post-processing route for your desired destination
3. Recieve bacon



## Release Notes

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
