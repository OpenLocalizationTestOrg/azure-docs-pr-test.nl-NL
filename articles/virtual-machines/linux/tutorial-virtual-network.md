---
title: aaaAzure virtuele netwerken en virtuele Linux-Machines | Microsoft Docs
description: Zelfstudie - beheert virtuele Azure-netwerken en virtuele Linux-Machines met hello Azure CLI
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a>Azure virtuele netwerken en virtuele Linux-Machines beheren met hello Azure CLI

Azure netwerken virtuele Azure-machines gebruiken voor interne en externe communicatie. Deze zelfstudie wordt begeleid twee virtuele machines implementeren en configureren van Azure netwerken voor deze virtuele machines. Hallo-voorbeelden in deze zelfstudie wordt ervan uitgegaan dat Hallo virtuele machines als host voor een webtoepassing met een database back-end optreden, maar een toepassing niet is geïmplementeerd in de zelfstudie Hallo. In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Een virtueel netwerk implementeren
> * Een subnet binnen een virtueel netwerk maken
> * Virtuele machines tooa subnet koppelen
> * Virtuele machine openbare IP-adressen beheren
> * Binnenkomend internetverkeer beveiligen
> * Beveiliging van verkeer van de VM-tooVM


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="vm-networking-overview"></a>Overzicht van VM-netwerken

Virtuele netwerken van Azure inschakelen van beveiligde netwerkverbindingen tussen virtuele machines, Hallo internet en andere Azure-services zoals Azure SQL database. Virtuele netwerken zijn onderverdeeld in logische segmenten subnetten genoemd. Subnetten gebruikt toocontrol netwerk flow, en als een beveiligingsgrens. Bij het implementeren van een virtuele machine, omvat het doorgaans de virtuele netwerkinterface, gekoppelde tooa subnet.

## <a name="deploy-virtual-network"></a>Virtueel netwerk implementeren

Voor deze zelfstudie wordt één virtueel netwerk met twee subnetten gemaakt. Een front-end-subnet voor het hosten van een webtoepassing en een back-end-subnet voor het hosten van een database-server.

Voordat u een virtueel netwerk maken kunt, maakt u een resourcegroep met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myRGNetwork* op Hallo eastus locatie.

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a>Virtueel netwerk maken

Ons Hallo [az network vnet maken](/cli/azure/network/vnet#create) opdracht toocreate een virtueel netwerk. In dit voorbeeld Hallo netwerk heet *mvVnet* en krijgt een adresvoorvoegsel van *10.0.0.0/16*. Een subnet wordt ook gemaakt met de naam *mySubnetFrontEnd* en het voorvoegsel *10.0.1.0/24*. Verderop in deze zelfstudie is een front-virtuele machine verbonden toothis subnet. 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a>Subnet maken

Een nieuw subnet is toegevoegd toohello virtueel netwerk met behulp van Hallo [az network vnet subnet maken](/cli/azure/network/vnet/subnet#create) opdracht. In dit voorbeeld Hallo subnet heet *mySubnetBackEnd* en krijgt een adresvoorvoegsel van *10.0.2.0/24*. Dit subnet wordt gebruikt met alle back-end-services.

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

Op dit moment is een netwerk gemaakt en gesegmenteerde in twee subnetten, één voor de front-end-services en een andere voor back-end-services. In de volgende sectie hello, virtuele machines worden gemaakt en verbonden toothese subnetten.

## <a name="understand-public-ip-address"></a>Openbaar IP-adres begrijpen

Een openbaar IP-adres kan Azure-resources toobe toegankelijk is op Hallo van internet. Een virtuele machine wordt in deze sectie van de zelfstudie Hallo toodemonstrate hoe toowork met openbare IP-adressen worden gemaakt.

### <a name="allocation-method"></a>Toewijzingsmethode

Een openbaar IP-adres kan worden toegewezen als dynamische of statische. Openbaar IP-adres is standaard dynamisch toegewezen. Dynamische IP-adressen worden vrijgegeven wanneer een virtuele machine toewijzing ongedaan wordt gemaakt. Dit gedrag zorgt ervoor dat Hallo IP-adres toochange tijdens een bewerking met een VM toewijzing is opgeheven.

Hallo-toewijzingsmethode toostatic, kan worden ingesteld tooa virtuele machine, zelfs tijdens de status van een toewijzing ongedaan is gemaakt waardoor wordt gegarandeerd dat Hallo IP-adres blijven worden toegewezen. Wanneer u een statisch toegewezen IP-adres, kan niet Hallo IP-adres zelf worden opgegeven. Het wordt toegewezen uit een groep met beschikbare adressen.

### <a name="dynamic-allocation"></a>Dynamische toewijzing

Bij het maken van een virtuele machine met Hallo [az vm maken](/cli/azure/vm#create) opdracht Hallo standaard openbare IP-adres toewijzingsmethode is dynamisch. In Hallo voorbeeld te volgen, wordt een virtuele machine gemaakt met een dynamische IP-adres. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a>Statische toewijzing

Bij het maken van een virtuele machine met Hallo [az vm maken](/cli/azure/vm#create) opdracht, opnemen Hallo `--public-ip-address-allocation static` argument tooassign statisch openbaar IP-adres. Deze bewerking wordt niet gedemonstreerd in deze zelfstudie echter in Hallo volgende sectie een dynamisch toegewezen IP-adres wordt gewijzigd tooa statisch toegewezen adres. 

### <a name="change-allocation-method"></a>Toewijzingsmethode wijzigen

Hallo IP-adres toewijzingsmethode kan worden gewijzigd met Hallo [az netwerk openbare ip-update](/cli/azure/network/public-ip#update) opdracht. Hallo methode voor de toewijzing van IP-adressen van Hallo front-VM wordt gewijzigd in dit voorbeeld toostatic.

Ten eerste toewijzing Hallo VM.

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

Gebruik Hallo [az netwerk openbare ip-update](/cli/azure/network/public-ip#update) opdracht tooupdate Hallo toewijzingsmethode. In dit geval Hallo `--allocation-method` te wordt ingesteld*statische*.

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

Hallo VM start.

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a>Er is geen openbaar IP-adres

Vaak een virtuele machine hoeft niet toobe toegankelijk zijn via internet Hallo. een virtuele machine zonder een openbaar IP-adres, gebruik Hallo toocreate `--public-ip-address ""` argument met een lege set dubbele aanhalingstekens. Deze configuratie wordt later in deze zelfstudie gedemonstreerd

## <a name="secure-network-traffic"></a>Netwerkverkeer beveiligen

Een netwerkbeveiligingsgroep (NSG) bevat een lijst met regels voor toestaan of weigeren netwerkverkeer tooresources verbonden tooAzure virtuele netwerken (VNet). Nsg's kunnen worden gekoppeld toosubnets of afzonderlijke netwerkinterfaces. Wanneer u een NSG is gekoppeld aan een netwerkinterface, dit is alleen van toepassing hello VM die is gekoppeld. Wanneer een NSG gekoppeld tooa subnet is, Hallo regels van toepassing tooall bronnen verbonden toohello subnet. 

### <a name="network-security-group-rules"></a>Netwerkbeveiligingsgroepen

NSG-regels definiëren netwerken poorten waarover verkeer wordt toegestaan of geweigerd. Hallo-regels kunnen bron en doel-IP-adresbereiken bevatten, zodat verkeer wordt geregeld tussen specifieke systemen of subnetten. NSG-regels bevatten ook een prioriteit (tussen 1- en 4096). Regels worden in volgorde van prioriteit Hallo geëvalueerd. Een regel met een prioriteit van 100 wordt geëvalueerd voor een regel met prioriteit 200.

Alle NSG's bevatten een set met standaardregels. Hallo-standaardregels kunnen niet worden verwijderd, maar omdat ze de laagste prioriteit Hallo zijn toegewezen, kunnen ze worden overschreven door het Hallo-regels die u maakt.

- **Virtueel netwerk** - die afkomstig zijn van verkeer en eindigt in een virtueel netwerk is toegestaan beide kanten van binnenkomend en uitgaand.
- **Internet** - uitgaand verkeer is toegestaan, maar dat binnenkomend verkeer wordt geblokkeerd.
- **De load balancer** -toestaan Azure load balancer tooprobe Hallo status van uw VM's en rolinstanties. Als u een set met gelijke taakverdeling niet gebruikt, kunt u deze regel onderdrukken.

### <a name="create-network-security-groups"></a>Netwerk-beveiligingsgroepen maken

Een netwerkbeveiligingsgroep kan worden gemaakt op Hallo dezelfde tijd als een virtuele machine met behulp van Hallo [az vm maken](/cli/azure/vm#create) opdracht. Wanneer doet, Hallo NSG is gekoppeld aan de netwerkinterface Hallo-VM's en een NSG-regel is automatisch gemaakt tooallow verkeer op poort *22* van elke bron. Eerder in deze zelfstudie Hallo Hallo front-NSG is automatisch gemaakt met de front-VM. Een regel voor het NSG is ook automatisch gemaakt voor poort 22. 

In sommige gevallen kan zijn handig toopre-een NSG, zoals wanneer SSH standaardregels mogen niet worden gemaakt of wanneer Hallo NSG gekoppelde tooa subnet moet maken. 

Gebruik Hallo [az netwerk nsg maken](/cli/azure/network/nsg#create) opdracht toocreate een netwerkbeveiligingsgroep.

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

In plaats van het koppelen van Hallo NSG tooa netwerkinterface is gekoppeld aan een subnet. In deze configuratie worden overgenomen elke virtuele machine die is aangesloten toohello subnet Hallo NSG-regels.

Bijwerken van bestaande Hallo-subnet met de naam *mySubnetBackEnd* met nieuwe NSG Hallo.

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

Maak nu een virtuele machine, die aangesloten toohello is *mySubnetBackEnd*. U ziet dat Hallo `--nsg` argument heeft de waarde leeg dubbele aanhalingstekens. Een NSG is niet gemaakt met de Hallo VM toobe nodig. Hallo VM is aangesloten toohello back-end-subnet, waardoor Hello vooraf gemaakte back-end NSG wordt beveiligd. Deze NSG geldt toohello VM. Hier ziet ook dat Hallo `--public-ip-address` argument heeft de waarde leeg dubbele aanhalingstekens. Deze configuratie maakt u een virtuele machine zonder een openbaar IP-adres. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a>Binnenkomend verkeer beveiligen

Wanneer hello front-virtuele machine is gemaakt, is een regel voor het NSG tooallow binnenkomend verkeer op poort 22 gemaakt. Deze regel kunnen de SSH-verbindingen toohello VM. In dit voorbeeld moet ook verkeer op poort worden toegestaan *80*. Deze configuratie kunt een web application toobe geopend op Hallo VM.

Gebruik Hallo [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create) opdracht toocreate een regel voor de poort *80*.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

Hallo front-end VM nu alleen toegankelijk is op poort *22* en poort *80*. Alle binnenkomend verkeer wordt geblokkeerd op Hallo netwerkbeveiligingsgroep. Het wellicht handig toovisualize hello NSG regel configuraties. Retour Hallo NSG regelconfiguratie Hello [az netwerk Regellijst](/cli/azure/network/nsg/rule#list) opdracht. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

Uitvoer:

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a>Beveiliging van verkeer van de VM-tooVM

Netwerkbeveiligingsgroepen kunnen ook tussen VM's toepassen. In dit voorbeeld Hallo Hallo front-end VM moet toocommunicate met back-end-VM op poort *22* en *3306*. Met deze configuratie kan SSH-verbindingen van Hallo front-VM en ook toestaan dat een toepassing op Hallo toocommunicate met betrekking tot een front-VM met een back-end MySQL-database. Al het andere verkeer moet worden geblokkeerd tussen Hallo front-end en back-end virtuele machines.

Gebruik Hallo [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create) opdracht toocreate een regel voor poort 22. U ziet dat Hallo `--source-address-prefix` geeft een waarde van argument *10.0.1.0/24*. Deze configuratie zorgt ervoor dat alleen verkeer van de front-end-subnet Hallo door Hallo NSG wordt toegestaan.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

Nu een regel voor MySQL-verkeer op poort 3306 toevoegen.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

Ten slotte omdat nsg's een standaard-regel waarmee hebben alle verkeer tussen virtuele machines in Hallo hetzelfde VNet, een regel kan worden gemaakt voor Hallo back-end nsg's tooblock al het verkeer. U ziet hier dat Hallo `--priority` krijgt een waarde van *300*, die is lager dat beide Hallo NSG en MySQL-regels. Deze configuratie zorgt ervoor dat verkeer van SSH en MySQL nog steeds door Hallo NSG wordt toegestaan.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

Hallo back-end VM nu alleen toegankelijk is op poort *22* en poort *3306* van Hallo front-end-subnet. Alle binnenkomend verkeer wordt geblokkeerd op Hallo netwerkbeveiligingsgroep. Het wellicht handig toovisualize hello NSG regel configuraties. Retour Hallo NSG regelconfiguratie Hello [az netwerk Regellijst](/cli/azure/network/nsg/rule#list) opdracht. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

Uitvoer:

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt gemaakt en Azure-netwerken als verwante toovirtual machines beveiligd. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Een virtueel netwerk implementeren
> * Een subnet binnen een virtueel netwerk maken
> * Virtuele machines tooa subnet koppelen
> * Virtuele machine openbare IP-adressen beheren
> * Binnenkomend internetverkeer beveiligen
> * Beveiliging van verkeer van de VM-tooVM

Ga toohello volgende zelfstudie toolearn over het beveiligen van gegevens op virtuele machines met Azure backup. 

> [!div class="nextstepaction"]
> [Back-up van Linux virtuele machines in Azure](./tutorial-backup-vms.md)
