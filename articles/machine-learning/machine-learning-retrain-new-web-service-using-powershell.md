---
title: aaaRetrain een nieuwe Azure Machine Learning-webservice met PowerShell | Microsoft Docs
description: Meer informatie over hoe tooprogrammatically een model en update Hallo web service toouse Hallo zojuist getraind model in Azure Machine Learning met Machine Learning Management PowerShell-cmdlets voor Hallo opnieuw trainen.
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
ms.openlocfilehash: 5b77fa82cfe17f0b4e90007ef81c506ab712475b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="9351a-103">Een nieuwe Resource Manager gebaseerde webservice met Machine Learning Management PowerShell-cmdlets voor Hallo opnieuw trainen</span><span class="sxs-lookup"><span data-stu-id="9351a-103">Retrain a New Resource Manager based web service using hello Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="9351a-104">Wanneer u een nieuwe webservice opnieuw trainen, werkt u Hallo voorspellende web service definitie tooreference Hallo nieuwe getrainde model.</span><span class="sxs-lookup"><span data-stu-id="9351a-104">When you retrain a New web service, you update hello predictive web service definition tooreference hello new trained model.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="9351a-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9351a-105">Prerequisites</span></span>
<span data-ttu-id="9351a-106">U moet instellen van een trainingsexperiment en een Voorspellend experiment zoals weergegeven in [Retrain Machine Learning-modellen programmatisch](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="9351a-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9351a-107">Hallo Voorspellend experiment moet worden geïmplementeerd als een Azure Resource Manager (nieuw) op basis van machine learning-webservice.</span><span class="sxs-lookup"><span data-stu-id="9351a-107">hello predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span> <span data-ttu-id="9351a-108">toodeploy een nieuwe webservice die u moet voldoende machtigingen hebben in Hallo abonnement toowhich u Hallo-webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="9351a-108">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="9351a-109">Zie voor meer informatie [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="9351a-109">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="9351a-110">Zie voor meer informatie over webservices implementeren [Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="9351a-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="9351a-111">Dit proces vereist dat u hello Azure Machine Learning-Cmdlets zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="9351a-111">This process requires that you have installed hello Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="9351a-112">Zie voor informatie over het installeren van de Machine Learning-cmdlets Hallo Hallo [Azure Machine Learning-Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) -verwijzingen op MSDN.</span><span class="sxs-lookup"><span data-stu-id="9351a-112">For information installing hello Machine Learning cmdlets, see hello [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN.</span></span>

<span data-ttu-id="9351a-113">Gekopieerde Hallo volgende informatie uit Hallo retraining uitvoer:</span><span class="sxs-lookup"><span data-stu-id="9351a-113">Copied hello following information from hello retraining output:</span></span>

* <span data-ttu-id="9351a-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="9351a-114">BaseLocation</span></span>
* <span data-ttu-id="9351a-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="9351a-115">RelativeLocation</span></span>

<span data-ttu-id="9351a-116">Hallo stappen zijn:</span><span class="sxs-lookup"><span data-stu-id="9351a-116">hello steps you take are:</span></span>

1. <span data-ttu-id="9351a-117">Meld u aan tooyour Azure Resource Manager-account.</span><span class="sxs-lookup"><span data-stu-id="9351a-117">Sign in tooyour Azure Resource Manager account.</span></span>
2. <span data-ttu-id="9351a-118">Hallo webservicedefinitie ophalen</span><span class="sxs-lookup"><span data-stu-id="9351a-118">Get hello web service definition</span></span>
3. <span data-ttu-id="9351a-119">Hallo webservicedefinitie exporteren als JSON</span><span class="sxs-lookup"><span data-stu-id="9351a-119">Export hello Web Service Definition as JSON</span></span>
4. <span data-ttu-id="9351a-120">Hallo referentie toohello ilearner-blob in Hallo JSON bijwerken.</span><span class="sxs-lookup"><span data-stu-id="9351a-120">Update hello reference toohello ilearner blob in hello JSON.</span></span>
5. <span data-ttu-id="9351a-121">Hallo JSON importeren in de definitie van een Web-Service</span><span class="sxs-lookup"><span data-stu-id="9351a-121">Import hello JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="9351a-122">Hallo webservice bijwerken met definitie van een nieuwe Web-Service</span><span class="sxs-lookup"><span data-stu-id="9351a-122">Update hello web service with new Web Service Definition</span></span>

## <a name="sign-in-tooyour-azure-resource-manager-account"></a><span data-ttu-id="9351a-123">Meld u aan tooyour Azure Resource Manager-account</span><span class="sxs-lookup"><span data-stu-id="9351a-123">Sign in tooyour Azure Resource Manager account</span></span>
<span data-ttu-id="9351a-124">U moet eerst tooyour Azure-account uit binnen Hallo PowerShell-omgeving met Hallo aanmelden [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9351a-124">You must first sign in tooyour Azure account from within hello PowerShell environment using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition"></a><span data-ttu-id="9351a-125">Hallo webservicedefinitie ophalen</span><span class="sxs-lookup"><span data-stu-id="9351a-125">Get hello Web Service Definition</span></span>
<span data-ttu-id="9351a-126">Vervolgens ophalen Hallo Web Service door de aanroepende Hallo [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9351a-126">Next, get hello Web Service by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="9351a-127">Hallo webservicedefinitie is een interne representatie van het getrainde model van de webservice Hallo Hallo en kan niet rechtstreeks worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="9351a-127">hello Web Service Definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="9351a-128">Zorg ervoor dat u voor uw Voorspellend experiment en niet uw trainingsexperiment Hallo webservicedefinitie ophaalt.</span><span class="sxs-lookup"><span data-stu-id="9351a-128">Make sure that you are retrieving hello Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="9351a-129">toodetermine hello Resourcegroepnaam van een bestaande webservice Hallo Get AzureRmMlWebService cmdlet zonder parameters toodisplay Hallo webservices uitvoeren in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="9351a-129">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="9351a-130">Zoek Hallo webservice en zoek vervolgens naar de web service-ID.</span><span class="sxs-lookup"><span data-stu-id="9351a-130">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="9351a-131">Hallo-naam van de resourcegroep Hallo Hallo vierde element in het Hallo-ID is direct na Hallo *resourceGroups* element.</span><span class="sxs-lookup"><span data-stu-id="9351a-131">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="9351a-132">Hallo Resourcegroepnaam is in Hallo voorbeeld te volgen, standaard-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="9351a-132">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="9351a-133">U kunt ook toodetermine hello Resourcegroepnaam van een bestaande webservice aanmelden toohello Microsoft Azure Machine Learning Web Services-portal.</span><span class="sxs-lookup"><span data-stu-id="9351a-133">Alternatively, toodetermine hello resource group name of an existing web service, log on toohello Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="9351a-134">Hallo-webservice selecteren.</span><span class="sxs-lookup"><span data-stu-id="9351a-134">Select hello web service.</span></span> <span data-ttu-id="9351a-135">naam resourcegroep Hallo Hallo vijfde element van het Hallo-URL van webservice hello, wordt direct na Hallo *resourceGroups* element.</span><span class="sxs-lookup"><span data-stu-id="9351a-135">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="9351a-136">Hallo Resourcegroepnaam is in Hallo voorbeeld te volgen, standaard-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="9351a-136">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a><span data-ttu-id="9351a-137">Hallo webservicedefinitie exporteren als JSON</span><span class="sxs-lookup"><span data-stu-id="9351a-137">Export hello Web Service Definition as JSON</span></span>
<span data-ttu-id="9351a-138">toomodify hello definitie toohello getraind model toouse Hallo zojuist getrainde Model, moet u eerst hello gebruiken [Export AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport het bestand tooa JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="9351a-138">toomodify hello definition toohello trained model toouse hello newly Trained Model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a><span data-ttu-id="9351a-139">Hallo referentie toohello ilearner-blob in Hallo JSON bijwerken.</span><span class="sxs-lookup"><span data-stu-id="9351a-139">Update hello reference toohello ilearner blob in hello JSON.</span></span>
<span data-ttu-id="9351a-140">Zoek in Hallo activa, Hallo [getraind model] update Hallo *uri* waarde in Hallo *locationInfo* knooppunt met Hallo URI van Hallo ilearner-blob.</span><span class="sxs-lookup"><span data-stu-id="9351a-140">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="9351a-141">Hallo URI gegenereerd door een combinatie van Hallo *BaseLocation* en Hallo *RelativeLocation* van uitvoer Hallo Hallo BES retraining-aanroep.</span><span class="sxs-lookup"><span data-stu-id="9351a-141">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span> <span data-ttu-id="9351a-142">Hiermee werkt Hallo pad tooreference Hallo nieuwe getrainde model.</span><span class="sxs-lookup"><span data-stu-id="9351a-142">This updates hello path tooreference hello new trained model.</span></span>

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

## <a name="import-hello-json-into-a-web-service-definition"></a><span data-ttu-id="9351a-143">Hallo JSON importeren in de definitie van een Web-Service</span><span class="sxs-lookup"><span data-stu-id="9351a-143">Import hello JSON into a Web Service Definition</span></span>
<span data-ttu-id="9351a-144">Moet u Hallo [importeren AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert Hallo JSON-bestand weer in de definitie van een Web-Service waarmee u tooupdate hello webservicedefinitie kunt is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="9351a-144">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition that you can use tooupdate hello Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a><span data-ttu-id="9351a-145">Hallo webservice bijwerken met definitie van een nieuwe Web-Service</span><span class="sxs-lookup"><span data-stu-id="9351a-145">Update hello web service with new Web Service Definition</span></span>
<span data-ttu-id="9351a-146">Gebruik tot slot [Update AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello webservicedefinitie.</span><span class="sxs-lookup"><span data-stu-id="9351a-146">Finally, you use [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="9351a-147">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="9351a-147">Summary</span></span>
<span data-ttu-id="9351a-148">Hallo Machine Learning PowerShell-cmdlets voor beheer kunt u Hallo getraind model van een Voorspellend webservice inschakelen van scenario's zoals bijwerken:</span><span class="sxs-lookup"><span data-stu-id="9351a-148">Using hello Machine Learning PowerShell management cmdlets, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="9351a-149">Periodieke model retraining met nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="9351a-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="9351a-150">Distributie van een model toocustomers met Hallo doel van zodat ze opnieuw trainen Hallo-model met hun eigen gegevens.</span><span class="sxs-lookup"><span data-stu-id="9351a-150">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

