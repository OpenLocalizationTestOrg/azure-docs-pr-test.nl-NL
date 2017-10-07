---
title: aaaTroubleshooting Windows VM-extensie fouten | Microsoft Docs
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
ms.openlocfilehash: d24544743d9e0cb1a68ec9ab7718716f918054f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a><span data-ttu-id="37839-103">Virtuele machine van Windows Azure-extensie fouten oplossen</span><span class="sxs-lookup"><span data-stu-id="37839-103">Troubleshooting Azure Windows VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="37839-104">De Extensiestatus van weergeven</span><span class="sxs-lookup"><span data-stu-id="37839-104">Viewing extension status</span></span>
<span data-ttu-id="37839-105">Azure Resource Manager-sjablonen kunnen in Azure PowerShell worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="37839-105">Azure Resource Manager templates can be executed from Azure PowerShell.</span></span> <span data-ttu-id="37839-106">Zodra het Hallo-sjabloon wordt uitgevoerd, kan status van de extensie Hallo van Azure Resource Explorer of Hallo opdrachtregel-hulpprogramma's worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="37839-106">Once hello template is executed, hello extension status can be viewed from Azure Resource Explorer or hello command line tools.</span></span>

<span data-ttu-id="37839-107">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="37839-107">Here is an example:</span></span>

<span data-ttu-id="37839-108">Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="37839-108">Azure PowerShell:</span></span>

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

<span data-ttu-id="37839-109">Hier volgt voorbeelduitvoer Hallo:</span><span class="sxs-lookup"><span data-stu-id="37839-109">Here is hello sample output:</span></span>

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
  <span data-ttu-id="37839-110">]</span><span class="sxs-lookup"><span data-stu-id="37839-110">]</span></span>

## <a name="troubleshooting-extension-failures"></a><span data-ttu-id="37839-111">Het extensie-fouten oplossen</span><span class="sxs-lookup"><span data-stu-id="37839-111">Troubleshooting extension failures</span></span>
### <a name="re-running-hello-extension-on-hello-vm"></a><span data-ttu-id="37839-112">Hallo-uitbreiding opnieuw uit te voeren op Hallo VM</span><span class="sxs-lookup"><span data-stu-id="37839-112">Re-running hello extension on hello VM</span></span>
<span data-ttu-id="37839-113">Als u scripts op Hallo VM die gebruikmaakt van de aangepaste Scriptextensie uitvoert, kunt u soms uitvoeren in een fout waarbij VM is gemaakt maar Hallo-script is mislukt.</span><span class="sxs-lookup"><span data-stu-id="37839-113">If you are running scripts on hello VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but hello script has failed.</span></span> <span data-ttu-id="37839-114">Onder deze voorwaarden Hallo aanbevolen manier toorecover van deze fout is tooremove Hallo uitbreiding en voert u Hallo sjabloon opnieuw.</span><span class="sxs-lookup"><span data-stu-id="37839-114">Under these conditons, hello recommended way toorecover from this error is tooremove hello extension and rerun hello template again.</span></span>
<span data-ttu-id="37839-115">Opmerking: In de toekomst wordt deze functionaliteit zou worden uitgebreide tooremove nodig voor het verwijderen van extensie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="37839-115">Note: In future, this functionality would be enhanced tooremove hello need for uninstalling hello extension.</span></span>

#### <a name="remove-hello-extension-from-azure-powershell"></a><span data-ttu-id="37839-116">Hallo-uitbreiding uit Azure PowerShell verwijderen</span><span class="sxs-lookup"><span data-stu-id="37839-116">Remove hello extension from Azure PowerShell</span></span>
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

<span data-ttu-id="37839-117">Zodra het Hallo-extensie is verwijderd, kan Hallo sjabloon opnieuw uitgevoerd toorun Hallo scripts op Hallo VM zijn.</span><span class="sxs-lookup"><span data-stu-id="37839-117">Once hello extension has been removed, hello template can be re-executed toorun hello scripts on hello VM.</span></span>

