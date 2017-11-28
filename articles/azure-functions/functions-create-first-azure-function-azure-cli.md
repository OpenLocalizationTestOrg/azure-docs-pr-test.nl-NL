---
title: Uw eerste Azure-functie maken vanuit Azure CLI | Microsoft Docs
description: Informatie over het maken van uw eerste serverloze Azure-functie met behulp van Azure CLI.
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
ms.openlocfilehash: 8bd3e4bb7423db44c48b04f25edcf1074e6ea0bd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-using-the-azure-cli"></a><span data-ttu-id="8457c-103">Uw eerste functie maken met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8457c-103">Create your first function using the Azure CLI</span></span>

<span data-ttu-id="8457c-104">In deze Quick Start-zelfstudie wordt stapsgewijs uitgelegd hoe u Azure Functions kunt gebruiken om uw eerste functie te maken.</span><span class="sxs-lookup"><span data-stu-id="8457c-104">This quickstart tutorial walks through how to use Azure Functions to create your first function.</span></span> <span data-ttu-id="8457c-105">Azure CLI gebruikt u om een functie-app te maken. Het is de serverloze infrastructuur die als host fungeert voor uw functie.</span><span class="sxs-lookup"><span data-stu-id="8457c-105">You use the Azure CLI to create a function app, which is the serverless infrastructure that hosts your function.</span></span> <span data-ttu-id="8457c-106">De functiecode zelf wordt geïmplementeerd vanuit een voorbeeldopslagplaats in GitHub.</span><span class="sxs-lookup"><span data-stu-id="8457c-106">The function code itself is deployed from a GitHub sample repository.</span></span>    

<span data-ttu-id="8457c-107">U kunt de onderstaande stappen volgen op een Mac-, Windows- of Linux-computer.</span><span class="sxs-lookup"><span data-stu-id="8457c-107">You can follow the steps below using a Mac, Windows, or Linux computer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8457c-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8457c-108">Prerequisites</span></span> 

<span data-ttu-id="8457c-109">Voordat u dit voorbeeld kunt uitvoeren moet u ervoor zorgen dat u het volgende hebt:</span><span class="sxs-lookup"><span data-stu-id="8457c-109">Before running this sample, you must have the following:</span></span>

+ <span data-ttu-id="8457c-110">Een actief [GitHub](https://github.com)-account.</span><span class="sxs-lookup"><span data-stu-id="8457c-110">An active [GitHub](https://github.com) account.</span></span> 
+ <span data-ttu-id="8457c-111">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8457c-111">An active Azure subscription.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8457c-112">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="8457c-112">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8457c-113">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="8457c-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="8457c-114">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8457c-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="8457c-115">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="8457c-115">Create a resource group</span></span>

<span data-ttu-id="8457c-116">Maak een resourcegroep met de opdracht [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="8457c-116">Create a resource group with the [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="8457c-117">Een Azure-resourcegroep is een logische container waarin Azure-resources, zoals functie-apps, databases en opslagaccounts worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="8457c-117">An Azure resource group is a logical container into which Azure resources like function apps, databases, and storage accounts are deployed and managed.</span></span>

<span data-ttu-id="8457c-118">In het volgende voorbeeld wordt een resourcegroep met de naam `myResourceGroup` gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8457c-118">The following example creates a resource group named `myResourceGroup`.</span></span>  
<span data-ttu-id="8457c-119">Als u Cloud Shell niet gebruikt, moet u eerst zich aanmelden met `az login`.</span><span class="sxs-lookup"><span data-stu-id="8457c-119">If you are not using Cloud Shell, you must first sign in using `az login`.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a><span data-ttu-id="8457c-120">Een Azure Storage-account maken</span><span class="sxs-lookup"><span data-stu-id="8457c-120">Create an Azure Storage account</span></span>

<span data-ttu-id="8457c-121">Functions gebruikt een Azure Storage-account om de status van uw functies en andere informatie erover te onderhouden.</span><span class="sxs-lookup"><span data-stu-id="8457c-121">Functions uses an Azure Storage account to maintain state and other information about your functions.</span></span> <span data-ttu-id="8457c-122">Maak een opslagaccount in de resourcegroep die u hebt gemaakt met behulp van de opdracht [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="8457c-122">Create a storage account in the resource group you created by using the [az storage account create](/cli/azure/storage/account#create) command.</span></span>

<span data-ttu-id="8457c-123">Vervang in de volgende opdracht de plaatsaanduiding `<storage_name>` met uw eigen wereldwijd unieke opslagaccountnaam.</span><span class="sxs-lookup"><span data-stu-id="8457c-123">In the following command, substitute your own globally unique storage account name where you see the `<storage_name>` placeholder.</span></span> <span data-ttu-id="8457c-124">Namen van opslagaccounts moeten tussen 3 en 24 tekens lang zijn en mogen alleen cijfers en kleine letters bevatten.</span><span class="sxs-lookup"><span data-stu-id="8457c-124">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

<span data-ttu-id="8457c-125">Nadat het opslagaccount is gemaakt, toont Azure CLI soortgelijke informatie als in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8457c-125">After the storage account has been created, the Azure CLI shows information similar to the following example:</span></span>

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

## <a name="create-a-function-app"></a><span data-ttu-id="8457c-126">Een functie-app maken</span><span class="sxs-lookup"><span data-stu-id="8457c-126">Create a function app</span></span>

<span data-ttu-id="8457c-127">U moet een functie-app hebben die als host fungeert voor de uitvoering van uw functies.</span><span class="sxs-lookup"><span data-stu-id="8457c-127">You must have a function app to host the execution of your functions.</span></span> <span data-ttu-id="8457c-128">De functie-app biedt een omgeving waarin uw functiecode zonder server kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8457c-128">The function app provides an environment for serverless execution of your function code.</span></span> <span data-ttu-id="8457c-129">U kunt er functies mee groeperen in een logische eenheid, zodat u resources eenvoudiger kunt beheren, implementeren en delen.</span><span class="sxs-lookup"><span data-stu-id="8457c-129">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> <span data-ttu-id="8457c-130">Een functie-app maken met behulp van de opdracht [az functionapp create](/cli/azure/functionapp#create).</span><span class="sxs-lookup"><span data-stu-id="8457c-130">Create a function app by using the [az functionapp create](/cli/azure/functionapp#create) command.</span></span> 

<span data-ttu-id="8457c-131">Vervang in de volgende opdracht de plaatsaanduiding `<app_name>` en de opslagaccountnaam voor `<storage_name>` met uw eigen unieke functie-appnaam.</span><span class="sxs-lookup"><span data-stu-id="8457c-131">In the following command, substitute your own unique function app name where you see the `<app_name>` placeholder and the storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="8457c-132">De `<app_name>` wordt gebruikt als het standaard DNS-domein voor de functie-app. Om die reden moet de naam uniek zijn in alle apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="8457c-132">The `<app_name>` is used as the default DNS domain for the function app, and so the name needs to be unique across all apps in Azure.</span></span> 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
<span data-ttu-id="8457c-133">Standaard wordt een functie-app gemaakt met het hostingabonnement Consumption, wat betekent dat resources dynamisch worden toegevoegd wanneer ze voor uw functies zijn vereist; en u betaalt alleen wanneer functies worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8457c-133">By default, a function app is created with the Consumption hosting plan, which means that resources are added dynamically as required by your functions and you only pay when functions are running.</span></span> <span data-ttu-id="8457c-134">Zie [Het juiste hostingabonnement kiezen](functions-scale.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8457c-134">For more information, see [Choose the correct hosting plan](functions-scale.md).</span></span> 

<span data-ttu-id="8457c-135">Nadat de functie-app is gemaakt, toont Azure CLI soortgelijke informatie als in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8457c-135">After the function app has been created, the Azure CLI shows information similar to the following example:</span></span>

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

<span data-ttu-id="8457c-136">Nu u een functie-app hebt, kunt u de werkelijke functiecode vanuit de voorbeeldopslagplaats in GitHub implementeren.</span><span class="sxs-lookup"><span data-stu-id="8457c-136">Now that you have a function app, you can deploy the actual function code from the GitHub sample repository.</span></span>

## <a name="deploy-your-function-code"></a><span data-ttu-id="8457c-137">Uw functiecode implementeren</span><span class="sxs-lookup"><span data-stu-id="8457c-137">Deploy your function code</span></span>  

<span data-ttu-id="8457c-138">Er zijn verschillende manieren om uw functiecode te maken in uw nieuwe functie app.</span><span class="sxs-lookup"><span data-stu-id="8457c-138">There are several ways to create your function code in your new function app.</span></span> <span data-ttu-id="8457c-139">In dit onderwerp wordt verbinding gemaakt met een voorbeeldopslagplaats in GitHub.</span><span class="sxs-lookup"><span data-stu-id="8457c-139">This topic connects to a sample repository in GitHub.</span></span> <span data-ttu-id="8457c-140">Net als voorheen moet u in de volgende code de plaatsaanduiding `<app_name>` vervangen door de naam van de functie-app die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8457c-140">As before, in the following code replace the `<app_name>` placeholder with the name of the function app you created.</span></span> 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
<span data-ttu-id="8457c-141">Nadat de implementatiebron is ingesteld, wordt door Azure CLI informatie weergegeven die overeenkomt met het volgende voorbeeld (null-waarden zijn verwijderd vanwege de leesbaarheid):</span><span class="sxs-lookup"><span data-stu-id="8457c-141">After the deployment source been set, the Azure CLI shows information similar to the following example (null values removed for readability):</span></span>

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

## <a name="test-the-function"></a><span data-ttu-id="8457c-142">De functie testen</span><span class="sxs-lookup"><span data-stu-id="8457c-142">Test the function</span></span>

<span data-ttu-id="8457c-143">Gebruik cURL om de geïmplementeerde functie te testen op een Mac- of Linux-computer of met Bash op Windows.</span><span class="sxs-lookup"><span data-stu-id="8457c-143">Use cURL to test the deployed function on a Mac or Linux computer or using Bash on Windows.</span></span> <span data-ttu-id="8457c-144">Voer de volgende cURL-opdracht uit, waarbij u de plaatsaanduiding `<app_name>` vervangt door de naam van de functie-app die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8457c-144">Execute the following cURL command, replacing the `<app_name>` placeholder with the name of your function app.</span></span> <span data-ttu-id="8457c-145">Voeg de queryreeks `&name=<yourname>` toe aan de URL.</span><span class="sxs-lookup"><span data-stu-id="8457c-145">Append the query string `&name=<yourname>` to the URL.</span></span>

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Het antwoord van de functie weergegeven in een browser.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

<span data-ttu-id="8457c-147">Als cURL niet beschikbaar is op uw opdrachtregel, moet u gewoon dezelfde URL opgeven op de adresbalk van uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="8457c-147">If you don't have cURL available in your command line, enter the same URL in the address of your web browser.</span></span> <span data-ttu-id="8457c-148">Vervang weer de plaatsaanduiding `<app_name>` door de naam van uw functie-app, voeg de queryreeks `&name=<yourname>` toe aan de URL en voer de aanvraag uit.</span><span class="sxs-lookup"><span data-stu-id="8457c-148">Again, replace the `<app_name>` placeholder with the name of your function app, and append the query string `&name=<yourname>` to the URL and execute the request.</span></span> 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Het antwoord van de functie weergegeven in een browser.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a><span data-ttu-id="8457c-150">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="8457c-150">Clean up resources</span></span>

<span data-ttu-id="8457c-151">Andere Quick Starts in deze verzameling zijn op deze Quick Start gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="8457c-151">Other quickstarts in this collection build upon this quickstart.</span></span> <span data-ttu-id="8457c-152">Als u van plan bent om door te gaan met andere Quick Starts of met de zelfstudies, verwijdert u de resources die u in deze Quick Start hebt gemaakt niet.</span><span class="sxs-lookup"><span data-stu-id="8457c-152">If you plan to continue on to work with subsequent quickstarts or with the tutorials, do not clean up the resources created in this quickstart.</span></span> <span data-ttu-id="8457c-153">Als u niet wilt doorgaan, gebruikt u de volgende opdracht om alle resources die via deze Quick Start zijn gemaakt, te verwijderen:</span><span class="sxs-lookup"><span data-stu-id="8457c-153">If you do not plan to continue, use the following command to delete all resources created by this quickstart:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```
<span data-ttu-id="8457c-154">Typ `y` wanneer u daarom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="8457c-154">Type `y` when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8457c-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8457c-155">Next steps</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
