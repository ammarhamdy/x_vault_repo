

## `dd` command:
+ The `dd` command is a utility for copying files or entire partitions at the bit level.
```
dd [OPTIONS] OPERAND
```
+ This command has several useful features, including:
	- It can be used to clone or delete (wipe) entire disks or partitions.
	- It can be used to copy raw data to removable devices, such as USB drives and CDROMs.
	- It can backup and restore the MBR (Master Boot Record).
	- It can be used to create a file of a specific size that is filled with binary zeros, which can then be used as a swap file (virtual memory).


## Let's examine the following example: 
+ The `dd` command creates a file named `/tmp/swapex` with 50 blocks of zeros that are one megabyte in size:
```sh
dd if=/dev/zero of=/tmp/swapex bs=1M count=50
```
+ The `dd` command uses special arguments to specify how it will work. 
+ The following illustrates some of the more commonly used arguments:

| Argument | Description                                                                                                                                                                                                                                                                                                                                                   |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `if`     | Input File: The input file to be read from.<br><br>```<br>dd if=/dev/zero of=/tmp/swapex bs=1M count=50 <br>```<br><br>The example reads from the `/dev/zero`file, a special file containing an unlimited number of zeros.                                                                                                                                    |
| `of`     | Output File: The output file to be written.<br><br>```<br>dd if=/dev/zero of=/tmp/swapex bs=1M count=50<br>```                                                                                                                                                                                                                                                |
| `bs`     | Block Size: The block size to be used. By default, the value is considered to be in bytes. Use the following suffixes to specify other units: `K`, `M`, `G`, and `T` for kilobytes, megabytes, gigabytes and terabytes respectively.<br><br>```<br>dd if=/dev/zero of=/tmp/swapex bs=1M count=50<br>```<br><br>The example uses a block size of one megabyte. |
| `count`  | Count: The number of blocks to be read from the input file.<br><br>```<br>dd if=/dev/zero of=/tmp/swapex bs=1M count=50<br>```<br><br>The example command reads 50 blocks.                                                                                                                                                                                    |


## Clone one disk to another:
+ No block size or count needs to be specified when copying over entire devices.
+ For example, to clone from one hard drive (`/dev/sda`) to another (`/dev/sdb`) execute the following command: