---
title: Het Windows-VM-extensie fouten oplossen | Microsoft Docs
description: Meer informatie over het oplossen van fouten voor virtuele machine van Windows Azure-extensie
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: 878ab9b6-c3e6-40be-82d4-d77fecd5030f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 4dba196e1b838f2092b30972fb070514bd2a4b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a><span data-ttu-id="8dd55-103">Virtuele machine van Windows Azure-extensie fouten oplossen</span><span class="sxs-lookup"><span data-stu-id="8dd55-103">Troubleshooting Azure Windows VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="8dd55-104">De Extensiestatus van weergeven</span><span class="sxs-lookup"><span data-stu-id="8dd55-104">Viewing extension status</span></span>
<span data-ttu-id="8dd55-105">Azure Resource Manager-sjablonen kunnen in Azure PowerShell worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8dd55-105">Azure Resource Manager templates can be executed from Azure PowerShell.</span></span> <span data-ttu-id="8dd55-106">Nadat de sjabloon die wordt uitgevoerd, kan de status van de extensie van Azure Resource Explorer of de opdrachtregel-hulpprogramma's worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8dd55-106">Once the template is executed, the extension status can be viewed from Azure Resource Explorer or the command line tools.</span></span>

<span data-ttu-id="8dd55-107">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8dd55-107">Here is an example:</span></span>

<span data-ttu-id="8dd55-108">Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8dd55-108">Azure PowerShell:</span></span>

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

<span data-ttu-id="8dd55-109">Hier volgt een voorbeeld van uitvoer:</span><span class="sxs-lookup"><span data-stu-id="8dd55-109">Here is the sample output:</span></span>

      Extensions:  {
      "ExtensionType": "Microsoft.Compute.CustomScriptExtension",
      "Name": "myCustomScriptExtension",
      "SubStatuses": [
        {
          "Code": "ComponentStatus/StdOut/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "    Directory: C:\\temp\\n\\n\\nMode                LastWriteTime     Length Name
              \\n----                -------------     ------ ----                              \\n-a---          9/1/2015   2:03 AM         11
              test.txt                          \\n\\n",
                      "Time": null
          },
        {
          "Code": "ComponentStatus/StdErr/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "",
          "Time": null
        }
    }
  <span data-ttu-id="8dd55-110">]</span><span class="sxs-lookup"><span data-stu-id="8dd55-110">]</span></span>

## <a name="troubleshooting-extension-failures"></a><span data-ttu-id="8dd55-111">Het extensie-fouten oplossen</span><span class="sxs-lookup"><span data-stu-id="8dd55-111">Troubleshooting extension failures</span></span>
### <a name="re-running-the-extension-on-the-vm"></a><span data-ttu-id="8dd55-112">De uitbreiding opnieuw uit te voeren op de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="8dd55-112">Re-running the extension on the VM</span></span>
<span data-ttu-id="8dd55-113">Als u scripts op de virtuele machine met behulp van de aangepaste Scriptextensie, kan het soms uitvoeren in een fout waarbij VM is gemaakt, maar het script is mislukt.</span><span class="sxs-lookup"><span data-stu-id="8dd55-113">If you are running scripts on the VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but the script has failed.</span></span> <span data-ttu-id="8dd55-114">Onder deze voorwaarden is de aanbevolen manier om deze fout herstellen voor het verwijderen van de extensie en voert u de sjabloon opnieuw.</span><span class="sxs-lookup"><span data-stu-id="8dd55-114">Under these conditons, the recommended way to recover from this error is to remove the extension and rerun the template again.</span></span>
<span data-ttu-id="8dd55-115">Opmerking: In de toekomst deze functionaliteit zou worden uitgebreid om te verwijderen van de noodzaak voor het verwijderen van de extensie.</span><span class="sxs-lookup"><span data-stu-id="8dd55-115">Note: In future, this functionality would be enhanced to remove the need for uninstalling the extension.</span></span>

#### <a name="remove-the-extension-from-azure-powershell"></a><span data-ttu-id="8dd55-116">Verwijder de extensie van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8dd55-116">Remove the extension from Azure PowerShell</span></span>
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

<span data-ttu-id="8dd55-117">Wanneer de uitbreiding is verwijderd, is de sjabloon kan worden opnieuw uitgevoerd voor het uitvoeren van de scripts op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8dd55-117">Once the extension has been removed, the template can be re-executed to run the scripts on the VM.</span></span>

