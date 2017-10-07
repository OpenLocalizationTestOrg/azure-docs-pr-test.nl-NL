---
title: aaaUsing ACR met een Azure-DC/OS-cluster | Microsoft Docs
description: Een Azure Container Registry gebruiken met een DC/OS-cluster in Azure Container Service
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: Docker, Containers Micro-services, Mesos, Azure, bestandsshare, cifs
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a>ACR gebruiken met een DC/OS-cluster toodeploy uw toepassing

In dit artikel wordt besproken hoe toouse Azure Container register met een DC/OS-cluster. ACR kunt u tooprivately store en beheren van installatiekopieën van de container. Deze zelfstudie behandelt Hallo taken te volgen:

> [!div class="checklist"]
> * Azure Container register implementeren (indien nodig)
> * ACR-verificatie configureren op een DC/OS-cluster
> * Een installatiekopie toohello Azure Container register geüpload
> * Uitvoeren van een installatiekopie van een container vanaf hello Azure Container register

U moet een ACS DC/OS cluster toocomplete Hallo in deze zelfstudie stappen. Indien nodig, [dit voorbeeldscript](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) kunt maken voor u.

Deze zelfstudie vereist hello Azure CLI versie 2.0.4 of hoger. Voer `az --version` toofind Hallo versie. Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a>Register met Azure Container implementeren

Maak indien nodig een Azure-Container registry Hello [az acr maken](/cli/azure/acr#create) opdracht. 

Hallo volgende voorbeeld wordt een register met een willekeurige naam moet worden gegenereerd. Hallo-register wordt ook geconfigureerd met een beheerdersaccount met Hallo `--admin-enabled` argument.

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

Zodra het Hallo-register is gemaakt, levert hello Azure CLI gegevens vergelijkbaar toohello volgt. Let op Hallo `name` en `loginServer`, deze worden gebruikt in latere stappen.

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

Hallo container register referenties met Hallo [az acr referentie weergeven](/cli/azure/acr/credential) opdracht. Vervang Hallo `--name` Hello een vermeld in de laatste stap Hallo. Let op van een wachtwoord is vereist in een later stadium.

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

Zie voor meer informatie over Azure-Container register [inleiding tooprivate Docker-container registers](../../container-registry/container-registry-intro.md). 

## <a name="manage-acr-authentication"></a>ACR-verificatie beheren

Hallo conventionele wijze toopush en pull-installatiekopie van een persoonlijke register toofirst verifiëren met Hallo-register. toodo geval is, gebruikt u Hallo `docker login` opdracht op elke client die tooaccess Hallo persoonlijke register nodig. Omdat een DC/OS-cluster veel knooppunten bevatten kan, die allemaal toobe geverifieerd met Hallo ACR nodig hebt, is het handig tooautomate dit proces voor elk knooppunt. 

### <a name="create-shared-storage"></a>Gedeelde opslag maken

Dit proces maakt gebruik van een Azure-bestandsshare die is gekoppeld op elk knooppunt in het Hallo-cluster. Als u al geen gedeelde opslag hebt ingesteld, Zie [instellen van een bestandsshare in een DC/OS-cluster](container-service-dcos-fileshare.md).

### <a name="configure-acr-authentication"></a>ACR-verificatie configureren

Eerst ophalen Hallo FQDN-naam van Hallo DC/OS-master en op te slaan in een variabele.

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

Een SSH-verbinding maken met Hallo master (of het eerste model Hallo) van uw DC/OS gebaseerde cluster. Hallo-gebruikersnaam bijwerken als een niet-standaard-waarde is gebruikt bij het maken van Hallo-cluster.

```azurecli-interactive
ssh azureuser@$FQDN
```

Na de opdracht toologin toohello Azure Container register Hallo worden uitgevoerd. Vervang Hallo `--username` met de naam van Hallo container register en Hallo Hallo `--password` met een van de opgegeven Hallo wachtwoorden. Vervang het laatste argument Hallo *mycontainerregistry.azurecr.io* in Hallo voorbeeld met de naam van Hallo loginServer van Hallo container register. 

Deze opdracht worden opgeslagen Hallo verificatie waarden lokaal onder Hallo `~/.docker` pad.

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

Maak een gecomprimeerd bestand met Hallo container registerwaarden verificatie.

```azurecli-interactive
tar czf docker.tar.gz .docker
```

Kopieer dit bestand toohello gedeelde clusteropslag. Deze stap maakt beschikbaar zijn op alle knooppunten van de DC/OS-cluster Hallo Hallo-bestand.

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a>Afbeelding tooACR uploaden

Nu vanuit een ontwikkelcomputer of elk ander systeem met Docker geïnstalleerd, een installatiekopie maken en upload het toohello Azure Container register.

Een container van Hallo Ubuntu installatiekopie maken.

```azurecli-interactive
docker run ubunut --name base-image
```

Nu Hallo container vastleggen in een nieuwe installatiekopie. Hallo installatiekopie met de naam moet tooinclude hello `loginServer` naam van het Hallo-container registrywith een indeling van `loginServer/imageName`.

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

Meld u aan bij hello Azure Container register. Hallo naam vervangen door Hallo loginServer naam, Hallo--gebruikersnaam met de naam van de Hallo van Hallo container register en Hallo--wachtwoord met een van de opgegeven Hallo wachtwoorden.

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

Ten slotte uploaden Hallo installatiekopie toohello ACR register. In dit voorbeeld wordt een afbeelding met de naam dcos demo geüpload.

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a>Uitvoeren van een installatiekopie vanaf ACR

toouse een afbeelding uit Hallo ACR register, maakt u een bestand namen *acrDemo.json* en kopiëren Hallo tekst in de App. Vervangen door de naam van de installatiekopie Hallo Hallo container register loginServer naam en de naam van de installatiekopie, bijvoorbeeld `loginServer/imageName`. Let op Hallo `uris` eigenschap. Deze eigenschap bevat Hallo-locatie van Hallo container verificatie registerbestand, die in dit geval hello Azure-bestandsshare die is gekoppeld op elk knooppunt in Hallo DC/OS-cluster.

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

Hallo-toepassing Hello CLI DC/Overheadkosten implementeren.

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u DC/OS toouse Azure Container register met inbegrip van de volgende Hallo taken configureren:

> [!div class="checklist"]
> * Azure Container register implementeren (indien nodig)
> * ACR-verificatie configureren op een DC/OS-cluster
> * Een installatiekopie toohello Azure Container register geüpload
> * Uitvoeren van een installatiekopie van een container vanaf hello Azure Container register
