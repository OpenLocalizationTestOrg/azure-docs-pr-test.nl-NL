---
title: Azure N-reeks stuurprogramma-instellingen voor Linux | Microsoft Docs
description: Het instellen van NVIDIA GPU-stuurprogramma's voor N-reeks virtuele machines waarop Linux wordt uitgevoerd in Azure
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
ms.openlocfilehash: bdeb4d5ca1d9ff4d7dfd0961690412dd7530572a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a><span data-ttu-id="cbeba-103">NVIDIA GPU-stuurprogramma's installeren op N-reeks virtuele machines waarop Linux wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="cbeba-103">Install NVIDIA GPU drivers on N-series VMs running Linux</span></span>

<span data-ttu-id="cbeba-104">Als u wilt profiteren van de GPU-mogelijkheden van N-reeks virtuele machines in Azure waarop Linux wordt uitgevoerd, ondersteunde NVIDIA graphics-stuurprogramma's te installeren.</span><span class="sxs-lookup"><span data-stu-id="cbeba-104">To take advantage of the GPU capabilities of Azure N-series VMs running Linux, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="cbeba-105">Dit artikel bevat de installatiestappen stuurprogramma nadat u een VM N-serie implementeren.</span><span class="sxs-lookup"><span data-stu-id="cbeba-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="cbeba-106">Stuurprogramma-installatie-informatie is ook beschikbaar voor [VM's van Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cbeba-106">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


<span data-ttu-id="cbeba-107">Zie voor N-serie VM specificaties opslagcapaciteit en details van de schijf, [GPU Linux VM-grootten](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cbeba-107">For N-series VM specs, storage capacities, and disk details, see [GPU Linux VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a><span data-ttu-id="cbeba-108">RASTER stuurprogramma's voor virtuele machines NV installeren</span><span class="sxs-lookup"><span data-stu-id="cbeba-108">Install GRID drivers for NV VMs</span></span>

<span data-ttu-id="cbeba-109">NVIDIA RASTER stuurprogramma's installeren op virtuele machines NV, een SSH-verbinding maken met elke VM en volg de stappen voor uw Linux-distributie.</span><span class="sxs-lookup"><span data-stu-id="cbeba-109">To install NVIDIA GRID drivers on NV VMs, make an SSH connection to each VM and follow the steps for your Linux distribution.</span></span> 

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="cbeba-110">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="cbeba-110">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="cbeba-111">Voer de `lspci` opdracht.</span><span class="sxs-lookup"><span data-stu-id="cbeba-111">Run the `lspci` command.</span></span> <span data-ttu-id="cbeba-112">Controleer of de NVIDIA M60 kaart of kaarten zichtbaar als PCI-apparaten zijn.</span><span class="sxs-lookup"><span data-stu-id="cbeba-112">Verify that the NVIDIA M60 card or cards are visible as PCI devices.</span></span>

2. <span data-ttu-id="cbeba-113">Updates installeren.</span><span class="sxs-lookup"><span data-stu-id="cbeba-113">Install updates.</span></span>

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. <span data-ttu-id="cbeba-114">Het stuurprogramma van de kernel Nouveau, dat niet compatibel met het stuurprogramma NVIDIA is uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="cbeba-114">Disable the Nouveau kernel driver, which is incompatible with the NVIDIA driver.</span></span> <span data-ttu-id="cbeba-115">(Alleen NVIDIA stuurprogramma gebruiken op virtuele machines NV.) Om dit te doen, maakt u een bestand in `/etc/modprobe.d `met de naam `nouveau.conf` met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="cbeba-115">(Only use the NVIDIA driver on NV VMs.) To do this, create a file in `/etc/modprobe.d `named `nouveau.conf` with the following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. <span data-ttu-id="cbeba-116">Start de virtuele machine en opnieuw verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="cbeba-116">Reboot the VM and reconnect.</span></span> <span data-ttu-id="cbeba-117">Exit X-server:</span><span class="sxs-lookup"><span data-stu-id="cbeba-117">Exit X server:</span></span>

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. <span data-ttu-id="cbeba-118">Download en installeer het stuurprogramma RASTER:</span><span class="sxs-lookup"><span data-stu-id="cbeba-118">Download and install the GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. <span data-ttu-id="cbeba-119">Wanneer u wordt gevraagd of u wilt uitvoeren van het hulpprogramma nvidia xconfig selecteren om bij te werken uw configuratiebestand X **Ja**.</span><span class="sxs-lookup"><span data-stu-id="cbeba-119">When you're asked whether you want to run the nvidia-xconfig utility to update your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="cbeba-120">Nadat de installatie is voltooid, /etc/nvidia/gridd.conf.template naar een nieuw bestand gridd.conf op locatie/etc/nvidia/kopiëren</span><span class="sxs-lookup"><span data-stu-id="cbeba-120">After installation completes, copy /etc/nvidia/gridd.conf.template to a new file gridd.conf at location /etc/nvidia/</span></span>

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. <span data-ttu-id="cbeba-121">Het volgende toevoegen aan `/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="cbeba-121">Add the following to `/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="cbeba-122">Start de virtuele machine op en gaat u verder met de installatie verifiëren.</span><span class="sxs-lookup"><span data-stu-id="cbeba-122">Reboot the VM and proceed to verify the installation.</span></span>


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="cbeba-123">Op basis van centOS 7.3 of Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="cbeba-123">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>


1. <span data-ttu-id="cbeba-124">De kernel en DKMS bijwerken.</span><span class="sxs-lookup"><span data-stu-id="cbeba-124">Update the kernel and DKMS.</span></span>
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. <span data-ttu-id="cbeba-125">Het stuurprogramma van de kernel Nouveau, dat niet compatibel met het stuurprogramma NVIDIA is uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="cbeba-125">Disable the Nouveau kernel driver, which is incompatible with the NVIDIA driver.</span></span> <span data-ttu-id="cbeba-126">(Alleen NVIDIA stuurprogramma gebruiken op virtuele machines NV.) Om dit te doen, maakt u een bestand in `/etc/modprobe.d `met de naam `nouveau.conf` met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="cbeba-126">(Only use the NVIDIA driver on NV VMs.) To do this, create a file in `/etc/modprobe.d `named `nouveau.conf` with the following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. <span data-ttu-id="cbeba-127">De virtuele machine opnieuw opstarten, opnieuw verbinding maken en installeer de meest recente Linux-integratieservices voor Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="cbeba-127">Reboot the VM, reconnect, and install the latest Linux Integration Services for Hyper-V:</span></span>
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. <span data-ttu-id="cbeba-128">Opnieuw verbinding maken met de virtuele machine en voer de `lspci` opdracht.</span><span class="sxs-lookup"><span data-stu-id="cbeba-128">Reconnect to the VM and run the `lspci` command.</span></span> <span data-ttu-id="cbeba-129">Controleer of de NVIDIA M60 kaart of kaarten zichtbaar als PCI-apparaten zijn.</span><span class="sxs-lookup"><span data-stu-id="cbeba-129">Verify that the NVIDIA M60 card or cards are visible as PCI devices.</span></span>
 
5. <span data-ttu-id="cbeba-130">Download en installeer het stuurprogramma RASTER:</span><span class="sxs-lookup"><span data-stu-id="cbeba-130">Download and install the GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. <span data-ttu-id="cbeba-131">Wanneer u wordt gevraagd of u wilt uitvoeren van het hulpprogramma nvidia xconfig selecteren om bij te werken uw configuratiebestand X **Ja**.</span><span class="sxs-lookup"><span data-stu-id="cbeba-131">When you're asked whether you want to run the nvidia-xconfig utility to update your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="cbeba-132">Nadat de installatie is voltooid, /etc/nvidia/gridd.conf.template naar een nieuw bestand gridd.conf op locatie/etc/nvidia/kopiëren</span><span class="sxs-lookup"><span data-stu-id="cbeba-132">After installation completes, copy /etc/nvidia/gridd.conf.template to a new file gridd.conf at location /etc/nvidia/</span></span>
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. <span data-ttu-id="cbeba-133">Het volgende toevoegen aan `/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="cbeba-133">Add the following to `/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="cbeba-134">Start de virtuele machine op en gaat u verder met de installatie verifiëren.</span><span class="sxs-lookup"><span data-stu-id="cbeba-134">Reboot the VM and proceed to verify the installation.</span></span>

### <a name="verify-driver-installation"></a><span data-ttu-id="cbeba-135">Controleer of de installatie van stuurprogramma</span><span class="sxs-lookup"><span data-stu-id="cbeba-135">Verify driver installation</span></span>


<span data-ttu-id="cbeba-136">Query uitvoeren op de apparaatstatus GPU SSH naar de virtuele machine en voer de [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) opdrachtregelprogramma met het stuurprogramma geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="cbeba-136">To query the GPU device state, SSH to the VM and run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span> 

<span data-ttu-id="cbeba-137">Vergelijkbaar met de volgende uitvoer wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="cbeba-137">Output similar to the following appears:</span></span>

![De apparaatstatus NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a><span data-ttu-id="cbeba-139">X11 server</span><span class="sxs-lookup"><span data-stu-id="cbeba-139">X11 server</span></span>
<span data-ttu-id="cbeba-140">Als u een X11 moet server voor externe verbindingen met een VM NV [x11vnc](http://www.karlrunge.com/x11vnc/) wordt aanbevolen, omdat hiermee hardwareversnelling van afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="cbeba-140">If you need an X11 server for remote connections to an NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) is recommended because it allows hardware acceleration of graphics.</span></span> <span data-ttu-id="cbeba-141">De BusID van het apparaat M60 moet handmatig worden toegevoegd aan het bestand xconfig (`etc/X11/xorg.conf` op Ubuntu 16.04 TNS, `/etc/X11/XF86config` op CentOS 7.3 of Red Hat Enterprise Server 7.3).</span><span class="sxs-lookup"><span data-stu-id="cbeba-141">The BusID of the M60 device must be manually added to the xconfig file (`etc/X11/xorg.conf` on Ubuntu 16.04 LTS, `/etc/X11/XF86config` on CentOS 7.3 or Red Hat Enterprise Server 7.3).</span></span> <span data-ttu-id="cbeba-142">Voeg een `"Device"` vergelijkbaar met de volgende sectie:</span><span class="sxs-lookup"><span data-stu-id="cbeba-142">Add a `"Device"` section similar to the following:</span></span>
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
<span data-ttu-id="cbeba-143">Daarnaast uw `"Screen"` sectie voor het gebruik van dit apparaat.</span><span class="sxs-lookup"><span data-stu-id="cbeba-143">Additionally, update your `"Screen"` section to use this device.</span></span>
 
<span data-ttu-id="cbeba-144">De BusID kunt u vinden door te voeren</span><span class="sxs-lookup"><span data-stu-id="cbeba-144">The BusID can be found by running</span></span>

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
<span data-ttu-id="cbeba-145">De BusID kunt wijzigen als een virtuele machine opgehaald opnieuw toegewezen of opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="cbeba-145">The BusID can change when a VM gets reallocated or rebooted.</span></span> <span data-ttu-id="cbeba-146">Daarom kunt u een script gebruiken om bij te werken de BusID in de X11 configuratie wanneer u een virtuele machine opnieuw is opgestart.</span><span class="sxs-lookup"><span data-stu-id="cbeba-146">Therefore, you may want to use a script to update the BusID in the X11 configuration when a VM is rebooted.</span></span> <span data-ttu-id="cbeba-147">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="cbeba-147">For example:</span></span>

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed to ${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

<span data-ttu-id="cbeba-148">Dit bestand kan worden aangeroepen als basis voor opgestart door het maken van een vermelding voor het in `/etc/rc.d/rc3.d`.</span><span class="sxs-lookup"><span data-stu-id="cbeba-148">This file can be invoked as root on boot by creating an entry for it in `/etc/rc.d/rc3.d`.</span></span>


## <a name="install-cuda-drivers-for-nc-vms"></a><span data-ttu-id="cbeba-149">Voor virtuele machines NC CUDA stuurprogramma's installeren</span><span class="sxs-lookup"><span data-stu-id="cbeba-149">Install CUDA drivers for NC VMs</span></span>

<span data-ttu-id="cbeba-150">Hier volgen de stappen NVIDIA-stuurprogramma's installeren op Linux NC virtuele machines van de NVIDIA CUDA Toolkit 8.0.</span><span class="sxs-lookup"><span data-stu-id="cbeba-150">Here are steps to install NVIDIA drivers on Linux NC VMs from the NVIDIA CUDA Toolkit 8.0.</span></span> 

<span data-ttu-id="cbeba-151">C en C++-ontwikkelaars kunnen desgewenst installeren voor de volledige Toolkit om GPU-versnelde toepassingen te bouwen.</span><span class="sxs-lookup"><span data-stu-id="cbeba-151">C and C++ developers can optionally install the full Toolkit to build GPU-accelerated applications.</span></span> <span data-ttu-id="cbeba-152">Zie voor meer informatie de [CUDA installatiehandleiding](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span><span class="sxs-lookup"><span data-stu-id="cbeba-152">For more information, see the [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span></span>


> [!NOTE]
> <span data-ttu-id="cbeba-153">CUDA stuurprogramma downloadkoppelingen opgegeven op het moment van publicatie hier actueel zijn.</span><span class="sxs-lookup"><span data-stu-id="cbeba-153">CUDA driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="cbeba-154">Voor de nieuwste stuurprogramma's CUDA gaat u naar de [NVIDIA](http://www.nvidia.com/) website.</span><span class="sxs-lookup"><span data-stu-id="cbeba-154">For the latest CUDA drivers, visit the [NVIDIA](http://www.nvidia.com/) website.</span></span>
>

<span data-ttu-id="cbeba-155">Zorg voor het installeren van CUDA Toolkit een SSH-verbinding naar elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="cbeba-155">To install CUDA Toolkit, make an SSH connection to each VM.</span></span> <span data-ttu-id="cbeba-156">Om te controleren of het systeem een GPU die compatibel is met CUDA heeft, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="cbeba-156">To verify that the system has a CUDA-capable GPU, run the following command:</span></span>

```bash
lspci | grep -i NVIDIA
```
<span data-ttu-id="cbeba-157">Hier ziet u uitvoer die vergelijkbaar is met het volgende voorbeeld (met een kaart NVIDIA Tesla R80):</span><span class="sxs-lookup"><span data-stu-id="cbeba-157">You will see output similar to the following example (showing an NVIDIA Tesla K80 card):</span></span>

![opdrachtuitvoer lspci](./media/n-series-driver-setup/lspci.png)

<span data-ttu-id="cbeba-159">Vervolgens uitvoeren installatieopdrachten die specifiek is voor uw distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="cbeba-159">Then run installation commands specific for your distribution.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="cbeba-160">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="cbeba-160">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="cbeba-161">Download en installeer de CUDA stuurprogramma's.</span><span class="sxs-lookup"><span data-stu-id="cbeba-161">Download and install the CUDA drivers.</span></span>
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  <span data-ttu-id="cbeba-162">De installatie kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="cbeba-162">The installation can take several minutes.</span></span>

2. <span data-ttu-id="cbeba-163">Wilt eventueel de volledige CUDA toolkit installeren, typt u:</span><span class="sxs-lookup"><span data-stu-id="cbeba-163">To optionally install the complete CUDA toolkit, type:</span></span>

  ```bash
  sudo apt-get install cuda
  ```

3. <span data-ttu-id="cbeba-164">Start de virtuele machine op en gaat u verder met de installatie verifiëren.</span><span class="sxs-lookup"><span data-stu-id="cbeba-164">Reboot the VM and proceed to verify the installation.</span></span>

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="cbeba-165">Op basis van centOS 7.3 of Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="cbeba-165">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

1. <span data-ttu-id="cbeba-166">Updates downloaden.</span><span class="sxs-lookup"><span data-stu-id="cbeba-166">Get updates.</span></span> 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. <span data-ttu-id="cbeba-167">Opnieuw verbinding maken met de virtuele machine en installeer de meest recente Linux-integratieservices voor Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="cbeba-167">Reconnect to the VM and install the latest Linux Integration Services for Hyper-V.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="cbeba-168">Als u een installatiekopie op basis van CentOS HPC geïnstalleerd op een NC24r VM, gaat u verder met stap 3.</span><span class="sxs-lookup"><span data-stu-id="cbeba-168">If you installed a CentOS-based HPC image on an NC24r VM, skip to Step 3.</span></span> <span data-ttu-id="cbeba-169">Omdat Azure RDMA-stuurprogramma's en Linux-integratieservices vooraf worden geïnstalleerd in de installatiekopie zijn, LIS moet niet worden bijgewerkt en kernel-updates zijn standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cbeba-169">Because Azure RDMA drivers and Linux Integration Services are pre-installed in the image, LIS should not be upgraded, and kernel updates are disabled by default.</span></span>
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. <span data-ttu-id="cbeba-170">Opnieuw verbinding maken met de virtuele machine en doorgaan met installatie met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="cbeba-170">Reconnect to the VM and continue installation with the following commands:</span></span>

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

  <span data-ttu-id="cbeba-171">De installatie kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="cbeba-171">The installation can take several minutes.</span></span> 

4. <span data-ttu-id="cbeba-172">Wilt eventueel de volledige CUDA toolkit installeren, typt u:</span><span class="sxs-lookup"><span data-stu-id="cbeba-172">To optionally install the complete CUDA toolkit, type:</span></span>

  ```bash
  sudo yum install cuda
  ```

5. <span data-ttu-id="cbeba-173">Start de virtuele machine op en gaat u verder met de installatie verifiëren.</span><span class="sxs-lookup"><span data-stu-id="cbeba-173">Reboot the VM and proceed to verify the installation.</span></span>


### <a name="verify-driver-installation"></a><span data-ttu-id="cbeba-174">Controleer of de installatie van stuurprogramma</span><span class="sxs-lookup"><span data-stu-id="cbeba-174">Verify driver installation</span></span>


<span data-ttu-id="cbeba-175">Query uitvoeren op de apparaatstatus GPU SSH naar de virtuele machine en voer de [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) opdrachtregelprogramma met het stuurprogramma geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="cbeba-175">To query the GPU device state, SSH to the VM and run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span> 

<span data-ttu-id="cbeba-176">Vergelijkbaar met de volgende uitvoer wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="cbeba-176">Output similar to the following appears:</span></span>

![De apparaatstatus NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a><span data-ttu-id="cbeba-178">Updates voor stuurprogramma's CUDA</span><span class="sxs-lookup"><span data-stu-id="cbeba-178">CUDA driver updates</span></span>

<span data-ttu-id="cbeba-179">We bevelen aan dat u regelmatig CUDA stuurprogramma's na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="cbeba-179">We recommend that you periodically update CUDA drivers after deployment.</span></span>

#### <a name="ubuntu-1604-lts"></a><span data-ttu-id="cbeba-180">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="cbeba-180">Ubuntu 16.04 LTS</span></span>

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="cbeba-181">Op basis van centOS 7.3 of Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="cbeba-181">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a><span data-ttu-id="cbeba-182">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="cbeba-182">Troubleshooting</span></span>

* <span data-ttu-id="cbeba-183">Er is een bekend probleem met stuurprogramma's voor CUDA op N-reeks virtuele machines in Azure die de 4.4.0-75 Linux kernel op Ubuntu 16.04 TNS worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cbeba-183">There is a known issue with CUDA drivers on Azure N-series VMs running the 4.4.0-75 Linux kernel on Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="cbeba-184">Als u een upgrade vanaf een eerdere kernelversie uitvoert, upgrade uit naar ten minste kernel versie 4.4.0-77.</span><span class="sxs-lookup"><span data-stu-id="cbeba-184">If you are upgrading from an earlier kernel version, upgrade to at least kernel version 4.4.0-77.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="cbeba-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cbeba-185">Next steps</span></span>

* <span data-ttu-id="cbeba-186">Zie voor meer informatie over de NVIDIA GPU's op de N-reeks virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="cbeba-186">For more information about the NVIDIA GPUs on the N-series VMs, see:</span></span>
    * <span data-ttu-id="cbeba-187">[NVIDIA Tesla R80](http://www.nvidia.com/object/tesla-k80.html) (voor NC Azure VM's)</span><span class="sxs-lookup"><span data-stu-id="cbeba-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="cbeba-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (voor NV Azure VM's)</span><span class="sxs-lookup"><span data-stu-id="cbeba-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="cbeba-189">Zie voor het vastleggen van een Linux VM-installatiekopie met de geïnstalleerde stuurprogramma's voor NVIDIA [generaliseren en Linux-machine vastleggen](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cbeba-189">To capture a Linux VM image with your installed NVIDIA drivers, see [How to generalize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
