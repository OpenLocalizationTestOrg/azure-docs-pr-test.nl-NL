---
title: aaaUse hello Azure Docker VM-extensie | Microsoft Docs
description: Meer informatie over hoe toouse Hallo Docker VM-extensie tooquickly en veilig implementeert een Docker-omgeving in Azure met behulp van Resource Manager-sjablonen en hello Azure CLI 2.0
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
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a>Maakt een Docker-omgeving in Azure met behulp van Hallo Docker VM-extensie
Docker is een populair containerbeheer en installatiekopieën platform waarmee u tooquickly werken met containers op Linux. In Azure zijn er verschillende manieren waarop u Docker volgens tooyour behoeften kunt implementeren. Dit artikel is gericht op het gebruik van Hallo Docker VM-extensie en Azure Resource Manager-sjablonen met hello Azure CLI 2.0. U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](dockerextension-nodejs.md).

## <a name="azure-docker-vm-extension-overview"></a>Overzicht van Azure Docker VM-extensie
Hello Azure Docker VM-extensie installeert en configureert u het Hallo Docker-daemon, Docker-client en Docker Compose in uw virtuele Linux-machine (VM). U hebt meer controle en functies dan gewoon met behulp van Docker-Machine of maken van Hallo Docker-host met behulp van hello Azure Docker VM-extensie. Deze aanvullende functies, zoals [Docker Compose](https://docs.docker.com/compose/overview/), zorg hello Azure Docker VM-extensie is geschikt voor krachtiger developer- of productieomgevingen.

Zie voor meer informatie over Hallo verschillende implementatiemethoden, inclusief het gebruik van Docker-Machine en de Azure-Container Services Hallo artikelen te volgen:

* tooquickly prototype een app, kunt u één Docker-host met behulp van [Docker-Machine](docker-machine.md).
* toobuild gereed is voor productie, schaalbare omgevingen die extra hulpprogramma's voor planning en beheer bieden, u kunt een [Docker Swarm-cluster op Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a>Een sjabloon met hello Azure Docker VM-extensie implementeren
Laten we gebruik van een bestaande sjabloon Quick Start-toocreate een Ubuntu VM die gebruikmaakt van hello Azure Docker VM-extensie tooinstall en Hallo Docker host configureren. U kunt hier Hallo sjabloon weergeven: [eenvoudige implementatie van een VM Ubuntu met Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).

Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *westus* locatie:

```azurecli
az group create --name myResourceGroup --location westus
```

Vervolgens implementeert u een virtuele machine met [az implementatie maken](/cli/azure/group/deployment#create) waarin hello Azure Docker VM-extensie van [deze Azure Resource Manager-sjabloon op GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Uw eigen waarden opgeven voor *newStorageAccountName*, *adminUsername*, *adminPassword*, en *dnsNameForPublicIP* als volgt:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Het duurt enkele minuten duren voordat Hallo implementatie toofinish. Zodra het Hallo-implementatie is voltooid, [toonext stap verplaatsen](#deploy-your-first-nginx-container) tooSSH tooyour VM. 

Tooinstead return besturingselement toohello-prompt en laat Hallo implementatie blijven op de achtergrond hello, voegt u desgewenst Hallo `--no-wait` toohello opdracht vóór markering. Dit proces kunt u tooperform doorwerken in Hallo CLI tijdens het Hallo-implementatie blijft gedurende enkele minuten. 

Vervolgens kunt u meer informatie over de status van Hallo Docker-host met bekijken [az vm weergeven](/cli/azure/vm#show). Hallo volgende voorbeeld controleert Hallo status van virtuele machine met de naam Hallo *myDockerVM* (de standaardnaam van de sjabloon Hallo Hallo - deze naam niet wijzigen) in de resourcegroep Hallo met de naam *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Wanneer deze opdracht retourneert *geslaagd*, Hallo-implementatie is voltooid en kunt u SSH toohello VM in Hallo volgende stap.

## <a name="deploy-your-first-nginx-container"></a>Uw eerste nginx-container implementeren
tooview details van uw virtuele machine, inclusief Hallo DNS-naam gebruiken `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`. SSH tooyour nieuwe Docker hosten van uw lokale computer als volgt:

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

Wanneer toohello aangemeld met Docker-host, gaan we een nginx-container te uitvoeren:

```bash
sudo docker run -d -p 80:80 nginx
```

Hallo-uitvoer is vergelijkbaar toohello na voorbeeld Hallo nginx installatiekopie gedownload en een container gestart:

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

Controleer de status Hallo van Hallo-containers die zijn uitgevoerd op uw host Docker als volgt:

```bash
sudo docker ps
```

Hallo-uitvoer is vergelijkbaar toohello voorbeeld te volgen, die Hallo nginx-container met actief is en TCP-poorten 80 en 443 en ernaar worden doorgestuurd:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

toosee uw container in actie, open een webbrowser boven en Voer Hallo DNS-naam van de Docker-host:

![Actieve ngnix container](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Azure Docker VM-sjabloon uitbreidingsverwijzing
het vorige voorbeeld Hallo maakt gebruik van een bestaande Quick Start-sjabloon. U kunt ook hello Azure Docker VM-extensie implementeren met uw eigen Resource Manager-sjablonen. toodo toevoegen dus Hallo tooyour Resource Manager-sjablonen te volgen, Hallo definiëren `vmName` van uw virtuele machine op de juiste wijze:

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
U kunt desgewenst te[hello Docker-daemon TCP-poort configureren](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), begrijpen [Docker beveiliging](https://docs.docker.com/engine/security/security/), of met behulp van containers implementeren [Docker Compose](https://docs.docker.com/compose/overview/). Zie voor meer informatie over hello Azure Docker VM-extensie zichzelf Hallo [GitHub project](https://github.com/Azure/azure-docker-extension/).

Lees meer informatie over Hallo aanvullende Docker implementatieopties in Azure:

* [Docker-Machine Hello Azure stuurprogramma gebruiken](docker-machine.md)  
* [Aan de slag met Docker Compose toodefine en een toepassing met meerdere container uitvoert op een virtuele machine van Azure](docker-compose-quickstart.md).
* [Een Azure Container Service-cluster implementeren](../../container-service/dcos-swarm/container-service-deployment.md)

