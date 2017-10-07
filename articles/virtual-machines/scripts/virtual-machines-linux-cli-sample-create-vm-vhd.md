---
title: aaaAzure voorbeeldscript CLI - een virtuele machine maken met een VHD | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: een virtuele machine maken met een virtuele harde schijf.'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a>Een virtuele machine met een virtuele harde schijf maken

In dit voorbeeld maakt een VHD met een virtuele machine.
Het maakt een resourcegroep, een opslagaccount en een container en een virtuele machine wordt gemaakt door het uploaden van Hallo VHD toohello container.
Vervangt Hallo ssh openbare sleutel met de openbare sleutel, zodat u toegang toohello VM hebt.

U moet een opstartbare VHD.
U kunt downloaden Hallo VHD die wordt gebruikt vanuit https://azclisamples.blob.core.windows.net/vhds/sample.vhd of uw eigen VHD gebruiken. Hallo script zoekt `~/sample.vhd`.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, virtuele machine, beschikbaarheidsset, load balancer en alle gerelateerde resources te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [lijst met opslagaccounts AZ](https://docs.microsoft.com/cli/azure/storage/account#list) | Een lijst met storage-accounts |
| [AZ opslag Controleer accountnaam](https://docs.microsoft.com/cli/azure/storage/account#check-name) | Controleert of de naam van een account geldig is en nog niet bestaat |
| [lijst met opslagaccounts die sleutels AZ](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | Een lijst met sleutels voor opslagaccounts Hallo |
| [AZ storage-blob bestaat](https://docs.microsoft.com/cli/azure/storage/blob#exists) | Controleert of Hallo blob bestaat |
| [AZ storage-container maken](https://docs.microsoft.com/cli/azure/storage/container#create) | Maakt een container in een opslagaccount. |
| [uploaden van blob storage AZ](https://docs.microsoft.com/cli/azure/storage/blob#upload) | Hiermee maakt een blob in Hallo-container door uploaden Hallo VHD. |
| [AZ vm lijst](https://docs.microsoft.com/cli/azure/vm#list) | Gebruikt met `--query` controleren of de naam van de VM Hallo in gebruik is. | 
| [AZ vm maken](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Hallo virtuele machines maakt. |
| [AZ vm toegang set-linux-gebruikers](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | Hiermee stelt u Hallo SSH sleutel toogive Hallo huidige gebruiker toegang toohello VM. |
| [AZ vm lijst-ip-adressen](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Hiermee haalt u Hallo IP-adres van Hallo VM die is gemaakt. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
