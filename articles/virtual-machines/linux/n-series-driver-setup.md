---
title: setup voor het stuurprogramma voor Linux aaaAzure N-serie | Microsoft Docs
description: Hoe tooset NVIDIA GPU-stuurprogramma's voor N-reeks virtuele machines waarop Linux wordt uitgevoerd in Azure
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d91695d0-64b9-4e6b-84bd-18401eaecdde
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7db1b3859f9075c6d9f0319f39418946ea08743f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a>NVIDIA GPU-stuurprogramma's installeren op N-reeks virtuele machines waarop Linux wordt uitgevoerd

tootake profiteren van Hallo GPU-mogelijkheden van Azure N-reeks virtuele machines waarop Linux wordt uitgevoerd, installatie ondersteund NVIDIA grafische stuurprogramma's. Dit artikel bevat de installatiestappen stuurprogramma nadat u een VM N-serie implementeren. Stuurprogramma-installatie-informatie is ook beschikbaar voor [VM's van Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


Zie voor N-serie VM specificaties opslagcapaciteit en details van de schijf, [GPU Linux VM-grootten](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a>RASTER stuurprogramma's voor virtuele machines NV installeren

tooinstall NVIDIA RASTER stuurprogramma's op virtuele machines NV, een SSH-verbinding tooeach VM maken en volg de stappen Hallo voor uw Linux-distributie. 

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

1. Voer Hallo `lspci` opdracht. Controleer of Hallo NVIDIA M60 kaart of kaarten zichtbaar als PCI-apparaten zijn.

2. Updates installeren.

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. Hallo Nouveau kernelstuurprogramma dat niet compatibel met de Hallo NVIDIA stuurprogramma is uitschakelen. (Alleen gebruiken Hallo NVIDIA stuurprogramma op virtuele machines NV.) toodo dit, maakt u een bestand in `/etc/modprobe.d `met de naam `nouveau.conf` Hello volgende inhoud:

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. Hallo VM starten en opnieuw verbinding. Exit X-server:

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. Download en installeer Hallo RASTER stuurprogramma:

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. Wanneer u wordt gevraagd of u wilt dat toorun Hallo nvidia xconfig hulpprogramma tooupdate uw configuratiebestand X, selecteert u **Ja**.

7. Nadat de installatie is voltooid, kopieert u /etc/nvidia/gridd.conf.template tooa nieuwe bestand gridd.conf op locatie/etc/nvidia /

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. Hallo te volgende toevoegen`/etc/nvidia/gridd.conf`:
 
  ```
  IgnoreSP=TRUE
  ```
9. Hallo VM Start en tooverify Hallo installatie doorgaan.


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>Op basis van centOS 7.3 of Red Hat Enterprise Linux 7.3


1. Hallo kernel en DKMS bijwerken.
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. Hallo Nouveau kernelstuurprogramma dat niet compatibel met de Hallo NVIDIA stuurprogramma is uitschakelen. (Alleen gebruiken Hallo NVIDIA stuurprogramma op virtuele machines NV.) toodo dit, maakt u een bestand in `/etc/modprobe.d `met de naam `nouveau.conf` Hello volgende inhoud:

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. Hallo VM opnieuw opstarten, opnieuw verbinding maken en te installeren Hallo nieuwste Linux-integratieservices voor Hyper-V:
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. Toohello VM opnieuw en Voer Hallo `lspci` opdracht. Controleer of Hallo NVIDIA M60 kaart of kaarten zichtbaar als PCI-apparaten zijn.
 
5. Download en installeer Hallo RASTER stuurprogramma:

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. Wanneer u wordt gevraagd of u wilt dat toorun Hallo nvidia xconfig hulpprogramma tooupdate uw configuratiebestand X, selecteert u **Ja**.

7. Nadat de installatie is voltooid, kopieert u /etc/nvidia/gridd.conf.template tooa nieuwe bestand gridd.conf op locatie/etc/nvidia /
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. Hallo te volgende toevoegen`/etc/nvidia/gridd.conf`:
 
  ```
  IgnoreSP=TRUE
  ```
9. Hallo VM Start en tooverify Hallo installatie doorgaan.

### <a name="verify-driver-installation"></a>Controleer of de installatie van stuurprogramma


tooquery Hallo GPU Apparaatstatus, SSH toohello VM en Voer Hallo [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) opdrachtregelprogramma met Hallo stuurprogramma geïnstalleerd. 

De vergelijkbare toohello volgende uitvoer wordt weergegeven:

![De apparaatstatus NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a>X11 server
Als u een X11 moet server voor externe verbindingen tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) wordt aanbevolen, omdat hiermee hardwareversnelling van afbeeldingen. Hallo BusID Hallo M60 apparaat moet handmatig worden toegevoegd toohello xconfig-bestand (`etc/X11/xorg.conf` op Ubuntu 16.04 TNS, `/etc/X11/XF86config` op CentOS 7.3 of Red Hat Enterprise Server 7.3). Voeg een `"Device"` vergelijkbare toohello volgende sectie:
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
Daarnaast uw `"Screen"` sectie toouse dit apparaat.
 
Hallo BusID kunt u vinden door te voeren

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
Hallo BusID kunt wijzigen als een virtuele machine opgehaald opnieuw toegewezen of opnieuw opgestart. Daarom kunt u een script tooupdate hello BusID in Hallo X11 configuratie toouse wanneer een virtuele machine opnieuw is opgestart. Bijvoorbeeld:

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed too${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

Dit bestand kan worden aangeroepen als basis voor opgestart door het maken van een vermelding voor het in `/etc/rc.d/rc3.d`.


## <a name="install-cuda-drivers-for-nc-vms"></a>Voor virtuele machines NC CUDA stuurprogramma's installeren

Hier vindt u stappen tooinstall NVIDIA-stuurprogramma's op virtuele machines van Linux NC van Hallo NVIDIA CUDA Toolkit 8.0. 

C en C++-ontwikkelaars kunnen desgewenst Hallo volledige Toolkit toobuild GPU-versnelde toepassingen installeren. Zie voor meer informatie, Hallo [CUDA installatiehandleiding](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).


> [!NOTE]
> CUDA stuurprogramma downloadkoppelingen opgegeven op het moment van publicatie hier actueel zijn. Voor Hallo nieuwste CUDA stuurprogramma's, gaat u naar Hallo [NVIDIA](http://www.nvidia.com/) website.
>

tooinstall CUDA Toolkit, moet een SSH-verbinding tooeach VM. tooverify die Hallo systeem heeft een CUDA-compatibele GPU, Hallo volgende opdracht uitvoeren:

```bash
lspci | grep -i NVIDIA
```
Hier ziet u uitvoer vergelijkbare toohello voorbeeld (met een kaart NVIDIA Tesla R80) te volgen:

![opdrachtuitvoer lspci](./media/n-series-driver-setup/lspci.png)

Vervolgens uitvoeren installatieopdrachten die specifiek is voor uw distributiepunt.

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

1. Download en installeer Hallo CUDA stuurprogramma's.
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  Hallo-installatie kan enkele minuten duren.

2. toooptionally installatie Hallo voltooid CUDA toolkit, type:

  ```bash
  sudo apt-get install cuda
  ```

3. Hallo VM Start en tooverify Hallo installatie doorgaan.

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>Op basis van centOS 7.3 of Red Hat Enterprise Linux 7.3

1. Updates downloaden. 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. Toohello VM opnieuw aan en installeer Hallo nieuwste Linux-integratieservices voor Hyper-V.

  > [!IMPORTANT]
  > Als u een installatiekopie op basis van CentOS HPC geïnstalleerd op een NC24r VM, slaat u tooStep 3. Omdat Azure RDMA-stuurprogramma's en Linux-integratieservices zijn geïnstalleerd in Hallo-installatiekopie, LIS moet niet worden bijgewerkt en kernel-updates zijn standaard uitgeschakeld.
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. Opnieuw verbinding maken toohello VM en doorgaan met installatie Hello volgende opdrachten:

  ```bash
  sudo yum install kernel-devel

  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

  sudo yum install dkms

  CUDA_REPO_PKG=cuda-repo-rhel7-8.0.61-1.x86_64.rpm

  wget http://developer.download.nvidia.com/compute/cuda/repos/rhel7/x86_64/${CUDA_REPO_PKG} -O /tmp/${CUDA_REPO_PKG}

  sudo rpm -ivh /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo yum install cuda-drivers
  ```

  Hallo-installatie kan enkele minuten duren. 

4. toooptionally installatie Hallo voltooid CUDA toolkit, type:

  ```bash
  sudo yum install cuda
  ```

5. Hallo VM Start en tooverify Hallo installatie doorgaan.


### <a name="verify-driver-installation"></a>Controleer of de installatie van stuurprogramma


tooquery Hallo GPU Apparaatstatus, SSH toohello VM en Voer Hallo [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) opdrachtregelprogramma met Hallo stuurprogramma geïnstalleerd. 

De vergelijkbare toohello volgende uitvoer wordt weergegeven:

![De apparaatstatus NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a>Updates voor stuurprogramma's CUDA

We bevelen aan dat u regelmatig CUDA stuurprogramma's na de implementatie.

#### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>Op basis van centOS 7.3 of Red Hat Enterprise Linux 7.3

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a>Problemen oplossen

* Er is een bekend probleem met stuurprogramma's voor CUDA op N-reeks virtuele machines in Azure Hallo 4.4.0-75 Linux kernel op Ubuntu 16.04 TNS uitgevoerd. Als u een upgrade vanaf een eerdere kernelversie uitvoert upgraden tooat minimaal kernel versie 4.4.0-77. 



## <a name="next-steps"></a>Volgende stappen

* Zie voor meer informatie over Hallo NVIDIA GPU's op Hallo N-reeks virtuele machines:
    * [NVIDIA Tesla R80](http://www.nvidia.com/object/tesla-k80.html) (voor NC Azure VM's)
    * [NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (voor NV Azure VM's)

* Zie toocapture een Linux VM-installatiekopie met de geïnstalleerde stuurprogramma's NVIDIA [hoe toogeneralize en een virtuele Linux-machine vastleggen](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
