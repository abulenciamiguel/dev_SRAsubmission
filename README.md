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

The following column headers are to be filled out. </br>

| Headers | Example | Remarks |
| ------- | ------- | ------- |
| *sample_name | PH-RITM-3839-2022 | asdasd |
| bioproject_accession | PRJNA942069 | asdasd |
| *organism | Severe acute respiratory syndrome coronavirus 2 | asdasd |
| *collected_by | Oriental Mindoro Provincial Hospital | asdasd |
| *collection_date | 12/26/2022 | asdasd |
| *geo_loc_name | Philippines | asdasd |
| *host | Homo sapiens | asdasd |
| *host_disease | COVID-19 | asdasd |
| *isolate | hCoV-19/Philippines/PH-RITM-3839/2022 | asdasd |
| *isolation_source | oropharyngeal/nasopharyngeal swab | asdasd |