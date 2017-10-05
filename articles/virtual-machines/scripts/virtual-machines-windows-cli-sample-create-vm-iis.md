---
title: Azure CLI-voorbeeldscript - Installeer IIS | Microsoft Docs
description: Azure CLI-voorbeeldscript - Installeer IIS
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/28/2017
ms.author: nepeters
ms.openlocfilehash: 426418c01b23845372443af5b8f4e826fb321f7d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="quick-create-a-virtual-machine-with-the-azure-cli"></a>Snel een virtuele machine maken met de Azure CLI

Dit script maakt een Azure-virtuele Machine met Windows Server 2016 en de aangepaste Scriptextensie voor Azure virtuele Machine gebruikt voor het installeren van IIS. Nadat het script is uitgevoerd, kunt u toegang tot de standaardwebsite van IIS op het openbare IP-adres van de virtuele machine.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/virtual-machine/create-vm-windows-iis/create-vm-windows-iis.sh "snelle VM maken")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, virtuele machine en alle gerelateerde resources. Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ vm maken](https://docs.microsoft.com/cli/azure/vm#create) | De virtuele machine maakt en met de netwerkkaart, virtueel netwerk, subnet en netwerkbeveiligingsgroep is verbonden. Deze opdracht geeft ook aan de installatiekopie van de virtuele machine om te worden gebruikt en administratieve referenties.  |
| [AZ vm open-poort](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Maakt een groep van de netwerkbeveiligingsregel dat binnenkomend verkeer toegestaan. In dit voorbeeld wordt is poort 80 geopend voor HTTP-verkeer. |
| [Azure vm-extensie instellen](https://docs.microsoft.com/cli/azure/vm/extension#set) | Wordt toegevoegd en wordt de extensie van een virtuele machine naar een virtuele machine wordt uitgevoerd. In dit voorbeeld wordt de extensie voor aangepaste scripts worden gebruikt om IIS te installeren.|
| [AZ groep verwijderen](https://docs.microsoft.com/cli/azure/vm/extension#set) | Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra virtuele machine CLI scriptvoorbeelden vindt u in de [virtuele machine van Windows Azure-documentatie](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
