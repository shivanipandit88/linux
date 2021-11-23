# Division of Work:
 

## Shivani Pandit : (Email : shivani.pandit@sjsu.edu , Student ID: 015925273)

Build and install new kernel version:  
Fork the Git repo torvalds/linux to my own account  
git clone https://github.com/shivanipandit88/linux.git to clone it locally into linux and cd into the new directory  
uname -a : give the current running linux version   
`cp /boot/config-5.13.0-21-generic .config` to copy the current boot config locally  
`sudo apt install gcc bison flex libssl-dev` to install the necessary prerequisites for installing the kernel  
`sudo apt install make`  
make oldconfig to copy the current boot config into the new one (kept the enter key pressed as per the Professor’s suggestion to get default new values)  
make prepare  
`scripts/config --set-str SYSTEM_TRUSTED_KEYS ""` By default, the make config was trying to sign the kernel modules with a Canonical private key, which obviously I don't have.   The fix was to manually set this  
`scripts/config --disable SYSTEM_REVOCATION_KEYS` - to disable the revocation keys  
`sudo apt install dwarves` to fix the error -  
BTF: .tmp_vmlinux.btf: pahole (pahole) is not available  
Failed to generate BTF for vmlinux  
Try to disable CONFIG_DEBUG_INFO_BTF  
make: *** [Makefile:1106: vmlinux] Error 1  
`make -j 4 modules` to build all the new kernel modules  
`make -j 4` to build the new kernel  
`sudo make INSTALL_MOD_STRIP=1 modules_install` to install the modules  
`sudo make install` to install the kernel  
I faced an issue when configuring the kernel as I was working on the VM installed in my windows (as windows doesn’t have a boot menu there were issues with the config files) so I loaded the Linux OS from Dual Boot mode.   


## Chirag Rajpal : (Email : chiragbiharilal.rajpal@sjsu.edu , Student ID : 015951585 )

Build and run the module that queries processor capabilities: (Wrote code for the Primary VM Based Controls and Secondary VM Based Controls by referring to Professor's boilerplate code and SDM modules.)  
Create `CMPE-283` directory inside linux directory and copy the Makefile and cmpe283-1.c file provided by the Professor  
Append the licence information at the end of cmpe283-1.c  
make to build the kernel  
`sudo insmod cmpe283-1.ko` to install the module  
`sudo rmmod cmpe283-1` to remove the module  
`sudo sysctl kernel.dmesg_restrict=0`  
dmesg to obtain the output for printk lines  


## Output:
```
[  280.089997]   CMPE 283 Assignment 1 Module Start
[  280.090003]   Pinbased Controls MSR: 0x0
[  280.090005]   External Interrupt Exiting: Can set=No, Can clear=Yes
[  280.090006]   NMI Exiting: Can set=No, Can clear=Yes
[  280.090007]   Virtual NMIs: Can set=No, Can clear=Yes
[  280.090008]   Activate VMX Preemption Timer: Can set=No, Can clear=Yes
[  280.090009]   Process Posted Interrupts: Can set=No, Can clear=Yes
[  280.090011]   Entry Controls MSR: 0x0
[  280.090012]   Load Debug Controls: Can set=No, Can clear=Yes
[  280.090013]   IA-32e mode guest: Can set=No, Can clear=Yes
[  280.090013]   Entry to SMM: Can set=No, Can clear=Yes
[  280.090014]   Deactivate dual-monitor treatment: Can set=No, Can clear=Yes
[  280.090015]   Load IA32_PERF_GLOBAL_CTRL: Can set=No, Can clear=Yes
[  280.090016]   Load IA32_PAT: Can set=No, Can clear=Yes
[  280.090017]   Load IA32_EFER: Can set=No, Can clear=Yes
[  280.090017]   Load IA32_BNDCFGS: Can set=No, Can clear=Yes
[  280.090018]   Conceal VMX from PT: Can set=No, Can clear=Yes
[  280.090019]   Load IA32_RTIT_CTL: Can set=No, Can clear=Yes
[  280.090020]   Load CET state: Can set=No, Can clear=Yes
[  280.090021]   Load PKRS: Can set=No, Can clear=Yes
[  280.090023]   Exit Controls MSR: 0x0
[  280.090031]   Save debug controls: Can set=No, Can clear=Yes
[  280.090032]   Host address-space size: Can set=No, Can clear=Yes
[  280.090033]   Load IA32_PERF_GLOBAL_CTRL: Can set=No, Can clear=Yes
[  280.090034]   Acknowledge interrupt on exit: Can set=No, Can clear=Yes
[  280.090035]   Save IA32_PAT: Can set=No, Can clear=Yes
[  280.090050]   Load IA32_PAT: Can set=No, Can clear=Yes
[  280.090050]   Save IA32_EFER: Can set=No, Can clear=Yes
[  280.090051]   Load IA32_EFER: Can set=No, Can clear=Yes
[  280.090051]   Save VMX-preemption timer value: Can set=No, Can clear=Yes
[  280.090052]   Clear IA32_BNDCFGS: Can set=No, Can clear=Yes
[  280.090052]   Conceal VMX from PT: Can set=No, Can clear=Yes
[  280.090053]   Clear IA32_RTIT_CTL: Can set=No, Can clear=Yes
[  280.090053]   Load CET state: Can set=No, Can clear=Yes
[  280.090055]   Primary Processor based Controls MSR: 0x0
[  280.090056]   Interrupt-window exiting: Can set=No, Can clear=Yes
[  280.090056]   Use TSC offsetting: Can set=No, Can clear=Yes
[  280.090057]   HLT exiting: Can set=No, Can clear=Yes
[  280.090057]   INVLPG exiting: Can set=No, Can clear=Yes
[  280.090058]   MWAIT exiting: Can set=No, Can clear=Yes
[  280.090058]   RDPMC exiting: Can set=No, Can clear=Yes
[  280.090059]   RDTSC exiting: Can set=No, Can clear=Yes
[  280.090059]   CR-3-load exiting: Can set=No, Can clear=Yes
[  280.090060]   CR-3-store exiting: Can set=No, Can clear=Yes
[  280.090060]   CR8-load exiting: Can set=No, Can clear=Yes
[  280.090061]   CR8-store exiting: Can set=No, Can clear=Yes
[  280.090061]   Use TPR shadow: Can set=No, Can clear=Yes
[  280.090062]   NMI-window exiting: Can set=No, Can clear=Yes
[  280.090062]   MOV-DR exiting: Can set=No, Can clear=Yes
[  280.090063]   Unconditional I/O exiting: Can set=No, Can clear=Yes
[  280.090063]   Use I/O bitmaps: Can set=No, Can clear=Yes
[  280.090064]   Monitor trap flag: Can set=No, Can clear=Yes
[  280.090064]   Use MSR bitmaps: Can set=No, Can clear=Yes
[  280.090065]   MONITOR exiting: Can set=No, Can clear=Yes
[  280.090065]   PAUSE exiting: Can set=No, Can clear=Yes
[  280.090066]   Activate secondary controls: Can set=No, Can clear=Yes
[  280.090067]   Secondary Processor based Controls MSR: 0x0
[  280.090068]   Virtualize APIC accesses: Can set=No, Can clear=Yes
[  280.090068]   Enable EPT: Can set=No, Can clear=Yes
[  280.090069]   Descriptor-table exiting: Can set=No, Can clear=Yes
[  280.090069]   Enable RDTSCP: Can set=No, Can clear=Yes
[  280.090070]   Virtualize x2APIC mode: Can set=No, Can clear=Yes
[  280.090071]   Enable VPID: Can set=No, Can clear=Yes
[  280.090071]   WBINVD exiting: Can set=No, Can clear=Yes
[  280.090072]   Unrestricted guest: Can set=No, Can clear=Yes
[  280.090072]   APIC-register virtualization: Can set=No, Can clear=Yes
[  280.090073]   Virtual-interrupt delivery: Can set=No, Can clear=Yes
[  280.090073]   PAUSE-loop exiting: Can set=No, Can clear=Yes
[  280.090074]   RDRAND exiting: Can set=No, Can clear=Yes
[  280.090074]   Enable INVPCID: Can set=No, Can clear=Yes
[  280.090075]   Enable VM functions: Can set=No, Can clear=Yes
[  280.090075]   VMCS shadowing: Can set=No, Can clear=Yes
[  280.090076]   Enable ENCLS exiting: Can set=No, Can clear=Yes
[  280.090076]   RDSEED exiting: Can set=No, Can clear=Yes
[  280.090077]   Enable PML: Can set=No, Can clear=Yes
[  280.090077]   EPT-violation #VE: Can set=No, Can clear=Yes
[  280.090078]   Conceal VMX from PT: Can set=No, Can clear=Yes
[  280.090078]   Enable XSAVES/XRSTORS: Can set=No, Can clear=Yes
[  280.090079]   Mode-based execute control for EPT: Can set=No, Can clear=Yes
[  280.090079]   Sub-page write permissions for EPT: Can set=No, Can clear=Yes
[  280.090080]   Intel PT uses guest physical addresses: Can set=No, Can clear=Yes
[  280.090080]   Use TSC scaling: Can set=No, Can clear=Yes
[  280.090081]   Enable user wait and pause: Can set=No, Can clear=Yes
[  280.090081]   Enable ENCLV exiting: Can set=No, Can clear=Yes
[  282.200210]   CMPE 283 Assignment 1 Module Exits
```


## CMPE283 - Assignment 2

**Steps Followed to Complete the Assignment:** 
Step1: Identify the functions which are responsible for handling VM Exits. 
To identify the "vm_handle_exit" from vmx.c and "kvm_emulate_cpuid" as the two target functions.
vmx.c contains all potential exits as well as their respective exit handling functions. The "vm handle exit" function is called whenever a VM exit occurs. This function is in charge of delegating exit handling to one of the handler functions indicated in the map. The function to be tested for the assignment is "kvm emulate cpuid," which may be found in cpuid.c. A particular treatment of the leaf function "0x4FFFFFFF" is required.

Step2: There were problems in setting up the inner VM. I had the Ubuntu host properly configured for assignment1. According to my understanding, I needed to deploy a VM on the host in order to test the VM exits.

Step3: Another issue faced was that I tried to construct the "cpuid" module instead of the "kvm" module.

STEPS TO EMULATE ASSIGNMENT FUNCTIONALITY:

To clone the github repository in local directory.
Execute ```cd linux```
We need to run the following commands to load the modules:
```
rmmod kvm-intel;
rmmod kvm;
make M=arch/x86/kvm modules;
insmod arch/x86/kvm/kvm.ko;
insmod arch/x86/kvm/kvm-intel.ko;
```

Once the modules are loaded, we need to start the inner Virtual Machine using **qemu**. In order to do so, we run the following command: 
```qemu-system-x86_64 -m 2048 -drive file=ubuntu.qcow,format=qcow2 -enable-kvm -smp 2,sockets=1,cores=1,threads=2 -d cpu_reset -no-fd=bootchk```
The above command assumes that you have already created a disk with ubuntu installed before booting the machine.
Once the inner VM starts, one can run the custom program or execute the instruction ```cpuid -l 0x4FFFFFFF```.
This command will be responsible to invoke the particular leaf function.

Following scripts have been modified along with the comments in the code to emulate the functionality as required for the assignment:
```
https://github.com/shivanipandit88/linux/blob/master/arch/x86/kvm/vmx/vmx.c
https://github.com/shivanipandit88/linux/blob/master/arch/x86/kvm/cpuid.c
```

## Comments on Exits Observed:

An arbitrary number of exits based on the time after VM boot which executes the cpuid instruction in the inner VM.
These exits seem stable on executing cpuid multiple times. Number of exits as well as processing time increases linearly on repeated execution of the same exit instruction.
Roughly 10698558 exits were observed on the full VM boot with a processing time of 10407133758.

Linux kernel
============

There are several guides for kernel developers and users. These guides can
be rendered in a number of formats, like HTML and PDF. Please read
Documentation/admin-guide/README.rst first.

In order to build the documentation, use ```make htmldocs``` or ```make pdfdocs```.  The formatted documentation can also be read online at:

    https://www.kernel.org/doc/html/latest/

There are various text files in the Documentation/ subdirectory,
several of them using the Restructured Text markup notation.

Please read the Documentation/process/changes.rst file, as it contains the
requirements for building and running the kernel, and information about
the problems which may result by upgrading your kernel.
