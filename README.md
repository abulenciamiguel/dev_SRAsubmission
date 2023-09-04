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
Refer to `redcap_RITM.csv`

The following columns are to be filled out. </br>
*sample_name
bioproject_accession
*organism
*collected_by
*collection_date
*geo_loc_name
*host
*host_disease
*isolate
*isolation_source


| Headers | Example |
| ------- | ------- |
| *sample_name | PH-RITM-3839-2022 |
| bioproject_accession | PRJNA942069 |
| *organism | Severe acute respiratory syndrome coronavirus 2 |
| *collected_by | Oriental Mindoro Provincial Hospital |
| *collection_date | 12/26/2022 |
| *geo_loc_name | Philippines |
| *host | Homo sapiens |
| *host_disease | COVID-19 |
| *isolate | hCoV-19/Philippines/PH-RITM-3839/2022 |
| *isolation_source | oropharyngeal/nasopharyngeal swab| 