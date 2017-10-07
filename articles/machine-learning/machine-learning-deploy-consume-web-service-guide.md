---
title: 'Azure Machine Learning-webservices: De implementatie en het verbruik | Microsoft Docs'
description: Bronnen voor het implementeren en gebruiken van web-services.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="7eb49-103">Azure Machine Learning-webservices: implementatie en verbruik</span><span class="sxs-lookup"><span data-stu-id="7eb49-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="7eb49-104">U kunt Azure Machine Learning toodeploy machine learning-werkstromen en modellen als webservices gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7eb49-104">You can use Azure Machine Learning toodeploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="7eb49-105">Deze webservices kunnen vervolgens gebruikte toocall Hallo machine learning-modellen van toepassingen worden via Hallo Internet toodo voorspellingen in realtime of in de batchmodus.</span><span class="sxs-lookup"><span data-stu-id="7eb49-105">These web services can then be used toocall hello machine-learning models from applications over hello Internet toodo predictions in real time or in batch mode.</span></span> <span data-ttu-id="7eb49-106">Omdat de webservices Hallo RESTful, kunt u ze aanroepen uit verschillende programmeertalen en platforms, zoals .NET en Java, en toepassingen, zoals Excel.</span><span class="sxs-lookup"><span data-stu-id="7eb49-106">Because hello web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="7eb49-107">Hallo volgende secties vindt u koppelingen toowalkthroughs, code en documentatie toohelp slag ophalen.</span><span class="sxs-lookup"><span data-stu-id="7eb49-107">hello next sections provide links toowalkthroughs, code, and documentation toohelp get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="7eb49-108">Een webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="7eb49-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="7eb49-109">Met Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="7eb49-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="7eb49-110">Machine Learning Studio en het Hallo-portal voor Microsoft Azure Machine Learning-webservices te implementeren en beheren van een webservice zonder code te schrijven.</span><span class="sxs-lookup"><span data-stu-id="7eb49-110">Machine Learning Studio and hello Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="7eb49-111">Hallo volgende koppelingen vindt u algemene informatie over het toodeploy een nieuwe webservice:</span><span class="sxs-lookup"><span data-stu-id="7eb49-111">hello following links provide general Information about how toodeploy a new web service:</span></span>

* <span data-ttu-id="7eb49-112">Voor een overzicht van hoe toodeploy een nieuwe webservice die gebaseerd op Azure Resource Manager, Zie [implementeren van een nieuwe webservice](machine-learning-webservice-deploy-a-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="7eb49-112">For an overview about how toodeploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="7eb49-113">Voor een overzicht over het toodeploy een webservice, Zie [Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="7eb49-113">For a walkthrough about how toodeploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="7eb49-114">Voor een overzicht over het toocreate en implementeren van een webservice, Zie [scenario stap 1: een Machine Learning-werkruimte maken](machine-learning-walkthrough-1-create-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="7eb49-114">For a full walkthrough about how toocreate and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="7eb49-115">Zie voor specifieke voorbeelden die een webservice implementeert:</span><span class="sxs-lookup"><span data-stu-id="7eb49-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="7eb49-116">Scenario-stap 5: Hello Azure Machine Learning-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="7eb49-116">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="7eb49-117">Hoe toodeploy een web service toomultiple regio 's</span><span class="sxs-lookup"><span data-stu-id="7eb49-117">How toodeploy a web service toomultiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="7eb49-118">Met web services resourceprovider API's (Azure Resource Manager-API's)</span><span class="sxs-lookup"><span data-stu-id="7eb49-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="7eb49-119">Hello Azure Machine Learning resourceprovider voor web-services kan implementatie en beheer van web-services via REST API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="7eb49-119">hello Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="7eb49-120">Zie voor meer informatie de [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) verwijzing.</span><span class="sxs-lookup"><span data-stu-id="7eb49-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="7eb49-121">Met PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="7eb49-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="7eb49-122">Azure Machine Learning-resourceprovider voor webservices kunt implementatie en beheer van web-services met behulp van PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="7eb49-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="7eb49-123">toouse hello cmdlets, u moet zich eerst aanmelden tooyour Azure-account uit binnen Hallo PowerShell-omgeving met behulp van Hallo [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7eb49-123">toouse hello cmdlets, you must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="7eb49-124">Als u niet bekend bent met het hoe toocall PowerShell-opdrachten die op Resource Manager zijn gebaseerd, Zie [Azure PowerShell gebruiken met Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="7eb49-124">If you are unfamiliar with how toocall PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="7eb49-125">tooexport uw Voorspellend experiment, gebruikt u [deze voorbeeldcode](https://github.com/ritwik20/AzureML-WebServices).</span><span class="sxs-lookup"><span data-stu-id="7eb49-125">tooexport your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="7eb49-126">Nadat u Hallo .exe-bestand van het Hallo-code hebt gemaakt, kunt u het volgende typen:</span><span class="sxs-lookup"><span data-stu-id="7eb49-126">After you create hello .exe file from hello code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="7eb49-127">Hallo toepassing uitvoert, maakt een web service JSON-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="7eb49-127">Running hello application creates a web service JSON template.</span></span> <span data-ttu-id="7eb49-128">toouse hello sjabloon toodeploy een webservice, moet u Hallo volgende informatie toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7eb49-128">toouse hello template toodeploy a web service, you must add hello following information:</span></span>

* <span data-ttu-id="7eb49-129">Naam van het opslagaccount en de sleutel</span><span class="sxs-lookup"><span data-stu-id="7eb49-129">Storage account name and key</span></span>

    <span data-ttu-id="7eb49-130">U kunt Hallo opslagaccountnaam en sleutel ophalen van beide Hallo [Azure-portal](https://portal.azure.com/) of Hallo [klassieke Azure-portal](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="7eb49-130">You can get hello storage account name and key from either hello [Azure portal](https://portal.azure.com/) or hello [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="7eb49-131">Het streven plan-ID</span><span class="sxs-lookup"><span data-stu-id="7eb49-131">Commitment plan ID</span></span>

    <span data-ttu-id="7eb49-132">U kunt Hallo plan-ID ophalen uit Hallo [Azure Machine Learning-webservices](https://services.azureml.net) portal aanmelden en de naam van een abonnement op.</span><span class="sxs-lookup"><span data-stu-id="7eb49-132">You can get hello plan ID from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="7eb49-133">Deze toohello JSON-sjabloon toevoegen als onderliggende Hallo *eigenschappen* knooppunt op Hallo van hetzelfde niveau als Hallo *MachineLearningWorkspace* knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7eb49-133">Add them toohello JSON template as children of hello *Properties* node at hello same level as hello *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="7eb49-134">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7eb49-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="7eb49-135">Zie Hallo artikelen te volgen en voorbeeldcode voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="7eb49-135">See hello following articles and sample code for additional details:</span></span>

* <span data-ttu-id="7eb49-136">[Azure Machine Learning-Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) -verwijzingen op MSDN</span><span class="sxs-lookup"><span data-stu-id="7eb49-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="7eb49-137">Voorbeeld [scenario](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) op GitHub</span><span class="sxs-lookup"><span data-stu-id="7eb49-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-hello-web-services"></a><span data-ttu-id="7eb49-138">Hallo-webservices gebruiken</span><span class="sxs-lookup"><span data-stu-id="7eb49-138">Consume hello web services</span></span>
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="7eb49-139">Hallo van Azure Machine Learning Web Services UI (getest)</span><span class="sxs-lookup"><span data-stu-id="7eb49-139">From hello Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="7eb49-140">U kunt uw webservice vanuit hello Azure Machine Learning-webservices portal testen.</span><span class="sxs-lookup"><span data-stu-id="7eb49-140">You can test your web service from hello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="7eb49-141">Dit omvat Hallo aanvraag en antwoord-service (RSS) testen en batchuitvoeringsservice (BES)-interfaces.</span><span class="sxs-lookup"><span data-stu-id="7eb49-141">This includes testing hello Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="7eb49-142">Een nieuwe webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="7eb49-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* [<span data-ttu-id="7eb49-143">Een Azure Machine Learning-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="7eb49-143">Deploy an Azure Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
* [<span data-ttu-id="7eb49-144">Scenario-stap 5: Hello Azure Machine Learning-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="7eb49-144">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="7eb49-145">Vanuit Excel</span><span class="sxs-lookup"><span data-stu-id="7eb49-145">From Excel</span></span>
<span data-ttu-id="7eb49-146">U kunt een Excel-sjabloon die de webservice Hallo verbruikt downloaden:</span><span class="sxs-lookup"><span data-stu-id="7eb49-146">You can download an Excel template that consumes hello web service:</span></span>

* [<span data-ttu-id="7eb49-147">Een Azure Machine Learning-webservice vanuit Excel gebruiken</span><span class="sxs-lookup"><span data-stu-id="7eb49-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="7eb49-148">Excel-invoegtoepassing voor Azure Machine Learning-webservices</span><span class="sxs-lookup"><span data-stu-id="7eb49-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="7eb49-149">Van een REST-client</span><span class="sxs-lookup"><span data-stu-id="7eb49-149">From a REST-based client</span></span>
<span data-ttu-id="7eb49-150">Azure Machine Learning-webservices zijn RESTful-API's.</span><span class="sxs-lookup"><span data-stu-id="7eb49-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="7eb49-151">U kunt deze API's van verschillende platforms, zoals .NET, Python, R, Java, enz. Hallo verbruiken **verbruiken** pagina voor uw webservice op Hallo [portal voor Microsoft Azure Machine Learning-webservices](https://services.azureml.net) voorbeeld heeft code die u kan helpen aan de slag.</span><span class="sxs-lookup"><span data-stu-id="7eb49-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. hello **Consume** page for your web service on hello [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="7eb49-152">Zie voor meer informatie [hoe een Azure Machine Learning-webservice tooconsume](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="7eb49-152">For more information, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>
