---
title: aaaUse hello Azure Docker VM-extensie Hello Azure CLI 1.0 | Microsoft Docs
description: Informatie over hoe toouse Hallo Docker VM-extensie tooquickly en veilig implementeert een Docker-omgeving in Azure met behulp van Resource Manager-sjablonen.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2133cdb1af741fe30093910fae5c3b2c91e8d5fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension-with-hello-azure-cli-10"></a>Maakt een Docker-omgeving in Azure met behulp van Docker VM-extensie voor Hallo Hello Azure CLI 1.0
Docker is een populair containerbeheer en installatiekopieën platform waarmee u tooquickly werken met containers op Linux (en ook Windows). In Azure zijn er verschillende manieren waarop u Docker volgens tooyour behoeften kunt implementeren. Dit artikel is gericht op het gebruik van Hallo Docker VM-extensie en Azure Resource Manager-sjablonen. 

Zie voor meer informatie over Hallo verschillende implementatiemethoden, inclusief het gebruik van Docker-Machine en de Azure-Container Services Hallo artikelen te volgen:

* tooquickly prototype een app, kunt u één Docker-host met behulp van [Docker-Machine](docker-machine.md).
* Voor grotere, stabiele omgevingen, kunt u hello Azure Docker VM-extensie, dat ook wordt ondersteund [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate consistente containerimplementaties. Dit artikel gegevens met behulp van hello Azure Docker VM-extensie.
* toobuild gereed is voor productie, schaalbare omgevingen die extra hulpprogramma's voor planning en beheer bieden, u kunt een [Docker Swarm-cluster op Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 1.0](#azure-docker-vm-extension-overview) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](dockerextension.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel 

## <a name="azure-docker-vm-extension-overview"></a>Overzicht van Azure Docker VM-extensie
Hello Azure Docker VM-extensie installeert en configureert u het Hallo Docker-daemon, Docker-client en Docker Compose in uw virtuele Linux-machine (VM). U hebt meer controle en functies dan gewoon met behulp van Docker-Machine of maken van Hallo Docker-host met behulp van hello Azure Docker VM-extensie. Deze aanvullende functies, zoals [Docker Compose](https://docs.docker.com/compose/overview/), zorg hello Azure Docker VM-extensie is geschikt voor krachtiger developer- of productieomgevingen.

Azure Resource Manager-sjablonen definiëren Hallo volledige structuur van uw omgeving. Sjablonen kunnen u toocreate en bronnen zoals Hallo Docker host virtuele machines, opslag, op rollen gebaseerde toegangsbeheer (RBAC) en diagnostische gegevens configureren. U kunt deze sjablonen toocreate extra implementaties op een consistente manier hergebruiken. Zie voor meer informatie over Azure Resource Manager en sjablonen [overzicht van Resource Manager](../../azure-resource-manager/resource-group-overview.md). 

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a>Een sjabloon met hello Azure Docker VM-extensie implementeren
Laten we gebruik van een bestaande sjabloon Quick Start-toocreate een Ubuntu VM die gebruikmaakt van hello Azure Docker VM-extensie tooinstall en Hallo Docker host configureren. U kunt hier Hallo sjabloon weergeven: [eenvoudige implementatie van een VM Ubuntu met Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). 

U moet Hallo [nieuwste Azure CLI](../../cli-install-nodejs.md) geïnstalleerd en geregistreerd in het Hallo-Resource Manager-modus als volgt gebruiken:

```azurecli
azure config mode arm
```

Hallo-sjabloon met gebruik van Azure CLI, geven Hallo sjabloon URI Hallo implementeren. Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *westus* locatie. Uw eigen Resourcegroepnaam en locatie als volgt gebruiken:

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Hallo prompts tooname beantwoord uw storage-account, een gebruikersnaam en wachtwoord, en bieden een DNS-naam. Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for hello following parameters
newStorageAccountName: mystorageaccount
adminUsername: azureuser
adminPassword: P@ssword!
dnsNameForPublicIP: mypublicidns
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

Hello Azure CLI retourneert u toohello prompt na slechts enkele seconden, maar de Docker-host wordt nog steeds gemaakt en geconfigureerd door hello Azure Docker VM-extensie. Het duurt enkele minuten duren voordat Hallo implementatie toofinish. U kunt details zien over Hallo Docker host de status van Hallo `azure vm show` opdracht.

Hallo volgende voorbeeld controleert Hallo status van virtuele machine met de naam Hallo *myDockerVM* (de standaardnaam van de sjabloon Hallo Hallo - deze naam niet wijzigen) in de resourcegroep Hallo met de naam *myResourceGroup*. Geef de naam Hallo van Hallo-resourcegroep die u hebt gemaakt in de voorgaande stap Hallo:

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

uitvoer van Hallo Hallo `azure vm show` is vergelijkbaar toohello voorbeeld van de volgende opdracht:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myDockerVM"
+ Looking up hello NIC "myVMNicD"
+ Looking up hello public ip "myPublicIPD"
data:    Id                              :/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Compute/virtualMachines/MyDockerVM
data:    ProvisioningState               :Succeeded
data:    Name                            :MyDockerVM
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
[...]
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-D3-95
data:          Provisioning State        :Succeeded
data:          Name                      :myVMNicD
data:          Location                  :westus
data:            Public IP address       :13.91.107.235
data:            FQDN                    :mypublicdns.westus.cloudapp.azure.com
data:
data:    Diagnostics Instance View:
info:    vm show command OK
```

Aan de bovenkant van de Hallo van Hallo uitvoer, ziet u Hallo **ProvisioningState** Hallo VM. Wanneer u ziet nu *geslaagd*, Hallo-implementatie is voltooid en kunt u SSH toohello VM.

Naar einde van Hallo-uitvoer, Hallo *FQDN* Hallo volledig gekwalificeerde domeinnaam van uw Docker-host wordt weergegeven. Deze FDQN-naam is die u gebruikt tooSSH tooyour Docker-host in de resterende stappen Hallo.

## <a name="deploy-your-first-nginx-container"></a>Uw eerste nginx-container implementeren
Eenmaal Hallo-implementatie is voltooid, SSH tooyour nieuwe Docker-host van de lokale computer. Voer uw eigen gebruikersnaam en de FQDN-naam als volgt:

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
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

toosee uw container in actie, open een webbrowser omhoog en Voer Hallo FQDN-naam van de Docker-host:

![Actieve ngnix container](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Azure Docker VM-sjabloon uitbreidingsverwijzing
het vorige voorbeeld Hallo maakt gebruik van een bestaande Quick Start-sjabloon. U kunt ook hello Azure Docker VM-extensie implementeren met uw eigen Resource Manager-sjablonen. toodo toevoegen dus Hallo tooyour Resource Manager-sjablonen te volgen, Hallo definiëren *vmName* van uw virtuele machine op de juiste wijze:

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
    "typeHandlerVersion": "1.1",
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

