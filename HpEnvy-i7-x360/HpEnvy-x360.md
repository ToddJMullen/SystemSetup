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

### Remove unmovable files

1. [x] Disable hibernate
   1. Open Admin command prompt
   2. `> powercfg /h off`
2. [x] Disable page file
   1. Super (Windows) > "Advanced System Settings" > (Performance) Settings > Advanced (tab) > Virtual Memory (Change)
    (uncheck) Automatically manage paging filesize > "No Paging File" > Set > (Yes to warning) > Ok > Ok 
3. [x] Disable system restore
    "Advanced System Settings" > "System Protection" (tab) > "Configure" > "Disable System Protection" > (Yes to warning)
4. [x] Restart (They should be gone)
5. [] 

Refs: [Super User ](https://superuser.com/questions/1017764/how-can-i-shrink-a-windows-10-partition)
[Other Article](https://www.download3k.com/articles/How-to-shrink-a-disk-volume-beyond-the-point-where-any-unmovable-files-are-located-00432)

### Shrink Volume

1. [x] Super (Windows) + X > Disk Management > Right Click System Volume > Type number of Mb to shrink the volume
    The right boundary of the volume will be shifted left that amount & leave that space unallocated on the right.

### Windows System Repair

This may not be needed usually. I have done the same steps on my previous Acer without problems, but After shrinking the volume, there were frequent crashed of Firefox & Opera, "Out of memory" errors, & random screen freezing or blanking.
Thinking that they might have config flags that pointed to disk locations that were no longer valid, I tried reinstalling both, but it did not fix the problem.  I found & tried the following commands run 
with admin privileges:
`sfc /scannow`
followed by
`Dism /Online /Cleanup-Image /RestoreHealth`

Ref: [Microsoft Forum](https://answers.microsoft.com/en-us/windows/forum/windows_10-update/system-file-check-sfc-scan-and-repair-system-files/bc609315-da1f-4775-812c-695b60477a93)

This *seemed* to work for a while, but the system is still very crashy when trying to browser 'normally' (Opera + Firefox ~45 tabs together).

Symptoms: Tabs keep crashing, browsers keep crashing, video display goes black and fails to correct. Generally when the video goes black, closing the lid until it goes to sleep & opening it back up is the only way I've been able to 'recover' the display (holding the power button ~45s did not even do *anything* -- including not shutting it off).  Even then, the display is corrupted as I am typing this the lock screen & desktop are scrambled together.


### Addendum

I had added more notes on trying to recover Windows, but did not push the changes.  While playing with the installing options for POP OS, 
I kept getting warnings about the partition asking me if I wanted to repair it. I ignored it multiple times as I played with options, but at some point I thought perhaps that would repair the problem with the random crashes in Windows and I agreed to let it 'repair' the partition. 
I have not been able to log back into Windows since.  I attempted to repair or recover Windows numberous ways,
but Windows kept complaining that it couldn't start.  I did/do not have the restore disk with me as I went traveling spontaneously some time back.
I decided to complete the installation and continue as is. I will try to recover it again when I get back home.


# Pop OS - Post Install

### Customizations

#### Turn on minimize/maximize
1 Install GNOME Tweaks from Pop Store  
    Tweaks > Windows Titlebars > (enable Minimize & Maximize)




### Applications

**Pop Shop**
- GNOME Tweaks
- VS Code
- Tiled 
- Wireshark
- Umbrello
- Manuskript
- Telegram Desktop
- Krita
- Inkscape
- Gimp
- Meld

**External**
- Opera [Opera](https://www.opera.com/download)
- ThinkOrSwim [ThinkOrSwim]()
- Unreal Engine
    1 [Create an Epic Account](https://www.unrealengine.com)
    1 Confirm Email
    1 [Add Github Connection](https://www.unrealengine.com/account/connections)
    1 Accept Invitation from [Epic Game on Github](https://github.com/EpicGames)
    1 cd to where we want the source code & clone it (will require authentication to execute)
    `git clone https://github.com/EpicGames/UnrealEngine.git`
    1 Once cloning is complete README.md says to run
    `./Setup.sh`
    1 When that is complete:  `./GenerateProjectFiles.sh`
    1 If Setup completes with a "Success" message, then the needed requirements have been downloaded & other build requirements have been created.
    To compile Unreal Engine:  
    `make -f Makefile`
    Note: Instructions recommend a 'powerful' system to build with an estimated build time of 10m to 1h.
    I am not sure if their estimate was for a first build or a rebuild, but this system has 8Gb & 10th Gen i7 & took ~2.5h to build. 
    Compilation instructions can be found in Engine/Build/BatchFiles/Linux/README.md & the [UnrealEngine Forum](https://www.ue4community.wiki/Legacy/Building_On_Linux)  
    1 Run:  
    `bash
    > cd Engine/Binaries/Linux/
    > ./UE4Engine
    `

When trying to run it shows many 'building shaders' and finally crashes with:  
`Engine crash handling finished; re-raising signal 11 for the default handler. Good bye.`
Much further up I also noted these lines:  
`bash
[2021.01.02-01.24.04:741][  2]LogShaderCompilers: Display: Worker (3/5): shaders left to compile 3953
INTEL-MESA: error: ../src/intel/vulkan/anv_device.c:3263: GPU hung on one of our command buffers (VK_ERROR_DEVICE_LOST)
[2021.01.02-01.24.05:514][  2]LogVulkanRHI: Error: VulkanRHI::vkQueueSubmit(Queue, 1, &SubmitInfo, Fence->GetHandle()) failed, VkResult=-4
 at /home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanQueue.cpp:71 
 with error VK_ERROR_DEVICE_LOST
Fatal error: [File:/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanUtil.cpp] [Line: 803] 
VulkanRHI::vkQueueSubmit(Queue, 1, &SubmitInfo, Fence->GetHandle()) failed, VkResult=-4
 at /home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanQueue.cpp:71 
 with error VK_ERROR_DEVICE_LOST
Signal 11 caught.
Malloc Size=65538 LargeMemoryPoolOffset=65554 
CommonUnixCrashHandler: Signal=11
[2021.01.02-01.24.05:617][  2]LogCore: === Critical error: ===
Unhandled Exception: SIGSEGV: invalid attempt to write memory at address 0x0000000000000003

[2021.01.02-01.24.05:617][  2]LogCore: Fatal error: [File:/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanUtil.cpp] [Line: 803] 
VulkanRHI::vkQueueSubmit(Queue, 1, &SubmitInfo, Fence->GetHandle()) failed, VkResult=-4
 at /home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanQueue.cpp:71 
 with error VK_ERROR_DEVICE_LOST

`
A recommended fix I found for a similar looking error requires a dist upgrad, so I am adding this note & pushing these changes before continuing.  
`apt-add-repository ppa:oibaf/graphics-drivers && apt-get update && apt-get dist-upgrade`
https://stackoverflow.com/questions/43405720/unreal-engine-crashes-on-startup-on-linux
See also: https://ue4community.wiki/legacy/building-on-linux-qr8t0si2 
and https://ue4community.wiki/legacy/running-on-linux-4r2hfjw7

There is no noticable difference. Reading through more documentation, I noted that I may not meet all the minimum requirements:  
`
Quad-core Intel or AMD processor, 2.5 GHz or faster
NVIDIA GeForce 470 GTX or AMD Radeon 6870 HD series card or higher
8 GB RAM
`
So, to figure out if I do, I see:  
`About > Processor > Intel® Core™ i7-10510U CPU @ 1.80GHz × 8 ` I am not sure if this is sufficient processor since it is less GHz, but more cores.
Graphics card:  
`About > Graphics > Mesa Intel® UHD Graphics (CML GT2)`
`lspci | grep VGA` outputs `00:02.0 VGA compatible controller: Intel Corporation UHD Graphics (rev 02)` so this looks to fail.
Using `sudo lshw -C video` I get
`*-display
    description: VGA compatible controller
    product: UHD Graphics
    vendor: Intel Corporation
    physical id: 2
    bus info: pci@0000:00:02.0
    version: 02
    width: 64 bits
    clock: 33MHz
    capabilities: pciexpress msi pm vga_controller bus_master cap_list rom
    configuration: driver=i915 latency=0
    resources: irq:147 memory:b0000000-b0ffffff memory:a0000000-afffffff ioport:3000(size=64) memory:c0000-dffff.
`
Which give more detail, but still no mention of NVIDIA or AMD, so that is not likely sufficient either.  
However, I will continue trying to see if it will work, since I didn't see any mention of it in the courses I bought.

I installed in `~/Dev/UnrealEngine` and the log files are located at `~/Dev/UnrealEngine/Engine/Saved/Logs/`



Refs: [Linux Quick Start](https://docs.unrealengine.com/en-US/SharingAndReleasing/Linux/BeginnerLinuxDeveloper/SettingUpAnUnrealWorkflow/index.html)



- Komodo IDE
 [Komodo IDE](https://www.activestate.com/products/komodo-ide/downloads/edit/)
 I haven't used this before, but it was mentioned in a course, so I thought I'd see if they supported Linux & try it out.


### Wireshark Permission Denied Error

Trying to run after installation gives a "Couldn’t run /usr/bin/dumpcap in child process: Permission denied" error because I (the user) 
does not have permission to record the network.  
Temp fix:
`bash
> sudo wireskark
`

Permanent fix:
`bash
> sudo usermod -a -G wireshark $USER
`
Ref:
(Tech Overflow)[https://techoverflow.net/2019/06/10/how-to-fix-wireshark-couldnt-run-usr-bin-dumpcap-in-child-process-permission-denied-on-linux/]


Noted that WIreshark does not show the min, max, close buttons. This 'fix' *may* be related to 
the missing buttons here or in VS Code.


### Fix Opera Video
(Note: not working yet)

Refs: 
- (Opera Forums)[https://forums.opera.com/topic/27463/bug-html5-h-264-codec-videos-no-longer-working-on-opera-54-0-2952-41-ubuntu-18-04-lts-x86_64-xfce/7]
- (SE H264 Support for Opera)[https://unix.stackexchange.com/questions/384015/h-264-support-for-opera-and-opensuse]
- 



### ThinkOrSwim

`bash
> \# Enable Universe to install Open JDK. Note: Universe includes all Community-Maintained, Open-Source Software
> sudo add-apt-repository universe
> sudo apt-get update
> sudo apt install openjdk-8-jdk
> cd ~/Downloads
> sudo chmod +x thinkorswim_installer.sh
> ./thinkorswim_installer.sh
`
Notes:  
No JRE/JDK was present in Pop OS, so unlike my previous systems, there was no need to switch / manage other versions or create desktop
links to alter PATH before starting ToS.
However, on the following day I installed some other applications and at some point Java 11 got installed by something else. 
Or, possibly more likely as a security upgrade. So I will need to tell the OS to use Java 8 just before launching.

`bash
> java -version
> update-alternatives --list java
> sudo update-alternatives --config java
\# select desired version 
> java -version \# to confirm
`

**Setup Alias Shortcut to open ThinkOrSwim**  
`bash
> \# .bashrc already includes a check for .bash_aliases, so I'll add it for parsing when .bashrc is read.
> echo "alias tos="~/thinkorswim/thinkorswim" > ~/.bash_aliases
> . ~/.bashrc \# Reload .bashrc
> tos \# Test it out
`


Refs:
- (Running ToS on Mint 19)[https://unix.stackexchange.com/questions/545041/running-thinkorswim-on-linux-mint-19]



## Aside: Problems Noted

### Noted Before ~12/20/20  
VS Code no longer opens to the full screen, nor shows the min, max, close buttons on the window (only 90% sure it did originally). 
I have to use the Super key / overview to close the application.  I will try to uninstall / reinstall to see if that fixes it.  
Restart on 12/27/20 did *not* fix it, so I will try to reinstall it now.  
After reinstalling, the application seems to open fullscreen now although the problem may resurface again with use.
There are still no min, max, close buttons though.

### Noted Before ~12/24/20  
Pop Shop will no longer open. From the menu it simply shows that it is working, then stop after some time.
Using the CLI to try & launch also fails, but returns `Failed to register: Timeout was reached`
Restarted on 12/27/20 and have been able to to open & repoen it multiple times. (I had read previously where other people could
not open it after the first time.) 



### Make CLI remember last tabs & auto re-open on restart





#### Aside ToS IV Rank Script

`
declare lower;
declare hide_on_intraday; 
input days_back = 252;
def df = if (GetSymbol() == "/ES") then close("VIX") / 100
else if (GetSymbol() == "/CL") then close("OIV") / 100
else if (GetSymbol() == "/GC") then close("GVX") / 100
else if (GetSymbol() == "/SI") then close("VXSLV") / 100
else if (GetSymbol() == "/NQ") then close("VXN") / 100
else if (GetSymbol() == "/TF") then close("RVX") / 100
else if (GetSymbol() == "/YM") then close("VXD") / 100
else if (GetSymbol() == "/6E") then close("EVZ") / 100
else if (GetSymbol() == "/ZN") then close("VXTYN") / 100
else imp_volatility();
def df1 = if !IsNaN(df) then df else df[-1];
def low_over_timespan = Lowest(df1, days_back);
def high_over_timespan = Highest(df1, days_back);
def iv_rank = Round( (df1 -low_over_timespan) / (high_over_timespan -low_over_timespan) * 100.0, 0);
plot IVRank = iv_rank;
IVRank.SetDefaultColor(Color.GREEN);
AddLabel(yes, "IV Rank: " + iv_rank + " (IV in comparison to its yearly high and low IV)", Color.GREEN);
def counts_below = fold i = 1 to days_back + 1 with count = 0
do if df1[0] > df1[i] then count + 1 else count;
def iv_percentile = Round(counts_below / days_back * 100.0, 0);
plot IVPercentile = iv_percentile;
IVPercentile.SetDefaultColor(Color.YELLOW);
AddLabel(yes, "IV Percentile: " + iv_percentile + 
" (" + iv_percentile + "% of days or "
 + counts_below + " days out of " + days_back + " days were below the current IV)", Color.YELLOW);
`









