---
title: een nieuw rapport uit een gegevensset in Azure Power BI Embedded aaaCreate | Microsoft Docs
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
ms.openlocfilehash: 41a0a52e4c833313f495bb5ff14749203fef9b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="96640-103">Een nieuw rapport maken uit een gegevensset in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="96640-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="96640-104">Power BI Embedded rapporten kunnen nu worden gemaakt uit een gegevensset in uw eigen toepassing.</span><span class="sxs-lookup"><span data-stu-id="96640-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="96640-105">Hallo verificatiemethode is vergelijkbaar toothat van rapport insluiten.</span><span class="sxs-lookup"><span data-stu-id="96640-105">hello authentication method is similar toothat of report embed.</span></span> <span data-ttu-id="96640-106">Deze is gebaseerd op toegangstokens die specifieke tooa gegevensset zijn.</span><span class="sxs-lookup"><span data-stu-id="96640-106">It is based on access tokens that are specific tooa dataset.</span></span> <span data-ttu-id="96640-107">Gebruikt voor PowerBI.com tokens worden uitgegeven door Azure Active Directory (AAD) en Power BI Embedded tokens worden uitgegeven door uw eigen service.</span><span class="sxs-lookup"><span data-stu-id="96640-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="96640-108">Wanneer u een rapport ingesloten uitvoerbestanden Hallo zijn uitgegeven tokens voor een bepaalde gegevensset.</span><span class="sxs-lookup"><span data-stu-id="96640-108">When createing an Embedded report, hello tokens issued are for a specific dataset.</span></span> <span data-ttu-id="96640-109">Tokens moeten worden gekoppeld met de Hallo insluiten URL op Hallo dezelfde element tooensure elke heeft een unieke token.</span><span class="sxs-lookup"><span data-stu-id="96640-109">Tokens should be associated with hello embed URL on hello same element tooensure each has a unique token.</span></span> <span data-ttu-id="96640-110">In volgorde toocreate een rapport ingesloten *Dataset.Read en Workspace.Report.Create* scopes in Hallo toegangstoken moeten worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="96640-110">In order toocreate an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in hello access token.</span></span>

## <a name="create-access-token-needed-toocreate-new-report"></a><span data-ttu-id="96640-111">Access token benodigde toocreate nieuw rapport maken</span><span class="sxs-lookup"><span data-stu-id="96640-111">Create access token needed toocreate new report</span></span>

<span data-ttu-id="96640-112">Maakt gebruik van Power BI Embedded insluiten token, JSON Web Tokens die HMAC zijn ondertekend.</span><span class="sxs-lookup"><span data-stu-id="96640-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="96640-113">Hallo tokens zijn ondertekend door de toegangssleutel Hallo van uw Azure Power BI Embedded werkruimteverzameling.</span><span class="sxs-lookup"><span data-stu-id="96640-113">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="96640-114">Sluit tokens, standaard, zijn gebruikte tooprovide lezen alleen toegang tot tooa rapport tooembed in een toepassing.</span><span class="sxs-lookup"><span data-stu-id="96640-114">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="96640-115">Sluit tokens worden uitgegeven voor een specifiek rapport en moeten worden gekoppeld aan een URL insluiten.</span><span class="sxs-lookup"><span data-stu-id="96640-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="96640-116">Toegangstokens moeten worden gemaakt op de server Hallo Hallo toegangstoetsen zijn gebruikte toosign/versleutelen Hallo-tokens.</span><span class="sxs-lookup"><span data-stu-id="96640-116">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="96640-117">Voor meer informatie over een toegangstoken toocreate Zie [Authenticating en autoriseren met Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="96640-117">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="96640-118">U kunt ook bekijken Hallo [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methode.</span><span class="sxs-lookup"><span data-stu-id="96640-118">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="96640-119">Hier volgt een voorbeeld van hoe dit eruitziet Hallo .NET SDK gebruiken voor Power BI.</span><span class="sxs-lookup"><span data-stu-id="96640-119">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="96640-120">In dit voorbeeld hebben we onze gegevensset-id die we willen toocreat Hallo nieuw rapport op.</span><span class="sxs-lookup"><span data-stu-id="96640-120">In this example, we have our dataset id that we want toocreat hello new report on.</span></span> <span data-ttu-id="96640-121">Er moet ook tooadd Hallo bereiken voor *Dataset.Read en Workspace.Report.Create*.</span><span class="sxs-lookup"><span data-stu-id="96640-121">We also need tooadd hello scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="96640-122">Hallo *PowerBIToken klasse* vereist dat u Hallo installeert [Power BI Core NuGut pakket](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="96640-122">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="96640-123">**NuGet-pakket installeren**</span><span class="sxs-lookup"><span data-stu-id="96640-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="96640-124">**C#-code**</span><span class="sxs-lookup"><span data-stu-id="96640-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="96640-125">Maak een nieuwe leeg rapport</span><span class="sxs-lookup"><span data-stu-id="96640-125">Create a new blank report</span></span>

<span data-ttu-id="96640-126">Maak in volgorde toocreate een nieuw rapport, Hallo configuratie moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="96640-126">In order toocreate a new report, hello create configuration should be provided.</span></span> <span data-ttu-id="96640-127">Dit dient toegangstoken hello, Hallo embedURL en Hallo datasetID die we toocreate Hallo rapport op basis van willen omvatten.</span><span class="sxs-lookup"><span data-stu-id="96640-127">This should include hello access token, hello embedURL and hello datasetID that we want toocreate hello report against.</span></span> <span data-ttu-id="96640-128">Dit vereist dat u Hallo nuget installeert [Power BI JavaScript pakket](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="96640-128">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="96640-129">Hallo embedUrl worden alleen https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="96640-129">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="96640-130">U kunt Hallo [JavaScript rapport insluiten voorbeeld](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest-functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="96640-130">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="96640-131">Het biedt ook voorbeelden van code voor verschillende bewerkingen Hallo die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="96640-131">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="96640-132">**NuGet-pakket installeren**</span><span class="sxs-lookup"><span data-stu-id="96640-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="96640-133">**JavaScript-code**</span><span class="sxs-lookup"><span data-stu-id="96640-133">**JavaScript code**</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

<span data-ttu-id="96640-134">Het aanroepen van *powerbi.createReport()* maakt een leeg canvas in de bewerkingsmodus voorkomen binnen de Hallo *div* element.</span><span class="sxs-lookup"><span data-stu-id="96640-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within hello *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="96640-135">Nieuwe rapporten opslaan</span><span class="sxs-lookup"><span data-stu-id="96640-135">Save new reports</span></span>

<span data-ttu-id="96640-136">Hallo-rapport niet daadwerkelijk gemaakt totdat u Hallo aanroepen **opslaan als** bewerking.</span><span class="sxs-lookup"><span data-stu-id="96640-136">hello report will not actually be created until you call hello **save as** operation.</span></span> <span data-ttu-id="96640-137">Dit kan worden gedaan vanuit het bestandsmenu of vanuit JavaScript.</span><span class="sxs-lookup"><span data-stu-id="96640-137">This can be done from file menu or from JavaScript.</span></span>

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> <span data-ttu-id="96640-138">Een nieuw rapport wordt gemaakt nadat **opslaan als** wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="96640-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="96640-139">Nadat u hebt opgeslagen, wordt Hallo canvas Hallo gegevensset nog steeds weergegeven in de modus en niet Hallo rapport bewerken.</span><span class="sxs-lookup"><span data-stu-id="96640-139">After you save, hello canvas will still show hello dataset in edit mode and not hello report.</span></span> <span data-ttu-id="96640-140">U moet tooreload Hallo nieuw rapport net als andere rapporten.</span><span class="sxs-lookup"><span data-stu-id="96640-140">You will need tooreload hello new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a><span data-ttu-id="96640-141">Hallo nieuw rapport laden</span><span class="sxs-lookup"><span data-stu-id="96640-141">Load hello new report</span></span>

<span data-ttu-id="96640-142">In de volgorde toointeract met het nieuwe rapport Hallo moet u tooembed in dezelfde manier Hallo toepassing wordt ingesloten een reguliere rapport, betekenis, een nieuw token moet worden verstrekt specifiek voor het nieuwe rapport Hallo Hallo en klik vervolgens op Hallo aanroep van methode insluiten.</span><span class="sxs-lookup"><span data-stu-id="96640-142">In order toointeract with hello new report you need tooembed it in hello same way hello application embeds a regular report, meaning, a new token must be issued specifically for hello new report and then call hello embed method.</span></span>

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a><span data-ttu-id="96640-143">Automatiseren opslaan en laden van een nieuw rapport met Hallo 'opgeslagen' gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="96640-143">Automate save and load of a new report using hello "saved" event</span></span>

<span data-ttu-id="96640-144">In de volgorde tooautomate proces 'opslaan als' hello en vervolgens bij het laden van Hallo nieuw rapport kunt u het gebruik van Hallo 'opgeslagen' gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="96640-144">In order tooautomate hello process of "save as" and then loading hello new report you can make use of hello "saved" Event.</span></span> <span data-ttu-id="96640-145">Deze gebeurtenis wordt geactiveerd wanneer Hallo opslagbewerking voltooid is en een Json-object met de nieuwe reportId hello, rapportnaam, oude reportId Hallo wordt (als er een) en als Hallo bewerking saveAs is of opslaan.</span><span class="sxs-lookup"><span data-stu-id="96640-145">This event is fired when hello save operation is complete and it returns a Json object containing hello new reportId, report name, hello old reportId(if there was one) and if hello operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="96640-146">tooAutomate hello proces u kunt luisteren op Hallo 'opgeslagen' gebeurtenis, nieuwe reportId hello, Hallo nieuw token maken en Hallo nieuw rapport insluiten met deze.</span><span class="sxs-lookup"><span data-stu-id="96640-146">tooAutomate hello process you can listen on hello "saved" event, take hello new reportId, create hello new token and embed hello new report with it.</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints tooLog window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that hello application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide hello wanted scopes*/);
        
        
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

## <a name="see-also"></a><span data-ttu-id="96640-147">Zie ook</span><span class="sxs-lookup"><span data-stu-id="96640-147">See also</span></span>

[<span data-ttu-id="96640-148">Aan de slag met het voorbeeld</span><span class="sxs-lookup"><span data-stu-id="96640-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="96640-149">Rapporten opslaan</span><span class="sxs-lookup"><span data-stu-id="96640-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
[<span data-ttu-id="96640-150">Een rapport insluiten</span><span class="sxs-lookup"><span data-stu-id="96640-150">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="96640-151">Verifiëren en autoriseren in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="96640-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="96640-152">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="96640-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="96640-153">Voorbeeld van ingesloten JavaScript</span><span class="sxs-lookup"><span data-stu-id="96640-153">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="96640-154">Power BI Core NuGut-pakket</span><span class="sxs-lookup"><span data-stu-id="96640-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="96640-155">Power BI JavaScript-pakket</span><span class="sxs-lookup"><span data-stu-id="96640-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="96640-156">Nog vragen?</span><span class="sxs-lookup"><span data-stu-id="96640-156">More questions?</span></span> [<span data-ttu-id="96640-157">Probeer Hallo Power BI-Community</span><span class="sxs-lookup"><span data-stu-id="96640-157">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
