---
title: aaaSave rapporten in Azure Power BI Embedded | Microsoft Docs
description: Meer informatie over hoe toosave rapporten in Power BI embedded. Dit de juiste machtigingen in volgorde toowork is vereist.
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
ms.openlocfilehash: 984537ce1ce1afc787d6c6c9f61ae8d6226d1171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="save-reports-in-power-bi-embedded"></a><span data-ttu-id="0b18f-104">Rapporten opslaan in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="0b18f-104">Save reports in Power BI Embedded</span></span>

<span data-ttu-id="0b18f-105">Meer informatie over hoe toosave rapporten in Power BI embedded.</span><span class="sxs-lookup"><span data-stu-id="0b18f-105">Learn how toosave reports within Power BI embedded.</span></span> <span data-ttu-id="0b18f-106">Dit de juiste machtigingen in volgorde toowork is vereist.</span><span class="sxs-lookup"><span data-stu-id="0b18f-106">This requires proper permissions in order toowork successfully.</span></span>

<span data-ttu-id="0b18f-107">In Power BI Embedded, kunt u bestaande rapporten bewerken en opslaan.</span><span class="sxs-lookup"><span data-stu-id="0b18f-107">Within Power BI Embedded, you can edit existing reports and save them.</span></span> <span data-ttu-id="0b18f-108">U kunt ook een nieuw rapport maken en opslaan als een nieuw rapport toocreate een.</span><span class="sxs-lookup"><span data-stu-id="0b18f-108">You can also create a new report and save as a new report toocreate one.</span></span>

<span data-ttu-id="0b18f-109">In de volgorde toosave een rapport moet u eerst toocreate een token voor specifieke rapport met het juiste bereik Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="0b18f-109">In order toosave a report you first need toocreate a token for hello specific report with hello right scopes:</span></span>

* <span data-ttu-id="0b18f-110">tooenable opslaan Report.ReadWrite bereik is vereist</span><span class="sxs-lookup"><span data-stu-id="0b18f-110">tooenable save Report.ReadWrite scope is required</span></span>
* <span data-ttu-id="0b18f-111">tooenable opslaan als Report.Read en Workspace.Report.Copy scopes zijn vereist</span><span class="sxs-lookup"><span data-stu-id="0b18f-111">tooenable save as, Report.Read and Workspace.Report.Copy scopes are required</span></span>
* <span data-ttu-id="0b18f-112">tooenable opslaan en opslaan als, Report.ReadWrite en Workspace.Report.Copy zijn requierd</span><span class="sxs-lookup"><span data-stu-id="0b18f-112">tooenable save and save as, Report.ReadWrite and Workspace.Report.Copy are requierd</span></span>

<span data-ttu-id="0b18f-113">Respectievelijk in volgorde tooenable Hallo rechts opslaan of opslaan moet als knoppen in het bestandsmenu tooprovide Hallo rechter-machtiging in Hallo insluiten configuratie wanneer u insluiten Hallo rapport:</span><span class="sxs-lookup"><span data-stu-id="0b18f-113">Respectively in order tooenable hello right save/save as buttons in file menu you need tooprovide hello right permission in hello Embed configuration when you Embed hello report:</span></span>

* <span data-ttu-id="0b18f-114">modellen. Permissions.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="0b18f-114">models.Permissions.ReadWrite</span></span>
* <span data-ttu-id="0b18f-115">modellen. Permissions.Copy</span><span class="sxs-lookup"><span data-stu-id="0b18f-115">models.Permissions.Copy</span></span>
* <span data-ttu-id="0b18f-116">modellen. Permissions.All</span><span class="sxs-lookup"><span data-stu-id="0b18f-116">models.Permissions.All</span></span>

> [!NOTE]
> <span data-ttu-id="0b18f-117">Uw toegangstoken moet ook Hallo toepasselijke bereiken.</span><span class="sxs-lookup"><span data-stu-id="0b18f-117">Your access token also needs hello appropriate scopes.</span></span> <span data-ttu-id="0b18f-118">Zie voor meer informatie [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="0b18f-118">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

## <a name="embed-report-in-edit-mode"></a><span data-ttu-id="0b18f-119">Rapport insluiten in de bewerkingsmodus</span><span class="sxs-lookup"><span data-stu-id="0b18f-119">Embed report in edit mode</span></span>

<span data-ttu-id="0b18f-120">Stel dat u een rapport in de bewerkingsmodus tooEmbed binnen uw app wilt, toodo zodat alleen Hallo rechts eigenschappen doorgeven in insluiten configuratie en powerbi.embed() aanroepen.</span><span class="sxs-lookup"><span data-stu-id="0b18f-120">Let's say you want tooEmbed a report in edit mode inside your app, toodo so just pass hello right properties in Embed configuration and call powerbi.embed().</span></span> <span data-ttu-id="0b18f-121">U moet toosupply machtigingen en een viewMode in volgorde toosee Hallo opslaan en op te slaan als knoppen in de bewerkingsmodus.</span><span class="sxs-lookup"><span data-stu-id="0b18f-121">You will need toosupply permissions and a viewMode in order toosee hello save and save as buttons when in edit mode.</span></span> <span data-ttu-id="0b18f-122">Zie voor meer informatie [insluiten configuratiedetails](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span><span class="sxs-lookup"><span data-stu-id="0b18f-122">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="0b18f-123">Bijvoorbeeld in JavaScript:</span><span class="sxs-lookup"><span data-stu-id="0b18f-123">For example in JavaScript:</span></span>

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used toodescribe hello what and how tooembed.
    // This object is used when calling powerbi.embed.
    // This also includes settings and options such as filters.
    // You can find more information at https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details.
    var config= {
        type: 'report',
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        id:  '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
        permissions: models.Permissions.All /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.Edit,
        settings: {
            filterPaneEnabled: true,
            navContentPaneEnabled: true
        }
    };

    // Get a reference toohello embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed hello report and display it within hello div container.
    var report = powerbi.embed(reportContainer, config);
```

<span data-ttu-id="0b18f-124">Nu worden een rapport ingesloten in uw app in de bewerkingsmodus.</span><span class="sxs-lookup"><span data-stu-id="0b18f-124">Now a report will be embedded in your app in edit mode.</span></span>

## <a name="save-report"></a><span data-ttu-id="0b18f-125">Rapport opslaan</span><span class="sxs-lookup"><span data-stu-id="0b18f-125">Save report</span></span>

<span data-ttu-id="0b18f-126">Nadat Embbeding Hallo rapport in de modus met Hallo rechts token en machtigingen bewerken kunt u Hallo rapport opslaan vanuit het bestandsmenu Hallo of vanuit javascript:</span><span class="sxs-lookup"><span data-stu-id="0b18f-126">After Embbeding hello report in edit mode with hello right token and permissions you can save hello report from hello file menu or from javascript:</span></span>

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a><span data-ttu-id="0b18f-127">Opslaan als</span><span class="sxs-lookup"><span data-stu-id="0b18f-127">Save as</span></span>

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
> <span data-ttu-id="0b18f-128">Alleen na *opslaan als* is een nieuw rapport gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0b18f-128">Only after *save as* is a new report created.</span></span> <span data-ttu-id="0b18f-129">Nadat Hallo hebt opgeslagen, worden Hallo canvas Hallo oude rapport nog steeds in bewerken modus en niet Hallo nieuw rapport weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0b18f-129">After hello save, hello canvas is still showing hello old report in edit mode and not hello new report.</span></span> <span data-ttu-id="0b18f-130">U moet tooembed Hallo nieuw rapport dat is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0b18f-130">You will need tooembed hello new report that was created.</span></span> <span data-ttu-id="0b18f-131">Hiervoor moet een nieuw toegangstoken nadat ze zijn gemaakt per rapport.</span><span class="sxs-lookup"><span data-stu-id="0b18f-131">This requires a new access token as they are created per report.</span></span>

<span data-ttu-id="0b18f-132">Vervolgens moet u tooload Hallo nieuw rapport na een *opslaan als*.</span><span class="sxs-lookup"><span data-stu-id="0b18f-132">You will then need tooload hello new report after a *save as*.</span></span> <span data-ttu-id="0b18f-133">Dit is vergelijkbaar tooembedding rapporten.</span><span class="sxs-lookup"><span data-stu-id="0b18f-133">This is similar tooembedding any report.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="0b18f-134">Zie ook</span><span class="sxs-lookup"><span data-stu-id="0b18f-134">See also</span></span>

[<span data-ttu-id="0b18f-135">Aan de slag met het voorbeeld</span><span class="sxs-lookup"><span data-stu-id="0b18f-135">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="0b18f-136">Een rapport insluiten</span><span class="sxs-lookup"><span data-stu-id="0b18f-136">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="0b18f-137">Een nieuw rapport maken op basis van een gegevensset</span><span class="sxs-lookup"><span data-stu-id="0b18f-137">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="0b18f-138">Verifiëren en autoriseren in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="0b18f-138">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="0b18f-139">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="0b18f-139">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="0b18f-140">Voorbeeld van ingesloten JavaScript</span><span class="sxs-lookup"><span data-stu-id="0b18f-140">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="0b18f-141">Nog vragen?</span><span class="sxs-lookup"><span data-stu-id="0b18f-141">More questions?</span></span> [<span data-ttu-id="0b18f-142">Probeer Hallo Power BI-Community</span><span class="sxs-lookup"><span data-stu-id="0b18f-142">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

