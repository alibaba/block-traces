# Alibaba Block Traces

These traces are published by Alibaba Group to help researchers understand the real-world workload in the cloud.

They are collected from a cluster in production of the olastic block service of Alibaba Cloud (i.e. storage for virtual disks).  The cluster is located in Beijing region, one of the most popular regions of Alibaba Cloud.

There are 1000 virtual disks randomly sampled from that cluster, and all their I/O activities are recorded over the month of January 2020.  These virtual disks are *ultra disk* products.  Ultra disks are backed by a storage cluster and offer high data reliability.  Ultra disks are cheaper and offer lower random I/O performance, compared to standard SSD and enhanced SSD disks [link](https://www.alibabacloud.com/help/doc-detail/25383.htm).  Typical applications of ultra disks are running operating systems, big data processing software, web servers, etc..

## Download

The data are available for download from Alibaba OSS.  You will get the download link after taking a short [survey](https://yida.alibaba-inc.com/o/alibaba_block_traces_2020_survey).  If you have any questions or ideas about the trace data, feel free to contact us.  The current maintainer is Chao Shi \<chao.shi AT alibaba-inc.com\>.  We are happy to see research work based on the trace data.

Just a kind reminder, the tarball is very large, 181GB gzip-compressed and 751GB uncompressed, so make sure you have enough space on your disk.

Here are MD5 checksums of the tarball and files inside.

Filename                           | MD5 checksum
-----------------------------------|---------------
`alibaba_block_traces_2020.tar.gz` | `95780fc531a60fd4ca0513ef88ef469c`
`io_traces.csv`                    | `c60dd8f771738d4d8df56271e56dd308`
`device_size.csv`                  | `6641abe8a0f3625f13776120d2884e84`

## Schema

There are two files in CSV format.  Their file format is defined as follow.

*io\_traces.csv*

Each row is a read or write operation.

Column     | Type    | Example          | Description
-----------|---------|------------------|-----------------------
device\_id | uint32  | 0                | ID of the virtual disk
opcode     | char    | R                | Either of 'R' or 'W', indicating this operation is read or write
offset     | uint64  | 126703644672     | Offset of this operation, in bytes
length     | uint32  | 4096             | Length of this operation, in bytes
timestmap  | uint64  | 1577808000000626 | Timestamp of this operation received by server, in microseconds

*device\_size.csv*

Each row is a device with is capacity.

Column     | Type   | Example         | Description
-----------|--------|-----------------|------------------------------------------
device\_id | uint32 | 0               | ID of the virtual disk
capacity   | uint64 | 536870912000    | Capacity of the virtual disk, in bytes

All IDs of virtual disks are re-mapped to the range of 0 - 999.

## Acknowledgements

Thanks to Qiuping Wang and Jinhong Li from the Chinese University of Hong Kong for analyzing and validating the data at an early stage.

## License

The trace data and document are licensed under [CC-4.0](https://creativecommons.org/licenses/by/4.0/).

