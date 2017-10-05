---
title: Opstarten van diagnostische gegevens van virtuele Linux-machines in Azure | Microsoft-document
description: Overzicht van de twee foutopsporing functies voor virtuele Linux-machines in Azure
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
ms.openlocfilehash: 70254d39b5c6326166f7e29fdfc99533835502f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-boot-diagnostics-to-troubleshoot-linux-virtual-machines-in-azure"></a><span data-ttu-id="f1f86-103">Het gebruik van diagnostische gegevens over opstarten Linux virtuele machines in Azure oplossen</span><span class="sxs-lookup"><span data-stu-id="f1f86-103">How to use boot diagnostics to troubleshoot Linux virtual machines in Azure</span></span>

<span data-ttu-id="f1f86-104">Ondersteuning voor twee foutopsporingsfuncties is nu beschikbaar in Azure: ondersteuning voor Console-uitvoer en Schermafbeelding voor het Azure Virtual Machines Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="f1f86-104">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="f1f86-105">Wanneer u uw eigen installatiekopie importeert in Azure of een van de installatiekopieën van het platform opstart, kan een VM vanwege verschillende redenen in een status belanden waarin deze niet kan worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="f1f86-105">When bringing your own image to Azure or even booting one of the platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="f1f86-106">Met deze functies kunt u uw virtuele machines eenvoudig analyseren en herstellen na fouten bij het opstarten.</span><span class="sxs-lookup"><span data-stu-id="f1f86-106">These features enable you to easily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="f1f86-107">Bij virtuele Linux-machines kunt u eenvoudig de uitvoer van uw consolelogboek bekijken via de portal:</span><span class="sxs-lookup"><span data-stu-id="f1f86-107">For Linux Virtual Machines, you can easily view the output of your console log from the Portal:</span></span>

![Azure Portal](./media/boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="f1f86-109">U kunt echter bij zowel virtuele Windows- als Linux-machines een schermopname van de virtuele machine bekijken via de hypervisor van Azure:</span><span class="sxs-lookup"><span data-stu-id="f1f86-109">However, for both Windows and Linux Virtual Machines, Azure also enables you to see a screenshot of the VM from the hypervisor:</span></span>

![Fout](./media/boot-diagnostics/screenshot2.png)

<span data-ttu-id="f1f86-111">Beide functies worden ondersteund voor virtuele Azure-machines in alle regio's.</span><span class="sxs-lookup"><span data-stu-id="f1f86-111">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="f1f86-112">Houd er rekening mee dat het tot 10 minuten kan duren voordat de schermafbeeldingen en uitvoer worden weergegeven in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="f1f86-112">Note, screenshots, and output can take up to 10 minutes to appear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="f1f86-113">Veelvoorkomende opstartfouten</span><span class="sxs-lookup"><span data-stu-id="f1f86-113">Common boot errors</span></span>

- [<span data-ttu-id="f1f86-114">Bestandssystemen</span><span class="sxs-lookup"><span data-stu-id="f1f86-114">File system issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [<span data-ttu-id="f1f86-115">Kernel-problemen</span><span class="sxs-lookup"><span data-stu-id="f1f86-115">Kernel Issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [<span data-ttu-id="f1f86-116">FSTAB-fouten</span><span class="sxs-lookup"><span data-stu-id="f1f86-116">FSTAB errors</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="f1f86-117">Diagnostische gegevens op een nieuwe virtuele machine inschakelen</span><span class="sxs-lookup"><span data-stu-id="f1f86-117">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="f1f86-118">Wanneer u een nieuwe virtuele machine maakt in de Preview Portal, selecteert u de **Azure Resource Manager** uit de vervolgkeuzelijst van het implementatiemodel:</span><span class="sxs-lookup"><span data-stu-id="f1f86-118">When creating a new Virtual Machine from the Preview Portal, select the **Azure Resource Manager** from the deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="f1f86-120">Configureer de optie Bewaking om het opslagaccount te selecteren waarin u wilt deze diagnostische bestanden wilt plaatsen.</span><span class="sxs-lookup"><span data-stu-id="f1f86-120">Configure the Monitoring option to select the storage account where you would like to place these diagnostic files.</span></span>
 
    ![VM maken](./media/boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="f1f86-122">Als u met een Azure Resource Manager-sjabloon implementeert, gaat u naar de resource van de virtuele machine en voegt u de sectie diagnostisch profiel toe.</span><span class="sxs-lookup"><span data-stu-id="f1f86-122">If you are deploying from an Azure Resource Manager template, navigate to your Virtual Machine resource and append the diagnostics profile section.</span></span> <span data-ttu-id="f1f86-123">Vergeet niet de API-versieheader '2015-06-15' te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f1f86-123">Remember to use the “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="f1f86-124">Met het diagnostische profiel kunt u het opslagaccount selecteren waarin u deze logboeken wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="f1f86-124">The diagnostics profile enables you to select the storage account where you want to put these logs.</span></span>

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

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="f1f86-125">Een bestaande virtuele machine bijwerken</span><span class="sxs-lookup"><span data-stu-id="f1f86-125">Update an existing virtual machine</span></span>

<span data-ttu-id="f1f86-126">U kunt ook een bestaande virtuele machine via de portal bijwerken zodat de diagnostische gegevens over opstarten via de portal.</span><span class="sxs-lookup"><span data-stu-id="f1f86-126">To enable boot diagnostics through the portal, you can also update an existing virtual machine through the portal.</span></span> <span data-ttu-id="f1f86-127">Selecteer de optie Diagnostische gegevens over het opstarten en selecteer vervolgens Opslaan.</span><span class="sxs-lookup"><span data-stu-id="f1f86-127">Select the Boot Diagnostics option and Save.</span></span> <span data-ttu-id="f1f86-128">Start de VM opnieuw op om de wijzigingen door te voeren.</span><span class="sxs-lookup"><span data-stu-id="f1f86-128">Restart the VM to take effect.</span></span>

![Bestaande VM bijwerken](./media/boot-diagnostics/screenshot5.png)