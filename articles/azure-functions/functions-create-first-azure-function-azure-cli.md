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
# <a name="create-your-first-function-using-hello-azure-cli"></a><span data-ttu-id="718d9-103">Maken van uw eerste functie met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="718d9-103">Create your first function using hello Azure CLI</span></span>

<span data-ttu-id="718d9-104">Deze Quick Start-zelfstudie wordt uitgelegd hoe u toouse Azure Functions toocreate uw eerste functie.</span><span class="sxs-lookup"><span data-stu-id="718d9-104">This quickstart tutorial walks through how toouse Azure Functions toocreate your first function.</span></span> <span data-ttu-id="718d9-105">U hello Azure CLI toocreate een functie-app, zonder server Hallo-infrastructuur die als host fungeert voor de functie.</span><span class="sxs-lookup"><span data-stu-id="718d9-105">You use hello Azure CLI toocreate a function app, which is hello serverless infrastructure that hosts your function.</span></span> <span data-ttu-id="718d9-106">Hallo functiecode zelf wordt geïmplementeerd vanaf een GitHub-opslagplaats voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="718d9-106">hello function code itself is deployed from a GitHub sample repository.</span></span>    

<span data-ttu-id="718d9-107">U kunt stappen Hallo hieronder een Mac-, Windows- of Linux-computer.</span><span class="sxs-lookup"><span data-stu-id="718d9-107">You can follow hello steps below using a Mac, Windows, or Linux computer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="718d9-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="718d9-108">Prerequisites</span></span> 

<span data-ttu-id="718d9-109">Voordat u dit voorbeeld uitvoert, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="718d9-109">Before running this sample, you must have hello following:</span></span>

+ <span data-ttu-id="718d9-110">Een actief [GitHub](https://github.com)-account.</span><span class="sxs-lookup"><span data-stu-id="718d9-110">An active [GitHub](https://github.com) account.</span></span> 
+ <span data-ttu-id="718d9-111">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="718d9-111">An active Azure subscription.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="718d9-112">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="718d9-112">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="718d9-113">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="718d9-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="718d9-114">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="718d9-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="718d9-115">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="718d9-115">Create a resource group</span></span>

<span data-ttu-id="718d9-116">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="718d9-116">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="718d9-117">Een Azure-resourcegroep is een logische container waarin Azure-resources, zoals functie-apps, databases en opslagaccounts worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="718d9-117">An Azure resource group is a logical container into which Azure resources like function apps, databases, and storage accounts are deployed and managed.</span></span>

<span data-ttu-id="718d9-118">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="718d9-118">hello following example creates a resource group named `myResourceGroup`.</span></span>  
<span data-ttu-id="718d9-119">Als u Cloud Shell niet gebruikt, moet u eerst zich aanmelden met `az login`.</span><span class="sxs-lookup"><span data-stu-id="718d9-119">If you are not using Cloud Shell, you must first sign in using `az login`.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a><span data-ttu-id="718d9-120">Een Azure Storage-account maken</span><span class="sxs-lookup"><span data-stu-id="718d9-120">Create an Azure Storage account</span></span>

<span data-ttu-id="718d9-121">Functies maakt gebruik van een Azure Storage-account toomaintain status en andere informatie over uw functies.</span><span class="sxs-lookup"><span data-stu-id="718d9-121">Functions uses an Azure Storage account toomaintain state and other information about your functions.</span></span> <span data-ttu-id="718d9-122">Een opslagaccount maken in Hallo resourcegroep hebt gemaakt met de Hallo [az storage-account maken](/cli/azure/storage/account#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="718d9-122">Create a storage account in hello resource group you created by using hello [az storage account create](/cli/azure/storage/account#create) command.</span></span>

<span data-ttu-id="718d9-123">In Hallo opdracht, na uw eigen globaal unieke opslagaccountnaam waarin u zien hoe Hallo ook `<storage_name>` tijdelijke aanduiding.</span><span class="sxs-lookup"><span data-stu-id="718d9-123">In hello following command, substitute your own globally unique storage account name where you see hello `<storage_name>` placeholder.</span></span> <span data-ttu-id="718d9-124">Namen van opslagaccounts moeten tussen 3 en 24 tekens lang zijn en mogen alleen cijfers en kleine letters bevatten.</span><span class="sxs-lookup"><span data-stu-id="718d9-124">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

<span data-ttu-id="718d9-125">Nadat het Hallo-storage-account is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="718d9-125">After hello storage account has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

## <a name="create-a-function-app"></a><span data-ttu-id="718d9-126">Een functie-app maken</span><span class="sxs-lookup"><span data-stu-id="718d9-126">Create a function app</span></span>

<span data-ttu-id="718d9-127">U moet een functie-app toohost Hallo uitvoering van uw functies hebben.</span><span class="sxs-lookup"><span data-stu-id="718d9-127">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="718d9-128">Hallo functie-app biedt een omgeving voor zonder server uitvoeren van de functiecode.</span><span class="sxs-lookup"><span data-stu-id="718d9-128">hello function app provides an environment for serverless execution of your function code.</span></span> <span data-ttu-id="718d9-129">U kunt er functies mee groeperen in een logische eenheid, zodat u resources eenvoudiger kunt beheren, implementeren en delen.</span><span class="sxs-lookup"><span data-stu-id="718d9-129">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> <span data-ttu-id="718d9-130">Een functie-app maken met behulp van Hallo [az functionapp maken](/cli/azure/functionapp#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="718d9-130">Create a function app by using hello [az functionapp create](/cli/azure/functionapp#create) command.</span></span> 

<span data-ttu-id="718d9-131">In Hallo volgende opdracht, vervangt u de naam van uw eigen unieke functie-app waarin u zien hoe Hallo `<app_name>` tijdelijke aanduiding en Hallo opslagaccountnaam voor `<storage_name>`.</span><span class="sxs-lookup"><span data-stu-id="718d9-131">In hello following command, substitute your own unique function app name where you see hello `<app_name>` placeholder and hello storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="718d9-132">Hallo `<app_name>` wordt gebruikt als Hallo standaard DNS-domein voor Hallo functie-app en geval Hallo-naam toobe uniek zijn in alle apps in Azure moet.</span><span class="sxs-lookup"><span data-stu-id="718d9-132">hello `<app_name>` is used as hello default DNS domain for hello function app, and so hello name needs toobe unique across all apps in Azure.</span></span> 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
<span data-ttu-id="718d9-133">Standaard wordt een functie-app gemaakt met Hallo verbruik hosting plan, wat betekent dat bronnen dynamisch zoals vereist door uw functies zijn toegevoegd en u alleen betaalt wanneer functies worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="718d9-133">By default, a function app is created with hello Consumption hosting plan, which means that resources are added dynamically as required by your functions and you only pay when functions are running.</span></span> <span data-ttu-id="718d9-134">Zie voor meer informatie [Kies Hallo juist hosting plan](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="718d9-134">For more information, see [Choose hello correct hosting plan](functions-scale.md).</span></span> 

<span data-ttu-id="718d9-135">Nadat het Hallo-functie-app is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="718d9-135">After hello function app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="718d9-136">Nu dat u een functie-app hebt, kunt u de werkelijke functiecode Hallo van Hallo GitHub-opslagplaats voor voorbeeld kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="718d9-136">Now that you have a function app, you can deploy hello actual function code from hello GitHub sample repository.</span></span>

## <a name="deploy-your-function-code"></a><span data-ttu-id="718d9-137">Uw functiecode implementeren</span><span class="sxs-lookup"><span data-stu-id="718d9-137">Deploy your function code</span></span>  

<span data-ttu-id="718d9-138">Er zijn verschillende manieren toocreate uw functiecode in uw nieuwe functie-app.</span><span class="sxs-lookup"><span data-stu-id="718d9-138">There are several ways toocreate your function code in your new function app.</span></span> <span data-ttu-id="718d9-139">In dit onderwerp maakt verbinding tooa voorbeeld opslagplaats in GitHub.</span><span class="sxs-lookup"><span data-stu-id="718d9-139">This topic connects tooa sample repository in GitHub.</span></span> <span data-ttu-id="718d9-140">Als voorheen in Hallo na code vervangt Hallo `<app_name>` aanduiding voor items met de naam Hallo van Hallo functie-app u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="718d9-140">As before, in hello following code replace hello `<app_name>` placeholder with hello name of hello function app you created.</span></span> 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
<span data-ttu-id="718d9-141">Na de implementatie van Hallo is bron ingesteld, hello Azure CLI toont informatie vergelijkbare toohello voorbeeld (null-waarden voor de leesbaarheid verwijderd) te volgen:</span><span class="sxs-lookup"><span data-stu-id="718d9-141">After hello deployment source been set, hello Azure CLI shows information similar toohello following example (null values removed for readability):</span></span>

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

## <a name="test-hello-function"></a><span data-ttu-id="718d9-142">Hallo functie testen</span><span class="sxs-lookup"><span data-stu-id="718d9-142">Test hello function</span></span>

<span data-ttu-id="718d9-143">CURL tootest Hallo geïmplementeerd functie op een Mac- of Linux-computer- of Bash via op Windows gebruiken.</span><span class="sxs-lookup"><span data-stu-id="718d9-143">Use cURL tootest hello deployed function on a Mac or Linux computer or using Bash on Windows.</span></span> <span data-ttu-id="718d9-144">Uitvoeren van de volgende cURL-opdracht, waarbij vervangt Hallo Hallo `<app_name>` aanduiding voor items met Hallo-naam van de functie-app.</span><span class="sxs-lookup"><span data-stu-id="718d9-144">Execute hello following cURL command, replacing hello `<app_name>` placeholder with hello name of your function app.</span></span> <span data-ttu-id="718d9-145">Hallo-queryreeks toevoegen `&name=<yourname>` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="718d9-145">Append hello query string `&name=<yourname>` toohello URL.</span></span>

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Het antwoord van de functie weergegeven in een browser.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

<span data-ttu-id="718d9-147">Als u geen cURL beschikbaar in de opdrachtregel, voert u dezelfde URL Hallo-adres van uw webbrowser Hallo.</span><span class="sxs-lookup"><span data-stu-id="718d9-147">If you don't have cURL available in your command line, enter hello same URL in hello address of your web browser.</span></span> <span data-ttu-id="718d9-148">Opnieuw vervangen Hallo `<app_name>` tijdelijke aanduiding met de naam van uw app functie Hallo en toevoeg-queryreeks Hallo `&name=<yourname>` toohello URL en Hallo aanvraag uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="718d9-148">Again, replace hello `<app_name>` placeholder with hello name of your function app, and append hello query string `&name=<yourname>` toohello URL and execute hello request.</span></span> 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Het antwoord van de functie weergegeven in een browser.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a><span data-ttu-id="718d9-150">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="718d9-150">Clean up resources</span></span>

<span data-ttu-id="718d9-151">Andere Quick Starts in deze verzameling zijn op deze Quick Start gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="718d9-151">Other quickstarts in this collection build upon this quickstart.</span></span> <span data-ttu-id="718d9-152">Als u van plan toocontinue toowork daaropvolgende snelstartgidsen of met Hallo zelfstudies bent, gaat u als Hallo-resources die zijn gemaakt in deze snelstartgids niet opruimen.</span><span class="sxs-lookup"><span data-stu-id="718d9-152">If you plan toocontinue on toowork with subsequent quickstarts or with hello tutorials, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="718d9-153">Als u niet van plan toocontinue bent, gebruikt u Hallo opdracht toodelete na alle resources die zijn gemaakt door deze snelstartgids:</span><span class="sxs-lookup"><span data-stu-id="718d9-153">If you do not plan toocontinue, use hello following command toodelete all resources created by this quickstart:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```
<span data-ttu-id="718d9-154">Typ `y` wanneer u daarom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="718d9-154">Type `y` when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="718d9-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="718d9-155">Next steps</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
