---
title: een virtuele Machine-Schaalsets Linux in Azure aaaCreate | Microsoft Docs
description: Maken en implementeren van een maximaal beschikbare toepassing op virtuele Linux-machines met behulp van een virtuele-machineschaalset
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a>Een virtuele-Machineschaalset maken en implementeren van een maximaal beschikbare app op Linux
Een virtuele-machineschaalset kunt u toodeploy en beheren van een reeks identiek zijn, automatisch schalen virtuele machines. U kunt Hallo aantal virtuele machines in de schaalset Hallo handmatig schalen of regels tooautoscale op basis van CPU-gebruik, geheugen-aanvraag of netwerkverkeer definiëren. In deze zelfstudie maakt implementeren u een virtuele-machineschaalset instellen in Azure. Procedures voor:

> [!div class="checklist"]
> * Cloud-init toocreate een tooscale app gebruiken
> * Maken van een virtuele-machineschaalset
> * Vergroten of verkleinen Hallo aantal exemplaren in een schaalset
> * Verbindingsgegevens voor scale set exemplaren weergeven
> * Gegevensschijven in een schaalset gebruiken


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="scale-set-overview"></a>Overzicht van Scale Set
Een virtuele-machineschaalset kunt u toodeploy en beheren van een reeks identiek zijn, automatisch schalen virtuele machines. Schaal wordt ingesteld gebruik Hallo dezelfde onderdelen die u kennisgemaakt in de vorige zelfstudie hello te[maximaal beschikbare virtuele machines maken](tutorial-availability-sets.md). Virtuele machines in een schaalset worden gemaakt in een beschikbaarheidsset ingesteld en verdeeld over logica probleem- en domeinen.

Virtuele machines worden gemaakt als nodig in een schaalset. U automatisch schalen regels toocontrol definiëren hoe en wanneer virtuele machines worden toegevoegd of verwijderd uit het Hallo-schaalset. Deze regels kunnen activeren op basis van metrische gegevens zoals CPU-belasting, geheugengebruik of netwerkverkeer.

Schaal wordt ingesteld voor ondersteuning van too1, 000 VM's wanneer u een installatiekopie van een Azure-platform. Voor productieworkloads, kunt u desgewenst te[maken van een aangepaste VM-installatiekopie](tutorial-custom-images.md). U kunt maken van too100 virtuele machines in een schaal instelt met behulp van een aangepaste installatiekopie.


## <a name="create-an-app-tooscale"></a>Maken van een app-tooscale
Voor gebruik in productieomgevingen, kunt u desgewenst te[maken van een aangepaste VM-installatiekopie](tutorial-custom-images.md) waarin uw toepassing geïnstalleerd en geconfigureerd. Voor deze zelfstudie kunt aanpassen Hallo die VM 's op de eerste opstarten tooquickly een schaal instelt in actie zien.

In een vorige zelfstudie hebt u geleerd [hoe toocustomize virtuele Linux-machine op de eerste keer opstarten](tutorial-automate-vm-deployment.md) met cloud-init. U kunt dezelfde cloud init configuration file tooinstall NGINX Hallo en uitvoeren van een eenvoudige 'Hallo wereld' Node.js-app. 

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


## <a name="create-a-scale-set"></a>Maken van een schaalset
Voordat u een schaalset maken kunt, maakt u een resourcegroep met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupScaleSet* in Hallo *eastus* locatie:

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

Maak nu de schaal van een virtuele machine in te stellen [az vmss maken](/cli/azure/vmss#create). Hallo volgende voorbeeld wordt een set met de naam scale *myScaleSet*Hallo cloud init bestand toocustomize Hallo VM gebruikt en SSH-sleutels worden gegenereerd als deze nog niet bestaan:

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

Het duurt enkele minuten toocreate en configureer alle Hallo scale set resources en virtuele machines. Er zijn achtergrondtaken die toorun verder gaat nadat hello Azure CLI keert u terug toohello prompt. Het is mogelijk een andere paar minuten voordat u toegang hebt tot Hallo-app.


## <a name="allow-web-traffic"></a>Webverkeer toestaan
Een load balancer is automatisch als onderdeel van Hallo virtuele-machineschaalset gemaakt. Hallo load balancer wordt verkeer over een reeks gedefinieerde virtuele machines met regels voor load balancer. U kunt meer informatie over de load balancer concepten en configuratie in de volgende zelfstudie Hallo, [hoe tooload balans vinden tussen virtuele machines in Azure](tutorial-load-balancer.md).

tooallow verkeer tooreach Hallo web-app, maakt u een regel met [az network Load Balancer-regel maken](/cli/azure/network/lb/rule#create). Hallo volgende voorbeeld maakt u een regel met naam *myLoadBalancerRuleWeb*:

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a>Uw app testen
toosee uw Node.js-app op Hallo web verkrijgen Hallo openbare IP-adres van de load balancer met [az netwerk openbare ip-weergeven](/cli/azure/network/public-ip#show). Hallo volgende voorbeeld Hallo IP-adres krijgt voor *myScaleSetLBPublicIP* gemaakt als onderdeel van het Hallo-schaalset:

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

Voer Hallo openbaar IP-adres in de webbrowser tooa. Hallo-app wordt weergegeven, inclusief Hallo hostnaam Hallo VM die Hallo load balancer gedistribueerde verkeer naar:

![Actieve Node.js-app](./media/tutorial-create-vmss/running-nodejs-app.png)

toosee hello schaal instellen in actie, u kunt force vernieuwen uw web browser toosee Hallo load balancer verkeer verdelen over alle Hallo virtuele machines waarop uw app wordt uitgevoerd.


## <a name="management-tasks"></a>Beheertaken
Gedurende de levenscyclus van de Hallo van Hallo scale is ingesteld, moet u mogelijk toorun een of meer beheertaken. U kunt bovendien toocreate scripts die verschillende lifecycle-taken automatiseren. Hello Azure CLI 2.0 biedt een snelle manier toodo deze taken. Hier volgen enkele algemene taken.

### <a name="view-vms-in-a-scale-set"></a>Weergave virtuele machines in een schaalset
tooview een lijst met virtuele machines die worden uitgevoerd in uw scale ingesteld, gebruikt u [az vmss lijstexemplaren](/cli/azure/vmss#list-instances) als volgt:

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a>Vergroten of verkleinen van VM-exemplaren
toosee hello aantal exemplaren van u momenteel hebt in een schaal ingesteld, gebruikt u [az vmss weergeven](/cli/azure/vmss#show) en query's uitvoeren op *sku.capacity*:

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

U kunt vervolgens handmatig vergroten of verkleinen Hallo aantal virtuele machines in Hallo schaal in te stellen [az vmss scale](/cli/azure/vmss#scale). Hallo volgende voorbeeld wordt Hallo aantal virtuele machines in te stellen schaal*5*:

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

Regels voor automatisch schalen kunt u definiëren hoe tooscale omhoog of omlaag Hallo aantal VM's in uw scale ingesteld in antwoord toodemand zoals netwerkverkeer of CPU-gebruik. Deze regels kunnen op dit moment kunnen niet worden ingesteld in de Azure CLI 2.0. Gebruik Hallo [Azure-portal](https://portal.azure.com) tooconfigure automatisch schalen.

### <a name="get-connection-info"></a>Verbindingsgegevens ophalen
verbindingsgegevens tooobtain over VM's in uw schaalsets hello, gebruik [az vmss lijst--verbinding-Instantiegegevens](/cli/azure/vmss#list-instance-connection-info). Met deze opdracht levert Hallo openbaar IP-adres en poort voor elke virtuele machine waarmee u tooconnect met SSH:

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a>Gegevensschijven met schaalsets gebruiken
U kunt maken en gebruiken van gegevensschijven met-schaalsets. In een vorige zelfstudie hebt u geleerd hoe te[Azure beheren schijven](tutorial-manage-disks.md) dat overzichten Hallo best practices en verbeterde prestaties voor het bouwen van apps op gegevensschijven in plaats van Hallo OS-schijf.

### <a name="create-scale-set-with-data-disks"></a>Schaalset met gegevensschijven maken
toocreate een schaal instellen en gegevensschijven, koppel toevoegen Hallo `--data-disk-sizes-gb` parameter toohello [az vmss maken](/cli/azure/vmss#create) opdracht. Hallo volgende voorbeeld wordt een instellen met schaal *50*Gb gegevensschijven gekoppeld tooeach exemplaar:

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

Wanneer instanties zijn verwijderd uit een schaalset, worden ook eventuele gekoppelde gegevensschijven verwijderd.

### <a name="add-data-disks"></a>Gegevensschijven toevoegen
tooadd een tooinstances gegevens schijf in uw scale instellen, gebruikt u [az vmss schijf koppelen](/cli/azure/vmss/disk#attach). Hallo volgende voorbeeld wordt een *50*Gb schijf tooeach exemplaar:

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a>Loskoppelen van gegevensschijven
tooremove een tooinstances gegevens schijf in uw scale instellen, gebruikt u [az vmss schijf loskoppelen](/cli/azure/vmss/disk#detach). Hallo volgende voorbeeld wordt verwijderd Hallo gegevensschijf met LUN *2* van elk exemplaar:

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie maakt u een virtuele-machineschaalset gemaakt. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Cloud-init toocreate een tooscale app gebruiken
> * Maken van een virtuele-machineschaalset
> * Vergroten of verkleinen Hallo aantal exemplaren in een schaalset
> * Verbindingsgegevens voor scale set exemplaren weergeven
> * Gegevensschijven in een schaalset gebruiken

De volgende zelfstudie toolearn toohello voor vooraf informatie over taakverdeling concepten voor virtuele machines.

> [!div class="nextstepaction"]
> [Load balance virtuele machines](tutorial-load-balancer.md)