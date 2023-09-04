# Submitting sequences to SRA
> [!NOTE]
> Verify the Project ID

## Prepare fastq files
Fastq files that will be submitted can be found in the `fastq_pass` directory.

### 1. Decompress `fastq_gz` files
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
