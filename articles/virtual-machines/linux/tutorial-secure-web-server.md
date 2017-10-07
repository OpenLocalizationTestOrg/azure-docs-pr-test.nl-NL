---
title: een webserver met SSL-in Azure certificaten aaaSecure | Microsoft Docs
description: Meer informatie over hoe toosecure hello NGINX-webserver met SSL-certificaten op een Linux VM in Azure
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
ms.date: 07/17/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d3a62d77ac05c9aa2a44356b7c8e44cb485b81aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a>Een webserver met SSL-certificaten op een virtuele Linux-machine in Azure beveiligen
toosecure webservers, een certificaat Later SSL (Secure Sockets) kan worden gebruikt tooencrypt internetverkeer. Deze SSL-certificaten kunnen worden opgeslagen in Azure Sleutelkluis en beveiligde implementaties van certificaten tooLinux virtuele machines (VM's) in Azure toestaan. In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Maken van een Azure Sleutelkluis
> * Upload een certificaat toohello Sleutelkluis of genereren
> * Een virtuele machine maken en Hallo NGINX-webserver installeren
> * Hallo certificaat invoeren in Hallo VM en NGINX configureren met een SSL-binding

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).  


## <a name="overview"></a>Overzicht
Azure Sleutelkluis beschermt cryptografische sleutels en geheimen, zoals certificaten of wachtwoorden. Sleutelkluis helpt Hallo certificate management stroomlijnen en kunt u toomaintain beheer van sleutels die toegang hebben tot deze certificaten. U kunt een zelfondertekend certificaat in de Sleutelkluis maken of een bestaande, vertrouwd certificaat dat u al bezit uploaden.

In plaats van met een aangepaste VM-installatiekopie die certificaten bevat standaard uitbreidbaar module u certificaten kunt invoeren in een actieve virtuele machine. Dit proces zorgt ervoor dat de meest recente certificaten Hallo tijdens de implementatie op een webserver zijn geïnstalleerd. Als u vernieuwen of vervangen van een certificaat, hebt u niet ook toocreate een nieuwe aangepaste VM-installatiekopie. Hallo nieuwste certificaten worden automatisch ingevoegd als u extra virtuele machines maken. Tijdens het hele proces hello, Hallo certificaten nooit laat hello Azure-platform of beschikbaar worden gesteld in een script, opdrachtregel geschiedenis of sjabloon.


## <a name="create-an-azure-key-vault"></a>Maken van een Azure Sleutelkluis
Voordat u certificaten en een Sleutelkluis maken kunt, maakt u een resourcegroep met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupSecureWeb* in Hallo *eastus* locatie:

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

Maak vervolgens een Sleutelkluis met [az keyvault maken](/cli/azure/keyvault#create) en inschakelen voor gebruik wanneer u een virtuele machine implementeert. Elke Sleutelkluis moet een unieke naam hebben en moet alle kleine letters. Vervang  *<mykeyvault>*  in het volgende voorbeeld met de naam van uw eigen unieke Sleutelkluis Hallo:

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>Een certificaat genereren en opslaan in de Sleutelkluis
Voor gebruik in productieomgevingen, moet u een geldig certificaat dat is ondertekend door een vertrouwde provider met importeren [az keyvault certificaat importeren](/cli/azure/certificate#import). Voor deze zelfstudie hello volgende voorbeeld ziet u hoe u een zelfondertekend certificaat met genereren [az keyvault-certificaat maken](/cli/azure/certificate#create) die gebruikmaakt van Hallo-standaardbeleid certificaat:

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a>Een certificaat voor gebruik met een virtuele machine voorbereiden
toouse hello certificaat tijdens Hallo VM proces voor het maken, verkrijgen Hallo-ID van uw certificaat met [az keyvault lijst-versies van het clientgeheim](/cli/azure/keyvault/secret#list-versions). Hallo-certificaat met converteren [az vm indeling-geheim](/cli/azure/vm#format-secret). Hallo volgt toegewezen Hallo-uitvoer van deze opdrachten toovariables voor eenvoudig te gebruiken in Hallo volgende stappen:

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a>Maken van een cloud-init config toosecure NGINX
[Cloud-init](https://cloudinit.readthedocs.io) is een veelgebruikte methode toocustomize zoals deze wordt opgestart voor Hallo eerst een Linux-VM. U kunt de cloud init tooinstall pakketten gebruiken en schrijven van bestanden, of tooconfigure gebruikers en beveiliging. Cloud-init wordt uitgevoerd tijdens het opstartproces hello, er zijn geen extra stappen of agents tooapply uw configuratie is vereist.

Wanneer u maakt een virtuele machine, certificaten en sleutels worden opgeslagen in Hallo beveiligd */var/lib/waagent/* directory. tooautomate toe te voegen Hallo certificaat toohello VM en cloud-init Hallo webserver configureren gebruiken. In dit voorbeeld we installeren en configureren van Hallo NGINX-webserver. U kunt Hallo dezelfde tooinstall verwerken en Apache configureren. 

Maak een bestand met de naam *cloud-init-web-server.txt* en plakken Hallo volgende configuratie:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
      }
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
```

### <a name="create-a-secure-vm"></a>Een beveiligde virtuele machine maken
Maak nu een virtuele machine met [az vm maken](/cli/azure/vm#create). Hallo certificaatgegevens wordt geïnjecteerd uit Sleutelkluis Hello `--secrets` parameter. U doorgeeft in Hallo cloud init-config Hallo `--custom-data` parameter:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-web-server.txt \
    --secrets "$vm_secret"
```

Het duurt enkele minuten voordat Hallo VM toobe gemaakt, hello-pakketten tooinstall en Hallo app toostart. Wanneer Hallo VM is gemaakt, noteer Hallo `publicIpAddress` weergegeven door hello Azure CLI. Dit adres wordt gebruikt tooaccess uw site in een webbrowser.

virtuele machine, open poort 443 van Hallo Internet met voor secure web verkeer tooreach tooallow [az vm open poort](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a>Test Hallo beveiligde web-app
Nu kunt u een webbrowser openen en voer *https://<publicIpAddress>*  in de adresbalk Hallo. Geef uw eigen openbare IP-adres uit Hallo VM proces maken. Beveiligingswaarschuwing Hallo accepteren als u een zelfondertekend certificaat gebruikt:

![Beveiligingswaarschuwing voor web browser accepteren](./media/tutorial-secure-web-server/browser-warning.png)

Uw beveiligde NGINX-site wordt vervolgens weergegeven zoals in het volgende voorbeeld Hallo:

![Actief beveiligde NGINX-site weergeven](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie maakt beveiligd u een NGINX-webserver met een SSL-certificaat dat is opgeslagen in Azure Sleutelkluis. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Maken van een Azure Sleutelkluis
> * Upload een certificaat toohello Sleutelkluis of genereren
> * Een virtuele machine maken en Hallo NGINX-webserver installeren
> * Hallo certificaat invoeren in Hallo VM en NGINX configureren met een SSL-binding

Volg deze link toosee vooraf gemaakte virtuele machine scriptvoorbeelden.

> [!div class="nextstepaction"]
> [Windows virtuele machine scriptvoorbeelden](./cli-samples.md)