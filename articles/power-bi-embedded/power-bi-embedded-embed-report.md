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
# <a name="embed-a-report-in-power-bi-embedded"></a><span data-ttu-id="bb342-103">Een rapport insluiten in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="bb342-103">Embed a report in Power BI Embedded</span></span>

<span data-ttu-id="bb342-104">Meer informatie over hoe een rapport dat in uw toepassing in Power BI Embedded tooembed.</span><span class="sxs-lookup"><span data-stu-id="bb342-104">Learn how tooembed a report that is in Power BI Embedded into your application.</span></span>

<span data-ttu-id="bb342-105">Laten we zien hoe tooactually een rapport insluiten in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="bb342-105">We will look at how tooactually embed a report into your application.</span></span> <span data-ttu-id="bb342-106">Hierbij wordt verondersteld dat er al een rapport dat bestaat in een werkruimte in uw werkruimteverzameling.</span><span class="sxs-lookup"><span data-stu-id="bb342-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span></span> <span data-ttu-id="bb342-107">Als u deze stap nog niet hebt gedaan, Zie [aan de slag met Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bb342-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

<span data-ttu-id="bb342-108">U kunt Hallo .NET (C#) of Node.js SDK, samen met JavaScript, tooeasily uw toepassing met Power BI Embedded bouwen.</span><span class="sxs-lookup"><span data-stu-id="bb342-108">You can use hello .NET (C#) or Node.js SDK, along with JavaScript, tooeasily build your application with Power BI Embedded.</span></span> 

## <a name="using-hello-access-keys-toouse-rest-apis"></a><span data-ttu-id="bb342-109">Hallo toegang sleutels toouse REST-API's gebruiken</span><span class="sxs-lookup"><span data-stu-id="bb342-109">Using hello access keys toouse REST APIs</span></span>

<span data-ttu-id="bb342-110">U kunt in volgorde toocall Hallo REST-API, Hallo toegangssleutel die u via hello Azure-portal voor een bepaalde werkruimteverzameling krijgen kunt doorgeven.</span><span class="sxs-lookup"><span data-stu-id="bb342-110">In order toocall hello REST API, you can pass hello access key which you can get from hello Azure portal for a given workspace collection.</span></span> <span data-ttu-id="bb342-111">Zie voor meer informatie [aan de slag met Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bb342-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="get-a-report-id"></a><span data-ttu-id="bb342-112">Een rapport-id ophalen</span><span class="sxs-lookup"><span data-stu-id="bb342-112">Get a report id</span></span>

<span data-ttu-id="bb342-113">Elke toegangstoken is gebaseerd op een rapport.</span><span class="sxs-lookup"><span data-stu-id="bb342-113">Every access token is based on a report.</span></span> <span data-ttu-id="bb342-114">U moet tooget Hallo lijst-id opgegeven voor het Hallo-rapport dat u wilt dat tooembed.</span><span class="sxs-lookup"><span data-stu-id="bb342-114">You will need tooget hello given report id for hello report that you want tooembed.</span></span> <span data-ttu-id="bb342-115">Dit kan worden gedaan op basis van aanroepen toohello [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST-API.</span><span class="sxs-lookup"><span data-stu-id="bb342-115">This can be done based on calls toohello [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span></span> <span data-ttu-id="bb342-116">Dit wordt Hallo rapport-id en het Hallo insluiten url geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="bb342-116">This will return hello report id and hello embed url.</span></span> <span data-ttu-id="bb342-117">U kunt dit doen met behulp van Hallo Power BI .NET SDK of rechtstreeks Hallo REST-API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="bb342-117">This can be done using hello Power BI .NET SDK or calling hello REST API directly.</span></span>

### <a name="using-hello-power-bi-net-sdk"></a><span data-ttu-id="bb342-118">Met behulp van Hallo Power BI .NET SDK</span><span class="sxs-lookup"><span data-stu-id="bb342-118">Using hello Power BI .NET SDK</span></span>

<span data-ttu-id="bb342-119">Wanneer u Hallo .NET SDK, moet u toocreate een token referentie die is gebaseerd op Hallo toegangssleutel die u via hello Azure-portal krijgen.</span><span class="sxs-lookup"><span data-stu-id="bb342-119">When using hello .NET SDK, you will need toocreate a token credential which is based on hello access key you get from hello Azure portal.</span></span> <span data-ttu-id="bb342-120">Dit is vereist dat u Hallo installeert [Power BI API NuGet-pakket](https://www.nuget.org/profiles/powerbi).</span><span class="sxs-lookup"><span data-stu-id="bb342-120">This requires that you install hello [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span></span>

<span data-ttu-id="bb342-121">**NuGet-pakket installeren**</span><span class="sxs-lookup"><span data-stu-id="bb342-121">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Api
```

<span data-ttu-id="bb342-122">**C#-code**</span><span class="sxs-lookup"><span data-stu-id="bb342-122">**C# code**</span></span>

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a><span data-ttu-id="bb342-123">Rechtstreeks aanroepen Hallo REST-API</span><span class="sxs-lookup"><span data-stu-id="bb342-123">Calling hello REST API directly</span></span>

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

## <a name="create-an-access-token"></a><span data-ttu-id="bb342-124">Maken van een toegangstoken</span><span class="sxs-lookup"><span data-stu-id="bb342-124">Create an access token</span></span>

<span data-ttu-id="bb342-125">Maakt gebruik van Power BI Embedded insluiten token, JSON Web Tokens die HMAC zijn ondertekend.</span><span class="sxs-lookup"><span data-stu-id="bb342-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="bb342-126">Hallo tokens zijn ondertekend door de toegangssleutel Hallo van uw Azure Power BI Embedded werkruimteverzameling.</span><span class="sxs-lookup"><span data-stu-id="bb342-126">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="bb342-127">Sluit tokens, standaard, zijn gebruikte tooprovide lezen alleen toegang tot tooa rapport tooembed in een toepassing.</span><span class="sxs-lookup"><span data-stu-id="bb342-127">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="bb342-128">Sluit tokens worden uitgegeven voor een specifiek rapport en moeten worden gekoppeld aan een URL insluiten.</span><span class="sxs-lookup"><span data-stu-id="bb342-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="bb342-129">Toegangstokens moeten worden gemaakt op de server Hallo Hallo toegangstoetsen zijn gebruikte toosign/versleutelen Hallo-tokens.</span><span class="sxs-lookup"><span data-stu-id="bb342-129">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="bb342-130">Voor meer informatie over een toegangstoken toocreate Zie [Authenticating en autoriseren met Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="bb342-130">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="bb342-131">U kunt ook bekijken Hallo [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methode.</span><span class="sxs-lookup"><span data-stu-id="bb342-131">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="bb342-132">Hier volgt een voorbeeld van hoe dit eruitziet Hallo .NET SDK gebruiken voor Power BI.</span><span class="sxs-lookup"><span data-stu-id="bb342-132">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="bb342-133">U gebruikt Hallo rapport-id die u eerder hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="bb342-133">You will use hello report id that you retrieved earlier.</span></span> <span data-ttu-id="bb342-134">Zodra Hallo insluiten token is gemaakt, gebruikt u vervolgens Hallo sleutel toogenerate Hallo toegangstoken dat u vanuit javascript-perspectief Hallo gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="bb342-134">Once hello embed token is created, you will then use hello access key toogenerate hello token which you can use from hello javascript perspective.</span></span> <span data-ttu-id="bb342-135">Hallo *PowerBIToken klasse* vereist dat u Hallo installeert [Power BI Core NuGut pakket](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="bb342-135">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="bb342-136">**NuGet-pakket installeren**</span><span class="sxs-lookup"><span data-stu-id="bb342-136">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="bb342-137">**C#-code**</span><span class="sxs-lookup"><span data-stu-id="bb342-137">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a><span data-ttu-id="bb342-138">Machtiging scopes tooembed-tokens toevoegen</span><span class="sxs-lookup"><span data-stu-id="bb342-138">Adding permission scopes tooembed tokens</span></span>

<span data-ttu-id="bb342-139">Wanneer u insluiten tokens gebruikt, kunt u toorestrict informatie over het gebruik van Hallo-resources die u toegang te geven.</span><span class="sxs-lookup"><span data-stu-id="bb342-139">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="bb342-140">Daarom kunt u een token met bereik machtigingen genereren.</span><span class="sxs-lookup"><span data-stu-id="bb342-140">For this reason, you can generate a token with scoped permissions.</span></span> <span data-ttu-id="bb342-141">Zie voor meer informatie [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span><span class="sxs-lookup"><span data-stu-id="bb342-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span></span>

## <a name="embed-using-javascript"></a><span data-ttu-id="bb342-142">Insluiten met JavaScript</span><span class="sxs-lookup"><span data-stu-id="bb342-142">Embed using JavaScript</span></span>

<span data-ttu-id="bb342-143">Nadat u Hallo-toegangstoken en Hallo lijst-id hebt, kunt we met JavaScript Hallo-rapport insluiten.</span><span class="sxs-lookup"><span data-stu-id="bb342-143">After you have hello access token and hello report id, we can embed hello report using JavaScript.</span></span> <span data-ttu-id="bb342-144">Dit vereist dat u Hallo nuget installeert [Power BI JavaScript pakket](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="bb342-144">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="bb342-145">Hallo embedUrl worden alleen https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="bb342-145">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="bb342-146">U kunt Hallo [JavaScript rapport insluiten voorbeeld](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest-functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="bb342-146">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="bb342-147">Het biedt ook voorbeelden van code voor verschillende bewerkingen Hallo die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="bb342-147">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="bb342-148">**NuGet-pakket installeren**</span><span class="sxs-lookup"><span data-stu-id="bb342-148">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="bb342-149">**JavaScript-code**</span><span class="sxs-lookup"><span data-stu-id="bb342-149">**JavaScript code**</span></span>

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

### <a name="set-hello-size-of-embedded-elements"></a><span data-ttu-id="bb342-150">Hallo-grootte van de ingesloten elementen instellen</span><span class="sxs-lookup"><span data-stu-id="bb342-150">Set hello size of embedded elements</span></span>

<span data-ttu-id="bb342-151">Hallo-rapport wordt automatisch op basis van de grootte van de container Hallo worden ingesloten.</span><span class="sxs-lookup"><span data-stu-id="bb342-151">hello report will automatically be embedded based on hello size of its container.</span></span> <span data-ttu-id="bb342-152">toooverride hello standaardgrootte Hallo ingesloten gewoon een CSS-klasse-kenmerk of inline stijlen voor breedte en hoogte toevoegen.</span><span class="sxs-lookup"><span data-stu-id="bb342-152">toooverride hello default size of hello embeds simply add a CSS class attribute or inline styles for width & height.</span></span>

## <a name="see-also"></a><span data-ttu-id="bb342-153">Zie ook</span><span class="sxs-lookup"><span data-stu-id="bb342-153">See also</span></span>

[<span data-ttu-id="bb342-154">Aan de slag met het voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bb342-154">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="bb342-155">Verifiëren en autoriseren in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="bb342-155">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="bb342-156">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="bb342-156">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="bb342-157">Voorbeeld van ingesloten JavaScript</span><span class="sxs-lookup"><span data-stu-id="bb342-157">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="bb342-158">Power BI JavaScript-pakket</span><span class="sxs-lookup"><span data-stu-id="bb342-158">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="bb342-159">[Power BI API NuGet-pakket](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut-pakket](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span><span class="sxs-lookup"><span data-stu-id="bb342-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span></span>  
[<span data-ttu-id="bb342-160">Power BI-CSharp Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="bb342-160">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="bb342-161">Power BI-knooppunt Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="bb342-161">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="bb342-162">Nog vragen?</span><span class="sxs-lookup"><span data-stu-id="bb342-162">More questions?</span></span> [<span data-ttu-id="bb342-163">Probeer Hallo Power BI-Community</span><span class="sxs-lookup"><span data-stu-id="bb342-163">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
