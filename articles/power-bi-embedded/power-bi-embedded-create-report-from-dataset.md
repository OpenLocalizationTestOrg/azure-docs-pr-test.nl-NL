---
title: Een nieuw rapport maken uit een gegevensset in Azure Power BI Embedded | Microsoft Docs
description: Power BI Embedded rapporten kunnen nu worden gemaakt uit een gegevensset in uw eigen toepassing.
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 457f53aa76059dbb2faed6b264102f1f59b9918a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="106f2-103">Een nieuw rapport maken uit een gegevensset in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="106f2-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="106f2-104">Power BI Embedded rapporten kunnen nu worden gemaakt uit een gegevensset in uw eigen toepassing.</span><span class="sxs-lookup"><span data-stu-id="106f2-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="106f2-105">De verificatiemethode is vergelijkbaar met dat van het rapport insluiten.</span><span class="sxs-lookup"><span data-stu-id="106f2-105">The authentication method is similar to that of report embed.</span></span> <span data-ttu-id="106f2-106">Deze is gebaseerd op toegangstokens die specifiek voor een gegevensset zijn.</span><span class="sxs-lookup"><span data-stu-id="106f2-106">It is based on access tokens that are specific to a dataset.</span></span> <span data-ttu-id="106f2-107">Gebruikt voor PowerBI.com tokens worden uitgegeven door Azure Active Directory (AAD) en Power BI Embedded tokens worden uitgegeven door uw eigen service.</span><span class="sxs-lookup"><span data-stu-id="106f2-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="106f2-108">Wanneer een ingesloten rapport, de uitgegeven tokens uitvoerbestanden zijn voor een bepaalde gegevensset.</span><span class="sxs-lookup"><span data-stu-id="106f2-108">When createing an Embedded report, the tokens issued are for a specific dataset.</span></span> <span data-ttu-id="106f2-109">Tokens moeten worden gekoppeld aan de URL van de insluiten op hetzelfde element zodat elk een unieke token heeft.</span><span class="sxs-lookup"><span data-stu-id="106f2-109">Tokens should be associated with the embed URL on the same element to ensure each has a unique token.</span></span> <span data-ttu-id="106f2-110">Om te kunnen maken van een rapport ingesloten *Dataset.Read en Workspace.Report.Create* scopes moeten worden opgegeven in het toegangstoken.</span><span class="sxs-lookup"><span data-stu-id="106f2-110">In order to create an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in the access token.</span></span>

## <a name="create-access-token-needed-to-create-new-report"></a><span data-ttu-id="106f2-111">Toegangstoken voor het maken van nieuw rapport maken</span><span class="sxs-lookup"><span data-stu-id="106f2-111">Create access token needed to create new report</span></span>

<span data-ttu-id="106f2-112">Maakt gebruik van Power BI Embedded insluiten token, JSON Web Tokens die HMAC zijn ondertekend.</span><span class="sxs-lookup"><span data-stu-id="106f2-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="106f2-113">De tokens zijn ondertekend door de toegangssleutel van uw Azure Power BI Embedded werkruimteverzameling.</span><span class="sxs-lookup"><span data-stu-id="106f2-113">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="106f2-114">Sluit tokens, standaard, alleen-lezen toegang aan een rapport insluiten in een toepassing worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="106f2-114">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span></span> <span data-ttu-id="106f2-115">Sluit tokens worden uitgegeven voor een specifiek rapport en moeten worden gekoppeld aan een URL insluiten.</span><span class="sxs-lookup"><span data-stu-id="106f2-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="106f2-116">Toegangstokens moeten worden gemaakt op de server, zoals de toegangssleutels voor het teken/versleutelen van de tokens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="106f2-116">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span></span> <span data-ttu-id="106f2-117">Zie voor meer informatie over het maken van een toegangstoken [Authenticating en autoriseren met Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="106f2-117">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="106f2-118">U kunt ook bekijken de [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methode.</span><span class="sxs-lookup"><span data-stu-id="106f2-118">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="106f2-119">Hier volgt een voorbeeld van hoe dit eruitziet met de .NET SDK voor Power BI.</span><span class="sxs-lookup"><span data-stu-id="106f2-119">Here is an example of what this would look like using the .NET SDK for Power BI.</span></span>

<span data-ttu-id="106f2-120">In dit voorbeeld hebben we onze gegevensset-id die we willen maken het nieuwe rapport op.</span><span class="sxs-lookup"><span data-stu-id="106f2-120">In this example, we have our dataset id that we want to creat the new report on.</span></span> <span data-ttu-id="106f2-121">Er moet ook de scopes voor toevoegen *Dataset.Read en Workspace.Report.Create*.</span><span class="sxs-lookup"><span data-stu-id="106f2-121">We also need to add the scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="106f2-122">De *PowerBIToken klasse* vereist dat u installeert de [Power BI Core NuGut pakket](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="106f2-122">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="106f2-123">**NuGet-pakket installeren**</span><span class="sxs-lookup"><span data-stu-id="106f2-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="106f2-124">**C#-code**</span><span class="sxs-lookup"><span data-stu-id="106f2-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="106f2-125">Maak een nieuwe leeg rapport</span><span class="sxs-lookup"><span data-stu-id="106f2-125">Create a new blank report</span></span>

<span data-ttu-id="106f2-126">Om een nieuw rapport maakt, moet de configuratie maken worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="106f2-126">In order to create a new report, the create configuration should be provided.</span></span> <span data-ttu-id="106f2-127">Dit dient het toegangstoken, de embedURL en de datasetID die we willen maken van het rapport op basis van omvatten.</span><span class="sxs-lookup"><span data-stu-id="106f2-127">This should include the access token, the embedURL and the datasetID that we want to create the report against.</span></span> <span data-ttu-id="106f2-128">Dit vereist dat u het nuget installeert [Power BI JavaScript pakket](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="106f2-128">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="106f2-129">De embedUrl worden alleen https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="106f2-129">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="106f2-130">U kunt de [JavaScript rapport insluiten voorbeeld](https://microsoft.github.io/PowerBI-JavaScript/demo/) om functionaliteit te testen.</span><span class="sxs-lookup"><span data-stu-id="106f2-130">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span></span> <span data-ttu-id="106f2-131">Het biedt ook voorbeelden van code voor de verschillende bewerkingen die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="106f2-131">It also gives code examples for the different operations that are available.</span></span>

<span data-ttu-id="106f2-132">**NuGet-pakket installeren**</span><span class="sxs-lookup"><span data-stu-id="106f2-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="106f2-133">**JavaScript-code**</span><span class="sxs-lookup"><span data-stu-id="106f2-133">**JavaScript code**</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

<span data-ttu-id="106f2-134">Het aanroepen van *powerbi.createReport()* maakt een leeg canvas in de bewerkingsmodus voorkomen binnen de *div* element.</span><span class="sxs-lookup"><span data-stu-id="106f2-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within the *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="106f2-135">Nieuwe rapporten opslaan</span><span class="sxs-lookup"><span data-stu-id="106f2-135">Save new reports</span></span>

<span data-ttu-id="106f2-136">Het rapport niet daadwerkelijk gemaakt totdat u de **opslaan als** bewerking.</span><span class="sxs-lookup"><span data-stu-id="106f2-136">The report will not actually be created until you call the **save as** operation.</span></span> <span data-ttu-id="106f2-137">Dit kan worden gedaan vanuit het bestandsmenu of vanuit JavaScript.</span><span class="sxs-lookup"><span data-stu-id="106f2-137">This can be done from file menu or from JavaScript.</span></span>

```
 // Get a reference to the embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> <span data-ttu-id="106f2-138">Een nieuw rapport wordt gemaakt nadat **opslaan als** wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="106f2-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="106f2-139">Nadat u hebt opgeslagen, wordt het canvas de dataset nog steeds weergegeven in de bewerkingsmodus en niet in het rapport.</span><span class="sxs-lookup"><span data-stu-id="106f2-139">After you save, the canvas will still show the dataset in edit mode and not the report.</span></span> <span data-ttu-id="106f2-140">U moet het nieuwe rapport laden net als andere rapporten.</span><span class="sxs-lookup"><span data-stu-id="106f2-140">You will need to reload the new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-the-new-report"></a><span data-ttu-id="106f2-141">Het nieuwe rapport laden</span><span class="sxs-lookup"><span data-stu-id="106f2-141">Load the new report</span></span>

<span data-ttu-id="106f2-142">Om te communiceren met het nieuwe rapport moet u dit op dezelfde manier als de toepassing wordt ingesloten een reguliere rapport insluiten wil zeggen, een nieuw token specifiek voor het nieuwe rapport moet worden verstrekt en vervolgens de insluiten-methode aanroepen.</span><span class="sxs-lookup"><span data-stu-id="106f2-142">In order to interact with the new report you need to embed it in the same way the application embeds a regular report, meaning, a new token must be issued specifically for the new report and then call the embed method.</span></span>

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="automate-save-and-load-of-a-new-report-using-the-saved-event"></a><span data-ttu-id="106f2-143">Automatiseren opslaan en laden van een nieuw rapport met de 'opgeslagen' gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="106f2-143">Automate save and load of a new report using the "saved" event</span></span>

<span data-ttu-id="106f2-144">In volgorde voor het automatiseren van 'opslaan als' en vervolgens bij het laden van het nieuwe rapport kunt u het gebruik van de gebeurtenis 'opgeslagen'.</span><span class="sxs-lookup"><span data-stu-id="106f2-144">In order to automate the process of "save as" and then loading the new report you can make use of the "saved" Event.</span></span> <span data-ttu-id="106f2-145">Deze gebeurtenis wordt geactiveerd wanneer de opslagbewerking voltooid is en retourneert een Json-object met de nieuwe reportId, de naam van rapport, de oude reportId (als er een) en als de bewerking saveAs is of opslaan.</span><span class="sxs-lookup"><span data-stu-id="106f2-145">This event is fired when the save operation is complete and it returns a Json object containing the new reportId, report name, the old reportId(if there was one) and if the operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="106f2-146">Voor het automatiseren van het proces dat u op de 'opgeslagen' gebeurtenis luisteren kunt duren voordat de nieuwe reportId, maken van het nieuwe token en het nieuwe rapport insluiten met deze.</span><span class="sxs-lookup"><span data-stu-id="106f2-146">To Automate the process you can listen on the "saved" event, take the new reportId, create the new token and embed the new report with it.</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints to Log window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that the application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide the wanted scopes*/);
        
        
    var embedConfiguration = {
        accessToken: newToken ,
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: newReportId,
    };

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
       
   // report.off removes a given event handler if it exists.
   report.off("saved");
    });
```

## <a name="see-also"></a><span data-ttu-id="106f2-147">Zie ook</span><span class="sxs-lookup"><span data-stu-id="106f2-147">See also</span></span>

[<span data-ttu-id="106f2-148">Aan de slag met het voorbeeld</span><span class="sxs-lookup"><span data-stu-id="106f2-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="106f2-149">Rapporten opslaan</span><span class="sxs-lookup"><span data-stu-id="106f2-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
[<span data-ttu-id="106f2-150">Een rapport insluiten</span><span class="sxs-lookup"><span data-stu-id="106f2-150">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="106f2-151">Verifiëren en autoriseren in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="106f2-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="106f2-152">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="106f2-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="106f2-153">Voorbeeld van ingesloten JavaScript</span><span class="sxs-lookup"><span data-stu-id="106f2-153">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="106f2-154">Power BI Core NuGut-pakket</span><span class="sxs-lookup"><span data-stu-id="106f2-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="106f2-155">Power BI JavaScript-pakket</span><span class="sxs-lookup"><span data-stu-id="106f2-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="106f2-156">Nog vragen?</span><span class="sxs-lookup"><span data-stu-id="106f2-156">More questions?</span></span> [<span data-ttu-id="106f2-157">Probeer de Power BI-community</span><span class="sxs-lookup"><span data-stu-id="106f2-157">Try the Power BI Community</span></span>](http://community.powerbi.com/)