# Linux Mint 20.03


## Git
``` bash
sudo apt-get install git
git clone https://github.com/ToddJMullen/SystemSetup.git && cd SystemSetup/
mkdir newOs && cd $_
```

## Geogebra

``` bash
sudo apt-add-repository 'deb http://www.geogebra.net/linux/ stable main'
sudo apt install geogebra-classic
```

Software catalog: Font Manager

``` bash
sudo apt-get install font-manager #(this is just a guess)
```

## Graphics Tablet

``` bash
$ sudo dpkg --remove --force-remove-reinstreq digimend-dkms
```

## Setup Java
https://www.debugpoint.com/2020/04/install-latest-java-14-in-ubuntu-18-04-20-04-linux-mint/
*
https://www.itzgeek.com/post/how-to-install-java-on-ubuntu-20-04/

``` bash
$ sudo update-alternatives --config java

$ xed /etc/profile.d/jdk.sh
$ . /etc/profile.d/jdk.sh
 ```



## ThinkOrSwim

**Note** The problem is not that it is not Oracle Java or that it is not the latest Java, ToS requires Java *8* to run / while running.

```bash
sudo apt install openjdk-8-jdk
sudo update-alternatives --config java
```

Create script to first redirect java versions for the session & then launch ToS

```bash
xed tos.sh

#!/bin/sh

export PATH=/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/:$PATH
exec /home/todd/thinkorswim/thinkorswim "$@"
```

## BAMS - Battery Applet w/Monitoring & Shutdown
[Cinnamon Spices - BAMS](https://cinnamon-spices.linuxmint.com/applets/view/255)
``` bash
$ sudo apt-get install zenity sox libsox-fmt-mp3
```

## Tiled
## Ghostwriter
## Gimp
## Inkscape
## Krita
## Umbrello
## Modelio
## Fonts / Font Manager
## Opera
## Chromium
## Dropbox
## Ionic
## Android Studio
## JDK
## Node
## NG CLI
## Netbeans
## VS Code
