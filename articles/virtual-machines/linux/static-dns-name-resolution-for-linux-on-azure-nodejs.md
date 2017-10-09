---
title: aaaUsing interne DNS voor de virtuele machine naamomzetting in Azure | Microsoft Docs
description: Interne DNS gebruiken voor naamomzetting van de virtuele machine in Azure.
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
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a>Met behulp van de interne DNS voor naamomzetting van de virtuele machine in Azure

Dit artikel laat zien hoe tooset statische interne DNS-namen voor virtuele Linux-machines met virtuele NIC kaarten (VNic) en DNS-labelnamen. Statische DNS-namen worden gebruikt voor permanente infrastructuurservices zoals een Jenkins build-server, die wordt gebruikt voor dit document of een Git-server.

Hallo-vereisten zijn:

* [een Azure-account.](https://azure.microsoft.com/pricing/free-trial/)
* [bestanden voor openbare en persoonlijke SSH-sleutels](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 1.0](#quick-commands) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel


## <a name="quick-commands"></a>Snelle opdrachten

Als u moet tooquickly Hallo taak, Hallo sectie volgen details Hallo opdrachten die nodig zijn. Meer gedetailleerde informatie en context voor elke stap u rest Hallo van Hallo document vindt [vanaf hier](#detailed-walkthrough).  

Randvoorwaarden voor: Resourcegroep, VNet, NSG met SSH inkomende Subnet.

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a>Een VNic maken met een statische interne DNS-naam

Hallo `-r` cli-vlag is voor instelling Hallo DNS-label, waardoor Hallo statische DNS-naam voor Hallo VNic.

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a>Hallo VM in Hallo VNet, NSG en implementeert, verbinding maken met de Hallo VNic

Hallo `-N` hello VNic toohello verbindt nieuwe virtuele machine tijdens Hallo implementatie tooAzure.

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a>Gedetailleerd overzicht

Een volledige continue integratie en continue implementatie (CiCd) infrastructuur in Azure bepaalde servers toobe statisch of lange levensduur hebben servers vereist.  Het verdient aanbeveling dat Azure activa zoals Hallo virtuele netwerken (vnet's) en Netwerkbeveiligingsgroepen (nsg's), mag niet statisch en resources die zelden zijn geïmplementeerd langer bewaard moeten blijven.  Zodra een VNet is geïmplementeerd, kan opnieuw door nieuwe implementaties zonder een nadelige invloed toohello infrastructuur worden gebruikt.  Toe te voegen toothis statische netwerk een Git biedt repository server en een Jenkins automation-server CiCd tooyour ontwikkel- of testomgevingen.  

Interne DNS-namen zijn alleen omgezet in een Azure-netwerk.  Omdat Hallo DNS-namen interne zijn, zijn ze niet worden omgezet toohello buiten internet, zodat u extra beveiliging toohello infrastructuur.

_Vervang geen voorbeelden door uw eigen namen._

## <a name="create-hello-resource-group"></a>Hallo resourcegroep maken

Een resourcegroep benodigde tooorganize is alles wat er in dit scenario worden gemaakt.  Zie voor meer informatie over Azure-resourcegroepen [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a>Hallo VNet maken

de eerste stap Hallo is toobuild een VNet-toolaunch Hallo VM's in.  Hallo VNet bevat één subnet voor dit scenario.  Zie voor meer informatie over Azure VNets [een virtueel netwerk maken met behulp van hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a>Hallo NSG maken

Hallo Subnet is gebouwd achter een bestaande Netwerkbeveiligingsgroep zodat wij Hallo NSG voordat Hallo Subnet bouwen.  Azure nsg's zijn equivalent tooa firewall op Hallo netwerklaag.  Zie voor meer informatie over Azure nsg's [hoe toocreate nsg's in Azure CLI Hallo](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Regel voor geven van een binnenkomende SSH toevoegen

Hallo Linux VM moet toegang vanaf Hallo internet zodat een regel voor het toestaan van binnenkomende poort 22 verkeer toobe Hallo netwerk tooport 22 op Hallo Linux VM doorgegeven nodig is.

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>Voeg een subnet toohello VNet

Virtuele machines binnen Hallo VNet moeten zich bevinden in een subnet.  Elke VNet kan meerdere subnetten hebben.  Hallo subnet maken en Hallo subnet koppelen aan Hallo NSG tooadd een firewall toohello subnet.

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

Hallo Subnet is nu toegevoegd in Hallo VNet en die zijn gekoppeld aan het NSG hello en Hallo NSG regel.

## <a name="creating-static-dns-names"></a>Statische DNS-namen maken

Azure is zeer flexibel, maar toouse DNS-namen voor de naamomzetting voor virtuele machines, moet u ze als virtuele (VNics netwerkkaarten) met behulp van DNS-labels toocreate.  VNics zijn belangrijk omdat u deze hergebruiken kunt door deze te verbinden toodifferent virtuele machines, blijft Hallo VNic als statische resource Hallo VMs tijdelijke kan zijn.  Met behulp van DNS op Hallo VNic labels, zijn we kunnen tooenable eenvoudige naamomzetting van andere virtuele machines in Hallo VNet.  Andere virtuele machines tooaccess Hallo-automatiseringsserver met Hallo DNS-naam met omgezette namen kan `Jenkins` of Hallo Git-server als `gitrepo`.  Een VNic maken en deze koppelen aan een Subnet wordt gemaakt in de vorige stap Hallo Hallo.

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Hallo VM in Hallo VNet en NSG implementeren

We hebben nu een VNet, een subnet in dit VNet en een NSG fungeert als een firewall tooprotect onze subnet door alle binnenkomend verkeer behalve poort 22 voor SSH blokkeren.  Hallo VM kan nu worden geïmplementeerd in deze bestaande netwerkinfrastructuur.

Met behulp van Azure CLI Hallo en Hallo `azure vm create` opdracht Hallo Linux VM geïmplementeerde toohello bestaande Azure-resourcegroep, VNet Subnet en VNic is.  Zie voor meer informatie over het gebruik van Hallo CLI toodeploy een volledige virtuele machine [een volledige Linux-omgeving maken met behulp van hello Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

Met behulp van Hallo vlaggen CLI toocall uit bestaande resources we Azure toodeploy Hallo VM binnen de bestaande netwerk Hallo instrueren.  tooreiterate, zodra een VNet en een subnet is geïmplementeerd, kunnen ze worden gelaten als statisch of permanente resources binnen uw Azure-regio.  

## <a name="next-steps"></a>Volgende stappen
* [Rechtstreeks uw eigen aangepaste omgeving maken voor een virtuele Linux-machine met Azure CLI-opdrachten](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Linux-VM in Azure met behulp van sjablonen maken](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
