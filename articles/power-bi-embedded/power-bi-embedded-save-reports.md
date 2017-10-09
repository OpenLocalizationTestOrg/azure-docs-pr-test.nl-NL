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
# <a name="save-reports-in-power-bi-embedded"></a>Rapporten opslaan in Power BI Embedded

Meer informatie over hoe toosave rapporten in Power BI embedded. Dit de juiste machtigingen in volgorde toowork is vereist.

In Power BI Embedded, kunt u bestaande rapporten bewerken en opslaan. U kunt ook een nieuw rapport maken en opslaan als een nieuw rapport toocreate een.

In de volgorde toosave een rapport moet u eerst toocreate een token voor specifieke rapport met het juiste bereik Hallo Hallo:

* tooenable opslaan Report.ReadWrite bereik is vereist
* tooenable opslaan als Report.Read en Workspace.Report.Copy scopes zijn vereist
* tooenable opslaan en opslaan als, Report.ReadWrite en Workspace.Report.Copy zijn requierd

Respectievelijk in volgorde tooenable Hallo rechts opslaan of opslaan moet als knoppen in het bestandsmenu tooprovide Hallo rechter-machtiging in Hallo insluiten configuratie wanneer u insluiten Hallo rapport:

* modellen. Permissions.ReadWrite
* modellen. Permissions.Copy
* modellen. Permissions.All

> [!NOTE]
> Uw toegangstoken moet ook Hallo toepasselijke bereiken. Zie voor meer informatie [Scopes](power-bi-embedded-app-token-flow.md#scopes).

## <a name="embed-report-in-edit-mode"></a>Rapport insluiten in de bewerkingsmodus

Stel dat u een rapport in de bewerkingsmodus tooEmbed binnen uw app wilt, toodo zodat alleen Hallo rechts eigenschappen doorgeven in insluiten configuratie en powerbi.embed() aanroepen. U moet toosupply machtigingen en een viewMode in volgorde toosee Hallo opslaan en op te slaan als knoppen in de bewerkingsmodus. Zie voor meer informatie [insluiten configuratiedetails](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).

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

Nu worden een rapport ingesloten in uw app in de bewerkingsmodus.

## <a name="save-report"></a>Rapport opslaan

Nadat Embbeding Hallo rapport in de modus met Hallo rechts token en machtigingen bewerken kunt u Hallo rapport opslaan vanuit het bestandsmenu Hallo of vanuit javascript:

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a>Opslaan als

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
> Alleen na *opslaan als* is een nieuw rapport gemaakt. Nadat Hallo hebt opgeslagen, worden Hallo canvas Hallo oude rapport nog steeds in bewerken modus en niet Hallo nieuw rapport weergegeven. U moet tooembed Hallo nieuw rapport dat is gemaakt. Hiervoor moet een nieuw toegangstoken nadat ze zijn gemaakt per rapport.

Vervolgens moet u tooload Hallo nieuw rapport na een *opslaan als*. Dit is vergelijkbaar tooembedding rapporten.

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

## <a name="see-also"></a>Zie ook

[Aan de slag met het voorbeeld](power-bi-embedded-get-started-sample.md)  
[Een rapport insluiten](power-bi-embedded-embed-report.md)  
[Een nieuw rapport maken op basis van een gegevensset](power-bi-embedded-create-report-from-dataset.md)  
[Verifiëren en autoriseren in Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Voorbeeld van ingesloten JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Nog vragen? [Probeer Hallo Power BI-Community](http://community.powerbi.com/)

