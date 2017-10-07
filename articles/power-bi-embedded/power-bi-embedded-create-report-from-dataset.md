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
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a>Een nieuw rapport maken uit een gegevensset in Power BI Embedded

Power BI Embedded rapporten kunnen nu worden gemaakt uit een gegevensset in uw eigen toepassing. 

Hallo verificatiemethode is vergelijkbaar toothat van rapport insluiten. Deze is gebaseerd op toegangstokens die specifieke tooa gegevensset zijn. Gebruikt voor PowerBI.com tokens worden uitgegeven door Azure Active Directory (AAD) en Power BI Embedded tokens worden uitgegeven door uw eigen service.

Wanneer u een rapport ingesloten uitvoerbestanden Hallo zijn uitgegeven tokens voor een bepaalde gegevensset. Tokens moeten worden gekoppeld met de Hallo insluiten URL op Hallo dezelfde element tooensure elke heeft een unieke token. In volgorde toocreate een rapport ingesloten *Dataset.Read en Workspace.Report.Create* scopes in Hallo toegangstoken moeten worden opgegeven.

## <a name="create-access-token-needed-toocreate-new-report"></a>Access token benodigde toocreate nieuw rapport maken

Maakt gebruik van Power BI Embedded insluiten token, JSON Web Tokens die HMAC zijn ondertekend. Hallo tokens zijn ondertekend door de toegangssleutel Hallo van uw Azure Power BI Embedded werkruimteverzameling. Sluit tokens, standaard, zijn gebruikte tooprovide lezen alleen toegang tot tooa rapport tooembed in een toepassing. Sluit tokens worden uitgegeven voor een specifiek rapport en moeten worden gekoppeld aan een URL insluiten.

Toegangstokens moeten worden gemaakt op de server Hallo Hallo toegangstoetsen zijn gebruikte toosign/versleutelen Hallo-tokens. Voor meer informatie over een toegangstoken toocreate Zie [Authenticating en autoriseren met Power BI Embedded](power-bi-embedded-app-token-flow.md). U kunt ook bekijken Hallo [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methode. Hier volgt een voorbeeld van hoe dit eruitziet Hallo .NET SDK gebruiken voor Power BI.

In dit voorbeeld hebben we onze gegevensset-id die we willen toocreat Hallo nieuw rapport op. Er moet ook tooadd Hallo bereiken voor *Dataset.Read en Workspace.Report.Create*.

Hallo *PowerBIToken klasse* vereist dat u Hallo installeert [Power BI Core NuGut pakket](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

**NuGet-pakket installeren**

```
Install-Package Microsoft.PowerBI.Core
```

**C#-code**

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a>Maak een nieuwe leeg rapport

Maak in volgorde toocreate een nieuw rapport, Hallo configuratie moet worden opgegeven. Dit dient toegangstoken hello, Hallo embedURL en Hallo datasetID die we toocreate Hallo rapport op basis van willen omvatten. Dit vereist dat u Hallo nuget installeert [Power BI JavaScript pakket](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). Hallo embedUrl worden alleen https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> U kunt Hallo [JavaScript rapport insluiten voorbeeld](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest-functionaliteit. Het biedt ook voorbeelden van code voor verschillende bewerkingen Hallo die beschikbaar zijn.

**NuGet-pakket installeren**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**JavaScript-code**

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

Het aanroepen van *powerbi.createReport()* maakt een leeg canvas in de bewerkingsmodus voorkomen binnen de Hallo *div* element.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a>Nieuwe rapporten opslaan

Hallo-rapport niet daadwerkelijk gemaakt totdat u Hallo aanroepen **opslaan als** bewerking. Dit kan worden gedaan vanuit het bestandsmenu of vanuit JavaScript.

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
> Een nieuw rapport wordt gemaakt nadat **opslaan als** wordt aangeroepen. Nadat u hebt opgeslagen, wordt Hallo canvas Hallo gegevensset nog steeds weergegeven in de modus en niet Hallo rapport bewerken. U moet tooreload Hallo nieuw rapport net als andere rapporten.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a>Hallo nieuw rapport laden

In de volgorde toointeract met het nieuwe rapport Hallo moet u tooembed in dezelfde manier Hallo toepassing wordt ingesloten een reguliere rapport, betekenis, een nieuw token moet worden verstrekt specifiek voor het nieuwe rapport Hallo Hallo en klik vervolgens op Hallo aanroep van methode insluiten.

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

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a>Automatiseren opslaan en laden van een nieuw rapport met Hallo 'opgeslagen' gebeurtenis

In de volgorde tooautomate proces 'opslaan als' hello en vervolgens bij het laden van Hallo nieuw rapport kunt u het gebruik van Hallo 'opgeslagen' gebeurtenis. Deze gebeurtenis wordt geactiveerd wanneer Hallo opslagbewerking voltooid is en een Json-object met de nieuwe reportId hello, rapportnaam, oude reportId Hallo wordt (als er een) en als Hallo bewerking saveAs is of opslaan.

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

tooAutomate hello proces u kunt luisteren op Hallo 'opgeslagen' gebeurtenis, nieuwe reportId hello, Hallo nieuw token maken en Hallo nieuw rapport insluiten met deze.

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

## <a name="see-also"></a>Zie ook

[Aan de slag met het voorbeeld](power-bi-embedded-get-started-sample.md)  
[Rapporten opslaan](power-bi-embedded-save-reports.md)  
[Een rapport insluiten](power-bi-embedded-embed-report.md)  
[Verifiëren en autoriseren in Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Voorbeeld van ingesloten JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Power BI Core NuGut-pakket](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Power BI JavaScript-pakket](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
Nog vragen? [Probeer Hallo Power BI-Community](http://community.powerbi.com/)
