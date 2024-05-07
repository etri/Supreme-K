# XPU Device Driver for AB21-QEMU

The XPU device driver (AB21-XDD-QEMU) of this project is a SW, running on the Host system, developed by the Supercomputing Technology Research Center to execute the parallel operation kernel operation of the parallel application program written in the OpenCL programming model on the XPU device, which is an emulated operation accelerator based on QEMU. The main functions and features provided by AB21-XDD-QEMU are as follows.
 * XPU device registration/initialization/setting management
 * XPU device context management
 * Parallel operation queue management
 * Execution of parallel operation tasks
 * Event Management
 * XPU device memory allocation and management
## Overview
* This source code directory of AB21-XDD-QEMU includes 
	- XPU Driver Library (XDL)
	- XPU Hig-level Driver (XHD)
	- XPU Platform Driver (XPD)
	- Test program (XDL-test)
* To cross compile for AArch64 (AB21Q)
* Tested on x86_64 host.
* This is not fully debugged.
* AB21-XDD-QEMU can run on the AB21Q virtual machine. So, AB21Q needs to to build and installed before running AB21-XDD-QEMU.

## Directories
```
AB21-XDD-QEMU                                     --> XPU Device Driver (XDD) and XPU Platform Driver (XPD)
    ├── linux-source-5.4.0              --> Ubuntu kernel source
    └── xdlib                           --> XPU Driver Library (XDL) 
        └── test                        --> XDL-test application          
```
<br>
<br>

## Table of Contents
- [Environment & Prerequisites](#environment-and-prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Authors](#authors)

<br>

## Environment and Prerequisites

- Development languages:  Gcc 10.0.4 (ARM Cross compile)
- OS:  Ubuntu 20.04 (linux-5.4.0)
- QEMU 6.2.0

<br>


## Installation 

* Build ubuntu kernel

	- before kernel compile and build, you shoud download kernel source code (https://www.kernel.org)
```
$ cd AB21-XDD-QEMU/linux-5.4.0
$ cp ../u20_config .config 
$ make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j `nproc`
$ cd ..
```

* Build AB21-XDD-QEMU (in Supreme-K/AB21-XDD-QEMU)
```
$ cd AB21-XDD-QEMU
$ make all
$ ls
	xd.ko                             # driver module 
	xdlib/test/test                   # XDL-test program binary
	xdlib/test/axpu_kernel_binary     # OpenCL sample kernel binary which is used by XDL-test
```

## Install and run AB21Q
* Refer to https://git.etri.re.kr/parkym/supreme-k-poc/-/blob/master/ab21sim/ab21tsim/README.md
<br>


## Usage 

## How to run AB21-XDD-QEMU

* run AB21Q virtual machine image (in supreme-k-poc/ab21sim/ab21tsim/QEMU/qemu_test/test_ubuntu/)
	```
	$ cd ab21sim/ab21tsim/QEMU/qemu_test/test_ubuntu/
	$ source env.sh
	$ ./run_ubuntu_20.04_on_ab21q
	```
* in AB21Q virtual machine, copy XDD files from host 
	- use scp or sftp to your host in virtual machine
	- files to copy
		- AB21-XDD-QEMU/xd.ko
		- AB21-XDD-QEMU/xdlib/test/test
		- AB21-XDD-QEMU/xdlib/test/axpu_kernel_binary

* load AB21-XDD-QEMU module and execute XDL-test program
	```
	$ sudo insmod xd.ko
	$ ./test axpu_kernle_binary
	```
<br>
<br>

## Authors

* 김영호 &nbsp;&nbsp;&nbsp;  kyh05@etri.re.kr   
* 임은지 &nbsp;&nbsp;&nbsp;  ejlim@etri.re.kr   
* 안신영 &nbsp;&nbsp;&nbsp;  syahn@etri.re.kr   
<br>
<br>

## Version 
* AB21-XDD-QEMU 2.0.0 / 2022.12.15
<br>
<br>

