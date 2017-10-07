---
title: aaaBoot diagnostische gegevens van Linux virtuele machines in Azure | Microsoft-document
description: Overzicht van Hallo twee foutopsporing functies voor virtuele Linux-machines in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a><span data-ttu-id="049da-103">Hoe toouse diagnostics tootroubleshoot Linux virtuele machines in Azure worden opgestart</span><span class="sxs-lookup"><span data-stu-id="049da-103">How toouse boot diagnostics tootroubleshoot Linux virtual machines in Azure</span></span>

<span data-ttu-id="049da-104">Ondersteuning voor twee foutopsporingsfuncties is nu beschikbaar in Azure: ondersteuning voor Console-uitvoer en Schermafbeelding voor het Azure Virtual Machines Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="049da-104">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="049da-105">Wanneer u uw eigen installatiekopie tooAzure of zelfs opstarten een van de installatiekopieën van het platform hello te brengen, kunnen er diverse redenen waarom een virtuele Machine in een niet-opstartbare status opgehaald.</span><span class="sxs-lookup"><span data-stu-id="049da-105">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="049da-106">Met deze functies kunt u tooeasily diagnosticeren en op uw virtuele Machines herstellen.</span><span class="sxs-lookup"><span data-stu-id="049da-106">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="049da-107">Voor virtuele Linux-Machines, kunt u eenvoudig hello uitvoer van uw consolelogboek van Hallo Portal bekijken:</span><span class="sxs-lookup"><span data-stu-id="049da-107">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Azure Portal](./media/boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="049da-109">Echter voor Windows en Linux virtuele Machines kunt Azure ook u een schermopname van Hallo VM van de hypervisor Hallo toosee:</span><span class="sxs-lookup"><span data-stu-id="049da-109">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![Fout](./media/boot-diagnostics/screenshot2.png)

<span data-ttu-id="049da-111">Beide functies worden ondersteund voor virtuele Azure-machines in alle regio's.</span><span class="sxs-lookup"><span data-stu-id="049da-111">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="049da-112">Opmerking: de schermafbeeldingen en de uitvoer kunnen duren too10 minuten tooappear in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="049da-112">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="049da-113">Veelvoorkomende opstartfouten</span><span class="sxs-lookup"><span data-stu-id="049da-113">Common boot errors</span></span>

- [<span data-ttu-id="049da-114">Bestandssystemen</span><span class="sxs-lookup"><span data-stu-id="049da-114">File system issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [<span data-ttu-id="049da-115">Kernel-problemen</span><span class="sxs-lookup"><span data-stu-id="049da-115">Kernel Issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [<span data-ttu-id="049da-116">FSTAB-fouten</span><span class="sxs-lookup"><span data-stu-id="049da-116">FSTAB errors</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="049da-117">Diagnostische gegevens op een nieuwe virtuele machine inschakelen</span><span class="sxs-lookup"><span data-stu-id="049da-117">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="049da-118">Wanneer u een nieuwe virtuele Machine maakt van Hallo Preview-Portal, selecteer Hallo **Azure Resource Manager** uit Hallo deployment model vervolgkeuzelijst:</span><span class="sxs-lookup"><span data-stu-id="049da-118">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="049da-120">Hallo bewaking optie tooselect Hallo storage-account waarin u tooplace wilt dat deze diagnostische bestanden configureren.</span><span class="sxs-lookup"><span data-stu-id="049da-120">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![VM maken](./media/boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="049da-122">Als u met een Azure Resource Manager-sjabloon implementeert, virtuele-machinebron tooyour navigeren en Hallo diagnostische profielsectie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="049da-122">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="049da-123">Houd er rekening mee toouse Hallo '2015-06-15' API-versie-header.</span><span class="sxs-lookup"><span data-stu-id="049da-123">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="049da-124">Hallo diagnostische profiel kunt u tooselect Hallo storage-account waar u tooput deze logboeken.</span><span class="sxs-lookup"><span data-stu-id="049da-124">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="049da-125">Een bestaande virtuele machine bijwerken</span><span class="sxs-lookup"><span data-stu-id="049da-125">Update an existing virtual machine</span></span>

<span data-ttu-id="049da-126">tooenable diagnostische gegevens over opstarten via de portal hello, kunt u ook een bestaande virtuele machine via de portal Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="049da-126">tooenable boot diagnostics through hello portal, you can also update an existing virtual machine through hello portal.</span></span> <span data-ttu-id="049da-127">Selecteer Hallo Boot Diagnostics optie en opslaan.</span><span class="sxs-lookup"><span data-stu-id="049da-127">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="049da-128">Opnieuw opstarten Hallo VM tootake effect.</span><span class="sxs-lookup"><span data-stu-id="049da-128">Restart hello VM tootake effect.</span></span>

![Bestaande VM bijwerken](./media/boot-diagnostics/screenshot5.png)