# VMware_on_Raspberry 

Make Home Lab with RaspberryPi and Vmware

 Hardware:

 - Raspberry Pi 4 / 4GB 
 - 32 GB Pendrive
 - 64 GB Pendrive

# Downloads

- raspberry installer: https://www.raspberrypi.com/software/
- VMWare Installer, registry here ( free). (ISO ESXi Arm)Edition: https://flings.vmware.com/esxi-arm-edition
- (WINDOWS) Rufus: https://rufus.ie/hu/
- Latest Raspberry Pi Firmware: https://github.com/raspberrypi/firmware
- UEFI Raspberry Pi Firmware latest: https://github.com/pftf/RPi4/releases

# Update FW of Raspberry

- Install raspberry installer: 
- plug in Rasp SD Card
- Install Rasp lite version
- plug in SD card Raspberry, plug keyboard, plug monitor 
- admin: pi pass: raspberry
   
      sudo rpi-eeprom-update -a
      sudo reboot

- plug out SD Card

# Litle trick boot

 - plug in SD Card card on the card reader
 - use raspberry installer select erase
 - Unpack: Latest Raspberry Pi Firmware
 - Unpack: UEFI Raspberry Pi Firmware latest
 - Open Latest Raspberry Pi Firmware "boot" folder, copy all files from here
 - Open SD Card and paste 
 - Delete 4 kernel...img files
 - Open UEFI Raspberry Pi Firmware latest folder, copy all files from here
 - Open SD Card and paste, repleace all files
 - Open here "config.txt" and write this " gpu_mem=16 " , save
 - plug back The Sd Card in Rasp

 # ISO copy the pen

  - use Rufus
  - use 32 GB Pen drive
  - use ISO ESXi Arm
  - Fat32 / Cluster 32 kb

  # Setup Rasp bios   

  - plug in Rasp 32 GB usb
  - power on and spamming ESC
  - Device manager / Raspberry pi configuration / Limit ram disable / F10 Save, Y /
  - esc, esc, esc , continue,
  - reboot and spaming ESC
  - boot manager , select pendrive
  - ESC, and fast SHIFT + O

  # Install VMWare on to Rasp

  - Console here, tpye: " runweasel cdromBOOT  autoPartitionOSDateSize=8192 "
  - Accept License
  - Select a Disk..., plug in 64 GB Pendrive, F5 Refresh
  - Selecg new Pendrive and enter install
  - Select country, and give password with special char
  - F11 Install
  - Complet install,
  - reboot and spamming ESC
  - Boot Maintenance Manager / Boot Options / Change Boot Order
  - Enter and + + + very Top my pendrive
  - ESC ESC ESC , contiue
  - BOOT ESXi
# Connect VMware

- Check boot screen DHCP HTTPS IP adress
- Open my windows firefox browser use ip.
- This site add the security exception
- use admin: root pass: same instaling progress gived pass


# Testing

- download ubuntu server / ARM lite version:
https://ubuntu.com/download/server/arm

- create virtual machnie whit Ubuntu iso

# Connect USB hdd:

- Open SSH Consol
- Use Root Pass

      etc/init.d/usbarbitrator stop
      chkconfig usbarbitrator off

if you use Dell or Other server

    partedUtil mklabel /dev/disks/mpx.vmhba33:C0:xxxxxx
    
Calculate end sector:
   
    eval expr $(partedUtil getptbl /dev/disks/mpx.vmhba33:C0:xxxxx | tail -1 | awk '{print $1 " \\* " $2 " \\* " $3}') - 1
    partedUtil setptbl /dev/disks/mpx.vmhba33:C0:xxxxxx gpt "1 2048 1953455804 AA31E02A400F11DB9590000C2911D1B8 0"
    vmkfstools -C vmfs6 -S USB-Datastore_1TB /dev/disks/mpx.vmhba33:C0xxxx:1

- Back to VM control check Storage/Devices
- Select USB devices from list
- Action/Clear partition table
- New datastore
- Datastore name: " Virtual_lab_01_HDD_1GB"
- FullDisk / Finish


And continue 

# Vcenter

Later

https://www.vmware.com/products/vcenter-server.html

