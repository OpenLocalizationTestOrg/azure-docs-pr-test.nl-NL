---
title: uw eerste functie van Azure CLI Hallo aaaCreate | Microsoft Docs
description: Meer informatie over hoe uw eerste Azure-functie voor het gebruik van zonder server worden uitgevoerd toocreate hello Azure CLI.
services: functions
keywords: 
author: ggailey777
ms.author: glenga
ms.assetid: 674a01a7-fd34-4775-8b69-893182742ae0
ms.date: 08/22/2017
ms.topic: hero-article
ms.service: functions
ms.custom: mvc
ms.devlang: azure-cli
manager: erikre
ms.openlocfilehash: 5feed0045d4998b88b0e1bb50996cb7bb42b0822
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-hello-azure-cli"></a>Maken van uw eerste functie met hello Azure CLI

Deze Quick Start-zelfstudie wordt uitgelegd hoe u toouse Azure Functions toocreate uw eerste functie. U hello Azure CLI toocreate een functie-app, zonder server Hallo-infrastructuur die als host fungeert voor de functie. Hallo functiecode zelf wordt geïmplementeerd vanaf een GitHub-opslagplaats voorbeeld.    

U kunt stappen Hallo hieronder een Mac-, Windows- of Linux-computer. 

## <a name="prerequisites"></a>Vereisten 

Voordat u dit voorbeeld uitvoert, moet u de volgende Hallo hebben:

+ Een actief [GitHub](https://github.com)-account. 
+ Een actief Azure-abonnement.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 


## <a name="create-a-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create). Een Azure-resourcegroep is een logische container waarin Azure-resources, zoals functie-apps, databases en opslagaccounts worden geïmplementeerd en beheerd.

Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup`.  
Als u Cloud Shell niet gebruikt, moet u eerst zich aanmelden met `az login`.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a>Een Azure Storage-account maken

Functies maakt gebruik van een Azure Storage-account toomaintain status en andere informatie over uw functies. Een opslagaccount maken in Hallo resourcegroep hebt gemaakt met de Hallo [az storage-account maken](/cli/azure/storage/account#create) opdracht.

In Hallo opdracht, na uw eigen globaal unieke opslagaccountnaam waarin u zien hoe Hallo ook `<storage_name>` tijdelijke aanduiding. Namen van opslagaccounts moeten tussen 3 en 24 tekens lang zijn en mogen alleen cijfers en kleine letters bevatten.

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

Nadat het Hallo-storage-account is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:

```json
{
  "creationTime": "2017-04-15T17:14:39.320307+00:00",
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myresourcegroup/...",
  "kind": "Storage",
  "location": "westeurope",
  "name": "myfunctionappstorage",
  "primaryEndpoints": {
    "blob": "https://myfunctionappstorage.blob.core.windows.net/",
    "file": "https://myfunctionappstorage.file.core.windows.net/",
    "queue": "https://myfunctionappstorage.queue.core.windows.net/",
    "table": "https://myfunctionappstorage.table.core.windows.net/"
  },
     ....
    // Remaining output has been truncated for readability.
}
```

## <a name="create-a-function-app"></a>Een functie-app maken

U moet een functie-app toohost Hallo uitvoering van uw functies hebben. Hallo functie-app biedt een omgeving voor zonder server uitvoeren van de functiecode. U kunt er functies mee groeperen in een logische eenheid, zodat u resources eenvoudiger kunt beheren, implementeren en delen. Een functie-app maken met behulp van Hallo [az functionapp maken](/cli/azure/functionapp#create) opdracht. 

In Hallo volgende opdracht, vervangt u de naam van uw eigen unieke functie-app waarin u zien hoe Hallo `<app_name>` tijdelijke aanduiding en Hallo opslagaccountnaam voor `<storage_name>`. Hallo `<app_name>` wordt gebruikt als Hallo standaard DNS-domein voor Hallo functie-app en geval Hallo-naam toobe uniek zijn in alle apps in Azure moet. 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
Standaard wordt een functie-app gemaakt met Hallo verbruik hosting plan, wat betekent dat bronnen dynamisch zoals vereist door uw functies zijn toegevoegd en u alleen betaalt wanneer functies worden uitgevoerd. Zie voor meer informatie [Kies Hallo juist hosting plan](functions-scale.md). 

Nadat het Hallo-functie-app is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "containerSize": 1536,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "quickstart.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "quickstart.azurewebsites.net",
    "quickstart.scm.azurewebsites.net"
  ],
   ....
    // Remaining output has been truncated for readability.
}
```

Nu dat u een functie-app hebt, kunt u de werkelijke functiecode Hallo van Hallo GitHub-opslagplaats voor voorbeeld kunt implementeren.

## <a name="deploy-your-function-code"></a>Uw functiecode implementeren  

Er zijn verschillende manieren toocreate uw functiecode in uw nieuwe functie-app. In dit onderwerp maakt verbinding tooa voorbeeld opslagplaats in GitHub. Als voorheen in Hallo na code vervangt Hallo `<app_name>` aanduiding voor items met de naam Hallo van Hallo functie-app u hebt gemaakt. 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
Na de implementatie van Hallo is bron ingesteld, hello Azure CLI toont informatie vergelijkbare toohello voorbeeld (null-waarden voor de leesbaarheid verwijderd) te volgen:

```json
{
  "branch": "master",
  "deploymentRollbackEnabled": false,
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myResourceGroup/...",
  "isManualIntegration": true,
  "isMercurial": false,
  "location": "West Europe",
  "name": "quickstart",
  "repoUrl": "https://github.com/Azure-Samples/functions-quickstart",
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.Web/sites/sourcecontrols"
}
```

## <a name="test-hello-function"></a>Hallo functie testen

CURL tootest Hallo geïmplementeerd functie op een Mac- of Linux-computer- of Bash via op Windows gebruiken. Uitvoeren van de volgende cURL-opdracht, waarbij vervangt Hallo Hallo `<app_name>` aanduiding voor items met Hallo-naam van de functie-app. Hallo-queryreeks toevoegen `&name=<yourname>` toohello URL.

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Het antwoord van de functie weergegeven in een browser.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

Als u geen cURL beschikbaar in de opdrachtregel, voert u dezelfde URL Hallo-adres van uw webbrowser Hallo. Opnieuw vervangen Hallo `<app_name>` tijdelijke aanduiding met de naam van uw app functie Hallo en toevoeg-queryreeks Hallo `&name=<yourname>` toohello URL en Hallo aanvraag uit te voeren. 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Het antwoord van de functie weergegeven in een browser.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a>Resources opschonen

Andere Quick Starts in deze verzameling zijn op deze Quick Start gebaseerd. Als u van plan toocontinue toowork daaropvolgende snelstartgidsen of met Hallo zelfstudies bent, gaat u als Hallo-resources die zijn gemaakt in deze snelstartgids niet opruimen. Als u niet van plan toocontinue bent, gebruikt u Hallo opdracht toodelete na alle resources die zijn gemaakt door deze snelstartgids:

```azurecli-interactive
az group delete --name myResourceGroup
```
Typ `y` wanneer u daarom wordt gevraagd.

## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
