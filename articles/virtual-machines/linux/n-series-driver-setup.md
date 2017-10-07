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
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a><span data-ttu-id="b3e2e-103">NVIDIA GPU-stuurprogramma's installeren op N-reeks virtuele machines waarop Linux wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="b3e2e-103">Install NVIDIA GPU drivers on N-series VMs running Linux</span></span>

<span data-ttu-id="b3e2e-104">tootake profiteren van Hallo GPU-mogelijkheden van Azure N-reeks virtuele machines waarop Linux wordt uitgevoerd, installatie ondersteund NVIDIA grafische stuurprogramma's.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Linux, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="b3e2e-105">Dit artikel bevat de installatiestappen stuurprogramma nadat u een VM N-serie implementeren.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="b3e2e-106">Stuurprogramma-installatie-informatie is ook beschikbaar voor [VM's van Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b3e2e-106">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


<span data-ttu-id="b3e2e-107">Zie voor N-serie VM specificaties opslagcapaciteit en details van de schijf, [GPU Linux VM-grootten](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b3e2e-107">For N-series VM specs, storage capacities, and disk details, see [GPU Linux VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a><span data-ttu-id="b3e2e-108">RASTER stuurprogramma's voor virtuele machines NV installeren</span><span class="sxs-lookup"><span data-stu-id="b3e2e-108">Install GRID drivers for NV VMs</span></span>

<span data-ttu-id="b3e2e-109">tooinstall NVIDIA RASTER stuurprogramma's op virtuele machines NV, een SSH-verbinding tooeach VM maken en volg de stappen Hallo voor uw Linux-distributie.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-109">tooinstall NVIDIA GRID drivers on NV VMs, make an SSH connection tooeach VM and follow hello steps for your Linux distribution.</span></span> 

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="b3e2e-110">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="b3e2e-110">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="b3e2e-111">Voer Hallo `lspci` opdracht.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-111">Run hello `lspci` command.</span></span> <span data-ttu-id="b3e2e-112">Controleer of Hallo NVIDIA M60 kaart of kaarten zichtbaar als PCI-apparaten zijn.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-112">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>

2. <span data-ttu-id="b3e2e-113">Updates installeren.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-113">Install updates.</span></span>

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. <span data-ttu-id="b3e2e-114">Hallo Nouveau kernelstuurprogramma dat niet compatibel met de Hallo NVIDIA stuurprogramma is uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-114">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="b3e2e-115">(Alleen gebruiken Hallo NVIDIA stuurprogramma op virtuele machines NV.) toodo dit, maakt u een bestand in `/etc/modprobe.d `met de naam `nouveau.conf` Hello volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="b3e2e-115">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. <span data-ttu-id="b3e2e-116">Hallo VM starten en opnieuw verbinding.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-116">Reboot hello VM and reconnect.</span></span> <span data-ttu-id="b3e2e-117">Exit X-server:</span><span class="sxs-lookup"><span data-stu-id="b3e2e-117">Exit X server:</span></span>

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. <span data-ttu-id="b3e2e-118">Download en installeer Hallo RASTER stuurprogramma:</span><span class="sxs-lookup"><span data-stu-id="b3e2e-118">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. <span data-ttu-id="b3e2e-119">Wanneer u wordt gevraagd of u wilt dat toorun Hallo nvidia xconfig hulpprogramma tooupdate uw configuratiebestand X, selecteert u **Ja**.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-119">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="b3e2e-120">Nadat de installatie is voltooid, kopieert u /etc/nvidia/gridd.conf.template tooa nieuwe bestand gridd.conf op locatie/etc/nvidia /</span><span class="sxs-lookup"><span data-stu-id="b3e2e-120">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. <span data-ttu-id="b3e2e-121">Hallo te volgende toevoegen`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="b3e2e-121">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="b3e2e-122">Hallo VM Start en tooverify Hallo installatie doorgaan.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-122">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="b3e2e-123">Op basis van centOS 7.3 of Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="b3e2e-123">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>


1. <span data-ttu-id="b3e2e-124">Hallo kernel en DKMS bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-124">Update hello kernel and DKMS.</span></span>
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. <span data-ttu-id="b3e2e-125">Hallo Nouveau kernelstuurprogramma dat niet compatibel met de Hallo NVIDIA stuurprogramma is uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-125">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="b3e2e-126">(Alleen gebruiken Hallo NVIDIA stuurprogramma op virtuele machines NV.) toodo dit, maakt u een bestand in `/etc/modprobe.d `met de naam `nouveau.conf` Hello volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="b3e2e-126">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. <span data-ttu-id="b3e2e-127">Hallo VM opnieuw opstarten, opnieuw verbinding maken en te installeren Hallo nieuwste Linux-integratieservices voor Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="b3e2e-127">Reboot hello VM, reconnect, and install hello latest Linux Integration Services for Hyper-V:</span></span>
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. <span data-ttu-id="b3e2e-128">Toohello VM opnieuw en Voer Hallo `lspci` opdracht.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-128">Reconnect toohello VM and run hello `lspci` command.</span></span> <span data-ttu-id="b3e2e-129">Controleer of Hallo NVIDIA M60 kaart of kaarten zichtbaar als PCI-apparaten zijn.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-129">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>
 
5. <span data-ttu-id="b3e2e-130">Download en installeer Hallo RASTER stuurprogramma:</span><span class="sxs-lookup"><span data-stu-id="b3e2e-130">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. <span data-ttu-id="b3e2e-131">Wanneer u wordt gevraagd of u wilt dat toorun Hallo nvidia xconfig hulpprogramma tooupdate uw configuratiebestand X, selecteert u **Ja**.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-131">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="b3e2e-132">Nadat de installatie is voltooid, kopieert u /etc/nvidia/gridd.conf.template tooa nieuwe bestand gridd.conf op locatie/etc/nvidia /</span><span class="sxs-lookup"><span data-stu-id="b3e2e-132">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. <span data-ttu-id="b3e2e-133">Hallo te volgende toevoegen`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="b3e2e-133">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="b3e2e-134">Hallo VM Start en tooverify Hallo installatie doorgaan.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-134">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="verify-driver-installation"></a><span data-ttu-id="b3e2e-135">Controleer of de installatie van stuurprogramma</span><span class="sxs-lookup"><span data-stu-id="b3e2e-135">Verify driver installation</span></span>


<span data-ttu-id="b3e2e-136">tooquery Hallo GPU Apparaatstatus, SSH toohello VM en Voer Hallo [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) opdrachtregelprogramma met Hallo stuurprogramma geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-136">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="b3e2e-137">De vergelijkbare toohello volgende uitvoer wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="b3e2e-137">Output similar toohello following appears:</span></span>

![De apparaatstatus NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a><span data-ttu-id="b3e2e-139">X11 server</span><span class="sxs-lookup"><span data-stu-id="b3e2e-139">X11 server</span></span>
<span data-ttu-id="b3e2e-140">Als u een X11 moet server voor externe verbindingen tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) wordt aanbevolen, omdat hiermee hardwareversnelling van afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-140">If you need an X11 server for remote connections tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) is recommended because it allows hardware acceleration of graphics.</span></span> <span data-ttu-id="b3e2e-141">Hallo BusID Hallo M60 apparaat moet handmatig worden toegevoegd toohello xconfig-bestand (`etc/X11/xorg.conf` op Ubuntu 16.04 TNS, `/etc/X11/XF86config` op CentOS 7.3 of Red Hat Enterprise Server 7.3).</span><span class="sxs-lookup"><span data-stu-id="b3e2e-141">hello BusID of hello M60 device must be manually added toohello xconfig file (`etc/X11/xorg.conf` on Ubuntu 16.04 LTS, `/etc/X11/XF86config` on CentOS 7.3 or Red Hat Enterprise Server 7.3).</span></span> <span data-ttu-id="b3e2e-142">Voeg een `"Device"` vergelijkbare toohello volgende sectie:</span><span class="sxs-lookup"><span data-stu-id="b3e2e-142">Add a `"Device"` section similar toohello following:</span></span>
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
<span data-ttu-id="b3e2e-143">Daarnaast uw `"Screen"` sectie toouse dit apparaat.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-143">Additionally, update your `"Screen"` section toouse this device.</span></span>
 
<span data-ttu-id="b3e2e-144">Hallo BusID kunt u vinden door te voeren</span><span class="sxs-lookup"><span data-stu-id="b3e2e-144">hello BusID can be found by running</span></span>

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
<span data-ttu-id="b3e2e-145">Hallo BusID kunt wijzigen als een virtuele machine opgehaald opnieuw toegewezen of opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-145">hello BusID can change when a VM gets reallocated or rebooted.</span></span> <span data-ttu-id="b3e2e-146">Daarom kunt u een script tooupdate hello BusID in Hallo X11 configuratie toouse wanneer een virtuele machine opnieuw is opgestart.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-146">Therefore, you may want toouse a script tooupdate hello BusID in hello X11 configuration when a VM is rebooted.</span></span> <span data-ttu-id="b3e2e-147">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b3e2e-147">For example:</span></span>

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed too${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

<span data-ttu-id="b3e2e-148">Dit bestand kan worden aangeroepen als basis voor opgestart door het maken van een vermelding voor het in `/etc/rc.d/rc3.d`.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-148">This file can be invoked as root on boot by creating an entry for it in `/etc/rc.d/rc3.d`.</span></span>


## <a name="install-cuda-drivers-for-nc-vms"></a><span data-ttu-id="b3e2e-149">Voor virtuele machines NC CUDA stuurprogramma's installeren</span><span class="sxs-lookup"><span data-stu-id="b3e2e-149">Install CUDA drivers for NC VMs</span></span>

<span data-ttu-id="b3e2e-150">Hier vindt u stappen tooinstall NVIDIA-stuurprogramma's op virtuele machines van Linux NC van Hallo NVIDIA CUDA Toolkit 8.0.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-150">Here are steps tooinstall NVIDIA drivers on Linux NC VMs from hello NVIDIA CUDA Toolkit 8.0.</span></span> 

<span data-ttu-id="b3e2e-151">C en C++-ontwikkelaars kunnen desgewenst Hallo volledige Toolkit toobuild GPU-versnelde toepassingen installeren.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-151">C and C++ developers can optionally install hello full Toolkit toobuild GPU-accelerated applications.</span></span> <span data-ttu-id="b3e2e-152">Zie voor meer informatie, Hallo [CUDA installatiehandleiding](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span><span class="sxs-lookup"><span data-stu-id="b3e2e-152">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span></span>


> [!NOTE]
> <span data-ttu-id="b3e2e-153">CUDA stuurprogramma downloadkoppelingen opgegeven op het moment van publicatie hier actueel zijn.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-153">CUDA driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="b3e2e-154">Voor Hallo nieuwste CUDA stuurprogramma's, gaat u naar Hallo [NVIDIA](http://www.nvidia.com/) website.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-154">For hello latest CUDA drivers, visit hello [NVIDIA](http://www.nvidia.com/) website.</span></span>
>

<span data-ttu-id="b3e2e-155">tooinstall CUDA Toolkit, moet een SSH-verbinding tooeach VM.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-155">tooinstall CUDA Toolkit, make an SSH connection tooeach VM.</span></span> <span data-ttu-id="b3e2e-156">tooverify die Hallo systeem heeft een CUDA-compatibele GPU, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b3e2e-156">tooverify that hello system has a CUDA-capable GPU, run hello following command:</span></span>

```bash
lspci | grep -i NVIDIA
```
<span data-ttu-id="b3e2e-157">Hier ziet u uitvoer vergelijkbare toohello voorbeeld (met een kaart NVIDIA Tesla R80) te volgen:</span><span class="sxs-lookup"><span data-stu-id="b3e2e-157">You will see output similar toohello following example (showing an NVIDIA Tesla K80 card):</span></span>

![opdrachtuitvoer lspci](./media/n-series-driver-setup/lspci.png)

<span data-ttu-id="b3e2e-159">Vervolgens uitvoeren installatieopdrachten die specifiek is voor uw distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-159">Then run installation commands specific for your distribution.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="b3e2e-160">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="b3e2e-160">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="b3e2e-161">Download en installeer Hallo CUDA stuurprogramma's.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-161">Download and install hello CUDA drivers.</span></span>
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  <span data-ttu-id="b3e2e-162">Hallo-installatie kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-162">hello installation can take several minutes.</span></span>

2. <span data-ttu-id="b3e2e-163">toooptionally installatie Hallo voltooid CUDA toolkit, type:</span><span class="sxs-lookup"><span data-stu-id="b3e2e-163">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo apt-get install cuda
  ```

3. <span data-ttu-id="b3e2e-164">Hallo VM Start en tooverify Hallo installatie doorgaan.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-164">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="b3e2e-165">Op basis van centOS 7.3 of Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="b3e2e-165">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

1. <span data-ttu-id="b3e2e-166">Updates downloaden.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-166">Get updates.</span></span> 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. <span data-ttu-id="b3e2e-167">Toohello VM opnieuw aan en installeer Hallo nieuwste Linux-integratieservices voor Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-167">Reconnect toohello VM and install hello latest Linux Integration Services for Hyper-V.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b3e2e-168">Als u een installatiekopie op basis van CentOS HPC geïnstalleerd op een NC24r VM, slaat u tooStep 3.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-168">If you installed a CentOS-based HPC image on an NC24r VM, skip tooStep 3.</span></span> <span data-ttu-id="b3e2e-169">Omdat Azure RDMA-stuurprogramma's en Linux-integratieservices zijn geïnstalleerd in Hallo-installatiekopie, LIS moet niet worden bijgewerkt en kernel-updates zijn standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-169">Because Azure RDMA drivers and Linux Integration Services are pre-installed in hello image, LIS should not be upgraded, and kernel updates are disabled by default.</span></span>
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. <span data-ttu-id="b3e2e-170">Opnieuw verbinding maken toohello VM en doorgaan met installatie Hello volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="b3e2e-170">Reconnect toohello VM and continue installation with hello following commands:</span></span>

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

  <span data-ttu-id="b3e2e-171">Hallo-installatie kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-171">hello installation can take several minutes.</span></span> 

4. <span data-ttu-id="b3e2e-172">toooptionally installatie Hallo voltooid CUDA toolkit, type:</span><span class="sxs-lookup"><span data-stu-id="b3e2e-172">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo yum install cuda
  ```

5. <span data-ttu-id="b3e2e-173">Hallo VM Start en tooverify Hallo installatie doorgaan.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-173">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="verify-driver-installation"></a><span data-ttu-id="b3e2e-174">Controleer of de installatie van stuurprogramma</span><span class="sxs-lookup"><span data-stu-id="b3e2e-174">Verify driver installation</span></span>


<span data-ttu-id="b3e2e-175">tooquery Hallo GPU Apparaatstatus, SSH toohello VM en Voer Hallo [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) opdrachtregelprogramma met Hallo stuurprogramma geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-175">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="b3e2e-176">De vergelijkbare toohello volgende uitvoer wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="b3e2e-176">Output similar toohello following appears:</span></span>

![De apparaatstatus NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a><span data-ttu-id="b3e2e-178">Updates voor stuurprogramma's CUDA</span><span class="sxs-lookup"><span data-stu-id="b3e2e-178">CUDA driver updates</span></span>

<span data-ttu-id="b3e2e-179">We bevelen aan dat u regelmatig CUDA stuurprogramma's na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-179">We recommend that you periodically update CUDA drivers after deployment.</span></span>

#### <a name="ubuntu-1604-lts"></a><span data-ttu-id="b3e2e-180">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="b3e2e-180">Ubuntu 16.04 LTS</span></span>

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="b3e2e-181">Op basis van centOS 7.3 of Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="b3e2e-181">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a><span data-ttu-id="b3e2e-182">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="b3e2e-182">Troubleshooting</span></span>

* <span data-ttu-id="b3e2e-183">Er is een bekend probleem met stuurprogramma's voor CUDA op N-reeks virtuele machines in Azure Hallo 4.4.0-75 Linux kernel op Ubuntu 16.04 TNS uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-183">There is a known issue with CUDA drivers on Azure N-series VMs running hello 4.4.0-75 Linux kernel on Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="b3e2e-184">Als u een upgrade vanaf een eerdere kernelversie uitvoert upgraden tooat minimaal kernel versie 4.4.0-77.</span><span class="sxs-lookup"><span data-stu-id="b3e2e-184">If you are upgrading from an earlier kernel version, upgrade tooat least kernel version 4.4.0-77.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="b3e2e-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b3e2e-185">Next steps</span></span>

* <span data-ttu-id="b3e2e-186">Zie voor meer informatie over Hallo NVIDIA GPU's op Hallo N-reeks virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="b3e2e-186">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="b3e2e-187">[NVIDIA Tesla R80](http://www.nvidia.com/object/tesla-k80.html) (voor NC Azure VM's)</span><span class="sxs-lookup"><span data-stu-id="b3e2e-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="b3e2e-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (voor NV Azure VM's)</span><span class="sxs-lookup"><span data-stu-id="b3e2e-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="b3e2e-189">Zie toocapture een Linux VM-installatiekopie met de geïnstalleerde stuurprogramma's NVIDIA [hoe toogeneralize en een virtuele Linux-machine vastleggen](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b3e2e-189">toocapture a Linux VM image with your installed NVIDIA drivers, see [How toogeneralize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
