---
title: aaaUse interne DNS voor de virtuele machine naamomzetting Hello Azure CLI 2.0 | Microsoft Docs
description: Hoe het virtuele netwerk toocreate netwerkinterfacekaarten en interne DNS gebruiken voor VM-naamomzetting in Azure met Azure CLI 2.0 Hallo
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
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a>Maken van virtuele netwerkinterfacekaarten en interne DNS gebruiken voor naamomzetting van de virtuele machine in Azure
Dit artikel laat zien hoe tooset statische interne DNS-namen voor virtuele Linux-machines met virtual network netwerkinterfacekaarten (vNics) en DNS-labelnamen Hello Azure CLI 2.0. U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Statische DNS-namen worden gebruikt voor permanente infrastructuurservices zoals een Jenkins build-server, die wordt gebruikt voor dit document of een Git-server.

Hallo-vereisten zijn:

* [een Azure-account.](https://azure.microsoft.com/pricing/free-trial/)
* [bestanden voor openbare en persoonlijke SSH-sleutels](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>Snelle opdrachten
Als u moet tooquickly Hallo taak, Hallo sectie volgen details Hallo opdrachten die nodig zijn. Meer gedetailleerde informatie en context voor elke stap u in de rest Hallo van Hallo document vindt [vanaf hier](#detailed-walkthrough). tooperform deze stappen, moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).

Randvoorwaarden voor: Resourcegroep, virtueel netwerk en subnet, Netwerkbeveiligingsgroep met SSH voor binnenkomend verkeer.

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a>Maken van een virtuele netwerkadapter met een statische interne DNS-naam
Maken van Hallo vNic met [az netwerk nic maken](/cli/azure/network/nic#create). Hallo `--internal-dns-name` CLI-vlag is voor instelling Hallo DNS-label, waardoor Hallo statische DNS-naam voor Hallo virtuele netwerkinterfacekaart (vNic). Hallo volgende voorbeeld wordt een vNic met de naam `myNic`, verbonden toohello `myVnet` virtueel netwerk, en maakt een interne DNS-naam-record genoemd `jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a>Een virtuele machine implementeert en verbinden van Hallo vNic
Maak een VM met [az vm create](/cli/azure/vm#create). Hallo `--nics` vlag Hallo vNic toohello VM tijdens Hallo implementatie tooAzure verbindt. Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM` met Azure beheerd schijven en wordt Hallo vNic met de naam `myNic` van Hallo vóór stap:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a>Gedetailleerd overzicht

Een volledige continue integratie en continue implementatie (CiCd) infrastructuur in Azure bepaalde servers toobe statisch of lange levensduur hebben servers vereist. Het verdient aanbeveling dat Azure activa zoals Hallo virtuele netwerken en Netwerkbeveiligingsgroepen statisch zijn en resources die zelden zijn geïmplementeerd langer bewaard moeten blijven. Zodra een virtueel netwerk is geïmplementeerd, kan opnieuw door nieuwe implementaties zonder een nadelige invloed toohello infrastructuur worden gebruikt. U kunt later een Git-opslagplaatsserver toevoegen of een automatiseringsserver Jenkins biedt CiCd toothis virtueel netwerk voor uw ontwikkel- of testomgevingen.  

Interne DNS-namen zijn alleen omgezet in een Azure-netwerk. Omdat Hallo DNS-namen interne zijn, zijn ze niet worden omgezet toohello buiten internet, zodat u extra beveiliging toohello infrastructuur.

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. De namen van de voorbeeld-parameter `myResourceGroup`, `myNic`, en `myVM`.

## <a name="create-hello-resource-group"></a>Hallo resourcegroep maken
Maak eerst de resourcegroep Hallo met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `westus` locatie:

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a>Hallo virtueel netwerk maken

de volgende stap Hallo is toobuild een virtueel netwerk toolaunch Hallo VM's in. Hallo virtueel netwerk bevat één subnet voor dit scenario. Zie voor meer informatie over virtuele netwerken van Azure [een virtueel netwerk maken met behulp van Azure CLI Hallo](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Virtueel netwerk met Hallo maken [az network vnet maken](/cli/azure/network/vnet#create). Hallo volgende voorbeeld wordt een virtueel netwerk met de naam `myVnet` en subnet met de naam `mySubnet`:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a>Hallo Netwerkbeveiligingsgroep maken
Beveiligingsgroepen voor Azure-netwerk zijn equivalent tooa firewall op Hallo netwerklaag. Zie voor meer informatie over Netwerkbeveiligingsgroepen [hoe toocreate nsg's in Azure CLI Hallo](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Maken van de netwerkbeveiligingsgroep met Hallo [az netwerk nsg maken](/cli/azure/network/nsg#create). Hallo volgende voorbeeld wordt een netwerkbeveiligingsgroep met de naam `myNetworkSecurityGroup`:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a>Een inkomende regel tooallow SSH toevoegen
Toevoegen van een inkomende regel voor de netwerkbeveiligingsgroep Hallo met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create). Hallo volgende voorbeeld maakt u een regel met naam `myRuleAllowSSH`:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a>Hallo subnet koppelen aan Hallo Netwerkbeveiligingsgroep
tooassociate hello subnet Hello Netwerkbeveiligingsgroep, gebruiken [az network vnet subnet update](/cli/azure/network/vnet/subnet#update). Hallo volgende voorbeeld wordt de subnetnaam hello `mySubnet` Hello Netwerkbeveiligingsgroep met de naam `myNetworkSecurityGroup`:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a>Hallo virtuele netwerkinterfacekaart en statische DNS-namen maken
Azure is zeer flexibel, maar toouse DNS-namen voor naamomzetting van de virtuele machine, moet u toocreate virtuele netwerkinterfacekaarten (vNics) met een DNS-label. vNics zijn belangrijk omdat u deze hergebruiken kunt door deze te verbinden toodifferent VM's via Hallo infrastructuur levenscyclus. Deze aanpak houdt Hallo vNic als statische resource Hallo VMs tijdelijke kan zijn. Met behulp van DNS op Hallo vNic labels, zijn we kunnen tooenable eenvoudige naamomzetting van andere virtuele machines in Hallo VNet. Andere virtuele machines tooaccess Hallo-automatiseringsserver met Hallo DNS-naam met omgezette namen kan `Jenkins` of Hallo Git-server als `gitrepo`.  

Maken van Hallo vNic met [az netwerk nic maken](/cli/azure/network/nic#create). Hallo volgende voorbeeld wordt een vNic met de naam `myNic`, verbonden toohello `myVnet` virtueel netwerk met de naam `myVnet`, en maakt een interne DNS-naam-record genoemd `jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Hallo VM in Hallo virtuele netwerkinfrastructuur implementeren
We hebben nu een virtueel netwerk en subnet, een Netwerkbeveiligingsgroep fungeert als een firewall tooprotect onze subnet door alle binnenkomend verkeer behalve poort 22 voor SSH en een vNic blokkeren. U kunt nu een virtuele machine binnen deze bestaande netwerkinfrastructuur implementeren.

Maak een VM met [az vm create](/cli/azure/vm#create). Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM` met Azure beheerd schijven en wordt Hallo vNic met de naam `myNic` van Hallo vóór stap:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

Met behulp van Hallo vlaggen CLI toocall uit bestaande resources we Azure toodeploy Hallo VM binnen de bestaande netwerk Hallo instrueren. tooreiterate, zodra een VNet en een subnet is geïmplementeerd, kunnen ze worden gelaten als statisch of permanente resources binnen uw Azure-regio.  

## <a name="next-steps"></a>Volgende stappen
* [Rechtstreeks uw eigen aangepaste omgeving maken voor een virtuele Linux-machine met Azure CLI-opdrachten](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Linux-VM in Azure met behulp van sjablonen maken](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
