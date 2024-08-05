# Uploading/Downloading Files to 10x Genomics Cloud Using the CLI Method


[10x Genomics](https://www.10xgenomics.com/) is a leading biotech company that is commonly used for single-cell RNA-sequencing, single-cell spatial-sequencing, and single-cell ATAC-sequencing techniques. As part of their service, 10x Genomics also provides a [Cloud Analysis](https://www.10xgenomics.com/products/cloud-analysis) web portal, where users can upload sequencing data (e.g., Fastq files) and run [Cell Ranger](https://www.10xgenomics.com/support/software/cell-ranger/latest) analysis pipelines. The purpose of this guide is to provide a basic workflow for uploading/downloading files to the 10x Cloud using the command line interface (CLI) method on a Linux operating system. 

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Linux Installation

Link to the full guide on the 10x Genomics website is available [here](https://www.10xgenomics.com/support/software/cloud-analysis/latest/tutorials/CA-upload-via-cli-for-linux). 

First, download the 10x Genomics Cloud CLI for your operating system (Linux) and unpack it in an appropriate location. 
```
# Download the files
$ curl -f -o txg-linux-v1.3.1.tar.gz https://cf.10xgenomics.com/cloud-cli/v1.3.1/txg-linux-v1.3.1.tar.gz

# Unpack
$ tar -zxvf txg-linux-v1.3.1.tar.gz

```
+ [`curl`](https://curl.se/) is used in command lines or scripts to transfer data. Use `man curl` to view the available options.
  +   The `-f` or `--fail` option means that if the server returns an error, curl fails silently and returns error 22.
  +   The `-o` or `--output <file>` options means to store output in a file. The output is not shown in stdout.
+ [`tar`](https://www.tutorialspoint.com/linux-tar-command) is short for Tape Archive and is used to create and extract archive files. Use `man tar` to view the available options. 
  +   The `-z` option creates a tar file using gzip compression.
  +   The `-x` option extracts the archive file.
  +   The `-v` option prints verbose information for any tar operation on the terminal
  +   The `-f` option specifies the filename of the archive file.
 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Usage
#### Uploading Fastq Files: <br>
10x Genomics Cloud has an option to upload Fastq files to the server via the web browser. However, this can be very slow and unreliable as uploads may often be interrupted. A much more efficient option is to use the CLI method. To upload Fastq files into a project, simply copy and past the command provided in the project on the webpage (note that you will can to create a free account and start a project first). 
```
# Upload Fastq files to 10x Cloud for Cell Ranger analysis
$ ./txg fastqs upload --project-id [insert project id] [insert path to fastq files]
```
+ The `project-id` is a unique identifier that is automatically generated when a new project is created in the 10x Cloud portal.
+ The `[path to fastq files]` should reflect the path to the directory of the Fastq files to be uploaded.
<br>

<ins>A few notes: </ins>
+ The first time that you use the 10x Genomics Cloud CLI you will need to provide an access token, which can be found in Account Settings.
+ The Fastq files to be uploaded must follow the [Illumina naming convention](https://help.basespace.illumina.com/files-used-by-basespace/fastq-files), such as `SampleName_S1_L001_R01_001.fastq.gz`.
+ The CLI will only upload Fastq files to the project, even if there are other files types present in the provided directory. 
+ Files can be stored on the 10x Genomics Cloud server for up to 90 days free of charge, but extra storage after that point requires monthly payment. 
<br>

#### Downloading Analysis Files: <br>
+ Once the Cell Ranager analysis pipeline has completed, there are 11 different files that may be downloaded. While this can be done one at a time via the browser, a faster and more efficient method is to use the CLI method again. 
+ First, go to the analysis page that contains all of the output files, select the output files to be downloaded, and then select the Download with CLI button. A `txg` command will appear in a dialog box that can be copied and pasted into the terminal.
  + Include the optional `--target-dir` option if the desired output directory is in a different location than the current working directory.
+ Note: Only a limited about of data can be downloaded before 10x Genomics requires payment (there should be enough data to download all the output files at least once). 

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------


