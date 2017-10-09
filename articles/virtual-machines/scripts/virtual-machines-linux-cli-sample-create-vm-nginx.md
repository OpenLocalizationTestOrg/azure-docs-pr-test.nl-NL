---
title: aaaAzure voorbeeldscript CLI - Maak een Linux-VM met NGINX | Microsoft Docs
description: Azure CLI Script voorbeeld - een virtuele Linux-machine maken met NGINX
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9166ccfd4f2e6eea731a8dc6956575d9f8f85488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-nginx"></a>Een virtuele machine maken met NGINX

Dit script maakt van een virtuele Machine van Azure en hello Azure virtuele Machine aangepaste Scriptextensie tooinstall NGINX gebruikt. Na het uitvoeren van script hello, kunt u toegang tot een demo-website op Hallo openbare IP-adres van Hallo virtuele machine.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a>Aangepaste scriptextensie

Hallo-extensie voor aangepaste scripts kopieert u dit script op Hallo virtuele machine. Hallo script vervolgens tooinstall wordt uitgevoerd en een NGINX-webserver configureren. 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt Hallo opdrachten toocreate een resourcegroep of virtuele machine te volgen en alle bijbehorende resources. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ vm maken](https://docs.microsoft.com/cli/azure/vm#create) | Hallo virtuele machine maakt. Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.  |
| [AZ vm open-poort](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Hiermee maakt u een netwerk beveiliging groep regel tooallow binnenkomend verkeer. In dit voorbeeld wordt is poort 80 geopend voor HTTP-verkeer. |
| [Azure vm-extensie instellen](https://docs.microsoft.com/cli/azure/vm/extension#set) | Wordt toegevoegd en wordt een virtuele machine extensie tooa VM wordt uitgevoerd. In dit voorbeeld is de aangepaste scriptextensie Hallo gebruikte tooinstall NGINX.|
| [AZ groep verwijderen](https://docs.microsoft.com/cli/azure/vm/extension#set) | Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
