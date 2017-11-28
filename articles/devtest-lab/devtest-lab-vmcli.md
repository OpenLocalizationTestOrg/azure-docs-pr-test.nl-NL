---
title: Maken en beheren van virtuele machines in DevTest Labs met Azure CLI | Microsoft Docs
description: Informatie over het gebruik van Azure DevTest Labs maken en beheren van virtuele machines met Azure CLI 2.0
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
ms.openlocfilehash: 42b0448c1bcdfa909715abd5075353d63cab8389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-the-azure-cli"></a><span data-ttu-id="0921d-103">Maken en beheren van virtuele machines met DevTest Labs met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0921d-103">Create and manage virtual machines with DevTest Labs using the Azure CLI</span></span>
<span data-ttu-id="0921d-104">Deze snel starten begeleidt u bij het maken, starten, verbinding te maken, bijwerken en een ontwikkelcomputer in uw testomgeving opruimen.</span><span class="sxs-lookup"><span data-stu-id="0921d-104">This quick start will guide you through creating, starting, connecting, updating and cleaning up a development machine in your lab.</span></span> 

<span data-ttu-id="0921d-105">Voordat u begint:</span><span class="sxs-lookup"><span data-stu-id="0921d-105">Before you begin:</span></span>

* <span data-ttu-id="0921d-106">Als een lab niet gemaakt is, vindt u instructies [hier](devtest-lab-create-lab.md).</span><span class="sxs-lookup"><span data-stu-id="0921d-106">If a lab has not been created, instructions can be found [here](devtest-lab-create-lab.md).</span></span>

* <span data-ttu-id="0921d-107">[CLI 2.0 installeren](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0921d-107">[Install CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="0921d-108">Als u wilt starten, az aanmelding voor het maken van een verbinding met Azure worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0921d-108">To start, run az login to create a connection with Azure.</span></span> 

## <a name="create-and-verify-the-virtual-machine"></a><span data-ttu-id="0921d-109">Maken en controleer of de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="0921d-109">Create and verify the virtual machine</span></span> 
<span data-ttu-id="0921d-110">Een virtuele machine maken vanuit een marketplace-installatiekopie met ssh verificatie.</span><span class="sxs-lookup"><span data-stu-id="0921d-110">Create a VM from a marketplace image with ssh authentication.</span></span>
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> <span data-ttu-id="0921d-111">Plaats de **lab van resourcegroep** naam in de--resourcegroep parameter.</span><span class="sxs-lookup"><span data-stu-id="0921d-111">Put the **lab's resource group** name in the --resource-group parameter.</span></span>
>

<span data-ttu-id="0921d-112">Als u wilt maken van een virtuele machine met een formule, gebruik de parameter van de--formule in [az lab vm maken](https://docs.microsoft.com/cli/azure/lab/vm#create).</span><span class="sxs-lookup"><span data-stu-id="0921d-112">If you want to create a VM using a formula, use the --formula parameter in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>


<span data-ttu-id="0921d-113">Controleer of de virtuele machine beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="0921d-113">Verify that the VM is available.</span></span>
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

## <a name="start-and-connect-to-the-virtual-machine"></a><span data-ttu-id="0921d-114">Start en verbinding met de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="0921d-114">Start and connect to the virtual machine</span></span>
<span data-ttu-id="0921d-115">Een virtuele machine start.</span><span class="sxs-lookup"><span data-stu-id="0921d-115">Start a VM.</span></span>
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> <span data-ttu-id="0921d-116">Plaats de **lab van resourcegroep** naam in de--resourcegroep parameter.</span><span class="sxs-lookup"><span data-stu-id="0921d-116">Put the **lab's resource group** name in the --resource-group parameter.</span></span>
>

<span data-ttu-id="0921d-117">Verbinding maken met een virtuele machine: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) of [extern bureaublad](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="0921d-117">Connect to a VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) or [Remote Desktop](../virtual-machines/windows/connect-logon.md).</span></span>
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-the-virtual-machine"></a><span data-ttu-id="0921d-118">De virtuele machine bijwerken</span><span class="sxs-lookup"><span data-stu-id="0921d-118">Update the virtual machine</span></span>
<span data-ttu-id="0921d-119">Artefacten toepassen op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0921d-119">Apply artifacts to a VM.</span></span>
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

<span data-ttu-id="0921d-120">Lijst met artefacten is beschikbaar in de testomgeving.</span><span class="sxs-lookup"><span data-stu-id="0921d-120">List artifacts available in the lab.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-the-virtual-machine"></a><span data-ttu-id="0921d-121">Stoppen en verwijderen van de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="0921d-121">Stop and delete the virtual machine</span></span>    
<span data-ttu-id="0921d-122">Een virtuele machine stoppen.</span><span class="sxs-lookup"><span data-stu-id="0921d-122">Stop a VM.</span></span>
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

<span data-ttu-id="0921d-123">Verwijderen van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0921d-123">Delete a VM.</span></span>
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]