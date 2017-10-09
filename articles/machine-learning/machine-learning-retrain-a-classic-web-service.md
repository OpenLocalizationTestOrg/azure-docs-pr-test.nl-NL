---
title: een klassieke webservice aaaRetrain | Microsoft Docs
description: Meer informatie over hoe tooprogrammatically opnieuw trainen model en update Hallo web service toouse Hallo nieuw model is getraind in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="16411-103">Een klassieke webservice opnieuw trainen</span><span class="sxs-lookup"><span data-stu-id="16411-103">Retrain a Classic web service</span></span>
<span data-ttu-id="16411-104">Hallo voorspellende u geïmplementeerde webservice is Hallo standaard score-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="16411-104">hello Predictive Web Service you deployed is hello default scoring endpoint.</span></span> <span data-ttu-id="16411-105">Standaardeindpunten worden gesynchroniseerd met Hallo oorspronkelijke trainings- en experimenten score berekenen en daarom hello getrainde model voor het standaardeindpunt Hallo kan niet worden vervangen.</span><span class="sxs-lookup"><span data-stu-id="16411-105">Default endpoints are kept in sync with hello original training and scoring experiments, and therefore hello trained model for hello default endpoint cannot be replaced.</span></span> <span data-ttu-id="16411-106">tooretrain hello web-service, moet u een nieuwe webservice van de endpoint-toohello toevoegen.</span><span class="sxs-lookup"><span data-stu-id="16411-106">tooretrain hello web service, you must add a new endpoint toohello web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="16411-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="16411-107">Prerequisites</span></span>
<span data-ttu-id="16411-108">U moet een trainingsexperiment en een Voorspellend experiment hebt ingesteld zoals wordt weergegeven in [Retrain Machine Learning-modellen programmatisch](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="16411-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="16411-109">Hallo Voorspellend experiment moet worden geïmplementeerd als een klassiek machine learning-webservice.</span><span class="sxs-lookup"><span data-stu-id="16411-109">hello predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="16411-110">Zie voor meer informatie over webservices implementeren [Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="16411-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="16411-111">Een nieuw eindpunt toevoegen</span><span class="sxs-lookup"><span data-stu-id="16411-111">Add a new Endpoint</span></span>
<span data-ttu-id="16411-112">Hallo voorspellende webservice die u hebt geïmplementeerd bevat een standaardexemplaar score-eindpunt dat is gesynchroniseerd met de oorspronkelijke training Hallo en scoreprofiel experimenten getrainde model.</span><span class="sxs-lookup"><span data-stu-id="16411-112">hello Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with hello original training and scoring experiments trained model.</span></span> <span data-ttu-id="16411-113">tooupdate toowith een nieuw getraind model van uw web-service moet u een nieuw score-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="16411-113">tooupdate your web service toowith a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="16411-114">een nieuw scoreprofiel eindpunt op Hallo voorspellende webservice die kan worden bijgewerkt met het getrainde model Hallo toocreate:</span><span class="sxs-lookup"><span data-stu-id="16411-114">toocreate a new scoring endpoint, on hello Predictive Web Service that can be updated with hello trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="16411-115">Zorg ervoor dat u toevoegt Hallo eindpunt toohello voorspellende webservice niet Hallo Training Web Service.</span><span class="sxs-lookup"><span data-stu-id="16411-115">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="16411-116">Als u correct zowel een trainings- en een Voorspellend webservice hebt geïmplementeerd, ziet u twee afzonderlijke webservices die worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="16411-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="16411-117">Hallo voorspellende webservice moet eindigen met '[voorspellende exp.]'.</span><span class="sxs-lookup"><span data-stu-id="16411-117">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="16411-118">Er zijn drie manieren waarop u een nieuwe webservice van de eindpunt-tooa kunt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="16411-118">There are three ways in which you can add a new end point tooa web service:</span></span>

1. <span data-ttu-id="16411-119">Programmatisch</span><span class="sxs-lookup"><span data-stu-id="16411-119">Programmatically</span></span>
2. <span data-ttu-id="16411-120">Hallo webservices voor Microsoft Azure portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="16411-120">Use hello Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="16411-121">Hallo klassieke Azure-portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="16411-121">Use hello Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="16411-122">Programmatisch een eindpunt toevoegen</span><span class="sxs-lookup"><span data-stu-id="16411-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="16411-123">U kunt scoreprofiel Hallo voorbeeldcode in dit om eindpunten toevoegen [github-opslagplaats](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="16411-123">You can add scoring endpoints using hello sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a><span data-ttu-id="16411-124">Hallo webservices voor Microsoft Azure portal tooadd een eindpunt gebruiken</span><span class="sxs-lookup"><span data-stu-id="16411-124">Use hello Microsoft Azure Web Services portal tooadd an endpoint</span></span>
1. <span data-ttu-id="16411-125">Klik op Web-Services op Hallo linkernavigatievenster kolom in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="16411-125">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="16411-126">Aan de onderkant van de Hallo van Hallo web servicedashboard, klikt u op **beheren eindpunten preview**.</span><span class="sxs-lookup"><span data-stu-id="16411-126">At hello bottom of hello web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="16411-127">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="16411-127">Click **Add**.</span></span>
4. <span data-ttu-id="16411-128">Typ een naam en beschrijving voor het nieuwe eindpunt Hallo.</span><span class="sxs-lookup"><span data-stu-id="16411-128">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="16411-129">Selecteer het logboekregistratieniveau Hallo en of voorbeeldgegevens is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="16411-129">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="16411-130">Zie voor meer informatie over logboekregistratie [logboekregistratie inschakelen voor Machine Learning-webservices](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="16411-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a><span data-ttu-id="16411-131">Gebruik hello Azure classic portal tooadd een eindpunt</span><span class="sxs-lookup"><span data-stu-id="16411-131">Use hello Azure classic portal tooadd an endpoint</span></span>
1. <span data-ttu-id="16411-132">Meld u aan toohello [klassieke Azure portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="16411-132">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="16411-133">Klik in het linkermenu hello, **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="16411-133">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="16411-134">Onder de naam, uw werkruimte op en klik op **webservices**.</span><span class="sxs-lookup"><span data-stu-id="16411-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="16411-135">Klik onder de naam, **telling Model [voorspellende exp].** .</span><span class="sxs-lookup"><span data-stu-id="16411-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="16411-136">Klik onder aan de pagina Hallo Hallo op **eindpunt toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="16411-136">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="16411-137">Zie voor meer informatie over het toevoegen van eindpunten [eindpunten maken](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="16411-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-hello-added-endpoints-trained-model"></a><span data-ttu-id="16411-138">Update Hallo Trained Model-eindpunt toegevoegd</span><span class="sxs-lookup"><span data-stu-id="16411-138">Update hello added endpoint’s Trained Model</span></span>
<span data-ttu-id="16411-139">toocomplete hello retraining proces, moet u bijwerken Hallo getrainde model van het nieuwe eindpunt Hallo die u hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="16411-139">toocomplete hello retraining process, you must update hello trained model of hello new endpoint that you added.</span></span>

* <span data-ttu-id="16411-140">Als u nieuwe Hallo-eindpunt met de klassieke Azure portal Hallo hebt toegevoegd, kunt u op de naam van de Hallo nieuw eindpunt in Hallo-portal en vervolgens Hallo **UpdateResource** tooget Hallo URL moet u tooupdate Hallo eindpunt model koppelen.</span><span class="sxs-lookup"><span data-stu-id="16411-140">If you added hello new endpoint using hello classic Azure portal, you can click hello new endpoint's name in hello portal, then hello **UpdateResource** link tooget hello URL you would need tooupdate hello endpoint's model.</span></span>
* <span data-ttu-id="16411-141">Als u met behulp van de voorbeeldcode Hallo Hallo-eindpunt toegevoegd, dit omvat de locatie van Hallo help-URL is geïdentificeerd door Hallo *HelpLocationURL* waarde in het Hallo-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="16411-141">If you added hello endpoint using hello sample code, this includes location of hello help URL identified by hello *HelpLocationURL* value in hello output.</span></span>

<span data-ttu-id="16411-142">tooretrieve hello pad URL:</span><span class="sxs-lookup"><span data-stu-id="16411-142">tooretrieve hello path URL:</span></span>

1. <span data-ttu-id="16411-143">Kopieer en plak Hallo-URL in uw browser.</span><span class="sxs-lookup"><span data-stu-id="16411-143">Copy and paste hello URL into your browser.</span></span>
2. <span data-ttu-id="16411-144">Klik op Hallo Update Resource koppeling.</span><span class="sxs-lookup"><span data-stu-id="16411-144">Click hello Update Resource link.</span></span>
3. <span data-ttu-id="16411-145">Hallo POST-URL van de PATCH-aanvraag Hallo kopiëren.</span><span class="sxs-lookup"><span data-stu-id="16411-145">Copy hello POST URL of hello PATCH request.</span></span> <span data-ttu-id="16411-146">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="16411-146">For example:</span></span>
   
     <span data-ttu-id="16411-147">URL VAN DE PATCH: HTTPS://MANAGEMENT.AZUREML.NET/WORKSPACES/00BF70534500B34REBFA1843D6/WEBSERVICES/AF3ER32AD393852F9B30AC9A35B/ENDPOINTS/NEWENDPOINT2</span><span class="sxs-lookup"><span data-stu-id="16411-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="16411-148">U kunt nu Hallo getrainde model tooupdate Hallo score-eindpunt dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="16411-148">You can now use hello trained model tooupdate hello scoring endpoint that you created previously.</span></span>

<span data-ttu-id="16411-149">Hallo volgende voorbeeldcode laat zien u hoe toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*, en URL PATCH tooupdate Hallo-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="16411-149">hello following sample code shows you how toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL tooupdate hello endpoint.</span></span>

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

<span data-ttu-id="16411-150">Hallo *apiKey* en Hallo *endpointUrl* voor Hallo aanroep kan worden verkregen van endpoint-dashboard.</span><span class="sxs-lookup"><span data-stu-id="16411-150">hello *apiKey* and hello *endpointUrl* for hello call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="16411-151">waarde van Hallo Hallo *naam* parameter in *Resources* moeten identieke Hallo resourcenaam Hallo opgeslagen getrainde Model Hallo Voorspellend experiment.</span><span class="sxs-lookup"><span data-stu-id="16411-151">hello value of hello *Name* parameter in *Resources* should match hello Resource Name of hello saved Trained Model in hello predictive experiment.</span></span> <span data-ttu-id="16411-152">tooget hello resourcenaam:</span><span class="sxs-lookup"><span data-stu-id="16411-152">tooget hello Resource Name:</span></span>

1. <span data-ttu-id="16411-153">Meld u aan toohello [klassieke Azure portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="16411-153">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="16411-154">Klik in het linkermenu hello, **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="16411-154">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="16411-155">Onder de naam, uw werkruimte op en klik op **webservices**.</span><span class="sxs-lookup"><span data-stu-id="16411-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="16411-156">Klik onder de naam, **telling Model [voorspellende exp].** .</span><span class="sxs-lookup"><span data-stu-id="16411-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="16411-157">Klik op de nieuwe eindpunt Hallo die u hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="16411-157">Click hello new endpoint you added.</span></span>
6. <span data-ttu-id="16411-158">Klik op Hallo eindpunt dashboard **Update Resource**.</span><span class="sxs-lookup"><span data-stu-id="16411-158">On hello endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="16411-159">Op Hallo Update Resource API-documentatie pagina voor de webservice Hallo vindt u Hallo **resourcenaam** onder **bij te werken bronnen**.</span><span class="sxs-lookup"><span data-stu-id="16411-159">On hello Update Resource API Documentation page for hello web service, you can find hello **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="16411-160">Als uw SAS-token is verstreken voordat u klaar bent met het eindpunt van de Hallo bijwerken, moet u een GET met Hallo taak-Id tooobtain-token van een nieuwe uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="16411-160">If your SAS token expires before you finish updating hello endpoint, you must perform a GET with hello Job Id tooobtain a fresh token.</span></span>

<span data-ttu-id="16411-161">Wanneer Hallo code met succes is uitgevoerd, nieuw Hallo-eindpunt moet zich eerst Hallo retrained objectmodel gebruiken in ongeveer 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="16411-161">When hello code has successfully run, hello new endpoint should start using hello retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="16411-162">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="16411-162">Summary</span></span>
<span data-ttu-id="16411-163">Met behulp van Hallo Retraining API's, kunt u Hallo getraind model van een Voorspellend webservice scenario's zoals inschakelen bijwerken:</span><span class="sxs-lookup"><span data-stu-id="16411-163">Using hello Retraining APIs, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="16411-164">Periodieke model retraining met nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="16411-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="16411-165">Distributie van een model toocustomers met Hallo doel van zodat ze opnieuw trainen Hallo-model met hun eigen gegevens.</span><span class="sxs-lookup"><span data-stu-id="16411-165">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16411-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="16411-166">Next steps</span></span>
[<span data-ttu-id="16411-167">Het oplossen van problemen Hallo retraining van een klassieke Azure Machine Learning-webservice</span><span class="sxs-lookup"><span data-stu-id="16411-167">Troubleshooting hello retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

