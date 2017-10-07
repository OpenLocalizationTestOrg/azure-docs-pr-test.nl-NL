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
# <a name="toggle-between-view-and-edit-mode-for-reports-in-power-bi-embedded"></a>Schakelen tussen weergeven en bewerken van de modus voor rapporten in Power BI Embedded

Meer informatie over hoe tootoggle tussen de modus voor weergeven en bewerken voor uw rapporten in Power BI Embedded.

## <a name="creating-an-access-token"></a>Maken van een toegangstoken

U moet toocreate een toegangstoken dat u Hallo mogelijkheid tooboth weergeven en bewerken van een rapport hebt. tooedit en slaat u een rapport moet u Hallo **Report.ReadWrite** token machtiging. Zie voor meer informatie [Authenticating en autorisatie in Power BI Embedded](power-bi-embedded-app-token-flow.md).

> [!NOTE]
> Hiermee kunt u tooedit en wijzigingen tooan bestaand rapport opslaan. Als u ook Hallo functie ondersteunen wilt **OpslaanAls**, moet u extra machtigingen toosupply. Zie voor meer informatie [Scopes](power-bi-embedded-app-token-flow.md#scopes).

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Report.ReadWrite";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="embed-configuration"></a>Configuratie insluiten

U moet toosupply machtigingen en een viewMode in volgorde toosee Hallo knop in de bewerkingsmodus opslaan. Zie voor meer informatie [insluiten configuratiedetails](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).

Bijvoorbeeld in JavaScript:

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

Hiermee wordt aangegeven tooembed Hallo rapport op basis van de weergavemodus **viewMode** te wordt ingesteld op**modellen. ViewMode.View**.

## <a name="view-mode"></a>Weergavemodus

U kunt Hallo JavaScript tooswitch te volgen in de weergavemodus, als u in de bewerkingsmodus.

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooview mode.
report.switchMode("view");

```

## <a name="edit-mode"></a>De modus bewerken

U kunt Hallo JavaScript tooswitch te volgen in de bewerkingsmodus, als u in de weergave modus.

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooedit mode.
report.switchMode("edit");

```

## <a name="see-also"></a>Zie ook

[Aan de slag met het voorbeeld](power-bi-embedded-get-started-sample.md)  
[Een rapport insluiten](power-bi-embedded-embed-report.md)  
[Verifiëren en autoriseren in Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Voorbeeld van ingesloten JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Power BI-CSharp Git-opslagplaats](https://github.com/Microsoft/PowerBI-CSharp)  
[Power BI-knooppunt Git-opslagplaats](https://github.com/Microsoft/PowerBI-Node)  
Nog vragen? [Probeer Hallo Power BI-Community](http://community.powerbi.com/)
