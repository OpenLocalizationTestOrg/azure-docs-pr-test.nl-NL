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
# <a name="embed-a-report-in-power-bi-embedded"></a><span data-ttu-id="00aa7-103">Een rapport insluiten in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="00aa7-103">Embed a report in Power BI Embedded</span></span>

<span data-ttu-id="00aa7-104">Informatie over het insluiten van een rapport dat zich in Power BI Embedded in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="00aa7-104">Learn how to embed a report that is in Power BI Embedded into your application.</span></span>

<span data-ttu-id="00aa7-105">Laten we zien hoe u daadwerkelijk een rapport insluiten in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="00aa7-105">We will look at how to actually embed a report into your application.</span></span> <span data-ttu-id="00aa7-106">Hierbij wordt verondersteld dat er al een rapport dat bestaat in een werkruimte in uw werkruimteverzameling.</span><span class="sxs-lookup"><span data-stu-id="00aa7-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span></span> <span data-ttu-id="00aa7-107">Als u deze stap nog niet hebt gedaan, Zie [aan de slag met Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="00aa7-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

<span data-ttu-id="00aa7-108">U kunt de .NET (C#) of Node.js-SDK, samen met JavaScript, gemakkelijk maken voor uw toepassing met Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="00aa7-108">You can use the .NET (C#) or Node.js SDK, along with JavaScript, to easily build your application with Power BI Embedded.</span></span> 

## <a name="using-the-access-keys-to-use-rest-apis"></a><span data-ttu-id="00aa7-109">Met behulp van de toegangssleutels REST-API's gebruiken</span><span class="sxs-lookup"><span data-stu-id="00aa7-109">Using the access keys to use REST APIs</span></span>

<span data-ttu-id="00aa7-110">Om de REST-API aanroept, kunt u de toegangssleutel die u via de Azure-portal voor een bepaalde werkruimteverzameling krijgen kunt doorgeven.</span><span class="sxs-lookup"><span data-stu-id="00aa7-110">In order to call the REST API, you can pass the access key which you can get from the Azure portal for a given workspace collection.</span></span> <span data-ttu-id="00aa7-111">Zie voor meer informatie [aan de slag met Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="00aa7-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="get-a-report-id"></a><span data-ttu-id="00aa7-112">Een rapport-id ophalen</span><span class="sxs-lookup"><span data-stu-id="00aa7-112">Get a report id</span></span>

<span data-ttu-id="00aa7-113">Elke toegangstoken is gebaseerd op een rapport.</span><span class="sxs-lookup"><span data-stu-id="00aa7-113">Every access token is based on a report.</span></span> <span data-ttu-id="00aa7-114">U moet de opgegeven rapport-id niet ophalen voor het rapport dat u wilt insluiten.</span><span class="sxs-lookup"><span data-stu-id="00aa7-114">You will need to get the given report id for the report that you want to embed.</span></span> <span data-ttu-id="00aa7-115">Dit kan worden gedaan op basis van aanroepen naar de [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST-API.</span><span class="sxs-lookup"><span data-stu-id="00aa7-115">This can be done based on calls to the [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span></span> <span data-ttu-id="00aa7-116">Hiermee herstelt u de lijst-id en de url insluiten.</span><span class="sxs-lookup"><span data-stu-id="00aa7-116">This will return the report id and the embed url.</span></span> <span data-ttu-id="00aa7-117">Dit kan worden gedaan met behulp van de Power BI .NET SDK of de REST-API rechtstreeks aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="00aa7-117">This can be done using the Power BI .NET SDK or calling the REST API directly.</span></span>

### <a name="using-the-power-bi-net-sdk"></a><span data-ttu-id="00aa7-118">Met behulp van de Power BI .NET SDK</span><span class="sxs-lookup"><span data-stu-id="00aa7-118">Using the Power BI .NET SDK</span></span>

<span data-ttu-id="00aa7-119">Wanneer u de .NET SDK, moet u een token referentie die is gebaseerd op de toegangssleutel die u via de Azure portal krijgen maken.</span><span class="sxs-lookup"><span data-stu-id="00aa7-119">When using the .NET SDK, you will need to create a token credential which is based on the access key you get from the Azure portal.</span></span> <span data-ttu-id="00aa7-120">Dit vereist dat u installeert de [Power BI API NuGet-pakket](https://www.nuget.org/profiles/powerbi).</span><span class="sxs-lookup"><span data-stu-id="00aa7-120">This requires that you install the [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span></span>

<span data-ttu-id="00aa7-121">**NuGet-pakket installeren**</span><span class="sxs-lookup"><span data-stu-id="00aa7-121">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Api
```

<span data-ttu-id="00aa7-122">**C#-code**</span><span class="sxs-lookup"><span data-stu-id="00aa7-122">**C# code**</span></span>

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select the report that you want to work with from the collection of reports.
```

### <a name="calling-the-rest-api-directly"></a><span data-ttu-id="00aa7-123">Rechtstreeks aanroepen van de REST-API</span><span class="sxs-lookup"><span data-stu-id="00aa7-123">Calling the REST API directly</span></span>

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

## <a name="create-an-access-token"></a><span data-ttu-id="00aa7-124">Maken van een toegangstoken</span><span class="sxs-lookup"><span data-stu-id="00aa7-124">Create an access token</span></span>

<span data-ttu-id="00aa7-125">Maakt gebruik van Power BI Embedded insluiten token, JSON Web Tokens die HMAC zijn ondertekend.</span><span class="sxs-lookup"><span data-stu-id="00aa7-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="00aa7-126">De tokens zijn ondertekend door de toegangssleutel van uw Azure Power BI Embedded werkruimteverzameling.</span><span class="sxs-lookup"><span data-stu-id="00aa7-126">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="00aa7-127">Sluit tokens, standaard, alleen-lezen toegang aan een rapport insluiten in een toepassing worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="00aa7-127">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span></span> <span data-ttu-id="00aa7-128">Sluit tokens worden uitgegeven voor een specifiek rapport en moeten worden gekoppeld aan een URL insluiten.</span><span class="sxs-lookup"><span data-stu-id="00aa7-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="00aa7-129">Toegangstokens moeten worden gemaakt op de server, zoals de toegangssleutels voor het teken/versleutelen van de tokens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="00aa7-129">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span></span> <span data-ttu-id="00aa7-130">Zie voor meer informatie over het maken van een toegangstoken [Authenticating en autoriseren met Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="00aa7-130">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="00aa7-131">U kunt ook bekijken de [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methode.</span><span class="sxs-lookup"><span data-stu-id="00aa7-131">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="00aa7-132">Hier volgt een voorbeeld van hoe dit eruitziet met de .NET SDK voor Power BI.</span><span class="sxs-lookup"><span data-stu-id="00aa7-132">Here is an example of what this would look like using the .NET SDK for Power BI.</span></span>

<span data-ttu-id="00aa7-133">Gebruikt u de id die u eerder hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="00aa7-133">You will use the report id that you retrieved earlier.</span></span> <span data-ttu-id="00aa7-134">Zodra de insluittoken is gemaakt, wordt u vervolgens de toegangssleutel voor het genereren van het token dat u kunt gebruiken vanuit het perspectief van javascript gebruiken.</span><span class="sxs-lookup"><span data-stu-id="00aa7-134">Once the embed token is created, you will then use the access key to generate the token which you can use from the javascript perspective.</span></span> <span data-ttu-id="00aa7-135">De *PowerBIToken klasse* vereist dat u installeert de [Power BI Core NuGut pakket](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="00aa7-135">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="00aa7-136">**NuGet-pakket installeren**</span><span class="sxs-lookup"><span data-stu-id="00aa7-136">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="00aa7-137">**C#-code**</span><span class="sxs-lookup"><span data-stu-id="00aa7-137">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-to-embed-tokens"></a><span data-ttu-id="00aa7-138">Scopes van de machtiging voor het insluiten van tokens toevoegen</span><span class="sxs-lookup"><span data-stu-id="00aa7-138">Adding permission scopes to embed tokens</span></span>

<span data-ttu-id="00aa7-139">Wanneer u insluiten tokens gebruikt, kunt u beperkt gebruik van de resources die u toegang te geven.</span><span class="sxs-lookup"><span data-stu-id="00aa7-139">When using Embed tokens, you may want to restrict usage of the resources you give access to.</span></span> <span data-ttu-id="00aa7-140">Daarom kunt u een token met bereik machtigingen genereren.</span><span class="sxs-lookup"><span data-stu-id="00aa7-140">For this reason, you can generate a token with scoped permissions.</span></span> <span data-ttu-id="00aa7-141">Zie voor meer informatie [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span><span class="sxs-lookup"><span data-stu-id="00aa7-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span></span>

## <a name="embed-using-javascript"></a><span data-ttu-id="00aa7-142">Insluiten met JavaScript</span><span class="sxs-lookup"><span data-stu-id="00aa7-142">Embed using JavaScript</span></span>

<span data-ttu-id="00aa7-143">Nadat u het toegangstoken en de lijst-id hebt, kunnen we het rapport met JavaScript insluiten.</span><span class="sxs-lookup"><span data-stu-id="00aa7-143">After you have the access token and the report id, we can embed the report using JavaScript.</span></span> <span data-ttu-id="00aa7-144">Dit vereist dat u het nuget installeert [Power BI JavaScript pakket](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="00aa7-144">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="00aa7-145">De embedUrl worden alleen https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="00aa7-145">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="00aa7-146">U kunt de [JavaScript rapport insluiten voorbeeld](https://microsoft.github.io/PowerBI-JavaScript/demo/) om functionaliteit te testen.</span><span class="sxs-lookup"><span data-stu-id="00aa7-146">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span></span> <span data-ttu-id="00aa7-147">Het biedt ook voorbeelden van code voor de verschillende bewerkingen die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="00aa7-147">It also gives code examples for the different operations that are available.</span></span>

<span data-ttu-id="00aa7-148">**NuGet-pakket installeren**</span><span class="sxs-lookup"><span data-stu-id="00aa7-148">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="00aa7-149">**JavaScript-code**</span><span class="sxs-lookup"><span data-stu-id="00aa7-149">**JavaScript code**</span></span>

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

### <a name="set-the-size-of-embedded-elements"></a><span data-ttu-id="00aa7-150">De grootte van de ingesloten elementen instellen</span><span class="sxs-lookup"><span data-stu-id="00aa7-150">Set the size of embedded elements</span></span>

<span data-ttu-id="00aa7-151">Het rapport wordt automatisch op basis van de grootte van de container worden ingesloten.</span><span class="sxs-lookup"><span data-stu-id="00aa7-151">The report will automatically be embedded based on the size of its container.</span></span> <span data-ttu-id="00aa7-152">Voor het onderdrukken van de standaardgrootte van het ingesloten toe te voegen een CSS-klasse-kenmerk of inline stijlen voor breedte en hoogte.</span><span class="sxs-lookup"><span data-stu-id="00aa7-152">To override the default size of the embeds simply add a CSS class attribute or inline styles for width & height.</span></span>

## <a name="see-also"></a><span data-ttu-id="00aa7-153">Zie ook</span><span class="sxs-lookup"><span data-stu-id="00aa7-153">See also</span></span>

[<span data-ttu-id="00aa7-154">Aan de slag met het voorbeeld</span><span class="sxs-lookup"><span data-stu-id="00aa7-154">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="00aa7-155">Verifiëren en autoriseren in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="00aa7-155">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="00aa7-156">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="00aa7-156">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="00aa7-157">Voorbeeld van ingesloten JavaScript</span><span class="sxs-lookup"><span data-stu-id="00aa7-157">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="00aa7-158">Power BI JavaScript-pakket</span><span class="sxs-lookup"><span data-stu-id="00aa7-158">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="00aa7-159">[Power BI API NuGet-pakket](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut-pakket](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span><span class="sxs-lookup"><span data-stu-id="00aa7-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span></span>  
[<span data-ttu-id="00aa7-160">Power BI-CSharp Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="00aa7-160">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="00aa7-161">Power BI-knooppunt Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="00aa7-161">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="00aa7-162">Nog vragen?</span><span class="sxs-lookup"><span data-stu-id="00aa7-162">More questions?</span></span> [<span data-ttu-id="00aa7-163">Probeer de Power BI-community</span><span class="sxs-lookup"><span data-stu-id="00aa7-163">Try the Power BI Community</span></span>](http://community.powerbi.com/)
