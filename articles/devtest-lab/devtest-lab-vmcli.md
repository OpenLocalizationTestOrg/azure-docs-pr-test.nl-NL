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
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-hello-azure-cli"></a>Maken en beheren van virtuele machines met DevTest Labs hello Azure CLI gebruiken
Deze snel starten begeleidt u bij het maken, starten, verbinding te maken, bijwerken en een ontwikkelcomputer in uw testomgeving opruimen. 

Voordat u begint:

* Als een lab niet gemaakt is, vindt u instructies [hier](devtest-lab-create-lab.md).

* [CLI 2.0 installeren](https://docs.microsoft.com/cli/azure/install-azure-cli). toostart, voer az aanmelding toocreate een verbinding met Azure. 

## <a name="create-and-verify-hello-virtual-machine"></a>Maken en controleer of Hallo virtuele machine 
Een virtuele machine maken vanuit een marketplace-installatiekopie met ssh verificatie.
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> Hallo plaatsen **lab van resourcegroep** naam in Hallo--resourcegroep parameter.
>

Als u op een virtuele machine met een formule toocreate wilt, gebruikt u Hallo--formule parameter in [az lab vm maken](https://docs.microsoft.com/cli/azure/lab/vm#create).


Controleer of dat deze Hallo VM beschikbaar is.
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

## <a name="start-and-connect-toohello-virtual-machine"></a>Start en verbinding toohello virtuele machine
Een virtuele machine start.
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> Hallo plaatsen **lab van resourcegroep** naam in Hallo--resourcegroep parameter.
>

Verbinding maken met tooa VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) of [extern bureaublad](../virtual-machines/windows/connect-logon.md).
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-hello-virtual-machine"></a>Hallo virtuele machine bijwerken
Toepassing artefacten tooa VM.
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

Lijst met artefacten beschikbaar in Hallo lab.
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-hello-virtual-machine"></a>Stop en Hallo virtuele machine verwijderen    
Een virtuele machine stoppen.
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

Verwijderen van een virtuele machine.
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]