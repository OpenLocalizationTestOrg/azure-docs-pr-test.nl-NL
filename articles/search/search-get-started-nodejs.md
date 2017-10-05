---
title: Aan de slag met Azure Search in Node.js | Microsoft Docs
description: Stappen voor het bouwen van een zoektoepassing op een door Azure gehoste service voor zoeken in de cloud, waarbij gebruik wordt gemaakt van de programmeertaal Node.js.
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: 32865ed986f5eea961ef2c3813dcc6531498c90a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="b35a7-103">Aan de slag met Azure Search in Node.js</span><span class="sxs-lookup"><span data-stu-id="b35a7-103">Get started with Azure Search in Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b35a7-104">Portal</span><span class="sxs-lookup"><span data-stu-id="b35a7-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="b35a7-105">.NET</span><span class="sxs-lookup"><span data-stu-id="b35a7-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="b35a7-106">Informatie over het bouwen van een aangepaste Node.js-zoektoepassing die voor de zoekfunctie gebruikmaakt van Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b35a7-106">Learn how to build a custom Node.js search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="b35a7-107">In deze zelfstudie wordt de [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) gebruikt om de objecten en bewerkingen in deze oefening te bouwen.</span><span class="sxs-lookup"><span data-stu-id="b35a7-107">This tutorial uses the [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) to construct the objects and operations used in this exercise.</span></span>

<span data-ttu-id="b35a7-108">We hebben [Node.js](https://Nodejs.org), NPM, [Sublime Text 3](http://www.sublimetext.com/3) en Windows PowerShell op Windows 8.1 gebruikt om deze code te ontwikkelen en te testen.</span><span class="sxs-lookup"><span data-stu-id="b35a7-108">We used [Node.js](https://Nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 to develop and test this code.</span></span>

<span data-ttu-id="b35a7-109">Als u dit voorbeeld wilt uitvoeren, moet u over de Azure Search-service beschikken. U kunt zich hiervoor aanmelden in [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b35a7-109">To run this sample, you must have an Azure Search service, which you can sign up for in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b35a7-110">Zie [Een Azure Search-service in de portal maken](search-create-service-portal.md) voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="b35a7-110">See [Create an Azure Search service in the portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-the-data"></a><span data-ttu-id="b35a7-111">Over de gegevens</span><span class="sxs-lookup"><span data-stu-id="b35a7-111">About the data</span></span>
<span data-ttu-id="b35a7-112">In deze voorbeeldtoepassing wordt gebruikgemaakt van gegevens van [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), gefilterd op de staat Rhode Island om de grootte van de gegevensset te reduceren.</span><span class="sxs-lookup"><span data-stu-id="b35a7-112">This sample application uses data from the [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on the state of Rhode Island to reduce the dataset size.</span></span> <span data-ttu-id="b35a7-113">We gebruiken deze gegevens om een zoektoepassing te bouwen die kenmerkende gebouwen, zoals ziekenhuizen of scholen, gebouwen zoals ziekenhuizen en scholen, maar ook geologische kenmerken, zoals stromen, meren en toppen, retourneert.</span><span class="sxs-lookup"><span data-stu-id="b35a7-113">We'll use this data to build a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="b35a7-114">In deze toepassing zorgt het programma **DataIndexer** er met een [indexeerfunctie](https://msdn.microsoft.com/library/azure/dn798918.aspx) voor dat de index wordt gebouwd en geladen en dat de gefilterde USGS-gegevensset uit een openbare Azure SQL-database wordt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="b35a7-114">In this application, the **DataIndexer** program builds and loads the index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving the filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="b35a7-115">De programmacode bevat de referenties en gegevens voor verbinding met de onlinegegevensbron.</span><span class="sxs-lookup"><span data-stu-id="b35a7-115">Credentials and connection information to the online data source is provided in the program code.</span></span> <span data-ttu-id="b35a7-116">U hoeft verder niets te configureren.</span><span class="sxs-lookup"><span data-stu-id="b35a7-116">No further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="b35a7-117">Er is een filter op de gegevensset toegepast om onder de limiet van 10.000 documenten voor de gratis prijscategorie te blijven.</span><span class="sxs-lookup"><span data-stu-id="b35a7-117">We applied a filter on this dataset to stay under the 10,000 document limit of the free pricing tier.</span></span> <span data-ttu-id="b35a7-118">Als u de standaardcategorie gebruikt, is deze limiet niet van toepassing.</span><span class="sxs-lookup"><span data-stu-id="b35a7-118">If you use the standard tier, this limit does not apply.</span></span> <span data-ttu-id="b35a7-119">Zie [Limieten voor de Search-service](search-limits-quotas-capacity.md) voor meer informatie over de capaciteit voor elke prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="b35a7-119">For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).</span></span>
> 
> 

<a id="sub-2"></a>

## <a name="find-the-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="b35a7-120">De servicenaam en API-sleutel van uw Azure Search-service zoeken</span><span class="sxs-lookup"><span data-stu-id="b35a7-120">Find the service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="b35a7-121">Zodra u de service hebt gemaakt, keert u terug naar de portal om de URL of `api-key` op te halen.</span><span class="sxs-lookup"><span data-stu-id="b35a7-121">After you create the service, return to the portal to get the URL or `api-key`.</span></span> <span data-ttu-id="b35a7-122">Verbindingen met uw Search-service vereisen dat u zowel over de URL als een `api-key` beschikt om de aanroep te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="b35a7-122">Connections to your Search service require that you have both the URL and an `api-key` to authenticate the call.</span></span>

1. <span data-ttu-id="b35a7-123">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b35a7-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b35a7-124">Klik in de snelbalk op de **Search-service** om alle Azure Search-services weer te geven die zijn ingericht voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="b35a7-124">In the jump bar, click **Search service** to list all Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="b35a7-125">Selecteer de service die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b35a7-125">Select the service you want to use.</span></span>
4. <span data-ttu-id="b35a7-126">Op het servicedashboard worden als het goed is tegels weergegeven voor essentiële informatie, zoals het sleutelpictogram voor toegang tot de beheersleutels.</span><span class="sxs-lookup"><span data-stu-id="b35a7-126">On the service dashboard, you should see tiles for essential information, such as the key icon for accessing the admin keys.</span></span>
5. <span data-ttu-id="b35a7-127">Kopieer de service-URL, een beheersleutel en een querysleutel.</span><span class="sxs-lookup"><span data-stu-id="b35a7-127">Copy the service URL, an admin key, and a query key.</span></span> <span data-ttu-id="b35a7-128">Deze voegt u in een later stadium toe aan het bestand config.js.</span><span class="sxs-lookup"><span data-stu-id="b35a7-128">You need all three later when you add them to the config.js file.</span></span>

## <a name="download-the-sample-files"></a><span data-ttu-id="b35a7-129">De voorbeeldbestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="b35a7-129">Download the sample files</span></span>
<span data-ttu-id="b35a7-130">Gebruik een van de volgende methoden om het voorbeeld te downloaden.</span><span class="sxs-lookup"><span data-stu-id="b35a7-130">Use either one of the following approaches to download the sample.</span></span>

1. <span data-ttu-id="b35a7-131">Ga naar [AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span><span class="sxs-lookup"><span data-stu-id="b35a7-131">Go to [AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span></span>
2. <span data-ttu-id="b35a7-132">Klik op **Download ZIP** (ZIP downloaden), sla het zip-bestand op en pak vervolgens alle bestanden in het zip-bestand uit.</span><span class="sxs-lookup"><span data-stu-id="b35a7-132">Click **Download ZIP**, save the .zip file, and then extract all the files it contains.</span></span>

<span data-ttu-id="b35a7-133">Alle volgende bestandswijzigingen en uitvoerinstructies worden uitgevoerd voor de bestanden in deze map.</span><span class="sxs-lookup"><span data-stu-id="b35a7-133">All subsequent file modifications and run statements are made against files in this folder.</span></span>

## <a name="update-the-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="b35a7-134">Werk het bestand config.js bij</span><span class="sxs-lookup"><span data-stu-id="b35a7-134">Update the config.js.</span></span> <span data-ttu-id="b35a7-135">met de URL van de Search-service en uw API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="b35a7-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="b35a7-136">Gebruik de URL en API-sleutel die u eerder hebt gekopieerd om de URL, beheersleutel en querysleutel in het configuratiebestand op te geven.</span><span class="sxs-lookup"><span data-stu-id="b35a7-136">Using the URL and api-key that you copied earlier, specify the URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="b35a7-137">Beheersleutels bieden u de volledige controle over de servicebewerkingen, inclusief het maken of verwijderen van een index en het laden van documenten.</span><span class="sxs-lookup"><span data-stu-id="b35a7-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="b35a7-138">Querysleutels kunnen daarentegen alleen leesbewerkingen uitvoeren en worden doorgaans gebruikt door clienttoepassingen die verbinding maken met Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b35a7-138">In contrast, query keys are for read-only operations, typically used by client applications that connect to Azure Search.</span></span>

<span data-ttu-id="b35a7-139">In dit voorbeeld nemen we de querysleutel op om de aanbevolen procedure voor het gebruik van de querysleutel in clienttoepassingen nog maar eens onder de aandacht te brengen.</span><span class="sxs-lookup"><span data-stu-id="b35a7-139">In this sample, we include the query key to help reinforce the best practice of using the query key in client applications.</span></span>

<span data-ttu-id="b35a7-140">De volgende afbeelding is een schermopname van het bestand **config.js**. Het bestand is geopend in een teksteditor en de relevante items zijn gemarkeerd, zodat u kunt zien waar het bestand moet worden bijgewerkt met geldige waarden voor uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="b35a7-140">The following screenshot shows **config.js** open in a text editor, with the relevant entries demarcated so that you can see where to update the file with the values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-the-sample"></a><span data-ttu-id="b35a7-141">Een runtime-omgeving voor het voorbeeld hosten</span><span class="sxs-lookup"><span data-stu-id="b35a7-141">Host a runtime environment for the sample</span></span>
<span data-ttu-id="b35a7-142">Voor dit voorbeeld hebt u een HTTP-server nodig. Deze kunt u globaal installeren met npm.</span><span class="sxs-lookup"><span data-stu-id="b35a7-142">The sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="b35a7-143">Gebruik voor de volgende opdrachten een PowerShell-venster.</span><span class="sxs-lookup"><span data-stu-id="b35a7-143">Use a PowerShell window for the following commands.</span></span>

1. <span data-ttu-id="b35a7-144">Navigeer naar de map met het bestand **package.json**.</span><span class="sxs-lookup"><span data-stu-id="b35a7-144">Navigate to the folder that contains the **package.json** file.</span></span>
2. <span data-ttu-id="b35a7-145">Typ `npm install`.</span><span class="sxs-lookup"><span data-stu-id="b35a7-145">Type `npm install`.</span></span>
3. <span data-ttu-id="b35a7-146">Typ `npm install -g http-server`.</span><span class="sxs-lookup"><span data-stu-id="b35a7-146">Type `npm install -g http-server`.</span></span>

## <a name="build-the-index-and-run-the-application"></a><span data-ttu-id="b35a7-147">Bouw de index en voer de toepassing uit</span><span class="sxs-lookup"><span data-stu-id="b35a7-147">Build the index and run the application</span></span>
1. <span data-ttu-id="b35a7-148">Typ `npm run indexDocuments`.</span><span class="sxs-lookup"><span data-stu-id="b35a7-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="b35a7-149">Typ `npm run build`.</span><span class="sxs-lookup"><span data-stu-id="b35a7-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="b35a7-150">Typ `npm run start_server`.</span><span class="sxs-lookup"><span data-stu-id="b35a7-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="b35a7-151">Ga in uw browser naar `http://localhost:8080/index.html`</span><span class="sxs-lookup"><span data-stu-id="b35a7-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="b35a7-152">Zoeken in USGS-gegevens</span><span class="sxs-lookup"><span data-stu-id="b35a7-152">Search on USGS data</span></span>
<span data-ttu-id="b35a7-153">De USGS-gegevensset bevat records die relevant zijn voor de staat Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="b35a7-153">The USGS data set includes records that are relevant to the state of Rhode Island.</span></span> <span data-ttu-id="b35a7-154">Als u op **Zoeken** klikt terwijl het zoekvak leeg is, worden de bovenste 50 vermeldingen weergegeven. Dit is de standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="b35a7-154">If you click **Search** on an empty search box, you get the top 50 entries, which is the default.</span></span>

<span data-ttu-id="b35a7-155">Als u een zoekterm invoert, geeft u de zoekmachine iets om mee te werken.</span><span class="sxs-lookup"><span data-stu-id="b35a7-155">Entering a search term gives the search engine something to go on.</span></span> <span data-ttu-id="b35a7-156">Voer een regionale naam in.</span><span class="sxs-lookup"><span data-stu-id="b35a7-156">Try entering a regional name.</span></span> <span data-ttu-id="b35a7-157">'Roger Williams' was de eerste gouverneur van Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="b35a7-157">"Roger Williams" was the first governor of Rhode Island.</span></span> <span data-ttu-id="b35a7-158">Er zijn verschillende parken, gebouwen en scholen naar hem vernoemd.</span><span class="sxs-lookup"><span data-stu-id="b35a7-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="b35a7-159">U kunt ook de volgende termen proberen:</span><span class="sxs-lookup"><span data-stu-id="b35a7-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="b35a7-160">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="b35a7-160">Pawtucket</span></span>
* <span data-ttu-id="b35a7-161">Pembroke</span><span class="sxs-lookup"><span data-stu-id="b35a7-161">Pembroke</span></span>
* <span data-ttu-id="b35a7-162">goose +cape</span><span class="sxs-lookup"><span data-stu-id="b35a7-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="b35a7-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b35a7-163">Next steps</span></span>
<span data-ttu-id="b35a7-164">Dit is de eerste Azure Search-zelfstudie op basis van Node.js en de USGS-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="b35a7-164">This is the first Azure Search tutorial based on Node.js and the USGS dataset.</span></span> <span data-ttu-id="b35a7-165">In de loop van de tijd zal deze zelfstudie worden uitgebreid om aanvullende zoekfuncties te demonstreren die u mogelijk wilt gebruiken in uw aangepaste oplossingen.</span><span class="sxs-lookup"><span data-stu-id="b35a7-165">Over time, we'll extend this tutorial to demonstrate additional search features you might want to use in your custom solutions.</span></span>

<span data-ttu-id="b35a7-166">Als u al enige ervaring met Azure Search hebt, kunt u dit voorbeeld gebruiken als springplank om een suggestiefunctie (type-ahead of automatisch aangevulde query's), filters en facetnavigatie uit te proberen.</span><span class="sxs-lookup"><span data-stu-id="b35a7-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="b35a7-167">U kunt ook de pagina met zoekresultaten verbeteren door tellers toe te voegen document in batch te verwerken, zodat gebruikers door de resultaten kunnen bladeren.</span><span class="sxs-lookup"><span data-stu-id="b35a7-167">You can also improve upon the search results page by adding counts and batching documents so that users can page through the results.</span></span>

<span data-ttu-id="b35a7-168">Bent u niet bekend met Azure Search?</span><span class="sxs-lookup"><span data-stu-id="b35a7-168">New to Azure Search?</span></span> <span data-ttu-id="b35a7-169">Het is raadzaam andere zelfstudies te bekijken om inzicht te verwerven in wat u zoal kunt maken.</span><span class="sxs-lookup"><span data-stu-id="b35a7-169">We recommend trying other tutorials to develop an understanding of what you can create.</span></span> <span data-ttu-id="b35a7-170">Bezoek de [documentatiepagina](https://azure.microsoft.com/documentation/services/search/) voor meer resources.</span><span class="sxs-lookup"><span data-stu-id="b35a7-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) to find more resources.</span></span> <span data-ttu-id="b35a7-171">U kunt ook de koppelingen in de [lijst met video's en zelfstudies](search-video-demo-tutorial-list.md) volgen om meer informatie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="b35a7-171">You can also view the links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) to access more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
