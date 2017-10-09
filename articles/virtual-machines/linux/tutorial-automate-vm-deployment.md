---
title: aaaCustomize een Linux-VM voor eerst wordt opgestart in Azure | Microsoft Docs
description: Meer informatie over hoe toouse cloud-init en Sleutelkluis toocustomze virtuele Linux-machines Hallo eerste keer dat ze worden opgestart in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 280189723ac0205226f9c0068bd605da13249ace
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a>Hoe toocustomize virtuele Linux-machine op de eerste keer opstarten
In een vorige zelfstudie hebt u geleerd hoe tooSSH tooa virtuele machine (VM) en NGINX handmatig installeren. toocreate virtuele machines op een snelle en consistente manier, een vorm van automatisering is doorgaans gewenste. Een algemene methode toocustomize een VM op de eerste keer opstarten is toouse [cloud init](https://cloudinit.readthedocs.io). In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Maken van een cloud-init-configuratiebestand
> * Een virtuele machine die gebruikmaakt van een cloud-init-bestand maken
> * Een actieve Node.js-app weergeven na Hallo die virtuele machine wordt gemaakt
> * Sleutelkluis toosecurely store certificaten gebruiken
> * Beveiligde implementaties van NGINX met cloud-init automatiseren


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).  



## <a name="cloud-init-overview"></a>Cloud-init-overzicht
[Cloud-init](https://cloudinit.readthedocs.io) is een veelgebruikte methode toocustomize zoals deze wordt opgestart voor Hallo eerst een Linux-VM. U kunt de cloud init tooinstall pakketten gebruiken en schrijven van bestanden, of tooconfigure gebruikers en beveiliging. Cloud-init wordt uitgevoerd tijdens het opstartproces hello, er zijn geen extra stappen of agents tooapply uw configuratie is vereist.

Cloud-init werkt ook via distributies. Bijvoorbeeld, u niet gebruikt **apt get-installatie** of **yum installeren** tooinstall een pakket. In plaats daarvan kunt u een lijst met pakketten tooinstall definiëren. Hallo systeemeigen pakket beheerprogramma cloud init automatisch gebruikt voor Hallo distro die u selecteert.

We kunnen werken met onze partners tooget cloud-init opgenomen en werken in dat ze tooAzure bieden Hallo-installatiekopieën. Hallo volgende tabel geeft een overzicht van de huidige cloud init-beschikbaarheid Hallo op Azure-platform installatiekopieën:

| Alias | Uitgever | Aanbieding | SKU | Versie |
|:--- |:--- |:--- |:--- |:--- |:--- |
| UbuntuLTS |Canonical |UbuntuServer |16.04 TNS |meest recente |
| UbuntuLTS |Canonical |UbuntuServer |14.04.5-LTS |meest recente |
| CoreOS |CoreOS |CoreOS |Stabiel |meest recente |


## <a name="create-cloud-init-config-file"></a>Cloud-init-configuratiebestand maken
toosee cloud-init in actie, maak een VM die NGINX installeert en een eenvoudige 'Hallo wereld' Node.js-app wordt uitgevoerd. Hallo na configuratie voor cloud-init vereist hello-pakketten worden geïnstalleerd, maakt u een Node.js-app en vervolgens initialiseren en Hallo-app wordt gestart.

Maak een bestand met de naam in uw huidige shell *cloud init.txt* en plakken Hallo configuratie. Bijvoorbeeld, Hallo-bestand in Hallo Cloud-Shell op uw lokale machine niet maken. U kunt een editor die u wilt gebruiken. Voer `sensible-editor cloud-init.txt` toocreate Hallo bestand en een overzicht van beschikbare editors. Zorg ervoor dat Hallo hele cloud-init-bestand correct is gekopieerd, met name Hallo eerste regel:

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

Zie voor meer informatie over configuratieopties voor cloud-init [cloud init config voorbeelden](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).

## <a name="create-virtual-machine"></a>Virtuele machine maken
Voordat u een virtuele machine maken kunt, maakt u een resourcegroep met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupAutomate* in Hallo *eastus* locatie:

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

Maak nu een virtuele machine met [az vm maken](/cli/azure/vm#create). Gebruik Hallo `--custom-data` parameter toopass in uw cloud-init-configuratiebestand. Hallo volledig pad toohello bieden *cloud init.txt* config als Hallo bestand buiten de huidige werkmap is opgeslagen. Hallo volgende voorbeeld wordt een virtuele machine met de naam *myAutomatedVM*:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Het duurt enkele minuten voordat Hallo VM toobe gemaakt, hello-pakketten tooinstall en Hallo app toostart. Er zijn achtergrondtaken die toorun verder gaat nadat hello Azure CLI keert u terug toohello prompt. Het is mogelijk een andere paar minuten voordat u toegang hebt tot Hallo-app. Wanneer Hallo VM is gemaakt, noteer Hallo `publicIpAddress` weergegeven door hello Azure CLI. Dit adres is gebruikte tooaccess hello Node.js-app via een webbrowser.

virtuele machine, open poort 80 van Hallo Internet met het web verkeer tooreach tooallow [az vm open poort](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a>Test-web-app
Nu kunt u een webbrowser openen en voer *http://<publicIpAddress>*  in de adresbalk Hallo. Geef uw eigen openbare IP-adres uit Hallo VM proces maken. Uw Node.js-app wordt weergegeven zoals in het volgende voorbeeld Hallo:

![Bekijk actieve NGINX-website](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a>Certificaten van de Sleutelkluis invoeren
Deze optionele sectie wordt beschreven hoe u veilig opslaan van certificaten in Azure Sleutelkluis en ze tijdens het Hallo-VM-implementatie te injecteren. In plaats van met een aangepaste installatiekopie met de Hallo certificaten standaard uitbreidbaar, in dit proces zorgt ervoor dat de meest recente certificaten Hallo tooa VM op de eerste keer opstarten zijn ingevoegd. Tijdens Hallo Hallo certificaat nooit verlaat hello Azure-platform of in een script, opdrachtregel geschiedenis of sjabloon wordt blootgesteld.

Azure Sleutelkluis beschermt cryptografische sleutels en geheimen, zoals certificaten of wachtwoorden. Sleutelkluis helpt Hallo Sleutelbeheer stroomlijnen en kunt u toomaintain beheer van sleutels die toegang tot en uw gegevens te versleutelen. Dit scenario maakt u kennis met enkele Sleutelkluis concepten toocreate en een certificaat gebruiken, maar is niet een volledig overzicht over het toouse Sleutelkluis.

Hallo stappen te volgen laten zien hoe u kunt:

- Maken van een Azure Sleutelkluis
- Upload een certificaat toohello Sleutelkluis of genereren
- Een geheim van Hallo certificaat tooinject in tooa VM maken
- Een virtuele machine maken en te ' injecteren ' hello certificaat

### <a name="create-an-azure-key-vault"></a>Maken van een Azure Sleutelkluis
Maak eerst een Sleutelkluis met [az keyvault maken](/cli/azure/keyvault#create) en inschakelen voor gebruik wanneer u een virtuele machine implementeert. Elke Sleutelkluis moet een unieke naam hebben en moet alle kleine letters. Vervang *mykeyvault* in het volgende voorbeeld met de naam van uw eigen unieke Sleutelkluis Hallo:

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a>Certificaat genereren en opslaan in de Sleutelkluis
Voor gebruik in productieomgevingen, moet u een geldig certificaat dat is ondertekend door een vertrouwde provider met importeren [az keyvault certificaat importeren](/cli/azure/keyvault/certificate#import). Voor deze zelfstudie hello volgende voorbeeld ziet u hoe u een zelfondertekend certificaat met genereren [az keyvault-certificaat maken](/cli/azure/keyvault/certificate#create) die gebruikmaakt van Hallo-standaardbeleid certificaat:

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a>Certificaat voor gebruik met de virtuele machine voorbereiden
toouse hello certificaat tijdens Hallo VM proces voor het maken, verkrijgen Hallo-ID van uw certificaat met [az keyvault lijst-versies van het clientgeheim](/cli/azure/keyvault/secret#list-versions). Hallo VM Hallo certificaat moet in een bepaalde opmaak tooinject converteren deze opstart, dus Hallo-certificaat met [az vm indeling-geheim](/cli/azure/vm#format-secret). Hallo volgt toegewezen Hallo-uitvoer van deze opdrachten toovariables voor eenvoudig te gebruiken in Hallo volgende stappen:

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a>Cloud-init config toosecure NGINX maken
Wanneer u maakt een virtuele machine, certificaten en sleutels worden opgeslagen in Hallo beveiligd */var/lib/waagent/* directory. tooautomate toe te voegen Hallo certificaat toohello VM en NGINX te configureren, kunt u een bijgewerkte cloud-init-configuratie van het vorige voorbeeld Hallo.

Maak een bestand met de naam *cloud-init-secured.txt* en plakken Hallo configuratie. Opnieuw als u Hallo Cloud-Shell, maakt Hallo cloud init-configuratiebestand er en niet op uw lokale computer. Gebruik `sensible-editor cloud-init-secured.txt` toocreate Hallo bestand en een overzicht van beschikbare editors. Zorg ervoor dat Hallo hele cloud-init-bestand correct is gekopieerd, met name Hallo eerste regel:

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
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
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
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-secure-vm"></a>Beveiligde virtuele machine maken
Maak nu een virtuele machine met [az vm maken](/cli/azure/vm#create). Hallo certificaatgegevens wordt geïnjecteerd uit Sleutelkluis Hello `--secrets` parameter. Zoals in het vorige voorbeeld hello, u ook doorgeven in de configuratie van cloud-init Hallo Hello `--custom-data` parameter:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-secured.txt \
    --secrets "$vm_secret"
```

Het duurt enkele minuten voordat Hallo VM toobe gemaakt, hello-pakketten tooinstall en Hallo app toostart. Er zijn achtergrondtaken die toorun verder gaat nadat hello Azure CLI keert u terug toohello prompt. Het is mogelijk een andere paar minuten voordat u toegang hebt tot Hallo-app. Wanneer Hallo VM is gemaakt, noteer Hallo `publicIpAddress` weergegeven door hello Azure CLI. Dit adres is gebruikte tooaccess hello Node.js-app via een webbrowser.

virtuele machine, open poort 443 van Hallo Internet met voor secure web verkeer tooreach tooallow [az vm open poort](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a>Test beveiligde web-app
Nu kunt u een webbrowser openen en voer *https://<publicIpAddress>*  in de adresbalk Hallo. Geef uw eigen openbare IP-adres uit Hallo VM proces maken. Beveiligingswaarschuwing Hallo accepteren als u een zelfondertekend certificaat gebruikt:

![Beveiligingswaarschuwing voor web browser accepteren](./media/tutorial-automate-vm-deployment/browser-warning.png)

Uw beveiligde NGINX-site en Node.js app wordt vervolgens weergegeven zoals in het volgende voorbeeld Hallo:

![Actief beveiligde NGINX-site weergeven](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie kunt u virtuele machines op de eerste keer opstarten met cloud-init geconfigureerd. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Maken van een cloud-init-configuratiebestand
> * Een virtuele machine die gebruikmaakt van een cloud-init-bestand maken
> * Een actieve Node.js-app weergeven na Hallo die virtuele machine wordt gemaakt
> * Sleutelkluis toosecurely store certificaten gebruiken
> * Beveiligde implementaties van NGINX met cloud-init automatiseren

Hoe gaan van de volgende zelfstudie toolearn toohello toocreate aangepaste VM-installatiekopieën.

> [!div class="nextstepaction"]
> [Aangepaste VM-installatiekopieën maken](./tutorial-custom-images.md)
