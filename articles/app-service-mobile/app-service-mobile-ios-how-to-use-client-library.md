---
title: Hoe gebruik iOS SDK voor Azure Mobile Apps
description: Hoe gebruik iOS SDK voor Azure Mobile Apps
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
ms.openlocfilehash: 65817208e1b26fb5f9eb56d164f48b44d57dce56
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="a319d-103">Hoe gebruik iOS-clientbibliotheek voor Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="a319d-103">How to Use iOS Client Library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="a319d-104">Deze handleiding leert u veelvoorkomende scenario's met behulp van de meest recente uitvoeren [iOS SDK voor Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="a319d-104">This guide teaches you to perform common scenarios using the latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="a319d-105">Als u niet bekend met Azure Mobile Apps bent, eerst voltooien [Azure Mobile Apps Quick Start] voor het maken van een back-end van een tabel maken en een vooraf samengestelde iOS Xcode-project downloaden.</span><span class="sxs-lookup"><span data-stu-id="a319d-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="a319d-106">In deze handleiding richten we op de client-side iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="a319d-106">In this guide, we focus on the client-side iOS SDK.</span></span> <span data-ttu-id="a319d-107">Zie voor meer informatie over de SDK-serverzijde voor de back-end, de HOWTOs van de SDK-Server.</span><span class="sxs-lookup"><span data-stu-id="a319d-107">To learn more about the server-side SDK for the backend, see the Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="a319d-108">Referentiedocumentatie</span><span class="sxs-lookup"><span data-stu-id="a319d-108">Reference documentation</span></span>
<span data-ttu-id="a319d-109">De documentatie bij de client-iOS SDK bevindt zich hier: [Azure Mobile Apps iOS referentie Client][2].</span><span class="sxs-lookup"><span data-stu-id="a319d-109">The reference documentation for the iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="a319d-110">Ondersteunde Platforms</span><span class="sxs-lookup"><span data-stu-id="a319d-110">Supported Platforms</span></span>
<span data-ttu-id="a319d-111">De iOS SDK biedt ondersteuning voor Objective-C-projecten, Swift 2.2 projecten en Swift 2.3 projecten voor iOS-versie 8.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="a319d-111">The iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="a319d-112">De verificatie 'server-flow' maakt gebruik van een webweergave voor de gebruikersinterface weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a319d-112">The "server-flow" authentication uses a WebView for the presented UI.</span></span>  <span data-ttu-id="a319d-113">Als het apparaat is niet een UI WebView presentatie mogelijk en vervolgens een andere verificatiemethode is vereist is die buiten het bereik van het product.</span><span class="sxs-lookup"><span data-stu-id="a319d-113">If the device is not able to present a WebView UI, then another method of authentication is required that is outside the scope of the product.</span></span>  
<span data-ttu-id="a319d-114">Deze SDK is derhalve niet geschikt voor controle-type of op dezelfde manier beperkte apparaten.</span><span class="sxs-lookup"><span data-stu-id="a319d-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="a319d-115"><a name="Setup"></a>Het installatieprogramma en vereisten</span><span class="sxs-lookup"><span data-stu-id="a319d-115"><a name="Setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="a319d-116">Deze handleiding wordt ervan uitgegaan dat u een back-end hebt gemaakt met een tabel.</span><span class="sxs-lookup"><span data-stu-id="a319d-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="a319d-117">Deze handleiding wordt ervan uitgegaan dat de tabel heeft van hetzelfde schema als de tabellen in deze zelfstudies.</span><span class="sxs-lookup"><span data-stu-id="a319d-117">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span> <span data-ttu-id="a319d-118">Deze handleiding wordt ervan uitgegaan dat in uw code u verwijzen naar `MicrosoftAzureMobile.framework` en importeer `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span><span class="sxs-lookup"><span data-stu-id="a319d-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <span data-ttu-id="a319d-119"><a name="create-client"></a>How to: Client maken</span><span class="sxs-lookup"><span data-stu-id="a319d-119"><a name="create-client"></a>How to: Create Client</span></span>
<span data-ttu-id="a319d-120">Als u een back-end van Azure Mobile Apps in uw project, maak een `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="a319d-120">To access an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="a319d-121">Vervang `AppUrl` met de app-URL.</span><span class="sxs-lookup"><span data-stu-id="a319d-121">Replace `AppUrl` with the app URL.</span></span> <span data-ttu-id="a319d-122">U laten `gatewayURLString` en `applicationKey` leeg.</span><span class="sxs-lookup"><span data-stu-id="a319d-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="a319d-123">Als u een gateway voor verificatie instelt, vullen `gatewayURLString` met de URL van de gateway.</span><span class="sxs-lookup"><span data-stu-id="a319d-123">If you set up a gateway for authentication, populate `gatewayURLString` with the gateway URL.</span></span>

<span data-ttu-id="a319d-124">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-124">**Objective-C**:</span></span>

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="a319d-125">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-125">**Swift**:</span></span>

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <span data-ttu-id="a319d-126"><a name="table-reference"></a>How to: tabelverwijzing maken</span><span class="sxs-lookup"><span data-stu-id="a319d-126"><a name="table-reference"></a>How to: Create Table Reference</span></span>
<span data-ttu-id="a319d-127">Maak een verwijzing naar de back-endtabel als u gegevens wilt bekijken of bijwerken.</span><span class="sxs-lookup"><span data-stu-id="a319d-127">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="a319d-128">Vervang `TodoItem` door de naam van uw tabel</span><span class="sxs-lookup"><span data-stu-id="a319d-128">Replace `TodoItem` with the name of your table</span></span>

<span data-ttu-id="a319d-129">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-129">**Objective-C**:</span></span>

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="a319d-130">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-130">**Swift**:</span></span>

```
let table = client.tableWithName("TodoItem")
```


## <span data-ttu-id="a319d-131"><a name="querying"></a>Procedure: een Query over gegevens</span><span class="sxs-lookup"><span data-stu-id="a319d-131"><a name="querying"></a>How to: Query Data</span></span>
<span data-ttu-id="a319d-132">Query voor het maken van een databasequery uitvoeren op de `MSTable` object.</span><span class="sxs-lookup"><span data-stu-id="a319d-132">To create a database query, query the `MSTable` object.</span></span> <span data-ttu-id="a319d-133">De volgende query haalt alle items in `TodoItem` en registreert de tekst van elk item.</span><span class="sxs-lookup"><span data-stu-id="a319d-133">The following query gets all the items in `TodoItem` and logs the text of each item.</span></span>

<span data-ttu-id="a319d-134">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-134">**Objective-C**:</span></span>

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

<span data-ttu-id="a319d-135">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-135">**Swift**:</span></span>

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

## <span data-ttu-id="a319d-136"><a name="filtering"></a>How to: Filter gegevens geretourneerd</span><span class="sxs-lookup"><span data-stu-id="a319d-136"><a name="filtering"></a>How to: Filter Returned Data</span></span>
<span data-ttu-id="a319d-137">Om resultaten te filteren, zijn er veel opties beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="a319d-137">To filter results, there are many available options.</span></span>

<span data-ttu-id="a319d-138">Als u wilt filteren met behulp van een predicaat, gebruiken een `NSPredicate` en `readWithPredicate`.</span><span class="sxs-lookup"><span data-stu-id="a319d-138">To filter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="a319d-139">De volgende filters resultaatgegevens om alleen onvolledige Todo-items te vinden.</span><span class="sxs-lookup"><span data-stu-id="a319d-139">The following filters returned data to find only incomplete Todo items.</span></span>

<span data-ttu-id="a319d-140">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-140">**Objective-C**:</span></span>

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query the TodoItem table
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

<span data-ttu-id="a319d-141">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-141">**Swift**:</span></span>

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query the TodoItem table
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

## <span data-ttu-id="a319d-142"><a name="query-object"></a>How to: MSQuery gebruiken</span><span class="sxs-lookup"><span data-stu-id="a319d-142"><a name="query-object"></a>How to: Use MSQuery</span></span>
<span data-ttu-id="a319d-143">Als een complexe query (inclusief sortering en paginering) uitvoert, maakt u een `MSQuery` object, rechtstreeks of via een predikaat:</span><span class="sxs-lookup"><span data-stu-id="a319d-143">To perform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="a319d-144">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-144">**Objective-C**:</span></span>

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="a319d-145">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-145">**Swift**:</span></span>

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="a319d-146">`MSQuery`kunt u verschillende query gedrag bepalen.</span><span class="sxs-lookup"><span data-stu-id="a319d-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="a319d-147">Geef de volgorde van resultaten</span><span class="sxs-lookup"><span data-stu-id="a319d-147">Specify order of results</span></span>
* <span data-ttu-id="a319d-148">Beperken welke velden u wilt retourneren</span><span class="sxs-lookup"><span data-stu-id="a319d-148">Limit which fields to return</span></span>
* <span data-ttu-id="a319d-149">Hoeveel records om terug te beperken</span><span class="sxs-lookup"><span data-stu-id="a319d-149">Limit how many records to return</span></span>
* <span data-ttu-id="a319d-150">Totaal aantal opgeven om in het antwoord</span><span class="sxs-lookup"><span data-stu-id="a319d-150">Specify total count in response</span></span>
* <span data-ttu-id="a319d-151">Aangepaste queryreeksparameters in aanvraag opgeven</span><span class="sxs-lookup"><span data-stu-id="a319d-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="a319d-152">Aanvullende functies toepassen</span><span class="sxs-lookup"><span data-stu-id="a319d-152">Apply additional functions</span></span>

<span data-ttu-id="a319d-153">Uitvoeren van een `MSQuery` query door het aanroepen van `readWithCompletion` op het object.</span><span class="sxs-lookup"><span data-stu-id="a319d-153">Execute an `MSQuery` query by calling `readWithCompletion` on the object.</span></span>

## <span data-ttu-id="a319d-154"><a name="sorting"></a>How to: gegevens met MSQuery sorteren</span><span class="sxs-lookup"><span data-stu-id="a319d-154"><a name="sorting"></a>How to: Sort Data with MSQuery</span></span>
<span data-ttu-id="a319d-155">Om te sorteren resultaten, kunt u een voorbeeld gaan we kijken.</span><span class="sxs-lookup"><span data-stu-id="a319d-155">To sort results, let's look at an example.</span></span> <span data-ttu-id="a319d-156">Aanroepen om te sorteren op het veld 'text' oplopende, vervolgens op het 'complete' aflopende, `MSQuery` als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="a319d-156">To sort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="a319d-157">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-157">**Objective-C**:</span></span>

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

<span data-ttu-id="a319d-158">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-158">**Swift**:</span></span>

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


## <span data-ttu-id="a319d-159"><a name="selecting"></a><a name="parameters"></a>How to: beperken van velden en vouw queryreeksparameters met MSQuery</span><span class="sxs-lookup"><span data-stu-id="a319d-159"><a name="selecting"></a><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>
<span data-ttu-id="a319d-160">Geef de namen van de velden in om te beperken velden moeten worden geretourneerd in een query, het **selectFields** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="a319d-160">To limit fields to be returned in a query, specify the names of the fields in the **selectFields** property.</span></span> <span data-ttu-id="a319d-161">In dit voorbeeld retourneert alleen de tekst en voltooide velden:</span><span class="sxs-lookup"><span data-stu-id="a319d-161">This example returns only the text and completed fields:</span></span>

<span data-ttu-id="a319d-162">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-162">**Objective-C**:</span></span>

```
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="a319d-163">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-163">**Swift**:</span></span>

```
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="a319d-164">Als u wilt aanvullende queryreeksparameters opnemen in de aanvraag van de server (bijvoorbeeld omdat ze maakt gebruik van een aangepast script van de server-side), vullen `query.parameters` als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="a319d-164">To include additional query string parameters in the server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="a319d-165">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-165">**Objective-C**:</span></span>

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="a319d-166">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-166">**Swift**:</span></span>

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <span data-ttu-id="a319d-167"><a name="paging"></a>How to: paginaformaat configureren</span><span class="sxs-lookup"><span data-stu-id="a319d-167"><a name="paging"></a>How to: Configure Page Size</span></span>
<span data-ttu-id="a319d-168">Met Azure Mobile Apps bepaalt de grootte van het aantal records dat tegelijk uit de back-end-tabellen worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="a319d-168">With Azure Mobile Apps, the page size controls the number of records that are pulled at a time from the backend tables.</span></span> <span data-ttu-id="a319d-169">Een aanroep van `pull` gegevens zou vervolgens batch-up van gegevens, op basis van dit paginaformaat tot er zijn geen records meer om op te halen.</span><span class="sxs-lookup"><span data-stu-id="a319d-169">A call to `pull` data would then batch up data, based on this page size, until there are no more records to pull.</span></span>

<span data-ttu-id="a319d-170">Het is mogelijk voor het configureren van een pagina grootte met **MSPullSettings** zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a319d-170">It's possible to configure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="a319d-171">Grootte van de pagina is 50 en het onderstaande voorbeeld gewijzigd in 3.</span><span class="sxs-lookup"><span data-stu-id="a319d-171">The default page size is 50, and the example below changes it to 3.</span></span>

<span data-ttu-id="a319d-172">U kunt een ander paginaformaat Prestatieoverwegingen configureren.</span><span class="sxs-lookup"><span data-stu-id="a319d-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="a319d-173">Als u een groot aantal kleine gegevensrecords hebt, minder een hoge paginaformaat server retourbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="a319d-173">If you have a large number of small data records, a high page size reduces the number of server round-trips.</span></span>

<span data-ttu-id="a319d-174">Deze instelling bepaalt de paginagrootte aan de clientzijde.</span><span class="sxs-lookup"><span data-stu-id="a319d-174">This setting controls only the page size on the client side.</span></span> <span data-ttu-id="a319d-175">Als de client om een pagina groter vraagt dan de back-end van Mobile Apps wordt ondersteund, is het paginaformaat beperkt tot het maximum dat de back-end is geconfigureerd voor ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="a319d-175">If the client asks for a larger page size than the Mobile Apps backend supports, the page size is capped at the maximum the backend is configured to support.</span></span>

<span data-ttu-id="a319d-176">Deze instelling is ook de *getal* gegevensrecords, niet de *bytegrootte*.</span><span class="sxs-lookup"><span data-stu-id="a319d-176">This setting is also the *number* of data records, not the *byte size*.</span></span>

<span data-ttu-id="a319d-177">Als u het formaat van de client verhoogt, moet u ook de paginagrootte van de op de server te verhogen.</span><span class="sxs-lookup"><span data-stu-id="a319d-177">If you increase the client page size, you should also increase the page size on the server.</span></span> <span data-ttu-id="a319d-178">Zie [' How to: pas de grootte van de tabel paginering '](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) voor de stappen om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="a319d-178">See ["How to: Adjust the table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for the steps to do this.</span></span>

<span data-ttu-id="a319d-179">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-179">**Objective-C**:</span></span>

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


<span data-ttu-id="a319d-180">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-180">**Swift**:</span></span>

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <span data-ttu-id="a319d-181"><a name="inserting"></a>How to: gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="a319d-181"><a name="inserting"></a>How to: Insert Data</span></span>
<span data-ttu-id="a319d-182">Voor het invoegen van een rij in een nieuwe tabel maken van een `NSDictionary` en oproepen `table insert`.</span><span class="sxs-lookup"><span data-stu-id="a319d-182">To insert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="a319d-183">Als [dynamische Schema] is ingeschakeld, de Azure App Service mobiele back-end genereert automatisch nieuwe kolommen op basis van de `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="a319d-183">If [Dynamic Schema] is enabled, the Azure App Service mobile backend automatically generates new columns based on the `NSDictionary`.</span></span>

<span data-ttu-id="a319d-184">Als `id` is niet opgegeven, wordt de back-end genereert automatisch een nieuwe unieke ID.</span><span class="sxs-lookup"><span data-stu-id="a319d-184">If `id` is not provided, the backend automatically generates a new unique ID.</span></span> <span data-ttu-id="a319d-185">Geef uw eigen `id` e-mailadres gebruiken adressen, gebruikersnamen, of uw eigen aangepaste waarden als de ID.</span><span class="sxs-lookup"><span data-stu-id="a319d-185">Provide your own `id` to use email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="a319d-186">Uw eigen ID bieden gemakkelijker joins en database zakelijke logica.</span><span class="sxs-lookup"><span data-stu-id="a319d-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="a319d-187">De `result` bevat het nieuwe item dat is ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="a319d-187">The `result` contains the new item that was inserted.</span></span> <span data-ttu-id="a319d-188">Afhankelijk van de logische server, kan deze extra of gewijzigde gegevens vergeleken met wat is doorgegeven aan de server hebben.</span><span class="sxs-lookup"><span data-stu-id="a319d-188">Depending on your server logic, it may have additional or modified data compared to what was passed to the server.</span></span>

<span data-ttu-id="a319d-189">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-189">**Objective-C**:</span></span>

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

<span data-ttu-id="a319d-190">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-190">**Swift**:</span></span>

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

## <span data-ttu-id="a319d-191"><a name="modifying"></a>How to: gegevens wijzigen</span><span class="sxs-lookup"><span data-stu-id="a319d-191"><a name="modifying"></a>How to: Modify Data</span></span>
<span data-ttu-id="a319d-192">Voor het bijwerken van een bestaande rij wijzigen van een item en de aanroep `update`:</span><span class="sxs-lookup"><span data-stu-id="a319d-192">To update an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="a319d-193">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-193">**Objective-C**:</span></span>

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

<span data-ttu-id="a319d-194">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-194">**Swift**:</span></span>

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

<span data-ttu-id="a319d-195">U kunt ook de rij-ID en het bijgewerkte veld opgeven:</span><span class="sxs-lookup"><span data-stu-id="a319d-195">Alternatively, supply the row ID and the updated field:</span></span>

<span data-ttu-id="a319d-196">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-196">**Objective-C**:</span></span>

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="a319d-197">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-197">**Swift**:</span></span>

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="a319d-198">Ten minste de `id` kenmerk moet worden ingesteld bij het maken van updates.</span><span class="sxs-lookup"><span data-stu-id="a319d-198">At minimum, the `id` attribute must be set when making updates.</span></span>

## <span data-ttu-id="a319d-199"><a name="deleting"></a>How to: gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="a319d-199"><a name="deleting"></a>How to: Delete Data</span></span>
<span data-ttu-id="a319d-200">Als u wilt een item verwijdert, worden aangeroepen `delete` met het item:</span><span class="sxs-lookup"><span data-stu-id="a319d-200">To delete an item, invoke `delete` with the item:</span></span>

<span data-ttu-id="a319d-201">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-201">**Objective-C**:</span></span>

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="a319d-202">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-202">**Swift**:</span></span>

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="a319d-203">U kunt ook verwijderen door op te geven van een rij-ID:</span><span class="sxs-lookup"><span data-stu-id="a319d-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="a319d-204">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-204">**Objective-C**:</span></span>

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="a319d-205">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-205">**Swift**:</span></span>

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="a319d-206">Ten minste de `id` kenmerk moet worden ingesteld wanneer u wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a319d-206">At minimum, the `id` attribute must be set when making deletes.</span></span>

## <span data-ttu-id="a319d-207"><a name="customapi"></a>How to: aangepaste API aanroepen</span><span class="sxs-lookup"><span data-stu-id="a319d-207"><a name="customapi"></a>How to: Call Custom API</span></span>
<span data-ttu-id="a319d-208">Met een aangepaste API kan geen back-end-functies worden blootgesteld.</span><span class="sxs-lookup"><span data-stu-id="a319d-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="a319d-209">Heeft geen toewijzen aan een tabel-bewerking.</span><span class="sxs-lookup"><span data-stu-id="a319d-209">It doesn't have to map to a table operation.</span></span> <span data-ttu-id="a319d-210">Niet alleen doet u meer controle krijgen over messaging, maar u kunt zelfs lezen/set headers en wijzigt u de indeling van het antwoord-instantie.</span><span class="sxs-lookup"><span data-stu-id="a319d-210">Not only do you gain more control over messaging, you can even read/set headers and change the response body format.</span></span> <span data-ttu-id="a319d-211">Lees voor meer informatie over het maken van een aangepaste API gebruiken op de back-end, [aangepaste API's](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span><span class="sxs-lookup"><span data-stu-id="a319d-211">To learn how to create a custom API on the backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="a319d-212">Voor het aanroepen van aangepaste API aanroepen `MSClient.invokeAPI`.</span><span class="sxs-lookup"><span data-stu-id="a319d-212">To call a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="a319d-213">De aanvraag en antwoord inhoud worden behandeld als JSON.</span><span class="sxs-lookup"><span data-stu-id="a319d-213">The request and response content are treated as JSON.</span></span> <span data-ttu-id="a319d-214">Andere typen media [gebruik de andere overbelasting van `invokeAPI` ] [ 5].</span><span class="sxs-lookup"><span data-stu-id="a319d-214">To use other media types, [use the other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="a319d-215">Om ervoor een `GET` aanvragen in plaats van een `POST` aanvraagt, setparameter `HTTPMethod` naar `"GET"` en parameter `body` naar `nil` (omdat de GET-aanvragen beschikt niet over de berichttekst.) Als uw aangepaste API andere HTTP-termen ondersteunt, wijzigt u `HTTPMethod` op de juiste wijze.</span><span class="sxs-lookup"><span data-stu-id="a319d-215">To make a `GET` request instead of a `POST` request, set parameter `HTTPMethod` to `"GET"` and parameter `body` to `nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="a319d-216">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-216">**Objective-C**:</span></span>

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

<span data-ttu-id="a319d-217">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-217">**Swift**:</span></span>

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

## <span data-ttu-id="a319d-218"><a name="templates"></a>Hoe: Register push sjablonen om platformoverschrijdende meldingen te verzenden</span><span class="sxs-lookup"><span data-stu-id="a319d-218"><a name="templates"></a>How to: Register push templates to send cross-platform notifications</span></span>
<span data-ttu-id="a319d-219">Voor het registreren van sjablonen doorgeven sjablonen met uw **client.push registerDeviceToken** methode in uw client-app.</span><span class="sxs-lookup"><span data-stu-id="a319d-219">To register templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="a319d-220">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-220">**Objective-C**:</span></span>

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="a319d-221">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-221">**Swift**:</span></span>

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

<span data-ttu-id="a319d-222">Uw sjablonen van het type NSDictionary en kunnen meerdere sjablonen in de volgende indeling bevatten:</span><span class="sxs-lookup"><span data-stu-id="a319d-222">Your templates are of type NSDictionary and can contain multiple templates in the following format:</span></span>

<span data-ttu-id="a319d-223">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-223">**Objective-C**:</span></span>

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="a319d-224">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-224">**Swift**:</span></span>

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="a319d-225">Alle codes worden verwijderd van de aanvraag voor beveiliging.</span><span class="sxs-lookup"><span data-stu-id="a319d-225">All tags are stripped from the request for security.</span></span>  <span data-ttu-id="a319d-226">Zie voor informatie over het toevoegen van labels op installaties of -sjablonen in installaties [werken met de .NET-back-endserver SDK voor Azure Mobile Apps][4].</span><span class="sxs-lookup"><span data-stu-id="a319d-226">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="a319d-227">Om meldingen te verzenden met behulp van deze geregistreerde sjablonen, werken met [Notification Hubs-API's][3].</span><span class="sxs-lookup"><span data-stu-id="a319d-227">To send notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <span data-ttu-id="a319d-228"><a name="errors"></a>How to: afhandelen van fouten</span><span class="sxs-lookup"><span data-stu-id="a319d-228"><a name="errors"></a>How to: Handle Errors</span></span>
<span data-ttu-id="a319d-229">Wanneer u een Azure App Service mobiele back-end aanroept, wordt het blok voltooiing bevat een `NSError` parameter.</span><span class="sxs-lookup"><span data-stu-id="a319d-229">When you call an Azure App Service mobile backend, the completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="a319d-230">Wanneer er een fout optreedt, wordt met deze parameter niet nul is.</span><span class="sxs-lookup"><span data-stu-id="a319d-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="a319d-231">U moet deze parameter inschakelt en verwerken van de fout naar behoefte, zoals wordt beschreven in de voorgaande codefragmenten in uw code.</span><span class="sxs-lookup"><span data-stu-id="a319d-231">In your code, you should check this parameter and handle the error as needed, as demonstrated in the preceding code snippets.</span></span>

<span data-ttu-id="a319d-232">Het bestand [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] definieert de constanten `MSErrorResponseKey`, `MSErrorRequestKey`, en `MSErrorServerItemKey`.</span><span class="sxs-lookup"><span data-stu-id="a319d-232">The file [`<WindowsAzureMobileServices/MSError.h>`][6] defines the constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="a319d-233">Ophalen van meer gegevens met betrekking tot de volgende fout:</span><span class="sxs-lookup"><span data-stu-id="a319d-233">To get more data related to the error:</span></span>

<span data-ttu-id="a319d-234">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-234">**Objective-C**:</span></span>

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="a319d-235">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-235">**Swift**:</span></span>

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="a319d-236">Het bestand definieert bovendien constanten voor elke foutcode:</span><span class="sxs-lookup"><span data-stu-id="a319d-236">In addition, the file defines constants for each error code:</span></span>

<span data-ttu-id="a319d-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-237">**Objective-C**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="a319d-238">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-238">**Swift**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

## <span data-ttu-id="a319d-239"><a name="adal"></a>Procedure: verificatie van gebruikers met de Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="a319d-239"><a name="adal"></a>How to: Authenticate users with the Active Directory Authentication Library</span></span>
<span data-ttu-id="a319d-240">U kunt de Active Directory Authentication Library (ADAL) gebruiken voor het ondertekenen van gebruikers in uw toepassing met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a319d-240">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="a319d-241">Stroom clientverificatie met een id-provider SDK heeft de voorkeur boven met behulp van de `loginWithProvider:completion:` methode.</span><span class="sxs-lookup"><span data-stu-id="a319d-241">Client flow authentication using an identity provider SDK is preferable to using the `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="a319d-242">Stroom clientverificatie biedt een meer systeemeigen UX idee en kunt u extra aanpassingen.</span><span class="sxs-lookup"><span data-stu-id="a319d-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="a319d-243">Uw mobiele app back-end voor aanmelding bij de AAD instellen door de [App Service configureren voor Active Directory-aanmelding] [ 7] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a319d-243">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="a319d-244">Zorg ervoor dat de optionele stap voor het registreren van een systeemeigen clienttoepassing van voltooien.</span><span class="sxs-lookup"><span data-stu-id="a319d-244">Make sure to complete the optional step of registering a native client application.</span></span> <span data-ttu-id="a319d-245">Voor iOS-, we raden aan dat de omleidings-URI van het formulier is `<app-scheme>://<bundle-id>`.</span><span class="sxs-lookup"><span data-stu-id="a319d-245">For iOS, we recommend that the redirect URI is of the form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="a319d-246">Zie voor meer informatie de [ADAL iOS Quick Start][8].</span><span class="sxs-lookup"><span data-stu-id="a319d-246">For more information, see the [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="a319d-247">Installeren met behulp van Cocoapods ADAL.</span><span class="sxs-lookup"><span data-stu-id="a319d-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="a319d-248">Uw Podfile zodanig dat de volgende definitie bewerken vervangen **uw PROJECT** met de naam van uw Xcode-project:</span><span class="sxs-lookup"><span data-stu-id="a319d-248">Edit your Podfile to include the following definition, replacing **YOUR-PROJECT** with the name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="a319d-249">en een schil:</span><span class="sxs-lookup"><span data-stu-id="a319d-249">and the Pod:</span></span>

        pod 'ADALiOS'
3. <span data-ttu-id="a319d-250">Met behulp van de Terminal en voer `pod install` uit de directory waarin u uw project en open vervolgens de gegenereerde Xcode-werkruimte (niet op het project).</span><span class="sxs-lookup"><span data-stu-id="a319d-250">Using the Terminal, run `pod install` from the directory containing your project, and then open the generated Xcode workspace (not the project).</span></span>
4. <span data-ttu-id="a319d-251">De volgende code toevoegen aan uw toepassing, volgens de taal die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a319d-251">Add the following code to your application, according to the language you are using.</span></span> <span data-ttu-id="a319d-252">In elk, moet u deze vervangingen:</span><span class="sxs-lookup"><span data-stu-id="a319d-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="a319d-253">Vervang **INSERT-instantie-hier** met de naam van de tenant waarin u uw toepassing hebt ingericht.</span><span class="sxs-lookup"><span data-stu-id="a319d-253">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="a319d-254">De indeling moet https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="a319d-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="a319d-255">Deze waarde kan worden gekopieerd vanaf het tabblad domein in uw Azure Active Directory in de [klassieke Azure portal].</span><span class="sxs-lookup"><span data-stu-id="a319d-255">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span></span>
   * <span data-ttu-id="a319d-256">Vervang **INSERT RESOURCE-ID hier** met de client-ID voor uw back-end voor de mobiele app.</span><span class="sxs-lookup"><span data-stu-id="a319d-256">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="a319d-257">U vindt de client-ID van de **Geavanceerd** tabblad onder **Azure Active Directory-instellingen** in de portal.</span><span class="sxs-lookup"><span data-stu-id="a319d-257">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
   * <span data-ttu-id="a319d-258">Vervang **INSERT-CLIENT-ID-hier** met de client-ID die u hebt gekopieerd uit de native client-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a319d-258">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
   * <span data-ttu-id="a319d-259">Vervang **INSERT-OMLEIDINGS-URI-hier** aan uw site */.auth/login/done* eindpunt, met behulp van het HTTPS-schema.</span><span class="sxs-lookup"><span data-stu-id="a319d-259">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="a319d-260">Deze waarde moet er ongeveer als *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="a319d-260">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="a319d-261">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-261">**Objective-C**:</span></span>

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


<span data-ttu-id="a319d-262">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-262">**Swift**:</span></span>

    // add the following imports to your bridging header:
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

## <span data-ttu-id="a319d-263"><a name="facebook-sdk"></a>Procedure: verificatie van gebruikers met de Facebook-SDK voor iOS</span><span class="sxs-lookup"><span data-stu-id="a319d-263"><a name="facebook-sdk"></a>How to: Authenticate users with the Facebook SDK for iOS</span></span>
<span data-ttu-id="a319d-264">U kunt de Facebook SDK voor iOS gebruiken voor het ondertekenen van gebruikers in uw toepassing met Facebook.</span><span class="sxs-lookup"><span data-stu-id="a319d-264">You can use the Facebook SDK for iOS to sign users into your application using Facebook.</span></span>  <span data-ttu-id="a319d-265">Met behulp van een stroom clientverificatie heeft de voorkeur boven met behulp van de `loginWithProvider:completion:` methode.</span><span class="sxs-lookup"><span data-stu-id="a319d-265">Using a client flow authentication is preferable to using the `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="a319d-266">De verificatie van de client-stroom biedt een meer systeemeigen UX idee en kunt u extra aanpassingen.</span><span class="sxs-lookup"><span data-stu-id="a319d-266">The client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="a319d-267">Uw mobiele app back-end voor aanmelding bij Facebook instellen door de [App Service configureren voor aanmelding Facebook] [ 9] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a319d-267">Configure your mobile app backend for Facebook sign-in by following the [How to configure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="a319d-268">De Facebook-SDK voor iOS installeren door de [Facebook SDK voor iOS - aan de slag] [ 10] documentatie.</span><span class="sxs-lookup"><span data-stu-id="a319d-268">Install the Facebook SDK for iOS by following the [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="a319d-269">In plaats van een app maken, kunt u het iOS-platform toevoegen aan uw bestaande registratie.</span><span class="sxs-lookup"><span data-stu-id="a319d-269">Instead of creating an app, you can add the iOS platform to your existing registration.</span></span>
3. <span data-ttu-id="a319d-270">Facebook van documentatie bevat enkele Objective-C-code in de gemachtigde voor de App.</span><span class="sxs-lookup"><span data-stu-id="a319d-270">Facebook's documentation includes some Objective-C code in the App Delegate.</span></span> <span data-ttu-id="a319d-271">Als u **Swift**, kunt u de volgende vertalingen voor AppDelegate.swift:</span><span class="sxs-lookup"><span data-stu-id="a319d-271">If you are using **Swift**, you can use the following translations for AppDelegate.swift:</span></span>

        // Add the following import to your bridging header:
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
4. <span data-ttu-id="a319d-272">Naast het toevoegen van `FBSDKCoreKit.framework` aan uw project een verwijzing naar ook toevoegen `FBSDKLoginKit.framework` op dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="a319d-272">In addition to adding `FBSDKCoreKit.framework` to your project, also add a reference to `FBSDKLoginKit.framework` in the same way.</span></span>
5. <span data-ttu-id="a319d-273">De volgende code toevoegen aan uw toepassing, volgens de taal die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a319d-273">Add the following code to your application, according to the language you are using.</span></span>

<span data-ttu-id="a319d-274">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-274">**Objective-C**:</span></span>

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

<span data-ttu-id="a319d-275">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-275">**Swift**:</span></span>

    // Add the following imports to your bridging header:
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

## <span data-ttu-id="a319d-276"><a name="twitter-fabric"></a>Procedure: verificatie van gebruikers met Twitter Fabric voor iOS</span><span class="sxs-lookup"><span data-stu-id="a319d-276"><a name="twitter-fabric"></a>How to: Authenticate users with Twitter Fabric for iOS</span></span>
<span data-ttu-id="a319d-277">Fabric voor iOS kunt u gebruikers zich aanmelden in uw toepassing met Twitter.</span><span class="sxs-lookup"><span data-stu-id="a319d-277">You can use Fabric for iOS to sign users into your application using Twitter.</span></span> <span data-ttu-id="a319d-278">Verificatie van client-stroom heeft de voorkeur boven met behulp van de `loginWithProvider:completion:` methode, zoals deze biedt een meer systeemeigen UX idee en kunt u extra aanpassingen.</span><span class="sxs-lookup"><span data-stu-id="a319d-278">Client Flow authentication is preferable to using the `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="a319d-279">Instellen van uw mobiele app back-end voor Twitter aanmelding door de [App Service configureren voor aanmelding Twitter](app-service-mobile-how-to-configure-twitter-authentication.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a319d-279">Configure your mobile app backend for Twitter sign-in by following the [How to configure App Service for Twitter login](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="a319d-280">Fabric toevoegen aan uw project door de [Fabric voor iOS - aan de slag] documentatie en TwitterKit in te stellen.</span><span class="sxs-lookup"><span data-stu-id="a319d-280">Add Fabric to your project by following the [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a319d-281">Standaard Fabric Twitter-toepassing voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a319d-281">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="a319d-282">U kunt voorkomen dat een toepassing maken via het registreren van de Consumer-sleutel en de consumentgeheim eerder met de volgende codefragmenten hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a319d-282">You can avoid creating an application by registering the Consumer Key and Consumer Secret you created earlier using the following code snippets.</span></span>    <span data-ttu-id="a319d-283">U kunt ook kunt u de sleutel van de Consumer en consumentgeheim waarden die u in App Service met de waarden die u ziet opgeeft in vervangen de [Dashboard voor Infrastructuurresources].</span><span class="sxs-lookup"><span data-stu-id="a319d-283">Alternatively, you can replace the Consumer Key and Consumer Secret values that you provide to App Service with the values you see in the [Fabric Dashboard].</span></span> <span data-ttu-id="a319d-284">Als u deze optie kiest, moet u de callback-URL, zoals ingesteld in een tijdelijke aanduidingswaarde, `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="a319d-284">If you choose this option, be sure to set the callback URL to a placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>
   >
   >

    <span data-ttu-id="a319d-285">Als u gebruiken de geheimen die u eerder hebt gemaakt wilt, moet u de volgende code toevoegen aan uw App gemachtigde:</span><span class="sxs-lookup"><span data-stu-id="a319d-285">If you choose to use the secrets you created earlier, add the following code to your App Delegate:</span></span>

    <span data-ttu-id="a319d-286">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-286">**Objective-C**:</span></span>

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

    <span data-ttu-id="a319d-287">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-287">**Swift**:</span></span>

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. <span data-ttu-id="a319d-288">De volgende code toevoegen aan uw toepassing, volgens de taal die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a319d-288">Add the following code to your application, according to the language you are using.</span></span>

<span data-ttu-id="a319d-289">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-289">**Objective-C**:</span></span>

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

<span data-ttu-id="a319d-290">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-290">**Swift**:</span></span>

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

## <span data-ttu-id="a319d-291"><a name="google-sdk"></a>Procedure: verificatie van gebruikers met de Google-In SDK voor iOS</span><span class="sxs-lookup"><span data-stu-id="a319d-291"><a name="google-sdk"></a>How to: Authenticate users with the Google Sign-In SDK for iOS</span></span>
<span data-ttu-id="a319d-292">U kunt de Google-In SDK voor iOS gebruiken voor het ondertekenen van gebruikers in uw toepassing met behulp van een Google-account.</span><span class="sxs-lookup"><span data-stu-id="a319d-292">You can use the Google Sign-In SDK for iOS to sign users into your application using a Google account.</span></span>  <span data-ttu-id="a319d-293">Google aangekondigd onlangs wijzigingen in hun OAuth-beveiligingsbeleid.</span><span class="sxs-lookup"><span data-stu-id="a319d-293">Google recently announced changes to their OAuth security policies.</span></span>  <span data-ttu-id="a319d-294">Deze wijzigingen vereisen het gebruik van de Google-SDK in de toekomst.</span><span class="sxs-lookup"><span data-stu-id="a319d-294">These policy changes will require the use of the Google SDK in the future.</span></span>

1. <span data-ttu-id="a319d-295">Instellen van uw mobiele app back-end voor Google aanmelding door de [het configureren van App Service voor Google aanmelding](app-service-mobile-how-to-configure-google-authentication.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a319d-295">Configure your mobile app backend for Google sign-in by following the [How to configure App Service for Google login](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="a319d-296">Installeer de Google SDK voor iOS door de [Google Sign-In voor iOS - Start integreren](https://developers.google.com/identity/sign-in/ios/start-integrating) documentatie.</span><span class="sxs-lookup"><span data-stu-id="a319d-296">Install the Google SDK for iOS by following the [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="a319d-297">U kunt de sectie 'Verifiëren met een back-endserver' overslaan.</span><span class="sxs-lookup"><span data-stu-id="a319d-297">You may skip the "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="a319d-298">Voeg het volgende toe aan uw gemachtigde `signIn:didSignInForUser:withError:` methode volgens de taal die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a319d-298">Add the following to your delegate's `signIn:didSignInForUser:withError:` method, according to the language you are using.</span></span>

<span data-ttu-id="a319d-299">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-299">**Objective-C**:</span></span>

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

<span data-ttu-id="a319d-300">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-300">**Swift**:</span></span>

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. <span data-ttu-id="a319d-301">Zorg ervoor dat u ook het volgende toevoegen aan `application:didFinishLaunchingWithOptions:` in uw app gemachtigde, 'SERVER_CLIENT_ID' met dezelfde ID die u gebruikt voor het configureren van App Service in stap 1 vervangen.</span><span class="sxs-lookup"><span data-stu-id="a319d-301">Make sure you also add the following to `application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with the same ID that you used to configure App Service in step 1.</span></span>

<span data-ttu-id="a319d-302">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-302">**Objective-C**:</span></span>

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 <span data-ttu-id="a319d-303">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-303">**Swift**:</span></span>

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. <span data-ttu-id="a319d-304">De volgende code toevoegen aan uw toepassing in een UIViewController waarmee de `GIDSignInUIDelegate` protocol, volgens de taal die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a319d-304">Add the following code to your application in a UIViewController that implements the `GIDSignInUIDelegate` protocol, according to the language you are using.</span></span>  <span data-ttu-id="a319d-305">U bent afgemeld voordat opnieuw wordt ondertekend en hoewel u niet hoeft uw referenties opnieuw invoeren, ziet u een dialoogvenster toestemming.</span><span class="sxs-lookup"><span data-stu-id="a319d-305">You are signed out before being signed in again, and although you don't need to enter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="a319d-306">Deze methode pas aanroepen wanneer het sessietoken is verlopen.</span><span class="sxs-lookup"><span data-stu-id="a319d-306">Only call this method when the session token has expired.</span></span>

   <span data-ttu-id="a319d-307">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a319d-307">**Objective-C**:</span></span>

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   <span data-ttu-id="a319d-308">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="a319d-308">**Swift**:</span></span>

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
[How to: Create the Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data to the user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize the client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
<span data-ttu-id="a319d-309">[Azure Mobile Apps Quick Start]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="a319d-309">[Azure Mobile Apps Quick Start]: app-service-mobile-ios-get-started.md</span></span>

[Add Mobile Services to Existing App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts to authorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
<span data-ttu-id="a319d-310">[dynamische Schema]: http://go.microsoft.com/fwlink/p/?LinkId=296271</span><span class="sxs-lookup"><span data-stu-id="a319d-310">[Dynamic Schema]: http://go.microsoft.com/fwlink/p/?LinkId=296271</span></span>
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI to manage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

<span data-ttu-id="a319d-311">[Dashboard voor Infrastructuurresources]: https://www.fabric.io/home</span><span class="sxs-lookup"><span data-stu-id="a319d-311">[Fabric Dashboard]: https://www.fabric.io/home</span></span>
<span data-ttu-id="a319d-312">[Fabric voor iOS - aan de slag]: https://docs.fabric.io/ios/fabric/getting-started.html</span><span class="sxs-lookup"><span data-stu-id="a319d-312">[Fabric for iOS - Getting Started]: https://docs.fabric.io/ios/fabric/getting-started.html</span></span>
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
