---
title: aaaHow toouse Power BI Embedded met REST | Microsoft Docs
description: 'Meer informatie over hoe toouse Power BI Embedded met REST '
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 98057724e60ba868f9c93de8c50383569eb8852d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-power-bi-embedded-with-rest"></a><span data-ttu-id="9d58d-103">Hoe toouse Power BI Embedded met REST</span><span class="sxs-lookup"><span data-stu-id="9d58d-103">How toouse Power BI Embedded with REST</span></span>

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a><span data-ttu-id="9d58d-104">Power BI Embedded: Wat is en wat het doet</span><span class="sxs-lookup"><span data-stu-id="9d58d-104">Power BI Embedded: What it is and what it's for</span></span>

<span data-ttu-id="9d58d-105">Een overzicht van Power BI Embedded wordt beschreven in de officiële Hallo [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), maar we even voordat we Hallo details over het gebruik van deze met REST krijgen.</span><span class="sxs-lookup"><span data-stu-id="9d58d-105">An overview of Power BI Embedded is described in hello official [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), but let's take a quick look before we get into hello details about using it with REST.</span></span>

<span data-ttu-id="9d58d-106">Het is heel heel eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="9d58d-106">It's quite simple, really.</span></span> <span data-ttu-id="9d58d-107">u kunt toouse Hallo dynamische gegevensvisualisaties van [Power BI](https://powerbi.microsoft.com) in uw eigen toepassing.</span><span class="sxs-lookup"><span data-stu-id="9d58d-107">you may want toouse hello dynamic data visualizations of [Power BI](https://powerbi.microsoft.com) in your own application.</span></span>

<span data-ttu-id="9d58d-108">De meeste aangepaste toepassingen nodig toodeliver Hallo gegevens hebben voor hun eigen klanten, niet noodzakelijkerwijs gebruikers in hun eigen organisatie.</span><span class="sxs-lookup"><span data-stu-id="9d58d-108">Most custom applications need toodeliver hello data for their own customers, not necessarily users in their own organization.</span></span> <span data-ttu-id="9d58d-109">Bijvoorbeeld, als u deel van de service voor bedrijf A en B bedrijf bieden, moeten gebruikers in bedrijf A alleen gegevens zien voor hun eigen bedrijf A. Dat wil zeggen, is Hallo multi-tenancymodus nodig voor de levering van Hallo.</span><span class="sxs-lookup"><span data-stu-id="9d58d-109">For example, if you're delivering some service for both company A and company B, users in company A should only see data for their own company A. That is, hello multi-tenancy is needed for hello delivery.</span></span>

<span data-ttu-id="9d58d-110">aangepaste toepassing Hello mogelijk worden biedt tevens een eigen verificatiemethoden zoals formulierverificatie, basic auth, enzovoort...</span><span class="sxs-lookup"><span data-stu-id="9d58d-110">hello custom application might also be offering its own authentication methods such as forms auth, basic auth, etc..</span></span> <span data-ttu-id="9d58d-111">Vervolgens Hallo insluiten oplossing moet werken samen met deze bestaande verificatiemethoden veilig.</span><span class="sxs-lookup"><span data-stu-id="9d58d-111">Then, hello embedding solution must collaborate with this existing authentication methods safely.</span></span> <span data-ttu-id="9d58d-112">Het is ook nodig zijn voor gebruikers toobe kunnen toouse die ISV-toepassingen zonder Hallo extra aankoop- of -licentieverlening van een Power BI-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9d58d-112">It's also necessary for users toobe able toouse those ISV applications without hello extra purchase or licensing of a Power BI subscription.</span></span>

 <span data-ttu-id="9d58d-113">**Power BI Embedded** is ontworpen voor nauwkeurig dit soort scenario's.</span><span class="sxs-lookup"><span data-stu-id="9d58d-113">**Power BI Embedded** is designed for precisely these kinds of scenarios.</span></span> <span data-ttu-id="9d58d-114">Dus nu dat we deze korte inleiding buiten Hallo manier hebben, gaan we krijgen tot de details van sommige</span><span class="sxs-lookup"><span data-stu-id="9d58d-114">So, now that we have that quick introduction out of hello way, let's get into some details</span></span>

<span data-ttu-id="9d58d-115">U kunt .NET Hallo \(C#) of Node.js SDK, tooeasily uw toepassing met Power BI Embedded bouwen.</span><span class="sxs-lookup"><span data-stu-id="9d58d-115">You can use hello .NET \(C#) or Node.js SDK, tooeasily build your application with Power BI Embedded.</span></span> <span data-ttu-id="9d58d-116">Maar in dit artikel wordt uitgelegd over HTTP-stroom \(inclusief AuthN) van Power BI zonder SDK's.</span><span class="sxs-lookup"><span data-stu-id="9d58d-116">But, in this article, we'll explain about HTTP flow \(incl. AuthN) of Power BI without SDKs.</span></span> <span data-ttu-id="9d58d-117">Kennis van deze overdracht, kunt u uw toepassing bouwen **met elke programmeertaal**, en u kunt begrijpt diep Hallo essentie van Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="9d58d-117">Understanding this flow, you can build your application **with any programming language**, and you can understand deeply hello essence of Power BI Embedded.</span></span>

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a><span data-ttu-id="9d58d-118">Maken van Power BI-werkruimteverzameling en get-toegangssleutel \(inrichten)</span><span class="sxs-lookup"><span data-stu-id="9d58d-118">Create Power BI workspace collection, and get access key \(Provisioning)</span></span>

<span data-ttu-id="9d58d-119">Power BI Embedded is een van de hello Azure-services.</span><span class="sxs-lookup"><span data-stu-id="9d58d-119">Power BI Embedded is one of hello Azure services.</span></span> <span data-ttu-id="9d58d-120">Alleen Hallo ISV die gebruikmaakt van Azure Portal wordt in rekening gebracht voor gebruikskosten \(per uur gebruikerssessie), en het Hallo-gebruiker die weergaven Hallo rapport is niet geladen of zelfs een Azure-abonnement nodig.</span><span class="sxs-lookup"><span data-stu-id="9d58d-120">Only hello ISV who uses Azure Portal is charged for usage fees \(per hourly user session), and hello user who views hello report isn't charged or even require an Azure subscription.</span></span>
<span data-ttu-id="9d58d-121">Voordat u begint onze toepassingsontwikkeling, maken we Hallo **Power BI-werkruimteverzameling** met behulp van Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="9d58d-121">Before starting our application development, we must create hello **Power BI workspace collection** by using Azure Portal.</span></span>

<span data-ttu-id="9d58d-122">Elke werkruimte van Power BI Embedded Hallo werkruimte voor elke klant (tenant) is en we veel werkruimten in elke werkruimteverzameling kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9d58d-122">Each workspace of Power BI Embedded is hello workspace for each customer (tenant), and we can add many workspaces in each workspace collection.</span></span> <span data-ttu-id="9d58d-123">Hallo dezelfde toegangssleutel wordt gebruikt in elke werkruimteverzameling.</span><span class="sxs-lookup"><span data-stu-id="9d58d-123">hello same access key is used in each workspace collection.</span></span> <span data-ttu-id="9d58d-124">In effect Hallo werkruimteverzameling is de beveiligingsgrens Hallo voor Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="9d58d-124">In-effect, hello workspace collection is hello security boundary for Power BI Embedded.</span></span>

![](media/power-bi-embedded-iframe/create-workspace.png)

<span data-ttu-id="9d58d-125">Wanneer we klaar bent met het Hallo-werkruimteverzameling maken, kopieert u de toegangssleutel Hallo vanuit Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9d58d-125">When we finish creating hello workspace collection, copy hello access key from Azure Portal.</span></span>

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> <span data-ttu-id="9d58d-126">We kunnen ook Hallo werkruimteverzameling inrichten en verkrijgen toegangssleutel via REST-API.</span><span class="sxs-lookup"><span data-stu-id="9d58d-126">We can also provision hello workspace collection and get access key via REST API.</span></span> <span data-ttu-id="9d58d-127">toolearn meer, Zie [Power BI Resource Provider-API's](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d58d-127">toolearn more, see [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span></span>

## <a name="create-pbix-file-with-power-bi-desktop"></a><span data-ttu-id="9d58d-128">Pbix-bestand maken met Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="9d58d-128">Create .pbix file with Power BI Desktop</span></span>

<span data-ttu-id="9d58d-129">Vervolgens maken we moet gegevensverbinding Hallo en rapporten toobe ingesloten.</span><span class="sxs-lookup"><span data-stu-id="9d58d-129">Next, we must create hello data connection and reports toobe embedded.</span></span>
<span data-ttu-id="9d58d-130">Voor deze taak is er geen programmeren of de code.</span><span class="sxs-lookup"><span data-stu-id="9d58d-130">For this task, there’s no programming or code.</span></span> <span data-ttu-id="9d58d-131">We gebruiken gewoon Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="9d58d-131">We just use Power BI Desktop.</span></span>
<span data-ttu-id="9d58d-132">In dit artikel won't doorloopt u informatie over het Hallo toouse Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="9d58d-132">In this article, we won't go through hello details about how toouse Power BI Desktop.</span></span> <span data-ttu-id="9d58d-133">Als u moet enkele hier, raadpleegt u [aan de slag met Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="9d58d-133">If you need some help here, see [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span></span> <span data-ttu-id="9d58d-134">In ons voorbeeld gebruiken we zojuist Hallo [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span><span class="sxs-lookup"><span data-stu-id="9d58d-134">For our example, we'll just use hello [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span></span>

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a><span data-ttu-id="9d58d-135">Een Power BI-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="9d58d-135">Create a Power BI workspace</span></span>

<span data-ttu-id="9d58d-136">Nu dat Hallo inrichten is voltooid, aan de slag van een klant-werkruimte maken in de werkruimteverzameling Hallo via REST-API's.</span><span class="sxs-lookup"><span data-stu-id="9d58d-136">Now that hello provisioning is all done, let’s get started creating a customer’s workspace in hello workspace collection via REST APIs.</span></span> <span data-ttu-id="9d58d-137">Hallo maakt volgende HTTP POST aanvragen (REST) Hallo nieuwe werkruimte in de werkruimteverzameling van onze bestaande.</span><span class="sxs-lookup"><span data-stu-id="9d58d-137">hello following HTTP POST Request (REST) is creating hello new workspace in our existing workspace collection.</span></span> <span data-ttu-id="9d58d-138">Dit is Hallo [POST werkruimte API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d58d-138">This is hello [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span> <span data-ttu-id="9d58d-139">In ons voorbeeld is de naam van Hallo werkruimte verzameling **mypbiapp**.</span><span class="sxs-lookup"><span data-stu-id="9d58d-139">In our example, hello workspace collection name is **mypbiapp**.</span></span> <span data-ttu-id="9d58d-140">We stelt u de toegangssleutel hello, die we eerder hebt gekopieerd, als **App-sleutel**.</span><span class="sxs-lookup"><span data-stu-id="9d58d-140">We just set hello access key, which we previously copied, as **AppKey**.</span></span> <span data-ttu-id="9d58d-141">Het is zeer eenvoudig verificatie.</span><span class="sxs-lookup"><span data-stu-id="9d58d-141">It’s very simple authentication!</span></span>

<span data-ttu-id="9d58d-142">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="9d58d-142">**HTTP Request**</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="9d58d-143">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="9d58d-143">**HTTP Response**</span></span>

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

<span data-ttu-id="9d58d-144">Hallo geretourneerd **workspaceId** wordt gebruikt voor Hallo na de volgende API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="9d58d-144">hello returned **workspaceId** is used for hello following subsequent API calls.</span></span> <span data-ttu-id="9d58d-145">Onze toepassing moet deze waarde bewaren.</span><span class="sxs-lookup"><span data-stu-id="9d58d-145">Our application must retain this value.</span></span>

## <a name="import-pbix-file-into-hello-workspace"></a><span data-ttu-id="9d58d-146">Hallo-werkruimte van pbix-bestand importeren</span><span class="sxs-lookup"><span data-stu-id="9d58d-146">Import .pbix file into hello workspace</span></span>

<span data-ttu-id="9d58d-147">Elk rapport in een werkruimte overeenkomt met tooa één Power BI Desktop-bestand met een gegevensset \(met inbegrip van instellingen voor gegevensbron).</span><span class="sxs-lookup"><span data-stu-id="9d58d-147">Each report in a workspace corresponds tooa single Power BI Desktop file with a dataset \(including datasource settings).</span></span> <span data-ttu-id="9d58d-148">We kunt onze werkruimte pbix-bestand toohello zoals weergegeven in onderstaande Hallo code importeren.</span><span class="sxs-lookup"><span data-stu-id="9d58d-148">We can import our .pbix file toohello workspace as shown in hello code below.</span></span> <span data-ttu-id="9d58d-149">Zoals u ziet, kunnen we Hallo binair van pbix-bestand met MIME-multipart in HTTP-uploaden.</span><span class="sxs-lookup"><span data-stu-id="9d58d-149">As you can see, we can upload hello binary of .pbix file using MIME multipart in http.</span></span>

<span data-ttu-id="9d58d-150">Hallo-uri-fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** hello workspaceId en queryparameter **datasetDisplayName** Hallo gegevensset naam toocreate is.</span><span class="sxs-lookup"><span data-stu-id="9d58d-150">hello uri fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is hello workspaceId, and query parameter **datasetDisplayName** is hello dataset name toocreate.</span></span> <span data-ttu-id="9d58d-151">Hallo gemaakt gegevensset bevat alle gegevens met betrekking artefacten in pbix-bestand, zoals de geïmporteerde gegevens Hallo aanwijzer toohello gegevensbron, enzovoort...</span><span class="sxs-lookup"><span data-stu-id="9d58d-151">hello created dataset holds all data related artifacts in .pbix file such as imported data, hello pointer toohello data source, etc..</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{hello content (binary) of .pbix file}
--A300testx--
```

<span data-ttu-id="9d58d-152">Deze importtaak kan uitvoeren voor een tijdje.</span><span class="sxs-lookup"><span data-stu-id="9d58d-152">This import task might run for a while.</span></span> <span data-ttu-id="9d58d-153">Als u klaar kunt onze toepassing hello taakstatus import-id met vragen. In ons voorbeeld Hallo import-id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span><span class="sxs-lookup"><span data-stu-id="9d58d-153">When complete, our application can ask hello task status using import id. In our example, hello import id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span></span>

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

<span data-ttu-id="9d58d-154">Hallo volgende vraagt de status van deze import-id:</span><span class="sxs-lookup"><span data-stu-id="9d58d-154">hello following is asking status using this import id:</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="9d58d-155">Als Hallo-taak niet is voltooid, kan de Hallo HTTP-antwoord zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="9d58d-155">If hello task isn't complete, hello HTTP response could be like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

<span data-ttu-id="9d58d-156">Als het Hallo-taak is voltooid, kan de Hallo HTTP-antwoord meer als volgt zijn:</span><span class="sxs-lookup"><span data-stu-id="9d58d-156">If hello task is complete, hello HTTP response could be more like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a><span data-ttu-id="9d58d-157">Gegevensbron connectiviteit \(en multi-tenancymodus van gegevens)</span><span class="sxs-lookup"><span data-stu-id="9d58d-157">Data source connectivity \(and multi-tenancy of data)</span></span>

<span data-ttu-id="9d58d-158">Terwijl bijna alle Hallo artefacten in pbix-bestand in de werkruimte worden geïmporteerd, zijn geen Hallo referenties voor gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="9d58d-158">While almost all of hello artifacts in .pbix file are imported into our workspace, hello  credentials for data sources are not.</span></span> <span data-ttu-id="9d58d-159">Als gevolg hiervan, wanneer u **DirectQuery-modus**, hello ingesloten rapport kan niet meer correct weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9d58d-159">As a result, when using **DirectQuery mode**, hello embedded report cannot be shown correctly.</span></span> <span data-ttu-id="9d58d-160">Maar wanneer u **importmodus**, we Hallo rapport met Hallo bestaande geïmporteerde gegevens kunt bekijken.</span><span class="sxs-lookup"><span data-stu-id="9d58d-160">But, when using **Import mode**, we can view hello report using hello existing imported data.</span></span> <span data-ttu-id="9d58d-161">In dat geval moet er Hallo-referentie met behulp van de volgende stappen uit via de REST-aanroepen Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="9d58d-161">In such a case, we must set hello credential using hello following steps via REST calls.</span></span>

<span data-ttu-id="9d58d-162">Er moet eerst Hallo gateway datasource ophalen.</span><span class="sxs-lookup"><span data-stu-id="9d58d-162">First, we must get hello gateway datasource.</span></span> <span data-ttu-id="9d58d-163">We weten Hallo gegevensset **id** Hallo eerder geretourneerd id.</span><span class="sxs-lookup"><span data-stu-id="9d58d-163">We know hello dataset **id** is hello previously returned id.</span></span>

<span data-ttu-id="9d58d-164">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="9d58d-164">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="9d58d-165">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="9d58d-165">**HTTP Response**</span></span>

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

<span data-ttu-id="9d58d-166">Met behulp van Hallo geretourneerd gateway-id en een datasource-id \(Zie vorige Hallo **gatewayId** en **id** in Hallo resultaat geretourneerd), kunnen we Hallo referentie van deze gegevensbron als volgt wijzigen:</span><span class="sxs-lookup"><span data-stu-id="9d58d-166">Using hello returned gateway id and datasource id \(see hello previous **gatewayId** and **id** in hello returned result), we can change hello credential of this datasource as follows:</span></span>

<span data-ttu-id="9d58d-167">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="9d58d-167">**HTTP Request**</span></span>

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

<span data-ttu-id="9d58d-168">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="9d58d-168">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

<span data-ttu-id="9d58d-169">In productie, kunnen we ook Hallo verschillende verbindingsreeks voor elke werkruimte met REST-API instellen.</span><span class="sxs-lookup"><span data-stu-id="9d58d-169">In production, we can also set hello different connection string for each workspace using REST API.</span></span> <span data-ttu-id="9d58d-170">\(Internet Explorer, we kunt scheiden Hallo database voor elk klanten.)</span><span class="sxs-lookup"><span data-stu-id="9d58d-170">\(i.e, we can separate hello database for each customers.)</span></span>

<span data-ttu-id="9d58d-171">Hallo volgende met het wijzigen van de verbindingsreeks Hallo van datasource via REST.</span><span class="sxs-lookup"><span data-stu-id="9d58d-171">hello following is changing hello connection string of datasource via REST.</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

<span data-ttu-id="9d58d-172">Of we beveiliging op rijniveau in Power BI Embedded kunnen gebruiken en we Hallo-gegevens voor elke gebruikers in een rapport kunt scheiden.</span><span class="sxs-lookup"><span data-stu-id="9d58d-172">Or, we can use Row Level Security in Power BI Embedded and we can separate hello data for each users in one report.</span></span> <span data-ttu-id="9d58d-173">We kunnen as a Result, elke klant rapport met dezelfde pbix inrichten \(gebruikersinterface, enz.) en andere gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="9d58d-173">As a result, we can provision each customer report with same .pbix \(UI, etc.) and different data sources.</span></span>

> [!NOTE]
> <span data-ttu-id="9d58d-174">Als u **importmodus** in plaats van **DirectQuery-modus**, er is geen modellen manier toorefresh via API.</span><span class="sxs-lookup"><span data-stu-id="9d58d-174">If you’re using **Import mode** instead of **DirectQuery mode**, there’s no way toorefresh models via API.</span></span> <span data-ttu-id="9d58d-175">En on-premises gegevensbronnen via Power BI gateway nog wordt niet ondersteund in Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="9d58d-175">And, on-premises datasources through Power BI gateway isn't yet supported in Power BI Embedded.</span></span> <span data-ttu-id="9d58d-176">Echter zeker zult u tookeep gaten Hallo [Power BI-blog](https://powerbi.microsoft.com/blog/) voor wat is er nieuw en wat er nieuw in toekomstige releases.</span><span class="sxs-lookup"><span data-stu-id="9d58d-176">However, you'll really want tookeep an eye on hello [Power BI blog](https://powerbi.microsoft.com/blog/) for what's new and what's coming in future releases.</span></span>

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a><span data-ttu-id="9d58d-177">Verificatie en die als host fungeert voor (insluiten) rapporten in onze webpagina</span><span class="sxs-lookup"><span data-stu-id="9d58d-177">Authentication and hosting (embedding) reports in our web page</span></span>

<span data-ttu-id="9d58d-178">In Hallo vorige REST-API, gebruiken we Hallo toegangssleutel **App-sleutel** zelf als Hallo autorisatie-header.</span><span class="sxs-lookup"><span data-stu-id="9d58d-178">In hello previous REST API, we can use hello access key **AppKey** itself as hello authorization header.</span></span> <span data-ttu-id="9d58d-179">Het is veilig omdat deze aanroepen kunnen worden verwerkt op Hallo back-end-serverzijde.</span><span class="sxs-lookup"><span data-stu-id="9d58d-179">Because these calls can be handled on hello backend server side, it's safe.</span></span>

<span data-ttu-id="9d58d-180">Maar wanneer we Hallo rapport in onze webpagina insluiten, dit soort informatie over beveiliging zou worden verwerkt met JavaScript \(frontend).</span><span class="sxs-lookup"><span data-stu-id="9d58d-180">But, when we embed hello report in our web page, this kind of security information would be handled using JavaScript \(frontend).</span></span> <span data-ttu-id="9d58d-181">Vervolgens moet Hallo autorisatie-header-waarde worden beveiligd.</span><span class="sxs-lookup"><span data-stu-id="9d58d-181">Then hello authorization header value must be secured.</span></span> <span data-ttu-id="9d58d-182">Als onze toegangssleutel wordt gedetecteerd door een kwaadwillende gebruiker of schadelijke code, kunnen ze geen bewerkingen met deze sleutel aanroepen.</span><span class="sxs-lookup"><span data-stu-id="9d58d-182">If our access key is discovered by a malicious user or malicious code, they can call any operations using this key.</span></span>

<span data-ttu-id="9d58d-183">Wanneer we Hallo rapport in onze webpagina insluiten, moet we berekende Hallo-token gebruiken in plaats van de toegangssleutel **App-sleutel**.</span><span class="sxs-lookup"><span data-stu-id="9d58d-183">When we embed hello report in our web page, we must use hello computed token instead of access key **AppKey**.</span></span> <span data-ttu-id="9d58d-184">Onze toepassing hello OAuth Json Web Token moet maken \(JWT) die bestaat uit Hallo claims en Hallo berekende digitale handtekening.</span><span class="sxs-lookup"><span data-stu-id="9d58d-184">Our application must create hello OAuth Json Web Token \(JWT) which consists of hello claims and hello computed digital signature.</span></span> <span data-ttu-id="9d58d-185">Zoals hieronder weergegeven, is deze OAuth JWT-tokens punt gescheiden gecodeerde tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9d58d-185">As illustrated below, this OAuth JWT is dot-delimited encoded string tokens.</span></span>

![](media/power-bi-embedded-iframe/oauth-jwt.png)

<span data-ttu-id="9d58d-186">Er moet eerst Hallo invoerwaarde, die later wordt ondertekend voorbereiden.</span><span class="sxs-lookup"><span data-stu-id="9d58d-186">First, we must prepare hello input value, which is signed later.</span></span> <span data-ttu-id="9d58d-187">Deze waarde is Hallo base64-gecodeerd url (rfc4648) tekenreeks Hallo volgende json en deze worden gescheiden door Hallo punt \(.) teken.</span><span class="sxs-lookup"><span data-stu-id="9d58d-187">This value is hello base64 url encoded (rfc4648) string of hello following json, and these are delimited by hello dot \(.) character.</span></span> <span data-ttu-id="9d58d-188">Later, wordt uitgelegd hoe tooget Hallo lijst-id.</span><span class="sxs-lookup"><span data-stu-id="9d58d-188">Later, we'll explain how tooget hello report id.</span></span>

> [!NOTE]
> <span data-ttu-id="9d58d-189">Als we toouse rij Level Security (RLS) met Power BI Embedded willen, er moet ook opgeven **gebruikersnaam** en **rollen** in Hallo claims.</span><span class="sxs-lookup"><span data-stu-id="9d58d-189">If we want toouse Row Level Security (RLS) with Power BI Embedded, we must also specify **username** and **roles** in hello claims.</span></span>

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

<span data-ttu-id="9d58d-190">Vervolgens maken we Hallo base64-gecodeerde tekenreeks HMAC \(Hallo handtekening) met SHA256-algoritme.</span><span class="sxs-lookup"><span data-stu-id="9d58d-190">Next, we must create hello base64 encoded string of HMAC \(hello signature) with SHA256 algorithm.</span></span> <span data-ttu-id="9d58d-191">Deze ondertekende invoerwaarde is Hallo vorige tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9d58d-191">This signed input value is hello previous string.</span></span>

<span data-ttu-id="9d58d-192">Laatste, moet we Hallo invoerwaarde en handtekening tekenreeks op basis van de periode combineren \(.) teken.</span><span class="sxs-lookup"><span data-stu-id="9d58d-192">Last, we must combine hello input value and signature string using period \(.) character.</span></span> <span data-ttu-id="9d58d-193">Hallo voltooid tekenreeks is Hallo app-token voor het Hallo-rapport insluiten.</span><span class="sxs-lookup"><span data-stu-id="9d58d-193">hello completed string is hello app token for hello report embedding.</span></span> <span data-ttu-id="9d58d-194">Zelfs als Hallo app-token wordt gedetecteerd door een kwaadwillende gebruiker, kunnen ze Hallo oorspronkelijke toegangssleutel niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="9d58d-194">Even if hello app token is discovered by a malicious user, they cannot get hello original access key.</span></span> <span data-ttu-id="9d58d-195">Deze app-token verloopt snel.</span><span class="sxs-lookup"><span data-stu-id="9d58d-195">This app token will expire quickly.</span></span>

<span data-ttu-id="9d58d-196">Hier volgt een voorbeeld van een PHP voor deze stappen:</span><span class="sxs-lookup"><span data-stu-id="9d58d-196">Here's a PHP example for these steps:</span></span>

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is hello apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-hello-report-into-hello-web-page"></a><span data-ttu-id="9d58d-197">Ten slotte Hallo rapport insluiten in Hallo webpagina</span><span class="sxs-lookup"><span data-stu-id="9d58d-197">Finally, embed hello report into hello web page</span></span>

<span data-ttu-id="9d58d-198">Voor het insluiten van onze rapport krijgen we Hallo-url en het rapport insluiten **id** met Hallo REST-API te volgen.</span><span class="sxs-lookup"><span data-stu-id="9d58d-198">For embedding our report, we must get hello embed url and report **id** using hello following REST API.</span></span>

<span data-ttu-id="9d58d-199">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="9d58d-199">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="9d58d-200">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="9d58d-200">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

<span data-ttu-id="9d58d-201">We kunt Hallo rapport insluiten in de web-app met behulp van Hallo eerdere app-token.</span><span class="sxs-lookup"><span data-stu-id="9d58d-201">We can embed hello report in our web app using hello previous app token.</span></span>
<span data-ttu-id="9d58d-202">Als we de volgende voorbeeldcode Hallo bekijkt, is Hallo voormalige onderdeel hetzelfde als het vorige voorbeeld Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="9d58d-202">If we look at hello next sample code, hello former part is hello same as hello previous example.</span></span> <span data-ttu-id="9d58d-203">In het laatste gedeelte hello, dit voorbeeld wordt Hallo **embedUrl** \(Zie vorige resultaat Hallo) in Hallo iframe en boekt Hallo app-token in Hallo iframe.</span><span class="sxs-lookup"><span data-stu-id="9d58d-203">In hello latter part, this sample shows hello **embedUrl** \(see hello previous result) in hello iframe, and is posting hello app token into hello iframe.</span></span>

> [!NOTE]
> <span data-ttu-id="9d58d-204">U moet toochange Hallo rapport id waarde tooone van uzelf.</span><span class="sxs-lookup"><span data-stu-id="9d58d-204">You'll need toochange hello report id value tooone of your own.</span></span> <span data-ttu-id="9d58d-205">Vervaldatum tooa bug in ons systeem inhoudsbeheer is Hallo iframe-code in Hallo-codevoorbeeld Lees ook letterlijk.</span><span class="sxs-lookup"><span data-stu-id="9d58d-205">Also, due tooa bug in our content management system, hello iframe tag in hello code sample is read literally.</span></span> <span data-ttu-id="9d58d-206">Verwijder Hallo beperkt tekst uit Hallo label als u kopieert en plakt deze voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="9d58d-206">Remove hello capped text from hello tag if you copy and paste this sample code.</span></span>

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

<span data-ttu-id="9d58d-207">En dit is het resultaat:</span><span class="sxs-lookup"><span data-stu-id="9d58d-207">And here's our result:</span></span>

![](media/power-bi-embedded-iframe/view-report.png)

<span data-ttu-id="9d58d-208">Op dit moment bevat Power BI Embedded alleen Hallo rapport in Hallo iframe.</span><span class="sxs-lookup"><span data-stu-id="9d58d-208">At this time, Power BI Embedded only shows hello report in hello iframe.</span></span> <span data-ttu-id="9d58d-209">Maar let op Hallo [Power BI Blog](https://powerbi.microsoft.com/blog/).</span><span class="sxs-lookup"><span data-stu-id="9d58d-209">But, keep an eye on hello [Power BI Blog](https://powerbi.microsoft.com/blog/).</span></span> <span data-ttu-id="9d58d-210">Toekomstige verbeteringen kunnen gebruiken om nieuwe clientzijde API's die worden laat het ons verzenden van informatie naar Hallo iframe, evenals informatie opvragen uit. Interessante spullen!</span><span class="sxs-lookup"><span data-stu-id="9d58d-210">Future improvements could use new client side APIs that will let us send information into hello iframe as well as get information out. Exciting stuff!</span></span>

## <a name="see-also"></a><span data-ttu-id="9d58d-211">Zie ook</span><span class="sxs-lookup"><span data-stu-id="9d58d-211">See also</span></span>
* [<span data-ttu-id="9d58d-212">Verifiëren en autoriseren in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="9d58d-212">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)

<span data-ttu-id="9d58d-213">Nog vragen?</span><span class="sxs-lookup"><span data-stu-id="9d58d-213">More questions?</span></span> [<span data-ttu-id="9d58d-214">Probeer Hallo Power BI-Community</span><span class="sxs-lookup"><span data-stu-id="9d58d-214">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

