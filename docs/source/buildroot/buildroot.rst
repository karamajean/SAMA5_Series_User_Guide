.. sama5 documentation master file, created by
   sphinx-quickstart on Thu Mar  3 16:46:51 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Buildroot
============================

Build from source
-----------

* 下載並安裝 [VMWARE Workstation Player](https://www.vmware.com/tw/products/workstation-player/workstation-player-evaluation.html).

* 下載  [Ubuntu 1804LTS 64位元桌面版本](https://www.ubuntu-tw.org/modules/tinyd0//)

* 安裝 Ubuntu, 空間建議開到 60G 

* 開機進 ubuntu系統後，進入終端機，先安裝必要的 套件 

.. highlight:: sh

::

   # sudo apt update
   # sudo apt install build-essential ccache ecj fastjar file g++ gawk \
   gettext git java-propose-classpath libelf-dev libncurses5-dev \
   libncursesw5-dev libssl-dev python python2.7-dev python3 unzip wget \
   python3-distutils python3-setuptools python3-dev rsync subversion \
   swig time xsltproc zlib1g-dev 
   # sudo apt-get install libssl1.0-dev

建一個資料夾 放 buildroot source code

.. highlight:: sh

::

   # mkdir git


下載  build-root & 切換Branch

.. highlight:: sh

::

   # git clone https://github.com/linux4sam/buildroot-external-microchip.git -b 2020.02-at91
   # git clone https://github.com/linux4sam/buildroot-at91.git -b 2020.02-at91


buildroot source build，第一次 build 過程大約需 3-4個小時 
SAMA5D27 WLSOM1 EK source build

.. highlight:: sh

::

   # git clone https://github.com/linux4sam/buildroot-external-microchip.git -b 2021.02-at91
   # git clone https://github.com/linux4sam/buildroot-at91.git -b 2021.02-at91
   # cd build-at91
   # make microchip_sama5d27_wlsom1_ek_mmc_dev_defconfig
   # BR2_EXTERNAL=../buildroot-external-microchip/ make sama5d27_wlsom1_ek_graphics_defconfig
   # make


SAMA5D27 SOM1 EK source build 

.. highlight:: sh

::

# cd build-at91
# make atmel_sama5d27_som1_ek_mmc_dev_defconfig
# BR2_EXTERNAL=../buildroot-external-microchip/ make sama5d27_som1_ek_graphics_defconfig
# make


SAM9X60 EK source build ,目前測 Demo image 2021.02 是ok 的，較舊的版本會出現 Bad magic 的錯誤

.. highlight:: sh

::

   # git clone https://github.com/linux4sam/buildroot-external-microchip.git -b 2021.02-at91
   # git clone https://github.com/linux4sam/buildroot-at91.git -b 2021.02-at91
   # make at91sam9260eknf_defconfig
   # BR2_EXTERNAL=../buildroot-external-microchip/ make sam9x60ek_graphics_defconfig
   # make


* build 成功後 image 會放在```buildroot-at91/output/images```底下

* 燒錄 image	燒錄檔 : sdcard.img ，用 Etcher 燒,   

* 參考 : https://www.linux4sam.org/bin/view/Linux4SAM/DemoSD

* 將 sdcard 放入板子的 sdcard 槽 後開機， 登入密碼  root 

* 準備 USB-TO-UART 線 連接到 板子的 Debug connector 