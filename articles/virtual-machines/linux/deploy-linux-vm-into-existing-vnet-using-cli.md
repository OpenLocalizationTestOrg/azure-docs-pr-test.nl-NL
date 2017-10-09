---
title: aaaDeploy virtuele Linux-machines in bestaande netwerk met Azure CLI 2.0 | Microsoft Docs
description: Meer informatie over hoe een virtuele Linux-machine naar een bestaand virtueel netwerk met behulp van toodeploy hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a>Hoe toodeploy virtuele Linux-machine in Azure een bestaand virtueel netwerk met hello Azure CLI

Dit artikel ziet u hoe toouse hello Azure CLI 2.0 toodeploy een virtuele machine (VM) in een bestaand virtueel netwerk. Hallo-vereisten zijn:

- [een Azure-account.](https://azure.microsoft.com/pricing/free-trial/)
- [bestanden voor openbare en persoonlijke SSH-sleutels](mac-create-ssh-keys.md)

U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).


## <a name="quick-commands"></a>Snelle opdrachten
Als u moet tooquickly Hallo taak, Hallo sectie volgen details Hallo opdrachten die nodig zijn. Meer gedetailleerde informatie en context voor elke stap u rest Hallo van Hallo document vindt [vanaf hier](#detailed-walkthrough).

toocreate deze aangepaste omgeving, moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. De namen van de voorbeeld-parameter *myResourceGroup*, *myVnet*, en *myVM*.

**Randvoorwaarden voor:** Azure-resourcegroep, virtueel netwerk en subnet, inkomende netwerkbeveiligingsgroep met SSH, en een virtuele netwerkinterfacekaart.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Hallo VM in Hallo virtuele netwerkinfrastructuur implementeren

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a>Gedetailleerd overzicht

Azure activa zoals virtuele netwerken en netwerkbeveiligingsgroepen moeten statisch en resources die zelden zijn geïmplementeerd langer bewaard moeten blijven. Zodra een virtueel netwerk is geïmplementeerd, kan opnieuw door nieuwe implementaties zonder een nadelige invloed toohello infrastructuur worden gebruikt. Nadenken over een virtueel netwerk als een netwerkswitch traditionele hardware - u moet een geheel nieuwe hardware overschakelen met elke implementatie tooconfigure niet. Met een virtueel netwerk correct is geconfigureerd, kunt u blijven toodeploy nieuwe virtuele machines in dit virtuele netwerk met weinig steeds, eventuele wijzigingen vereist over Hallo levensduur van het virtuele netwerk Hallo.

toocreate deze aangepaste omgeving, moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. De namen van de voorbeeld-parameter *myResourceGroup*, *myVnet*, en *myVM*.

## <a name="create-hello-resource-group"></a>Hallo resourcegroep maken

Maak eerst een Azure resource group tooorganize alles wat die u in dit scenario maakt. Zie [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md) (Overzicht van Azure Resource Manager) voor meer informatie over resourcegroepen. Maak Hallo resourcegroep met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a>Hallo virtueel netwerk maken

U kunt bouwen van een virtuele Azure-netwerk toolaunch Hallo VM's in. Zie voor meer informatie over virtuele netwerken [een virtueel netwerk maken met behulp van Azure CLI Hallo](../../virtual-network/virtual-networks-create-vnet-arm-cli.md). Virtueel netwerk met Hallo maken [az network vnet maken](/cli/azure/network/vnet#create). Hallo volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet* en subnet met de naam *mySubnet*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a>Hallo netwerkbeveiligingsgroep maken

Beveiligingsgroepen voor Azure-netwerk zijn equivalent tooa firewall op Hallo netwerklaag. Zie voor meer informatie over netwerkbeveiligingsgroepen [hoe toocreate netwerk beveiligingsgroepen in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md). Maken van de netwerkbeveiligingsgroep met Hallo [az netwerk nsg maken](/cli/azure/network/nsg#create). Hallo volgende voorbeeld wordt een netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Regel voor geven van een binnenkomende SSH toevoegen

Hallo VM nodig toegang vanaf internet, zodat een regel voor het toestaan van binnenkomende poort 22 verkeer toobe Hallo netwerk tooport 22 op Hallo VM doorgegeven nodig Hallo. Toevoegen van een inkomende regel voor de netwerkbeveiligingsgroep Hallo met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create). Hallo volgende voorbeeld maakt u een regel met naam *myNetworkSecurityGroupRuleSSH*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a>Hallo subnet toohello netwerkbeveiligingsgroep toevoegen

Hallo netwerkbeveiligingsgroepen mag toegepaste tooa subnet of een specifieke virtuele netwerkinterface. U kunt Hallo beveiliging groep tooour netwerksubnet koppelen. Koppel uw subnet toohello netwerkbeveiligingsgroep met [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a>Een virtueel netwerk interface kaart toohello subnet toevoegen

Virtuele netwerkinterfacekaarten (VNics) zijn belangrijk omdat u ze hergebruiken kunt door deze toodifferent virtuele machines te verbinden. Deze opnieuw gebruiken kunt u tookeep hello VNic als statische resource Hallo VMs tijdelijke kan zijn. Een VNic maken en deze koppelen aan Hallo subnet met [az netwerk nic maken](/cli/azure/network/nic#create). Hallo volgende voorbeeld wordt een VNic met de naam *myNic*:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Hallo VM in Hallo virtuele netwerkinfrastructuur implementeren

U hebt nu een virtueel netwerk en subnet en een security group tooprotect Hallo netwerksubnet door alle binnenkomend verkeer behalve poort 22 voor SSH blokkeren. Hallo VM kan nu worden geïmplementeerd in deze bestaande netwerkinfrastructuur.

Maken van uw virtuele machine met [az vm maken](/cli/azure/vm#create). Zie voor meer informatie over het Hallo toouse met hello Azure CLI 2.0 toodeploy een volledige virtuele machine vlaggen, [een volledige Linux-omgeving maken met behulp van Azure CLI Hallo](create-cli-complete.md).

Hallo volgende voorbeeld maakt een VM die gebruikmaakt van Azure-beheerde schijven. Deze schijven worden afgehandeld door hello Azure-platform en hoeven niet alle toostore voorbereidings- of locatie ze. Zie voor meer informatie over beheerde schijven [overzicht Azure Managed Disks](../../storage/storage-managed-disks-overview.md). Als u toouse zonder begeleiding schijven wenst, Zie Hallo aanvullende opmerking hieronder.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

Als u beheerde schijven gebruikt, moet u deze stap overslaan. Als u toouse zonder begeleiding schijven wenst, moet u tooadd Hallo na extra parameters toohello procedure opdracht toocreate zonder begeleiding schijven in Hallo opslagaccount met de naam `mystorageaccount`: 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

Met behulp van Hallo vlaggen CLI toocall uit bestaande resources instrueren van Azure toodeploy Hallo VM binnen de bestaande netwerk Hallo. Zodra een virtueel netwerk en subnet is geïmplementeerd, kunnen ze als statisch of permanente resources binnen uw Azure-regio worden gelaten. In dit voorbeeld u niet maken en toewijzen van een openbare IP-adres toohello VNic, zodat deze virtuele machine niet openbaar toegankelijk via Hallo Internet is. Zie voor meer informatie [een virtuele machine maken met een statische openbare IP-adres met behulp van Azure CLI Hallo](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over manieren toocreate virtuele machines in Azure Hallo resources te volgen:

* [Een Azure Resource Manager-sjabloon toocreate een specifieke implementatie gebruiken](../windows/cli-deploy-templates.md)
* [Rechtstreeks uw eigen aangepaste omgeving maken voor een virtuele Linux-machine met Azure CLI-opdrachten](create-cli-complete.md)
* [Linux-VM in Azure met behulp van sjablonen maken](create-ssh-secured-vm-from-template.md)
