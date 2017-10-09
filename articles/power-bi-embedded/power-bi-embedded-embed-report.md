---
title: een rapport in Azure Power BI Embedded aaaEmbed | Microsoft Docs
description: Meer informatie over hoe een rapport dat in uw toepassing in Power BI Embedded tooembed.
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
ms.openlocfilehash: f25344bbd0b9c092ef19da04d0b455d453b426a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a>Een rapport insluiten in Power BI Embedded

Meer informatie over hoe een rapport dat in uw toepassing in Power BI Embedded tooembed.

Laten we zien hoe tooactually een rapport insluiten in uw toepassing. Hierbij wordt verondersteld dat er al een rapport dat bestaat in een werkruimte in uw werkruimteverzameling. Als u deze stap nog niet hebt gedaan, Zie [aan de slag met Power BI Embedded](power-bi-embedded-get-started.md).

U kunt Hallo .NET (C#) of Node.js SDK, samen met JavaScript, tooeasily uw toepassing met Power BI Embedded bouwen. 

## <a name="using-hello-access-keys-toouse-rest-apis"></a>Hallo toegang sleutels toouse REST-API's gebruiken

U kunt in volgorde toocall Hallo REST-API, Hallo toegangssleutel die u via hello Azure-portal voor een bepaalde werkruimteverzameling krijgen kunt doorgeven. Zie voor meer informatie [aan de slag met Power BI Embedded](power-bi-embedded-get-started.md).

## <a name="get-a-report-id"></a>Een rapport-id ophalen

Elke toegangstoken is gebaseerd op een rapport. U moet tooget Hallo lijst-id opgegeven voor het Hallo-rapport dat u wilt dat tooembed. Dit kan worden gedaan op basis van aanroepen toohello [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST-API. Dit wordt Hallo rapport-id en het Hallo insluiten url geretourneerd. U kunt dit doen met behulp van Hallo Power BI .NET SDK of rechtstreeks Hallo REST-API aanroepen.

### <a name="using-hello-power-bi-net-sdk"></a>Met behulp van Hallo Power BI .NET SDK

Wanneer u Hallo .NET SDK, moet u toocreate een token referentie die is gebaseerd op Hallo toegangssleutel die u via hello Azure-portal krijgen. Dit is vereist dat u Hallo installeert [Power BI API NuGet-pakket](https://www.nuget.org/profiles/powerbi).

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

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a>Rechtstreeks aanroepen Hallo REST-API

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response tooget hello report you want toowork with.
    }

}
```

## <a name="create-an-access-token"></a>Maken van een toegangstoken

Maakt gebruik van Power BI Embedded insluiten token, JSON Web Tokens die HMAC zijn ondertekend. Hallo tokens zijn ondertekend door de toegangssleutel Hallo van uw Azure Power BI Embedded werkruimteverzameling. Sluit tokens, standaard, zijn gebruikte tooprovide lezen alleen toegang tot tooa rapport tooembed in een toepassing. Sluit tokens worden uitgegeven voor een specifiek rapport en moeten worden gekoppeld aan een URL insluiten.

Toegangstokens moeten worden gemaakt op de server Hallo Hallo toegangstoetsen zijn gebruikte toosign/versleutelen Hallo-tokens. Voor meer informatie over een toegangstoken toocreate Zie [Authenticating en autoriseren met Power BI Embedded](power-bi-embedded-app-token-flow.md). U kunt ook bekijken Hallo [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methode. Hier volgt een voorbeeld van hoe dit eruitziet Hallo .NET SDK gebruiken voor Power BI.

U gebruikt Hallo rapport-id die u eerder hebt opgehaald. Zodra Hallo insluiten token is gemaakt, gebruikt u vervolgens Hallo sleutel toogenerate Hallo toegangstoken dat u vanuit javascript-perspectief Hallo gebruiken kunt. Hallo *PowerBIToken klasse* vereist dat u Hallo installeert [Power BI Core NuGut pakket](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

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

### <a name="adding-permission-scopes-tooembed-tokens"></a>Machtiging scopes tooembed-tokens toevoegen

Wanneer u insluiten tokens gebruikt, kunt u toorestrict informatie over het gebruik van Hallo-resources die u toegang te geven. Daarom kunt u een token met bereik machtigingen genereren. Zie voor meer informatie [Scopes](power-bi-embedded-app-token-flow.md#scopes)

## <a name="embed-using-javascript"></a>Insluiten met JavaScript

Nadat u Hallo-toegangstoken en Hallo lijst-id hebt, kunt we met JavaScript Hallo-rapport insluiten. Dit vereist dat u Hallo nuget installeert [Power BI JavaScript pakket](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). Hallo embedUrl worden alleen https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> U kunt Hallo [JavaScript rapport insluiten voorbeeld](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest-functionaliteit. Het biedt ook voorbeelden van code voor verschillende bewerkingen Hallo die beschikbaar zijn.

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

### <a name="set-hello-size-of-embedded-elements"></a>Hallo-grootte van de ingesloten elementen instellen

Hallo-rapport wordt automatisch op basis van de grootte van de container Hallo worden ingesloten. toooverride hello standaardgrootte Hallo ingesloten gewoon een CSS-klasse-kenmerk of inline stijlen voor breedte en hoogte toevoegen.

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
Nog vragen? [Probeer Hallo Power BI-Community](http://community.powerbi.com/)
