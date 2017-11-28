---
title: aaaWorking Hello App Service Mobile Apps-clientbibliotheek beheerd (Windows | Microsoft Docs
description: Meer informatie over hoe toouse een .NET-client voor Azure App Service Mobile Apps met Windows en Xamarin-apps.
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0280785c-e027-4e0d-aaf2-6f155e5a6197
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 01/04/2017
ms.author: glenga
ms.openlocfilehash: b056e606b19406398f5b6faabb0931ad651125e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="71095-103">Hoe toouse Hallo-client voor mobiele Apps van Azure beheerd</span><span class="sxs-lookup"><span data-stu-id="71095-103">How toouse hello managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="71095-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="71095-104">Overview</span></span>
<span data-ttu-id="71095-105">Deze handleiding wordt getoond hoe tooperform algemene scenario's met behulp van Hallo-clientbibliotheek voor apps in Azure App Service Mobile Apps voor Windows en Xamarin beheerd.</span><span class="sxs-lookup"><span data-stu-id="71095-105">This guide shows you how tooperform common scenarios using hello managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="71095-106">Als u nieuwe tooMobile Apps, moet u eerst voltooit Hallo [Azure Mobile Apps Quick Start] [ 1] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="71095-106">If you are new tooMobile Apps, you should consider first completing hello [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="71095-107">In deze handleiding we richten op Hallo clientzijde beheerd SDK.</span><span class="sxs-lookup"><span data-stu-id="71095-107">In this guide, we focus on hello client-side managed SDK.</span></span> <span data-ttu-id="71095-108">informatie over hello serverzijde SDK's voor mobiele Apps, Zie Hallo-documentatie voor Hallo toolearn [.NET Server SDK] [ 2] of de [Node.js Server SDK] [ 3].</span><span class="sxs-lookup"><span data-stu-id="71095-108">toolearn more about hello server-side SDKs for Mobile Apps, see hello documentation for hello [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="71095-109">Referentiedocumentatie</span><span class="sxs-lookup"><span data-stu-id="71095-109">Reference documentation</span></span>
<span data-ttu-id="71095-110">Hallo-naslagdocumentatie voor Hallo client SDK bevindt zich hier: [referentie voor Azure Mobile Apps .NET client][4].</span><span class="sxs-lookup"><span data-stu-id="71095-110">hello reference documentation for hello client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="71095-111">U vindt ook enkele voorbeelden van de client in Hallo [Azure-Samples GitHub-opslagplaats][5].</span><span class="sxs-lookup"><span data-stu-id="71095-111">You can also find several client samples in hello [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="71095-112">Ondersteunde Platforms</span><span class="sxs-lookup"><span data-stu-id="71095-112">Supported Platforms</span></span>
<span data-ttu-id="71095-113">Hallo .NET-Platform ondersteunt Hallo volgende platforms:</span><span class="sxs-lookup"><span data-stu-id="71095-113">hello .NET Platform supports hello following platforms:</span></span>

* <span data-ttu-id="71095-114">Xamarin Android-versies voor API-19 tot en met 24 (KitKat via deze)</span><span class="sxs-lookup"><span data-stu-id="71095-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="71095-115">Xamarin iOS-versies voor iOS 8.0 en hoger</span><span class="sxs-lookup"><span data-stu-id="71095-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="71095-116">Universele Windows-Platform</span><span class="sxs-lookup"><span data-stu-id="71095-116">Universal Windows Platform</span></span>
* <span data-ttu-id="71095-117">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="71095-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="71095-118">Windows Phone 8.0, met uitzondering van Silverlight-toepassingen</span><span class="sxs-lookup"><span data-stu-id="71095-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="71095-119">Hallo 'server-flow' verificatie maakt gebruik van een webweergave voor Hallo gebruikersinterface weergegeven.</span><span class="sxs-lookup"><span data-stu-id="71095-119">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="71095-120">Als Hallo apparaat niet kunt toopresent een WebView UI, er zijn andere methoden voor verificatie nodig.</span><span class="sxs-lookup"><span data-stu-id="71095-120">If hello device is not able toopresent a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="71095-121">Deze SDK is derhalve niet geschikt voor controle-type of op dezelfde manier beperkte apparaten.</span><span class="sxs-lookup"><span data-stu-id="71095-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="71095-122"><a name="setup"></a>Het installatieprogramma en vereisten</span><span class="sxs-lookup"><span data-stu-id="71095-122"><a name="setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="71095-123">Er wordt ervan uitgegaan dat u hebt al gemaakt en gepubliceerd van uw mobiele App back-end-project, waaronder ten minste één tabel.</span><span class="sxs-lookup"><span data-stu-id="71095-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="71095-124">In het Hallo-code die wordt gebruikt in dit onderwerp, Hallo tabel heet `TodoItem` en of hieraan Hallo volgende kolommen: `Id`, `Text`, en `Complete`.</span><span class="sxs-lookup"><span data-stu-id="71095-124">In hello code used in this topic, hello table is named `TodoItem` and it has hello following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="71095-125">Deze tabel is Hallo dezelfde tabel gemaakt wanneer u voltooit de [Azure Mobile Apps Quick Start][1].</span><span class="sxs-lookup"><span data-stu-id="71095-125">This table is hello same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="71095-126">Hallo corresponderende getypte clientzijde type in C# is Hallo klasse te volgen:</span><span class="sxs-lookup"><span data-stu-id="71095-126">hello corresponding typed client-side type in C# is hello following class:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }
}
```

<span data-ttu-id="71095-127">Hallo [JsonPropertyAttribute] [ 6] gebruikte toodefine Hallo is *PropertyName* toewijzing tussen Hallo client velden en Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="71095-127">hello [JsonPropertyAttribute][6] is used toodefine hello *PropertyName* mapping between hello client field and hello table field.</span></span>

<span data-ttu-id="71095-128">toolearn hoe toocreate tabellen in uw Mobile Apps back-end, Zie Hallo [onderwerp SDK voor .NET-Server] [ 7] of Hallo [Node.js Server SDK onderwerp] [ 8] .</span><span class="sxs-lookup"><span data-stu-id="71095-128">toolearn how toocreate tables in your Mobile Apps backend, see hello [.NET Server SDK topic][7] or hello [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="71095-129">Als u uw back-end voor de mobiele App gemaakt in hello Azure portal met behulp van Hallo Quick Start, kunt u ook Hallo **gemakkelijk tabellen** instellen in Hallo [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="71095-129">If you created your Mobile App backend in hello Azure portal using hello QuickStart, you can also use hello **Easy tables** setting in hello [Azure portal].</span></span>

### <a name="how-to-install-hello-managed-client-sdk-package"></a><span data-ttu-id="71095-130">Hoe: installatie Hallo beheerde client SDK-pakket</span><span class="sxs-lookup"><span data-stu-id="71095-130">How to: Install hello managed client SDK package</span></span>
<span data-ttu-id="71095-131">Gebruik een van de volgende methoden tooinstall Hallo Hallo beheerde client SDK-pakket voor mobiele Apps van [NuGet][9]:</span><span class="sxs-lookup"><span data-stu-id="71095-131">Use one of hello following methods tooinstall hello managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="71095-132">**Visual Studio** met de rechtermuisknop op uw project, klikt u op **NuGet-pakketten beheren**, zoekt u Hallo `Microsoft.Azure.Mobile.Client` van het pakket en klik vervolgens op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="71095-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="71095-133">**Xamarin Studio** met de rechtermuisknop op uw project, klikt u op **toevoegen** > **NuGet-pakketten toevoegen**, zoekt u Hallo `Microsoft.Azure.Mobile.Client `van het pakket en klik vervolgens op **toevoegen Pakket**.</span><span class="sxs-lookup"><span data-stu-id="71095-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="71095-134">In het bestand hoofdactiviteit Onthoud tooadd Hallo volgende **met** instructie:</span><span class="sxs-lookup"><span data-stu-id="71095-134">In your main activity file, remember tooadd hello following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <span data-ttu-id="71095-135"><a name="symbolsource"></a>Procedure: werken met symbolen in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="71095-135"><a name="symbolsource"></a>How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="71095-136">Hallo symbolen voor Hallo Microsoft.Azure.Mobile naamruimte zijn beschikbaar op [SymbolSource][10].</span><span class="sxs-lookup"><span data-stu-id="71095-136">hello symbols for hello Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="71095-137">Raadpleeg toothe [SymbolSource instructies] [ 11] toointegrate SymbolSource met Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71095-137">Refer toothe [SymbolSource instructions][11] toointegrate SymbolSource with Visual Studio.</span></span>

## <span data-ttu-id="71095-138"><a name="create-client"></a>Hallo Mobile Apps-client maken</span><span class="sxs-lookup"><span data-stu-id="71095-138"><a name="create-client"></a>Create hello Mobile Apps client</span></span>
<span data-ttu-id="71095-139">Hallo volgende code maakt Hallo [MobileServiceClient] [ 12] -object dat is gebruikt tooaccess backend voor mobiele Apps.</span><span class="sxs-lookup"><span data-stu-id="71095-139">hello following code creates hello [MobileServiceClient][12] object that is used tooaccess your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="71095-140">Vervang in Hallo voorafgaand aan code, `MOBILE_APP_URL` met Hallo-URL van back-end van Hallo Mobile Apps, die is gevonden in de blade voor uw back-end voor mobiele App in Hallo [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="71095-140">In hello preceding code, replace `MOBILE_APP_URL` with hello URL of hello Mobile App backend, which is found in the blade for your Mobile App backend in hello [Azure portal].</span></span> <span data-ttu-id="71095-141">Hallo MobileServiceClient object moet een singleton.</span><span class="sxs-lookup"><span data-stu-id="71095-141">hello MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="71095-142">Werken met tabellen</span><span class="sxs-lookup"><span data-stu-id="71095-142">Work with Tables</span></span>
<span data-ttu-id="71095-143">Hallo hoe volgende van de sectie details toosearch records ophalen en Hallo gegevens binnen Hallo tabel wijzigen.</span><span class="sxs-lookup"><span data-stu-id="71095-143">hello following section details how toosearch and retrieve records and modify hello data within hello table.</span></span>  <span data-ttu-id="71095-144">Hallo volgende onderwerpen komen aan bod:</span><span class="sxs-lookup"><span data-stu-id="71095-144">hello following topics are covered:</span></span>

* [<span data-ttu-id="71095-145">De tabelverwijzing van een maken</span><span class="sxs-lookup"><span data-stu-id="71095-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="71095-146">Opvragen van gegevens</span><span class="sxs-lookup"><span data-stu-id="71095-146">Query data</span></span>](#querying)
* [<span data-ttu-id="71095-147">Geretourneerde gegevens filteren</span><span class="sxs-lookup"><span data-stu-id="71095-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="71095-148">Geretourneerde gegevens sorteren</span><span class="sxs-lookup"><span data-stu-id="71095-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="71095-149">Gegevens weergeven op pagina 's</span><span class="sxs-lookup"><span data-stu-id="71095-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="71095-150">Selecteer specifieke kolommen</span><span class="sxs-lookup"><span data-stu-id="71095-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="71095-151">Een record door-Id niet opzoeken</span><span class="sxs-lookup"><span data-stu-id="71095-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="71095-152">Omgaan met niet-getypeerde query 's</span><span class="sxs-lookup"><span data-stu-id="71095-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="71095-153">Gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="71095-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="71095-154">Bijwerken van gegevens</span><span class="sxs-lookup"><span data-stu-id="71095-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="71095-155">Verwijderen van gegevens</span><span class="sxs-lookup"><span data-stu-id="71095-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="71095-156">Conflictoplossing en optimistische gelijktijdigheid</span><span class="sxs-lookup"><span data-stu-id="71095-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="71095-157">Binding tooa Windows-gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="71095-157">Binding tooa Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="71095-158">Hallo paginagrootte wijzigen</span><span class="sxs-lookup"><span data-stu-id="71095-158">Changing hello Page Size</span></span>](#pagesize)

### <span data-ttu-id="71095-159"><a name="instantiating"></a>Procedure: een tabelverwijzing maken</span><span class="sxs-lookup"><span data-stu-id="71095-159"><a name="instantiating"></a>How to: Create a table reference</span></span>
<span data-ttu-id="71095-160">Alle Hallo-code die toegang heeft tot of gegevens wijzigt in een tabel van de back-end-functies aanroepen op Hallo `MobileServiceTable` object.</span><span class="sxs-lookup"><span data-stu-id="71095-160">All hello code that accesses or modifies data in a backend table calls functions on hello `MobileServiceTable` object.</span></span> <span data-ttu-id="71095-161">Een toohello verwijzingstabel verkrijgen door de aanroepende Hallo [GetTable] methode als volgt:</span><span class="sxs-lookup"><span data-stu-id="71095-161">Obtain a reference toohello table by calling hello [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="71095-162">Hallo geretourneerd object maakt gebruik van Hallo getypte serialisatie.</span><span class="sxs-lookup"><span data-stu-id="71095-162">hello returned object uses hello typed serialization model.</span></span> <span data-ttu-id="71095-163">Een model met niet-getypeerde serialisatie wordt ook ondersteund.</span><span class="sxs-lookup"><span data-stu-id="71095-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="71095-164">Het volgende voorbeeld [maakt u een niet-getypeerde tabel tooan]:</span><span class="sxs-lookup"><span data-stu-id="71095-164">The following example [creates a reference tooan untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="71095-165">In niet-getypeerde query's, moet u Hallo onderliggende OData-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="71095-165">In untyped queries, you must specify hello underlying OData query string.</span></span>

### <span data-ttu-id="71095-166"><a name="querying"></a>Procedure: een Query over gegevens van uw mobiele App</span><span class="sxs-lookup"><span data-stu-id="71095-166"><a name="querying"></a>How to: Query data from your Mobile App</span></span>
<span data-ttu-id="71095-167">Deze sectie wordt beschreven hoe tooissue backend voor mobiele Apps toohello, waaronder de volgende functionaliteit Hallo query:</span><span class="sxs-lookup"><span data-stu-id="71095-167">This section describes how tooissue queries toohello Mobile App backend, which includes hello following functionality:</span></span>

* [<span data-ttu-id="71095-168">Geretourneerde gegevens filteren</span><span class="sxs-lookup"><span data-stu-id="71095-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="71095-169">Geretourneerde gegevens sorteren</span><span class="sxs-lookup"><span data-stu-id="71095-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="71095-170">Gegevens weergeven op pagina 's</span><span class="sxs-lookup"><span data-stu-id="71095-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="71095-171">Selecteer specifieke kolommen</span><span class="sxs-lookup"><span data-stu-id="71095-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="71095-172">Opzoeken van gegevens door-ID</span><span class="sxs-lookup"><span data-stu-id="71095-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="71095-173">Een server aangestuurde paginaformaat is afgedwongen tooprevent alle rijen worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="71095-173">A server-driven page size is enforced tooprevent all rows from being returned.</span></span>  <span data-ttu-id="71095-174">Standaard-aanvragen voor grote gegevenssets houdt paginering Hallo service negatief beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="71095-174">Paging keeps default requests for large data sets from negatively impacting hello service.</span></span>  <span data-ttu-id="71095-175">tooreturn meer dan 50 rijen gebruiken Hallo `Skip` en `Take` methode, zoals beschreven in [gegevens retourneren op pagina's](#paging).</span><span class="sxs-lookup"><span data-stu-id="71095-175">tooreturn more than 50 rows, use hello `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <span data-ttu-id="71095-176"><a name="filtering"></a>Hoe: Filter gegevens geretourneerd</span><span class="sxs-lookup"><span data-stu-id="71095-176"><a name="filtering"></a>How to: Filter returned data</span></span>
<span data-ttu-id="71095-177">Hallo volgende code laat zien hoe gegevens door te nemen toofilter een `Where` -component in een query.</span><span class="sxs-lookup"><span data-stu-id="71095-177">hello following code illustrates how toofilter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="71095-178">Deze retourneert alle items uit `todoTable` waarvan `Complete` eigenschap is gelijk te`false`.</span><span class="sxs-lookup"><span data-stu-id="71095-178">It returns all items from `todoTable` whose `Complete` property is equal too`false`.</span></span> <span data-ttu-id="71095-179">Hallo [waar] functie is van toepassing een rij predicaat Hallo-query op Hallo tabel filteren.</span><span class="sxs-lookup"><span data-stu-id="71095-179">hello [Where] function applies a row filtering predicate to hello query against hello table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="71095-180">U kunt Hallo URI van aanvraag verzonden toohello back-end van Hallo weergeven met behulp van bericht inspectie software, zoals browser ontwikkelhulpprogramma's of [Fiddler].</span><span class="sxs-lookup"><span data-stu-id="71095-180">You can view hello URI of hello request sent toohello backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="71095-181">Als u Hallo aanvraag-URI bekijkt, ziet u dat de queryreeks Hallo is gewijzigd:</span><span class="sxs-lookup"><span data-stu-id="71095-181">If you look at hello request URI, notice that hello query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="71095-182">Deze OData-aanvraag wordt omgezet in een SQL-query door Hallo Server SDK:</span><span class="sxs-lookup"><span data-stu-id="71095-182">This OData request is translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="71095-183">de functie die wordt doorgegeven toohello Hallo `Where` methode een willekeurig aantal voorwaarden kan hebben.</span><span class="sxs-lookup"><span data-stu-id="71095-183">hello function that is passed toohello `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="71095-184">In dit voorbeeld zou worden vertaald naar een SQL-query door Hallo Server SDK:</span><span class="sxs-lookup"><span data-stu-id="71095-184">This example would be translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="71095-185">Deze query kan ook worden gesplitst in meerdere componenten:</span><span class="sxs-lookup"><span data-stu-id="71095-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="71095-186">Hallo twee methoden zijn equivalent en door elkaar worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="71095-186">hello two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="71095-187">Hallo voormalige optie&mdash;van meerdere predicaten in één query cookievalidatie&mdash;is compact en aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="71095-187">hello former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="71095-188">Hallo `Where` component ondersteunt bewerkingen die worden vertaald naar Hallo OData subset.</span><span class="sxs-lookup"><span data-stu-id="71095-188">hello `Where` clause supports operations that be translated into hello OData subset.</span></span> <span data-ttu-id="71095-189">Bewerkingen zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="71095-189">Operations include:</span></span>

* <span data-ttu-id="71095-190">Relationele operators (==,! =, <, < =, >, > =),</span><span class="sxs-lookup"><span data-stu-id="71095-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="71095-191">Rekenkundige operatoren (+, -, /, *, %),</span><span class="sxs-lookup"><span data-stu-id="71095-191">Arithmetic operators (+, -, /, *, %),</span></span>
* <span data-ttu-id="71095-192">Number precision (Math.Floor, Math.Ceiling)</span><span class="sxs-lookup"><span data-stu-id="71095-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="71095-193">Tekenreeks-functies (lengte, subtekenreeks, vervangen, IndexOf, StartsWith, EndsWith)</span><span class="sxs-lookup"><span data-stu-id="71095-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="71095-194">Datumeigenschappen (jaar, maand, dag, uur, minuut, seconde)</span><span class="sxs-lookup"><span data-stu-id="71095-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="71095-195">Toegang tot de eigenschappen van een object, en</span><span class="sxs-lookup"><span data-stu-id="71095-195">Access properties of an object, and</span></span>
* <span data-ttu-id="71095-196">Expressies combineren van deze bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="71095-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="71095-197">Wanneer u in overweging wat Hallo Server SDK ondersteunt, zou u kunnen Hallo [OData v3 documentatie].</span><span class="sxs-lookup"><span data-stu-id="71095-197">When considering what hello Server SDK supports, you can consider hello [OData v3 Documentation].</span></span>

### <span data-ttu-id="71095-198"><a name="sorting"></a>Hoe: sorteren gegevens geretourneerd</span><span class="sxs-lookup"><span data-stu-id="71095-198"><a name="sorting"></a>How to: Sort returned data</span></span>
<span data-ttu-id="71095-199">Hallo volgende code laat zien hoe gegevens door te nemen toosort een [OrderBy] of [OrderByDescending] functie in Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="71095-199">hello following code illustrates how toosort data by including an [OrderBy] or [OrderByDescending] function in hello query.</span></span> <span data-ttu-id="71095-200">Deze items uit retourneert `todoTable` gesorteerd door Hallo oplopende `Text` veld.</span><span class="sxs-lookup"><span data-stu-id="71095-200">It returns items from `todoTable` sorted ascending by hello `Text` field.</span></span>

```
// Sort items in ascending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderBy(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();

// Sort items in descending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderByDescending(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();
```

### <span data-ttu-id="71095-201"><a name="paging"></a>Procedure: gegevens retourneren op pagina's</span><span class="sxs-lookup"><span data-stu-id="71095-201"><a name="paging"></a>How to: Return data in pages</span></span>
<span data-ttu-id="71095-202">Standaard Hallo back-end van alleen Hallo eerste 50 rijen geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="71095-202">By default, hello backend returns only hello first 50 rows.</span></span> <span data-ttu-id="71095-203">U kunt het aantal geretourneerde rijen Hallo vergroten door aanroepen Hallo [nemen] methode.</span><span class="sxs-lookup"><span data-stu-id="71095-203">You can increase hello number of returned rows by calling hello [Take] method.</span></span> <span data-ttu-id="71095-204">Gebruik `Take` samen met de Hallo [overslaan] methode toorequest een bepaalde 'pagina' van de totale gegevensset Hallo geretourneerd door Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="71095-204">Use `Take` along with hello [Skip] method toorequest a specific "page" of hello total dataset returned by hello query.</span></span> <span data-ttu-id="71095-205">Hallo retourneert volgende tijdens de uitvoering van query Hallo drie belangrijkste items in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="71095-205">hello following query, when executed, returns hello top three items in hello table.</span></span>

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="71095-206">Hallo volgende slaat het gereviseerde query Hallo eerste drie resultaten en retourneert de volgende drie resultaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="71095-206">hello following revised query skips hello first three results and returns hello next three results.</span></span> <span data-ttu-id="71095-207">Deze query produceert tweede Hallo 'pagina"gegevens, waarbij de paginagrootte Hallo drie items is.</span><span class="sxs-lookup"><span data-stu-id="71095-207">This query produces hello second "page" of data, where hello page size is three items.</span></span>

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="71095-208">Hallo [IncludeTotalCount] Hallo totale aantal voor aanvragen voor methode *alle* Hallo records die zou zijn geretourneerd, eventuele opgegeven paginering/limiet-component wordt genegeerd:</span><span class="sxs-lookup"><span data-stu-id="71095-208">hello [IncludeTotalCount] method requests hello total count for *all* hello records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="71095-209">In werkelijkheid-app kunt u query's vergelijkbaar toohello voorgaande voorbeeld met een pagineringsbesturingselement of een vergelijkbare UI navigeren tussen pagina's.</span><span class="sxs-lookup"><span data-stu-id="71095-209">In a real world app, you can use queries similar toohello preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="71095-210">toooverride hello 50-Rijlimiet in een back-end voor de mobiele App, moet u ook Hallo toepassen [EnableQueryAttribute] toohello openbare methode GET en Hallo paginering gedrag opgeven.</span><span class="sxs-lookup"><span data-stu-id="71095-210">toooverride hello 50-row limit in a Mobile App backend, you must also apply hello [EnableQueryAttribute] toohello public GET method and specify hello paging behavior.</span></span> <span data-ttu-id="71095-211">Toegepaste toohello methode Hallo na ingesteld wanneer het maximum aantal geretourneerde rijen too1000:</span><span class="sxs-lookup"><span data-stu-id="71095-211">When applied toohello method, hello following sets the maximum returned rows too1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <span data-ttu-id="71095-212"><a name="selecting"></a>Hoe: specifieke kolommen selecteren</span><span class="sxs-lookup"><span data-stu-id="71095-212"><a name="selecting"></a>How to: Select specific columns</span></span>
<span data-ttu-id="71095-213">U kunt opgeven welke set eigenschappen tooinclude in Hallo resulteert door toe te voegen een [Selecteer] component tooyour query.</span><span class="sxs-lookup"><span data-stu-id="71095-213">You can specify which set of properties tooinclude in hello results by adding a [Select] clause tooyour query.</span></span> <span data-ttu-id="71095-214">Bijvoorbeeld, Hallo volgende code wordt getoond hoe tooselect één veld en ook hoe tooselect en formatteren van meerdere velden:</span><span class="sxs-lookup"><span data-stu-id="71095-214">For example, hello following code shows how tooselect just one field and also how tooselect and format multiple fields:</span></span>

```
// Select one field -- just hello Text
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => todoItem.Text);
List<string> items = await query.ToListAsync();

// Select multiple fields -- both Complete and Text info
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => string.Format("{0} -- {1}",
                    todoItem.Text.PadRight(30), todoItem.Complete ?
                    "Now complete!" : "Incomplete!"));
List<string> items = await query.ToListAsync();
```

<span data-ttu-id="71095-215">Alle functies beschreven dusver Hallo additieve, zodat we kunt houden chaining ze zijn.</span><span class="sxs-lookup"><span data-stu-id="71095-215">All hello functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="71095-216">Elke aanroep van de keten is van invloed op meer Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="71095-216">Each chained call affects more of hello query.</span></span> <span data-ttu-id="71095-217">Een voorbeeld van meer:</span><span class="sxs-lookup"><span data-stu-id="71095-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <span data-ttu-id="71095-218"><a name="lookingup"></a>Hoe: opzoeken van gegevens door-ID</span><span class="sxs-lookup"><span data-stu-id="71095-218"><a name="lookingup"></a>How to: Look up data by ID</span></span>
<span data-ttu-id="71095-219">Hallo [LookupAsync] functie gebruikte toolook objecten uit de database met een bepaalde ID. Hallo kan zijn</span><span class="sxs-lookup"><span data-stu-id="71095-219">hello [LookupAsync] function can be used toolook up objects from hello database with a particular ID.</span></span>

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <span data-ttu-id="71095-220"><a name="untypedqueries"></a>Hoe: niet-getypeerde query's uitvoeren</span><span class="sxs-lookup"><span data-stu-id="71095-220"><a name="untypedqueries"></a>How to: Execute untyped queries</span></span>
<span data-ttu-id="71095-221">Bij het uitvoeren van een query met een niet-getypeerde tabelobject moet u expliciet Hallo OData-query-tekenreeks opgeven door het aanroepen van [ReadAsync], Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="71095-221">When executing a query using an untyped table object, you must explicitly specify hello OData query string by calling [ReadAsync], as in hello following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="71095-222">U terughalen JSON-waarden die u, zoals een eigenschappenverzameling gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="71095-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="71095-223">Zie voor meer informatie over JToken en Newtonsoft Json.NET hello [Json.NET] site.</span><span class="sxs-lookup"><span data-stu-id="71095-223">For more information on JToken and Newtonsoft Json.NET, see hello [Json.NET] site.</span></span>

### <span data-ttu-id="71095-224"><a name="inserting"></a>Procedure: gegevens invoegen in een back-end voor de mobiele App</span><span class="sxs-lookup"><span data-stu-id="71095-224"><a name="inserting"></a>How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="71095-225">Alle clienttypen moeten bevatten een lid genaamd **Id**, dit is standaard een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="71095-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="71095-226">Dit **Id** CRUD-bewerkingen uit te voeren is vereist en voor het offline synchroniseren. Hallo volgende code laat zien hoe toouse hello [InsertAsync] methode tooinsert nieuwe rijen in een tabel.</span><span class="sxs-lookup"><span data-stu-id="71095-226">This **Id** is required to perform CRUD operations and for offline sync. hello following code illustrates how toouse hello [InsertAsync] method tooinsert new rows into a table.</span></span> <span data-ttu-id="71095-227">Hallo-parameter bevat Hallo gegevens toobe ingevoegd als .NET-object.</span><span class="sxs-lookup"><span data-stu-id="71095-227">hello parameter contains hello data toobe inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="71095-228">Als een unieke aangepaste ID-waarde niet is opgenomen in Hallo `todoItem` tijdens een insert-, een GUID wordt gegenereerd door Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="71095-228">If a unique custom ID value is not included in hello `todoItem` during an insert, a GUID is generated by hello server.</span></span>
<span data-ttu-id="71095-229">U kunt ophalen Hallo Id gegenereerd door het Hallo-object te bekijken nadat Hallo aanroep retourneert.</span><span class="sxs-lookup"><span data-stu-id="71095-229">You can retrieve hello generated Id by inspecting hello object after hello call returns.</span></span>

<span data-ttu-id="71095-230">tooinsert getypeerde gegevens, kunt u profiteren van Json.NET:</span><span class="sxs-lookup"><span data-stu-id="71095-230">tooinsert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="71095-231">Hier volgt een voorbeeld van een e-mailadres als een unieke tekenreeks-id:</span><span class="sxs-lookup"><span data-stu-id="71095-231">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="71095-232">Werken met de id-waarden</span><span class="sxs-lookup"><span data-stu-id="71095-232">Working with ID values</span></span>
<span data-ttu-id="71095-233">Mobile Apps ondersteunt unieke aangepaste tekenreekswaarden voor van Hallo tabel **id** kolom.</span><span class="sxs-lookup"><span data-stu-id="71095-233">Mobile Apps supports unique custom string values for hello table's **id** column.</span></span> <span data-ttu-id="71095-234">Een string-waarde zorgt ervoor dat toepassingen toouse aangepaste waarden zoals e-mailadressen of gebruikersnamen voor Hallo-ID.</span><span class="sxs-lookup"><span data-stu-id="71095-234">A string value allows applications toouse custom values such as email addresses or user names for hello ID.</span></span>  <span data-ttu-id="71095-235">Tekenreeks-id's bieden u Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="71095-235">String IDs provide you with hello following benefits:</span></span>

* <span data-ttu-id="71095-236">Id's worden zonder dat een round trip toohello database gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="71095-236">IDs are generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="71095-237">Records zijn eenvoudiger toomerge uit verschillende tabellen of databases.</span><span class="sxs-lookup"><span data-stu-id="71095-237">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="71095-238">Id-waarden kunnen beter geïntegreerd met een toepassing logica.</span><span class="sxs-lookup"><span data-stu-id="71095-238">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="71095-239">Wanneer de waarde van een tekenreeks-ID niet is ingesteld op een ingevoegde record, backend voor mobiele Apps hello wordt gegenereerd voor een unieke waarde voor de ID.</span><span class="sxs-lookup"><span data-stu-id="71095-239">When a string ID value is not set on an inserted record, hello Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="71095-240">U kunt Hallo [Guid.NewGuid] methode toogenerate uw eigen ID-, op Hallo-client of in Hallo back-end waarden.</span><span class="sxs-lookup"><span data-stu-id="71095-240">You can use hello [Guid.NewGuid] method toogenerate your own ID values, either on hello client or in hello backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <span data-ttu-id="71095-241"><a name="modifying"></a>Procedure: gegevens wijzigen in een back-end voor de mobiele App</span><span class="sxs-lookup"><span data-stu-id="71095-241"><a name="modifying"></a>How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="71095-242">Hallo volgende code laat zien hoe toouse hello [UpdateAsync] methode tooupdate een bestaande record met Hallo met dezelfde ID met nieuwe informatie.</span><span class="sxs-lookup"><span data-stu-id="71095-242">hello following code illustrates how toouse hello [UpdateAsync] method tooupdate an existing record with hello same ID with new information.</span></span> <span data-ttu-id="71095-243">Hallo-parameter bevat Hallo gegevens toobe bijgewerkt als .NET-object.</span><span class="sxs-lookup"><span data-stu-id="71095-243">hello parameter contains hello data toobe updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="71095-244">tooupdate getypeerde gegevens, kunt u profiteren van [Json.NET] als volgt:</span><span class="sxs-lookup"><span data-stu-id="71095-244">tooupdate untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="71095-245">Een `id` veld moet worden opgegeven bij het maken van een update.</span><span class="sxs-lookup"><span data-stu-id="71095-245">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="71095-246">Hallo back-end gebruikt Hallo `id` veld tooidentify die tooupdate rij.</span><span class="sxs-lookup"><span data-stu-id="71095-246">hello backend uses hello `id` field tooidentify which row tooupdate.</span></span> <span data-ttu-id="71095-247">Hallo `id` veld kan worden verkregen van Hallo resultaat Hallo `InsertAsync` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="71095-247">hello `id` field can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="71095-248">Een `ArgumentException` treedt op als u een item tooupdate probeert zonder Hallo `id` waarde.</span><span class="sxs-lookup"><span data-stu-id="71095-248">An `ArgumentException` is raised if you try tooupdate an item without providing hello `id` value.</span></span>

### <span data-ttu-id="71095-249"><a name="deleting"></a>Hoe: verwijderen van gegevens in een back-end voor de mobiele App</span><span class="sxs-lookup"><span data-stu-id="71095-249"><a name="deleting"></a>How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="71095-250">Hallo volgende code laat zien hoe toouse hello [DeleteAsync] methode toodelete een bestaand exemplaar.</span><span class="sxs-lookup"><span data-stu-id="71095-250">hello following code illustrates how toouse hello [DeleteAsync] method toodelete an existing instance.</span></span> <span data-ttu-id="71095-251">Hallo-exemplaar wordt geïdentificeerd door Hallo `id` veld is ingesteld op Hallo `todoItem`.</span><span class="sxs-lookup"><span data-stu-id="71095-251">hello instance is identified by hello `id` field set on hello `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="71095-252">toodelete getypeerde gegevens, u kunt profiteren van Json.NET als volgt:</span><span class="sxs-lookup"><span data-stu-id="71095-252">toodelete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="71095-253">Wanneer u een aanvraag verwijderen, moet een ID worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="71095-253">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="71095-254">Andere eigenschappen toohello service niet worden doorgegeven of worden genegeerd op Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="71095-254">Other properties are not passed toohello service or are ignored at hello service.</span></span> <span data-ttu-id="71095-255">Hallo resultaat van een `DeleteAsync` aanroep is meestal `null`.</span><span class="sxs-lookup"><span data-stu-id="71095-255">hello result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="71095-256">Hallo-ID toopass in kunnen worden verkregen van Hallo resultaat Hallo `InsertAsync` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="71095-256">hello ID toopass in can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="71095-257">Een `MobileServiceInvalidOperationException` wordt gegenereerd wanneer u een item toodelete probeert zonder op te geven Hallo `id` veld.</span><span class="sxs-lookup"><span data-stu-id="71095-257">A `MobileServiceInvalidOperationException` is thrown when you try toodelete an item without specifying hello `id` field.</span></span>

### <span data-ttu-id="71095-258"><a name="optimisticconcurrency"></a>Hoe: gebruikt optimistische gelijktijdigheid voor conflictoplossing</span><span class="sxs-lookup"><span data-stu-id="71095-258"><a name="optimisticconcurrency"></a>How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="71095-259">Twee of meer clients kunnen schrijven van wijzigingen toohello dezelfde item op Hallo dezelfde tijd.</span><span class="sxs-lookup"><span data-stu-id="71095-259">Two or more clients may write changes toohello same item at hello same time.</span></span> <span data-ttu-id="71095-260">Zonder conflictdetectie overschrijft Hallo laatste schrijven alle vorige updates.</span><span class="sxs-lookup"><span data-stu-id="71095-260">Without conflict detection, hello last write would overwrite any previous updates.</span></span> <span data-ttu-id="71095-261">**Optimistisch gelijktijdigheidbeheer** wordt ervan uitgegaan dat elke transactie kan worden doorgevoerd en daarom geen vergrendeling van elke resource gebruikt.</span><span class="sxs-lookup"><span data-stu-id="71095-261">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="71095-262">Voordat u een transactie doorvoert, controleert Optimistisch gelijktijdigheidbeheer of dat er geen andere transactie Hallo gegevens is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="71095-262">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified hello data.</span></span> <span data-ttu-id="71095-263">Als Hallo gegevens is gewijzigd, is Hallo vastleggen van de transactie teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="71095-263">If hello data has been modified, hello committing transaction is rolled back.</span></span>

<span data-ttu-id="71095-264">Mobiele Apps biedt ondersteuning voor Optimistisch gelijktijdigheidbeheer door het bijhouden van wijzigingen tooeach item Hallo met `version` systeemkolom eigenschap die is gedefinieerd voor elke tabel in uw back-end voor de mobiele App.</span><span class="sxs-lookup"><span data-stu-id="71095-264">Mobile Apps supports optimistic concurrency control by tracking changes tooeach item using hello `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="71095-265">Telkens wanneer een record is bijgewerkt, Mobile Apps ingesteld Hallo `version` eigenschap voor dat de nieuwe waarde tooa vastleggen.</span><span class="sxs-lookup"><span data-stu-id="71095-265">Each time a record is updated, Mobile Apps sets hello `version` property for that record tooa new value.</span></span> <span data-ttu-id="71095-266">Tijdens elke updateaanvraag Hallo `version` eigenschap van het Hallo-record die deel uitmaakt van het Hallo-aanvraag is vergeleken toohello dezelfde eigenschap voor Hallo record op Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="71095-266">During each update request, hello `version` property of hello record included with hello request is compared toohello same property for hello record on hello server.</span></span> <span data-ttu-id="71095-267">Als de versie die is doorgegeven met Hallo-aanvraag komt niet overeen met de Hallo back-end en vervolgens Hallo-clientbibliotheek genereert een `MobileServicePreconditionFailedException<T>` uitzondering.</span><span class="sxs-lookup"><span data-stu-id="71095-267">If the version passed with hello request does not match hello backend, then hello client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="71095-268">Hallo-type opgenomen met de Hallo uitzondering is Hallo-record van Hallo back-end met Hallo servers versie van het Hallo-record.</span><span class="sxs-lookup"><span data-stu-id="71095-268">hello type included with hello exception is hello record from hello backend containing hello servers version of hello record.</span></span> <span data-ttu-id="71095-269">Hallo toepassing kan vervolgens worden gebruikt deze informatie toodecide of tooexecute Hallo updateaanvraag opnieuw met de juiste Hallo `version` waarde van Hallo back-end toocommit wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="71095-269">hello application can then use this information toodecide whether tooexecute hello update request again with hello correct `version` value from hello backend toocommit changes.</span></span>

<span data-ttu-id="71095-270">Een kolom definiëren op Hallo tabel klasse voor Hallo `version` system eigenschap tooenable optimistische gelijktijdigheid.</span><span class="sxs-lookup"><span data-stu-id="71095-270">Define a column on hello table class for hello `version` system property tooenable optimistic concurrency.</span></span> <span data-ttu-id="71095-271">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="71095-271">For example:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }

    // *** Enable Optimistic Concurrency *** //
    [JsonProperty(PropertyName = "version")]
    public string Version { set; get; }
}
```

<span data-ttu-id="71095-272">Toepassingen die gebruikmaken van niet-getypeerde tabellen optimistische gelijktijdigheid inschakelen door de instelling Hallo `Version` vlag op de `SystemProperties` Hallo tabel als volgt.</span><span class="sxs-lookup"><span data-stu-id="71095-272">Applications using untyped tables enable optimistic concurrency by setting hello `Version` flag on the `SystemProperties` of hello table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="71095-273">In aanvulling tooenabling optimistische gelijktijdigheid, moet u ook Hallo catch `MobileServicePreconditionFailedException<T>` uitzondering in uw code bij het aanroepen van [UpdateAsync].</span><span class="sxs-lookup"><span data-stu-id="71095-273">In addition tooenabling optimistic concurrency, you must also catch hello `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="71095-274">Hallo conflict oplossen door toe te passen Hallo juist `version` toothe bijgewerkt record en aanroep [UpdateAsync] Hello opgelost record.</span><span class="sxs-lookup"><span data-stu-id="71095-274">Resolve hello conflict by applying hello correct `version` toothe updated record and call [UpdateAsync] with hello resolved record.</span></span> <span data-ttu-id="71095-275">Hallo volgende code toont hoe tooresolve een schrijfconflict eenmaal gedetecteerd:</span><span class="sxs-lookup"><span data-stu-id="71095-275">hello following code shows how tooresolve a write conflict once detected:</span></span>

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at hello remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, hello item has changed since hello last query
        // Resolve hello conflict between hello local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user toochoose hello resoltion between versions
    MessageDialog msgDialog = new MessageDialog(
        String.Format("Server Text: \"{0}\" \nLocal Text: \"{1}\"\n",
        serverItem.Text, localItem.Text),
        "CONFLICT DETECTED - Select a resolution:");

    UICommand localBtn = new UICommand("Commit Local Text");
    UICommand ServerBtn = new UICommand("Leave Server Text");
    msgDialog.Commands.Add(localBtn);
    msgDialog.Commands.Add(ServerBtn);

    localBtn.Invoked = async (IUICommand command) =>
    {
        // tooresolve hello conflict, update hello version of hello item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while hello user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

<span data-ttu-id="71095-276">Zie voor meer informatie, Hallo [Offline synchroniseren van gegevens in Azure Mobile Apps] onderwerp.</span><span class="sxs-lookup"><span data-stu-id="71095-276">For more information, see hello [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <span data-ttu-id="71095-277"><a name="binding"></a>Hoe: Bind Mobile Apps gegevens tooa Windows-gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="71095-277"><a name="binding"></a>How to: Bind Mobile Apps data tooa Windows user interface</span></span>
<span data-ttu-id="71095-278">Deze sectie wordt beschreven hoe toodisplay geretourneerd met behulp van UI-elementen in een Windows-app-gegevensobjecten.</span><span class="sxs-lookup"><span data-stu-id="71095-278">This section shows how toodisplay returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="71095-279">De volgende voorbeeldcode wordt gebonden toohello bron van Hallo lijst met een query voor onvolledige items.</span><span class="sxs-lookup"><span data-stu-id="71095-279">The following example code binds toohello source of hello list with a query for incomplete items.</span></span> <span data-ttu-id="71095-280">De [MobileServiceCollection] maakt een mobiele Apps-bewuste binding-verzameling.</span><span class="sxs-lookup"><span data-stu-id="71095-280">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound tooa UI list control
IEnumerable itemsControl  = items;

// Bind this tooa ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="71095-281">Sommige besturingselementen in Hallo beheerde runtimeondersteuning die een interface aangeroepen [ISupportIncrementalLoading].</span><span class="sxs-lookup"><span data-stu-id="71095-281">Some controls in hello managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="71095-282">Deze interface kunt besturingselementen toorequest extra gegevens wanneer hello wordt geschoven.</span><span class="sxs-lookup"><span data-stu-id="71095-282">This interface allows controls toorequest extra data when hello user scrolls.</span></span> <span data-ttu-id="71095-283">Er is ingebouwde ondersteuning voor deze interface voor universele Windows-apps via [MobileServiceIncrementalLoadingCollection], die automatisch de aanroepen van Hallo besturingselementen verwerkt.</span><span class="sxs-lookup"><span data-stu-id="71095-283">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from hello controls.</span></span> <span data-ttu-id="71095-284">Gebruik `MobileServiceIncrementalLoadingCollection` in Windows-apps als volgt:</span><span class="sxs-lookup"><span data-stu-id="71095-284">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="71095-285">toouse nieuwe verzameling op Windows Phone 8 en 'Silverlight' apps, gebruik Hallo Hallo `ToCollection` uitbreidingsmethoden op `IMobileServiceTableQuery<T>` en `IMobileServiceTable<T>`.</span><span class="sxs-lookup"><span data-stu-id="71095-285">toouse hello new collection on Windows Phone 8 and "Silverlight" apps, use hello `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="71095-286">tooload gegevens, roepen `LoadMoreItemsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="71095-286">tooload data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="71095-287">Bij het gebruik van Hallo-verzameling gemaakt door het aanroepen van `ToCollectionAsync` of `ToCollection`, ophalen van een verzameling die gebonden tooUI besturingselementen worden kan.</span><span class="sxs-lookup"><span data-stu-id="71095-287">When you use hello collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound tooUI controls.</span></span>  <span data-ttu-id="71095-288">Deze verzameling is paginering-bewust.</span><span class="sxs-lookup"><span data-stu-id="71095-288">This collection is paging-aware.</span></span>  <span data-ttu-id="71095-289">Aangezien Hallo verzameling gegevens worden geladen vanaf het netwerk, soms laden is mislukt.</span><span class="sxs-lookup"><span data-stu-id="71095-289">Since hello collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="71095-290">toohandle dergelijke fouten negeren Hallo `OnException` methode op `MobileServiceIncrementalLoadingCollection` toohandle uitzonderingen ten gevolge van aanroepen te`LoadMoreItemsAsync`.</span><span class="sxs-lookup"><span data-stu-id="71095-290">toohandle such failures, override hello `OnException` method on `MobileServiceIncrementalLoadingCollection` toohandle exceptions resulting from calls too`LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="71095-291">Overweeg als de tabel veel velden heeft, maar u wilt dat alleen toodisplay enkele ervan in het besturingselement.</span><span class="sxs-lookup"><span data-stu-id="71095-291">Consider if your table has many fields but you only want toodisplay some of them in your control.</span></span> <span data-ttu-id="71095-292">Hallo richtlijnen kunt u in de voorgaande sectie Hallo '[specifieke kolommen selecteren](#selecting)' tooselect specifieke kolommen toodisplay in Hallo gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="71095-292">You may use hello guidance in hello preceding section "[Select specific columns](#selecting)" tooselect specific columns toodisplay in hello UI.</span></span>

### <span data-ttu-id="71095-293"><a name="pagesize"></a>Wijziging Hallo paginagrootte</span><span class="sxs-lookup"><span data-stu-id="71095-293"><a name="pagesize"></a>Change hello Page size</span></span>
<span data-ttu-id="71095-294">Azure Mobile Apps retourneert een maximum van 50 items per aanvraag standaard.</span><span class="sxs-lookup"><span data-stu-id="71095-294">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="71095-295">U kunt Hallo paginering grootte wijzigen door het verhogen van de maximale paginagrootte Hallo op Hallo-client en server.</span><span class="sxs-lookup"><span data-stu-id="71095-295">You can change hello paging size by increasing hello maximum page size on both hello client and server.</span></span>  <span data-ttu-id="71095-296">tooincrease Hallo van de grootte van de aangevraagde pagina, geef `PullOptions` bij gebruik van `PullAsync()`:</span><span class="sxs-lookup"><span data-stu-id="71095-296">tooincrease hello requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="71095-297">Ervan uitgaande dat u hebt aangebracht Hallo `PageSize` gelijk tooor groter zijn dan 100 binnen Hallo-server een aanvraag maximaal 100 items geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="71095-297">Assuming you have made hello `PageSize` equal tooor greater than 100 within hello server, a request returns up to 100 items.</span></span>

## <span data-ttu-id="71095-298"><a name="#offlinesync"></a>Werken met Offline tabellen</span><span class="sxs-lookup"><span data-stu-id="71095-298"><a name="#offlinesync"></a>Work with Offline Tables</span></span>
<span data-ttu-id="71095-299">Een lokale SQLite store toostore gegevens offline tabellen gebruiken voor gebruik wanneer u offline bent.</span><span class="sxs-lookup"><span data-stu-id="71095-299">Offline tables use a local SQLite store toostore data for use when offline.</span></span>  <span data-ttu-id="71095-300">Alle tabel bewerkingen worden uitgevoerd voor Hallo lokale SQLite opslaan in plaats van het archief van de externe server Hallo.</span><span class="sxs-lookup"><span data-stu-id="71095-300">All table operations are done against hello local SQLite store instead of hello remote server store.</span></span>  <span data-ttu-id="71095-301">toocreate een offline tabel eerst uw project voorbereiden:</span><span class="sxs-lookup"><span data-stu-id="71095-301">toocreate an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="71095-302">In Visual Studio met de rechtermuisknop op Hallo oplossing > **NuGet-pakketten beheren voor oplossing...** , zoek vervolgens naar en installeren de **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet-pakket voor alle projecten in Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="71095-302">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="71095-303">Windows-apparaten (optioneel) toosupport, installeert u een Hallo SQLite runtime pakketten te volgen:</span><span class="sxs-lookup"><span data-stu-id="71095-303">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="71095-304">**Windows 8.1 Runtime:** installeren [SQLite voor Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="71095-304">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="71095-305">**Windows Phone 8.1:** installeren [SQLite voor Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="71095-305">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="71095-306">**Universele Windows-Platform** installeren [SQLite voor universele Windows hello][5].</span><span class="sxs-lookup"><span data-stu-id="71095-306">**Universal Windows Platform** Install [SQLite for hello Universal Windows][5].</span></span>
3. <span data-ttu-id="71095-307">(Optioneel).</span><span class="sxs-lookup"><span data-stu-id="71095-307">(Optional).</span></span> <span data-ttu-id="71095-308">Voor Windows-apparaten, klikt u op **verwijzingen** > **verwijzing toevoegen...** , vouw Hallo **Windows** map > **extensies**, schakel vervolgens de juiste Hallo **SQLite voor Windows** SDK samen met de Hallo  **Visual C++ 2013-Runtime voor Windows** SDK.</span><span class="sxs-lookup"><span data-stu-id="71095-308">For Windows devices, click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**, then enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="71095-309">Hallo verschillen SQLite SDK namen met elke Windows-platform.</span><span class="sxs-lookup"><span data-stu-id="71095-309">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="71095-310">Voordat een tabelverwijzing kan worden gemaakt, moet het lokale archief Hallo worden voorbereid:</span><span class="sxs-lookup"><span data-stu-id="71095-310">Before a table reference can be created, hello local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="71095-311">Initialiseren van de wordt normaal uitgevoerd onmiddellijk nadat het Hallo-client wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="71095-311">Store initialization is normally done immediately after hello client is created.</span></span>  <span data-ttu-id="71095-312">Hallo **OfflineDbPath** moet een bestandsnaam hebben die geschikt zijn voor gebruik op alle platforms die u ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="71095-312">hello **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="71095-313">Als het Hallo-pad is een volledig gekwalificeerde pad (dat wil zeggen, begint met een slash), wordt dat pad gebruikt.</span><span class="sxs-lookup"><span data-stu-id="71095-313">If hello path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="71095-314">Als Hallo pad niet volledig opgegeven is, wordt Hallo-bestand in een platform-specifieke locatie geplaatst.</span><span class="sxs-lookup"><span data-stu-id="71095-314">If hello path is not fully qualified, hello file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="71095-315">Voor iOS en Android-apparaten is het standaardpad Hallo Hallo 'Persoonlijke bestanden' map.</span><span class="sxs-lookup"><span data-stu-id="71095-315">For iOS and Android devices, hello default path is hello "Personal Files" folder.</span></span>
* <span data-ttu-id="71095-316">Voor Windows-apparaten is het standaardpad Hallo Hallo toepassingsspecifieke 'AppData' map.</span><span class="sxs-lookup"><span data-stu-id="71095-316">For Windows devices, hello default path is hello application-specific "AppData" folder.</span></span>

<span data-ttu-id="71095-317">Een tabelverwijzing kan worden verkregen met Hallo `GetSyncTable<>` methode:</span><span class="sxs-lookup"><span data-stu-id="71095-317">A table reference can be obtained using hello `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="71095-318">U hoeft niet tooauthenticate toouse een offline-tabel.</span><span class="sxs-lookup"><span data-stu-id="71095-318">You do not need tooauthenticate toouse an offline table.</span></span>  <span data-ttu-id="71095-319">U hoeft alleen tooauthenticate wanneer u met de Hallo back-endservice communiceert.</span><span class="sxs-lookup"><span data-stu-id="71095-319">You only need tooauthenticate when you are communicating with hello backend service.</span></span>

### <span data-ttu-id="71095-320"><a name="syncoffline"></a>Synchroniseren van een Offline-tabel</span><span class="sxs-lookup"><span data-stu-id="71095-320"><a name="syncoffline"></a>Syncing an Offline Table</span></span>
<span data-ttu-id="71095-321">Offline tabellen zijn niet gesynchroniseerd met Hallo back-end standaard.</span><span class="sxs-lookup"><span data-stu-id="71095-321">Offline tables are not synchronized with hello backend by default.</span></span>  <span data-ttu-id="71095-322">Synchronisatie is opgesplitst in twee delen.</span><span class="sxs-lookup"><span data-stu-id="71095-322">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="71095-323">U kunt wijzigingen afzonderlijk forceren nieuwe items worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="71095-323">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="71095-324">Hier volgt een typisch synchronisatiemethode:</span><span class="sxs-lookup"><span data-stu-id="71095-324">Here is a typical sync method:</span></span>

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //hello first parameter is a query name that is used internally by hello client SDK tooimplement incremental sync.
            //Use a different query name for each unique query in your program
            "allTodoItems",
            this.todoTable.CreateQuery());
    }
    catch (MobileServicePushFailedException exc)
    {
        if (exc.PushResult != null)
        {
            syncErrors = exc.PushResult.Errors;
        }
    }

    // Simple error/conflict handling. A real application would handle hello various errors like network conditions,
    // server conflicts and others via hello IMobileServiceSyncHandler.
    if (syncErrors != null)
    {
        foreach (var error in syncErrors)
        {
            if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
            {
                //Update failed, reverting tooserver's copy.
                await error.CancelAndUpdateItemAsync(error.Result);
            }
            else
            {
                // Discard local change.
                await error.CancelAndDiscardItemAsync();
            }

            Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.", error.TableName, error.Item["id"]);
        }
    }
}
```

<span data-ttu-id="71095-325">Als eerste argument te Hallo`PullAsync` null incrementele synchronisatie wordt niet gebruikt.</span><span class="sxs-lookup"><span data-stu-id="71095-325">If hello first argument too`PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="71095-326">Elke synchronisatiebewerking haalt alle records.</span><span class="sxs-lookup"><span data-stu-id="71095-326">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="71095-327">Hallo SDK voert een impliciete `PushAsync()` voordat binnenhalen van records.</span><span class="sxs-lookup"><span data-stu-id="71095-327">hello SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="71095-328">Conflict verwerking wordt uitgevoerd op een `PullAsync()` methode.</span><span class="sxs-lookup"><span data-stu-id="71095-328">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="71095-329">U kunt bekommeren om conflicten in Hallo dezelfde manier als online-tabellen.</span><span class="sxs-lookup"><span data-stu-id="71095-329">You can deal with conflicts in hello same way as online tables.</span></span>  <span data-ttu-id="71095-330">Hallo conflict wordt gemaakt wanneer `PullAsync()` wordt aangeroepen in plaats van tijdens het Hallo insert, update of delete.</span><span class="sxs-lookup"><span data-stu-id="71095-330">hello conflict is produced when `PullAsync()` is called instead of during hello insert, update, or delete.</span></span> <span data-ttu-id="71095-331">Als meerdere conflicten optreden, worden ze in een enkel MobileServicePushFailedException gebundeld.</span><span class="sxs-lookup"><span data-stu-id="71095-331">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="71095-332">Elke fout afzonderlijk verwerkt.</span><span class="sxs-lookup"><span data-stu-id="71095-332">Handle each failure separately.</span></span>

## <span data-ttu-id="71095-333"><a name="#customapi"></a>Werken met een aangepaste API gebruiken</span><span class="sxs-lookup"><span data-stu-id="71095-333"><a name="#customapi"></a>Work with a custom API</span></span>
<span data-ttu-id="71095-334">Een aangepaste API kunt u toodefine aangepaste eindpunten die serverfunctionaliteit weergeven die geen toewijzen tooan invoegen, bijwerken, verwijderen of leesbewerking.</span><span class="sxs-lookup"><span data-stu-id="71095-334">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="71095-335">Met behulp van een aangepaste API gebruiken, kunt u meer controle over messaging, hebben waaronder lezen en HTTP-bericht headers instellen en definiëren van een berichttekst de indeling dan JSON.</span><span class="sxs-lookup"><span data-stu-id="71095-335">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="71095-336">U een aangepaste API aanroepen door een Hallo [InvokeApiAsync] methoden op Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="71095-336">You call a custom API by calling one of hello [InvokeApiAsync] methods on hello client.</span></span> <span data-ttu-id="71095-337">Hallo volgende regel code verzendt bijvoorbeeld een POST-aanvraag toohello **completeAll** API op Hallo back-end:</span><span class="sxs-lookup"><span data-stu-id="71095-337">For example, hello following line of code sends a POST request toohello **completeAll** API on hello backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="71095-338">Dit formulier is een methodeaanroep getypte en vereist dat Hallo **MarkAllResult** retourneren type is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="71095-338">This form is a typed method call and requires that hello **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="71095-339">Getypte en niet-getypeerde methoden worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="71095-339">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="71095-340">Hallo InvokeApiAsync() methode voegt toe toohello API/api/u wenst toocall tenzij Hallo API met begint een '/'.</span><span class="sxs-lookup"><span data-stu-id="71095-340">hello InvokeApiAsync() method prepends '/api/' toohello API that you wish toocall unless hello API starts with a '/'.</span></span>
<span data-ttu-id="71095-341">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="71095-341">For example:</span></span>

* <span data-ttu-id="71095-342">`InvokeApiAsync("completeAll",...)`/api/completeAll aanroepen op Hallo back-end</span><span class="sxs-lookup"><span data-stu-id="71095-342">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on hello backend</span></span>
* <span data-ttu-id="71095-343">`InvokeApiAsync("/.auth/me",...)`/.auth/me aanroepen op Hallo back-end</span><span class="sxs-lookup"><span data-stu-id="71095-343">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on hello backend</span></span>

<span data-ttu-id="71095-344">U kunt WebAPI, met inbegrip van deze WebAPIs die niet zijn gedefinieerd met Azure Mobile Apps InvokeApiAsync toocall.</span><span class="sxs-lookup"><span data-stu-id="71095-344">You can use InvokeApiAsync toocall any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="71095-345">Wanneer u InvokeApiAsync() gebruikt, worden met Hallo aanvraag Hallo juiste headers, waaronder verificatieheaders, verzonden.</span><span class="sxs-lookup"><span data-stu-id="71095-345">When you use InvokeApiAsync(), hello appropriate headers, including authentication headers, are sent with hello request.</span></span>

## <span data-ttu-id="71095-346"><a name="authentication"></a>Verificatie van gebruikers</span><span class="sxs-lookup"><span data-stu-id="71095-346"><a name="authentication"></a>Authenticate users</span></span>
<span data-ttu-id="71095-347">Mobiele Apps biedt ondersteuning voor verificatie en autorisatie van app-gebruikers met behulp van verschillende externe id-providers: Facebook, Google, Microsoft-Account, Twitter en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="71095-347">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="71095-348">U kunt machtigingen instellen voor tabellen toorestrict toegang voor specifieke bewerkingen tooonly geverifieerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="71095-348">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="71095-349">U kunt ook Hallo identiteit van autorisatieregels voor geverifieerde gebruikers tooimplement in server-scripts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="71095-349">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="71095-350">Zie voor meer informatie, Hallo zelfstudie [toevoegen verificatie tooyour app].</span><span class="sxs-lookup"><span data-stu-id="71095-350">For more information, see hello tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="71095-351">Twee verificatie stromen worden ondersteund: *client beheerd* en *server beheerd* stroom.</span><span class="sxs-lookup"><span data-stu-id="71095-351">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="71095-352">Hallo server beheerd stroom biedt Hallo eenvoudigste verificatie-ervaring, is afhankelijk van de webinterface verificatie Hallo-provider.</span><span class="sxs-lookup"><span data-stu-id="71095-352">hello server-managed flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="71095-353">Hallo client beheerd stroom kan voor de diepgaande integratie met apparaatspecifieke mogelijkheden, zoals is afhankelijk van de provider-specifieke apparaat-specifieke SDK's.</span><span class="sxs-lookup"><span data-stu-id="71095-353">hello client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="71095-354">U wordt aangeraden met behulp van een stroom client beheerd in uw productie-apps.</span><span class="sxs-lookup"><span data-stu-id="71095-354">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="71095-355">tooset van verificatie, moet u uw app registreren bij een of meer id-providers.</span><span class="sxs-lookup"><span data-stu-id="71095-355">tooset up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="71095-356">Hallo-identiteitsprovider genereert een client-ID en een clientgeheim voor uw app.</span><span class="sxs-lookup"><span data-stu-id="71095-356">hello identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="71095-357">Deze waarden worden vervolgens ingesteld in uw back-end tooenable Azure App Service-verificatie/autorisatie.</span><span class="sxs-lookup"><span data-stu-id="71095-357">These values are then set in your backend tooenable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="71095-358">Volg voor meer informatie Hallo gedetailleerde instructies in de zelfstudie [toevoegen verificatie tooyour app].</span><span class="sxs-lookup"><span data-stu-id="71095-358">For more information, follow hello detailed instructions in the tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="71095-359">Hallo volgende onderwerpen worden in deze sectie behandeld:</span><span class="sxs-lookup"><span data-stu-id="71095-359">hello following topics are covered in this section:</span></span>

* [<span data-ttu-id="71095-360">Verificatie van client beheerd</span><span class="sxs-lookup"><span data-stu-id="71095-360">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="71095-361">Beheerde server-verificatie</span><span class="sxs-lookup"><span data-stu-id="71095-361">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="71095-362">In het cachegeheugen Hallo-verificatietoken</span><span class="sxs-lookup"><span data-stu-id="71095-362">Caching hello authentication token</span></span>](#caching)

### <span data-ttu-id="71095-363"><a name="clientflow"></a>Verificatie van client beheerd</span><span class="sxs-lookup"><span data-stu-id="71095-363"><a name="clientflow"></a>Client-managed authentication</span></span>
<span data-ttu-id="71095-364">Uw app kan onafhankelijk contact Hallo id-provider en geef vervolgens Hallo geretourneerde token tijdens het aanmelden met uw back-end.</span><span class="sxs-lookup"><span data-stu-id="71095-364">Your app can independently contact hello identity provider and then provide hello returned token during login with your backend.</span></span> <span data-ttu-id="71095-365">Deze stroom client kunt u een ervaring voor eenmalige aanmelding voor gebruikers of tooretrieve extra gebruikersgegevens van de identiteitsprovider Hallo tooprovide.</span><span class="sxs-lookup"><span data-stu-id="71095-365">This client flow enables you tooprovide a single sign-on experience for users or tooretrieve additional user data from hello identity provider.</span></span> <span data-ttu-id="71095-366">Verificatie van de stroom is voorkeur toousing een stroom server als Hallo identiteitsprovider SDK een meer systeemeigen UX idee biedt en kunt u extra aanpassingen.</span><span class="sxs-lookup"><span data-stu-id="71095-366">Client flow authentication is preferred toousing a server flow as hello identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="71095-367">Voorbeelden zijn bedoeld voor Hallo-stroom verificatie patronen te volgen:</span><span class="sxs-lookup"><span data-stu-id="71095-367">Examples are provided for hello following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="71095-368">Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="71095-368">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="71095-369">Facebook of Google</span><span class="sxs-lookup"><span data-stu-id="71095-369">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="71095-370">Live SDK</span><span class="sxs-lookup"><span data-stu-id="71095-370">Live SDK</span></span>](#client-livesdk)

#### <span data-ttu-id="71095-371"><a name="adal"></a>Verificatie van gebruikers met Active Directory Authentication Library Hallo</span><span class="sxs-lookup"><span data-stu-id="71095-371"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="71095-372">U kunt Hallo Active Directory Authentication Library (ADAL) tooinitiate gebruikersverificatie van Hallo-client met behulp van Azure Active Directory-verificatie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="71095-372">You can use hello Active Directory Authentication Library (ADAL) tooinitiate user authentication from hello client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="71095-373">Uw mobiele app back-end voor AAD eenmalige aanmelding configureren door de volgende Hallo [hoe tooconfigure App Service voor Active Directory-aanmelding] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="71095-373">Configure your mobile app backend for AAD sign-on by following hello [How tooconfigure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="71095-374">Zorg ervoor dat toocomplete Hallo optionele stap voor het registreren van een systeemeigen clienttoepassing van.</span><span class="sxs-lookup"><span data-stu-id="71095-374">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="71095-375">In Visual Studio of Xamarin Studio, open het project en voeg een verwijzing toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="71095-375">In Visual Studio or Xamarin Studio, open your project and add a reference toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="71095-376">Wanneer u zoekt, omvatten voorlopige versies.</span><span class="sxs-lookup"><span data-stu-id="71095-376">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="71095-377">Hallo code tooyour toepassing te volgen, op basis van toohello platform u toevoegen.</span><span class="sxs-lookup"><span data-stu-id="71095-377">Add hello following code tooyour application, according toohello platform you are using.</span></span> <span data-ttu-id="71095-378">Controleer in elk, Hallo vervangingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="71095-378">In each, make hello following replacements:</span></span>

   * <span data-ttu-id="71095-379">Vervang **INSERT-instantie-hier** met de naam van de Hallo van Hallo tenant waarin u uw toepassing hebt ingericht.</span><span class="sxs-lookup"><span data-stu-id="71095-379">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="71095-380">De indeling moet https://login.microsoftonline.com/contoso.onmicrosoft.com. Deze waarde kan worden gekopieerd vanaf Hallo domein tabblad in uw Azure Active Directory in Hallo [klassieke Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="71095-380">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="71095-381">Vervang **INSERT RESOURCE-ID hier** met Hallo client-ID voor uw back-end voor de mobiele app.</span><span class="sxs-lookup"><span data-stu-id="71095-381">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="71095-382">U kunt Hallo client-ID verkrijgen van Hallo **Geavanceerd** tabblad onder **Azure Active Directory-instellingen** in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="71095-382">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="71095-383">Vervang **INSERT-CLIENT-ID-hier** met client-ID Hallo u hebt gekopieerd uit Hallo native client-toepassing.</span><span class="sxs-lookup"><span data-stu-id="71095-383">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="71095-384">Vervang **INSERT-OMLEIDINGS-URI-hier** aan uw site */.auth/login/done* eindpunt, met Hallo HTTPS-schema.</span><span class="sxs-lookup"><span data-stu-id="71095-384">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="71095-385">Deze waarde moet er ongeveer te*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="71095-385">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="71095-386">Hallo-code die nodig is voor elk platform volgt:</span><span class="sxs-lookup"><span data-stu-id="71095-386">hello code needed for each platform follows:</span></span>

     <span data-ttu-id="71095-387">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="71095-387">**Windows:**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        while (user == null)
        {
            string message;
            try
            {
                AuthenticationContext ac = new AuthenticationContext(authority);
                AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                    new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, false) );
                JObject payload = new JObject();
                payload["access_token"] = ar.AccessToken;
                user = await App.MobileService.LoginAsync(
                    MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
                message = string.Format("You are now logged in - {0}", user.UserId);
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
    ```

     <span data-ttu-id="71095-388">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="71095-388">**Xamarin.iOS**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync(UIViewController view)
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(view));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine(@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
        }
    }
    ```

     <span data-ttu-id="71095-389">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="71095-389">**Xamarin.Android**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(this));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(ex.Message);
            builder.SetTitle("You must log in. Login Required");
            builder.Create().Show();
        }
    }
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {

        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ```

#### <span data-ttu-id="71095-390"><a name="client-facebook"></a>Eenmalige aanmelding met behulp van een token van Facebook of Google</span><span class="sxs-lookup"><span data-stu-id="71095-390"><a name="client-facebook"></a>Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="71095-391">U kunt Hallo stroom kunt gebruiken, zoals weergegeven in dit fragment voor Facebook of Google.</span><span class="sxs-lookup"><span data-stu-id="71095-391">You can use hello client flow as shown in this snippet for Facebook or Google.</span></span>

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using hello Facebook or Google SDK.
token.Add("access_token", "access_token_value");

private MobileServiceUser user;
private async Task AuthenticateAsync()
{
    while (user == null)
    {
        string message;
        try
        {
            // Change MobileServiceAuthenticationProvider.Facebook
            // tooMobileServiceAuthenticationProvider.Google if using Google auth.
            user = await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
            message = string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

#### <span data-ttu-id="71095-392"><a name="client-livesdk"></a>Eenmalige aanmelding met Microsoft-Account met Hallo Live SDK</span><span class="sxs-lookup"><span data-stu-id="71095-392"><a name="client-livesdk"></a>Single Sign On using Microsoft Account with hello Live SDK</span></span>
<span data-ttu-id="71095-393">tooauthenticate gebruikers, moet u uw app op Hallo van Microsoft-account Developer Center registreren.</span><span class="sxs-lookup"><span data-stu-id="71095-393">tooauthenticate users, you must register your app at hello Microsoft account Developer Center.</span></span> <span data-ttu-id="71095-394">Configureer de registratiedetails op uw mobiele App back-end.</span><span class="sxs-lookup"><span data-stu-id="71095-394">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="71095-395">toocreate een Microsoft account is geregistreerd en verbindt u deze back-end van tooyour Mobile Apps, volledige Hallo stappen in [registreren van uw app toouse een Microsoft-account aanmelding].</span><span class="sxs-lookup"><span data-stu-id="71095-395">toocreate a Microsoft account registration and connect it tooyour Mobile App backend, complete hello steps in [Register your app toouse a Microsoft account login].</span></span> <span data-ttu-id="71095-396">Als u zowel de Windows Store en Windows Phone 8/Silverlight-versies van uw app hebt, registreert u eerst Hallo Windows Store-versie.</span><span class="sxs-lookup"><span data-stu-id="71095-396">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register hello Windows Store version first.</span></span>

<span data-ttu-id="71095-397">Hallo volgende code wordt geverifieerd met Live SDK en Hallo token toosign geretourneerd in backend voor mobiele Apps tooyour gebruikt.</span><span class="sxs-lookup"><span data-stu-id="71095-397">hello following code authenticates using Live SDK and uses hello returned token toosign in tooyour Mobile App backend.</span></span>

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get hello URL hello Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create hello authentication client for Windows Store using hello service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create hello authentication client for Windows Phone using hello client ID of hello registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request hello authentication token from hello Live authentication service.
        // hello wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about hello logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use hello Microsoft account auth token toosign in tooApp Service.
            MobileServiceUser loginResult = await App.MobileService
                .LoginWithMicrosoftAccountAsync(result.Session.AuthenticationToken);

            // Display a personalized sign-in greeting.
            string title = string.Format("Welcome {0}!", meResult.Result["first_name"]);
            var message = string.Format("You are now logged in - {0}", loginResult.UserId);
            var dialog = new MessageDialog(message, title);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
        else
        {
            session = null;
            var dialog = new MessageDialog("You must log in.", "Login Required");
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
}
```

<span data-ttu-id="71095-398">Zie voor meer informatie, Hallo [Windows Live SDK] documentatie.</span><span class="sxs-lookup"><span data-stu-id="71095-398">For more information, see hello [Windows Live SDK] documentation.</span></span>

### <span data-ttu-id="71095-399"><a name="serverflow"></a>Beheerde server-verificatie</span><span class="sxs-lookup"><span data-stu-id="71095-399"><a name="serverflow"></a>Server-managed authentication</span></span>
<span data-ttu-id="71095-400">Wanneer u de id-provider hebt geregistreerd, aanroepen Hallo [LoginAsync] methode op Hallo [MobileServiceClient] Hello [MobileServiceAuthenticationProvider] waarde van de provider.</span><span class="sxs-lookup"><span data-stu-id="71095-400">Once you have registered your identity provider, call hello [LoginAsync] method on hello [MobileServiceClient] with hello [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="71095-401">Bijvoorbeeld: hello volgende code initieert een server stroom aanmelden via Facebook.</span><span class="sxs-lookup"><span data-stu-id="71095-401">For example, hello following code initiates a server flow sign-in by using Facebook.</span></span>

```
private MobileServiceUser user;
private async System.Threading.Tasks.Task Authenticate()
{
    while (user == null)
    {
        string message;
        try
        {
            user = await client
                .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
            message =
                string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

<span data-ttu-id="71095-402">Als u van een id-provider dan Facebook gebruikmaakt, wijzigt u de waarde Hallo van [MobileServiceAuthenticationProvider] toohello waarde voor de provider.</span><span class="sxs-lookup"><span data-stu-id="71095-402">If you are using an identity provider other than Facebook, change hello value of [MobileServiceAuthenticationProvider] toohello value for your provider.</span></span>

<span data-ttu-id="71095-403">In een stroom server beheert Azure App Service Hallo OAuth-authenticatiestroom door Hallo aanmeldingspagina van de geselecteerde provider Hallo weer te geven.</span><span class="sxs-lookup"><span data-stu-id="71095-403">In a server flow, Azure App Service manages hello OAuth authentication flow by displaying hello sign-in page of hello selected provider.</span></span>  <span data-ttu-id="71095-404">Hallo-id-provider retourneert, Azure App Service genereert eenmaal een App Service-verificatietoken.</span><span class="sxs-lookup"><span data-stu-id="71095-404">Once hello identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="71095-405">Hallo [LoginAsync] methode retourneert een [MobileServiceUser], waarmee u zowel Hallo [UserId] Hallo geverifieerde gebruiker en Hallo [ MobileServiceAuthenticationToken], als een JSON web token (JWT).</span><span class="sxs-lookup"><span data-stu-id="71095-405">hello [LoginAsync] method returns a [MobileServiceUser], which provides both hello [UserId] of hello authenticated user and hello [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="71095-406">Dit token kan worden opgeslagen in de cache en opnieuw worden gebruikt totdat het verloopt.</span><span class="sxs-lookup"><span data-stu-id="71095-406">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="71095-407">Zie voor meer informatie [opslaan in cache Hallo-verificatietoken](#caching).</span><span class="sxs-lookup"><span data-stu-id="71095-407">For more information, see [Caching hello authentication token](#caching).</span></span>

### <span data-ttu-id="71095-408"><a name="caching"></a>In het cachegeheugen Hallo-verificatietoken</span><span class="sxs-lookup"><span data-stu-id="71095-408"><a name="caching"></a>Caching hello authentication token</span></span>
<span data-ttu-id="71095-409">In sommige gevallen kan na de eerste geslaagde verificatie Hallo doordat Hallo-verificatietoken van Hallo provider toohello Hallo-aanmelding aanroepmethode worden vermeden.</span><span class="sxs-lookup"><span data-stu-id="71095-409">In some cases, hello call toohello login method can be avoided after hello first successful authentication by storing hello authentication token from hello provider.</span></span>  <span data-ttu-id="71095-410">Windows Store en UWP-apps kunt gebruiken [PasswordVault] toocache de huidige verificatie token na een geslaagde aanmelden, als volgt:</span><span class="sxs-lookup"><span data-stu-id="71095-410">Windows Store and UWP apps can use [PasswordVault] toocache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="71095-411">Hallo UserId waarde wordt opgeslagen als gebruikersnaam van de referentie Hallo Hallo en Hallo-token is opgeslagen als Hallo wachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="71095-411">hello UserId value is stored as hello UserName of hello credential and hello token is hello stored as hello Password.</span></span> <span data-ttu-id="71095-412">Op de volgende startende, kunt u controleren Hallo **PasswordVault** voor in cache opgeslagen referenties.</span><span class="sxs-lookup"><span data-stu-id="71095-412">On subsequent start-ups, you can check hello **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="71095-413">Hallo volgende voorbeeld wordt in de cache opgeslagen referenties wanneer ze worden gevonden, en anders probeert tooauthenticate opnieuw met de Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="71095-413">hello following example uses cached credentials when they are found, and otherwise attempts tooauthenticate again with hello backend:</span></span>

```
// Try tooretrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create hello current user from hello stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache hello token as shown above.
}
```

<span data-ttu-id="71095-414">Wanneer u een gebruiker afmelden, moet u Hallo opgeslagen referentie, ook als volgt verwijderen:</span><span class="sxs-lookup"><span data-stu-id="71095-414">When you sign out a user, you must also remove hello stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="71095-415">Xamarin-apps gebruiken Hallo [Xamarin.Auth] referenties voor de gegevensopslag van API's toosecurely in een **Account** object.</span><span class="sxs-lookup"><span data-stu-id="71095-415">Xamarin    apps use hello [Xamarin.Auth] APIs toosecurely store credentials in an **Account** object.</span></span> <span data-ttu-id="71095-416">Zie voor een voorbeeld van het gebruik van deze API's, Hallo [AuthStore.cs] codebestand in Hallo [ContosoMoments photo delen voorbeeld](https://github.com/azure-appservice-samples/ContosoMoments).</span><span class="sxs-lookup"><span data-stu-id="71095-416">For an example of using these APIs, see hello [AuthStore.cs] code file in hello [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="71095-417">Als u client beheerd authenticatie gebruikt, u kunt ook de cache Hallo toegangstoken is verkregen van uw provider zoals Facebook en Twitter.</span><span class="sxs-lookup"><span data-stu-id="71095-417">When you use client-managed authentication, you can also cache hello access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="71095-418">Dit token kan worden opgegeven toorequest verificatietoken voor een nieuwe vanuit Hallo back-end, als volgt:</span><span class="sxs-lookup"><span data-stu-id="71095-418">This token can be supplied toorequest a new authentication token from hello backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <span data-ttu-id="71095-419"><a name="pushnotifications"></a>Pushmeldingen</span><span class="sxs-lookup"><span data-stu-id="71095-419"><a name="pushnotifications"></a>Push Notifications</span></span>
<span data-ttu-id="71095-420">Hallo volgende onderwerpen vindt u Pushmeldingen:</span><span class="sxs-lookup"><span data-stu-id="71095-420">hello following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="71095-421">Registreren voor Pushmeldingen</span><span class="sxs-lookup"><span data-stu-id="71095-421">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="71095-422">Verkrijgen van een pakket-SID van de Windows Store</span><span class="sxs-lookup"><span data-stu-id="71095-422">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="71095-423">Registreren bij platformoverschrijdende sjablonen</span><span class="sxs-lookup"><span data-stu-id="71095-423">Register with Cross-platform templates</span></span>](#register-xplat)

### <span data-ttu-id="71095-424"><a name="register-for-push"></a>How to: registreren voor Pushmeldingen</span><span class="sxs-lookup"><span data-stu-id="71095-424"><a name="register-for-push"></a>How to: Register for Push Notifications</span></span>
<span data-ttu-id="71095-425">Hallo Mobile Apps-client kunt u tooregister voor pushmeldingen met Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="71095-425">hello Mobile Apps client enables you tooregister for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="71095-426">Als u registreert, krijgt u een koppeling die u Hallo platform-specifieke aanschaft Push Notification Service (PNS).</span><span class="sxs-lookup"><span data-stu-id="71095-426">When registering, you obtain a handle that you obtain from hello platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="71095-427">Deze waarde samen met eventuele labels wordt vervolgens opgeven wanneer u Hallo registratie maakt.</span><span class="sxs-lookup"><span data-stu-id="71095-427">You then provide this value along with any tags when you create hello registration.</span></span> <span data-ttu-id="71095-428">Hallo registreert volgende code uw Windows-app voor pushmeldingen Hello Windows Notification Service (WNS):</span><span class="sxs-lookup"><span data-stu-id="71095-428">hello following code registers your Windows app for push notifications with hello Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="71095-429">Als u tooWNS worden gepusht, dan u moet [verkrijgen van een pakket-SID van de Windows Store](#package-sid).</span><span class="sxs-lookup"><span data-stu-id="71095-429">If you are pushing tooWNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="71095-430">Voor meer informatie over Windows-apps, met inbegrip van hoe tooregister voor registraties van de sjabloon zien [Add push notifications tooyour app].</span><span class="sxs-lookup"><span data-stu-id="71095-430">For more information on Windows apps, including how tooregister for template registrations, see [Add push notifications tooyour app].</span></span>

<span data-ttu-id="71095-431">Aanvragen van de labels van Hallo-client wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="71095-431">Requesting tags from hello client is not supported.</span></span>  <span data-ttu-id="71095-432">Tag aanvragen zijn achtergrond verwijderd uit de inschrijving.</span><span class="sxs-lookup"><span data-stu-id="71095-432">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="71095-433">Als u wenst dat tooregister uw apparaat met labels, maakt u een aangepaste API die gebruikmaakt van Hallo Notification Hubs-API tooperform Hallo registratie namens jou.</span><span class="sxs-lookup"><span data-stu-id="71095-433">If you wish tooregister your device with tags, create a Custom API that uses hello Notification Hubs API tooperform hello registration on your behalf.</span></span>  <span data-ttu-id="71095-434">[Hallo aangepaste API aanroepen](#customapi) in plaats van Hallo `RegisterNativeAsync()` methode.</span><span class="sxs-lookup"><span data-stu-id="71095-434">[Call hello Custom API](#customapi) instead of hello `RegisterNativeAsync()` method.</span></span>

### <span data-ttu-id="71095-435"><a name="package-sid"></a>Hoe: verkrijgen van een pakket-SID van de Windows Store</span><span class="sxs-lookup"><span data-stu-id="71095-435"><a name="package-sid"></a>How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="71095-436">Een pakket-SID is nodig voor het inschakelen van pushmeldingen in Windows Store-apps.</span><span class="sxs-lookup"><span data-stu-id="71095-436">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="71095-437">tooreceive een pakket-SID, wordt uw toepassing registreren met Hallo Windows Store.</span><span class="sxs-lookup"><span data-stu-id="71095-437">tooreceive a package SID, register your application with hello Windows Store.</span></span>

<span data-ttu-id="71095-438">tooobtain deze waarde:</span><span class="sxs-lookup"><span data-stu-id="71095-438">tooobtain this value:</span></span>

1. <span data-ttu-id="71095-439">Klik in Visual Studio Solution Explorer met de rechtermuisknop op Hallo Windows Store-app-project, klikt u op **Store** > **App aan Hallo Store koppelen...** .</span><span class="sxs-lookup"><span data-stu-id="71095-439">In Visual Studio Solution Explorer, right-click hello Windows Store app project, click **Store** > **Associate App with hello Store...**.</span></span>
2. <span data-ttu-id="71095-440">Klik in de wizard Hallo op **volgende**, meld u aan met uw Microsoft-account, typ een naam voor uw app in **een nieuwe appnaam reserveren**, klikt u vervolgens op **Reserve**.</span><span class="sxs-lookup"><span data-stu-id="71095-440">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="71095-441">Nadat het Hallo-app-registratie is de naam van de app is gemaakt, selecteer hello, klikt u op **volgende**, en klik vervolgens op **koppelen**.</span><span class="sxs-lookup"><span data-stu-id="71095-441">After hello app registration is successfully created, select hello app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="71095-442">Meld u bij toohello [Windows-ontwikkelaarscentrum] met uw Microsoft-Account.</span><span class="sxs-lookup"><span data-stu-id="71095-442">Log in toohello [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="71095-443">Onder **mijn apps**, klikt u op Hallo app registratie die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="71095-443">Under **My apps**, click hello app registration you created.</span></span>
5. <span data-ttu-id="71095-444">Klik op **appbeheer** > **App identiteit**, en schuif omlaag toofind uw **pakket-SID**.</span><span class="sxs-lookup"><span data-stu-id="71095-444">Click **App management** > **App identity**, and then scroll down toofind your **Package SID**.</span></span>

<span data-ttu-id="71095-445">Vele toepassingen van Hallo pakket-SID behandelen als een URI in dat geval moet u toouse *ms-app: / /* als Hallo schema.</span><span class="sxs-lookup"><span data-stu-id="71095-445">Many uses of hello package SID treat it as a URI, in which case you need toouse *ms-app://* as hello scheme.</span></span> <span data-ttu-id="71095-446">Noteer Hallo-versie van uw pakket-SID gevormd door samenvoeging van deze waarde als voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="71095-446">Make note of hello version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="71095-447">Xamarin-apps nodig enkele aanvullende code toobe kunnen tooregister een app die wordt uitgevoerd op Hallo iOS of Android-platform.</span><span class="sxs-lookup"><span data-stu-id="71095-447">Xamarin apps require some additional code toobe able tooregister an app running on hello iOS or Android platforms.</span></span> <span data-ttu-id="71095-448">Zie voor meer informatie Hallo-onderwerp voor uw platform:</span><span class="sxs-lookup"><span data-stu-id="71095-448">For more information, see hello topic for your platform:</span></span>

* [<span data-ttu-id="71095-449">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="71095-449">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="71095-450">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="71095-450">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <span data-ttu-id="71095-451"><a name="register-xplat"></a>Hoe: Register sjablonen toosend platformoverschrijdende pushmeldingen</span><span class="sxs-lookup"><span data-stu-id="71095-451"><a name="register-xplat"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="71095-452">tooregister sjablonen gebruiken Hallo `RegisterAsync()` methode met Hallo-sjablonen, als volgt:</span><span class="sxs-lookup"><span data-stu-id="71095-452">tooregister templates, use hello `RegisterAsync()` method with hello templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="71095-453">Uw sjablonen moet `JObject` van het type en kan meerdere sjablonen in de volgende JSON-indeling Hallo bevatten:</span><span class="sxs-lookup"><span data-stu-id="71095-453">Your templates should be `JObject` types and can contain multiple templates in hello following JSON format:</span></span>

```
public JObject myTemplates()
{
    // single template for Windows Notification Service toast
    var template = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(message)</text></binding></visual></toast>";

    var templates = new JObject
    {
        ["generic-message"] = new JObject
        {
            ["body"] = template,
            ["headers"] = new JObject
            {
                ["X-WNS-Type"] = "wns/toast"
            },
            ["tags"] = new JArray()
        },
        ["more-templates"] = new JObject {...}
    };
    return templates;
}
```

<span data-ttu-id="71095-454">Hallo methode **RegisterAsync()** accepteert ook secundaire tegels:</span><span class="sxs-lookup"><span data-stu-id="71095-454">hello method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="71095-455">Alle codes zijn te vertalen tijdens de registratie voor beveiliging.</span><span class="sxs-lookup"><span data-stu-id="71095-455">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="71095-456">tooadd tags tooinstallations of sjablonen binnen installaties, Zie [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="71095-456">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="71095-457">toosend meldingen met behulp van deze geregistreerde sjablonen verwijzen toohello [Notification Hubs-API's].</span><span class="sxs-lookup"><span data-stu-id="71095-457">toosend notifications utilizing these registered templates, refer toohello [Notification Hubs APIs].</span></span>

## <span data-ttu-id="71095-458"><a name="misc"></a>Diverse onderwerpen</span><span class="sxs-lookup"><span data-stu-id="71095-458"><a name="misc"></a>Miscellaneous Topics</span></span>
### <span data-ttu-id="71095-459"><a name="errors"></a>Hoe: afhandelen van fouten</span><span class="sxs-lookup"><span data-stu-id="71095-459"><a name="errors"></a>How to: Handle errors</span></span>
<span data-ttu-id="71095-460">Wanneer een fout in Hallo back-end optreedt, Hallo client SDK leidt tot een `MobileServiceInvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="71095-460">When an error occurs in hello backend, hello client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="71095-461">Het volgende voorbeeld wordt getoond hoe toohandle een uitzondering die is geretourneerd door Hallo back-end:</span><span class="sxs-lookup"><span data-stu-id="71095-461">The following example shows how toohandle an exception that is returned by hello backend:</span></span>

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into hello database. When hello operation completes
    // and App Service has assigned an Id, hello item is added toohello CollectionView
    try
    {
        await todoTable.InsertAsync(todoItem);
        items.Add(todoItem);
    }
    catch (MobileServiceInvalidOperationException e)
    {
        // Handle error
    }
}
```

<span data-ttu-id="71095-462">Een ander voorbeeld van moeten omgaan met de foutvoorwaarden vindt u in Hallo [Mobile Apps bestanden voorbeeld].</span><span class="sxs-lookup"><span data-stu-id="71095-462">Another example of dealing with error conditions can be found in hello [Mobile Apps Files Sample].</span></span> <span data-ttu-id="71095-463">De [LoggingHandler] voorbeeld bevat een gemachtigde logboekregistratie handler toolog Hallo aanvragen wordt toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="71095-463">The [LoggingHandler] example provides a logging delegate handler toolog hello requests being made toohello backend.</span></span>

### <span data-ttu-id="71095-464"><a name="headers"></a>Hoe: aanpassen aanvraagheaders</span><span class="sxs-lookup"><span data-stu-id="71095-464"><a name="headers"></a>How to: Customize request headers</span></span>
<span data-ttu-id="71095-465">toosupport uw specifieke app-scenario, moet u mogelijk toocustomize communicatie met Hallo mobiele App back-end.</span><span class="sxs-lookup"><span data-stu-id="71095-465">toosupport your specific app scenario, you might need toocustomize communication with hello Mobile App backend.</span></span> <span data-ttu-id="71095-466">U kunt bijvoorbeeld wilt tooadd een aangepaste header tooevery uitgaande aanvraag of zelfs antwoorden statuscodes wijzigen.</span><span class="sxs-lookup"><span data-stu-id="71095-466">For example, you may want tooadd a custom header tooevery outgoing request or even change responses status codes.</span></span> <span data-ttu-id="71095-467">U kunt een aangepaste [DelegatingHandler], Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="71095-467">You can use a custom [DelegatingHandler], as in hello following example:</span></span>

```
public async Task CallClientWithHandler()
{
    MobileServiceClient client = new MobileServiceClient("AppUrl", new MyHandler());
    IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
    var newItem = new TodoItem { Text = "Hello world", Complete = false };
    await todoTable.InsertAsync(newItem);
}

public class MyHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage>
        SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        // Change hello request-side here based on hello HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do hello request
        var response = await base.SendAsync(request, cancellationToken);

        // Change hello response-side here based on hello HttpResponseMessage

        // Return hello modified response
        return response;
    }
}
```


<!-- Anchors. -->


<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-windows-store-dotnet-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[4]: https://msdn.microsoft.com/en-us/library/azure/mt419521(v=azure.10).aspx
[5]: https://github.com/Azure-Samples
[6]: http://www.newtonsoft.com/json/help/html/Properties_T_Newtonsoft_Json_JsonPropertyAttribute.htm
[7]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[8]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[9]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/
[10]: http://www.symbolsource.org/
[11]: http://www.symbolsource.org/Public/Wiki/Using
[12]: https://msdn.microsoft.com/en-us/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient(v=azure.10).aspx

[toevoegen verificatie tooyour app]: app-service-mobile-windows-store-dotnet-get-started-users.md
[Offline synchroniseren van gegevens in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md
[Add push notifications tooyour app]: app-service-mobile-windows-store-dotnet-get-started-push.md
[registreren van uw app toouse een Microsoft-account aanmelding]: app-service-mobile-how-to-configure-microsoft-authentication.md
[hoe tooconfigure App Service voor Active Directory-aanmelding]: app-service-mobile-how-to-configure-active-directory-authentication.md

<!-- Microsoft URLs. -->
[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx
[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx
[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx
[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx
[ MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx
[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx
[maakt u een niet-getypeerde tabel tooan]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx
[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx
[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx
[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx
[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx
[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx
[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx
[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx
[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx
[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx
[nemen]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx
[Selecteer]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx
[overslaan]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx
[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx
[Gebruikers-id]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx
[waar]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx
[Azure-portal]: https://portal.azure.com/
[klassieke Azure-portal]: https://manage.windowsazure.com/
[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx
[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx
[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx
[Windows-ontwikkelaarscentrum]: https://dev.windows.com/en-us/overview
[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx
[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx
[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
[Notification Hubs-API's]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[Mobile Apps bestanden voorbeeld]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files
[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63

<!-- External URLs -->
[OData v3 documentatie]: http://www.odata.org/documentation/odata-version-3-0/
[Fiddler]: http://www.telerik.com/fiddler
[Json.NET]: http://www.newtonsoft.com/json
[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/
[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
