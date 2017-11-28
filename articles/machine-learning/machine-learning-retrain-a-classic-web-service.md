---
title: Een klassieke webservice Retrain | Microsoft Docs
description: Informatie over het programmatisch opnieuw trainen van een model en het bijwerken van de webservice voor het gebruik van het zojuist getrainde model in Azure Machine Learning.
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
ms.openlocfilehash: 3f9f4cd5ed36262845f7a3139073ccd4e49f472a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="317d7-103">Een klassieke webservice opnieuw trainen</span><span class="sxs-lookup"><span data-stu-id="317d7-103">Retrain a Classic web service</span></span>
<span data-ttu-id="317d7-104">De voorspellende webservice die u hebt geïmplementeerd is de standaardinstelling score-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="317d7-104">The Predictive Web Service you deployed is the default scoring endpoint.</span></span> <span data-ttu-id="317d7-105">Standaardeindpunten worden gesynchroniseerd met de oorspronkelijke training en experimenten score berekenen en daarom het getrainde model voor het standaardeindpunt kan niet worden vervangen.</span><span class="sxs-lookup"><span data-stu-id="317d7-105">Default endpoints are kept in sync with the original training and scoring experiments, and therefore the trained model for the default endpoint cannot be replaced.</span></span> <span data-ttu-id="317d7-106">Als u wilt opnieuw trainen van de webservice, moet u een nieuw eindpunt toevoegen aan de webservice.</span><span class="sxs-lookup"><span data-stu-id="317d7-106">To retrain the web service, you must add a new endpoint to the web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="317d7-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="317d7-107">Prerequisites</span></span>
<span data-ttu-id="317d7-108">U moet een trainingsexperiment en een Voorspellend experiment hebt ingesteld zoals wordt weergegeven in [Retrain Machine Learning-modellen programmatisch](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="317d7-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="317d7-109">De Voorspellend experiment moet worden geïmplementeerd als een klassiek machine learning-webservice.</span><span class="sxs-lookup"><span data-stu-id="317d7-109">The predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="317d7-110">Zie voor meer informatie over webservices implementeren [Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="317d7-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="317d7-111">Een nieuw eindpunt toevoegen</span><span class="sxs-lookup"><span data-stu-id="317d7-111">Add a new Endpoint</span></span>
<span data-ttu-id="317d7-112">De voorspellende webservice die u hebt geïmplementeerd, bevat een standaardexemplaar score-eindpunt dat is gesynchroniseerd met de oorspronkelijke training en experimenten getrainde model score berekenen.</span><span class="sxs-lookup"><span data-stu-id="317d7-112">The Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with the original training and scoring experiments trained model.</span></span> <span data-ttu-id="317d7-113">Als u wilt uw webservice bijwerken met een nieuwe getraind model, moet u een nieuw score-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="317d7-113">To update your web service to with a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="317d7-114">Een nieuw score-eindpunt op de voorspellende webservice die kan worden bijgewerkt met het getrainde model maken:</span><span class="sxs-lookup"><span data-stu-id="317d7-114">To create a new scoring endpoint, on the Predictive Web Service that can be updated with the trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="317d7-115">Zorg ervoor dat u het eindpunt wilt toevoegen aan de voorspellende Web Service, niet de trainings-webservice.</span><span class="sxs-lookup"><span data-stu-id="317d7-115">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="317d7-116">Als u correct zowel een trainings- en een Voorspellend webservice hebt geïmplementeerd, ziet u twee afzonderlijke webservices die worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="317d7-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="317d7-117">De voorspellende webservice moet eindigen met '[voorspellende exp.]'.</span><span class="sxs-lookup"><span data-stu-id="317d7-117">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="317d7-118">Er zijn drie manieren waarin u een nieuw eindpunt met een webservice kunt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="317d7-118">There are three ways in which you can add a new end point to a web service:</span></span>

1. <span data-ttu-id="317d7-119">Programmatisch</span><span class="sxs-lookup"><span data-stu-id="317d7-119">Programmatically</span></span>
2. <span data-ttu-id="317d7-120">Gebruik de Microsoft Azure Web Services-portal</span><span class="sxs-lookup"><span data-stu-id="317d7-120">Use the Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="317d7-121">Gebruik de klassieke Azure portal</span><span class="sxs-lookup"><span data-stu-id="317d7-121">Use the Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="317d7-122">Programmatisch een eindpunt toevoegen</span><span class="sxs-lookup"><span data-stu-id="317d7-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="317d7-123">U kunt toevoegen scoreprofiel eindpunten voor de voorbeeldcode in dit [github-opslagplaats](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="317d7-123">You can add scoring endpoints using the sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-the-microsoft-azure-web-services-portal-to-add-an-endpoint"></a><span data-ttu-id="317d7-124">De Microsoft Azure Web Services-portal gebruiken voor een eindpunt toevoegen</span><span class="sxs-lookup"><span data-stu-id="317d7-124">Use the Microsoft Azure Web Services portal to add an endpoint</span></span>
1. <span data-ttu-id="317d7-125">Klik op webservices op de linkernavigatiebalk-kolom in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="317d7-125">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="317d7-126">Klik aan de onderkant van het dashboard van web service **beheren eindpunten preview**.</span><span class="sxs-lookup"><span data-stu-id="317d7-126">At the bottom of the web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="317d7-127">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="317d7-127">Click **Add**.</span></span>
4. <span data-ttu-id="317d7-128">Typ een naam en beschrijving voor het nieuwe eindpunt.</span><span class="sxs-lookup"><span data-stu-id="317d7-128">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="317d7-129">Selecteer het niveau van logboekregistratie en of de voorbeeldgegevens is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="317d7-129">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="317d7-130">Zie voor meer informatie over logboekregistratie [logboekregistratie inschakelen voor Machine Learning-webservices](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="317d7-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-the-azure-classic-portal-to-add-an-endpoint"></a><span data-ttu-id="317d7-131">Gebruik de klassieke Azure portal een eindpunt toevoegen</span><span class="sxs-lookup"><span data-stu-id="317d7-131">Use the Azure classic portal to add an endpoint</span></span>
1. <span data-ttu-id="317d7-132">Aanmelden bij de [klassieke Azure portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="317d7-132">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="317d7-133">Klik in het menu links op **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="317d7-133">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="317d7-134">Onder de naam, uw werkruimte op en klik op **webservices**.</span><span class="sxs-lookup"><span data-stu-id="317d7-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="317d7-135">Klik onder de naam, **telling Model [voorspellende exp].** .</span><span class="sxs-lookup"><span data-stu-id="317d7-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="317d7-136">Klik onder aan de pagina op **eindpunt toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="317d7-136">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="317d7-137">Zie voor meer informatie over het toevoegen van eindpunten [eindpunten maken](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="317d7-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-the-added-endpoints-trained-model"></a><span data-ttu-id="317d7-138">Het toegevoegde eindpunt getraind Model bijwerken</span><span class="sxs-lookup"><span data-stu-id="317d7-138">Update the added endpoint’s Trained Model</span></span>
<span data-ttu-id="317d7-139">De retraining om proces te voltooien, moet u het getrainde model van het nieuwe eindpunt dat u hebt toegevoegd bijwerken.</span><span class="sxs-lookup"><span data-stu-id="317d7-139">To complete the retraining process, you must update the trained model of the new endpoint that you added.</span></span>

* <span data-ttu-id="317d7-140">Als u het nieuwe eindpunt met de klassieke Azure portal hebt toegevoegd, kunt u de naam van het nieuwe eindpunt in de portal, de **UpdateResource** koppeling voor de URL die u moet van het eindpunt model bijwerken.</span><span class="sxs-lookup"><span data-stu-id="317d7-140">If you added the new endpoint using the classic Azure portal, you can click the new endpoint's name in the portal, then the **UpdateResource** link to get the URL you would need to update the endpoint's model.</span></span>
* <span data-ttu-id="317d7-141">Als u het eindpunt met de voorbeeldcode hebt toegevoegd, dit omvat de locatie van de help-URL die is geïdentificeerd door de *HelpLocationURL* waarde in de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="317d7-141">If you added the endpoint using the sample code, this includes location of the help URL identified by the *HelpLocationURL* value in the output.</span></span>

<span data-ttu-id="317d7-142">Voor het ophalen van de pad-URL:</span><span class="sxs-lookup"><span data-stu-id="317d7-142">To retrieve the path URL:</span></span>

1. <span data-ttu-id="317d7-143">Kopieer en plak de URL in uw browser.</span><span class="sxs-lookup"><span data-stu-id="317d7-143">Copy and paste the URL into your browser.</span></span>
2. <span data-ttu-id="317d7-144">Klik op de koppeling van de Update-Resource.</span><span class="sxs-lookup"><span data-stu-id="317d7-144">Click the Update Resource link.</span></span>
3. <span data-ttu-id="317d7-145">Kopieer de POST-URL van de PATCH-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="317d7-145">Copy the POST URL of the PATCH request.</span></span> <span data-ttu-id="317d7-146">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="317d7-146">For example:</span></span>
   
     <span data-ttu-id="317d7-147">URL VAN DE PATCH: HTTPS://MANAGEMENT.AZUREML.NET/WORKSPACES/00BF70534500B34REBFA1843D6/WEBSERVICES/AF3ER32AD393852F9B30AC9A35B/ENDPOINTS/NEWENDPOINT2</span><span class="sxs-lookup"><span data-stu-id="317d7-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="317d7-148">U kunt nu het getrainde model gebruiken om bij te werken het score-eindpunt dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="317d7-148">You can now use the trained model to update the scoring endpoint that you created previously.</span></span>

<span data-ttu-id="317d7-149">De volgende voorbeeldcode laat zien u hoe u de *BaseLocation*, *RelativeLocation*, *SasBlobToken*, en PATCH URL naar het eindpunt worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="317d7-149">The following sample code shows you how to use the *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL to update the endpoint.</span></span>

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
                        RelativeLocation = "your endpoint relative location", //from the output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from the output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
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

<span data-ttu-id="317d7-150">De *apiKey* en de *endpointUrl* voor de aanroep kan worden verkregen van endpoint-dashboard.</span><span class="sxs-lookup"><span data-stu-id="317d7-150">The *apiKey* and the *endpointUrl* for the call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="317d7-151">De waarde van de *naam* parameter in *Resources* moet overeenkomen met de naam van de Resource van het opgeslagen getraind Model in de Voorspellend experiment.</span><span class="sxs-lookup"><span data-stu-id="317d7-151">The value of the *Name* parameter in *Resources* should match the Resource Name of the saved Trained Model in the predictive experiment.</span></span> <span data-ttu-id="317d7-152">De resourcenaam ophalen:</span><span class="sxs-lookup"><span data-stu-id="317d7-152">To get the Resource Name:</span></span>

1. <span data-ttu-id="317d7-153">Aanmelden bij de [klassieke Azure portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="317d7-153">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="317d7-154">Klik in het menu links op **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="317d7-154">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="317d7-155">Onder de naam, uw werkruimte op en klik op **webservices**.</span><span class="sxs-lookup"><span data-stu-id="317d7-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="317d7-156">Klik onder de naam, **telling Model [voorspellende exp].** .</span><span class="sxs-lookup"><span data-stu-id="317d7-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="317d7-157">Klik op het nieuwe eindpunt dat u hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="317d7-157">Click the new endpoint you added.</span></span>
6. <span data-ttu-id="317d7-158">Klik op het dashboard endpoint **Update Resource**.</span><span class="sxs-lookup"><span data-stu-id="317d7-158">On the endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="317d7-159">U kunt vinden op de pagina Update Resource API-documentatie voor de webservice de **resourcenaam** onder **bij te werken bronnen**.</span><span class="sxs-lookup"><span data-stu-id="317d7-159">On the Update Resource API Documentation page for the web service, you can find the **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="317d7-160">Als uw SAS-token is verstreken voordat u klaar bent met het bijwerken van het eindpunt, moet u een GET met de taak-Id verkrijgen van een nieuw token uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="317d7-160">If your SAS token expires before you finish updating the endpoint, you must perform a GET with the Job Id to obtain a fresh token.</span></span>

<span data-ttu-id="317d7-161">Wanneer de code met succes is uitgevoerd, kan het nieuwe eindpunt moet beginnen met het retrained model in ongeveer 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="317d7-161">When the code has successfully run, the new endpoint should start using the retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="317d7-162">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="317d7-162">Summary</span></span>
<span data-ttu-id="317d7-163">De Retraining API's kunt u het getrainde model van een Voorspellend webservice inschakelen van scenario's zoals bijwerken:</span><span class="sxs-lookup"><span data-stu-id="317d7-163">Using the Retraining APIs, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="317d7-164">Periodieke model retraining met nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="317d7-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="317d7-165">Distributie van een model voor klanten met het doel van zodat ze opnieuw trainen van het model met hun eigen gegevens.</span><span class="sxs-lookup"><span data-stu-id="317d7-165">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="317d7-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="317d7-166">Next steps</span></span>
[<span data-ttu-id="317d7-167">Het oplossen van de retraining van een klassieke Azure Machine Learning-webservice</span><span class="sxs-lookup"><span data-stu-id="317d7-167">Troubleshooting the retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

