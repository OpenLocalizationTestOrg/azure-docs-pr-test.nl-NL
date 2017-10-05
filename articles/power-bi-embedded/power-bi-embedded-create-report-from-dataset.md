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
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a>Een nieuw rapport maken uit een gegevensset in Power BI Embedded

Power BI Embedded rapporten kunnen nu worden gemaakt uit een gegevensset in uw eigen toepassing. 

De verificatiemethode is vergelijkbaar met dat van het rapport insluiten. Deze is gebaseerd op toegangstokens die specifiek voor een gegevensset zijn. Gebruikt voor PowerBI.com tokens worden uitgegeven door Azure Active Directory (AAD) en Power BI Embedded tokens worden uitgegeven door uw eigen service.

Wanneer een ingesloten rapport, de uitgegeven tokens uitvoerbestanden zijn voor een bepaalde gegevensset. Tokens moeten worden gekoppeld aan de URL van de insluiten op hetzelfde element zodat elk een unieke token heeft. Om te kunnen maken van een rapport ingesloten *Dataset.Read en Workspace.Report.Create* scopes moeten worden opgegeven in het toegangstoken.

## <a name="create-access-token-needed-to-create-new-report"></a>Toegangstoken voor het maken van nieuw rapport maken

Maakt gebruik van Power BI Embedded insluiten token, JSON Web Tokens die HMAC zijn ondertekend. De tokens zijn ondertekend door de toegangssleutel van uw Azure Power BI Embedded werkruimteverzameling. Sluit tokens, standaard, alleen-lezen toegang aan een rapport insluiten in een toepassing worden gebruikt. Sluit tokens worden uitgegeven voor een specifiek rapport en moeten worden gekoppeld aan een URL insluiten.

Toegangstokens moeten worden gemaakt op de server, zoals de toegangssleutels voor het teken/versleutelen van de tokens worden gebruikt. Zie voor meer informatie over het maken van een toegangstoken [Authenticating en autoriseren met Power BI Embedded](power-bi-embedded-app-token-flow.md). U kunt ook bekijken de [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methode. Hier volgt een voorbeeld van hoe dit eruitziet met de .NET SDK voor Power BI.

In dit voorbeeld hebben we onze gegevensset-id die we willen maken het nieuwe rapport op. Er moet ook de scopes voor toevoegen *Dataset.Read en Workspace.Report.Create*.

De *PowerBIToken klasse* vereist dat u installeert de [Power BI Core NuGut pakket](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

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

Om een nieuw rapport maakt, moet de configuratie maken worden opgegeven. Dit dient het toegangstoken, de embedURL en de datasetID die we willen maken van het rapport op basis van omvatten. Dit vereist dat u het nuget installeert [Power BI JavaScript pakket](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). De embedUrl worden alleen https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> U kunt de [JavaScript rapport insluiten voorbeeld](https://microsoft.github.io/PowerBI-JavaScript/demo/) om functionaliteit te testen. Het biedt ook voorbeelden van code voor de verschillende bewerkingen die beschikbaar zijn.

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
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

Het aanroepen van *powerbi.createReport()* maakt een leeg canvas in de bewerkingsmodus voorkomen binnen de *div* element.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a>Nieuwe rapporten opslaan

Het rapport niet daadwerkelijk gemaakt totdat u de **opslaan als** bewerking. Dit kan worden gedaan vanuit het bestandsmenu of vanuit JavaScript.

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
> Een nieuw rapport wordt gemaakt nadat **opslaan als** wordt aangeroepen. Nadat u hebt opgeslagen, wordt het canvas de dataset nog steeds weergegeven in de bewerkingsmodus en niet in het rapport. U moet het nieuwe rapport laden net als andere rapporten.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-the-new-report"></a>Het nieuwe rapport laden

Om te communiceren met het nieuwe rapport moet u dit op dezelfde manier als de toepassing wordt ingesloten een reguliere rapport insluiten wil zeggen, een nieuw token specifiek voor het nieuwe rapport moet worden verstrekt en vervolgens de insluiten-methode aanroepen.

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

## <a name="automate-save-and-load-of-a-new-report-using-the-saved-event"></a>Automatiseren opslaan en laden van een nieuw rapport met de 'opgeslagen' gebeurtenis

In volgorde voor het automatiseren van 'opslaan als' en vervolgens bij het laden van het nieuwe rapport kunt u het gebruik van de gebeurtenis 'opgeslagen'. Deze gebeurtenis wordt geactiveerd wanneer de opslagbewerking voltooid is en retourneert een Json-object met de nieuwe reportId, de naam van rapport, de oude reportId (als er een) en als de bewerking saveAs is of opslaan.

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

Voor het automatiseren van het proces dat u op de 'opgeslagen' gebeurtenis luisteren kunt duren voordat de nieuwe reportId, maken van het nieuwe token en het nieuwe rapport insluiten met deze.

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

## <a name="see-also"></a>Zie ook

[Aan de slag met het voorbeeld](power-bi-embedded-get-started-sample.md)  
[Rapporten opslaan](power-bi-embedded-save-reports.md)  
[Een rapport insluiten](power-bi-embedded-embed-report.md)  
[Verifiëren en autoriseren in Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Voorbeeld van ingesloten JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Power BI Core NuGut-pakket](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Power BI JavaScript-pakket](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
Nog vragen? [Probeer de Power BI-community](http://community.powerbi.com/)