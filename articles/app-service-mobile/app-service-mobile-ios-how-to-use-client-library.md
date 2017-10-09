---
title: aaaHow tooUse iOS SDK voor Azure Mobile Apps
description: Hoe tooUse iOS SDK voor Azure Mobile Apps
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="ffe2f-103">Hoe tooUse iOS-clientbibliotheek voor Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="ffe2f-103">How tooUse iOS Client Library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="ffe2f-104">Deze handleiding leert u tooperform algemene scenario's met Hallo nieuwste [iOS SDK voor Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="ffe2f-104">This guide teaches you tooperform common scenarios using hello latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="ffe2f-105">Als u nieuwe tooAzure Mobile Apps, eerst voltooien [Azure Mobile Apps Quick Start] toocreate een back-end van een tabel maken en deze te downloaden van een vooraf samengestelde iOS Xcode-project.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="ffe2f-106">In deze handleiding richten we op Hallo clientzijde iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-106">In this guide, we focus on hello client-side iOS SDK.</span></span> <span data-ttu-id="ffe2f-107">toolearn informatie over Hallo van server-side '-SDK voor Hallo back-end, Zie Hallo Server SDK HOWTOs.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-107">toolearn more about hello server-side SDK for hello backend, see hello Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="ffe2f-108">Referentiedocumentatie</span><span class="sxs-lookup"><span data-stu-id="ffe2f-108">Reference documentation</span></span>
<span data-ttu-id="ffe2f-109">Hallo-naslagdocumentatie voor Hallo iOS client SDK bevindt zich hier: [Azure Mobile Apps iOS referentie Client][2].</span><span class="sxs-lookup"><span data-stu-id="ffe2f-109">hello reference documentation for hello iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="ffe2f-110">Ondersteunde Platforms</span><span class="sxs-lookup"><span data-stu-id="ffe2f-110">Supported Platforms</span></span>
<span data-ttu-id="ffe2f-111">Hallo iOS SDK biedt ondersteuning voor Objective-C-projecten, Swift 2.2 projecten en Swift 2.3 projecten voor iOS-versie 8.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-111">hello iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="ffe2f-112">Hallo 'server-flow' verificatie maakt gebruik van een webweergave voor Hallo gebruikersinterface weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-112">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="ffe2f-113">Als het Hallo-apparaat is niet kunnen toopresent een UI WebView en vervolgens een andere verificatiemethode is vereist is die buiten Hallo-bereik van Hallo product.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-113">If hello device is not able toopresent a WebView UI, then another method of authentication is required that is outside hello scope of hello product.</span></span>  
<span data-ttu-id="ffe2f-114">Deze SDK is derhalve niet geschikt voor controle-type of op dezelfde manier beperkte apparaten.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="ffe2f-115"><a name="Setup"></a>Het installatieprogramma en vereisten</span><span class="sxs-lookup"><span data-stu-id="ffe2f-115"><a name="Setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="ffe2f-116">Deze handleiding wordt ervan uitgegaan dat u een back-end hebt gemaakt met een tabel.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="ffe2f-117">Deze handleiding wordt ervan uitgegaan dat Hallo-tabel heeft hetzelfde schema Hallo tabellen in deze zelfstudies.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-117">This guide assumes that hello table has the same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="ffe2f-118">Deze handleiding wordt ervan uitgegaan dat in uw code u verwijzen naar `MicrosoftAzureMobile.framework` en importeer `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <span data-ttu-id="ffe2f-119"><a name="create-client"></a>How to: Client maken</span><span class="sxs-lookup"><span data-stu-id="ffe2f-119"><a name="create-client"></a>How to: Create Client</span></span>
<span data-ttu-id="ffe2f-120">Maak een back-end van Azure Mobile Apps in uw project tooaccess een `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-120">tooaccess an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="ffe2f-121">Vervang `AppUrl` met Hallo app-URL.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-121">Replace `AppUrl` with hello app URL.</span></span> <span data-ttu-id="ffe2f-122">U laten `gatewayURLString` en `applicationKey` leeg.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="ffe2f-123">Als u een gateway voor verificatie instelt, vullen `gatewayURLString` met Hallo gateway URL.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-123">If you set up a gateway for authentication, populate `gatewayURLString` with hello gateway URL.</span></span>

<span data-ttu-id="ffe2f-124">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-124">**Objective-C**:</span></span>

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="ffe2f-125">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-125">**Swift**:</span></span>

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <span data-ttu-id="ffe2f-126"><a name="table-reference"></a>How to: tabelverwijzing maken</span><span class="sxs-lookup"><span data-stu-id="ffe2f-126"><a name="table-reference"></a>How to: Create Table Reference</span></span>
<span data-ttu-id="ffe2f-127">tooaccess of update gegevens, maken een verwijzing toohello back-end-tabel.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-127">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="ffe2f-128">Vervang `TodoItem` met de naam van de tabel Hallo</span><span class="sxs-lookup"><span data-stu-id="ffe2f-128">Replace `TodoItem` with hello name of your table</span></span>

<span data-ttu-id="ffe2f-129">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-129">**Objective-C**:</span></span>

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="ffe2f-130">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-130">**Swift**:</span></span>

```
let table = client.tableWithName("TodoItem")
```


## <span data-ttu-id="ffe2f-131"><a name="querying"></a>Procedure: een Query over gegevens</span><span class="sxs-lookup"><span data-stu-id="ffe2f-131"><a name="querying"></a>How to: Query Data</span></span>
<span data-ttu-id="ffe2f-132">toocreate een databasequery query Hallo `MSTable` object.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-132">toocreate a database query, query hello `MSTable` object.</span></span> <span data-ttu-id="ffe2f-133">Hallo volgende query haalt alle Hallo items in `TodoItem` en logboeken Hallo tekst van elk item.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-133">hello following query gets all hello items in `TodoItem` and logs hello text of each item.</span></span>

<span data-ttu-id="ffe2f-134">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-134">**Objective-C**:</span></span>

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="ffe2f-135">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-135">**Swift**:</span></span>

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="ffe2f-136"><a name="filtering"></a>How to: Filter gegevens geretourneerd</span><span class="sxs-lookup"><span data-stu-id="ffe2f-136"><a name="filtering"></a>How to: Filter Returned Data</span></span>
<span data-ttu-id="ffe2f-137">toofilter resultaten, er zijn veel opties beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-137">toofilter results, there are many available options.</span></span>

<span data-ttu-id="ffe2f-138">met behulp van een predicaat, gebruik toofilter een `NSPredicate` en `readWithPredicate`.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-138">toofilter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="ffe2f-139">Hallo volgende filtert geretourneerde gegevens toofind alleen onvolledige Todo-items.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-139">hello following filters returned data toofind only incomplete Todo items.</span></span>

<span data-ttu-id="ffe2f-140">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-140">**Objective-C**:</span></span>

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="ffe2f-141">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-141">**Swift**:</span></span>

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="ffe2f-142"><a name="query-object"></a>How to: MSQuery gebruiken</span><span class="sxs-lookup"><span data-stu-id="ffe2f-142"><a name="query-object"></a>How to: Use MSQuery</span></span>
<span data-ttu-id="ffe2f-143">tooperform maken van een complexe query's (inclusief sortering en paginering), een `MSQuery` object, rechtstreeks of via een predikaat:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-143">tooperform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="ffe2f-144">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-144">**Objective-C**:</span></span>

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="ffe2f-145">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-145">**Swift**:</span></span>

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="ffe2f-146">`MSQuery`kunt u verschillende query gedrag bepalen.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="ffe2f-147">Geef de volgorde van resultaten</span><span class="sxs-lookup"><span data-stu-id="ffe2f-147">Specify order of results</span></span>
* <span data-ttu-id="ffe2f-148">Welke velden tooreturn beperken</span><span class="sxs-lookup"><span data-stu-id="ffe2f-148">Limit which fields tooreturn</span></span>
* <span data-ttu-id="ffe2f-149">Hoeveel records tooreturn beperken</span><span class="sxs-lookup"><span data-stu-id="ffe2f-149">Limit how many records tooreturn</span></span>
* <span data-ttu-id="ffe2f-150">Totaal aantal opgeven om in het antwoord</span><span class="sxs-lookup"><span data-stu-id="ffe2f-150">Specify total count in response</span></span>
* <span data-ttu-id="ffe2f-151">Aangepaste queryreeksparameters in aanvraag opgeven</span><span class="sxs-lookup"><span data-stu-id="ffe2f-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="ffe2f-152">Aanvullende functies toepassen</span><span class="sxs-lookup"><span data-stu-id="ffe2f-152">Apply additional functions</span></span>

<span data-ttu-id="ffe2f-153">Uitvoeren van een `MSQuery` query door het aanroepen van `readWithCompletion` op Hallo-object.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-153">Execute an `MSQuery` query by calling `readWithCompletion` on hello object.</span></span>

## <span data-ttu-id="ffe2f-154"><a name="sorting"></a>How to: gegevens met MSQuery sorteren</span><span class="sxs-lookup"><span data-stu-id="ffe2f-154"><a name="sorting"></a>How to: Sort Data with MSQuery</span></span>
<span data-ttu-id="ffe2f-155">toosort resultaten, bekijk een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-155">toosort results, let's look at an example.</span></span> <span data-ttu-id="ffe2f-156">toosort op het veld 'text' oplopende, vervolgens op het 'complete' aflopende aanroepen `MSQuery` als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-156">toosort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="ffe2f-157">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-157">**Objective-C**:</span></span>

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="ffe2f-158">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-158">**Swift**:</span></span>

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <span data-ttu-id="ffe2f-159"><a name="selecting"></a><a name="parameters"></a>How to: beperken van velden en vouw queryreeksparameters met MSQuery</span><span class="sxs-lookup"><span data-stu-id="ffe2f-159"><a name="selecting"></a><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>
<span data-ttu-id="ffe2f-160">toolimit velden toobe geretourneerd in een query opgeven Hallo namen van Hallo velden in Hallo **selectFields** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-160">toolimit fields toobe returned in a query, specify hello names of hello fields in hello **selectFields** property.</span></span> <span data-ttu-id="ffe2f-161">In dit voorbeeld retourneert alleen tekst hello en voltooide velden:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-161">This example returns only hello text and completed fields:</span></span>

<span data-ttu-id="ffe2f-162">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-162">**Objective-C**:</span></span>

```
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="ffe2f-163">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-163">**Swift**:</span></span>

```
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="ffe2f-164">de aanvullende queryreeksparameters tooinclude in Hallo-server aanvragen (bijvoorbeeld omdat ze maakt gebruik van een aangepast script van de server-side), vullen `query.parameters` als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-164">tooinclude additional query string parameters in hello server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="ffe2f-165">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-165">**Objective-C**:</span></span>

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="ffe2f-166">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-166">**Swift**:</span></span>

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <span data-ttu-id="ffe2f-167"><a name="paging"></a>How to: paginaformaat configureren</span><span class="sxs-lookup"><span data-stu-id="ffe2f-167"><a name="paging"></a>How to: Configure Page Size</span></span>
<span data-ttu-id="ffe2f-168">Met Azure Mobile Apps Hallo Hallo grootte paginabesturingselementen aantal records dat tegelijk uit Hallo back-end tabellen worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-168">With Azure Mobile Apps, hello page size controls hello number of records that are pulled at a time from hello backend tables.</span></span> <span data-ttu-id="ffe2f-169">Een gesprek te starten`pull` gegevens zou vervolgens batch-up van gegevens, op basis van dit paginaformaat totdat er geen meer records toopull.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-169">A call too`pull` data would then batch up data, based on this page size, until there are no more records toopull.</span></span>

<span data-ttu-id="ffe2f-170">Het is mogelijk tooconfigure een pagina grootte met **MSPullSettings** zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-170">It's possible tooconfigure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="ffe2f-171">Hallo standaardpaginaformaat 50 en Hallo in het volgende voorbeeld wordt too3.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-171">hello default page size is 50, and hello example below changes it too3.</span></span>

<span data-ttu-id="ffe2f-172">U kunt een ander paginaformaat Prestatieoverwegingen configureren.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="ffe2f-173">Als er een groot aantal kleine gegevensrecords, vermindert een hoge paginaformaat Hallo aantal retouren van de server.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-173">If you have a large number of small data records, a high page size reduces hello number of server round-trips.</span></span>

<span data-ttu-id="ffe2f-174">Deze instelling bepaalt alleen Hallo paginagrootte aan clientzijde Hallo.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-174">This setting controls only hello page size on hello client side.</span></span> <span data-ttu-id="ffe2f-175">Als Hallo client om een pagina groter vraagt dan het Hallo Mobile Apps-back-end wordt ondersteund, is het paginaformaat Hallo beperkt tot Hallo maximale Hallo backend geconfigureerde toosupport is.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-175">If hello client asks for a larger page size than hello Mobile Apps backend supports, hello page size is capped at hello maximum hello backend is configured toosupport.</span></span>

<span data-ttu-id="ffe2f-176">Deze instelling is ook Hallo *getal* van records met gegevens niet Hallo *bytegrootte*.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-176">This setting is also hello *number* of data records, not hello *byte size*.</span></span>

<span data-ttu-id="ffe2f-177">Als u Hallo client paginagrootte verhoogt, moet u ook de paginagrootte Hallo op Hallo server verhogen.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-177">If you increase hello client page size, you should also increase hello page size on hello server.</span></span> <span data-ttu-id="ffe2f-178">Zie [' How to: Hallo tabel paginering grootte aanpassen '](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) voor Hallo toodo dit stappen.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-178">See ["How to: Adjust hello table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for hello steps toodo this.</span></span>

<span data-ttu-id="ffe2f-179">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-179">**Objective-C**:</span></span>

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


<span data-ttu-id="ffe2f-180">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-180">**Swift**:</span></span>

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <span data-ttu-id="ffe2f-181"><a name="inserting"></a>How to: gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="ffe2f-181"><a name="inserting"></a>How to: Insert Data</span></span>
<span data-ttu-id="ffe2f-182">maken van een nieuwe tabelrij tooinsert een `NSDictionary` en oproepen `table insert`.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-182">tooinsert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="ffe2f-183">Als [dynamische Schema] is ingeschakeld, hello Azure App Service mobiele back-end genereert automatisch nieuwe kolommen die zijn gebaseerd op Hallo `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-183">If [Dynamic Schema] is enabled, hello Azure App Service mobile backend automatically generates new columns based on hello `NSDictionary`.</span></span>

<span data-ttu-id="ffe2f-184">Als `id` is niet opgegeven Hallo back-end automatisch een nieuwe unieke ID genereert.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-184">If `id` is not provided, hello backend automatically generates a new unique ID.</span></span> <span data-ttu-id="ffe2f-185">Geef uw eigen `id` toouse e-adressen, gebruikersnamen of uw eigen aangepaste waarden als de ID.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-185">Provide your own `id` toouse email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="ffe2f-186">Uw eigen ID bieden gemakkelijker joins en database zakelijke logica.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="ffe2f-187">Hallo `result` bevat nieuwe Hallo-item dat is ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-187">hello `result` contains hello new item that was inserted.</span></span> <span data-ttu-id="ffe2f-188">Afhankelijk van de logische server wellicht aanvullende of gewijzigde gegevens vergeleken toowhat toohello server is doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-188">Depending on your server logic, it may have additional or modified data compared toowhat was passed toohello server.</span></span>

<span data-ttu-id="ffe2f-189">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-189">**Objective-C**:</span></span>

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="ffe2f-190">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-190">**Swift**:</span></span>

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <span data-ttu-id="ffe2f-191"><a name="modifying"></a>How to: gegevens wijzigen</span><span class="sxs-lookup"><span data-stu-id="ffe2f-191"><a name="modifying"></a>How to: Modify Data</span></span>
<span data-ttu-id="ffe2f-192">een bestaande rij tooupdate wijzigen een item en de aanroep `update`:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-192">tooupdate an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="ffe2f-193">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-193">**Objective-C**:</span></span>

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="ffe2f-194">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-194">**Swift**:</span></span>

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

<span data-ttu-id="ffe2f-195">U kunt ook Hallo rij-ID en het Hallo bijgewerkt veld opgeven:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-195">Alternatively, supply hello row ID and hello updated field:</span></span>

<span data-ttu-id="ffe2f-196">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-196">**Objective-C**:</span></span>

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="ffe2f-197">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-197">**Swift**:</span></span>

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="ffe2f-198">Ten minste Hallo `id` kenmerk moet worden ingesteld bij het maken van updates.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-198">At minimum, hello `id` attribute must be set when making updates.</span></span>

## <span data-ttu-id="ffe2f-199"><a name="deleting"></a>How to: gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="ffe2f-199"><a name="deleting"></a>How to: Delete Data</span></span>
<span data-ttu-id="ffe2f-200">aanroepen van toodelete een item, `delete` met Hallo item:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-200">toodelete an item, invoke `delete` with hello item:</span></span>

<span data-ttu-id="ffe2f-201">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-201">**Objective-C**:</span></span>

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="ffe2f-202">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-202">**Swift**:</span></span>

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="ffe2f-203">U kunt ook verwijderen door op te geven van een rij-ID:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="ffe2f-204">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-204">**Objective-C**:</span></span>

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="ffe2f-205">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-205">**Swift**:</span></span>

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="ffe2f-206">Ten minste Hallo `id` kenmerk moet worden ingesteld wanneer u wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-206">At minimum, hello `id` attribute must be set when making deletes.</span></span>

## <span data-ttu-id="ffe2f-207"><a name="customapi"></a>How to: aangepaste API aanroepen</span><span class="sxs-lookup"><span data-stu-id="ffe2f-207"><a name="customapi"></a>How to: Call Custom API</span></span>
<span data-ttu-id="ffe2f-208">Met een aangepaste API kan geen back-end-functies worden blootgesteld.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="ffe2f-209">Heeft geen toomap tooa tabel bewerking.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-209">It doesn't have toomap tooa table operation.</span></span> <span data-ttu-id="ffe2f-210">Niet alleen doet u meer controle krijgen over messaging, maar u kunt zelfs lezen/set headers en het Hallo-antwoordindeling hoofdtekst wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-210">Not only do you gain more control over messaging, you can even read/set headers and change hello response body format.</span></span> <span data-ttu-id="ffe2f-211">hoe toocreate aangepaste API op Hallo backend, lees toolearn [aangepaste API's](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span><span class="sxs-lookup"><span data-stu-id="ffe2f-211">toolearn how toocreate a custom API on hello backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="ffe2f-212">toocall aangepaste API aanroepen `MSClient.invokeAPI`.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-212">toocall a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="ffe2f-213">Hallo-aanvraag en -antwoord inhoud worden behandeld als JSON.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-213">hello request and response content are treated as JSON.</span></span> <span data-ttu-id="ffe2f-214">toouse andere mediatypen [gebruik andere overbelasting van de Hallo `invokeAPI` ] [ 5].</span><span class="sxs-lookup"><span data-stu-id="ffe2f-214">toouse other media types, [use hello other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="ffe2f-215">toomake een `GET` aanvragen in plaats van een `POST` aanvraagt, setparameter `HTTPMethod` te`"GET"` en parameter `body` te`nil` (omdat de GET-aanvragen beschikt niet over de berichttekst.) Als uw aangepaste API andere HTTP-termen ondersteunt, wijzigt u `HTTPMethod` op de juiste wijze.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-215">toomake a `GET` request instead of a `POST` request, set parameter `HTTPMethod` too`"GET"` and parameter `body` too`nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="ffe2f-216">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-216">**Objective-C**:</span></span>

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

<span data-ttu-id="ffe2f-217">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-217">**Swift**:</span></span>

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <span data-ttu-id="ffe2f-218"><a name="templates"></a>Hoe: Register sjablonen toosend platformoverschrijdende pushmeldingen</span><span class="sxs-lookup"><span data-stu-id="ffe2f-218"><a name="templates"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="ffe2f-219">tooregister sjablonen, doorgeven sjablonen met uw **client.push registerDeviceToken** methode in uw client-app.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-219">tooregister templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="ffe2f-220">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-220">**Objective-C**:</span></span>

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="ffe2f-221">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-221">**Swift**:</span></span>

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

<span data-ttu-id="ffe2f-222">Uw sjablonen van het type NSDictionary en kunnen meerdere sjablonen in de volgende indeling Hallo bevatten:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-222">Your templates are of type NSDictionary and can contain multiple templates in hello following format:</span></span>

<span data-ttu-id="ffe2f-223">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-223">**Objective-C**:</span></span>

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="ffe2f-224">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-224">**Swift**:</span></span>

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="ffe2f-225">Alle codes zijn verwijderd uit het Hallo-aanvraag voor beveiliging.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-225">All tags are stripped from hello request for security.</span></span>  <span data-ttu-id="ffe2f-226">tooadd tags tooinstallations of sjablonen binnen installaties, Zie [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps][4].</span><span class="sxs-lookup"><span data-stu-id="ffe2f-226">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="ffe2f-227">toosend meldingen met behulp van deze sjablonen geregistreerde werken met [Notification Hubs-API's][3].</span><span class="sxs-lookup"><span data-stu-id="ffe2f-227">toosend notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <span data-ttu-id="ffe2f-228"><a name="errors"></a>How to: afhandelen van fouten</span><span class="sxs-lookup"><span data-stu-id="ffe2f-228"><a name="errors"></a>How to: Handle Errors</span></span>
<span data-ttu-id="ffe2f-229">Wanneer u een Azure App Service mobiele back-end aanroept, Hallo voltooiing blok bevat een `NSError` parameter.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-229">When you call an Azure App Service mobile backend, hello completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="ffe2f-230">Wanneer er een fout optreedt, wordt met deze parameter niet nul is.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="ffe2f-231">U moet deze parameter inschakelt en verwerken Hallo fout indien nodig, zoals wordt beschreven in voorgaande codefragmenten Hallo in uw code.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-231">In your code, you should check this parameter and handle hello error as needed, as demonstrated in hello preceding code snippets.</span></span>

<span data-ttu-id="ffe2f-232">Hallo bestand [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] definieert Hallo constanten `MSErrorResponseKey`, `MSErrorRequestKey`, en `MSErrorServerItemKey`.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-232">hello file [`<WindowsAzureMobileServices/MSError.h>`][6] defines hello constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="ffe2f-233">tooget toohello fout met betrekking tot meer gegevens:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-233">tooget more data related toohello error:</span></span>

<span data-ttu-id="ffe2f-234">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-234">**Objective-C**:</span></span>

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="ffe2f-235">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-235">**Swift**:</span></span>

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="ffe2f-236">Hallo-bestand definieert bovendien constanten voor elke foutcode:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-236">In addition, hello file defines constants for each error code:</span></span>

<span data-ttu-id="ffe2f-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-237">**Objective-C**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="ffe2f-238">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-238">**Swift**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

## <span data-ttu-id="ffe2f-239"><a name="adal"></a>Procedure: verificatie van gebruikers met Active Directory Authentication Library Hallo</span><span class="sxs-lookup"><span data-stu-id="ffe2f-239"><a name="adal"></a>How to: Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="ffe2f-240">U kunt Hallo Active Directory Authentication Library (ADAL) toosign gebruikers in uw toepassing met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-240">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="ffe2f-241">Clientverificatie-stroom met een id-provider SDK is beter toousing hello `loginWithProvider:completion:` methode.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-241">Client flow authentication using an identity provider SDK is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="ffe2f-242">Stroom clientverificatie biedt een meer systeemeigen UX idee en kunt u extra aanpassingen.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="ffe2f-243">Uw mobiele app back-end voor aanmelding bij de AAD configureren door de volgende Hallo [hoe tooconfigure App Service voor Active Directory-aanmelding] [ 7] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-243">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="ffe2f-244">Zorg ervoor dat toocomplete Hallo optionele stap voor het registreren van een systeemeigen clienttoepassing van.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-244">Make sure toocomplete hello optional step of registering a native client application.</span></span> <span data-ttu-id="ffe2f-245">Voor iOS, raden we aan dat Hallo omleidings-URI Hallo vorm is `<app-scheme>://<bundle-id>`.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-245">For iOS, we recommend that hello redirect URI is of hello form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="ffe2f-246">Zie voor meer informatie, Hallo [ADAL iOS Quick Start][8].</span><span class="sxs-lookup"><span data-stu-id="ffe2f-246">For more information, see hello [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="ffe2f-247">Installeren met behulp van Cocoapods ADAL.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="ffe2f-248">Uw Podfile tooinclude Hallo definitie te volgen en vervangt bewerken **uw PROJECT** met Hallo-naam van uw Xcode-project:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-248">Edit your Podfile tooinclude hello following definition, replacing **YOUR-PROJECT** with hello name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="ffe2f-249">en Hallo schil:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-249">and hello Pod:</span></span>

        pod 'ADALiOS'
3. <span data-ttu-id="ffe2f-250">Hallo Terminal uitvoeren met `pod install` uit Hallo directory waarin u uw project en open vervolgens Hallo gegenereerd Xcode-werkruimte (geen Hallo project).</span><span class="sxs-lookup"><span data-stu-id="ffe2f-250">Using hello Terminal, run `pod install` from hello directory containing your project, and then open hello generated Xcode workspace (not hello project).</span></span>
4. <span data-ttu-id="ffe2f-251">Voeg Hallo code tooyour toepassing te volgen, op basis van toohello taal die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-251">Add hello following code tooyour application, according toohello language you are using.</span></span> <span data-ttu-id="ffe2f-252">In elk, moet u deze vervangingen:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="ffe2f-253">Vervang **INSERT-instantie-hier** met de naam van de Hallo van Hallo tenant waarin u uw toepassing hebt ingericht.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-253">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="ffe2f-254">De indeling moet https://login.microsoftonline.com/contoso.onmicrosoft.com. Deze waarde kan worden gekopieerd Hallo domein tabblad in uw Azure Active Directory in Hallo [klassieke Azure portal].</span><span class="sxs-lookup"><span data-stu-id="ffe2f-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="ffe2f-255">Vervang **INSERT RESOURCE-ID hier** met Hallo client-ID voor uw back-end voor de mobiele app.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-255">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="ffe2f-256">U kunt de client-ID verkrijgen van Hallo **Geavanceerd** tabblad onder **Azure Active Directory-instellingen** in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-256">You can obtain the client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="ffe2f-257">Vervang **INSERT-CLIENT-ID-hier** met client-ID Hallo u hebt gekopieerd uit Hallo native client-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-257">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="ffe2f-258">Vervang **INSERT-OMLEIDINGS-URI-hier** aan uw site */.auth/login/done* eindpunt, met Hallo HTTPS-schema.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-258">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="ffe2f-259">Deze waarde moet er ongeveer te*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-259">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="ffe2f-260">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-260">**Objective-C**:</span></span>

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


<span data-ttu-id="ffe2f-261">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-261">**Swift**:</span></span>

    // add hello following imports tooyour bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <span data-ttu-id="ffe2f-262"><a name="facebook-sdk"></a>Procedure: verificatie van gebruikers met Hallo Facebook SDK voor iOS</span><span class="sxs-lookup"><span data-stu-id="ffe2f-262"><a name="facebook-sdk"></a>How to: Authenticate users with hello Facebook SDK for iOS</span></span>
<span data-ttu-id="ffe2f-263">U kunt Hallo Facebook SDK voor iOS toosign gebruikers in uw toepassing met Facebook.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-263">You can use hello Facebook SDK for iOS toosign users into your application using Facebook.</span></span>  <span data-ttu-id="ffe2f-264">Met behulp van een stroom clientverificatie is beter toousing hello `loginWithProvider:completion:` methode.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-264">Using a client flow authentication is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="ffe2f-265">Hallo-clientverificatie stroom biedt een meer systeemeigen UX idee en kunt u extra aanpassingen.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-265">hello client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="ffe2f-266">Uw mobiele app back-end voor aanmelding bij Facebook instellen door de [hoe tooconfigure App Service voor Facebook aanmelding] [ 9] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-266">Configure your mobile app backend for Facebook sign-in by following the [How tooconfigure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="ffe2f-267">Hallo Facebook SDK voor iOS door de volgende Hallo installeren [Facebook SDK voor iOS - aan de slag] [ 10] documentatie.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-267">Install hello Facebook SDK for iOS by following hello [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="ffe2f-268">In plaats van een app maken, kunt u bestaande tooyour-registratie van de Hallo iOS-platform toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-268">Instead of creating an app, you can add hello iOS platform tooyour existing registration.</span></span>
3. <span data-ttu-id="ffe2f-269">Facebook van documentatie bevat enkele Objective-C-code in Hallo App gemachtigde.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-269">Facebook's documentation includes some Objective-C code in hello App Delegate.</span></span> <span data-ttu-id="ffe2f-270">Als u **Swift**, kunt u Hallo vertalingen voor AppDelegate.swift te volgen:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-270">If you are using **Swift**, you can use hello following translations for AppDelegate.swift:</span></span>

        // Add hello following import tooyour bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. <span data-ttu-id="ffe2f-271">In aanvulling tooadding `FBSDKCoreKit.framework` tooyour project, Voeg een verwijzing ook te`FBSDKLoginKit.framework` in Hallo dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-271">In addition tooadding `FBSDKCoreKit.framework` tooyour project, also add a reference too`FBSDKLoginKit.framework` in hello same way.</span></span>
5. <span data-ttu-id="ffe2f-272">Voeg Hallo code tooyour toepassing te volgen, op basis van toohello taal die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-272">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="ffe2f-273">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-273">**Objective-C**:</span></span>

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

<span data-ttu-id="ffe2f-274">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-274">**Swift**:</span></span>

    // Add hello following imports tooyour bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <span data-ttu-id="ffe2f-275"><a name="twitter-fabric"></a>Procedure: verificatie van gebruikers met Twitter Fabric voor iOS</span><span class="sxs-lookup"><span data-stu-id="ffe2f-275"><a name="twitter-fabric"></a>How to: Authenticate users with Twitter Fabric for iOS</span></span>
<span data-ttu-id="ffe2f-276">U kunt voor iOS toosign gebruikers Fabric in uw toepassing met Twitter.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-276">You can use Fabric for iOS toosign users into your application using Twitter.</span></span> <span data-ttu-id="ffe2f-277">Clientverificatie voor de stroom is beter toousing hello `loginWithProvider:completion:` methode, zoals deze biedt een meer systeemeigen UX idee en kunt u extra aanpassingen.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-277">Client Flow authentication is preferable toousing hello `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="ffe2f-278">Uw mobiele app back-end voor aanmelding bij Twitter configureren door de volgende Hallo [hoe tooconfigure App Service voor Twitter aanmelding](app-service-mobile-how-to-configure-twitter-authentication.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-278">Configure your mobile app backend for Twitter sign-in by following hello [How tooconfigure App Service for Twitter login](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="ffe2f-279">Voeg Fabric tooyour project met de volgende Hallo [Fabric voor iOS - aan de slag] documentatie en TwitterKit in te stellen.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-279">Add Fabric tooyour project by following hello [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ffe2f-280">Standaard Fabric Twitter-toepassing voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-280">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="ffe2f-281">U kunt voorkomen dat het maken van een toepassing registreren Hallo Consumer-sleutel en consumentgeheim eerder met Hallo volgende codefragmenten hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-281">You can avoid creating an application by registering hello Consumer Key and Consumer Secret you created earlier using hello following code snippets.</span></span>    <span data-ttu-id="ffe2f-282">U kunt ook kunt u Hallo consumentsleutel vervangen en consumentgeheim waarden op te geven tooApp Service Hello waarden die u hebt ziet in Hallo [Dashboard voor Infrastructuurresources].</span><span class="sxs-lookup"><span data-stu-id="ffe2f-282">Alternatively, you can replace hello Consumer Key and Consumer Secret values that you provide tooApp Service with hello values you see in hello [Fabric Dashboard].</span></span> <span data-ttu-id="ffe2f-283">Als u deze optie kiest, is ervoor tooset Hallo callback URL tooa tijdelijke aanduiding voor waarde, zoals `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-283">If you choose this option, be sure tooset hello callback URL tooa placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>
   >
   >

    <span data-ttu-id="ffe2f-284">Als u toouse Hallo geheimen die u eerder hebt gemaakt kiest, toevoegen Hallo code tooyour App gemachtigde te volgen:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-284">If you choose toouse hello secrets you created earlier, add hello following code tooyour App Delegate:</span></span>

    <span data-ttu-id="ffe2f-285">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-285">**Objective-C**:</span></span>

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    <span data-ttu-id="ffe2f-286">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-286">**Swift**:</span></span>

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. <span data-ttu-id="ffe2f-287">Voeg Hallo code tooyour toepassing te volgen, op basis van toohello taal die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-287">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="ffe2f-288">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-288">**Objective-C**:</span></span>

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

<span data-ttu-id="ffe2f-289">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-289">**Swift**:</span></span>

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <span data-ttu-id="ffe2f-290"><a name="google-sdk"></a>Procedure: verificatie van gebruikers met Hallo Google-In SDK voor iOS</span><span class="sxs-lookup"><span data-stu-id="ffe2f-290"><a name="google-sdk"></a>How to: Authenticate users with hello Google Sign-In SDK for iOS</span></span>
<span data-ttu-id="ffe2f-291">U kunt Hallo Google-In SDK voor iOS toosign gebruikers in uw toepassing met behulp van een Google-account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-291">You can use hello Google Sign-In SDK for iOS toosign users into your application using a Google account.</span></span>  <span data-ttu-id="ffe2f-292">Google aangekondigd onlangs wijzigingen tootheir OAuth-beveiligingsbeleid.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-292">Google recently announced changes tootheir OAuth security policies.</span></span>  <span data-ttu-id="ffe2f-293">Deze beleidswijzigingen vereist het gebruik van de Google-SDK in toekomstige Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-293">These policy changes will require hello use of the Google SDK in hello future.</span></span>

1. <span data-ttu-id="ffe2f-294">Uw mobiele app back-end voor Google aanmelding configureren door de volgende Hallo [hoe tooconfigure App Service voor Google aanmelding](app-service-mobile-how-to-configure-google-authentication.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-294">Configure your mobile app backend for Google sign-in by following hello [How tooconfigure App Service for Google login](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="ffe2f-295">Hallo Google SDK voor iOS door de volgende Hallo installeren [Google Sign-In voor iOS - Start integreren](https://developers.google.com/identity/sign-in/ios/start-integrating) documentatie.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-295">Install hello Google SDK for iOS by following hello [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="ffe2f-296">Hallo verifiëren met een back-end sectie 'Server', kunt u overslaan.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-296">You may skip hello "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="ffe2f-297">Hallo van tooyour gemachtigde na toevoegen `signIn:didSignInForUser:withError:` methode op basis van toohello taal die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-297">Add hello following tooyour delegate's `signIn:didSignInForUser:withError:` method, according toohello language you are using.</span></span>

<span data-ttu-id="ffe2f-298">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-298">**Objective-C**:</span></span>

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

<span data-ttu-id="ffe2f-299">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-299">**Swift**:</span></span>

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. <span data-ttu-id="ffe2f-300">Zorg ervoor dat u ook de volgende te Hallo toevoegen`application:didFinishLaunchingWithOptions:` delegeren in uw app, "SERVER_CLIENT_ID" vervangen door een Hallo dezelfde ID die u hebt gebruikt tooconfigure App Service in stap 1.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-300">Make sure you also add hello following too`application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with hello same ID that you used tooconfigure App Service in step 1.</span></span>

<span data-ttu-id="ffe2f-301">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-301">**Objective-C**:</span></span>

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 <span data-ttu-id="ffe2f-302">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-302">**Swift**:</span></span>

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. <span data-ttu-id="ffe2f-303">Hallo na code tooyour toepassing in een UIViewController waarmee Hallo toevoegen `GIDSignInUIDelegate` -protocol op basis van toohello taal die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-303">Add hello following code tooyour application in a UIViewController that implements hello `GIDSignInUIDelegate` protocol, according toohello language you are using.</span></span>  <span data-ttu-id="ffe2f-304">U bent afgemeld voordat opnieuw wordt ondertekend en hoewel u niet tooenter uw referenties opnieuw hoeft, ziet u een dialoogvenster toestemming.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-304">You are signed out before being signed in again, and although you don't need tooenter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="ffe2f-305">Deze methode pas aanroepen wanneer Hallo sessietoken is verlopen.</span><span class="sxs-lookup"><span data-stu-id="ffe2f-305">Only call this method when hello session token has expired.</span></span>

   <span data-ttu-id="ffe2f-306">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-306">**Objective-C**:</span></span>

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   <span data-ttu-id="ffe2f-307">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ffe2f-307">**Swift**:</span></span>

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[Azure Mobile Apps Quick Start]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[dynamische Schema]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[Dashboard voor Infrastructuurresources]: https://www.fabric.io/home
[Fabric voor iOS - aan de slag]: https://docs.fabric.io/ios/fabric/getting-started.html
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
