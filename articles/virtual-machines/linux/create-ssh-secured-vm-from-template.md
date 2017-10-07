---
title: aaaCreate een Linux VM in Azure uit een sjabloon | Microsoft Docs
description: Hoe toouse hello Azure CLI 2.0 toocreate een Linux-VM met een Resource Manager-sjabloon
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a>Hoe toocreate virtuele Linux-machine met Azure Resource Manager-sjablonen
Dit artikel laat zien hoe tooquickly virtuele Linux-machine (VM) met Azure Resource Manager-sjablonen en hello Azure CLI 2.0 implementeren. U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).


## <a name="templates-overview"></a>Overzicht van sjablonen
Azure Resource Manager-sjablonen zijn JSON-bestanden die Hallo-infrastructuur en configuratie van uw Azure-oplossing te definiëren. Door het gebruik van een sjabloon kunt u gedurende de levenscyclus de oplossing herhaaldelijk implementeren en erop vertrouwen dat uw resources consistent worden geïmplementeerd. toolearn meer informatie over het Hallo-indeling van het Hallo-sjabloon en de manier waarop u samenstelt, Zie [maken van uw eerste Azure Resource Manager-sjabloon](../../azure-resource-manager/resource-manager-create-first-template.md). tooview hello JSON-syntaxis voor de typen resources, Zie [resources in Azure Resource Manager-sjablonen definiëren](/azure/templates/).


## <a name="create-resource-group"></a>Een resourcegroep maken
Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd. Een resourcegroep moet worden gemaakt voordat een virtuele machine. Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupVM* in Hallo *eastus* regio:

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Virtuele machine maken
Hallo volgende voorbeeld wordt een virtuele machine uit [deze Azure Resource Manager-sjabloon](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) met [az implementatie maken](/cli/azure/group/deployment#create). Geef een waarde van uw eigen openbare SSH-sleutel, zoals de inhoud van Hallo Hallo *~/.ssh/id_rsa.pub*. Als u een SSH-sleutelpaar toocreate nodig hebt, raadpleegt u [hoe toocreate en gebruikt een SSH sleutelpaar voor virtuele Linux-machines in Azure](mac-create-ssh-keys.md).

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

In dit voorbeeld moet u een sjabloon die is opgeslagen in GitHub opgegeven. U kunt ook downloaden of een sjabloon maken en geef het lokale pad Hallo Hello dezelfde `--template-file` parameter.

tooSSH tooyour VM, verkrijgen Hallo openbare IP-adres met [az netwerk openbare ip-weergeven](/cli/azure/network/public-ip#show):

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

U kunt vervolgens SSH tooyour VM als normale:

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a>Volgende stappen
In dit voorbeeld moet u een basis Linux VM gemaakt. Ga voor meer Resource Manager-sjablonen die complexere omgevingen maken of toepassingsframeworks bevatten, Hallo [Azure-sjablonen snelstartgalerie](https://azure.microsoft.com/documentation/templates/).
