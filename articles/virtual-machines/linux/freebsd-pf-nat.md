---
title: de aaaUse FreeBSD pakketfilters toocreate een firewall in Azure | Microsoft Docs
description: Meer informatie over hoe toodeploy een NAT-apparaat met behulp van FreeBSD firewall PF in Azure.
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/20/2017
ms.author: kyliel
ms.openlocfilehash: 3d3a5dde2ca03ba6fc384581c786f5eb746e6d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-freebsds-packet-filter-toocreate-a-secure-firewall-in-azure"></a>Hoe toouse FreeBSD van pakketfilter toocreate een veilige firewall in Azure
Dit artikel bevat hoe toodeploy een NAT-firewall met behulp van de FreeBSD verpakker Filter via Azure Resource Manager-sjabloon voor algemene scenario met web server.

## <a name="what-is-pf"></a>Wat is PF?
PF (pakketfilter, ook geschreven pf) is een centrale onderdeel van de software voor het gebruik van een BSD gelicentieerde stateful pakketfilter. PF sindsdien snel heeft ontwikkeld en nu heeft verschillende voordelen ten opzichte van andere beschikbare firewalls. NAT (Network Address Translation) wordt PF na één dag, klikt u vervolgens pakketplanner en actieve wachtrijbeheer zijn geïntegreerd in PF, door Hallo ALTQ integreren en waardoor het worden geconfigureerd via de PF configuratie. Functies zoals pfsync en CARP voor failover en redundantie, authpf voor sessieverificatie en FTP-proxy tooease gebruik Hallo moeilijk FTP-protocol, hebben ook uitgebreide PF. Kortom, is PF een krachtige en veelzijdige firewall. 

## <a name="get-started"></a>Aan de slag
Als u geïnteresseerd bent in een beveiligde firewall instellen in de cloud Hallo voor uw webservers en vervolgens aan de slag. Hallo-scripts die worden gebruikt in deze Azure Resource Manager-sjabloon tooset van uw netwerktopologie, kunt u ook toepassen.
Hello Azure Resource Manager-sjabloon instellen van een FreeBSD virtuele machine die voert NAT /redirection met PF en twee FreeBSD virtuele machines met Hallo Nginx webserver is geïnstalleerd en geconfigureerd. Bovendien tooperforming NAT voor twee webservers Hallo uitgaande verkeer, Hallo NAT/omleiding van virtuele machine onderschept HTTP-aanvragen en hen toohello twee webservers round-robin toewijst omleidt. Hallo VNet Hallo persoonlijke niet-routeerbare IP-adresruimte 10.0.0.2/24 gebruikt en u kunt de parameters Hallo van Hallo sjabloon wijzigen. Hello Azure Resource Manager-sjabloon wordt ook een routetabel voor de hele VNet een verzameling van afzonderlijke routes is gebruikt Azure standaardroutes toooverride op basis van IP-doeladres Hallo Hallo gedefinieerd. 

![pf_topology](./media/freebsd-pf-nat/pf_topology.jpg)
    
### <a name="deploy-through-azure-cli"></a>Implementeren via Azure CLI
Moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login). Maak een resourcegroep maken met [az group create](/cli/azure/group#create). Hallo volgende voorbeeld wordt een Resourcegroepnaam `myResourceGroup` in Hallo `West US` locatie.

```azurecli
az group create --name myResourceGroup --location westus
```

Vervolgens implementeert u de sjabloon Hallo [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup) met [az implementatie maken](/cli/azure/group/deployment#create). Download [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/pf-freebsd-setup/azuredeploy.parameters.json) onder hetzelfde pad Hallo en uw eigen waarden resource, zoals definiëren `adminPassword`, `networkPrefix`, en `domainNamePrefix`. 

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeploymentName \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/pf-freebsd-setup/azuredeploy.json \
    --parameters '@azuredeploy.parameters.json' --verbose
```

Na ongeveer 5 minuten, krijgt u informatie van Hallo `"provisioningState": "Succeeded"`. Vervolgens u ssh toohello frontend VM (NAT kunt) of toegang tot de webserver Nginx in een browser Hallo openbare IP-adres of FQDN-naam van Hallo frontend VM (NAT). Hallo volgende voorbeeld wordt een lijst FQDN-naam en openbare IP-adres die toohello frontend VM (NAT) in Hallo toegewezen `myResourceGroup` resourcegroep. 

```azurecli
az network public-ip list --resource-group myResourceGroup
```
    
## <a name="next-steps"></a>Volgende stappen
Wilt u tooset om uw eigen NAT in Azure? Open Source gratis maar krachtige? PF is dan een goede keuze. Met behulp van de sjabloon Hallo [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup), hoeft u slechts vijf minuten tooset van een NAT-firewall met round-robin van taakverdeling met behulp van FreeBSD PF in Azure voor veelvoorkomende scenario met web server. 

Als u wilt dat toolearn Hallo aanbod van FreeBSD in Azure, raadpleegt u te[tooFreeBSD inleiding op Azure](freebsd-intro-on-azure.md).

Desgewenst kunt u meer informatie over PF tooknow te verwijzen[FreeBSD handboek](https://www.freebsd.org/doc/handbook/firewalls-pf.html) of [PF User's Guide](https://www.freebsd.org/doc/handbook/firewalls-pf.html).
