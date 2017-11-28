---
title: aaaToggle tussen de modus voor weergeven en bewerken voor rapporten in Azure Power BI Embedded | Microsoft Docs
description: Meer informatie over hoe tootoggle tussen de modus voor weergeven en bewerken voor uw rapporten in Power BI Embedded.
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
ms.openlocfilehash: c9e3da5f9ae74d221af650adebde7c9d83b38a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="toggle-between-view-and-edit-mode-for-reports-in-power-bi-embedded"></a><span data-ttu-id="d2676-103">Schakelen tussen weergeven en bewerken van de modus voor rapporten in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="d2676-103">Toggle between view and edit mode for reports in Power BI Embedded</span></span>

<span data-ttu-id="d2676-104">Meer informatie over hoe tootoggle tussen de modus voor weergeven en bewerken voor uw rapporten in Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="d2676-104">Learn how tootoggle between view and edit mode for your reports within Power BI Embedded.</span></span>

## <a name="creating-an-access-token"></a><span data-ttu-id="d2676-105">Maken van een toegangstoken</span><span class="sxs-lookup"><span data-stu-id="d2676-105">Creating an access token</span></span>

<span data-ttu-id="d2676-106">U moet toocreate een toegangstoken dat u Hallo mogelijkheid tooboth weergeven en bewerken van een rapport hebt.</span><span class="sxs-lookup"><span data-stu-id="d2676-106">You will need toocreate an access token that gives you hello ability tooboth view and edit a report.</span></span> <span data-ttu-id="d2676-107">tooedit en slaat u een rapport moet u Hallo **Report.ReadWrite** token machtiging.</span><span class="sxs-lookup"><span data-stu-id="d2676-107">tooedit and save a report, you will need hello **Report.ReadWrite** token permission.</span></span> <span data-ttu-id="d2676-108">Zie voor meer informatie [Authenticating en autorisatie in Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="d2676-108">For more information, see [Authenticating and authorizing in Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d2676-109">Hiermee kunt u tooedit en wijzigingen tooan bestaand rapport opslaan.</span><span class="sxs-lookup"><span data-stu-id="d2676-109">This will allow you tooedit and save changes tooan existing report.</span></span> <span data-ttu-id="d2676-110">Als u ook Hallo functie ondersteunen wilt **OpslaanAls**, moet u extra machtigingen toosupply.</span><span class="sxs-lookup"><span data-stu-id="d2676-110">If you would also like hello function of supporting **Save As**, you will need toosupply additional permissions.</span></span> <span data-ttu-id="d2676-111">Zie voor meer informatie [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="d2676-111">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Report.ReadWrite";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="embed-configuration"></a><span data-ttu-id="d2676-112">Configuratie insluiten</span><span class="sxs-lookup"><span data-stu-id="d2676-112">Embed configuration</span></span>

<span data-ttu-id="d2676-113">U moet toosupply machtigingen en een viewMode in volgorde toosee Hallo knop in de bewerkingsmodus opslaan.</span><span class="sxs-lookup"><span data-stu-id="d2676-113">You will need toosupply permissions and a viewMode in order toosee hello save button when in edit mode.</span></span> <span data-ttu-id="d2676-114">Zie voor meer informatie [insluiten configuratiedetails](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span><span class="sxs-lookup"><span data-stu-id="d2676-114">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="d2676-115">Bijvoorbeeld in JavaScript:</span><span class="sxs-lookup"><span data-stu-id="d2676-115">For example in JavaScript:</span></span>

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
        permissions: models.Permissions.ReadWrite /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.View,
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

<span data-ttu-id="d2676-116">Hiermee wordt aangegeven tooembed Hallo rapport op basis van de weergavemodus **viewMode** te wordt ingesteld op**modellen. ViewMode.View**.</span><span class="sxs-lookup"><span data-stu-id="d2676-116">This will indicate tooembed hello report in view mode based on **viewMode** being set too**models.ViewMode.View**.</span></span>

## <a name="view-mode"></a><span data-ttu-id="d2676-117">Weergavemodus</span><span class="sxs-lookup"><span data-stu-id="d2676-117">View mode</span></span>

<span data-ttu-id="d2676-118">U kunt Hallo JavaScript tooswitch te volgen in de weergavemodus, als u in de bewerkingsmodus.</span><span class="sxs-lookup"><span data-stu-id="d2676-118">You can use hello following JavaScript tooswitch into view mode, if you are in edit mode.</span></span>

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooview mode.
report.switchMode("view");

```

## <a name="edit-mode"></a><span data-ttu-id="d2676-119">De modus bewerken</span><span class="sxs-lookup"><span data-stu-id="d2676-119">Edit mode</span></span>

<span data-ttu-id="d2676-120">U kunt Hallo JavaScript tooswitch te volgen in de bewerkingsmodus, als u in de weergave modus.</span><span class="sxs-lookup"><span data-stu-id="d2676-120">You can use hello following JavaScript tooswitch into edit mode, if you are in view mode.</span></span>

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooedit mode.
report.switchMode("edit");

```

## <a name="see-also"></a><span data-ttu-id="d2676-121">Zie ook</span><span class="sxs-lookup"><span data-stu-id="d2676-121">See also</span></span>

[<span data-ttu-id="d2676-122">Aan de slag met het voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d2676-122">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="d2676-123">Een rapport insluiten</span><span class="sxs-lookup"><span data-stu-id="d2676-123">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="d2676-124">Verifiëren en autoriseren in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="d2676-124">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="d2676-125">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="d2676-125">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="d2676-126">Voorbeeld van ingesloten JavaScript</span><span class="sxs-lookup"><span data-stu-id="d2676-126">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="d2676-127">Power BI-CSharp Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="d2676-127">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="d2676-128">Power BI-knooppunt Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="d2676-128">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="d2676-129">Nog vragen?</span><span class="sxs-lookup"><span data-stu-id="d2676-129">More questions?</span></span> [<span data-ttu-id="d2676-130">Probeer Hallo Power BI-Community</span><span class="sxs-lookup"><span data-stu-id="d2676-130">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
