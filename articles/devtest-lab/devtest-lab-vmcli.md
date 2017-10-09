---
title: aaaCreate en beheren van virtuele machines in DevTest Labs met Azure CLI | Microsoft Docs
description: Meer informatie over hoe toouse Azure DevTest Labs toocreate en beheren van virtuele machines met Azure CLI 2.0
services: devtest-lab,virtual-machines
documentationcenter: na
author: lisawong19
manager: douge
editor: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: liwong
ms.openlocfilehash: 98ea3aa7b2489bff61971573aaf584984cd811e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-hello-azure-cli"></a><span data-ttu-id="94005-103">Maken en beheren van virtuele machines met DevTest Labs hello Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="94005-103">Create and manage virtual machines with DevTest Labs using hello Azure CLI</span></span>
<span data-ttu-id="94005-104">Deze snel starten begeleidt u bij het maken, starten, verbinding te maken, bijwerken en een ontwikkelcomputer in uw testomgeving opruimen.</span><span class="sxs-lookup"><span data-stu-id="94005-104">This quick start will guide you through creating, starting, connecting, updating and cleaning up a development machine in your lab.</span></span> 

<span data-ttu-id="94005-105">Voordat u begint:</span><span class="sxs-lookup"><span data-stu-id="94005-105">Before you begin:</span></span>

* <span data-ttu-id="94005-106">Als een lab niet gemaakt is, vindt u instructies [hier](devtest-lab-create-lab.md).</span><span class="sxs-lookup"><span data-stu-id="94005-106">If a lab has not been created, instructions can be found [here](devtest-lab-create-lab.md).</span></span>

* <span data-ttu-id="94005-107">[CLI 2.0 installeren](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="94005-107">[Install CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="94005-108">toostart, voer az aanmelding toocreate een verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="94005-108">toostart, run az login toocreate a connection with Azure.</span></span> 

## <a name="create-and-verify-hello-virtual-machine"></a><span data-ttu-id="94005-109">Maken en controleer of Hallo virtuele machine</span><span class="sxs-lookup"><span data-stu-id="94005-109">Create and verify hello virtual machine</span></span> 
<span data-ttu-id="94005-110">Een virtuele machine maken vanuit een marketplace-installatiekopie met ssh verificatie.</span><span class="sxs-lookup"><span data-stu-id="94005-110">Create a VM from a marketplace image with ssh authentication.</span></span>
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> <span data-ttu-id="94005-111">Hallo plaatsen **lab van resourcegroep** naam in Hallo--resourcegroep parameter.</span><span class="sxs-lookup"><span data-stu-id="94005-111">Put hello **lab's resource group** name in hello --resource-group parameter.</span></span>
>

<span data-ttu-id="94005-112">Als u op een virtuele machine met een formule toocreate wilt, gebruikt u Hallo--formule parameter in [az lab vm maken](https://docs.microsoft.com/cli/azure/lab/vm#create).</span><span class="sxs-lookup"><span data-stu-id="94005-112">If you want toocreate a VM using a formula, use hello --formula parameter in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>


<span data-ttu-id="94005-113">Controleer of dat deze Hallo VM beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="94005-113">Verify that hello VM is available.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand 'properties($expand=ComputeVm,NetworkInterface)' --query '{status: computeVm.statuses[0].displayStatus, fqdn: fqdn, ipAddress: networkInterface.publicIpAddress}'
```
```json
{
  "fqdn": "lisalabvm.southcentralus.cloudapp.azure.com",
  "ipAddress": "13.85.228.112",
  "status": "Provisioning succeeded"
}
```

## <a name="start-and-connect-toohello-virtual-machine"></a><span data-ttu-id="94005-114">Start en verbinding toohello virtuele machine</span><span class="sxs-lookup"><span data-stu-id="94005-114">Start and connect toohello virtual machine</span></span>
<span data-ttu-id="94005-115">Een virtuele machine start.</span><span class="sxs-lookup"><span data-stu-id="94005-115">Start a VM.</span></span>
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> <span data-ttu-id="94005-116">Hallo plaatsen **lab van resourcegroep** naam in Hallo--resourcegroep parameter.</span><span class="sxs-lookup"><span data-stu-id="94005-116">Put hello **lab's resource group** name in hello --resource-group parameter.</span></span>
>

<span data-ttu-id="94005-117">Verbinding maken met tooa VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) of [extern bureaublad](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="94005-117">Connect tooa VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) or [Remote Desktop](../virtual-machines/windows/connect-logon.md).</span></span>
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-hello-virtual-machine"></a><span data-ttu-id="94005-118">Hallo virtuele machine bijwerken</span><span class="sxs-lookup"><span data-stu-id="94005-118">Update hello virtual machine</span></span>
<span data-ttu-id="94005-119">Toepassing artefacten tooa VM.</span><span class="sxs-lookup"><span data-stu-id="94005-119">Apply artifacts tooa VM.</span></span>
```azurecli
az lab vm apply-artifacts --lab-name  sampleLabName --name sampleVMName  --resource-group sampleResourceGroup  --artifacts @/artifacts.json
```

```json
[
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-java",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-install-nodejs",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-apt-package",
    "parameters": [
      {
        "name": "packages",
        "value": "abcd"
      },
      {
        "name": "update",
        "value": "true"
      },
      {
        "name": "options",
        "value": ""
      }
    ]
  } 
]
```

<span data-ttu-id="94005-120">Lijst met artefacten beschikbaar in Hallo lab.</span><span class="sxs-lookup"><span data-stu-id="94005-120">List artifacts available in hello lab.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-hello-virtual-machine"></a><span data-ttu-id="94005-121">Stop en Hallo virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="94005-121">Stop and delete hello virtual machine</span></span>    
<span data-ttu-id="94005-122">Een virtuele machine stoppen.</span><span class="sxs-lookup"><span data-stu-id="94005-122">Stop a VM.</span></span>
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

<span data-ttu-id="94005-123">Verwijderen van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="94005-123">Delete a VM.</span></span>
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]