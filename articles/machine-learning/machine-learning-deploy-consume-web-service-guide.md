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
ms.openlocfilehash: 18edabe267ec06c08074d7a7a6d71435cedc8489
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="20e9c-103">Azure Machine Learning-webservices: implementatie en verbruik</span><span class="sxs-lookup"><span data-stu-id="20e9c-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="20e9c-104">U kunt Azure Machine Learning gebruiken machine learning werkstromen en modellen als webservices te implementeren.</span><span class="sxs-lookup"><span data-stu-id="20e9c-104">You can use Azure Machine Learning to deploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="20e9c-105">Deze webservices kunnen vervolgens worden gebruikt voor het aanroepen van de machine learning-modellen van toepassingen via Internet te doen voorspellingen in realtime of in de batchmodus.</span><span class="sxs-lookup"><span data-stu-id="20e9c-105">These web services can then be used to call the machine-learning models from applications over the Internet to do predictions in real time or in batch mode.</span></span> <span data-ttu-id="20e9c-106">Omdat de webservices RESTful, kunt u ze aanroepen uit verschillende programmeertalen en platforms, zoals .NET en Java, en toepassingen, zoals Excel.</span><span class="sxs-lookup"><span data-stu-id="20e9c-106">Because the web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="20e9c-107">De volgende secties vindt u koppelingen naar procedures, code en documentatie waarmee u op weg.</span><span class="sxs-lookup"><span data-stu-id="20e9c-107">The next sections provide links to walkthroughs, code, and documentation to help get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="20e9c-108">Een webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="20e9c-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="20e9c-109">Met Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="20e9c-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="20e9c-110">Machine Learning Studio en de portal voor Microsoft Azure Machine Learning-webservices te implementeren en beheren van een webservice zonder code te schrijven.</span><span class="sxs-lookup"><span data-stu-id="20e9c-110">Machine Learning Studio and the Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="20e9c-111">De volgende koppelingen vindt algemene informatie over het implementeren van een nieuwe webservice:</span><span class="sxs-lookup"><span data-stu-id="20e9c-111">The following links provide general Information about how to deploy a new web service:</span></span>

* <span data-ttu-id="20e9c-112">Zie voor een overzicht over het implementeren van een nieuwe webservice die gebaseerd op Azure Resource Manager [implementeren van een nieuwe webservice](machine-learning-webservice-deploy-a-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="20e9c-112">For an overview about how to deploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="20e9c-113">Zie voor een overzicht over het implementeren van een webservice [Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="20e9c-113">For a walkthrough about how to deploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="20e9c-114">Zie voor een volledig overzicht over het maken en implementeren van een webservice [scenario stap 1: een Machine Learning-werkruimte maken](machine-learning-walkthrough-1-create-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="20e9c-114">For a full walkthrough about how to create and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="20e9c-115">Zie voor specifieke voorbeelden die een webservice implementeert:</span><span class="sxs-lookup"><span data-stu-id="20e9c-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="20e9c-116">Scenario-stap 5: De Azure Machine Learning-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="20e9c-116">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="20e9c-117">Een webservice implementeren op meerdere regio 's</span><span class="sxs-lookup"><span data-stu-id="20e9c-117">How to deploy a web service to multiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="20e9c-118">Met web services resourceprovider API's (Azure Resource Manager-API's)</span><span class="sxs-lookup"><span data-stu-id="20e9c-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="20e9c-119">De Azure Machine Learning-resourceprovider voor webservices kunt implementatie en beheer van web-services met behulp van de REST API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="20e9c-119">The Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="20e9c-120">Zie voor meer informatie de [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) verwijzing.</span><span class="sxs-lookup"><span data-stu-id="20e9c-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="20e9c-121">Met PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="20e9c-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="20e9c-122">Azure Machine Learning-resourceprovider voor webservices kunt implementatie en beheer van web-services met behulp van PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="20e9c-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="20e9c-123">Voor het gebruik van de cmdlets, u moet eerst aanmelden bij uw Azure-account uit binnen de PowerShell-omgeving met behulp van de [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20e9c-123">To use the cmdlets, you must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="20e9c-124">Als u niet bekend bent met het aanroepen van PowerShell-opdrachten die zijn gebaseerd op Resource Manager, raadpleegt [Azure PowerShell gebruiken met Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="20e9c-124">If you are unfamiliar with how to call PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="20e9c-125">Voor het exporteren van uw Voorspellend experiment [deze voorbeeldcode](https://github.com/ritwik20/AzureML-WebServices).</span><span class="sxs-lookup"><span data-stu-id="20e9c-125">To export your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="20e9c-126">Nadat u het .exe-bestand van de code hebt gemaakt, kunt u het volgende typen:</span><span class="sxs-lookup"><span data-stu-id="20e9c-126">After you create the .exe file from the code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="20e9c-127">De toepassing wordt uitgevoerd, maakt een web service JSON-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="20e9c-127">Running the application creates a web service JSON template.</span></span> <span data-ttu-id="20e9c-128">De sjabloon wilt gebruiken voor het implementeren van een webservice, moet u de volgende informatie toevoegen:</span><span class="sxs-lookup"><span data-stu-id="20e9c-128">To use the template to deploy a web service, you must add the following information:</span></span>

* <span data-ttu-id="20e9c-129">Naam van het opslagaccount en de sleutel</span><span class="sxs-lookup"><span data-stu-id="20e9c-129">Storage account name and key</span></span>

    <span data-ttu-id="20e9c-130">U kunt de opslagaccountnaam en sleutel ophalen uit de [Azure-portal](https://portal.azure.com/) of de [klassieke Azure-portal](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="20e9c-130">You can get the storage account name and key from either the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="20e9c-131">Het streven plan-ID</span><span class="sxs-lookup"><span data-stu-id="20e9c-131">Commitment plan ID</span></span>

    <span data-ttu-id="20e9c-132">U krijgt de abonnement-ID van de [Azure Machine Learning-webservices](https://services.azureml.net) portal aanmelden en de naam van een abonnement op.</span><span class="sxs-lookup"><span data-stu-id="20e9c-132">You can get the plan ID from the [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="20e9c-133">Toevoegen aan het JSON-sjabloon als onderliggende elementen van de *eigenschappen* knooppunt op hetzelfde niveau als het *MachineLearningWorkspace* knooppunt.</span><span class="sxs-lookup"><span data-stu-id="20e9c-133">Add them to the JSON template as children of the *Properties* node at the same level as the *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="20e9c-134">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="20e9c-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="20e9c-135">Zie de volgende artikelen en voorbeeldcode voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="20e9c-135">See the following articles and sample code for additional details:</span></span>

* <span data-ttu-id="20e9c-136">[Azure Machine Learning-Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) -verwijzingen op MSDN</span><span class="sxs-lookup"><span data-stu-id="20e9c-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="20e9c-137">Voorbeeld [scenario](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) op GitHub</span><span class="sxs-lookup"><span data-stu-id="20e9c-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-the-web-services"></a><span data-ttu-id="20e9c-138">De webservices</span><span class="sxs-lookup"><span data-stu-id="20e9c-138">Consume the web services</span></span>
### <a name="from-the-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="20e9c-139">Van de Azure Machine Learning-webservices UI (testen)</span><span class="sxs-lookup"><span data-stu-id="20e9c-139">From the Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="20e9c-140">U kunt testen uw webservice via de portal voor Azure Machine Learning-webservices.</span><span class="sxs-lookup"><span data-stu-id="20e9c-140">You can test your web service from the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="20e9c-141">Dit omvat het testen van de aanvraag en antwoord-service (RR's) en interfaces batchuitvoeringsservice (BES).</span><span class="sxs-lookup"><span data-stu-id="20e9c-141">This includes testing the Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="20e9c-142">Een nieuwe webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="20e9c-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* [<span data-ttu-id="20e9c-143">Een Azure Machine Learning-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="20e9c-143">Deploy an Azure Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
* [<span data-ttu-id="20e9c-144">Scenario-stap 5: De Azure Machine Learning-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="20e9c-144">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="20e9c-145">Vanuit Excel</span><span class="sxs-lookup"><span data-stu-id="20e9c-145">From Excel</span></span>
<span data-ttu-id="20e9c-146">U kunt een Excel-sjabloon die de webservice verbruikt downloaden:</span><span class="sxs-lookup"><span data-stu-id="20e9c-146">You can download an Excel template that consumes the web service:</span></span>

* [<span data-ttu-id="20e9c-147">Een Azure Machine Learning-webservice vanuit Excel gebruiken</span><span class="sxs-lookup"><span data-stu-id="20e9c-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="20e9c-148">Excel-invoegtoepassing voor Azure Machine Learning-webservices</span><span class="sxs-lookup"><span data-stu-id="20e9c-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="20e9c-149">Van een REST-client</span><span class="sxs-lookup"><span data-stu-id="20e9c-149">From a REST-based client</span></span>
<span data-ttu-id="20e9c-150">Azure Machine Learning-webservices zijn RESTful-API's.</span><span class="sxs-lookup"><span data-stu-id="20e9c-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="20e9c-151">U kunt deze API's van verschillende platformen, zoals .NET, Python, R, Java, enzovoort verbruiken. De **verbruiken** pagina voor uw webservice op de [portal voor Microsoft Azure Machine Learning-webservices](https://services.azureml.net) voorbeeldcode waarmee u aan de slag kunt heeft.</span><span class="sxs-lookup"><span data-stu-id="20e9c-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. The **Consume** page for your web service on the [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="20e9c-152">Zie [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md) (Azure Machine Learning-webservice gebruiken) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="20e9c-152">For more information, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>
