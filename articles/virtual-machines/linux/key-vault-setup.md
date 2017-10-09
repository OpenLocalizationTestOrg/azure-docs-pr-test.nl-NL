---
title: aaaSet van Azure Sleutelkluis voor virtuele Linux-machines | Microsoft Docs
description: Hoe Hallo tooset up Sleutelkluis voor gebruik met een virtuele machine van Azure Resource Manager met CLI 2.0.
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: a5dc1fbe59a71b4456ba5b9bbacdb90440064757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a>Hoe tooset up Sleutelkluis voor virtuele machines met Azure CLI 2.0 Hallo

In Azure Resource Manager-stack hello, worden geheimen/certificaten gemodelleerd als resources die worden geleverd door de Sleutelkluis. Zie toolearn meer informatie over Azure Key Vault [wat is Azure Sleutelkluis?](../../key-vault/key-vault-whatis.md) Hallo in volgorde voor Sleutelkluis toobe gebruikt met virtuele machines van Azure Resource Manager *EnabledForDeployment* eigenschap op Sleutelkluis tootrue moet worden ingesteld. Dit artikel ziet u hoe tooset up Sleutelkluis voor gebruik met virtuele Azure-machines (VM's) met behulp van Azure CLI 2.0 Hallo. U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

tooperform deze stappen, moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).

## <a name="create-a-key-vault"></a>Een sleutelkluis maken
Een sleutelkluis maken en toewijzen van beleid voor Hallo-implementatie met [az keyvault maken](/cli/azure/keyvault#create). Hallo volgende voorbeeld wordt een sleutelkluis met de naam `myKeyVault` in Hallo `myResourceGroup` resourcegroep:

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a>Een Sleutelkluis voor gebruik met virtuele machines bijwerken
Hallo implementatiebeleid instellen op een bestaande sleutelkluis met [az keyvault update](/cli/azure/keyvault#update). Hallo volgende updates Hallo met de naam sleutelkluis `myKeyVault` in Hallo `myResourceGroup` resourcegroep:

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a>Gebruik sjablonen tooset up Sleutelkluis
Wanneer u een sjabloon gebruikt, moet u tooset hello `enabledForDeployment` eigenschap te`true` voor Hallo Sleutelkluis resource als volgt:

```json
{
    "type": "Microsoft.KeyVault/vaults",
    "name": "ContosoKeyVault",
    "apiVersion": "2015-06-01",
    "location": "<location-of-key-vault>",
    "properties": {
    "enabledForDeployment": "true",
    ....
    ....
    }
}
```

## <a name="next-steps"></a>Volgende stappen
Zie voor andere opties die u configureren kunt wanneer u een Sleutelkluis maken met behulp van sjablonen, [een sleutelkluis maken](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).
