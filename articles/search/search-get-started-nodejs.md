---
title: aaaGet slag met Azure Search in Node.js | Microsoft Docs
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
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="c1535-103">Aan de slag met Azure Search in Node.js</span><span class="sxs-lookup"><span data-stu-id="c1535-103">Get started with Azure Search in Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1535-104">Portal</span><span class="sxs-lookup"><span data-stu-id="c1535-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="c1535-105">.NET</span><span class="sxs-lookup"><span data-stu-id="c1535-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="c1535-106">Meer informatie over hoe toobuild een aangepaste Node.js-toepassing die gebruikmaakt van Azure Search voor de zoekfunctie zoeken.</span><span class="sxs-lookup"><span data-stu-id="c1535-106">Learn how toobuild a custom Node.js search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="c1535-107">Deze zelfstudie wordt gebruikgemaakt van Hallo [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct Hallo objecten en bewerkingen in deze oefening.</span><span class="sxs-lookup"><span data-stu-id="c1535-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="c1535-108">We hebben gebruikt [Node.js](https://Nodejs.org) en NPM, [Sublime Text 3](http://www.sublimetext.com/3), en Windows PowerShell op Windows 8.1 toodevelop en test deze code.</span><span class="sxs-lookup"><span data-stu-id="c1535-108">We used [Node.js](https://Nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 toodevelop and test this code.</span></span>

<span data-ttu-id="c1535-109">toorun dit voorbeeld hebt u een Azure Search-service, u voor Hallo aanmelden kunt [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c1535-109">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c1535-110">Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="c1535-110">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-hello-data"></a><span data-ttu-id="c1535-111">Over Hallo-gegevens</span><span class="sxs-lookup"><span data-stu-id="c1535-111">About hello data</span></span>
<span data-ttu-id="c1535-112">Deze voorbeeldtoepassing gebruikt gegevens uit Hallo [Verenigde Staten Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), gefilterd op Hallo staat Rhode Island tooreduce Hallo gegevensset grootte.</span><span class="sxs-lookup"><span data-stu-id="c1535-112">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="c1535-113">We gebruiken deze gegevens toobuild een zoektoepassing die kenmerkende gebouwen zoals ziekenhuizen en scholen, evenals geologische kenmerken, zoals stromen, meren en toppen retourneert.</span><span class="sxs-lookup"><span data-stu-id="c1535-113">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="c1535-114">In deze toepassing hello **DataIndexer** programma bouwt en belastingen Hallo index met behulp van een [indexeerfunctie](https://msdn.microsoft.com/library/azure/dn798918.aspx) constructie, bij het ophalen van Hallo gefilterde USGS-gegevensset uit een openbare Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="c1535-114">In this application, hello **DataIndexer** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="c1535-115">Referenties en verbinding vindt u informatie toohello onlinegegevensbron in Hallo programmacode.</span><span class="sxs-lookup"><span data-stu-id="c1535-115">Credentials and connection information toohello online data source is provided in hello program code.</span></span> <span data-ttu-id="c1535-116">U hoeft verder niets te configureren.</span><span class="sxs-lookup"><span data-stu-id="c1535-116">No further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="c1535-117">We een filter toegepast op deze gegevensset toostay onder Hallo 10.000 Documentlimiet Hallo gratis prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="c1535-117">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="c1535-118">Als u de standaardcategorie Hallo gebruikt, is deze limiet niet van toepassing.</span><span class="sxs-lookup"><span data-stu-id="c1535-118">If you use hello standard tier, this limit does not apply.</span></span> <span data-ttu-id="c1535-119">Zie [Limieten voor de Search-service](search-limits-quotas-capacity.md) voor meer informatie over de capaciteit voor elke prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="c1535-119">For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).</span></span>
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="c1535-120">Hallo-servicenaam en api-sleutel van uw Azure Search-service zoeken</span><span class="sxs-lookup"><span data-stu-id="c1535-120">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="c1535-121">Nadat u Hallo service maakt, keert u terug toohello portal tooget Hallo URL of `api-key`.</span><span class="sxs-lookup"><span data-stu-id="c1535-121">After you create hello service, return toohello portal tooget hello URL or `api-key`.</span></span> <span data-ttu-id="c1535-122">Verbindingen tooyour Search-service vereisen dat u beide Hallo-URL en een `api-key` tooauthenticate Hallo aanroep.</span><span class="sxs-lookup"><span data-stu-id="c1535-122">Connections tooyour Search service require that you have both hello URL and an `api-key` tooauthenticate hello call.</span></span>

1. <span data-ttu-id="c1535-123">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c1535-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c1535-124">Klik in de snelbalk hello **zoekservice** toolist alle Azure Search-services die zijn ingericht voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="c1535-124">In hello jump bar, click **Search service** toolist all Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="c1535-125">Selecteer de gewenste toouse Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="c1535-125">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="c1535-126">U ziet op Hallo servicedashboard tegels voor essentiële informatie, zoals het sleutelpictogram voor toegang tot de beheersleutels Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1535-126">On hello service dashboard, you should see tiles for essential information, such as hello key icon for accessing hello admin keys.</span></span>
5. <span data-ttu-id="c1535-127">Kopieer Hallo service-URL, een beheersleutel en een querysleutel.</span><span class="sxs-lookup"><span data-stu-id="c1535-127">Copy hello service URL, an admin key, and a query key.</span></span> <span data-ttu-id="c1535-128">U moet alle drie later wanneer u ze toohello bestand config.js file toevoegt.</span><span class="sxs-lookup"><span data-stu-id="c1535-128">You need all three later when you add them toohello config.js file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="c1535-129">Hallo voorbeeldbestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="c1535-129">Download hello sample files</span></span>
<span data-ttu-id="c1535-130">Gebruik een van de Hallo benaderingen toodownload Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="c1535-130">Use either one of hello following approaches toodownload hello sample.</span></span>

1. <span data-ttu-id="c1535-131">Ga te[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span><span class="sxs-lookup"><span data-stu-id="c1535-131">Go too[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span></span>
2. <span data-ttu-id="c1535-132">Klik op **ZIP downloaden**, Hallo ZIP-bestand opslaan en pak vervolgens alle Hallo bestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="c1535-132">Click **Download ZIP**, save hello .zip file, and then extract all hello files it contains.</span></span>

<span data-ttu-id="c1535-133">Alle volgende bestandswijzigingen en uitvoerinstructies worden uitgevoerd voor de bestanden in deze map.</span><span class="sxs-lookup"><span data-stu-id="c1535-133">All subsequent file modifications and run statements are made against files in this folder.</span></span>

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="c1535-134">Hallo config.js bijwerken.</span><span class="sxs-lookup"><span data-stu-id="c1535-134">Update hello config.js.</span></span> <span data-ttu-id="c1535-135">met de URL van de Search-service en uw API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="c1535-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="c1535-136">URL en api-sleutel die u eerder hebt gekopieerd met behulp van Hallo Hallo-URL, beheersleutel en querysleutel opgeven in het configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="c1535-136">Using hello URL and api-key that you copied earlier, specify hello URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="c1535-137">Beheersleutels bieden u de volledige controle over de servicebewerkingen, inclusief het maken of verwijderen van een index en het laden van documenten.</span><span class="sxs-lookup"><span data-stu-id="c1535-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="c1535-138">Querysleutels zijn daarentegen voor alleen-lezen bewerkingen, meestal worden gebruikt door clienttoepassingen die verbinding maken met tooAzure zoeken.</span><span class="sxs-lookup"><span data-stu-id="c1535-138">In contrast, query keys are for read-only operations, typically used by client applications that connect tooAzure Search.</span></span>

<span data-ttu-id="c1535-139">In dit voorbeeld opnemen we Hallo query sleutel toohelp versterking Hallo beste praktijken van het gebruik van Hallo querysleutel in clienttoepassingen.</span><span class="sxs-lookup"><span data-stu-id="c1535-139">In this sample, we include hello query key toohelp reinforce hello best practice of using hello query key in client applications.</span></span>

<span data-ttu-id="c1535-140">Hallo volgende schermafbeelding ziet **config.js** openen in een teksteditor, hello relevante items zijn gemarkeerd, zodat u kunt zien waar tooupdate Hallo-bestand met de Hallo waarden die geldig zijn voor uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="c1535-140">hello following screenshot shows **config.js** open in a text editor, with hello relevant entries demarcated so that you can see where tooupdate hello file with hello values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a><span data-ttu-id="c1535-141">Een runtime-omgeving voor Hallo voorbeeld hosten</span><span class="sxs-lookup"><span data-stu-id="c1535-141">Host a runtime environment for hello sample</span></span>
<span data-ttu-id="c1535-142">Hallo vereist een HTTP-server die u kunt globaal installeren met npm.</span><span class="sxs-lookup"><span data-stu-id="c1535-142">hello sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="c1535-143">Gebruik een PowerShell-venster voor Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="c1535-143">Use a PowerShell window for hello following commands.</span></span>

1. <span data-ttu-id="c1535-144">Navigeer toohello-map met de Hallo **package.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="c1535-144">Navigate toohello folder that contains hello **package.json** file.</span></span>
2. <span data-ttu-id="c1535-145">Typ `npm install`.</span><span class="sxs-lookup"><span data-stu-id="c1535-145">Type `npm install`.</span></span>
3. <span data-ttu-id="c1535-146">Typ `npm install -g http-server`.</span><span class="sxs-lookup"><span data-stu-id="c1535-146">Type `npm install -g http-server`.</span></span>

## <a name="build-hello-index-and-run-hello-application"></a><span data-ttu-id="c1535-147">Hallo-toepassing hello index bouwen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c1535-147">Build hello index and run hello application</span></span>
1. <span data-ttu-id="c1535-148">Typ `npm run indexDocuments`.</span><span class="sxs-lookup"><span data-stu-id="c1535-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="c1535-149">Typ `npm run build`.</span><span class="sxs-lookup"><span data-stu-id="c1535-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="c1535-150">Typ `npm run start_server`.</span><span class="sxs-lookup"><span data-stu-id="c1535-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="c1535-151">Ga in uw browser naar `http://localhost:8080/index.html`</span><span class="sxs-lookup"><span data-stu-id="c1535-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="c1535-152">Zoeken in USGS-gegevens</span><span class="sxs-lookup"><span data-stu-id="c1535-152">Search on USGS data</span></span>
<span data-ttu-id="c1535-153">Hallo USGS-gegevensset bevat records die relevant toohello staat Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="c1535-153">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="c1535-154">Als u op **Search** op het zoekvak leeg is, u krijgen Hallo bovenste 50 vermeldingen, Hallo standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="c1535-154">If you click **Search** on an empty search box, you get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="c1535-155">Een zoekterm invoert biedt Hallo zoekmachine iets toogo op.</span><span class="sxs-lookup"><span data-stu-id="c1535-155">Entering a search term gives hello search engine something toogo on.</span></span> <span data-ttu-id="c1535-156">Voer een regionale naam in.</span><span class="sxs-lookup"><span data-stu-id="c1535-156">Try entering a regional name.</span></span> <span data-ttu-id="c1535-157">'Roger Williams' was Hallo eerste gouverneur van Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="c1535-157">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="c1535-158">Er zijn verschillende parken, gebouwen en scholen naar hem vernoemd.</span><span class="sxs-lookup"><span data-stu-id="c1535-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="c1535-159">U kunt ook de volgende termen proberen:</span><span class="sxs-lookup"><span data-stu-id="c1535-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="c1535-160">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="c1535-160">Pawtucket</span></span>
* <span data-ttu-id="c1535-161">Pembroke</span><span class="sxs-lookup"><span data-stu-id="c1535-161">Pembroke</span></span>
* <span data-ttu-id="c1535-162">goose +cape</span><span class="sxs-lookup"><span data-stu-id="c1535-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1535-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c1535-163">Next steps</span></span>
<span data-ttu-id="c1535-164">Dit is Hallo eerste Azure Search-zelfstudie op basis van Node.js en Hallo USGS-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="c1535-164">This is hello first Azure Search tutorial based on Node.js and hello USGS dataset.</span></span> <span data-ttu-id="c1535-165">Na verloop van tijd hebt we deze zelfstudie toodemonstrate aanvullende zoekfuncties kunt u toouse in uw aangepaste oplossingen uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="c1535-165">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="c1535-166">Als u al enige ervaring met Azure Search hebt, kunt u dit voorbeeld gebruiken als springplank om een suggestiefunctie (type-ahead of automatisch aangevulde query's), filters en facetnavigatie uit te proberen.</span><span class="sxs-lookup"><span data-stu-id="c1535-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="c1535-167">U kunt ook op Hallo pagina met zoekresultaten verbeteren door tellers toe te voegen document in batch zodat gebruikers kunnen via Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="c1535-167">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="c1535-168">Nieuwe tooAzure zoeken?</span><span class="sxs-lookup"><span data-stu-id="c1535-168">New tooAzure Search?</span></span> <span data-ttu-id="c1535-169">Het is raadzaam om bij andere zelfstudies toodevelop een goed begrip van kunt maken.</span><span class="sxs-lookup"><span data-stu-id="c1535-169">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="c1535-170">Ga naar onze [documentatiepagina](https://azure.microsoft.com/documentation/services/search/) toofind meer bronnen.</span><span class="sxs-lookup"><span data-stu-id="c1535-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="c1535-171">U kunt ook weergeven Hallo koppelingen in onze [Video's en zelfstudies lijst](search-video-demo-tutorial-list.md) tooaccess meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c1535-171">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
