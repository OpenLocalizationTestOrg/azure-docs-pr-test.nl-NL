---
title: Een Machine Learning-webservice met de sjabloon voor een web-apps gebruiken | Microsoft Docs
description: Gebruik de sjabloon voor een web-apps in Azure Marketplace gebruiken voor een Voorspellend webservice in Azure Machine Learning.
keywords: Web-service, uitoefening, REST API, machine learning
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 95aa1fa23d83ec0dcd00870179167e803bafbd16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="61dc0-104">Een Azure Machine Learning-webservice gebruiken met een web-app-sjabloon</span><span class="sxs-lookup"><span data-stu-id="61dc0-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="61dc0-105">Eenmaal hebt u uw Voorspellend model ontwikkeld en geïmplementeerd als een Azure-web-service met behulp van Machine Learning Studio of hulpprogramma's zoals R- of Python gebruikt, u toegang tot het operationalized model met behulp van een REST-API.</span><span class="sxs-lookup"><span data-stu-id="61dc0-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access the operationalized model using a REST API.</span></span>

<span data-ttu-id="61dc0-106">Er zijn een aantal manieren om de REST-API gebruiken en toegang tot de webservice.</span><span class="sxs-lookup"><span data-stu-id="61dc0-106">There are a number of ways to consume the REST API and access the web service.</span></span> <span data-ttu-id="61dc0-107">U kunt bijvoorbeeld een toepassing schrijven in C#, R of Python met behulp van de voorbeeldcode voor u gegenereerd tijdens de implementatie van de webservice (beschikbaar in de [Machine Learning Web Services-Portal](https://services.azureml.net/quickstart) of in het dashboard van de web-service op computer Learning Studio).</span><span class="sxs-lookup"><span data-stu-id="61dc0-107">For example, you can write an application in C#, R, or Python using the sample code generated for you when you deployed the web service (available in the [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in the web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="61dc0-108">Of u kunt de voorbeeld Microsoft Excel-werkmap die voor u gemaakt op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="61dc0-108">Or you can use the sample Microsoft Excel workbook created for you at the same time.</span></span>

<span data-ttu-id="61dc0-109">Maar de snelste en gemakkelijkste manier toegang krijgen tot uw webservice is via het Web-App sjablonen die beschikbaar zijn in de [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span><span class="sxs-lookup"><span data-stu-id="61dc0-109">But the quickest and easiest way to access your web service is through the Web App Templates available in the [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="the-azure-machine-learning-web-app-templates"></a><span data-ttu-id="61dc0-110">De Azure Machine Learning-sjablonen voor Web-App</span><span class="sxs-lookup"><span data-stu-id="61dc0-110">The Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="61dc0-111">De web-app beschikbare sjablonen in Azure Marketplace kunnen maken van een aangepaste web-app dat de invoergegevens van uw webservice en de verwachte resultaten kent.</span><span class="sxs-lookup"><span data-stu-id="61dc0-111">The web app templates available in the Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="61dc0-112">U hoeft te doen is de web-app-toegang geven tot uw web-service en -gegevens en doet de rest van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="61dc0-112">All you need to do is give the web app access to your web service and data, and the template does the rest.</span></span>

<span data-ttu-id="61dc0-113">Twee sjablonen zijn beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="61dc0-113">Two templates are available:</span></span>

* [<span data-ttu-id="61dc0-114">Azure ML-aanvragen en antwoorden Service Web-App-sjabloon</span><span class="sxs-lookup"><span data-stu-id="61dc0-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="61dc0-115">Azure ML-Batch uitvoering Web App servicesjabloon</span><span class="sxs-lookup"><span data-stu-id="61dc0-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="61dc0-116">Elke sjabloon een voorbeeldtoepassing ASP.NET, met behulp van de API-URI en sleutel van uw web-service maakt en implementeert dit als een website naar Azure.</span><span class="sxs-lookup"><span data-stu-id="61dc0-116">Each template creates a sample ASP.NET application, using the API URI and Key for your web service, and deploys it as a web site to Azure.</span></span> <span data-ttu-id="61dc0-117">De aanvraag en antwoord-Service (RR's)-sjabloon maakt u een web-app waarmee u één rij met gegevens verzenden naar de webservice moet een enkelvoudig resultaat wordt verkregen.</span><span class="sxs-lookup"><span data-stu-id="61dc0-117">The Request-Response Service (RRS) template creates a web app that allows you to send a single row of data to the web service to get a single result.</span></span> <span data-ttu-id="61dc0-118">De Service Batch-uitvoering (BES)-sjabloon maakt u een web-app waarmee u veel rijen gegevens ophalen van meerdere resultaten te verzenden.</span><span class="sxs-lookup"><span data-stu-id="61dc0-118">The Batch Execution Service (BES) template creates a web app that allows you to send many rows of data to get multiple results.</span></span>

<span data-ttu-id="61dc0-119">Er is geen codering is vereist om deze sjablonen te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="61dc0-119">No coding is required to use these templates.</span></span> <span data-ttu-id="61dc0-120">U gewoon de API-sleutel en de URI en de sjabloon wordt de toepassing voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="61dc0-120">You just supply the API Key and URI, and the template builds the application for you.</span></span>

<span data-ttu-id="61dc0-121">Ophalen van de API-sleutel en de aanvraag-URI voor een webservice:</span><span class="sxs-lookup"><span data-stu-id="61dc0-121">To get the API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="61dc0-122">In de [Web Services-Portal](https://services.azureml.net/quickstart), voor een nieuwe webservice, klikt u op **webservices** aan de bovenkant.</span><span class="sxs-lookup"><span data-stu-id="61dc0-122">In the [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at the top.</span></span> <span data-ttu-id="61dc0-123">Of voor een klassieke web service Klik **klassieke webservices**.</span><span class="sxs-lookup"><span data-stu-id="61dc0-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="61dc0-124">Klik op de webservice die u wilt openen.</span><span class="sxs-lookup"><span data-stu-id="61dc0-124">Click the web service you want to access.</span></span>
3. <span data-ttu-id="61dc0-125">Een klassieke-webservice, klikt u op het eindpunt dat u wilt openen.</span><span class="sxs-lookup"><span data-stu-id="61dc0-125">For a Classic web service, click the endpoint you want to access.</span></span>
4. <span data-ttu-id="61dc0-126">Klik op **verbruiken** aan de bovenkant.</span><span class="sxs-lookup"><span data-stu-id="61dc0-126">Click **Consume** at the top.</span></span>
5. <span data-ttu-id="61dc0-127">Kopieer de **primaire** of **secundaire sleutel** en op te slaan.</span><span class="sxs-lookup"><span data-stu-id="61dc0-127">Copy the **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="61dc0-128">Als u een aanvraag en antwoord-Service (RR's)-sjabloon maakt, kopieert u de **aanvragen en antwoorden** URI en op te slaan.</span><span class="sxs-lookup"><span data-stu-id="61dc0-128">If you're creating a Request-Response Service (RRS) template, copy the **Request-Response** URI and save it.</span></span> <span data-ttu-id="61dc0-129">Als u een Batch uitvoering Service (BES)-sjabloon maakt, kopieert u de **batchaanvragen** URI en op te slaan.</span><span class="sxs-lookup"><span data-stu-id="61dc0-129">If you're creating a Batch Execution Service (BES) template, copy the **Batch Requests** URI and save it.</span></span>


## <a name="how-to-use-the-request-response-service-rrs-template"></a><span data-ttu-id="61dc0-130">Het gebruik van de sjabloon voor de aanvraag en antwoord-Service (RR's)</span><span class="sxs-lookup"><span data-stu-id="61dc0-130">How to use the Request-Response Service (RRS) template</span></span>
<span data-ttu-id="61dc0-131">Volg deze stappen voor het gebruik van de sjabloon RRS web app, zoals wordt weergegeven in het volgende diagram.</span><span class="sxs-lookup"><span data-stu-id="61dc0-131">Follow these steps to use the RRS web app template, as shown in the following diagram.</span></span>

![Proces RRS websjabloon gebruiken][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="61dc0-133">Ga naar de [Azure-portal](https://portal.azure.com), **aanmelding**, klikt u op **nieuw**, zoekt en selecteert u **Web-App voor Azure ML aanvragen en antwoorden Service**, klikt u vervolgens op  **Maak**.</span><span class="sxs-lookup"><span data-stu-id="61dc0-133">Go to the [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="61dc0-134">Een unieke naam voor uw web-app geven.</span><span class="sxs-lookup"><span data-stu-id="61dc0-134">Give your web app a unique name.</span></span> <span data-ttu-id="61dc0-135">De URL van de web-app wordt deze gevolgd door naam worden `.azurewebsites.net.` bijvoorbeeld:`http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="61dc0-135">The URL of the web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="61dc0-136">Selecteer de Azure-abonnement en services, waaronder uw webservice wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="61dc0-136">Select the Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="61dc0-137">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="61dc0-137">Click **Create**.</span></span>
     
     ![Een web-app maken][image5]

4. <span data-ttu-id="61dc0-139">Wanneer de web-app implementeren, Azure is voltooid, klikt u op de **URL** pagina op de instellingen voor web-app in Azure of Voer de URL in een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="61dc0-139">When Azure has finished deploying the web app, click the **URL** on the web app settings page in Azure, or enter the URL in a web browser.</span></span> <span data-ttu-id="61dc0-140">Bijvoorbeeld: `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="61dc0-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="61dc0-141">Wanneer de web-app voor het eerst wordt uitgevoerd, wordt u gevraagt voor de **API Post URL** en **API-sleutel**.</span><span class="sxs-lookup"><span data-stu-id="61dc0-141">When the web app first runs it will ask you for the **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="61dc0-142">Voer de waarden die u eerder hebt opgeslagen (**aanvraag-URI** en **API-sleutel**respectievelijk).</span><span class="sxs-lookup"><span data-stu-id="61dc0-142">Enter the values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="61dc0-143">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="61dc0-143">Click **Submit**.</span></span>
     
     ![Voer Post URI en API-sleutel][image6]

6. <span data-ttu-id="61dc0-145">De web-app wordt weergegeven de **Web-App-configuratie** pagina met de huidige instellingen voor web-service.</span><span class="sxs-lookup"><span data-stu-id="61dc0-145">The web app displays its **Web App Configuration** page with the current web service settings.</span></span> <span data-ttu-id="61dc0-146">Hier kunt u wijzigingen aanbrengen in de instellingen die worden gebruikt door de web-app.</span><span class="sxs-lookup"><span data-stu-id="61dc0-146">Here you can make changes to the settings used by the web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="61dc0-147">Deze instellingen alleen wijzigt, worden ze voor deze web-app.</span><span class="sxs-lookup"><span data-stu-id="61dc0-147">Changing the settings here only changes them for this web app.</span></span> <span data-ttu-id="61dc0-148">Deze wijzigen de standaardinstellingen van uw web-service niet.</span><span class="sxs-lookup"><span data-stu-id="61dc0-148">It doesn't change the default settings of your web service.</span></span> <span data-ttu-id="61dc0-149">Als u bijvoorbeeld de **beschrijving** Hier wordt de beschrijving weergegeven op het web service-dashboard in Machine Learning Studio niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="61dc0-149">For example, if you change the **Description** here it doesn't change the description shown on the web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="61dc0-150">Wanneer u bent klaar, klikt u op **wijzigingen opslaan**, en klik vervolgens op **gaat u naar de startpagina**.</span><span class="sxs-lookup"><span data-stu-id="61dc0-150">When you're done, click **Save changes**, and then click **Go to Home Page**.</span></span>

7. <span data-ttu-id="61dc0-151">U kunt waarden om te verzenden naar uw webservice invoeren vanaf de startpagina.</span><span class="sxs-lookup"><span data-stu-id="61dc0-151">From the home page you can enter values to send to your web service.</span></span> <span data-ttu-id="61dc0-152">Klik op **indienen** wanneer u klaar bent, en het resultaat wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="61dc0-152">Click **Submit** when you're done, and the result will be returned.</span></span>

<span data-ttu-id="61dc0-153">Als u terugkeren wilt naar de **configuratie** pagina, gaat u naar de `setting.aspx` pagina van de web-app.</span><span class="sxs-lookup"><span data-stu-id="61dc0-153">If you want to return to the **Configuration** page, go to the `setting.aspx` page of the web app.</span></span> <span data-ttu-id="61dc0-154">Bijvoorbeeld: `http://carprediction.azurewebsites.net/setting.aspx.` wordt u gevraagd de API-sleutel opnieuw invoeren: u hebt nodig die toegang tot de pagina en de instellingen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="61dc0-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted to enter the API key again - you need that to access the page and update the settings.</span></span>

<span data-ttu-id="61dc0-155">U kunt stoppen, starten of te verwijderen van de web-app in de Azure portal als elke andere web-app.</span><span class="sxs-lookup"><span data-stu-id="61dc0-155">You can stop, restart, or delete the web app in the Azure portal like any other web app.</span></span> <span data-ttu-id="61dc0-156">U kunt bladeren naar het oorspronkelijke webadres en voer nieuwe waarden, zolang deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="61dc0-156">As long as it is running you can browse to the home web address and enter new values.</span></span>

## <a name="how-to-use-the-batch-execution-service-bes-template"></a><span data-ttu-id="61dc0-157">Het gebruik van de sjabloon Batch uitvoering Service (BES)</span><span class="sxs-lookup"><span data-stu-id="61dc0-157">How to use the Batch Execution Service (BES) template</span></span>
<span data-ttu-id="61dc0-158">Behalve dat de web-app die gemaakt, kunt u meerdere rijen met gegevens te verzenden en ontvangen van meerdere resultaten, kunt u de sjabloon BES web-app op dezelfde manier als de RSS-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="61dc0-158">You can use the BES web app template in the same way as the RRS template, except that the web app that's created will allow you to submit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="61dc0-159">De ingevoerde waarden voor een webservice van de batch-uitvoering kunnen afkomstig zijn van Azure-opslag of een lokaal bestand; de resultaten worden opgeslagen in een Azure storage-container.</span><span class="sxs-lookup"><span data-stu-id="61dc0-159">The input values for a batch execution web service can come from Azure storage or a local file; the results are stored in an Azure storage container.</span></span>
<span data-ttu-id="61dc0-160">Daarom moet u een Azure storage-container voor het opslaan van de resultaten van de web-app en moet u bereid u voor uw invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="61dc0-160">So, you'll need an Azure storage container to hold the results returned by the web app, and you'll need to get your input data ready.</span></span>

![Proces BES websjabloon gebruiken][image2]

1. <span data-ttu-id="61dc0-162">Volg dezelfde procedure voor het maken van de web-app voor BES als voor de sjabloon RRS behalve gaat u naar [Azure ML Batch uitvoering Web App servicesjabloon](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) de sjabloon BES op Azure Marketplace openen en klik op **Web-App maken**.</span><span class="sxs-lookup"><span data-stu-id="61dc0-162">Follow the same procedure to create the BES web app as for the RRS template, except go to [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) to open the BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="61dc0-163">Waar u de resultaten die zijn opgeslagen, typ de doelgegevens container op de startpagina van de web-app.</span><span class="sxs-lookup"><span data-stu-id="61dc0-163">To specify where you want the results stored, enter the destination container information on the web app home page.</span></span> <span data-ttu-id="61dc0-164">Ook kunt u opgeven waar de web-app de invoerwaarden in een lokaal bestand of een Azure storage-container kan krijgen.</span><span class="sxs-lookup"><span data-stu-id="61dc0-164">Also specify where the web app can get the input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="61dc0-165">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="61dc0-165">Click **Submit**.</span></span>
   
    ![Storage-gegevens][image7]

<span data-ttu-id="61dc0-167">De web-app wordt een pagina met de taakstatus weergegeven.</span><span class="sxs-lookup"><span data-stu-id="61dc0-167">The web app will display a page with job status.</span></span>
<span data-ttu-id="61dc0-168">Wanneer de taak is voltooid krijgt u de locatie van de resultaten in Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="61dc0-168">When the job has completed you'll be given the location of the results in Azure blob storage.</span></span> <span data-ttu-id="61dc0-169">U hebt ook de optie van de resultaten naar een lokaal bestand downloaden.</span><span class="sxs-lookup"><span data-stu-id="61dc0-169">You also have the option of downloading the results to a local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="61dc0-170">Voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="61dc0-170">For more information</span></span>
<span data-ttu-id="61dc0-171">Voor meer informatie over...</span><span class="sxs-lookup"><span data-stu-id="61dc0-171">To learn more about...</span></span>

* <span data-ttu-id="61dc0-172">het maken van een machine learning-experiment met Machine Learning Studio, Zie [uw eerste experiment maken in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span><span class="sxs-lookup"><span data-stu-id="61dc0-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="61dc0-173">het implementeren van uw machine learning-experiment als een webservice, Zie [een Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="61dc0-173">how to deploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="61dc0-174">Zie andere manieren om uw webservice [gebruiken van een Azure Machine Learning-webservice](machine-learning-consume-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="61dc0-174">other ways to access your web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md)</span></span>

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
