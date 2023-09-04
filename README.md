# Submitting sequences to SRA
> [!NOTE]
Ask the Project ID

## Prepare fastq files
Fastq files that will be submitted can be found in the `fastq_pass` directory.

### 1. Decompress `fastq.gz` files
> [!IMPORTANT]
The `FAU03107` in the `FAU03107_pass_barcode03_6bbd8ba6_0.fastq` is the Flowcell ID. This will be used later.
```
cd fastq_pass

gunzip */*.gz
```


### 2. List all directories into a file

```
ls -d */ | grep "barcode" | sed 's/\///g' > list.txt
```

### 3. Compress the individual `barcode` directories
```
while read barcode
do

tar -zcvf ${barcode}.tar.gz ${barcode}

done < list.txt
```


## Prepare metadata for Biosamples
A sample template `SARS-CoV-2.cl.1.0.xlsx` is provided. Refer to `redcap_RITM.csv`

The following column headers are to be filled out. </br>

| Headers | Example | Remarks |
| ------- | ------- | ------- |
| *sample_name | PH-RITM-3839-2022 | Column `gisaid_name` of `SARS-CoV-2.cl.1.0.xlsx` added with `-year`; unique for each sample |
| bioproject_accession | PRJNA42069 | Same for all samples |
| *organism | `Severe acute respiratory syndrome coronavirus 2` | Fill out as is |
| *collected_by | Oriental Mindoro Provincial Hospital | Column `originating_lab` of `SARS-CoV-2.cl.1.0.xlsx` |
| *collection_date | 12/26/2022 | Column `date_collected` of `SARS-CoV-2.cl.1.0.xlsx` |
| *geo_loc_name | `Philippines` | Fill out as is |
| *host | `Homo sapiens` | Fill out as is |
| *host_disease | `COVID-19` | Fill out as is |
| *isolate | hCoV-19/Philippines/PH-RITM-3839/2022 | Follow the pattern: `hCoV-19/Philippines`/`gisaid_name`/`year` |
| *isolation_source | oropharyngeal/nasopharyngeal swab | Column `sample_type_collected` of `SARS-CoV-2.cl.1.0.xlsx`: 0 = `serum`; 1 = `oropharyngeal/nasopharyngeal swab`; 2 = `other` |


## Prepare metadata for fastq files
A sample template `SRA_metadata_acc.xlsx` is provided.

>[!NOTE]
To determine which sample a particular barcode belongs to, use the `Flowcell ID` and `barcode number` in the `redcap_RITM.csv`.

The following column headers are to be filled out. </br>

| Headers | Example | Remarks |
| ------- | ------- | ------- |
| biosample_accession | SAMN420420420 | This will be provided by `SRA` after submitting the metadata of Biosamples |
| library_ID | PH-RITM-3839-2022 | This is the `*sample_name` in the metadata of Biosamples |
| title | ONT sequencing of SARS-CoV-2: PH-RITM-1387-2022 | Follow the pattern: `ONT sequencing of SARS-CoV-2: ``*sample_name` |
| library_strategy | `WGS` | Fill out as is |
| library_source | `VIRAL RNA` | Fill out as is |
| library_selection | `PCR` | Fill out as is |
| library_layout | `single` | Fill out as is |
| platform | `OXFORD_NANOPORE` | Fill out as is |
| instrument_model | GridION | Verify if it's `GridION` or `MinION`
| design_description | `Whole genome tiled amplicon; artic primer v4.1; ncov2019-artic-nf, artic 1.2.1, minimap2 2.17, nanopolish 0.13.2` | Fill out as is |
| filetype | `fastq` | Fill out as is |
| filename | barcode30.tar.gz | The corresponding barcode file |
