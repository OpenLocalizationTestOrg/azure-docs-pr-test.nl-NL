---
title: Het gebruik van Power BI Embedded met REST | Microsoft Docs
description: 'Informatie over het gebruik van Power BI Embedded met REST '
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
ms.openlocfilehash: 31624b9d15772a4f08cf013ac713b3aa636acfca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-power-bi-embedded-with-rest"></a><span data-ttu-id="41d14-103">Het gebruik van Power BI Embedded met REST</span><span class="sxs-lookup"><span data-stu-id="41d14-103">How to use Power BI Embedded with REST</span></span>

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a><span data-ttu-id="41d14-104">Power BI Embedded: Wat is en wat het doet</span><span class="sxs-lookup"><span data-stu-id="41d14-104">Power BI Embedded: What it is and what it's for</span></span>

<span data-ttu-id="41d14-105">Een overzicht van Power BI Embedded wordt beschreven in de officiële [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), maar we even voordat we de details over het gebruik van deze met REST krijgen.</span><span class="sxs-lookup"><span data-stu-id="41d14-105">An overview of Power BI Embedded is described in the official [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), but let's take a quick look before we get into the details about using it with REST.</span></span>

<span data-ttu-id="41d14-106">Het is heel heel eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="41d14-106">It's quite simple, really.</span></span> <span data-ttu-id="41d14-107">u kunt de dynamische gegevensvisualisaties van gebruiken [Power BI](https://powerbi.microsoft.com) in uw eigen toepassing.</span><span class="sxs-lookup"><span data-stu-id="41d14-107">you may want to use the dynamic data visualizations of [Power BI](https://powerbi.microsoft.com) in your own application.</span></span>

<span data-ttu-id="41d14-108">De meeste aangepaste toepassingen vereist voor het leveren van de gegevens voor hun eigen klanten, niet noodzakelijkerwijs gebruikers in hun eigen organisatie.</span><span class="sxs-lookup"><span data-stu-id="41d14-108">Most custom applications need to deliver the data for their own customers, not necessarily users in their own organization.</span></span> <span data-ttu-id="41d14-109">Bijvoorbeeld, als u deel van de service voor bedrijf A en B bedrijf bieden, moeten gebruikers in bedrijf A alleen gegevens zien voor hun eigen bedrijf A. Dat wil zeggen, is de multi-tenancymodus nodig voor de bezorging.</span><span class="sxs-lookup"><span data-stu-id="41d14-109">For example, if you're delivering some service for both company A and company B, users in company A should only see data for their own company A. That is, the multi-tenancy is needed for the delivery.</span></span>

<span data-ttu-id="41d14-110">De aangepaste toepassing mogelijk worden biedt tevens een eigen verificatiemethoden zoals formulierverificatie, basic auth, enzovoort...</span><span class="sxs-lookup"><span data-stu-id="41d14-110">The custom application might also be offering its own authentication methods such as forms auth, basic auth, etc..</span></span> <span data-ttu-id="41d14-111">Vervolgens de insluiten oplossing moet werken samen met deze bestaande verificatiemethoden veilig.</span><span class="sxs-lookup"><span data-stu-id="41d14-111">Then, the embedding solution must collaborate with this existing authentication methods safely.</span></span> <span data-ttu-id="41d14-112">Het is ook nodig zijn voor gebruikers om te kunnen gebruikmaken van deze ISV-toepassingen zonder de extra aankoop of licenties van een Power BI-abonnement.</span><span class="sxs-lookup"><span data-stu-id="41d14-112">It's also necessary for users to be able to use those ISV applications without the extra purchase or licensing of a Power BI subscription.</span></span>

 <span data-ttu-id="41d14-113">**Power BI Embedded** is ontworpen voor nauwkeurig dit soort scenario's.</span><span class="sxs-lookup"><span data-stu-id="41d14-113">**Power BI Embedded** is designed for precisely these kinds of scenarios.</span></span> <span data-ttu-id="41d14-114">Dus nu dat we deze korte inleiding uit de weg hebben, gaan we krijgen tot de details van sommige</span><span class="sxs-lookup"><span data-stu-id="41d14-114">So, now that we have that quick introduction out of the way, let's get into some details</span></span>

<span data-ttu-id="41d14-115">U kunt de .NET \(C#) of Node.js-SDK voor uw toepassing met Power BI Embedded eenvoudig te maken.</span><span class="sxs-lookup"><span data-stu-id="41d14-115">You can use the .NET \(C#) or Node.js SDK, to easily build your application with Power BI Embedded.</span></span> <span data-ttu-id="41d14-116">Maar in dit artikel wordt uitgelegd over HTTP-stroom \(inclusief AuthN) van Power BI zonder SDK's.</span><span class="sxs-lookup"><span data-stu-id="41d14-116">But, in this article, we'll explain about HTTP flow \(incl. AuthN) of Power BI without SDKs.</span></span> <span data-ttu-id="41d14-117">Kennis van deze overdracht, kunt u uw toepassing bouwen **met elke programmeertaal**, en u kunt begrijpt diep de essentie van Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="41d14-117">Understanding this flow, you can build your application **with any programming language**, and you can understand deeply the essence of Power BI Embedded.</span></span>

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a><span data-ttu-id="41d14-118">Maken van Power BI-werkruimteverzameling en get-toegangssleutel \(inrichten)</span><span class="sxs-lookup"><span data-stu-id="41d14-118">Create Power BI workspace collection, and get access key \(Provisioning)</span></span>

<span data-ttu-id="41d14-119">Power BI Embedded is een van de Azure-services.</span><span class="sxs-lookup"><span data-stu-id="41d14-119">Power BI Embedded is one of the Azure services.</span></span> <span data-ttu-id="41d14-120">Alleen de ISV die gebruikmaakt van Azure Portal wordt in rekening gebracht voor gebruikskosten \(per uur gebruikerssessie), en de gebruiker die het rapport is niet in rekening gebracht of zelfs vereisen een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="41d14-120">Only the ISV who uses Azure Portal is charged for usage fees \(per hourly user session), and the user who views the report isn't charged or even require an Azure subscription.</span></span>
<span data-ttu-id="41d14-121">Voordat u begint onze toepassingsontwikkeling, maken we de **Power BI-werkruimteverzameling** met behulp van Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="41d14-121">Before starting our application development, we must create the **Power BI workspace collection** by using Azure Portal.</span></span>

<span data-ttu-id="41d14-122">Elke werkruimte van Power BI Embedded is de werkruimte voor elke klant (tenant) en we veel werkruimten in elke werkruimteverzameling kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="41d14-122">Each workspace of Power BI Embedded is the workspace for each customer (tenant), and we can add many workspaces in each workspace collection.</span></span> <span data-ttu-id="41d14-123">De dezelfde toegangssleutel wordt gebruikt in elke werkruimteverzameling.</span><span class="sxs-lookup"><span data-stu-id="41d14-123">The same access key is used in each workspace collection.</span></span> <span data-ttu-id="41d14-124">In de effect, de werkruimteverzameling is de beveiligingsgrens voor Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="41d14-124">In-effect, the workspace collection is the security boundary for Power BI Embedded.</span></span>

![](media/power-bi-embedded-iframe/create-workspace.png)

<span data-ttu-id="41d14-125">Wanneer we klaar bent met het maken van de werkruimteverzameling, kopieert u de toegangssleutel vanuit Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="41d14-125">When we finish creating the workspace collection, copy the access key from Azure Portal.</span></span>

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> <span data-ttu-id="41d14-126">We kunnen ook de werkruimteverzameling inrichten en verkrijgen toegangssleutel via REST-API.</span><span class="sxs-lookup"><span data-stu-id="41d14-126">We can also provision the workspace collection and get access key via REST API.</span></span> <span data-ttu-id="41d14-127">Zie voor meer informatie, [Power BI Resource Provider-API's](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="41d14-127">To learn more, see [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span></span>

## <a name="create-pbix-file-with-power-bi-desktop"></a><span data-ttu-id="41d14-128">Pbix-bestand maken met Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="41d14-128">Create .pbix file with Power BI Desktop</span></span>

<span data-ttu-id="41d14-129">Vervolgens maken we moet de verbinding van gegevens en rapporten worden ingesloten.</span><span class="sxs-lookup"><span data-stu-id="41d14-129">Next, we must create the data connection and reports to be embedded.</span></span>
<span data-ttu-id="41d14-130">Voor deze taak is er geen programmeren of de code.</span><span class="sxs-lookup"><span data-stu-id="41d14-130">For this task, there’s no programming or code.</span></span> <span data-ttu-id="41d14-131">We gebruiken gewoon Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="41d14-131">We just use Power BI Desktop.</span></span>
<span data-ttu-id="41d14-132">In dit artikel won't doorloopt u de details over het gebruik van Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="41d14-132">In this article, we won't go through the details about how to use Power BI Desktop.</span></span> <span data-ttu-id="41d14-133">Als u moet enkele hier, raadpleegt u [aan de slag met Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="41d14-133">If you need some help here, see [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span></span> <span data-ttu-id="41d14-134">In ons voorbeeld alleen gebruiken we de [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span><span class="sxs-lookup"><span data-stu-id="41d14-134">For our example, we'll just use the [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span></span>

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a><span data-ttu-id="41d14-135">Een Power BI-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="41d14-135">Create a Power BI workspace</span></span>

<span data-ttu-id="41d14-136">Nu dat het inrichten is voltooid, aan de slag van een klant-werkruimte maken in de werkruimteverzameling via REST-API's.</span><span class="sxs-lookup"><span data-stu-id="41d14-136">Now that the provisioning is all done, let’s get started creating a customer’s workspace in the workspace collection via REST APIs.</span></span> <span data-ttu-id="41d14-137">De volgende HTTP POST aanvragen (REST) maakt de nieuwe werkruimte in de werkruimteverzameling van onze bestaande.</span><span class="sxs-lookup"><span data-stu-id="41d14-137">The following HTTP POST Request (REST) is creating the new workspace in our existing workspace collection.</span></span> <span data-ttu-id="41d14-138">Dit is de [POST werkruimte API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="41d14-138">This is the [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span> <span data-ttu-id="41d14-139">In ons voorbeeld wordt de naam van de werkruimte-verzameling is **mypbiapp**.</span><span class="sxs-lookup"><span data-stu-id="41d14-139">In our example, the workspace collection name is **mypbiapp**.</span></span> <span data-ttu-id="41d14-140">We stelt u de toegangssleutel die we eerder hebt gekopieerd, als **App-sleutel**.</span><span class="sxs-lookup"><span data-stu-id="41d14-140">We just set the access key, which we previously copied, as **AppKey**.</span></span> <span data-ttu-id="41d14-141">Het is zeer eenvoudig verificatie.</span><span class="sxs-lookup"><span data-stu-id="41d14-141">It’s very simple authentication!</span></span>

<span data-ttu-id="41d14-142">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="41d14-142">**HTTP Request**</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="41d14-143">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="41d14-143">**HTTP Response**</span></span>

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

<span data-ttu-id="41d14-144">De geretourneerde **workspaceId** wordt gebruikt voor de volgende volgende API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="41d14-144">The returned **workspaceId** is used for the following subsequent API calls.</span></span> <span data-ttu-id="41d14-145">Onze toepassing moet deze waarde bewaren.</span><span class="sxs-lookup"><span data-stu-id="41d14-145">Our application must retain this value.</span></span>

## <a name="import-pbix-file-into-the-workspace"></a><span data-ttu-id="41d14-146">Pbix-bestand importeren in de werkruimte</span><span class="sxs-lookup"><span data-stu-id="41d14-146">Import .pbix file into the workspace</span></span>

<span data-ttu-id="41d14-147">Elk rapport in een werkruimte komt overeen met één Power BI Desktop-bestand met een gegevensset \(met inbegrip van instellingen voor gegevensbron).</span><span class="sxs-lookup"><span data-stu-id="41d14-147">Each report in a workspace corresponds to a single Power BI Desktop file with a dataset \(including datasource settings).</span></span> <span data-ttu-id="41d14-148">We kunt onze pbix-bestand importeren naar de werkruimte, zoals wordt weergegeven in de onderstaande code.</span><span class="sxs-lookup"><span data-stu-id="41d14-148">We can import our .pbix file to the workspace as shown in the code below.</span></span> <span data-ttu-id="41d14-149">Zoals u ziet, kunnen we het binaire bestand van pbix-bestand met MIME-multipart in HTTP-uploaden.</span><span class="sxs-lookup"><span data-stu-id="41d14-149">As you can see, we can upload the binary of .pbix file using MIME multipart in http.</span></span>

<span data-ttu-id="41d14-150">De uri-fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is de workspaceId en queryparameter **datasetDisplayName** is de gegevenssetnaam te maken.</span><span class="sxs-lookup"><span data-stu-id="41d14-150">The uri fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is the workspaceId, and query parameter **datasetDisplayName** is the dataset name to create.</span></span> <span data-ttu-id="41d14-151">De gemaakte gegevensset bevat alle gegevens gerelateerd artefacten in pbix-bestand bijvoorbeeld als de geïmporteerde gegevens, de pointer naar de gegevensbron, enzovoort...</span><span class="sxs-lookup"><span data-stu-id="41d14-151">The created dataset holds all data related artifacts in .pbix file such as imported data, the pointer to the data source, etc..</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{the content (binary) of .pbix file}
--A300testx--
```

<span data-ttu-id="41d14-152">Deze importtaak kan uitvoeren voor een tijdje.</span><span class="sxs-lookup"><span data-stu-id="41d14-152">This import task might run for a while.</span></span> <span data-ttu-id="41d14-153">Als u klaar kunt onze toepassing de status van de taak met id importeren vragen.</span><span class="sxs-lookup"><span data-stu-id="41d14-153">When complete, our application can ask the task status using import id.</span></span> <span data-ttu-id="41d14-154">In ons voorbeeld wordt de invoer-id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span><span class="sxs-lookup"><span data-stu-id="41d14-154">In our example, the import id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span></span>

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

<span data-ttu-id="41d14-155">De volgende vraagt de status van deze import-id:</span><span class="sxs-lookup"><span data-stu-id="41d14-155">The following is asking status using this import id:</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="41d14-156">Als de taak niet is voltooid, kan het HTTP-antwoord zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="41d14-156">If the task isn't complete, the HTTP response could be like this:</span></span>

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

<span data-ttu-id="41d14-157">Als de taak voltooid is, is het mogelijk dat het HTTP-antwoord meer als volgt:</span><span class="sxs-lookup"><span data-stu-id="41d14-157">If the task is complete, the HTTP response could be more like this:</span></span>

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

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a><span data-ttu-id="41d14-158">Gegevensbron connectiviteit \(en multi-tenancymodus van gegevens)</span><span class="sxs-lookup"><span data-stu-id="41d14-158">Data source connectivity \(and multi-tenancy of data)</span></span>

<span data-ttu-id="41d14-159">Terwijl bijna alle de artefacten in pbix-bestand in de werkruimte worden geïmporteerd, zijn de referenties voor gegevensbronnen niet.</span><span class="sxs-lookup"><span data-stu-id="41d14-159">While almost all of the artifacts in .pbix file are imported into our workspace, the  credentials for data sources are not.</span></span> <span data-ttu-id="41d14-160">Als gevolg hiervan, wanneer u **DirectQuery-modus**, het ingesloten rapport correct kan niet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="41d14-160">As a result, when using **DirectQuery mode**, the embedded report cannot be shown correctly.</span></span> <span data-ttu-id="41d14-161">Maar wanneer u **importmodus**, wordt het rapport met de bestaande geïmporteerde gegevens kunt bekijken.</span><span class="sxs-lookup"><span data-stu-id="41d14-161">But, when using **Import mode**, we can view the report using the existing imported data.</span></span> <span data-ttu-id="41d14-162">In dat geval moet er de referentie met de volgende stappen via REST-aanroepen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="41d14-162">In such a case, we must set the credential using the following steps via REST calls.</span></span>

<span data-ttu-id="41d14-163">Er moet eerst de gateway datasource ophalen.</span><span class="sxs-lookup"><span data-stu-id="41d14-163">First, we must get the gateway datasource.</span></span> <span data-ttu-id="41d14-164">We weten dat de dataset **id** is de eerder geretourneerde-id.</span><span class="sxs-lookup"><span data-stu-id="41d14-164">We know the dataset **id** is the previously returned id.</span></span>

<span data-ttu-id="41d14-165">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="41d14-165">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="41d14-166">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="41d14-166">**HTTP Response**</span></span>

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

<span data-ttu-id="41d14-167">De geretourneerde gateway-id en de gegevensbron-id \(Zie de vorige **gatewayId** en **id** in de geretourneerde resultatenset), kunnen we de referentie van deze gegevensbron als volgt wijzigen:</span><span class="sxs-lookup"><span data-stu-id="41d14-167">Using the returned gateway id and datasource id \(see the previous **gatewayId** and **id** in the returned result), we can change the credential of this datasource as follows:</span></span>

<span data-ttu-id="41d14-168">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="41d14-168">**HTTP Request**</span></span>

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

<span data-ttu-id="41d14-169">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="41d14-169">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

<span data-ttu-id="41d14-170">In productie, kunnen we ook de andere verbindingsreeks voor elke werkruimte met REST-API instellen.</span><span class="sxs-lookup"><span data-stu-id="41d14-170">In production, we can also set the different connection string for each workspace using REST API.</span></span> <span data-ttu-id="41d14-171">\(Internet Explorer, we kunt scheidt u de database voor elk klanten.)</span><span class="sxs-lookup"><span data-stu-id="41d14-171">\(i.e, we can separate the database for each customers.)</span></span>

<span data-ttu-id="41d14-172">Het volgende is het wijzigen van de verbindingsreeks van de gegevensbron via REST.</span><span class="sxs-lookup"><span data-stu-id="41d14-172">The following is changing the connection string of datasource via REST.</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

<span data-ttu-id="41d14-173">Of we beveiliging op rijniveau in Power BI Embedded kunnen gebruiken en we kunnen de gegevens voor elke gebruikers in een rapport scheiden.</span><span class="sxs-lookup"><span data-stu-id="41d14-173">Or, we can use Row Level Security in Power BI Embedded and we can separate the data for each users in one report.</span></span> <span data-ttu-id="41d14-174">We kunnen as a Result, elke klant rapport met dezelfde pbix inrichten \(gebruikersinterface, enz.) en andere gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="41d14-174">As a result, we can provision each customer report with same .pbix \(UI, etc.) and different data sources.</span></span>

> [!NOTE]
> <span data-ttu-id="41d14-175">Als u **importmodus** in plaats van **DirectQuery-modus**, er is geen manier om te vernieuwen modellen via API.</span><span class="sxs-lookup"><span data-stu-id="41d14-175">If you’re using **Import mode** instead of **DirectQuery mode**, there’s no way to refresh models via API.</span></span> <span data-ttu-id="41d14-176">En on-premises gegevensbronnen via Power BI gateway nog wordt niet ondersteund in Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="41d14-176">And, on-premises datasources through Power BI gateway isn't yet supported in Power BI Embedded.</span></span> <span data-ttu-id="41d14-177">Echter zeker wilt u het oog houden de [Power BI-blog](https://powerbi.microsoft.com/blog/) voor wat is er nieuw en wat er nieuw in toekomstige releases.</span><span class="sxs-lookup"><span data-stu-id="41d14-177">However, you'll really want to keep an eye on the [Power BI blog](https://powerbi.microsoft.com/blog/) for what's new and what's coming in future releases.</span></span>

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a><span data-ttu-id="41d14-178">Verificatie en die als host fungeert voor (insluiten) rapporten in onze webpagina</span><span class="sxs-lookup"><span data-stu-id="41d14-178">Authentication and hosting (embedding) reports in our web page</span></span>

<span data-ttu-id="41d14-179">In de vorige REST-API, gebruiken we de toegangssleutel **App-sleutel** zelf als de autorisatie-header.</span><span class="sxs-lookup"><span data-stu-id="41d14-179">In the previous REST API, we can use the access key **AppKey** itself as the authorization header.</span></span> <span data-ttu-id="41d14-180">Het is veilig omdat deze aanroepen kunnen worden verwerkt op de server back-end.</span><span class="sxs-lookup"><span data-stu-id="41d14-180">Because these calls can be handled on the backend server side, it's safe.</span></span>

<span data-ttu-id="41d14-181">Maar als we het rapport in onze webpagina insluiten, dit soort informatie over beveiliging zou worden afgehandeld met JavaScript \(frontend).</span><span class="sxs-lookup"><span data-stu-id="41d14-181">But, when we embed the report in our web page, this kind of security information would be handled using JavaScript \(frontend).</span></span> <span data-ttu-id="41d14-182">De waarde van de autorisatie-header moet vervolgens worden beveiligd.</span><span class="sxs-lookup"><span data-stu-id="41d14-182">Then the authorization header value must be secured.</span></span> <span data-ttu-id="41d14-183">Als onze toegangssleutel wordt gedetecteerd door een kwaadwillende gebruiker of schadelijke code, kunnen ze geen bewerkingen met deze sleutel aanroepen.</span><span class="sxs-lookup"><span data-stu-id="41d14-183">If our access key is discovered by a malicious user or malicious code, they can call any operations using this key.</span></span>

<span data-ttu-id="41d14-184">Wanneer we het rapport in onze webpagina insluiten, we het berekende token moet gebruiken in plaats van de toegangssleutel **App-sleutel**.</span><span class="sxs-lookup"><span data-stu-id="41d14-184">When we embed the report in our web page, we must use the computed token instead of access key **AppKey**.</span></span> <span data-ttu-id="41d14-185">Onze toepassing moet maken OAuth Json Web Token \(JWT) die bestaat uit de claims en de berekende digitale handtekening.</span><span class="sxs-lookup"><span data-stu-id="41d14-185">Our application must create the OAuth Json Web Token \(JWT) which consists of the claims and the computed digital signature.</span></span> <span data-ttu-id="41d14-186">Zoals hieronder weergegeven, is deze OAuth JWT-tokens punt gescheiden gecodeerde tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="41d14-186">As illustrated below, this OAuth JWT is dot-delimited encoded string tokens.</span></span>

![](media/power-bi-embedded-iframe/oauth-jwt.png)

<span data-ttu-id="41d14-187">Er moet eerst de invoerwaarde is ondertekend later voorbereiden.</span><span class="sxs-lookup"><span data-stu-id="41d14-187">First, we must prepare the input value, which is signed later.</span></span> <span data-ttu-id="41d14-188">Deze waarde is de tekenreeks base64-gecodeerd url (rfc4648) van de volgende json en deze worden gescheiden door het punt \(.) teken.</span><span class="sxs-lookup"><span data-stu-id="41d14-188">This value is the base64 url encoded (rfc4648) string of the following json, and these are delimited by the dot \(.) character.</span></span> <span data-ttu-id="41d14-189">Later, wordt uitgelegd hoe u de id van het rapport niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="41d14-189">Later, we'll explain how to get the report id.</span></span>

> [!NOTE]
> <span data-ttu-id="41d14-190">Als we rij Level Security (RLS) gebruiken met Power BI Embedded willen, er moet ook opgeven **gebruikersnaam** en **rollen** in de claims.</span><span class="sxs-lookup"><span data-stu-id="41d14-190">If we want to use Row Level Security (RLS) with Power BI Embedded, we must also specify **username** and **roles** in the claims.</span></span>

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

<span data-ttu-id="41d14-191">Vervolgens maken we de met base64 gecodeerde tekenreeks van HMAC \(de handtekening) met SHA256-algoritme.</span><span class="sxs-lookup"><span data-stu-id="41d14-191">Next, we must create the base64 encoded string of HMAC \(the signature) with SHA256 algorithm.</span></span> <span data-ttu-id="41d14-192">Deze ondertekende invoerwaarde is de vorige tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="41d14-192">This signed input value is the previous string.</span></span>

<span data-ttu-id="41d14-193">Laatste combineren we de waarde en handtekening invoerreeks periode met \(.) teken.</span><span class="sxs-lookup"><span data-stu-id="41d14-193">Last, we must combine the input value and signature string using period \(.) character.</span></span> <span data-ttu-id="41d14-194">De voltooide tekenreeks is de app-token voor het rapport insluiten.</span><span class="sxs-lookup"><span data-stu-id="41d14-194">The completed string is the app token for the report embedding.</span></span> <span data-ttu-id="41d14-195">Zelfs als de app-token wordt gedetecteerd door een kwaadwillende gebruiker, kunnen ze de oorspronkelijke toegangssleutel niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="41d14-195">Even if the app token is discovered by a malicious user, they cannot get the original access key.</span></span> <span data-ttu-id="41d14-196">Deze app-token verloopt snel.</span><span class="sxs-lookup"><span data-stu-id="41d14-196">This app token will expire quickly.</span></span>

<span data-ttu-id="41d14-197">Hier volgt een voorbeeld van een PHP voor deze stappen:</span><span class="sxs-lookup"><span data-stu-id="41d14-197">Here's a PHP example for these steps:</span></span>

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

// 4. show result (which is the apptoken)
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

## <a name="finally-embed-the-report-into-the-web-page"></a><span data-ttu-id="41d14-198">Ten slotte wordt het rapport insluiten in de webpagina</span><span class="sxs-lookup"><span data-stu-id="41d14-198">Finally, embed the report into the web page</span></span>

<span data-ttu-id="41d14-199">Voor het insluiten van onze rapport moet krijgen we de insluiten-url en het rapport **id** met de volgende REST-API.</span><span class="sxs-lookup"><span data-stu-id="41d14-199">For embedding our report, we must get the embed url and report **id** using the following REST API.</span></span>

<span data-ttu-id="41d14-200">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="41d14-200">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="41d14-201">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="41d14-201">**HTTP Response**</span></span>

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

<span data-ttu-id="41d14-202">We kunnen het rapport insluiten in de web-app met behulp van het vorige app-token.</span><span class="sxs-lookup"><span data-stu-id="41d14-202">We can embed the report in our web app using the previous app token.</span></span>
<span data-ttu-id="41d14-203">Als we de volgende voorbeeldcode bekijkt, wordt het vorige gedeelte is hetzelfde als het vorige voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="41d14-203">If we look at the next sample code, the former part is the same as the previous example.</span></span> <span data-ttu-id="41d14-204">In het laatste deel dit voorbeeld wordt de **embedUrl** \(het vorige resultaat te bekijken) in de iframe en wordt het app-token boeken in de iframe.</span><span class="sxs-lookup"><span data-stu-id="41d14-204">In the latter part, this sample shows the **embedUrl** \(see the previous result) in the iframe, and is posting the app token into the iframe.</span></span>

> [!NOTE]
> <span data-ttu-id="41d14-205">U moet de id-waarde van het rapport wijzigen in een eigen.</span><span class="sxs-lookup"><span data-stu-id="41d14-205">You'll need to change the report id value to one of your own.</span></span> <span data-ttu-id="41d14-206">Vanwege een fout in ons systeem inhoudsbeheer is de iframe-code in het voorbeeld Lees ook letterlijk.</span><span class="sxs-lookup"><span data-stu-id="41d14-206">Also, due to a bug in our content management system, the iframe tag in the code sample is read literally.</span></span> <span data-ttu-id="41d14-207">Verwijder de capped tekst uit het label als u kopieert en plakt deze voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="41d14-207">Remove the capped text from the tag if you copy and paste this sample code.</span></span>

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

<span data-ttu-id="41d14-208">En dit is het resultaat:</span><span class="sxs-lookup"><span data-stu-id="41d14-208">And here's our result:</span></span>

![](media/power-bi-embedded-iframe/view-report.png)

<span data-ttu-id="41d14-209">Op dit moment Power BI Embedded alleen het rapport weergegeven in de iframe.</span><span class="sxs-lookup"><span data-stu-id="41d14-209">At this time, Power BI Embedded only shows the report in the iframe.</span></span> <span data-ttu-id="41d14-210">Maar let op de [Power BI Blog](https://powerbi.microsoft.com/blog/).</span><span class="sxs-lookup"><span data-stu-id="41d14-210">But, keep an eye on the [Power BI Blog](https://powerbi.microsoft.com/blog/).</span></span> <span data-ttu-id="41d14-211">Toekomstige verbeteringen kunnen gebruiken om nieuwe clientzijde API's die worden laat het ons informatie in de iframe verzenden, evenals informatie opvragen uit.</span><span class="sxs-lookup"><span data-stu-id="41d14-211">Future improvements could use new client side APIs that will let us send information into the iframe as well as get information out.</span></span> <span data-ttu-id="41d14-212">Interessante spullen!</span><span class="sxs-lookup"><span data-stu-id="41d14-212">Exciting stuff!</span></span>

## <a name="see-also"></a><span data-ttu-id="41d14-213">Zie ook</span><span class="sxs-lookup"><span data-stu-id="41d14-213">See also</span></span>
* [<span data-ttu-id="41d14-214">Verifiëren en autoriseren in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="41d14-214">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)

<span data-ttu-id="41d14-215">Nog vragen?</span><span class="sxs-lookup"><span data-stu-id="41d14-215">More questions?</span></span> [<span data-ttu-id="41d14-216">Probeer de Power BI-community</span><span class="sxs-lookup"><span data-stu-id="41d14-216">Try the Power BI Community</span></span>](http://community.powerbi.com/)

