---
title: aaaHow tooload saldo Linux virtuele machines in Azure | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure balancer toocreate een maximaal beschikbare en beveiligde toepassing geladen over drie Linux VM 's
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>Hoe tooload balans vinden tussen virtuele Linux-machines in Azure toocreate een maximaal beschikbare toepassing
Taakverdeling biedt een hoger niveau van de beschikbaarheid van binnenkomende aanvragen verspreid over meerdere virtuele machines. In deze zelfstudie leert u Hallo verschillende onderdelen van hello Azure load balancer die verkeer distribueren en bieden hoge beschikbaarheid. Procedures voor:

> [!div class="checklist"]
> * Een Azure load balancer maken
> * Een load balancer health test maken
> * Regels voor netwerkverkeer voor de load balancer maken
> * Cloud-init toocreate een eenvoudige Node.js-app gebruiken
> * Virtuele machines maken en koppelen tooa load balancer
> * Een load balancer in actie weergeven
> * Toevoegen of virtuele machines van een load balancer verwijderen


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="azure-load-balancer-overview"></a>Overzicht van Azure load balancer
Een Azure load balancer is een Layer-4 (TCP, UDP) load balancer die zorgt voor hoge beschikbaarheid door het distribueren van inkomend verkeer tussen orde virtuele machines. Een load balancer health test een bepaalde poort op elke virtuele machine bewaakt en distribueert u alleen verkeer tooan operationele VM.

U definieert een front-end-IP-configuratie met een of meer openbare IP-adressen. Deze front-end-IP-configuratie kan de load balancer en toepassingen toobe toegankelijk via Hallo Internet. 

Virtuele machines verbinding tooa load balancer met behulp van de virtuele netwerkinterfacekaart (NIC). toodistribute verkeer toohello VM's, een back-end-adresgroep bevat Hallo IP-adressen van Hallo virtuele (NIC's) verbonden toohello load balancer.

toocontrol hello stroom van verkeer, kunt u definiëren load balancerregels voor specifieke poorten en protocollen die zijn toegewezen tooyour virtuele machines.

Als u de vorige zelfstudie hello te gevolgd[maken van een virtuele-machineschaalset](tutorial-create-vmss.md), een load balancer voor u is gemaakt. Al deze onderdelen zijn geconfigureerd voor u als onderdeel van Hallo scale set.


## <a name="create-azure-load-balancer"></a>Azure load balancer maken
In deze sectie beschrijft hoe u kunt maken en configureren van elk onderdeel Hallo load balancer. Voordat u de load balancer maken kunt, maakt u een resourcegroep met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupLoadBalancer* in Hallo *eastus* locatie:

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a>Een openbaar IP-adres maken
tooaccess uw app op Hallo Internet, moet u een openbaar IP-adres voor Hallo load balancer. Maken van een openbaar IP-adres met [az netwerk openbare ip-maken](/cli/azure/network/public-ip#create). Hallo volgende voorbeeld maakt u een openbaar IP-adres met de naam *myPublicIP* in Hallo *myResourceGroupLoadBalancer* resourcegroep:

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a>Een load balancer maken
Maken van een load balancer met [az network Load Balancer maken](/cli/azure/network/lb#create). Hallo volgende voorbeeld maakt u een load balancer met de naam *myLoadBalancer* en wijst Hallo *myPublicIP* adres toohello front-end-IP-configuratie:

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a>Een health test maken
tooallow hello load balancer toomonitor Hallo status van uw app, dat u een health test gebruiken. Hallo health test wordt dynamisch toegevoegd of verwijderd van virtuele machines van Hallo load balancer wisselen op basis van hun antwoord toohealth controles. Standaard wordt een virtuele machine verwijderd uit Hallo load balancer-distributie na twee opeenvolgende fouten met intervallen van 15 seconden. U maakt een health test op basis van een protocol of de pagina voor de controle van een specifieke status voor uw app. 

Hallo volgende voorbeeld wordt een TCP-test. U kunt ook aangepaste HTTP-tests voor meer fijnmazige statuscontroles maken. Wanneer u een aangepaste HTTP-test, moet u Hallo selectievakje statuspagina, zoals *healthcheck.js*. Hallo test moet retourneren een **HTTP 200 OK** antwoord voor Hallo load balancer tookeep Hallo host in de draaihoek.

toocreate een TCP health test, die u gebruikt [az network Load Balancer-test maken](/cli/azure/network/lb/probe#create). Hallo volgende voorbeeld wordt een health test met de naam *myHealthProbe*:

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a>Een load balancer-regel maken
Een load balancer-regel is gebruikte toodefine hoe verkeer wordt gedistribueerde toohello virtuele machines. U definieert Hallo front-end-IP-configuratie voor Hallo binnenkomende verkeer en Hallo backend-IP-adresgroep tooreceive Hallo, samen met de vereiste bron Hallo en doelpoort. toomake zorgen dat alleen orde virtuele machines verkeer ontvangt, u Hallo health test toouse ook definiëren.

Maken van een regel voor load balancer met [az network Load Balancer-regel maken](/cli/azure/network/lb/rule#create). Hallo volgende voorbeeld maakt u een regel met naam *myLoadBalancerRule*, gebruikt Hallo *myHealthProbe* health test en saldo's verkeer op poort *80*:

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a>Virtueel netwerk configureren
Voordat u een aantal virtuele machines implementeren en uw balancer kunt testen, maak Hallo ondersteunende resources van een virtueel netwerk. Zie voor meer informatie over virtuele netwerken Hallo [Azure Virtual Networks beheren](tutorial-virtual-network.md) zelfstudie.

### <a name="create-network-resources"></a>Maken van netwerkbronnen
Maak een virtueel netwerk met [az network vnet maken](/cli/azure/network/vnet#create). Hallo volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet* met een subnet met de naam *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

een netwerkbeveiligingsgroep tooadd, die u gebruikt [az netwerk nsg maken](/cli/azure/network/nsg#create). Hallo volgende voorbeeld wordt een netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

Maken van een groep van de netwerkbeveiligingsregel met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create). Hallo volgende voorbeeld wordt een groep netwerkbeveiligingsregel met de naam *myNetworkSecurityGroupRule*:

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

Virtuele NIC's zijn gemaakt met [az netwerk nic maken](/cli/azure/network/nic#create). Hallo maakt volgende voorbeeld drie virtuele NIC's. (Een virtuele NIC voor elke VM die u maakt voor uw app in hello te volgen stappen.) U kunt extra virtuele NIC's en virtuele machines maken op elk gewenst moment en ze toohello load balancer toevoegen:

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a>Virtuele machines maken

### <a name="create-cloud-init-config"></a>Cloud-init-configuratie maken
In een vorige zelfstudie over [hoe een virtuele Linux-machine op de eerste keer opstarten toocustomize](tutorial-automate-vm-deployment.md), u leert hoe tooautomate VM aanpassing met cloud-init. U kunt dezelfde cloud init configuration file tooinstall NGINX Hallo en uitvoeren van een eenvoudige 'Hallo wereld' Node.js-app.

Maak een bestand met de naam in uw huidige shell *cloud init.txt* en plakken Hallo configuratie. Bijvoorbeeld, Hallo-bestand in Hallo Cloud-Shell op uw lokale machine niet maken. Voer `sensible-editor cloud-init.txt` toocreate Hallo bestand en een overzicht van beschikbare editors. Zorg ervoor dat Hallo hele cloud-init-bestand correct is gekopieerd, met name Hallo eerste regel:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-virtual-machines"></a>Virtuele machines maken
tooimprove hello hoge beschikbaarheid van uw app, uw virtuele machines in een beschikbaarheidsset plaatst. Zie voor meer informatie over beschikbaarheidssets Hallo vorige [hoe toocreate maximaal beschikbare virtuele machines](tutorial-availability-sets.md) zelfstudie.

Maken van een beschikbaarheidsset met [az vm beschikbaarheidsset maken](/cli/azure/vm/availability-set#create). Hallo volgende voorbeeld maakt u een beschikbaarheidsset benoemde *myAvailabilitySet*:

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

Nu kunt u virtuele machines Hallo met [az vm maken](/cli/azure/vm#create). Hallo volgende voorbeeld maakt drie virtuele machines en SSH-sleutels worden gegenereerd als deze niet al bestaan:

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

Er zijn achtergrondtaken die toorun verder gaat nadat hello Azure CLI keert u terug toohello prompt. Hallo `--no-wait` parameter wacht niet voor alle taken toocomplete Hallo. Het is mogelijk een andere paar minuten voordat u toegang hebt tot Hallo-app. Hallo load balancer health test automatisch gedetecteerd wanneer Hallo-app wordt uitgevoerd op elke virtuele machine. Zodra het Hallo-app wordt uitgevoerd, begint Hallo load balancer-regel toodistribute verkeer.


## <a name="test-load-balancer"></a>Test load balancer
Hallo openbare IP-adres van de load balancer met verkrijgen [az netwerk openbare ip-weergeven](/cli/azure/network/public-ip#show). Hallo volgende voorbeeld Hallo IP-adres krijgt voor *myPublicIP* eerder hebt gemaakt:

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

Vervolgens kunt u in de webbrowser tooa Hallo openbaar IP-adres invoeren. Houd er rekening mee - duurt een paar minuten Hallo Hallo VMs toobe gereed voordat Hallo load balancer toodistribute verkeer toothem wordt gestart. Hallo-app wordt weergegeven, inclusief Hallo hostnaam Hallo VM die Hallo load balancer gedistribueerde tooas verkeer in het volgende voorbeeld Hallo:

![Actieve Node.js-app](./media/tutorial-load-balancer/running-nodejs-app.png)

toosee hello load balancer verkeer verdelen over alle drie virtuele machines waarop uw app wordt uitgevoerd, u kunt force vernieuwen van uw webbrowser.


## <a name="add-and-remove-vms"></a>Toevoegen en verwijderen van virtuele machines
Mogelijk moet u tooperform onderhoud op Hallo van virtuele machines waarop uw app, zoals het installeren van updates voor het besturingssysteem wordt uitgevoerd. toodeal met tooyour-app voor verkeer, moet u mogelijk tooadd extra virtuele machines. Deze sectie leest u hoe tooremove of een virtuele machine van Hallo load balancer toe te voegen.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Een virtuele machine van Hallo load balancer verwijderen
U kunt een virtuele machine verwijderen uit Hallo back-end-adresgroep met [az nic ip-config-netwerkadresgroep verwijderen](/cli/azure/network/nic/ip-config/address-pool#remove). Hallo volgende voorbeeld verwijdert Hallo virtuele NIC voor **myVM2** van *myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

toosee hello load balancer verkeer verdelen over Hallo overige twee virtuele machines met uw app u kunt force vernieuwen van uw webbrowser. U kunt nu onderhoud uitvoeren op Hallo VM, zoals het installeren van updates voor het besturingssysteem of het uitvoeren van een VM opnieuw wordt opgestart.

### <a name="add-a-vm-toohello-load-balancer"></a>Een VM toohello load balancer toevoegen
Na het uitvoeren van onderhoud van de virtuele machine, of als u tooexpand capaciteit nodig hebt, kunt u toevoegen met een VM toohello back-end-adresgroep met [az nic ip-config-netwerkadresgroep toevoegen](/cli/azure/network/nic/ip-config/address-pool#add). Hallo volgende voorbeeld wordt toegevoegd Hallo virtuele NIC voor **myVM2** te*myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt gemaakt van een load balancer en virtuele machines tooit gekoppeld. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Een Azure load balancer maken
> * Een load balancer health test maken
> * Regels voor netwerkverkeer voor de load balancer maken
> * Cloud-init toocreate een eenvoudige Node.js-app gebruiken
> * Virtuele machines maken en koppelen tooa load balancer
> * Een load balancer in actie weergeven
> * Toevoegen of virtuele machines van een load balancer verwijderen

De volgende zelfstudie toolearn toohello voor vooraf meer informatie over de onderdelen van de virtuele Azure-netwerk.

> [!div class="nextstepaction"]
> [Virtuele machines en virtuele netwerken beheren](tutorial-virtual-network.md)
