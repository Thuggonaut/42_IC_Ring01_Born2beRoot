# 🖥️ 42_IC_Ring01_Born2beRoot
## Preface:
   - This is a guide to the Born2beRoot project, and it was written using resources from several other guides, therefore the credit is to them.
   - The purpose of re-writing this updated guide is to edit some errors that I've come across using some of the guides, and to help prevent issues that I've had to troubleshoot.
   - Debian is the chosen Operating System for this project.
   - The Mandatory part of the subject.pdf involves using the Guided Partitioning Method of the Debian installation. The Bonus part of the subject.pdf involves using the Manual Partitioning Method. This guide has instructions for the Manual Partitioning Method, which I recommend you do from the start, thus passing you both the Mandatory part, and 1/3 of the Bonus part of Born2beRoot. 

## 🔷 Outline of Steps:
   - Step 1: Download the Debian installer for your Virtual Machine (VM)
   - Step 2: Installing your VM
   - Step 3: Setting up your VM partitions
   - Step 4: Starting & setting up your VM
   - Step 5: Connecting to SSH
   - Step 6: Configuring your VM - Password Policy
   - Step 7: Creating Groups & Users
   - Step 8: Configuring your VM - User Priviledges
   - Step 9: Configuring your VM - Script Monitoring & Crontab
   - Step 10: Evaluation Checklist & Testing
   - Step 11: Retrieve the Signature of your machine’s virtual disk
   - Step 12: Evaluation Questions & Answers

## 🔷 Step 1: Download the Debian installer for your Virtual Machine (VM)

### 🔸 1.1: Debian
1. [Click here to download Debian GNU/Linux](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/)
2. Scroll to the bottom of the page and select `debian-mac-xx.x.x-amd64-netinst.iso`

### 🔸 1.2: VM Directory (For 42Adelaide Students)
1. In iTerm2:
    - `cd sgoinfre/students`
    - `mkdir <your_intra_usename>`
    - `chmod 700 <your_intra_usename>`
2. Find your Debian download file from Step 1.1 and put that download in this `sgoinfre/students/<your_intra_usename>` directory that you have just created (_in iTerm2,_ `open .` _to open/find the directory, and drag/drop your Debian download file in there_). 

### 🔸 1.3: Virtual Box
1. Open the Virtual Box application

## 🔷 Step 2: Installing your VM
1. Select `New`

2. Name and operating system:
    - Name: e.g. `Born2beRoot`
    - Machine Folder: `/sgoinfre/students/<your_intra_usename>` (_Do not type this in, use the drop down option._)
    - Type: `Linux `
    - Version: `Debian (64-bit)`
    - `Continue`

3. Memory Size:
    - `1024`MB
    - `Continue`

4. Hard disk:
    - Select `Create a Virtual Hard Disk Now`
    - `Create`

5. Hard disk file type:
    - Select `VDI (VirtualBox Disk Image)`
    - `Continue`

6. Storage on physical hard disk:
    - Select `Dyamically Allocated`
    - `Continue`

7. File location and size:
    - `12.00`GB
    - `Create`

8. VM Storage:
    - Go to `Settings`
    - Select `Storage`
    - Find "Optical Drive" under "Attributes" & click on the drop down menu. Select `Choose a disk file...`
    - Select the Debian Download file (.iso) from your `/sgoinfre/students/<your_intra_usename>` directory. 
    - `Open`
    - `Ok`

## 🔷 Step 3: Setting up your VM partitions
1. Go to `Start` (_The green arrow_)
    Note: you will only be able to use your Keyboard to operate your Virtual Machine.
    Note: to increase the size of your VM window, go to the menu bar and either:
    - Select `Scaled Mode (Host+C)` then, with your mouse drag the VM window.
    - Select `Virtual Screen 1` then, select `Scale to 200% (autoscaled output)`

2. Select `Install` (_Do not select "Graphical install"_).

3. Select a language: `English`

4. Select your location: `Australia`

5. Configure the keyboard: `American English`

6. Configure the network:
    - Hostname: `<your_intra_username42>` (_ensure "42" is at the end_)
    - Domain name: leave blank

7. Set up users and passwords:
    - Root password: it is reccomended you use the same passwords for all passwords. Write it down should you forget it. 
    - Full name for the new user: personally, I used `<your_intra_username>` without the "42". 
    - Username for your account: `<your_intra_username>` without the "42". 
    - Choose a password for the new user: use the same password as "Root password".

8. Partition disks:
   
   🔸
    - Select `Manual`
    - Select `SCSI1 (0,0,0) (sda) 8.6 GB ATA VBOX HARDDISK`
    - Create new empty partition table on this device?: `Yes`
    - Select `pri/log 8.6 GB FREE SPACE`
    - How to use this free space: `Create a new partition`
    - New partition size: `500M`
    - Type for the new partition: `Primary`
    - Location for the new partition: `Beginning`
    - Partition settings: `Mount point:     /`
    - Mount point for this partition: `/boot - static files of the boot loader`
    - Partition settings: `Done setting up the partition`
    
   🔸
    - Select `pri/log 8.6 GB FREE SPACE`
    - How to use this free space: `Create a new partition`
    - New partition size: `max`
    - Type for the new partition: `Logical`
    - Partition settings: `Mount point:     /`
    - Mount point for this partition: `Do not mount it`
    - Partition settings: `Done setting up the partition`
    
   🔸
    - Select `Configure encrypted volumes`
    - Write changes to disk and configure encrypted volumes?: `Yes`
    - Encryption configuration actions: `Create encrypted volumes`
    - Devices to encrypt: using <Space bar> to select/de-select, ensure that: 
        - `[ ] /dev/sda1` is de-selected
        - `[*] /dev/sda5` is selected 
    - Select `Done setting up the partitions`
    - Encryption configuration actions: `Finish`
    - Really erase the data on SCSI1 (0,0,0), partition #5 (sda)?: `Yes`
    - Encryption passphrase: Personally, I used the same password set previously, x2, to avoid forgetting it.

   🔸
    - Select `Configure the Logical Volume Manager`
    - Write the changes to disks and configure LVM?: `Yes`
    - LVM configuration action: `Create volume group`
    - Volume group name: `LVMGroup`
    - Devices for th new volume group:
        - `[*] /dev/mapper/sda5_crypt` is selected
        - `[ ] /dev/sda1` is de-selected
    
   🔸
    - LVM configuration action: `Create logical volume`
    - Volume group: `LVMGroup`
    - Logical volume name: `root`
    - Logical volume size: `2G`
    
   🔸
    - LVM configuration action: `Create logical volume`
    - Volume group: `LVMGroup`
    - Logical volume name: `swap`
    - Logical volume size: `1024MB`
    
   🔸
    - LVM configuration action: `Create logical volume`
    - Volume group: `LVMGroup`
    - Logical volume name: `home`
    - Logical volume size: `1G`
    
   🔸
    - LVM configuration action: `Create logical volume`
    - Volume group: `LVMGroup`
    - Logical volume name: `var`
    - Logical volume size: `1G`
    
   🔸
    - LVM configuration action: `Create logical volume`
    - Volume group: `LVMGroup`
    - Logical volume name: `srv`
    - Logical volume size: `1G`
    
   🔸
    - LVM configuration action: `Create logical volume`
    - Volume group: `LVMGroup`
    - Logical volume name: `tmp`
    - Logical volume size: `1G`
    
   🔸
    - LVM configuration action: `Create logical volume`
    - Volume group: `LVMGroup`
    - Logical volume name: `var-log` (_yes, type only one '-' which will be automatically updated to '--'_)
    - Logical volume size: `1056MB`
    - LVM configuration action: `Finish`
    
   🔸
    - Under the line with "LV home" in it, select `#1`
    - Partition settings: `Use as:    do not use`
    - How to use this partition: `Ext4 journaling file system`
    - Partition settings: `Mount point:   none`
    - Mount point for this partition: `/home - user home directories`
    - Partition settings: `Done setting up the partition`
   
   🔸
    - Under the line with "LV root" in it, select `#1`
    - Partition settings: `Use as:    do not use`
    - How to use this partition: `Ext4 journaling file system`
    - Partition settings: `Mount point:   none`
    - Mount point for this partition: `/ - the root file system`
    - Partition settings: `Done setting up the partition`

   🔸
    - Under the line with "LV srv" in it, select `#1`
    - Partition settings: `Use as:    do not use`
    - How to use this partition: `Ext4 journaling file system`
    - Partition settings: `Mount point:   none`
    - Mount point for this partition: `/srv - data for services provided by this system`
    - Partition settings: `Done setting up the partition`
   
   🔸
    - Under the line with "LV swap" in it, select `#1`
    - Partition settings: `Use as:    do not use`
    - How to use this partition: `swap area`
    - Partition settings: `Done setting up the partition`
   
   🔸
    - Under the line with "LV tmp" in it, select `#1`
    - Partition settings: `Use as:    do not use`
    - How to use this partition: `Ext4 journaling file system`
    - Partition settings: `Mount point:   none`
    - Mount point for this partition: `/tmp - temporary files`
    - Partition settings: `Done setting up the partition`
   
   🔸
    - Under the line with "LV var" in it, select `#1`
    - Partition settings: `Use as:    do not use`
    - How to use this partition: `Ext4 journaling file system`
    - Partition settings: `Mount point:   none`
    - Mount point for this partition: `/var - variable data`
    - Partition settings: `Done setting up the partition`

   🔸
    - Under the line with "LV var-log" in it, select `#1`
    - Partition settings: `Use as:    do not use`
    - How to use this partition: `Ext4 journaling file system`
    - Partition settings: `Mount point:   none`
    - Mount point for this partition: `Enter manually`
    - Mount point for this partition: `/var/log`
    - Partition settings: `Done setting up the partition`
    - At the end of the list, select `Finish partitioning and write changes to disk`
    - Write the changes to disk?: `Yes`
   
9. Confugure the package manager:
    - Scan another CD or DVD?: `No`
    - Debian archive mirror country: `Australia`
    - Debian archive mirror: `deb.debian.org`
    - HTTP proxy information (blank for none): leave blank

10. Software selection:
    - Choose software to install: ensure all items are de-selected

11. GRUB boot loader:
    - Install the GRUB boot loader to the master boot record?: `Yes`
