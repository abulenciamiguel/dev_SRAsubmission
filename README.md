# Submitting sequences to SRA
> [!NOTE]
> Ask the Project ID

## Prepare fastq files
Fastq files that will be submitted can be found in the `fastq_pass` directory.

### 1. Decompress `fastq.gz` files
> [!IMPORTANT]
> The `FAU03107` in the `FAU03107_pass_barcode03_6bbd8ba6_0.fastq` is the Flowcell ID. This will be used later.
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
[!NOTE]
To determine which sample a particular barcode belongs to, use the `Flowcell ID` and `barcode number` in the `redcap_RITM.csv`.