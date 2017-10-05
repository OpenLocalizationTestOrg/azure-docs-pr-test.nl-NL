---
title: Een nieuwe Azure Machine Learning-webservice met PowerShell Retrain | Microsoft Docs
description: Informatie over het programmatisch opnieuw trainen van een model en het bijwerken van de webservice voor het gebruik van het zojuist getrainde model in Azure Machine Learning met Machine Learning Management PowerShell-cmdlets.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3953a398-6174-4d2d-8bbd-e55cf1639415
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 804dd59e62f38ee1878045d93211ee18e0d5bfce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-the-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="d67e8-103">Een nieuwe Resource Manager gebaseerde webservice met Machine Learning Management PowerShell-cmdlets opnieuw trainen</span><span class="sxs-lookup"><span data-stu-id="d67e8-103">Retrain a New Resource Manager based web service using the Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="d67e8-104">Wanneer u een nieuwe webservice opnieuw trainen, kunt u de voorspellende webservicedefinitie om te verwijzen naar het nieuwe getrainde model bijwerken.</span><span class="sxs-lookup"><span data-stu-id="d67e8-104">When you retrain a New web service, you update the predictive web service definition to reference the new trained model.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="d67e8-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d67e8-105">Prerequisites</span></span>
<span data-ttu-id="d67e8-106">U moet instellen van een trainingsexperiment en een Voorspellend experiment zoals weergegeven in [Retrain Machine Learning-modellen programmatisch](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="d67e8-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d67e8-107">De Voorspellend experiment moet worden geïmplementeerd als een Azure Resource Manager (nieuw) op basis van machine learning-webservice.</span><span class="sxs-lookup"><span data-stu-id="d67e8-107">The predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span> <span data-ttu-id="d67e8-108">Voor het implementeren van een nieuwe webservice moet u voldoende machtigingen hebben in het abonnement waaraan u de webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="d67e8-108">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="d67e8-109">Zie voor meer informatie [beheren van een webservice via de portal voor Azure Machine Learning-webservices](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="d67e8-109">For more information, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="d67e8-110">Zie voor meer informatie over webservices implementeren [Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="d67e8-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="d67e8-111">Dit proces vereist dat u de Cmdlets van Azure Machine Learning hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="d67e8-111">This process requires that you have installed the Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="d67e8-112">Zie voor informatie over het installeren van de Machine Learning-cmdlets de [Azure Machine Learning-Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) -verwijzingen op MSDN.</span><span class="sxs-lookup"><span data-stu-id="d67e8-112">For information installing the Machine Learning cmdlets, see the [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN.</span></span>

<span data-ttu-id="d67e8-113">De volgende informatie uit de uitvoer van de retraining gekopieerd:</span><span class="sxs-lookup"><span data-stu-id="d67e8-113">Copied the following information from the retraining output:</span></span>

* <span data-ttu-id="d67e8-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="d67e8-114">BaseLocation</span></span>
* <span data-ttu-id="d67e8-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="d67e8-115">RelativeLocation</span></span>

<span data-ttu-id="d67e8-116">De stappen zijn:</span><span class="sxs-lookup"><span data-stu-id="d67e8-116">The steps you take are:</span></span>

1. <span data-ttu-id="d67e8-117">Aanmelden bij uw Azure Resource Manager-account.</span><span class="sxs-lookup"><span data-stu-id="d67e8-117">Sign in to your Azure Resource Manager account.</span></span>
2. <span data-ttu-id="d67e8-118">Definitie van de webservice ophalen</span><span class="sxs-lookup"><span data-stu-id="d67e8-118">Get the web service definition</span></span>
3. <span data-ttu-id="d67e8-119">Exporteren van de webservicedefinitie als JSON</span><span class="sxs-lookup"><span data-stu-id="d67e8-119">Export the Web Service Definition as JSON</span></span>
4. <span data-ttu-id="d67e8-120">De verwijzing naar de blob ilearner in de JSON bijwerken.</span><span class="sxs-lookup"><span data-stu-id="d67e8-120">Update the reference to the ilearner blob in the JSON.</span></span>
5. <span data-ttu-id="d67e8-121">De JSON importeren in de definitie van een Web-Service</span><span class="sxs-lookup"><span data-stu-id="d67e8-121">Import the JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="d67e8-122">De webservice bijwerken met definitie van een nieuwe Web-Service</span><span class="sxs-lookup"><span data-stu-id="d67e8-122">Update the web service with new Web Service Definition</span></span>

## <a name="sign-in-to-your-azure-resource-manager-account"></a><span data-ttu-id="d67e8-123">Aanmelden bij uw account voor Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d67e8-123">Sign in to your Azure Resource Manager account</span></span>
<span data-ttu-id="d67e8-124">U moet zich eerst aanmelden bij uw Azure-account uit binnen de PowerShell-omgeving met de [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d67e8-124">You must first sign in to your Azure account from within the PowerShell environment using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-the-web-service-definition"></a><span data-ttu-id="d67e8-125">Definitie van de webservice ophalen</span><span class="sxs-lookup"><span data-stu-id="d67e8-125">Get the Web Service Definition</span></span>
<span data-ttu-id="d67e8-126">De Web-Service vervolgens ophalen door het aanroepen van de [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d67e8-126">Next, get the Web Service by calling the [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="d67e8-127">Definitie van de webservice is een interne representatie van het getrainde model van de webservice en kan niet rechtstreeks worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="d67e8-127">The Web Service Definition is an internal representation of the trained model of the web service and is not directly modifiable.</span></span> <span data-ttu-id="d67e8-128">Zorg ervoor dat u voor uw Voorspellend experiment en niet uw trainingsexperiment definitie van de webservice ophaalt.</span><span class="sxs-lookup"><span data-stu-id="d67e8-128">Make sure that you are retrieving the Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="d67e8-129">Om te bepalen van de naam van de resourcegroep van een bestaande webservice, voert u de cmdlet Get-AzureRmMlWebService zonder parameters om weer te geven van de webservices in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="d67e8-129">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span></span> <span data-ttu-id="d67e8-130">Ga naar de webservice en zoek vervolgens naar de web service-ID.</span><span class="sxs-lookup"><span data-stu-id="d67e8-130">Locate the web service, and then look at its web service ID.</span></span> <span data-ttu-id="d67e8-131">De naam van de resourcegroep is het vierde element in de ID, direct na de *resourceGroups* element.</span><span class="sxs-lookup"><span data-stu-id="d67e8-131">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span></span> <span data-ttu-id="d67e8-132">In het volgende voorbeeld is de naam van de resourcegroep standaard-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="d67e8-132">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="d67e8-133">U kunt ook om te bepalen van de naam van de resourcegroep van een bestaande webservice, meld u aan bij de portal voor Microsoft Azure Machine Learning-webservices.</span><span class="sxs-lookup"><span data-stu-id="d67e8-133">Alternatively, to determine the resource group name of an existing web service, log on to the Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="d67e8-134">Selecteer de webservice.</span><span class="sxs-lookup"><span data-stu-id="d67e8-134">Select the web service.</span></span> <span data-ttu-id="d67e8-135">Naam van de resourcegroep is het vijfde element van de URL van de webservice direct na de *resourceGroups* element.</span><span class="sxs-lookup"><span data-stu-id="d67e8-135">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span></span> <span data-ttu-id="d67e8-136">In het volgende voorbeeld is de naam van de resourcegroep standaard-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="d67e8-136">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-the-web-service-definition-as-json"></a><span data-ttu-id="d67e8-137">Exporteren van de webservicedefinitie als JSON</span><span class="sxs-lookup"><span data-stu-id="d67e8-137">Export the Web Service Definition as JSON</span></span>
<span data-ttu-id="d67e8-138">Wijzig de definitie van het getrainde model gebruiken de zojuist getraind Model, moet u de [Export AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet exporteren naar bestand met een JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="d67e8-138">To modify the definition to the trained model to use the newly Trained Model, you must first use the [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet to export it to a JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-the-reference-to-the-ilearner-blob-in-the-json"></a><span data-ttu-id="d67e8-139">De verwijzing naar de blob ilearner in de JSON bijwerken.</span><span class="sxs-lookup"><span data-stu-id="d67e8-139">Update the reference to the ilearner blob in the JSON.</span></span>
<span data-ttu-id="d67e8-140">Zoek in de activa [getraind model], werkt de *uri* waarde in de *locationInfo* knooppunt met de URI van de ilearner-blob.</span><span class="sxs-lookup"><span data-stu-id="d67e8-140">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span></span> <span data-ttu-id="d67e8-141">De URI wordt gegenereerd door combineren de *BaseLocation* en de *RelativeLocation* uit de uitvoer van de retraining aanroep BES.</span><span class="sxs-lookup"><span data-stu-id="d67e8-141">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span></span> <span data-ttu-id="d67e8-142">Hiermee wordt het pad om te verwijzen naar het nieuwe getrainde model bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="d67e8-142">This updates the path to reference the new trained model.</span></span>

     "asset3": {
        "name": "Retrain Samp.le [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-the-json-into-a-web-service-definition"></a><span data-ttu-id="d67e8-143">De JSON importeren in de definitie van een Web-Service</span><span class="sxs-lookup"><span data-stu-id="d67e8-143">Import the JSON into a Web Service Definition</span></span>
<span data-ttu-id="d67e8-144">Moet u de [importeren AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet om te converteren van het gewijzigde JSON-bestand naar de definitie van een Web-Service die u gebruiken kunt voor het bijwerken van definitie van de webservice.</span><span class="sxs-lookup"><span data-stu-id="d67e8-144">You must use the [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet to convert the modified JSON file back into a Web Service Definition that you can use to update the Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-the-web-service-with-new-web-service-definition"></a><span data-ttu-id="d67e8-145">De webservice bijwerken met definitie van een nieuwe Web-Service</span><span class="sxs-lookup"><span data-stu-id="d67e8-145">Update the web service with new Web Service Definition</span></span>
<span data-ttu-id="d67e8-146">Gebruik tot slot [Update AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet bij te werken van definitie van de webservice.</span><span class="sxs-lookup"><span data-stu-id="d67e8-146">Finally, you use [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet to update the Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="d67e8-147">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="d67e8-147">Summary</span></span>
<span data-ttu-id="d67e8-148">De Machine Learning PowerShell-cmdlets kunt u het getrainde model van een Voorspellend webservice inschakelen van scenario's zoals bijwerken:</span><span class="sxs-lookup"><span data-stu-id="d67e8-148">Using the Machine Learning PowerShell management cmdlets, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="d67e8-149">Periodieke model retraining met nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="d67e8-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="d67e8-150">Distributie van een model voor klanten met het doel van zodat ze opnieuw trainen van het model met hun eigen gegevens.</span><span class="sxs-lookup"><span data-stu-id="d67e8-150">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

