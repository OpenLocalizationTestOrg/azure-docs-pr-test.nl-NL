---
title: Azure CLI Sample Script - versleutelen van een Windows VM | Microsoft Docs
description: Azure CLI Sample Script - versleutelen van een Windows VM
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 9574d779982c939aa970cd4bdf7df6e66793e3b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-a-windows-virtual-machine-in-azure"></a>Versleutelen van een virtuele Windows-machine in Azure

Dit script maakt een beveiligde Azure Sleutelkluis, versleutelingssleutels, Azure Active Directory service-principal en virtuele Windows-machine (VM). De virtuele machine wordt vervolgens versleuteld met behulp van de versleutelingssleutel van de Sleutelkluis en service principal referenties.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_windows_vm.sh "versleutelen VM-schijven")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, Azure Sleutelkluis, service-principal, virtuele machine en alle gerelateerde resources. Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ keyvault maken](https://docs.microsoft.com/cli/azure/keyvault#create) | Hiermee maakt u een Azure Key Vault voor het opslaan van beveiligde gegevens, zoals versleutelingssleutels. |
| [AZ keyvault-sleutel maken](https://docs.microsoft.com/cli/azure/keyvault/key#create) | Maakt een versleutelingssleutel in de Sleutelkluis. |
| [AZ ad sp maken-voor-rbac](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | Maakt een Azure Active Directory service-principal veilig verifiëren en toegang tot de versleutelingssleutels. |
| [AZ keyvault-beleid instellen](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Stelt de machtigingen op de Sleutelkluis de service principal toegang verlenen tot versleutelingssleutels. |
| [AZ vm maken](https://docs.microsoft.com/cli/azure/vm#create) | De virtuele machine maakt en met de netwerkkaart, virtueel netwerk, subnet en NSG is verbonden. Met deze opdracht geeft ook de afbeelding van de virtuele machine moet worden gebruikt en de beheerdersreferenties.  |
| [AZ vm-codering inschakelen](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | Hiermee schakelt u versleuteling op een virtuele machine met behulp van de service principal referenties en de versleutelingssleutel. |
| [AZ vm versleuteling weergeven](https://docs.microsoft.com/cli/azure/vm/encryption#show) | Toont de status van het VM-versleutelingsproces. |
| [AZ groep verwijderen](https://docs.microsoft.com/cli/azure/vm/extension#set) | Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra virtuele machine CLI scriptvoorbeelden vindt u in de [virtuele machine van Windows Azure-documentatie](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).
