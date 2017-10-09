---
title: AAA(deprecated) publiceren machine learning web service tooAzure Marketplace | Microsoft Docs
description: (afgeschaft) Hoe toopublish uw Azure Machine Learning-webservice toohello Azure Marketplace
services: machine-learning
documentationcenter: 
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: machine-learning-gallery-experiments
redirect_document_id: True
ms.openlocfilehash: 149abc3df9b79c1b37d233d5e85e803592ff1020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a><span data-ttu-id="1afb2-103">(afgeschaft) Azure Machine Learning-webservice toohello Azure Marketplace publiceren</span><span class="sxs-lookup"><span data-stu-id="1afb2-103">(deprecated) Publish Azure Machine Learning Web Service toohello Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="1afb2-104">DataMarket en Data Services worden gesteld en bestaande abonnementen wordt buiten gebruik worden gesteld en geannuleerd vanaf 3/31/2017.</span><span class="sxs-lookup"><span data-stu-id="1afb2-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="1afb2-105">Als gevolg hiervan wordt in dit artikel afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="1afb2-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="1afb2-106">Als alternatief kunt u uw Machine Learning-experimenten toohello kunt publiceren [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) voor Hallo voordeel van het Hallo gegevens wetenschappelijke community.</span><span class="sxs-lookup"><span data-stu-id="1afb2-106">As an alternative, you can publish your Machine Learning experiments toohello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for hello benefit of hello data science community.</span></span> <span data-ttu-id="1afb2-107">Zie voor meer informatie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="1afb2-107">For more information, see [Share and discover resources in hello Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="1afb2-108">Hello Azure Marketplace biedt de mogelijkheid Hallo betaald toopublish Azure Machine Learning-webservices of gratis services voor verbruik door externe klanten.</span><span class="sxs-lookup"><span data-stu-id="1afb2-108">hello Azure Marketplace provides hello ability toopublish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="1afb2-109">Dit artikel bevat een overzicht van het proces met koppelingen tooguidelines tooget die u gestart.</span><span class="sxs-lookup"><span data-stu-id="1afb2-109">This article provides an overview of that process with links tooguidelines tooget you started.</span></span> <span data-ttu-id="1afb2-110">Met behulp van dit proces kunt u uw webservices beschikbaar voor andere ontwikkelaars tooconsume in hun toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1afb2-110">By using this process, you can make your web services available for other developers tooconsume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a><span data-ttu-id="1afb2-111">Overzicht van Hallo publicatieproces</span><span class="sxs-lookup"><span data-stu-id="1afb2-111">Overview of hello publishing process</span></span>
<span data-ttu-id="1afb2-112">Hallo volgen Hallo stappen voor het publiceren van een Azure Machine Learning web service tooAzure Marketplace:</span><span class="sxs-lookup"><span data-stu-id="1afb2-112">hello following are hello steps for publishing an Azure Machine Learning web service tooAzure Marketplace:</span></span>

1. <span data-ttu-id="1afb2-113">Maken en publiceren van een Machine Learning-reactie op aanvragen-service (RR's)</span><span class="sxs-lookup"><span data-stu-id="1afb2-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="1afb2-114">Hallo service tooproduction implementeren en Hallo API-sleutel en OData-eindpuntinformatie verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="1afb2-114">Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="1afb2-115">Gebruik Hallo URL Hallo gepubliceerde web service toopublish te[Azure Marketplace (markt gegevens)](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="1afb2-115">Use hello URL of hello published web service toopublish too[Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="1afb2-116">Zodra ingediend, uw aanbieding wordt gecontroleerd en toobe goedgekeurd voordat uw klanten kunt met het aanschaffen beginnen moet.</span><span class="sxs-lookup"><span data-stu-id="1afb2-116">Once submitted, your offer is reviewed and needs toobe approved before your customers can start purchasing it.</span></span> <span data-ttu-id="1afb2-117">Hallo-publicatieproces kan enkele dagen duren.</span><span class="sxs-lookup"><span data-stu-id="1afb2-117">hello publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="1afb2-118">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1afb2-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="1afb2-119">Stap 1: Maken en publiceren van een Machine Learning-reactie op aanvragen-service (RR's)</span><span class="sxs-lookup"><span data-stu-id="1afb2-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="1afb2-120">Als u nog niet hebt gedaan dit, bekijk dan deze [doorlopen](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="1afb2-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a><span data-ttu-id="1afb2-121">Stap 2: Hallo service tooproduction implementeren en Hallo API-sleutel en OData-eindpuntinformatie verkrijgen</span><span class="sxs-lookup"><span data-stu-id="1afb2-121">Step 2: Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information</span></span>
1. <span data-ttu-id="1afb2-122">Van Hallo [klassieke Azure-Portal](http://manage.windowsazure.com), selecteer Hallo **MACHINE LEARNING** optie van de linkernavigatiebalk Hallo en selecteer uw werkruimte.</span><span class="sxs-lookup"><span data-stu-id="1afb2-122">From hello [Azure Classic Portal](http://manage.windowsazure.com), select hello **MACHINE LEARNING** option from hello left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="1afb2-123">Klik op Hallo **WEBSERVICES** tabblad en selecteer Hallo webservice gewenst toopublish toohello marketplace.</span><span class="sxs-lookup"><span data-stu-id="1afb2-123">Click on hello **WEB SERVICES** tab, and select hello web service you would like toopublish toohello marketplace.</span></span>
   
    ![Azure Marketplace][workspace]
3. <span data-ttu-id="1afb2-125">Selecteer Hallo eindpunt die u zou zoals toohave Hallo marketplace verbruiken.</span><span class="sxs-lookup"><span data-stu-id="1afb2-125">Select hello endpoint you would like toohave hello marketplace consume.</span></span> <span data-ttu-id="1afb2-126">Als u geen extra eindpunten niet hebt gemaakt, kunt u Hallo **standaard** eindpunt.</span><span class="sxs-lookup"><span data-stu-id="1afb2-126">If you have not created any additional endpoints, you can select hello **Default** endpoint.</span></span>
4. <span data-ttu-id="1afb2-127">Zodra u hebt geklikt op Hallo eindpunt, kunt u zich kunt toosee hello **API-sleutel**.</span><span class="sxs-lookup"><span data-stu-id="1afb2-127">Once you have clicked on hello endpoint, you will be able toosee hello **API KEY**.</span></span> <span data-ttu-id="1afb2-128">U moet dit stuk informatie later in stap 3, dus maak een kopie van deze.</span><span class="sxs-lookup"><span data-stu-id="1afb2-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure Marketplace][apikey]
5. <span data-ttu-id="1afb2-130">Klik op Hallo **aanvragen/reacties** methode op dit punt wordt niet ondersteund publishing Batchuitvoering services toohello marketplace.</span><span class="sxs-lookup"><span data-stu-id="1afb2-130">Click on hello **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services toohello marketplace.</span></span> <span data-ttu-id="1afb2-131">Die u gaat toohello API help-pagina voor Hallo aanvraag/antwoord-methode.</span><span class="sxs-lookup"><span data-stu-id="1afb2-131">That will take you toohello API help page for hello Request/Response method.</span></span>
6. <span data-ttu-id="1afb2-132">Kopiëren Hallo **adres van de OData-eindpunt**, moet u deze informatie later in stap 3.</span><span class="sxs-lookup"><span data-stu-id="1afb2-132">Copy hello **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure Marketplace][odata]

<span data-ttu-id="1afb2-134">Hallo service implementeren in productie.</span><span class="sxs-lookup"><span data-stu-id="1afb2-134">deploy hello service into production.</span></span>

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a><span data-ttu-id="1afb2-135">Stap 3: Gebruik Hallo URL Hallo gepubliceerde web service toopublish tooAzure Marketplace (DataMarket)</span><span class="sxs-lookup"><span data-stu-id="1afb2-135">Step 3: Use hello URL of hello published web service toopublish tooAzure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="1afb2-136">Navigeer te[Azure Marketplace (markt gegevens)](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="1afb2-136">Navigate too[Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="1afb2-137">Klik op Hallo **publiceren** koppeling bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="1afb2-137">Click on hello **Publish** link at hello top of hello page.</span></span> <span data-ttu-id="1afb2-138">Hiermee gaat u toohello [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="1afb2-138">This will take you toohello [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="1afb2-139">Klik op Hallo **uitgevers** sectie tooregister als een publisher.</span><span class="sxs-lookup"><span data-stu-id="1afb2-139">Click on hello **publishers** section tooregister as a publisher.</span></span>
4. <span data-ttu-id="1afb2-140">Wanneer u een nieuwe aanbieding maakt, selecteert u **Data Services**, klikt u vervolgens op **maken van een nieuwe gegevensservice**.</span><span class="sxs-lookup"><span data-stu-id="1afb2-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure Marketplace][image1]
   
   <br />
5. <span data-ttu-id="1afb2-142">Onder **plannen** bieden informatie over uw oplossing, inclusief een prijsstelling.</span><span class="sxs-lookup"><span data-stu-id="1afb2-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="1afb2-143">Bepaal als u een gratis of betaalde service biedt.</span><span class="sxs-lookup"><span data-stu-id="1afb2-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="1afb2-144">tooget betaald, bieden betalingsinformatie zoals uw bank en de btw-gegevens.</span><span class="sxs-lookup"><span data-stu-id="1afb2-144">tooget paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="1afb2-145">Onder **Marketing** bevatten informatie over uw aanbieding, zoals Hallo titel en beschrijving voor uw aanbieding.</span><span class="sxs-lookup"><span data-stu-id="1afb2-145">Under **Marketing** provide information about your offer, such as hello title and description for your offer.</span></span>
7. <span data-ttu-id="1afb2-146">Onder **prijzen** Hallo prijs ingesteld voor uw plannen voor specifieke landen of laat Hallo systeem 'autoprice' uw aanbieding.</span><span class="sxs-lookup"><span data-stu-id="1afb2-146">Under **Pricing** you can set hello price for your plans for specific countries, or let hello system "autoprice" your offer.</span></span>
8. <span data-ttu-id="1afb2-147">Op Hallo **gegevensservice** tabblad **webservice** als Hallo **gegevensbron**.</span><span class="sxs-lookup"><span data-stu-id="1afb2-147">On hello **Data Service** tab, click **Web Service** as hello **Data Source**.</span></span>
   
    ![Azure Marketplace][image2]
9. <span data-ttu-id="1afb2-149">Hallo web service-URL en API-sleutel ophalen van Hallo klassieke Azure-Portal, zoals beschreven in stap 2 hierboven.</span><span class="sxs-lookup"><span data-stu-id="1afb2-149">Get hello web service URL and API key from hello Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="1afb2-150">Hallo Marketplace Data Service-instelling in het dialoogvenster Plakken Hallo OData-eindpuntadres Hallo **Service-URL** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="1afb2-150">In hello Marketplace Data Service setup dialog box, paste hello OData endpoint address into hello **Service URL** text box.</span></span>
11. <span data-ttu-id="1afb2-151">Voor **verificatie**, kies **Header** als Hallo **verificatieschema**.</span><span class="sxs-lookup"><span data-stu-id="1afb2-151">For **Authentication**, choose **Header** as hello **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="1afb2-152">Voer 'Verificatie' voor Hallo **headernaam**.</span><span class="sxs-lookup"><span data-stu-id="1afb2-152">Enter "Authorization" for hello **Header Name**.</span></span>
    * <span data-ttu-id="1afb2-153">Voor Hallo **headerwaarde**, Voer u 'Bearer' (zonder aanhalingstekens Hallo), klik op Hallo **ruimte** balk en plak Hallo API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="1afb2-153">For hello **Header Value**, enter "Bearer" (without hello quotation marks), click hello **Space** bar, and then paste hello API key.</span></span>
    * <span data-ttu-id="1afb2-154">Selecteer Hallo **deze Service is OData** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="1afb2-154">Select hello **This Service is OData** check box.</span></span>
    * <span data-ttu-id="1afb2-155">Klik op **testverbinding** tootest Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="1afb2-155">Click **Test Connection** tootest hello connection.</span></span>
12. <span data-ttu-id="1afb2-156">Onder **categorieën**, zorg ervoor dat **Machine Learning** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="1afb2-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="1afb2-157">Wanneer u klaar bent, voeren alle Hallo metagegevens over uw aanbieding, klikt u op **publiceren**, en vervolgens **tooStaging Push**.</span><span class="sxs-lookup"><span data-stu-id="1afb2-157">When you are done entering all hello metadata about your offer, click on **Publish**, and then **Push tooStaging**.</span></span> <span data-ttu-id="1afb2-158">Op dit moment wordt u gewaarschuwd voor overige problemen moet u toofix.</span><span class="sxs-lookup"><span data-stu-id="1afb2-158">At this point, you will be notified of any remaining issues that you need toofix.</span></span>
14. <span data-ttu-id="1afb2-159">Nadat u ervoor gezorgd alle Hallo openstaande problemen is voltooid dat hebt, klikt u op **aanvragen van goedkeuring toopush tooProduction**.</span><span class="sxs-lookup"><span data-stu-id="1afb2-159">After you have ensured completion of all hello outstanding issues, click on **Request approval toopush tooProduction**.</span></span> <span data-ttu-id="1afb2-160">Hallo-publicatieproces kan enkele dagen duren.</span><span class="sxs-lookup"><span data-stu-id="1afb2-160">hello publishing process can take a few business days.</span></span> 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

