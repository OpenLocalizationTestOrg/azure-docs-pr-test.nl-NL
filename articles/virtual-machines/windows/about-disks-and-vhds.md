---
title: aaaAbout schijven en VHD's voor Microsoft Azure VM's van Windows | Microsoft Docs
description: Meer informatie over de basisprincipes van Hallo van schijven en virtuele harde schijven voor Windows virtuele machines in Azure.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 1b0d6bf05237bb3d1497b2c60f79a0159b730108
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a><span data-ttu-id="50399-103">Over schijven en VHD's voor VM's van Windows Azure</span><span class="sxs-lookup"><span data-stu-id="50399-103">About disks and VHDs for Azure Windows VMs</span></span>
<span data-ttu-id="50399-104">Net als een andere computer gebruik virtuele machines in Azure schijven als een plaats toostore een besturingssysteem, toepassingen en gegevens.</span><span class="sxs-lookup"><span data-stu-id="50399-104">Just like any other computer, virtual machines in Azure use disks as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="50399-105">Alle virtuele machines in Azure hebt ten minste twee schijven: de schijf van een Windows-besturingssysteem en een tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="50399-105">All Azure virtual machines have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="50399-106">Hallo besturingssysteemschijf wordt gemaakt van een installatiekopie en besturingssysteemschijf Hallo zowel Hallo installatiekopie zijn virtuele harde schijven (VHD's) opgeslagen in Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="50399-106">hello operating system disk is created from an image, and both hello operating system disk and hello image are virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="50399-107">Virtuele machines hebben ook een of meer gegevensschijven die ook als virtuele harde schijven zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="50399-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="50399-108">In dit artikel wordt bespreken Hallo verschillende manieren worden gebruikt voor Hallo schijven, en vervolgens bespreken Hallo verschillende typen schijven kunt u maken en gebruiken.</span><span class="sxs-lookup"><span data-stu-id="50399-108">In this article, we will talk about hello different uses for hello disks, and then discuss hello different types of disks you can create and use.</span></span> <span data-ttu-id="50399-109">In dit artikel is ook beschikbaar voor [virtuele Linux-machines](about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="50399-109">This article is also available for [Linux virtual machines](about-disks-and-vhds.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="50399-110">Schijven die worden gebruikt door virtuele machines</span><span class="sxs-lookup"><span data-stu-id="50399-110">Disks used by VMs</span></span>

<span data-ttu-id="50399-111">Eens kijken hoe Hallo schijven door Hallo VM's worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="50399-111">Let's take a look at how hello disks are used by hello VMs.</span></span>

### <a name="operating-system-disk"></a><span data-ttu-id="50399-112">Besturingssysteemschijf</span><span class="sxs-lookup"><span data-stu-id="50399-112">Operating system disk</span></span>
<span data-ttu-id="50399-113">Elke virtuele machine heeft een gekoppelde besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="50399-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="50399-114">Het is geregistreerd als een SATA harde schijf en gelabeld als Hallo tekstknooppunt standaard.</span><span class="sxs-lookup"><span data-stu-id="50399-114">It's registered as a SATA drive and labeled as hello C: drive by default.</span></span> <span data-ttu-id="50399-115">Deze schijf heeft een maximale capaciteit van 2048 gigabyte (GB).</span><span class="sxs-lookup"><span data-stu-id="50399-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

### <a name="temporary-disk"></a><span data-ttu-id="50399-116">Tijdelijke schijf</span><span class="sxs-lookup"><span data-stu-id="50399-116">Temporary disk</span></span>
<span data-ttu-id="50399-117">Elke virtuele machine bevat een tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="50399-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="50399-118">Hallo tijdelijke schijf opslag op korte termijn voor toepassingen en processen en gegevens van de beoogde tooonly opslaan zoals pagina of het swap-bestanden is.</span><span class="sxs-lookup"><span data-stu-id="50399-118">hello temporary disk provides short-term storage for applications and processes and is intended tooonly store data such as page or swap files.</span></span> <span data-ttu-id="50399-119">Gegevens op de tijdelijke schijf Hallo zijn mogelijk verloren gegaan tijdens een [onderhoud](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) of wanneer u [opnieuw implementeren van een virtuele machine](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="50399-119">Data on hello temporary disk may be lost during a [maintenance event](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="50399-120">Tijdens een standaard herstart Hallo VM moet Hallo-gegevens op de tijdelijke schijf Hallo handhaven.</span><span class="sxs-lookup"><span data-stu-id="50399-120">During a standard reboot of hello VM, hello data on hello temporary drive should persist.</span></span>

<span data-ttu-id="50399-121">Hallo tijdelijke schijf wordt aangeduid als Hallo station D: standaard en het wordt gebruikt voor het opslaan van pagefile.sys.</span><span class="sxs-lookup"><span data-stu-id="50399-121">hello temporary disk is labeled as hello D: drive by default and it used for storing pagefile.sys.</span></span> <span data-ttu-id="50399-122">tooremap deze schijf tooa andere stationsletter, Zie [wijziging stationsletter op Hallo van Hallo Windows tijdelijke schijf](change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="50399-122">tooremap this disk tooa different drive letter, see [Change hello drive letter of hello Windows temporary disk](change-drive-letter.md).</span></span> <span data-ttu-id="50399-123">Hallo-grootte van de tijdelijke schijf Hallo varieert, afhankelijk van de grootte van de Hallo van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="50399-123">hello size of hello temporary disk varies, based on hello size of hello virtual machine.</span></span> <span data-ttu-id="50399-124">Zie voor meer informatie [grootten voor Windows virtuele machines](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="50399-124">For more information, see [Sizes for Windows virtual machines](sizes.md).</span></span>

<span data-ttu-id="50399-125">Zie voor meer informatie over hoe Azure gebruikt voor de tijdelijke schijf Hallo [begrijpen Hallo tijdelijke station op Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="50399-125">For more information on how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>


### <a name="data-disk"></a><span data-ttu-id="50399-126">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="50399-126">Data disk</span></span>
<span data-ttu-id="50399-127">Een gegevensschijf is een VHD die is aangesloten tooa virtuele machine toostore toepassingsgegevens of andere gegevens die u nodig hebt tookeep.</span><span class="sxs-lookup"><span data-stu-id="50399-127">A data disk is a VHD that's attached tooa virtual machine toostore application data, or other data you need tookeep.</span></span> <span data-ttu-id="50399-128">Gegevensschijven worden geregistreerd als SCSI-stations en zijn gelabeld met een letter die u kiest.</span><span class="sxs-lookup"><span data-stu-id="50399-128">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="50399-129">Elke gegevensschijf heeft een maximale capaciteit van 4095 GB.</span><span class="sxs-lookup"><span data-stu-id="50399-129">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="50399-130">Hallo grootte van Hallo virtuele machine bepaalt hoeveel gegevensschijven kunt u tooit en Hallo type opslag kunt u koppelen toohost Hallo schijven.</span><span class="sxs-lookup"><span data-stu-id="50399-130">hello size of hello virtual machine determines how many data disks you can attach tooit and hello type of storage you can use toohost hello disks.</span></span>

> [!NOTE]
> <span data-ttu-id="50399-131">Zie voor meer informatie over de capaciteit van virtuele machines, [grootten voor Windows virtuele machines](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="50399-131">For more information about virtual machines capacities, see [Sizes for Windows virtual machines](sizes.md).</span></span>
> 

<span data-ttu-id="50399-132">Azure maakt een besturingssysteemschijf wanneer u een virtuele machine van een installatiekopie maakt.</span><span class="sxs-lookup"><span data-stu-id="50399-132">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="50399-133">Als u een afbeelding met gegevensschijven, maakt Azure ook Hallo gegevensschijven bij het maken van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="50399-133">If you use an image that includes data disks, Azure also creates hello data disks when it creates hello virtual machine.</span></span> <span data-ttu-id="50399-134">Anders toevoegen u gegevensschijven nadat u Hallo virtuele machine hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50399-134">Otherwise, you add data disks after you create hello virtual machine.</span></span>

<span data-ttu-id="50399-135">U kunt gegevens schijven tooa virtuele machine door op elk gewenst moment toevoegen **koppelen** Hallo schijf toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="50399-135">You can add data disks tooa virtual machine at any time, by **attaching** hello disk toohello virtual machine.</span></span> <span data-ttu-id="50399-136">U kunt een VHD die u hebt geüpload of gekopieerd tooyour storage-account of een die Azure voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50399-136">You can use a VHD that you've uploaded or copied tooyour storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="50399-137">Koppelen van een gegevensschijf koppelt Hallo VHD-bestand aan Hallo VM door het plaatsen van een 'lease' op Hallo VHD zodat deze kan niet worden verwijderd uit de opslag terwijl er nog steeds gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="50399-137">Attaching a data disk associates hello VHD file with hello VM by placing a 'lease' on hello VHD so it can't be deleted from storage while it's still attached.</span></span>


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a><span data-ttu-id="50399-138">Een laatste aanbeveling: gebruik TRIM met niet-beheerde standaardschijven</span><span class="sxs-lookup"><span data-stu-id="50399-138">One last recommendation: Use TRIM with unmanaged standard disks</span></span> 

<span data-ttu-id="50399-139">Als u niet-beheerde standaard schijven (HDD) gebruikt, moet u TRIM inschakelen.</span><span class="sxs-lookup"><span data-stu-id="50399-139">If you use unmanaged standard disks (HDD), you should enable TRIM.</span></span> <span data-ttu-id="50399-140">TRIM worden niet-gebruikte blokken op Hallo schijf verwijderd, zodat u wordt alleen gefactureerd voor opslag die u daadwerkelijk gebruikt.</span><span class="sxs-lookup"><span data-stu-id="50399-140">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="50399-141">Dit kunt besparen op kosten als u grote bestanden maken en deze vervolgens te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="50399-141">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="50399-142">U kunt deze opdracht toocheck Hallo beperkende instelling uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="50399-142">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="50399-143">Open een opdrachtprompt op de virtuele machine van Windows en typ:</span><span class="sxs-lookup"><span data-stu-id="50399-143">Open a command prompt on your Windows VM and type:</span></span>


```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="50399-144">Als de opdracht Hallo 0 retourneert, wordt ' trim ' correct ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="50399-144">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="50399-145">Als deze 1 retourneert, voert u de volgende opdracht tooenable ' trim ' Hallo:</span><span class="sxs-lookup"><span data-stu-id="50399-145">If it returns 1, run hello following command tooenable TRIM:</span></span>

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> <span data-ttu-id="50399-146">Opmerking: Ondersteuning begint met Windows Server 2012 / Windows 8 en hoger, Zie Zie [nieuwe API-apps toestaan toosend 'TRIM en ontkoppelen' hints toostorage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span><span class="sxs-lookup"><span data-stu-id="50399-146">Note: Trim support starts with Windows Server 2012 / Windows 8 and above, see see [New API allows apps toosend "TRIM and Unmap" hints toostorage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span></span>
> 

<!-- Might want toomatch next-steps from overview of managed disks -->
## <a name="next-steps"></a><span data-ttu-id="50399-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="50399-147">Next steps</span></span>
* <span data-ttu-id="50399-148">[Een schijf koppelen](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd extra opslagruimte voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="50399-148">[Attach a disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd additional storage for your VM.</span></span>
* <span data-ttu-id="50399-149">[Wijziging stationsletter op Hallo van Hallo Windows tijdelijke schijf](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) zodat uw toepassing hello D: station voor gegevens gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="50399-149">[Change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) so your application can use hello D: drive for data.</span></span>

