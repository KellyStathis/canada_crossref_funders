# FRDR Controlled Vocabularies

This project provides tools to parse ROR and Crossref Funder Registry data into CSV files for FRDR.

## Research Organization Registry (ROR)
`RORJsonParser.py` parses the ROR data dump (JSON) to a CSV file for use in FRDR affiliation metadata. 

Optionally, it can process an override file which specifies a name in English, a name in French, and additional alternate names for specified ROR IDs. Overrides should be specified in TSV format with columns **id**, **name_en**, **name_fr**, and **altnames**.

Usage: `python RORJsonParser.py --data ror-data.json --override ror_overrides.tsv`

The output file `frdr_affiliation_metadata.csv` has the following columns:

-  **id**: ROR ID
-  **country_code**: two-letter country code from ROR
-  **name_en**: main name in ROR or name_en from override file
-  **name_fr**: main name in ROR or name_fr from override
-  **altnames**: all labels, aliases, and acronyms in ROR - plus all altnames specified in override file - delimited by "||"


## Crossref Funder Registry
`FundrefRDFParser.py` parses the Crossref Funder Registry RDF file to a CSV file for use in FRDR funding metadata.

### Flags
Usage: `python FundrefRDFParser.py --graphpickle --metadatacsv`

- Step 1: `--graphpickle`: Generate registry.pickle from registry.rdf.
- Step 2: `--metadatacsv`: Generate funder_metadata.csv from registry.pickle.

Optional `--exporttype` argument can be used to change the output of step 2 (`--metadatacsv` flag):

- `--exporttype frdr`: Only include the columns *id*, *primary_name*, *additional_names*, *dcterms_created*, *dcterms_modified*, and *crossref_country*. Do not include funders with termstatus "Deprecated" or funders that have been superseded by a new funder.
- `--exporttype canada`: Optional processing for Canadian funders, including:
    - separating out labels by language to support usage in bilingual applications
    - adding related ROR IDs
    - replacing geonames URIs for Canada and the provinces/territories with names

## Workflow Documentation
- [ROR: Workflows for FRDR](https://docs.google.com/document/d/1-5n_A9Wo9OzVdQ6OYk0vIKF0khsY6iQu3REMBGWP5K4/edit#)
- [Crossref Funder Registry: Workflows for FRDR](https://docs.google.com/document/d/1swDZqb94xdmpEnHjKakF_DI_mXHRVIYcsodEBRPG1r0/edit#)









