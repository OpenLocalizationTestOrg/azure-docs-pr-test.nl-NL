---
title: aaaAzure voorbeeldscript CLI - ACS Windows Kubernetes Cluster maken | Microsoft Docs
description: Azure CLI Sample Script - ACS Windows Kubernetes Cluster maken
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: nepeters
ms.openlocfilehash: ace2f7a6dcd3ab02b61217766f4774cddbe8828b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-container-service-kubernetes-windows-cluster"></a>Een Azure Container Service Kubernetes Windows-Cluster maken

In dit voorbeeld wordt een Azure Container Service-cluster met Kubernetes voor Windows op basis van containers.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type kubernetes \
  --resource-group myResourceGroup \
  --name myK8SCluster \
  --generate-ssh-keys \
  --admin-username azureuser \
  --admin-password Password12 \
  --windows
```

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten toocreate Hallo implementatie te volgen. Elk item in de tabel Hallo koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ acs maken](https://docs.microsoft.com/cli/azure/acs#create) | Maakt en ACS-cluster. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra Azure Container Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Container Service documentatie](../cli-samples.md).
