---
title: aaaOptimize VM netwerkdoorvoer | Microsoft Docs
description: Meer informatie over hoe toooptimize virtuele machine van Azure-netwerk doorvoer.
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: a5cff2d0ab6e3553c3f90d99629521a431477de0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a><span data-ttu-id="a274f-103">Netwerkdoorvoer voor Azure virtual machines optimaliseren</span><span class="sxs-lookup"><span data-stu-id="a274f-103">Optimize network throughput for Azure virtual machines</span></span>

<span data-ttu-id="a274f-104">Azure virtuele machines (VM) hebben netwerk standaardinstellingen die verder kunnen worden geoptimaliseerd voor netwerkdoorvoer.</span><span class="sxs-lookup"><span data-stu-id="a274f-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span></span> <span data-ttu-id="a274f-105">Dit artikel wordt beschreven hoe toooptimize doorvoer netwerk voor Microsoft Azure Windows en Linux-virtuele machines, inclusief belangrijke distributies zoals Ubuntu en CentOS van Red Hat.</span><span class="sxs-lookup"><span data-stu-id="a274f-105">This article describes how toooptimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS and Red Hat.</span></span>

## <a name="windows-vm"></a><span data-ttu-id="a274f-106">Windows VM</span><span class="sxs-lookup"><span data-stu-id="a274f-106">Windows VM</span></span>

<span data-ttu-id="a274f-107">Als uw virtuele machine van Windows wordt ondersteund met [versnelde netwerken](virtual-network-create-vm-accelerated-networking.md), het inschakelen van deze functie zijn Hallo optimale configuratie voor de doorvoer.</span><span class="sxs-lookup"><span data-stu-id="a274f-107">If your Windows VM is supported with [Accelerated Networking](virtual-network-create-vm-accelerated-networking.md), enabling that feature would be hello optimal configuration for throughput.</span></span> <span data-ttu-id="a274f-108">Met behulp van ontvangen Side Scaling (RSS) bereiken hogere maximale doorvoer dan een virtuele machine zonder RSS voor alle andere Windows-VM.</span><span class="sxs-lookup"><span data-stu-id="a274f-108">For all other Windows VMs, using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span></span> <span data-ttu-id="a274f-109">RSS mogelijk in een virtuele machine van Windows standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a274f-109">RSS may be disabled by default in a Windows VM.</span></span> <span data-ttu-id="a274f-110">Hallo toodetermine stappen te volgen of RSS is ingeschakeld en tooenable voltooien als deze uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a274f-110">Complete hello following steps toodetermine whether RSS is enabled and tooenable it if it's disabled.</span></span>

1. <span data-ttu-id="a274f-111">Voer Hallo `Get-NetAdapterRss` PowerShell-opdracht toosee als de RSS is ingeschakeld voor een netwerkadapter.</span><span class="sxs-lookup"><span data-stu-id="a274f-111">Enter hello `Get-NetAdapterRss` PowerShell command toosee if RSS is enabled for a network adapter.</span></span> <span data-ttu-id="a274f-112">In Hallo volgende voorbeelduitvoer geretourneerd van Hallo `Get-NetAdapterRss`, RSS is niet ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a274f-112">In hello following example output returned from hello `Get-NetAdapterRss`, RSS is not enabled.</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. <span data-ttu-id="a274f-113">Voer Hallo opdracht tooenable RSS te volgen:</span><span class="sxs-lookup"><span data-stu-id="a274f-113">Enter hello following command tooenable RSS:</span></span>

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    <span data-ttu-id="a274f-114">vorige opdracht Hallo heeft geen uitvoer.</span><span class="sxs-lookup"><span data-stu-id="a274f-114">hello previous command does not have an output.</span></span> <span data-ttu-id="a274f-115">Hallo opdracht NIC-instellingen, waardoor tijdelijke verbinding wordt verbroken voor ongeveer een minuut gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="a274f-115">hello command changed NIC settings, causing temporary connectivity loss for about one minute.</span></span> <span data-ttu-id="a274f-116">Er verschijnt een dialoogvenster Reconnecting tijdens Hallo verbinding wordt verbroken.</span><span class="sxs-lookup"><span data-stu-id="a274f-116">A Reconnecting dialog box appears during hello connectivity loss.</span></span> <span data-ttu-id="a274f-117">Verbinding is doorgaans hersteld na Hallo derde poging.</span><span class="sxs-lookup"><span data-stu-id="a274f-117">Connectivity is typically restored after hello third attempt.</span></span>
3. <span data-ttu-id="a274f-118">Controleer of RSS is ingeschakeld in Hallo VM hiertoe Hallo `Get-NetAdapterRss` opdracht opnieuw.</span><span class="sxs-lookup"><span data-stu-id="a274f-118">Confirm that RSS is enabled in hello VM by entering hello `Get-NetAdapterRss` command again.</span></span> <span data-ttu-id="a274f-119">Als dit lukt, wordt Hallo volgende voorbeelduitvoer geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="a274f-119">If successful, hello following example output is returned:</span></span>

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a><span data-ttu-id="a274f-120">Virtuele Linux-machine</span><span class="sxs-lookup"><span data-stu-id="a274f-120">Linux VM</span></span>

<span data-ttu-id="a274f-121">RSS is altijd ingeschakeld in een Azure Linux VM standaard.</span><span class="sxs-lookup"><span data-stu-id="a274f-121">RSS is always enabled by default in an Azure Linux VM.</span></span> <span data-ttu-id="a274f-122">Linux-kernels die zijn uitgebracht sinds januari 2017 nieuwe netwerk Optimalisatieopties opnemen waarmee u een Linux-VM tooachieve hogere netwerkdoorvoer.</span><span class="sxs-lookup"><span data-stu-id="a274f-122">Linux kernels released since January, 2017 include new network optimization options that enable a Linux VM tooachieve higher network throughput.</span></span>

### <a name="ubuntu"></a><span data-ttu-id="a274f-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a274f-123">Ubuntu</span></span>

<span data-ttu-id="a274f-124">In de optimalisatie van bindingsvolgorde tooget Hallo, moet u eerst toohello ondersteund meest recente versie, vanaf juni 2017 die bijwerken:</span><span class="sxs-lookup"><span data-stu-id="a274f-124">In order tooget hello optimization, first update toohello latest supported version, as of June 2017, which is:</span></span>
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
<span data-ttu-id="a274f-125">Nadat het Hallo-update is voltooid, voert u Hallo opdrachten tooget Hallo nieuwste kernel te volgen:</span><span class="sxs-lookup"><span data-stu-id="a274f-125">After hello update is complete, enter hello following commands tooget hello latest kernel:</span></span>

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

<span data-ttu-id="a274f-126">Optionele opdracht:</span><span class="sxs-lookup"><span data-stu-id="a274f-126">Optional command:</span></span>

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a><span data-ttu-id="a274f-127">Ubuntu Azure Preview-kernel</span><span class="sxs-lookup"><span data-stu-id="a274f-127">Ubuntu Azure Preview kernel</span></span>
> [!WARNING]
> <span data-ttu-id="a274f-128">Deze Azure Linux Preview kernel heeft mogelijk geen Hallo hetzelfde niveau van beschikbaarheid en betrouwbaarheid als Marketplace-installatiekopieën en kernels die in het algemeen beschikbaarheid release.</span><span class="sxs-lookup"><span data-stu-id="a274f-128">This Azure Linux Preview kernel may not have hello same level of availability and reliability as Marketplace images and kernels that are in general availability release.</span></span> <span data-ttu-id="a274f-129">Hallo-functie wordt niet ondersteund, kan hebben beperkte mogelijkheden en zijn mogelijk niet zo betrouwbaar is als Hallo standaard kernel.</span><span class="sxs-lookup"><span data-stu-id="a274f-129">hello feature is not supported, may have constrained capabilities, and may not be as reliable as hello default kernel.</span></span> <span data-ttu-id="a274f-130">Gebruik deze kernel niet voor productieworkloads.</span><span class="sxs-lookup"><span data-stu-id="a274f-130">Do not use this kernel for production workloads.</span></span>

<span data-ttu-id="a274f-131">De prestaties aanzienlijk doorvoer kan worden bereikt door hello Azure Linux kernel voorgestelde installeren.</span><span class="sxs-lookup"><span data-stu-id="a274f-131">Significant throughput performance can be achieved by installing hello proposed Azure Linux kernel.</span></span> <span data-ttu-id="a274f-132">tootry deze kernel deze too/etc/apt/sources.list regel toevoegen</span><span class="sxs-lookup"><span data-stu-id="a274f-132">tootry this kernel, add this line too/etc/apt/sources.list</span></span>

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

<span data-ttu-id="a274f-133">Voer deze opdrachten als hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="a274f-133">Then run these commands as root.</span></span>
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a><span data-ttu-id="a274f-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="a274f-134">CentOS</span></span>

<span data-ttu-id="a274f-135">In de optimalisatie van bindingsvolgorde tooget Hallo, moet u eerst toohello ondersteund meest recente versie, vanaf juli 2017 die bijwerken:</span><span class="sxs-lookup"><span data-stu-id="a274f-135">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
<span data-ttu-id="a274f-136">Nadat het Hallo-update is voltooid, Hallo installeren de nieuwste Linux Integration Services (LIS).</span><span class="sxs-lookup"><span data-stu-id="a274f-136">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="a274f-137">Hallo doorvoeroptimalistatietaak wordt LIS, vanaf 4.2.2-2.</span><span class="sxs-lookup"><span data-stu-id="a274f-137">hello throughput optimization is in LIS, starting from 4.2.2-2.</span></span> <span data-ttu-id="a274f-138">Voer Hallo opdrachten tooinstall LIS te volgen:</span><span class="sxs-lookup"><span data-stu-id="a274f-138">Enter hello following commands tooinstall LIS:</span></span>

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a><span data-ttu-id="a274f-139">Red Hat</span><span class="sxs-lookup"><span data-stu-id="a274f-139">Red Hat</span></span>

<span data-ttu-id="a274f-140">In de optimalisatie van bindingsvolgorde tooget Hallo, moet u eerst toohello ondersteund meest recente versie, vanaf juli 2017 die bijwerken:</span><span class="sxs-lookup"><span data-stu-id="a274f-140">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
<span data-ttu-id="a274f-141">Nadat het Hallo-update is voltooid, Hallo installeren de nieuwste Linux Integration Services (LIS).</span><span class="sxs-lookup"><span data-stu-id="a274f-141">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="a274f-142">Hallo doorvoeroptimalistatietaak wordt LIS, vanaf 4.2.</span><span class="sxs-lookup"><span data-stu-id="a274f-142">hello throughput optimization is in LIS, starting from 4.2.</span></span> <span data-ttu-id="a274f-143">Voer Hallo opdrachten toodownload te volgen en installeren van LIS:</span><span class="sxs-lookup"><span data-stu-id="a274f-143">Enter hello following commands toodownload and install LIS:</span></span>

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

<span data-ttu-id="a274f-144">Meer informatie over Linux Integration Services versie 4.2 voor Hyper-V door het bekijken van Hallo [downloadpagina](https://www.microsoft.com/download/details.aspx?id=55106).</span><span class="sxs-lookup"><span data-stu-id="a274f-144">Learn more about Linux Integration Services Version 4.2 for Hyper-V by viewing hello [download page](https://www.microsoft.com/download/details.aspx?id=55106).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a274f-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a274f-145">Next steps</span></span>
* <span data-ttu-id="a274f-146">Nu hello VM geoptimaliseerd, gaat u naar Hallo resultaat [bandbreedte/doorvoer testen van de virtuele machine van Azure](virtual-network-bandwidth-testing.md) voor uw scenario.</span><span class="sxs-lookup"><span data-stu-id="a274f-146">Now that hello VM is optimized, see hello result with [Bandwidth/Throughput testing Azure VM](virtual-network-bandwidth-testing.md) for your scenario.</span></span>
* <span data-ttu-id="a274f-147">Klik hier als u meer wilt weten met [Azure Virtual Network Veelgestelde vragen (FAQ)](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="a274f-147">Learn more with [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
