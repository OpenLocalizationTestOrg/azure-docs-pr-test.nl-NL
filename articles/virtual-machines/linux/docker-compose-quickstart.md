---
title: aaaUse Docker Compose op een Linux VM in Azure | Microsoft Docs
description: Hoe Hallo toouse Docker en opstellen op Linux virtuele machines met Azure CLI
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a>Ophalen met Docker en opstellen toodefine gestart en het uitvoeren van een toepassing met meerdere container in Azure
Met [opstellen](http://github.com/docker/compose), u een eenvoudige tekst bestand toodefine gebruikt een toepassing die bestaat uit meerdere Docker-containers. U film van uw toepassing in één opdracht dat alles werkt toodeploy uw gedefinieerde omgeving. Een voorbeeld: in dit artikel laat zien u hoe tooquickly ingesteld met een back-end een WordPress-blog MariaDB SQL-database op een Ubuntu VM. U kunt ook tooset opstellen om complexere toepassingen gebruiken.


## <a name="set-up-a-linux-vm-as-a-docker-host"></a>Instellen van een Linux-VM als Docker-host
U kunt verschillende Azure procedures en de beschikbare installatiekopieën of de Resource Manager-sjablonen gebruiken in hello Azure Marketplace toocreate een Linux-VM en ingesteld als een Docker-host. Zie bijvoorbeeld [hello Docker VM-extensie toodeploy met uw omgeving](dockerextension.md) tooquickly een Ubuntu VM Hello Azure Docker VM-extensie maken met behulp van een [snelstartsjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). 

Wanneer u Hallo Docker VM-extensie, uw virtuele machine is automatisch geconfigureerd als een Docker-host en Compose is al geïnstalleerd.


### <a name="create-docker-host-with-azure-cli-20"></a>Docker-host te maken met Azure CLI 2.0
Meest recente installatie Hallo [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u bij het gebruik van de Azure-account tooan [az aanmelding](/cli/azure/#login).

Maak eerst een resourcegroep voor uw omgeving Docker met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *westus* locatie:

```azurecli
az group create --name myResourceGroup --location westus
```

Vervolgens implementeert u een virtuele machine met [az implementatie maken](/cli/azure/group/deployment#create) waarin hello Azure Docker VM-extensie van [deze Azure Resource Manager-sjabloon op GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Uw eigen waarden opgeven voor *newStorageAccountName*, *adminUsername*, *adminPassword*, en *dnsNameForPublicIP*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Het duurt enkele minuten duren voordat Hallo implementatie toofinish. Zodra het Hallo-implementatie is voltooid, [toonext stap verplaatsen](#verify-that-compose-is-installed) tooSSH tooyour VM. 

Tooinstead return besturingselement toohello-prompt en laat Hallo implementatie blijven op de achtergrond hello, voegt u desgewenst Hallo `--no-wait` toohello opdracht vóór markering. Dit proces kunt u tooperform doorwerken in Hallo CLI tijdens het Hallo-implementatie blijft gedurende enkele minuten. Vervolgens kunt u meer informatie over de status van Hallo Docker-host met bekijken [az vm weergeven](/cli/azure/vm#show). Hallo volgende voorbeeld controleert Hallo status van virtuele machine met de naam Hallo *myDockerVM* (de standaardnaam van de sjabloon Hallo Hallo - deze naam niet wijzigen) in de resourcegroep Hallo met de naam *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Wanneer deze opdracht retourneert *geslaagd*, Hallo-implementatie is voltooid en kunt u SSH toohello VM in Hallo volgende stap.


## <a name="verify-that-compose-is-installed"></a>Controleren of Compose is geïnstalleerd
Zodra het Hallo-implementatie is voltooid, SSH tooyour nieuwe Docker host Hallo DNS-naam u hebt opgegeven tijdens de implementatie. U kunt `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview details van uw virtuele machine, met inbegrip van Hallo DNS-naam.

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

toocheck waaruit is geïnstalleerd op Hallo VM, Hallo volgende opdracht uitvoeren:

```bash
docker-compose --version
```

Ziet u uitvoer ziet te*docker compose 1.6.2, 4d 72027 bouwen*.

> [!TIP]
> Als u een andere methode toocreate een Docker-host gebruikt en tooinstall zelf samenstellen moet, Zie Hallo [documentatie opstellen](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).


## <a name="create-a-docker-composeyml-configuration-file"></a>Maak een docker-compose.yml-configuratiebestand
Vervolgens maakt u een `docker-compose.yml` bestand, dat slechts een configuratie-tekstbestand, toodefine hello Docker containers toorun op Hallo VM is. Hallo-bestand bevat Hallo installatiekopie toorun op elke container (of het mogelijk een build van een Dockerfile) nodig omgevingsvariabelen en afhankelijkheden, poorten en Hallo koppelingen tussen containers. Zie voor meer informatie over yml file-syntaxis, [opstellen bestandsverwijzing](https://docs.docker.com/compose/compose-file/).

Hallo maken *docker-compose.yml* als volgt:

```bash
touch docker-compose.yml
```

Gebruik uw favoriete text editor tooadd sommige toohello gegevensbestand. Hallo volgende voorbeeld wordt Hallo *vi* editor:

```bash
vi docker-compose.yml
```

Hallo voorbeeld te volgen in het tekstbestand plakken. Deze configuratie wordt gebruikt voor afbeeldingen van Hallo [DockerHub register](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (Hallo open-source weblog en inhoud management system) en een gekoppelde back-end MariaDB SQL-database. Voer uw eigen *MYSQL_ROOT_PASSWORD* als volgt:

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-hello-containers-with-compose"></a>Start Hallo containers met opstellen
Hallo in dezelfde map als uw *docker-compose.yml* bestand Hallo volgende opdracht uitvoeren (afhankelijk van uw omgeving, moet u mogelijk toorun `docker-compose` met `sudo`):

```bash
docker-compose up -d
```

Deze opdracht start Hallo Docker-containers opgegeven in *docker-compose.yml*. Het duurt enkele minuten duren voor deze stap toocomplete. Ziet u uitvoer vergelijkbare toohello voorbeeld te volgen:

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> Ervoor toouse Hallo worden **-d** optie op opstarten, zodat Hallo containers worden uitgevoerd op de achtergrond Hallo continu.


tooverify die Hallo containers, type `docker-compose ps`. U ziet ongeveer als volgt:

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

U kunt nu verbinding tooWordPress rechtstreeks op Hallo VM op poort 80. Open een webbrowser en Voer Hallo DNS-naam van uw virtuele machine (zoals `http://mypublicdns.westus.cloudapp.azure.com`). U ziet nu Hallo die WordPress startscherm, waarin u kunt Hallo installatie voltooien en aan de slag met Hallo-toepassing.

![WordPress startscherm][wordpress_start]

## <a name="next-steps"></a>Volgende stappen
* Ga toohello [Docker VM-extensie-gebruikershandleiding](https://github.com/Azure/azure-docker-extension/blob/master/README.md) voor meer opties tooconfigure Docker en opstellen in uw Docker-virtuele machine. Bijvoorbeeld, is één optie tooput Hallo opstellen yml bestand (geconverteerde tooJSON) rechtstreeks in de configuratie Hallo Hallo Docker VM-extensie.
* Bekijk Hallo [opstellen Naslaggids](http://docs.docker.com/compose/reference/) en [gebruikershandleiding](http://docs.docker.com/compose/) voor meer voorbeelden van het maken en implementeren van meerdere container apps.
* Een Azure Resource Manager-sjabloon gebruiken uw eigen of een bijgedragen Hallo [community](https://azure.microsoft.com/documentation/templates/), toodeploy een Azure-VM met Docker en een toepassing die is ingesteld met opstellen. Bijvoorbeeld, Hallo [implementeren van een WordPress-blog met Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) sjabloon worden gebruikt voor Docker en opstellen tooquickly WordPress implementeert met een MySQL-back-end op een Ubuntu VM.
* Probeer de integratie van Docker Compose met een Docker Swarm-cluster. Zie [met behulp van opstellen met Swarm](https://docs.docker.com/compose/swarm/) voor scenario's.

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
