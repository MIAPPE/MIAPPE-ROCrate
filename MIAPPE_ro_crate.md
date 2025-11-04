[TOC]

# MIAPPE RO-Crate Profile

* Version: 1.0.0-draft.1
* Permalink: _coming soon_
* Authors
  * Cyril Pommier - https://orcid.org/0000-0002-9040-8733
  * Emma Leroy Pardonche
  * Etienne Bardet
  * ...
* Forked from [ROCrate-ISA profile](https://github.com/nfdi4plants/isa-ro-crate-profile/blob/release/profile/isa_ro_crate.md)
* 


## Overview

A significant part of the previous work on this [RO-Crate](https://www.researchobject.org/ro-crate/) profile for [MIAPPE](https://isa-tools.org/index.html) was produced as part of the Harvest and Agroserv project 

This profile iterate over the previous [ROCrate-ISA profile](https://github.com/nfdi4plants/isa-ro-crate-profile/blob/release/profile/isa_ro_crate.md) that was created during the [ELIXIR Biohackathon 2023](https://biohackathon-europe.org/), as part of [Project 14: Enabling continuous RDM using Annotated Research Contexts with RO-Crate profiles for ISA](https://github.com/elixir-europe/biohackathon-projects-2023/tree/main/14), the profile was further fine tuned and defined, and some remaining unresolved mappings resolved.

<!--[Annotated Research Context (ARC)](https://nfdi4plants.org/content/learn-more/annotated-research-context.html) project, through [arc-to-rocrate](https://github.com/nfdi4plants/arc-to-rocrate).

The profile got forked and iterated upon during [ELIXIR Biohackathon 2025](https://biohackathon-europe.org/)

The aim of the profile is to be able to fully represent [ISA-JSON](https://isa-specs.readthedocs.io/en/latest/isajson.html) as RO-Crate, fully capturing the metadata and files in a non-lossy form such that it
should be possible to convert between one to the other, in either direction, without loss of information.

The ISA RO-Crate has led to a few changes to [Bioschemas](https://bioschemas.org/) types:
  
**LabProtocol** - Has been redefined as a child of [HowTo](https://schema.org/HowTo) to make it clearer that it is intended to specifically describe the planned instructions for a lab process.

**LabProcess** - A new type has been defined as a child of [Action](https://schema.org/Action), to specifically describe the details and outcomes of an executed LabProtocol.
Thereby separating the "what was planned" and "what happened" between LabProtocol and LabProcess respectively.
A working group is working on the new type and adaptations of existing types.

An important change to the [Bioschemas](https://bioschemas.org/) specification that is still pending is the following:

**Dataset** - A new property _processSequence_ to describe how the Dataset was created.

The following graph summarizes the ISA model in terms of [Bioschemas](https://bioschemas.org/)/[Schema.org](https://schema.org/) vocabulary:--->


## Requirements

### Investigation

Is based upon [schema.org/Dataset](https://schema.org/Dataset) and maps to the [MIAPPE Investigation](https://github.com/MIAPPE/MIAPPE/blob/master/MIAPPE_Checklist_Data_Model.tsv)

| Property | Required | Expected Type | Description |
|----------|----------|---------------|-------------|
|@id|MUST|Text or URL|Should be “./”, the investigation object represents the root data entity.|
|@type|MUST|Text|MUST be '[schema.org/Dataset](https://schema.org/Dataset)'|
|additionalType|MUST|Text or URL|‘Investigation’ or ontology term to identify it as an Investigation|
|identifier|SHOULD|Text or URL|Identifying descriptor of the investigation MIAPPE.Investigation.investigationId.|
|name|MUST|Text|Human-readable string summarising the investigation.investigationTitle.|
|description|SHOULD|Text|Human-readable text describing the investigation in more detail.    gation.investigationDescription.|
|license|SHOULD|Text or URL| License for the reuse of the data associated with this investigation. The Creative Commons licenses cover most use cases and are recommended. When no license information is available on crate creation, use the default string `'ALL RIGHTS RESERVED BY THE AUTHORS'` |
|datePublished|COULD|DateTime|When the Investigation was published. If the Investigation is not (yet) published, use the date of the crate creation as default value.|
|dateSubmitted|COULD|DateTime|When the Investigation was published. If the Investigation is not (yet) published, use the date of the crate creation as default value.|
|creator|SHOULD|[schema.org/Person](#person)|The creator(s)/authors(s)/owner(s)/PI(s) of the investigation.|
|dateCreated|SHOULD|DateTime|When the Investigation was created|
|hasPart|SHOULD|[schema.org/Dataset](https://schema.org/Dataset) ([Study](#study))|An Investigation object should contain other datasets representing the _studies_ of the investigation. The dataset objects in this list MUST follow the [Study profile](#study) defined in this document.|
|citation|COULD|[schema.org/ScholarlyArticle](#scholarlyarticle)|Publications corresponding with this investigation.|
|comment|COULD|[schema.org/Comment](#comment)|Comment|
|dateModified|COULD|DateTime|When the Investigation was last modified|
|mentions|COULD|[schema.org/DefinedTermSet](https://schema.org/DefinedTermSet)|Ontologies referenced in this investigation.|
|url|COULD|URL|The filename or path of the metadata file describing the investigation.|

### Study

Is based upon [schema.org/Dataset](https://schema.org/Dataset) and maps to the [MIAPPE Study]([MIAPPE Investigation](https://github.com/MIAPPE/MIAPPE/blob/master/MIAPPE_Checklist_Data_Model.tsv))

| Property | Required | Expected Type | Description |
|----------|----------|---------------|-------------|
|@id|MUST|Text or URL|Should be a subdirectory corresponding to this study.|
|@type|MUST|Text|MUST be '[schema.org/Dataset](https://schema.org/Dataset)'|
|additionalType|MUST|Text or URL|‘Study’ or ontology term to identify it as a Study|
|identifier|MUST|Text or URL|Identifying descriptor of the study. MIAPPE.Study.studyId.|
|name|MUST|Text|Name, human-readable text summarising the study.|
|description|SHOULD|Text|Human-readable text describing the study (e.g an abstract)|
|studyStartDate|MUST|Date/Time (ISO 8601, optional time zone)|Date and, if relevant, time when the experiment started .|
|studyEndDate|SHOULD|Date/Time (ISO 8601, optional time zone)|Date and, if relevant, time when the experiment ended .|
|hasPerson|SHOULD|[schema.org/Person](#person)|The performers of the study.|
|dateCreated|SHOULD|DateTime|When the Study was created|
|datePublished|SHOULD|DateTime|When the Study was published|
|hasPart|SHOULD|[schema.org/Dataset](https://schema.org/Dataset) ([Assay](#assay)) or [File](https://schema.org/MediaObject)|Assays contained in this study or actual data files |
|/!\ PROPOSITION hasBiologicalMaterial|  MUST |[bioschemas.org/Sample](https://bioschemas.org/Sample) | Identifier of a biological material follwoing the schemas decalred below. MUST be a sample of additionalType "MIAPPE Biological Material" |
|/!\ PROPOSITION hasObservedVariable|  MUST |Text | Identifier (variableId) of an observedVariable follwoing the schemas decalred below.  |
|/!\ PROPOSITION hasDatafile|  SHOULD|[schema.org/Dataset](https://schema.org/Dataset)  or [File](https://schema.org/MediaObject)| Data contained in this study or actual data files |
|citation|COULD|[schema.org/ScholarlyArticle](#scholarlyarticle)|A publication corresponding to the study.|
|comment|COULD|[schema.org/Comment](#comment)|Comment|
|dateModified|COULD|DateTime|When the Study was last modified|
|url|COULD|URL|The filename or path of the metadata file describing the study. |
|contactInst|MUST| Text	|Name and address of the institution responsible for the study.|
|locationCountry|MUST| /!\ PROPOSITION Country name or 2-letter code (ISO 3166)	|The country where the experiment took place, either as a full name or preferably as a 2-letter code.|
|siteName|MUST|	Text |The name of the natural site, experimental field, greenhouse, phenotyping facility, etc. where the experiment took place.|
|locationLatitude|SHOULD|/!\ PROPOSITION degree decimal format (ISO 6709) |Latitude of the experimental site in degrees, in decimal format.|
|locationLongitude|SHOULD| /!\ PROPOSITION degree decimal format (ISO 6709)  |Longitude of the experimental site in degrees, in decimal format.|
|locationAltitude|SHOULD| /!\ PROPOSITION Numeric + unit abbreviation | Altitude of the experimental site, provided in metres (m).|
|expeDesignDesc|MUST| Text |Short description of the experimental design, possibly including statistical design. In specific cases, e.g. legacy datasets or data computed from several studies, the experimental design can be "unknown"/"NA", "aggregated/reduced data", or simply "none".|
|expeDesignType |COULD| URL or Text |Type of experimental design of the study, in the form of an accession number from the Crop Ontology (subclass of "CO_715:0000003" from https://agroportal.lirmm.fr/ontologies/CO_715)|
|obsUnitLevelHierarchy|COULD| Text |Hierarchy of the different levels of repetitions between each others|
obsUnitDesc	|MUST| Text |General description of the observation units in the study.|
|growthFacilityDesc|MUST| Text |Short description of the facility in which the study was carried out.|
|growthFacilityType|SHOULD| Text or URL |Type of growth facility in which the study was carried out, in the form of an accession number from the Crop Ontology (subclass of "CO_715:0000005" from https://agroportal.lirmm.fr/ontologies/CO_715)|
|culturalPractice|COULD| Text | General description of the cultural practices of the study.|
|expeDesignMap|COULD| Text or URL |Representation of the experimental design.|


### Assay

Is based upon [schema.org/Dataset](https://schema.org/Dataset) and maps to the [ISA-JSON Assay](https://isa-specs.readthedocs.io/en/latest/isajson.html#assay-schema-json)

| Property | Required | Expected Type | Description |
|----------|----------|---------------|-------------|
|@id|MUST|Text or URL|Should be a subdirectory corresponding to this assay.|
|@type|MUST|Text|MUST be '[schema.org/Dataset](https://schema.org/Dataset)'|
|additionalType|MUST|Text or URL|‘Assay’ or ontology term to identify it as an Assay|
|identifier|MUST|Text or URL|Identifying descriptor of the assay.|
|name|SHOULD|Text|A title of the assay.|
|description|SHOULD|Text|A short description of the assay (e.g. an abstract).|
|about|SHOULD|[bioschemas.org/LabProcess](#labprocess)|The experimental processes performed in this assay.|
|creator|SHOULD|[schema.org/Person](#person)|The performer of the experiments.|
|hasPart|SHOULD|[File](https://schema.org/MediaObject)|The data files resulting from the process sequence. MUST not be used to directly point to data fragments.|
|measurementMethod|SHOULD|URL or [schema.org/DefinedTerm](#definedterm)|Describes the type measurement e.g Complexomics or Transcriptomics as an ontology term|
|measurementTechnique|SHOULD|URL or [schema.org/DefinedTerm](#definedterm)|Describes the type of technology used to take the measurement, e.g mass spectrometry or deep sequencing|
|comment|COULD|[schema.org/Comment](#comment)|Comment|
|url|COULD|URL|The filename or path of the metadata file describing the assay. Optional, since in some contexts like an ARC the filename is implicit.|
|variableMeasured|COULD|Text or [schema.org/PropertyValue](#propertyvalue)|The target variable being measured E.g protein concentration|

### Biological Material
Is based upon [MIAPPE Biological Material](https://github.com/MIAPPE/MIAPPE/blob/master/MIAPPE_Checklist_Data_Model.tsv) which borrows concepts from ISA Source and Material. The biological material being studied (e.g. plants grown from a certain bag or seed, or plants grown in a particular field). The original source of that material (e.g., the genebank accession or the commercial variety or the laboratory mutant or line) is called the material source, which, when held by a material repository, should have its stock identified.


| Property | Required | Expected Type | Description |
|----------|----------|---------------|-------------|
|@id|MUST|Text or URL|Could be the unique biologicalMaterialId.|
|@type |MUST|Text|MUST be '[bioschemas.org/Sample](https://bioschemas.org/Sample)'|
|additionalType|MUST|Text or URL| Must have the value  "MIAPPE Biological Material". Can also be taken in PPEO.
|biologicalMaterialId|MUST|Unique identifier|Code used to identify the biological material in the data file. Should be unique within the Investigation. Can correspond to experimental plant ID, seed lot ID, etc… This material identification is different from a BiosampleID which corresponds to Observation Unit or Samples sections below.
|biologicalMaterialExtId|SHOULD|Semicolon-separated list of unique identifiers, possibly prefixed by repository name|One to many identifiers for the biological material. Can include EBI Biosamples ID. URI are recommended when possible.
|organism|SHOULD|Unique identifier|An identifier for the organism at the species level. Use of the NCBI taxon ID is recommended. <!-- See bioschemas.org taxonomicRange and studies -->
|genus|SHOULD|Genus name|Genus name for the organism under study, according to standard scientific nomenclature.
|species|SHOULD|Species name|Species name (formally: specific epithet) for the organism under study, according to standard scientific nomenclature.
|infraspecificName|SHOULD|Key-value pair list, or MCPD-compliant format|Name of any subtaxa level, including variety, crossing name, etc. It can be used to store any additional taxonomic identifier. To be filled as key-value pair list format (the key is the name of the rank/category and the value is the value of  the rank/category). Ranks/categories can be among the following terms: subspecies, cultivar, variety, subvariety, convariety, group, subgroup, hybrid, line, form, subform. For MCPD compliance, the following abbreviations are allowed: "subsp." (subspecies); "convar." (convariety); "var." (variety); "f." (form); "Group" (cultivar group). MIAPPE adds "cv." (cultivar).
|biologicalMaterialLatitude|COULD (MUST if longitude is provided)|Degrees in the decimal format (ISO 6709)|Latitude of the studied biological material. [Alternative identifier for in situ material]
|biologicalMaterialLongitude|COULD (MUST if latitude is provided)|Degrees in the decimal format (ISO 6709)|Longitude of the studied biological material. [Alternative identifier for in situ material]
|biologicalMaterialAltitude|COULD |Numeric + unit abbreviation|Altitude of the studied biological material, provided in meters (m). [Alternative identifier for in situ material]
|biologicalMaterialCoordUncertainty|COULD|Numeric|Circular uncertainty of the coordinates, preferably provided in meters (m). [Alternative identifier for in situ material]
|biologicalMaterialPreprocessing|COULD|Plant Environment Ontology and/or free text|Description of any process or treatment applied uniformly to the biological material, prior to the study itself. Can be provided as free text or as an accession number from a suitable controlled vocabulary.
|materialSourceId|SHOULD|Unique identifier|An identifier for the source of the biological material, in the form of a key-value pair comprising the name/identifier of the repository from which the material was sourced plus the accession number of the repository for that material. Where an accession number has not been assigned, but the material has been derived from the crossing of known accessions, the material can be defined as follows: "mother_accession X father_accession", or, if father is unknown, as "mother_accession X UNKNOWN". For in situ material, the region of provenance may be used when an accession is not available. The Material source is commonly called germplasm, accession, genotype and even variety for commercial varieties. For the latest, keep in mind that a variety is commonly ambiguously identified and polysemous
|materialSourceDoi|SHOULD|DOI|Digital Object Identifier (DOI) of the material source
|materialSourceAccNumber|COULD|Unique identifier|Unique identifier for accessions within a genebank. If material source is not from a genebank, use a laboratory ID. In the case of a commercial variety, use the variety code, or name if no code available.
|materialSourceAccName| COULD | Text |Can be: (i)genebank accession registered name or other designation given to the material, other than the donor"s accession number or collecting number. (ii) Variety name.
|materialSourceInstCode| COULD |Unique identifier|FAO WIEWS code of the institute where the accession is maintained. The current set of institute codes is available from https://www.fao.org/wiews. If no institute code is available, create your own (Laboratory acronym or research institute acronym ...).
|materialSourceInstName| COULD |Institute name|Name of the material source institute.
|materialSourceOtherIds| COULD |Key:Value pairs|Any other identifiers known to exist in other collections for this material source. Use key:value pairs, separated by semicolons.
|materialSourceLatitude| COULD ( MUST if longitude is provided)|Degrees in the decimal format (ISO 6709)|Latitude of the material source. [Alternative identifier for in situ material]
|materialSourceLongitude| COULD ( MUST if latitude is provided)|Degrees in the decimal format (ISO 6709)|Longitude of the material source. [Alternative identifier for in situ material]
|materialSourceAltitude| COULD |Numeric + unit abbreviation|Altitude of the material source, provided in metres (m). [Alternative identifier for in situ material]
|materialSourceCoordUncertainty| COULD |Numeric + unit abbreviation|Circular uncertainty of the coordinates, provided in meters (m). [Alternative identifier for in situ material]
|materialSourceDesc| COULD | Text |Description of the material sourc




### Sample

Is based on the Bioschemas [bioschemas.org/Sample](https://bioschemas.org/Sample) type, and represents the ISA-JSON [Sample](https://isa-specs.readthedocs.io/en/latest/isajson.html#sample-schema-json),
[Source](https://isa-specs.readthedocs.io/en/latest/isajson.html#source-schema-json) and [Material](https://isa-specs.readthedocs.io/en/latest/isajson.html#material-schema-json)

| Property | Required | Expected Type | Description |
|----------|----------|---------------|-------------|
|@id|MUST|Text or URL|Could be the unique sample name.|
|@type |MUST|Text|MUST be '[bioschemas.org/Sample](https://bioschemas.org/Sample)'|
|name|MUST|Text|A name identifying the sample.|
|additionalProperty|SHOULD|[schema.org/PropertyValue](https://schema.org/PropertyValue) ([Characteristic](#propertyvalue---characteristic) or [Factor](#propertyvalue---factor))|characteristics or factors|


### Observed Variable
Is based upon [MIAPPE Observed Variable](https://github.com/MIAPPE/MIAPPE/blob/master/MIAPPE_Checklist_Data_Model.tsv).


| Property | Required | Expected Type | Description |
|----------|----------|---------------|-------------|
|@id|MUST|Text or URL|Could be the unique variableId.|
|@type |MUST|Text| /!\ which type ?|
|additionalType|MUST|Text or URL| Must have the value "MIAPPE Observed Variable". Can also be taken in PPEO.
|variableId|MUST|Text|Code used to identify the variable in the data file. We recommend using a variable definition from the Crop Ontology where possible. Otherwise, the Crop Ontology naming convention is recommended: <trait abbreviation>_<method abbreviation>_<scale abbreviation>). A variable ID must be unique within a given investigation.
|variableName|SHOULD|Text|Name of the variable.
|variableAccNumber|COULD|Text or URL|Accession number of the variable in the Crop Ontology
|traitName|MUST|Text|Name of the (plant or environmental) trait under observation
|traitEntity|COULD|Text|Entity (part of the plant, whole plant, group of plant e.g. canopy) on which the trait has been measured
|traitEntityAccessionNumber|COULD|Text or URL|Accession number of the trait entity in a suitable controlled vocabulary (Plant Ontology). Term from Plant Trait Ontology, Crop Ontology, or XML Environment Ontology
|traitCharacteristic|COULD|Text|Characteristic measured. It can be a morphological characteristic (size, volume, surface), a molecular characteristic (sugar concentration), etc...
|traitCharacteristicAccessionNumber|COULD|Text or URL|Accession number of the trait characteristic in a suitable controlled vocabulary (PATO - the Phenotype And Trait Ontology). Term from Plant Trait Ontology, Crop Ontology, or XML Environment Ontology
|traitAccNumber|COULD|Text or URL|Accession number of the trait in a suitable controlled vocabulary (Crop Ontology, Trait Ontology). Term from Plant Trait Ontology, Crop Ontology, or XML Environment Ontology
|methodName|MUST|Text|Name of the method of observation
|methodAccNumber|COULD|Text or URL|Accession number of the method in a suitable controlled vocabulary (Crop Ontology, Trait Ontology). Term from Plant Trait Ontology, Crop Ontology, or XML Environment Ontology
|methodDesc|SHOULD|Text|Textual description of the method, which may extend a method defined in an external reference with specific parameters, e.g. growth stage, inoculation precise organ (leaf number)
|methodRef|COULD|Text or URL|URI/DOI of reference describing the method.
|scaleName|MUST|Text|Name of the scale associated with the variable
|scaleAccNumber|COULD|Text or URL|Accession number of the scale in a suitable controlled vocabulary (Crop Ontology).
|timeScale|COULD|Text|Name of the scale or unit of time with which observations of this type were recorded in the data file (for time series studies).



### Data

Describes and points to a Data file <!-- maps to the [ISA-JSON Data](https://isa-specs.readthedocs.io/en/latest/isajson.html#data-schema-json)-->

| Property | Required | Expected Type | Description |
|----------|----------|---------------|-------------|
|@id|MUST|Text or URL|Should be the path pointing to the file|
|@type |MUST|Text|MUST be 'File' or 'MediaObject'|
|name|MUST|Text or URL|The name of the file.|
|comment|COULD|[schema.org/Comment](#comment)|Comment|
|disambiguatingDescription|COULD|Text|The type of the data file (“Raw Data File", “Derived Data File" or "Image File").|
|encodingFormat|COULD|Text of URL|Media format as a MIME type|
|hasPart|COULD|Text of URL|Data fragments of this Data object, described by [data fragment selectors](https://www.w3.org/TR/annotation-model/#fragment-selector). SHOULD not be used on data fragments.|
|usageInfo|COULD|Text of URL|Description/specification of the [data fragment selector](https://www.w3.org/TR/annotation-model/#fragment-selector), if the object describes a data fragment and a selector is present in the path/`@id`. SHOULD only be used on data fragments.|

### Person

It is based on [schema.org/Person](https://schema.org/Person), and maps to the MIAPPE-PERSON <!--[ISA-JSON Person](https://isa-specs.readthedocs.io/en/latest/isajson.html#person-schema-json) -->

| Property | Required | Expected Type | Description |
|----------|----------|---------------|-------------|
|@id|MUST|Text or URL||
|@type |MUST|Text|MUST be '[schema.org/Person](https://schema.org/Person)'|
|givenName|MUST|Text|Given name of a person. Can be used for any type of name.|
|affiliation|MUST|[schema.org/Organization](https://schema.org/Organization)||
|email|SHOULD|Text||
|familyName|SHOULD|Text|Family name of a person.|
|identifier|SHOULD|Text or URL or [schema.org/PropertyValue](#propertyvalue)|One or many identifiers for this person, e.g. an ORCID. Can be of type PropertyValue to indicate the kind of reference.|
|jobTitle|MUST|[schema.org/DefinedTerm](#definedterm)||
|additionalName|COULD|Text||
|address|COULD|PostalAddress or Text||
|disambiguatingDescription|COULD|Text||
|telephone|COULD|Text||



### ScholarlyArticle
    
It is based on [schema.org/ScholarlyArticle](https://schema.org/ScholarlyArticle) and maps to the [ISA-JSON Publication](https://isa-specs.readthedocs.io/en/latest/isajson.html#publication-schema-json)

| Property | Required | Expected Type | Description |
|----------|----------|---------------|-------------|
|@id|MUST|Text or URL||
|@type |MUST|Text|MUST be '[schema.org/ScholarlyArticle](https://schema.org/ScholarlyArticle)'|
|headline|MUST|Text||
|identifier|MUST|Text or URL or [schema.org/PropertyValue](#propertyvalue)|One or many identifiers for this article like a DOI or PubMedID. Can be of type PropertyValue to indicate the kind of reference (See details in Section on PropertyValue).|
|author|SHOULD|[schema.org/Person](#person)||
|creativeWorkStatus|COULD|[schema.org/DefinedTerm](#definedterm)|The status of the publication in terms of its stage in a lifecycle.|
|comment|COULD|[schema.org/Comment](#comment)|Comment|

### DefinedTerm

It is based on [schema.org/DefinedTerm](https://schema.org/DefinedTerm) and maps to the [ISA-JSON OntologyAnnotation](https://isa-specs.readthedocs.io/en/latest/isajson.html#ontology-annotation-schema-json)

| Property | Required | Expected Type | Description |
|----------|----------|---------------|-------------|
|@id|MUST|Text or URL||
|@type |MUST|Text|MUST be '[schema.org/DefinedTerm](https://schema.org/DefinedTerm)'|
|name|MUST|Text|The term name.|
|termCode|SHOULD|Text|The identifier within the ontology.|
|inDefinedTermSet|COULD|URL or [schema.org/DefinedTermSet](https://schema.org/DefinedTermSet)|Link to the ontology.|
|disambiguatingDescription|COULD|Text|ISA comments|

### PropertyValue

General profile for key-value pairs. It is based on [schema.org/PropertyValue](https://schema.org/PropertyValue).

| Property | Required | Expected Type | Description |
|----------|----------|---------------|-------------|
|@id|MUST|Text or URL||
|@type |MUST|Text|MUST be '[schema.org/PropertyValue](https://schema.org/PropertyValue)'|
|name|MUST|Text|Key name|
|value|SHOULD|Text|Value text or number|
|propertyID|SHOULD|URL|Key ontology reference|
|additionalType|Could|Text|Can be used to further clarify the type of this property|
|unitCode|COULD|URL|Unit ontology reference|
|unitText|COULD|Text|Unit name|
|valueReference|COULD|URL|Value ontology reference|

#### PropertyValue - Parameter

Represents a process parameter. It is based on [schema.org/PropertyValue](https://schema.org/PropertyValue) and maps to the ISA-JSON Key-Value-Unit Triples [Process Parameter Value](https://isa-specs.readthedocs.io/en/latest/isajson.html#process-parameter-value-schema-json).

| Property | Required | Expected Type | Description |
|----------|----------|---------------|-------------|
|@id|MUST|Text or URL||
|@type |MUST|Text|MUST be '[schema.org/PropertyValue](https://schema.org/PropertyValue)'|
|name|MUST|Text|Key name|
|additionalType|MUST|Text|MUST be `"ParameterValue"`|
|value|SHOULD|Text|Value text or number|
|propertyID|SHOULD|URL|Key ontology reference|
|unitCode|COULD|URL|Unit ontology reference|
|unitText|COULD|Text|Unit name|
|valueReference|COULD|URL|Value ontology reference|

#### PropertyValue - Characteristic

Represents a characteristic. It is based on [schema.org/PropertyValue](https://schema.org/PropertyValue) and maps to the ISA-JSON Key-Value-Unit Triple [Material Attribute Value](https://isa-specs.readthedocs.io/en/latest/isajson.html#material-attribute-value-schema-json).

| Property | Required | Expected Type | Description |
|----------|----------|---------------|-------------|
|@id|MUST|Text or URL||
|@type |MUST|Text|MUST be '[schema.org/PropertyValue](https://schema.org/PropertyValue)'|
|name|MUST|Text|Key name|
|additionalType|MUST|Text|MUST be `"CharacteristicValue"`|
|value|SHOULD|Text|Value text or number|
|propertyID|SHOULD|URL|Key ontology reference|
|unitCode|COULD|URL|Unit ontology reference|
|unitText|COULD|Text|Unit name|
|valueReference|COULD|URL|Value ontology reference|

#### PropertyValue - Factor

Represents a factor. It is based on [schema.org/PropertyValue](https://schema.org/PropertyValue) and maps to the ISA-JSON Key-Value-Unit Triple [Factor Value](https://isa-specs.readthedocs.io/en/latest/isajson.html#factor-value-schema-json).

| Property | Required | Expected Type | Description |
|----------|----------|---------------|-------------|
|@id|MUST|Text or URL||
|@type |MUST|Text|MUST be '[schema.org/PropertyValue](https://schema.org/PropertyValue)'|
|name|MUST|Text|Key name|
|additionalType|MUST|Text|MUST be `"FactorValue"`|
|value|SHOULD|Text|Value text or number|
|propertyID|SHOULD|URL|Key ontology reference|
|unitCode|COULD|URL|Unit ontology reference|
|unitText|COULD|Text|Unit name|
|valueReference|COULD|URL|Value ontology reference|

#### PropertyValue - Component

Represents a protocol component. It is based on [schema.org/PropertyValue](https://schema.org/PropertyValue) and maps to the a component of an [ISA-JSON protocol](https://isa-specs.readthedocs.io/en/latest/isajson.html#protocol-schema-json).

| Property | Required | Expected Type | Description |
|----------|----------|---------------|-------------|
|@id|MUST|Text or URL||
|@type |MUST|Text|MUST be '[schema.org/PropertyValue](https://schema.org/PropertyValue)'|
|name|MUST|Text|Key name|
|additionalType|MUST|Text|MUST be `"Component"`|
|value|SHOULD|Text|Value text or number|
|propertyID|SHOULD|URL|Key ontology reference|
|valueReference|COULD|URL|Value ontology reference|

#### PropertyValue - DOI

If a [schema.org/PropertyValue](https://schema.org/PropertyValue) object represents a [DOI](https://www.doi.org/) identifier of an article, it is supposed to have the following exact values:

| Property | Required | Required Value | Description |
|----------|----------|---------------|-------------|
|name|MUST|'DOI'||
|value|SHOULD|-|The DOI without the 'https://www.doi.org' prefix|
|propertyID|MUST|'http://purl.obolibrary.org/obo/OBI_0002110'|Ontology term describing a DOI|

#### PropertyValue - PubMedID

If a [schema.org/PropertyValue](https://schema.org/PropertyValue) object represents a [PubMedID](https://pubmed.ncbi.nlm.nih.gov/) identifier of an article, it is supposed to have the following exact values:

| Property | Required | Required Value | Description |
|----------|----------|---------------|-------------|
|name|MUST|'PubMedID'||
|value|SHOULD|-|The PubMedID|
|propertyID|MUST|'http://purl.obolibrary.org/obo/OBI_0001617'|Ontology term describing a PubMedID|

## Example ro-crate-metadata.json

_TODO: simple example and a link to a more complete example_
