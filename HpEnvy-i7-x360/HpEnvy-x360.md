#  HP Envy x360 Convertible

The system was bought as clearance floor model at Sams Club, so additional steps may be added regarding changes to the store/user's config.

## Details
- Model: 15-dr1xxx (actual 15-dr1679cl)
- ProdID: 2E222UA#ABA
- CPU: i7-10510U @1.8GHz, 2304 Mhz, 4 Core, 8 Logical processors
- 8Gb RAM
- Input: 19.5V @3.33A
- Intel Radio Model AX201NGW
- UEFI


- [x] Install Git & Pull SystemSetup
- [x] Change admin account detail.
- [x] Turn off 'hide file extensions'
- [x] Turn on 'show full path in title bar'
- [x] Dump System Info into text file


## Create Restore Disk

Windows Menu > Type "Restore Disk" > Create Sytem Recovery Drive
It stated that the drive must be at least 16Gb, initial drive is 16Gb.


## Shrink Volume

To keep Windows alongside with Linux, but not waste hard disk space, the Win partition should be reduced.
Typically, windows will only suggest that it can be shrunk ~50% even on new systems.  This is due to
'unmovable' files that are in the 'middle' of the hard disk.  I believe they are put there strategically, but that's just
my feeling about it.  As I remember, the files are related to Hibernation, but once moved to an appropriate location,
then the Windows partition can be shrunk to the space actually being used.

### Move unmoved files

1. [x] Disable hibernate
   1. Open Admin command prompt
   2. `> powercfg /h off`
2. [] Disable page file
   1. Super (Windows) > "Advanced System Settings" > (Performance) Settings > Advanced (tab) > Virtual Memory (Change)
    (uncheck) Automatically manage paging filesize > "No Paging File" > Set > (Yes to warning) > Ok > Ok 
3. [] Disable system restore
    "Advanced System Settings" > "System Protection" (tab) > "Configure" > "Disable System Protection" > (Yes to warning)
4. [] Defrag
5. [] 

Refs: [Super User ](https://superuser.com/questions/1017764/how-can-i-shrink-a-windows-10-partition)
[Other Article](https://www.download3k.com/articles/How-to-shrink-a-disk-volume-beyond-the-point-where-any-unmovable-files-are-located-00432)



