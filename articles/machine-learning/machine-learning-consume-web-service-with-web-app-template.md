---
title: aaaConsume een Machine Learning-webservice met een web-app-sjabloon | Microsoft Docs
description: Gebruik de sjabloon voor een web-apps in Azure Marketplace tooconsume een Voorspellend webservice in Azure Machine Learning.
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
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="f91c7-104">Een Azure Machine Learning-webservice gebruiken met een web-app-sjabloon</span><span class="sxs-lookup"><span data-stu-id="f91c7-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="f91c7-105">Eenmaal hebt u uw Voorspellend model ontwikkeld en geïmplementeerd als een Azure-web-service met behulp van Machine Learning Studio of hulpprogramma's zoals R- of Python gebruikt, u toegang tot Hallo geoperationaliseerd model met behulp van een REST-API.</span><span class="sxs-lookup"><span data-stu-id="f91c7-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access hello operationalized model using a REST API.</span></span>

<span data-ttu-id="f91c7-106">Er zijn een aantal manieren tooconsume Hallo REST-API en toegang Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="f91c7-106">There are a number of ways tooconsume hello REST API and access hello web service.</span></span> <span data-ttu-id="f91c7-107">Bijvoorbeeld, kunt u een toepassing in C#, R, schrijven of Python Hallo met voorbeeldcode voor u gegenereerd tijdens de implementatie van de webservice Hallo (beschikbaar in Hallo [Machine Learning Web Services-Portal](https://services.azureml.net/quickstart) of in Hallo web servicedashboard in Machine Learning Studio).</span><span class="sxs-lookup"><span data-stu-id="f91c7-107">For example, you can write an application in C#, R, or Python using hello sample code generated for you when you deployed hello web service (available in hello [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in hello web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="f91c7-108">Of u kunt gebruiken voor u gemaakt op Hallo van Hallo voorbeeld Microsoft Excel-werkmap hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="f91c7-108">Or you can use hello sample Microsoft Excel workbook created for you at hello same time.</span></span>

<span data-ttu-id="f91c7-109">Maar de snelste en gemakkelijkste manier tooaccess uw webservice via Hallo Web App sjablonen beschikbaar zijn in Hallo wordt Hallo [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span><span class="sxs-lookup"><span data-stu-id="f91c7-109">But hello quickest and easiest way tooaccess your web service is through hello Web App Templates available in hello [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a><span data-ttu-id="f91c7-110">Hello Azure Machine Learning Web-App-sjablonen</span><span class="sxs-lookup"><span data-stu-id="f91c7-110">hello Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="f91c7-111">Hallo web app sjablonen beschikbaar zijn in Azure Marketplace Hallo kunnen maken van een aangepaste web-app dat de invoergegevens van uw webservice en de verwachte resultaten kent.</span><span class="sxs-lookup"><span data-stu-id="f91c7-111">hello web app templates available in hello Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="f91c7-112">Toodo hoeft u Hallo web app toegang tooyour-webservice en gegevens geven en Hallo sjabloon Hallo rest.</span><span class="sxs-lookup"><span data-stu-id="f91c7-112">All you need toodo is give hello web app access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="f91c7-113">Twee sjablonen zijn beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="f91c7-113">Two templates are available:</span></span>

* [<span data-ttu-id="f91c7-114">Azure ML-aanvragen en antwoorden Service Web-App-sjabloon</span><span class="sxs-lookup"><span data-stu-id="f91c7-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="f91c7-115">Azure ML-Batch uitvoering Web App servicesjabloon</span><span class="sxs-lookup"><span data-stu-id="f91c7-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="f91c7-116">Elke sjabloon een voorbeeldtoepassing ASP.NET, met behulp van Hallo API-URI en sleutel van uw web-service maakt en implementeert dit als een tooAzure website.</span><span class="sxs-lookup"><span data-stu-id="f91c7-116">Each template creates a sample ASP.NET application, using hello API URI and Key for your web service, and deploys it as a web site tooAzure.</span></span> <span data-ttu-id="f91c7-117">Hallo aanvraag en antwoord-Service (RR's)-sjabloon maakt u een web-app waarmee u toosend één rij met gegevens toohello web service tooget een enkelvoudig resultaat wordt verkregen.</span><span class="sxs-lookup"><span data-stu-id="f91c7-117">hello Request-Response Service (RRS) template creates a web app that allows you toosend a single row of data toohello web service tooget a single result.</span></span> <span data-ttu-id="f91c7-118">Hallo Batch uitvoering Service (BES)-sjabloon maakt u een web-app waarmee u toosend veel rijen met gegevens tooget meerdere resultaten.</span><span class="sxs-lookup"><span data-stu-id="f91c7-118">hello Batch Execution Service (BES) template creates a web app that allows you toosend many rows of data tooget multiple results.</span></span>

<span data-ttu-id="f91c7-119">Er is geen codering is vereist toouse deze sjablonen.</span><span class="sxs-lookup"><span data-stu-id="f91c7-119">No coding is required toouse these templates.</span></span> <span data-ttu-id="f91c7-120">U gewoon Hallo API-sleutel en de URI en toepassing hello Hallo-sjabloon is gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="f91c7-120">You just supply hello API Key and URI, and hello template builds hello application for you.</span></span>

<span data-ttu-id="f91c7-121">tooget hello API-sleutel en de aanvraag-URI voor een webservice:</span><span class="sxs-lookup"><span data-stu-id="f91c7-121">tooget hello API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="f91c7-122">In Hallo [Web Services-Portal](https://services.azureml.net/quickstart), voor een nieuwe webservice, klikt u op **webservices** Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="f91c7-122">In hello [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at hello top.</span></span> <span data-ttu-id="f91c7-123">Of voor een klassieke web service Klik **klassieke webservices**.</span><span class="sxs-lookup"><span data-stu-id="f91c7-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="f91c7-124">Klik op de gewenste tooaccess Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="f91c7-124">Click hello web service you want tooaccess.</span></span>
3. <span data-ttu-id="f91c7-125">Een klassieke-webservice, klikt u op Hallo eindpunt gewenste tooaccess.</span><span class="sxs-lookup"><span data-stu-id="f91c7-125">For a Classic web service, click hello endpoint you want tooaccess.</span></span>
4. <span data-ttu-id="f91c7-126">Klik op **verbruiken** Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="f91c7-126">Click **Consume** at hello top.</span></span>
5. <span data-ttu-id="f91c7-127">Kopiëren Hallo **primaire** of **secundaire sleutel** en op te slaan.</span><span class="sxs-lookup"><span data-stu-id="f91c7-127">Copy hello **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="f91c7-128">Als u een aanvraag en antwoord-Service (RR's)-sjabloon maakt, kopieert u Hallo **aanvragen en antwoorden** URI en op te slaan.</span><span class="sxs-lookup"><span data-stu-id="f91c7-128">If you're creating a Request-Response Service (RRS) template, copy hello **Request-Response** URI and save it.</span></span> <span data-ttu-id="f91c7-129">Als u een Batch uitvoering Service (BES)-sjabloon maakt, kopieert u Hallo **batchaanvragen** URI en op te slaan.</span><span class="sxs-lookup"><span data-stu-id="f91c7-129">If you're creating a Batch Execution Service (BES) template, copy hello **Batch Requests** URI and save it.</span></span>


## <a name="how-toouse-hello-request-response-service-rrs-template"></a><span data-ttu-id="f91c7-130">Hoe toouse Hallo sjabloon aanvraag en antwoord-Service (RR's)</span><span class="sxs-lookup"><span data-stu-id="f91c7-130">How toouse hello Request-Response Service (RRS) template</span></span>
<span data-ttu-id="f91c7-131">Volg deze stappen toouse Hallo RRS web-app-sjabloon, zoals wordt weergegeven in het volgende diagram Hallo.</span><span class="sxs-lookup"><span data-stu-id="f91c7-131">Follow these steps toouse hello RRS web app template, as shown in hello following diagram.</span></span>

![Processjabloon toouse RRS web][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="f91c7-133">Ga toohello [Azure-portal](https://portal.azure.com), **aanmelding**, klikt u op **nieuw**, zoekt en selecteert u **Web-App voor Azure ML aanvragen en antwoorden Service**, klikt u vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="f91c7-133">Go toohello [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="f91c7-134">Een unieke naam voor uw web-app geven.</span><span class="sxs-lookup"><span data-stu-id="f91c7-134">Give your web app a unique name.</span></span> <span data-ttu-id="f91c7-135">Hallo-URL van de web-app Hallo worden deze naam gevolgd door `.azurewebsites.net.` bijvoorbeeld:`http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="f91c7-135">hello URL of hello web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="f91c7-136">Selecteer hello Azure-abonnement en services die uw webservice wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f91c7-136">Select hello Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="f91c7-137">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f91c7-137">Click **Create**.</span></span>
     
     ![Een web-app maken][image5]

4. <span data-ttu-id="f91c7-139">Wanneer Azure is voltooid Hallo web-app implementeren, klikt u op Hallo **URL** op Hallo van pagina voor de web-app-instellingen in Azure of Hallo-URL opgeven in een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="f91c7-139">When Azure has finished deploying hello web app, click hello **URL** on hello web app settings page in Azure, or enter hello URL in a web browser.</span></span> <span data-ttu-id="f91c7-140">Bijvoorbeeld: `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="f91c7-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="f91c7-141">Wanneer Hallo web app eerste wordt uitgevoerd, u voor Hallo gevraagt wordt **API Post URL** en **API-sleutel**.</span><span class="sxs-lookup"><span data-stu-id="f91c7-141">When hello web app first runs it will ask you for hello **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="f91c7-142">Voer Hallo-waarden die u eerder hebt opgeslagen (**aanvraag-URI** en **API-sleutel**respectievelijk).</span><span class="sxs-lookup"><span data-stu-id="f91c7-142">Enter hello values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="f91c7-143">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="f91c7-143">Click **Submit**.</span></span>
     
     ![Voer Post URI en API-sleutel][image6]

6. <span data-ttu-id="f91c7-145">Hallo web app geeft de **Web-App-configuratie** pagina met Hallo huidige web service-instellingen.</span><span class="sxs-lookup"><span data-stu-id="f91c7-145">hello web app displays its **Web App Configuration** page with hello current web service settings.</span></span> <span data-ttu-id="f91c7-146">Hier kunt u wijzigingen aanbrengen toohello-instellingen die door Hallo web-app gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f91c7-146">Here you can make changes toohello settings used by hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f91c7-147">Hallo instellingen hier alleen wijzigt, worden ze voor deze web-app.</span><span class="sxs-lookup"><span data-stu-id="f91c7-147">Changing hello settings here only changes them for this web app.</span></span> <span data-ttu-id="f91c7-148">Het wijzigen Hallo-standaardinstellingen van uw web-service niet.</span><span class="sxs-lookup"><span data-stu-id="f91c7-148">It doesn't change hello default settings of your web service.</span></span> <span data-ttu-id="f91c7-149">Bijvoorbeeld, als u Hallo wijzigen **beschrijving** hier het Hallo-beschrijving weergegeven op Hallo web servicedashboard in Machine Learning Studio niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f91c7-149">For example, if you change hello **Description** here it doesn't change hello description shown on hello web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="f91c7-150">Wanneer u bent klaar, klikt u op **wijzigingen opslaan**, en klik vervolgens op **tooHome pagina gaat**.</span><span class="sxs-lookup"><span data-stu-id="f91c7-150">When you're done, click **Save changes**, and then click **Go tooHome Page**.</span></span>

7. <span data-ttu-id="f91c7-151">Startpagina die kunt u waarden van Hallo toosend tooyour-webservice.</span><span class="sxs-lookup"><span data-stu-id="f91c7-151">From hello home page you can enter values toosend tooyour web service.</span></span> <span data-ttu-id="f91c7-152">Klik op **indienen** wanneer u klaar bent en Hallo resultaat geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="f91c7-152">Click **Submit** when you're done, and hello result will be returned.</span></span>

<span data-ttu-id="f91c7-153">Als u wilt dat tooreturn toohello **configuratie** pagina, gaat u toohello `setting.aspx` pagina van Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="f91c7-153">If you want tooreturn toohello **Configuration** page, go toohello `setting.aspx` page of hello web app.</span></span> <span data-ttu-id="f91c7-154">Bijvoorbeeld: `http://carprediction.azurewebsites.net/setting.aspx.` kunt u zich na vragen aan gebruiker tooenter Hallo API-sleutel opnieuw: u hebt nodig dat tooaccess pagina Hallo en Hallo-instellingen worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f91c7-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted tooenter hello API key again - you need that tooaccess hello page and update hello settings.</span></span>

<span data-ttu-id="f91c7-155">U kunt stoppen, starten of te verwijderen van Hallo web-app in hello Azure-portal als elke andere web-app.</span><span class="sxs-lookup"><span data-stu-id="f91c7-155">You can stop, restart, or delete hello web app in hello Azure portal like any other web app.</span></span> <span data-ttu-id="f91c7-156">U kunt toohello thuis webadres bladeren en voer nieuwe waarden, zolang deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f91c7-156">As long as it is running you can browse toohello home web address and enter new values.</span></span>

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a><span data-ttu-id="f91c7-157">Hoe toouse Hallo Batch uitvoering Service (BES)-sjabloon</span><span class="sxs-lookup"><span data-stu-id="f91c7-157">How toouse hello Batch Execution Service (BES) template</span></span>
<span data-ttu-id="f91c7-158">Hallo BES kunt u web-app-sjabloon in Hallo dezelfde manier als Hallo RRS-sjabloon, met uitzondering van die Hallo web-app die gemaakt, kunt u toosubmit meerdere rijen met gegevens en meerdere resultaten krijgt.</span><span class="sxs-lookup"><span data-stu-id="f91c7-158">You can use hello BES web app template in hello same way as hello RRS template, except that hello web app that's created will allow you toosubmit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="f91c7-159">Hallo invoerwaarden voor een webservice van de batch-uitvoering kunnen afkomstig zijn van Azure-opslag of een lokaal bestand; Hallo resultaten worden opgeslagen in een Azure storage-container.</span><span class="sxs-lookup"><span data-stu-id="f91c7-159">hello input values for a batch execution web service can come from Azure storage or a local file; hello results are stored in an Azure storage container.</span></span>
<span data-ttu-id="f91c7-160">Ja, u hebt een Azure storage-container toohold Hallo moet resultaten geretourneerd door Hallo web-app, en moet u tooget uw invoergegevens gereed.</span><span class="sxs-lookup"><span data-stu-id="f91c7-160">So, you'll need an Azure storage container toohold hello results returned by hello web app, and you'll need tooget your input data ready.</span></span>

![Verwerken toouse BES websjabloon][image2]

1. <span data-ttu-id="f91c7-162">Volg dezelfde Hallo procedure toocreate Hallo BES web-app als voor Hallo RRS sjabloon, behalve Ga te[Azure ML Batch uitvoering Web App servicesjabloon](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen Hallo BES sjabloon op Azure Marketplace en klik op **Web-App maken** .</span><span class="sxs-lookup"><span data-stu-id="f91c7-162">Follow hello same procedure toocreate hello BES web app as for hello RRS template, except go too[Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="f91c7-163">toospecify waar u Hallo resultaten die zijn opgeslagen, Geef informatie op Hallo bestemming container op Hallo web-app-startpagina.</span><span class="sxs-lookup"><span data-stu-id="f91c7-163">toospecify where you want hello results stored, enter hello destination container information on hello web app home page.</span></span> <span data-ttu-id="f91c7-164">Ook kunt u opgeven waar vind Hallo web-app Hallo invoerwaarden, in een lokaal bestand of een Azure storage-container.</span><span class="sxs-lookup"><span data-stu-id="f91c7-164">Also specify where hello web app can get hello input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="f91c7-165">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="f91c7-165">Click **Submit**.</span></span>
   
    ![Storage-gegevens][image7]

<span data-ttu-id="f91c7-167">Hallo-web-app wordt een pagina met de taakstatus weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f91c7-167">hello web app will display a page with job status.</span></span>
<span data-ttu-id="f91c7-168">Wanneer het Hallo-taak is voltooid krijgt u Hallo-locatie van Hallo resulteert in een Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="f91c7-168">When hello job has completed you'll be given hello location of hello results in Azure blob storage.</span></span> <span data-ttu-id="f91c7-169">U hebt ook Hallo optie Hallo resultaten tooa lokale bestand te downloaden.</span><span class="sxs-lookup"><span data-stu-id="f91c7-169">You also have hello option of downloading hello results tooa local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="f91c7-170">Voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="f91c7-170">For more information</span></span>
<span data-ttu-id="f91c7-171">meer informatie over toolearn...</span><span class="sxs-lookup"><span data-stu-id="f91c7-171">toolearn more about...</span></span>

* <span data-ttu-id="f91c7-172">het maken van een machine learning-experiment met Machine Learning Studio, Zie [uw eerste experiment maken in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span><span class="sxs-lookup"><span data-stu-id="f91c7-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="f91c7-173">hoe uw machine learning-experiment als een webservice toodeploy zien [een Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="f91c7-173">how toodeploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="f91c7-174">andere manieren tooaccess uw webservice Zie [hoe tooconsume een Azure Machine Learning-webservice](machine-learning-consume-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="f91c7-174">other ways tooaccess your web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md)</span></span>

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
