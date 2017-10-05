---
title: Een rapport insluiten in Azure Power BI Embedded | Microsoft Docs
description: Informatie over het insluiten van een rapport dat zich in Power BI Embedded in uw toepassing.
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
ms.openlocfilehash: 3d865af2418c9c557c861a379766a125d75cebf1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a>Een rapport insluiten in Power BI Embedded

Informatie over het insluiten van een rapport dat zich in Power BI Embedded in uw toepassing.

Laten we zien hoe u daadwerkelijk een rapport insluiten in uw toepassing. Hierbij wordt verondersteld dat er al een rapport dat bestaat in een werkruimte in uw werkruimteverzameling. Als u deze stap nog niet hebt gedaan, Zie [aan de slag met Power BI Embedded](power-bi-embedded-get-started.md).

U kunt de .NET (C#) of Node.js-SDK, samen met JavaScript, gemakkelijk maken voor uw toepassing met Power BI Embedded. 

## <a name="using-the-access-keys-to-use-rest-apis"></a>Met behulp van de toegangssleutels REST-API's gebruiken

Om de REST-API aanroept, kunt u de toegangssleutel die u via de Azure-portal voor een bepaalde werkruimteverzameling krijgen kunt doorgeven. Zie voor meer informatie [aan de slag met Power BI Embedded](power-bi-embedded-get-started.md).

## <a name="get-a-report-id"></a>Een rapport-id ophalen

Elke toegangstoken is gebaseerd op een rapport. U moet de opgegeven rapport-id niet ophalen voor het rapport dat u wilt insluiten. Dit kan worden gedaan op basis van aanroepen naar de [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST-API. Hiermee herstelt u de lijst-id en de url insluiten. Dit kan worden gedaan met behulp van de Power BI .NET SDK of de REST-API rechtstreeks aan te roepen.

### <a name="using-the-power-bi-net-sdk"></a>Met behulp van de Power BI .NET SDK

Wanneer u de .NET SDK, moet u een token referentie die is gebaseerd op de toegangssleutel die u via de Azure portal krijgen maken. Dit vereist dat u installeert de [Power BI API NuGet-pakket](https://www.nuget.org/profiles/powerbi).

**NuGet-pakket installeren**

```
Install-Package Microsoft.PowerBI.Api
```

**C#-code**

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select the report that you want to work with from the collection of reports.
```

### <a name="calling-the-rest-api-directly"></a>Rechtstreeks aanroepen van de REST-API

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response to get the report you want to work with.
    }

}
```

## <a name="create-an-access-token"></a>Maken van een toegangstoken

Maakt gebruik van Power BI Embedded insluiten token, JSON Web Tokens die HMAC zijn ondertekend. De tokens zijn ondertekend door de toegangssleutel van uw Azure Power BI Embedded werkruimteverzameling. Sluit tokens, standaard, alleen-lezen toegang aan een rapport insluiten in een toepassing worden gebruikt. Sluit tokens worden uitgegeven voor een specifiek rapport en moeten worden gekoppeld aan een URL insluiten.

Toegangstokens moeten worden gemaakt op de server, zoals de toegangssleutels voor het teken/versleutelen van de tokens worden gebruikt. Zie voor meer informatie over het maken van een toegangstoken [Authenticating en autoriseren met Power BI Embedded](power-bi-embedded-app-token-flow.md). U kunt ook bekijken de [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methode. Hier volgt een voorbeeld van hoe dit eruitziet met de .NET SDK voor Power BI.

Gebruikt u de id die u eerder hebt opgehaald. Zodra de insluittoken is gemaakt, wordt u vervolgens de toegangssleutel voor het genereren van het token dat u kunt gebruiken vanuit het perspectief van javascript gebruiken. De *PowerBIToken klasse* vereist dat u installeert de [Power BI Core NuGut pakket](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

**NuGet-pakket installeren**

```
Install-Package Microsoft.PowerBI.Core
```

**C#-code**

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-to-embed-tokens"></a>Scopes van de machtiging voor het insluiten van tokens toevoegen

Wanneer u insluiten tokens gebruikt, kunt u beperkt gebruik van de resources die u toegang te geven. Daarom kunt u een token met bereik machtigingen genereren. Zie voor meer informatie [Scopes](power-bi-embedded-app-token-flow.md#scopes)

## <a name="embed-using-javascript"></a>Insluiten met JavaScript

Nadat u het toegangstoken en de lijst-id hebt, kunnen we het rapport met JavaScript insluiten. Dit vereist dat u het nuget installeert [Power BI JavaScript pakket](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). De embedUrl worden alleen https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> U kunt de [JavaScript rapport insluiten voorbeeld](https://microsoft.github.io/PowerBI-JavaScript/demo/) om functionaliteit te testen. Het biedt ook voorbeelden van code voor de verschillende bewerkingen die beschikbaar zijn.

**NuGet-pakket installeren**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**JavaScript-code**

```
<script src="/scripts/powerbi.js"></script>
<div id="reportContainer"></div>

var embedConfiguration = {
    type: 'report',
    accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
    id: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed'
};

var $reportContainer = $('#reportContainer');
var report = powerbi.embed($reportContainer.get(0), embedConfiguration);
```

### <a name="set-the-size-of-embedded-elements"></a>De grootte van de ingesloten elementen instellen

Het rapport wordt automatisch op basis van de grootte van de container worden ingesloten. Voor het onderdrukken van de standaardgrootte van het ingesloten toe te voegen een CSS-klasse-kenmerk of inline stijlen voor breedte en hoogte.

## <a name="see-also"></a>Zie ook

[Aan de slag met het voorbeeld](power-bi-embedded-get-started-sample.md)  
[Verifiëren en autoriseren in Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Voorbeeld van ingesloten JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Power BI JavaScript-pakket](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
[Power BI API NuGet-pakket](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut-pakket](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Power BI-CSharp Git-opslagplaats](https://github.com/Microsoft/PowerBI-CSharp)  
[Power BI-knooppunt Git-opslagplaats](https://github.com/Microsoft/PowerBI-Node)  
Nog vragen? [Probeer de Power BI-community](http://community.powerbi.com/)
