---
title: aaaTroubleshooting Linux VM extensie fouten | Microsoft Docs
description: Meer informatie over het oplossen van fouten van Azure Linux VM-extensie
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: f05d93f3-42fc-4a09-9798-d92f7929c417
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 29a0ca34207421e0014380000a313d3c44e7e594
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a><span data-ttu-id="08d43-103">Azure Linux VM-extensie fouten oplossen</span><span class="sxs-lookup"><span data-stu-id="08d43-103">Troubleshooting Azure Linux VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="08d43-104">De Extensiestatus van weergeven</span><span class="sxs-lookup"><span data-stu-id="08d43-104">Viewing extension status</span></span>
<span data-ttu-id="08d43-105">Azure Resource Manager-sjablonen worden uitgevoerd vanaf hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="08d43-105">Azure Resource Manager templates can be executed from hello  Azure CLI.</span></span> <span data-ttu-id="08d43-106">Zodra het Hallo-sjabloon wordt uitgevoerd, kan status van de extensie Hallo van Azure Resource Explorer of Hallo opdrachtregel-hulpprogramma's worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="08d43-106">Once hello template is executed, hello extension status can be viewed from Azure Resource Explorer or hello command line tools.</span></span>

<span data-ttu-id="08d43-107">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="08d43-107">Here is an example:</span></span>

<span data-ttu-id="08d43-108">Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="08d43-108">Azure CLI:</span></span>

      azure vm get-instance-view


<span data-ttu-id="08d43-109">Hier volgt voorbeelduitvoer Hallo:</span><span class="sxs-lookup"><span data-stu-id="08d43-109">Here is hello sample output:</span></span>

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
  <span data-ttu-id="08d43-110">]</span><span class="sxs-lookup"><span data-stu-id="08d43-110">]</span></span>

## <a name="troubleshooting-extenson-failures"></a><span data-ttu-id="08d43-111">Voor probleemoplossing Extenson fouten:</span><span class="sxs-lookup"><span data-stu-id="08d43-111">Troubleshooting Extenson failures:</span></span>
### <a name="re-running-hello-extension-on-hello-vm"></a><span data-ttu-id="08d43-112">Hallo-uitbreiding opnieuw uit te voeren op Hallo VM</span><span class="sxs-lookup"><span data-stu-id="08d43-112">Re-running hello extension on hello VM</span></span>
<span data-ttu-id="08d43-113">Als u scripts op Hallo VM die gebruikmaakt van de aangepaste Scriptextensie uitvoert, kunt u soms uitvoeren in een fout waarbij VM is gemaakt maar Hallo-script is mislukt.</span><span class="sxs-lookup"><span data-stu-id="08d43-113">If you are running scripts on hello VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but hello script has failed.</span></span> <span data-ttu-id="08d43-114">Onder deze voorwaarden Hallo aanbevolen manier toorecover van deze fout is tooremove Hallo uitbreiding en voert u Hallo sjabloon opnieuw.</span><span class="sxs-lookup"><span data-stu-id="08d43-114">Under these conditons, hello recommended way toorecover from this error is tooremove hello extension and rerun hello template again.</span></span>
<span data-ttu-id="08d43-115">Opmerking: In de toekomst wordt deze functionaliteit zou worden uitgebreide tooremove nodig voor het verwijderen van extensie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="08d43-115">Note: In future, this functionality would be enhanced tooremove hello need for uninstalling hello extension.</span></span>

#### <a name="remove-hello-extension-from-azure-cli"></a><span data-ttu-id="08d43-116">Hallo-uitbreiding uit Azure CLI verwijderen</span><span class="sxs-lookup"><span data-stu-id="08d43-116">Remove hello extension from Azure CLI</span></span>
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

<span data-ttu-id="08d43-117">Waarbij 'publsher-name' komt overeen toohello extensietype van Hallo-uitvoer van 'get-exemplaar-weergave van de azure vm' en is de naam Hallo van Hallo extensie resource van Hallo-sjabloon</span><span class="sxs-lookup"><span data-stu-id="08d43-117">Where "publsher-name" corresponds toohello extension type from hello output of "azure vm get-instance-view" and name is hello name of hello extension resource from hello template</span></span>

<span data-ttu-id="08d43-118">Zodra het Hallo-extensie is verwijderd, kan Hallo sjabloon opnieuw uitgevoerd toorun Hallo scripts op Hallo VM zijn.</span><span class="sxs-lookup"><span data-stu-id="08d43-118">Once hello extension has been removed, hello template can be re-executed toorun hello scripts on hello VM.</span></span>

