---
title: een Linux-VM met een Azure-sjabloon met Azure CLI 1.0 aaaCreate | Microsoft Docs
description: Maak een Linux-VM op Azure met behulp van hello Azure CLI 1.0- en een Azure Resource Manager-sjabloon.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a>Hoe toocreate een Linux-VM met behulp van Azure CLI 1.0 een Azure Resource Manager-sjabloon Hallo
Dit artikel laat zien hoe tooquickly implementeren voor een virtuele Linux-Machine met behulp van hello Azure CLI 1.0 en een Azure Resource Manager-sjabloon. Hallo artikel is vereist:

* een Azure-account ([probeer een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/))
* Hallo [Azure CLI 1.0](../../cli-install-nodejs.md) aangemeld `azure login`.
* Hello Azure CLI *moet* modus Azure Resource Manager `azure config mode arm`.

U kunt ook snel een Linux-VM-sjabloon implementeren met behulp van Hallo [Azure-portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 1.0](#quick-command-summary) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](create-ssh-secured-vm-from-template.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel

## <a name="quick-command-summary"></a>Beknopt overzicht van opdrachten
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a>Gedetailleerd overzicht
Sjablonen kunt u toocreate virtuele machines in Azure met instellingen die u wilt de toocustomize tijdens Hallo starten, instellingen, zoals gebruikersnamen en hostnamen. Voor dit artikel starten we een Azure-sjabloon waarbij we gebruikmaken van een Ubuntu VM en een netwerkbeveiligingsgroep (NSG) waarbij poort 22 is geopend voor SSH .

Azure Resource Manager-sjablonen zijn JSON-bestanden die kunnen worden gebruikt voor eenvoudige eenmalige taken, zoals het starten van een Ubuntu VM zoals in dit artikel wordt gedaan.  Azure-sjablonen kunnen ook worden gebruikt tooconstruct complexe Azure configuraties voor de volledige omgeving een stack testen, ontwikkeling of productie-implementatie.

## <a name="create-hello-linux-vm"></a>Hallo Linux VM maken
Hallo van de volgende code voorbeeld ziet u hoe toocall `azure group create` toocreate een bron groeperen en een Linux-VM SSH beveiligde op Hallo implementeren met behulp van dezelfde tijd [deze Azure Resource Manager-sjabloon](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json). Vergeet niet dat in uw voorbeeld moet u toouse namen die unieke tooyour omgeving. In dit voorbeeld wordt *myResourceGroup* als naam resourcegroep hello, en *myVM* als Hallo VM-naam.

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

Hallo-uitvoer moet eruitzien als Hallo uitvoerblok te volgen:

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

In dat geval een VM die gebruikmaakt van Hallo geïmplementeerd `--template-uri` parameter.  U kunt ook downloaden of lokaal een sjabloon maken en doorgeven met Hallo Hallo-sjabloon `--template-file` parameter met een pad toohello sjabloonbestand als argument. Hello Azure CLI vraagt u om de vereiste door Hallo sjabloon Hallo-parameters.

## <a name="next-steps"></a>Volgende stappen
Zoeken Hallo [sjablonengalerie](https://azure.microsoft.com/documentation/templates/) toodiscover welke app-frameworks toodeploy volgende.

