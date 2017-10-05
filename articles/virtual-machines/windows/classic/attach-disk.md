---
title: Een schijf koppelen aan een klassieke Azure-VM | Microsoft Docs
description: Een gegevensschijf koppelen aan een virtuele Windows-machine gemaakt met het klassieke implementatiemodel en het initialiseren.
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: 087d5cda354f6e1780bddd3725859444177abd16
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="attach-a-data-disk-to-a-windows-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="b0261-103">Een gegevensschijf koppelen aan een virtuele Windows-machine die is gemaakt volgens het klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="b0261-103">Attach a data disk to a Windows virtual machine created with the classic deployment model</span></span>
<!--
Refernce article:
    If you want to use the new portal, see [How to attach a data disk to a Windows VM in the Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

<span data-ttu-id="b0261-104">In dit artikel leest u hoe nieuwe en bestaande schijven die zijn gemaakt met het klassieke implementatiemodel om een virtuele Windows-computer met de Azure portal te koppelen.</span><span class="sxs-lookup"><span data-stu-id="b0261-104">This article shows you how to attach new and existing disks created with the Classic deployment model to a Windows virtual machine using the Azure portal.</span></span>

<span data-ttu-id="b0261-105">U kunt ook [een gegevensschijf koppelen aan een Linux-VM in de Azure portal](../../linux/attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b0261-105">You can also [attach a data disk to a Linux VM in the Azure portal](../../linux/attach-disk-portal.md).</span></span>

<span data-ttu-id="b0261-106">Voordat u een schijf koppelen, controleert u de volgende tips:</span><span class="sxs-lookup"><span data-stu-id="b0261-106">Before you attach a disk, review these tips:</span></span>

* <span data-ttu-id="b0261-107">De omvang van de virtuele machine bepaalt hoeveel gegevensschijven die u kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="b0261-107">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="b0261-108">Zie voor meer informatie [grootten voor virtuele machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b0261-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="b0261-109">Premium-opslag gebruiken, moet u een virtuele machine DS-serie- of GS-serie.</span><span class="sxs-lookup"><span data-stu-id="b0261-109">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="b0261-110">Met deze virtuele machines kunt u schijven uit zowel Premium en Standard-opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="b0261-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="b0261-111">Premium-opslag is beschikbaar in bepaalde regio's.</span><span class="sxs-lookup"><span data-stu-id="b0261-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="b0261-112">Zie voor meer informatie [Premium-opslag: krachtige opslag voor Azure Virtual Machine-werkbelasting](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b0261-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="b0261-113">Voor een nieuwe schijf hoeft u niet eerst maken omdat Azure gemaakt wanneer u dit aansluit.</span><span class="sxs-lookup"><span data-stu-id="b0261-113">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="b0261-114">U kunt ook [een gegevensschijf met behulp van Powershell koppelen](../../virtual-machines-windows-attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b0261-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0261-115">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b0261-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>

## <a name="find-the-virtual-machine"></a><span data-ttu-id="b0261-116">De virtuele machine gevonden</span><span class="sxs-lookup"><span data-stu-id="b0261-116">Find the virtual machine</span></span>
1. <span data-ttu-id="b0261-117">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b0261-117">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b0261-118">Selecteer de virtuele machine van de resource die worden vermeld op het dashboard.</span><span class="sxs-lookup"><span data-stu-id="b0261-118">Select the virtual machine from the resource listed on the dashboard.</span></span>
3. <span data-ttu-id="b0261-119">Klik in het linkerdeelvenster onder **instellingen**, klikt u op **schijven**.</span><span class="sxs-lookup"><span data-stu-id="b0261-119">In the left pane under **Settings**, click **Disks**.</span></span>

    ![Instellingen voor de schijf openen](./media/attach-disk/virtualmachinedisks.png)

<span data-ttu-id="b0261-121">Instructies voor het koppelen van een volgende om door te gaan een [nieuwe schijf](#option-1-attach-a-new-disk) of een [bestaande schijf](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="b0261-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="b0261-122">Optie 1: Koppelen en een nieuwe schijf initialiseren</span><span class="sxs-lookup"><span data-stu-id="b0261-122">Option 1: Attach and initialize a new disk</span></span>

1. <span data-ttu-id="b0261-123">Op de **schijven** blade, klikt u op **Attach nieuwe**.</span><span class="sxs-lookup"><span data-stu-id="b0261-123">On the **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="b0261-124">Controleer de standaardinstellingen, indien nodig bijwerken en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b0261-124">Review the default settings, update as necessary, and then click **OK**.</span></span>

   ![Controleer de Schijfinstellingen](./media/attach-disk/attach-new.png)

3. <span data-ttu-id="b0261-126">Nadat Azure de schijf wordt gemaakt en gekoppeld aan de virtuele machine, de nieuwe schijf wordt weergegeven in de instellingen voor de schijf van de virtuele machine onder **gegevensschijven**.</span><span class="sxs-lookup"><span data-stu-id="b0261-126">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="b0261-127">Initialiseer de gegevensschijf van een nieuwe</span><span class="sxs-lookup"><span data-stu-id="b0261-127">Initialize a new data disk</span></span>

1. <span data-ttu-id="b0261-128">Verbinding maken met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b0261-128">Connect to the virtual machine.</span></span> <span data-ttu-id="b0261-129">Zie voor instructies [verbinding maken met en meld u aan een virtuele machine van Azure waarop Windows wordt uitgevoerd bij](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b0261-129">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="b0261-130">Nadat u zich aanmeldt bij de virtuele machine, opent u **Serverbeheer**.</span><span class="sxs-lookup"><span data-stu-id="b0261-130">After you log on to the virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="b0261-131">Selecteer in het linkerdeelvenster **File and Storage Services**.</span><span class="sxs-lookup"><span data-stu-id="b0261-131">In the left pane, select **File and Storage Services**.</span></span>

    ![Open Serverbeheer](../media/attach-disk-portal/fileandstorageservices.png)

3. <span data-ttu-id="b0261-133">Selecteer **schijven**.</span><span class="sxs-lookup"><span data-stu-id="b0261-133">Select **Disks**.</span></span>
4. <span data-ttu-id="b0261-134">De **schijven** sectie vindt u de schijven.</span><span class="sxs-lookup"><span data-stu-id="b0261-134">The **Disks** section lists the disks.</span></span> <span data-ttu-id="b0261-135">De meeste gevallen heeft een virtuele machine schijf 0, schijf van 1 en 2 schijf.</span><span class="sxs-lookup"><span data-stu-id="b0261-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="b0261-136">Schijf 0 is de schijf van het besturingssysteem, schijf van 1 wordt de tijdelijke schijf en schijf 2 is de gegevensschijf die zojuist is gekoppeld aan de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b0261-136">Disk 0 is the operating system disk, disk 1 is the temporary disk, and disk 2 is the data disk newly attached to the virtual machine.</span></span> <span data-ttu-id="b0261-137">De gegevensschijf geeft een lijst van de partitie als **onbekende**.</span><span class="sxs-lookup"><span data-stu-id="b0261-137">The data disk lists the Partition as **Unknown**.</span></span>

 <span data-ttu-id="b0261-138">Met de rechtermuisknop op de schijf en selecteer **initialiseren**.</span><span class="sxs-lookup"><span data-stu-id="b0261-138">Right-click the disk and select **Initialize**.</span></span>

5. <span data-ttu-id="b0261-139">U wordt gewaarschuwd dat alle gegevens worden gewist wanneer de schijf wordt geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="b0261-139">You're notified that all data will be erased when the disk is initialized.</span></span> <span data-ttu-id="b0261-140">Klik op **Ja** te bevestigen van de waarschuwing en initialiseer de schijf.</span><span class="sxs-lookup"><span data-stu-id="b0261-140">Click **Yes** to acknowledge the warning and initialize the disk.</span></span> <span data-ttu-id="b0261-141">Hierna kunt u de partitie wordt weergegeven als **GPT**.</span><span class="sxs-lookup"><span data-stu-id="b0261-141">Once complete, the partition will be listed as **GPT**.</span></span> <span data-ttu-id="b0261-142">Opnieuw met de rechtermuisknop op de schijf en selecteer **NieuwVolume**.</span><span class="sxs-lookup"><span data-stu-id="b0261-142">Right-click the disk again and select **New Volume**.</span></span>

6. <span data-ttu-id="b0261-143">Voltooi de wizard met de standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="b0261-143">Complete the wizard using the default values.</span></span> <span data-ttu-id="b0261-144">Wanneer de wizard is voltooid, de **Volumes** sectie vindt u het nieuwe volume.</span><span class="sxs-lookup"><span data-stu-id="b0261-144">When the wizard is done, the **Volumes** section lists the new volume.</span></span> <span data-ttu-id="b0261-145">De schijf is nu online en gereed voor het opslaan van gegevens.</span><span class="sxs-lookup"><span data-stu-id="b0261-145">The disk is now online and ready to store data.</span></span>

    ![Volume is geïnitialiseerd](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="b0261-147">Optie 2: Een bestaande schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="b0261-147">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="b0261-148">Op de **schijven** blade, klikt u op **Attach bestaande**.</span><span class="sxs-lookup"><span data-stu-id="b0261-148">On the **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="b0261-149">Onder **bestaande schijf koppelen**, klikt u op **locatie**.</span><span class="sxs-lookup"><span data-stu-id="b0261-149">Under **Attach existing disk**, click **Location**.</span></span>

   ![Bestaande schijf koppelen](./media/attach-disk/attachexistingdisksettings.png)
3. <span data-ttu-id="b0261-151">Onder **opslagaccounts**, selecteert u het account en de container waarin het VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="b0261-151">Under **Storage accounts**, select the account and container that holds the .vhd file.</span></span>

   ![Locatie van de VHD vinden](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. <span data-ttu-id="b0261-153">Selecteer het VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="b0261-153">Select the .vhd file.</span></span>
5. <span data-ttu-id="b0261-154">Onder **bestaande schijf koppelen**, het bestand dat u zojuist hebt geselecteerd wordt vermeld onder **VHD-bestand**.</span><span class="sxs-lookup"><span data-stu-id="b0261-154">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="b0261-155">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b0261-155">Click **OK**.</span></span>
6. <span data-ttu-id="b0261-156">Nadat Azure de schijf is gekoppeld aan de virtuele machine, wordt deze weergegeven in de instellingen voor de schijf van de virtuele machine onder **gegevensschijven**.</span><span class="sxs-lookup"><span data-stu-id="b0261-156">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="b0261-157">Gebruik TRIM met standard-opslag</span><span class="sxs-lookup"><span data-stu-id="b0261-157">Use TRIM with standard storage</span></span>

<span data-ttu-id="b0261-158">Als u een standard-opslag (HDD) gebruikt, moet u TRIM inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b0261-158">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="b0261-159">TRIM worden niet-gebruikte blokken op de schijf verwijderd, zodat u wordt alleen gefactureerd voor opslag die u daadwerkelijk gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b0261-159">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="b0261-160">Met ' trim ', kun kosten, met inbegrip van niet-gebruikte blokken die het gevolg zijn van grote bestanden worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b0261-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span></span>

<span data-ttu-id="b0261-161">U kunt deze opdracht om te controleren van de beperkende instelling uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b0261-161">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="b0261-162">Open een opdrachtprompt op de virtuele machine van Windows en typ:</span><span class="sxs-lookup"><span data-stu-id="b0261-162">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="b0261-163">Als de opdracht 0 retourneert, wordt ' trim ' correct ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b0261-163">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="b0261-164">Als deze 1 retourneert, voert u de volgende opdracht voor het vrijmaken van opslagruimte inschakelen:</span><span class="sxs-lookup"><span data-stu-id="b0261-164">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a><span data-ttu-id="b0261-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b0261-165">Next steps</span></span>
<span data-ttu-id="b0261-166">Als uw toepassing gebruikt de D: station voor het opslaan van gegevens, kunt u [wijzigen van de stationsletter van de tijdelijke schijf Windows](../../virtual-machines-windows-change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="b0261-166">If your application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b0261-167">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b0261-167">Additional resources</span></span>
[<span data-ttu-id="b0261-168">Over schijven en virtuele harde schijven voor virtuele machines</span><span class="sxs-lookup"><span data-stu-id="b0261-168">About disks and VHDs for virtual machines</span></span>](../../virtual-machines-linux-about-disks-vhds.md)
