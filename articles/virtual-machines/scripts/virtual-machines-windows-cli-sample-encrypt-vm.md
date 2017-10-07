---
title: aaaAzure voorbeeldscript CLI - versleutelen van een virtuele machine van Windows | Microsoft Docs
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
ms.openlocfilehash: 7a9928467f818cd5358d3d19bff5129d8fa21313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-in-azure"></a>Versleutelen van een virtuele Windows-machine in Azure

Dit script maakt een beveiligde Azure Sleutelkluis, versleutelingssleutels, Azure Active Directory service-principal en virtuele Windows-machine (VM). Hallo VM wordt vervolgens versleuteld met de versleutelingssleutel Hallo van Sleutelkluis en de service principal referenties.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_windows_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt Hallo opdrachten toocreate na een resource groep Azure Key Vault service principal, virtuele machine, en alle bijbehorende resources. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ keyvault maken](https://docs.microsoft.com/cli/azure/keyvault#create) | Hiermee maakt u een beveiligde gegevens van Azure Sleutelkluis toostore zoals versleutelingssleutels. |
| [AZ keyvault-sleutel maken](https://docs.microsoft.com/cli/azure/keyvault/key#create) | Maakt een versleutelingssleutel in de Sleutelkluis. |
| [AZ ad sp maken-voor-rbac](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | Hiermee maakt u een Azure Active Directory-service principal toosecurely verifiëren en toegang tooencryption sleutels beheren. |
| [AZ keyvault-beleid instellen](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Machtigingen op Hallo Sleutelkluis toogrant Hallo service principal tooencryption toegangstoetsen ingesteld. |
| [AZ vm maken](https://docs.microsoft.com/cli/azure/vm#create) | Hallo virtuele machine maakt en toohello netwerkkaart, virtueel netwerk, subnet en NSG is verbonden. Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.  |
| [AZ vm-codering inschakelen](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | Hiermee schakelt u versleuteling op een virtuele machine met behulp van de principal Servicereferenties Hallo en versleutelingssleutel. |
| [AZ vm versleuteling weergeven](https://docs.microsoft.com/cli/azure/vm/encryption#show) | Geeft de status Hallo Hallo versleutelingsproces VM. |
| [AZ groep verwijderen](https://docs.microsoft.com/cli/azure/vm/extension#set) | Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).
