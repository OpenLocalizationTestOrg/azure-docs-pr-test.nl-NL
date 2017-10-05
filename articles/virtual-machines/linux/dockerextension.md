---
title: Gebruik de Azure Docker VM-extensie | Microsoft Docs
description: Informatie over het gebruik van de Docker-VM-extensie voor het snel en veilig implementeren van een Docker-omgeving in Azure met behulp van Resource Manager-sjablonen en Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 63d0d80999fd57d014c74d5c6aef3733ec2afe85
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-docker-environment-in-azure-using-the-docker-vm-extension"></a>Maakt een Docker-omgeving in Azure met behulp van de Docker-VM-extensie
Docker is een populair containerbeheer en installatiekopieën platform waarmee u snel werken met containers op Linux. In Azure zijn er verschillende manieren waarop u kunt Docker implementeren volgens uw behoeften. Dit artikel is gericht op het gebruik van de Docker-VM-extensie en Azure Resource Manager-sjablonen met de Azure CLI 2.0. U kunt deze stappen ook uitvoeren met de [Azure CLI 1.0](dockerextension-nodejs.md).

## <a name="azure-docker-vm-extension-overview"></a>Overzicht van Azure Docker VM-extensie
De virtuele machine in Azure Docker-extensie installeert en configureert u de Docker-daemon, Docker-client en Docker Compose in uw virtuele Linux-machine (VM). U hebt meer controle en functies dan gewoon met behulp van Docker-Machine of maken van de Docker-host met behulp van de virtuele machine in Azure Docker-extensie. Deze aanvullende functies, zoals [Docker Compose](https://docs.docker.com/compose/overview/), zorg dat de virtuele machine in Azure Docker-extensie is geschikt voor krachtiger developer- of productieomgevingen.

Zie voor meer informatie over de verschillende implementatiemethoden, met behulp van Docker-Machine en Services van Azure-Container, inclusief de volgende artikelen:

* Snel prototype een app kunt u één Docker-host met behulp van [Docker-Machine](docker-machine.md).
* Gereed voor productie, schaalbare omgevingen die aanvullende plannings- en hulpprogramma's bieden bouwen, kunt u implementeren een [Docker Swarm-cluster op Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="deploy-a-template-with-the-azure-docker-vm-extension"></a>Een sjabloon met de extensie Azure Docker VM implementeren
We gebruiken een bestaande sjabloon voor de Quick Start voor het maken van een Ubuntu VM die gebruikmaakt van de virtuele machine in Azure Docker-uitbreiding installeren en configureren van de Docker-host. U kunt de sjabloon hier weergeven: [eenvoudige implementatie van een VM Ubuntu met Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). U moet de meest recente [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in het gebruik van een Azure-account [az aanmelding](/cli/azure/#login).

Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create). Het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroup* in de *westus* locatie:

```azurecli
az group create --name myResourceGroup --location westus
```

Vervolgens implementeert u een virtuele machine met [az implementatie maken](/cli/azure/group/deployment#create) waarin de Azure Docker VM-extensie van [deze Azure Resource Manager-sjabloon op GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Uw eigen waarden opgeven voor *newStorageAccountName*, *adminUsername*, *adminPassword*, en *dnsNameForPublicIP* als volgt:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Het duurt enkele minuten duren voordat de implementatie is voltooid. Zodra de implementatie is voltooid, [verplaatsen naar de volgende stap](#deploy-your-first-nginx-container) naar SSH met uw virtuele machine. 

Voeg desgewenst in plaats daarvan om terug te beheren op de vraag en kunt de implementatie op de achtergrond voortgezet, de `--no-wait` vlag naar de voorgaande opdracht. Dit proces kunt u andere taken uitvoeren in de CLI tijdens de implementatie gedurende enkele minuten blijft. 

Vervolgens kunt u meer informatie over de hoststatus Docker met bekijken [az vm weergeven](/cli/azure/vm#show). Het volgende voorbeeld controleert de status van de virtuele machine met de naam *myDockerVM* (de standaardnaam van de sjabloon - geen deze naam niet wijzigen) in de resourcegroep met de naam *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Wanneer deze opdracht retourneert *geslaagd*, de implementatie is voltooid en kunt u SSH naar de virtuele machine in de volgende stap.

## <a name="deploy-your-first-nginx-container"></a>Uw eerste nginx-container implementeren
Gebruiken om de details van uw virtuele machine, met inbegrip van de DNS-naam te geven `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`. SSH kunt uitvoeren naar uw nieuwe Docker hosten van uw lokale computer als volgt:

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

Wanneer aangemeld bij de Docker-host, gaan we een nginx-container te uitvoeren:

```bash
sudo docker run -d -p 80:80 nginx
```

De uitvoer is vergelijkbaar met het volgende voorbeeld wordt de nginx-installatiekopie gedownload en een container gestart:

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

Controleer de status van de containers die wordt uitgevoerd op uw host Docker als volgt:

```bash
sudo docker ps
```

De uitvoer is vergelijkbaar met het volgende voorbeeld, waaruit blijkt dat de nginx-container actief is en TCP-poorten 80 en 443 en ernaar worden doorgestuurd:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

De container in actie zien, opent u een webbrowser en voer de DNS-naam van de Docker-host:

![Actieve ngnix container](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Azure Docker VM-sjabloon uitbreidingsverwijzing
Het vorige voorbeeld maakt gebruik van een bestaande Quick Start-sjabloon. U kunt ook de Azure Docker VM-extensie implementeren met uw eigen Resource Manager-sjablonen. Om dit te doen, kunt u het volgende toevoegen aan de Resource Manager-sjablonen, definiëren de `vmName` van uw virtuele machine op de juiste wijze:

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.*",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

U vindt meer gedetailleerde stapsgewijze instructies over het gebruik van Resource Manager-sjablonen door te lezen [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

## <a name="next-steps"></a>Volgende stappen
U kunt desgewenst [de Docker-daemon TCP-poort configureren](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), begrijpen [Docker-beveiliging](https://docs.docker.com/engine/security/security/), of met behulp van containers implementeren [Docker Compose](https://docs.docker.com/compose/overview/). Zie voor meer informatie over de Azure Docker VM-extensie zichzelf, het [GitHub project](https://github.com/Azure/azure-docker-extension/).

Lees meer informatie over de extra Docker implementatie-opties in Azure:

* [Docker-Machine met het Azure-stuurprogramma gebruiken](docker-machine.md)  
* [Aan de slag met Docker en opstellen om te definiëren en een toepassing met meerdere container uitvoert op een virtuele machine van Azure](docker-compose-quickstart.md).
* [Een Azure Container Service-cluster implementeren](../../container-service/dcos-swarm/container-service-deployment.md)

