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
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a>Hoe tooUse iOS-clientbibliotheek voor Azure Mobile Apps
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Deze handleiding leert u tooperform algemene scenario's met Hallo nieuwste [iOS SDK voor Azure Mobile Apps][1]. Als u nieuwe tooAzure Mobile Apps, eerst voltooien [Azure Mobile Apps Quick Start] toocreate een back-end van een tabel maken en deze te downloaden van een vooraf samengestelde iOS Xcode-project. In deze handleiding richten we op Hallo clientzijde iOS SDK. toolearn informatie over Hallo van server-side '-SDK voor Hallo back-end, Zie Hallo Server SDK HOWTOs.

## <a name="reference-documentation"></a>Referentiedocumentatie
Hallo-naslagdocumentatie voor Hallo iOS client SDK bevindt zich hier: [Azure Mobile Apps iOS referentie Client][2].

## <a name="supported-platforms"></a>Ondersteunde Platforms
Hallo iOS SDK biedt ondersteuning voor Objective-C-projecten, Swift 2.2 projecten en Swift 2.3 projecten voor iOS-versie 8.0 of hoger.

Hallo 'server-flow' verificatie maakt gebruik van een webweergave voor Hallo gebruikersinterface weergegeven.  Als het Hallo-apparaat is niet kunnen toopresent een UI WebView en vervolgens een andere verificatiemethode is vereist is die buiten Hallo-bereik van Hallo product.  
Deze SDK is derhalve niet geschikt voor controle-type of op dezelfde manier beperkte apparaten.

## <a name="Setup"></a>Het installatieprogramma en vereisten
Deze handleiding wordt ervan uitgegaan dat u een back-end hebt gemaakt met een tabel. Deze handleiding wordt ervan uitgegaan dat Hallo-tabel heeft hetzelfde schema Hallo tabellen in deze zelfstudies. Deze handleiding wordt ervan uitgegaan dat in uw code u verwijzen naar `MicrosoftAzureMobile.framework` en importeer `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.

## <a name="create-client"></a>How to: Client maken
Maak een back-end van Azure Mobile Apps in uw project tooaccess een `MSClient`. Vervang `AppUrl` met Hallo app-URL. U laten `gatewayURLString` en `applicationKey` leeg. Als u een gateway voor verificatie instelt, vullen `gatewayURLString` met Hallo gateway URL.

**Objective-C**:

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

**SWIFT**:

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <a name="table-reference"></a>How to: tabelverwijzing maken
tooaccess of update gegevens, maken een verwijzing toohello back-end-tabel. Vervang `TodoItem` met de naam van de tabel Hallo

**Objective-C**:

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

**SWIFT**:

```
let table = client.tableWithName("TodoItem")
```


## <a name="querying"></a>Procedure: een Query over gegevens
toocreate een databasequery query Hallo `MSTable` object. Hallo volgende query haalt alle Hallo items in `TodoItem` en logboeken Hallo tekst van elk item.

**Objective-C**:

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

**SWIFT**:

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

## <a name="filtering"></a>How to: Filter gegevens geretourneerd
toofilter resultaten, er zijn veel opties beschikbaar.

met behulp van een predicaat, gebruik toofilter een `NSPredicate` en `readWithPredicate`. Hallo volgende filtert geretourneerde gegevens toofind alleen onvolledige Todo-items.

**Objective-C**:

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

**SWIFT**:

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

## <a name="query-object"></a>How to: MSQuery gebruiken
tooperform maken van een complexe query's (inclusief sortering en paginering), een `MSQuery` object, rechtstreeks of via een predikaat:

**Objective-C**:

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

**SWIFT**:

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

`MSQuery`kunt u verschillende query gedrag bepalen.

* Geef de volgorde van resultaten
* Welke velden tooreturn beperken
* Hoeveel records tooreturn beperken
* Totaal aantal opgeven om in het antwoord
* Aangepaste queryreeksparameters in aanvraag opgeven
* Aanvullende functies toepassen

Uitvoeren van een `MSQuery` query door het aanroepen van `readWithCompletion` op Hallo-object.

## <a name="sorting"></a>How to: gegevens met MSQuery sorteren
toosort resultaten, bekijk een voorbeeld. toosort op het veld 'text' oplopende, vervolgens op het 'complete' aflopende aanroepen `MSQuery` als volgt te werk:

**Objective-C**:

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

**SWIFT**:

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


## <a name="selecting"></a><a name="parameters"></a>How to: beperken van velden en vouw queryreeksparameters met MSQuery
toolimit velden toobe geretourneerd in een query opgeven Hallo namen van Hallo velden in Hallo **selectFields** eigenschap. In dit voorbeeld retourneert alleen tekst hello en voltooide velden:

**Objective-C**:

```
query.selectFields = @[@"text", @"complete"];
```

**SWIFT**:

```
query.selectFields = ["text", "complete"]
```

de aanvullende queryreeksparameters tooinclude in Hallo-server aanvragen (bijvoorbeeld omdat ze maakt gebruik van een aangepast script van de server-side), vullen `query.parameters` als volgt te werk:

**Objective-C**:

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

**SWIFT**:

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <a name="paging"></a>How to: paginaformaat configureren
Met Azure Mobile Apps Hallo Hallo grootte paginabesturingselementen aantal records dat tegelijk uit Hallo back-end tabellen worden opgehaald. Een gesprek te starten`pull` gegevens zou vervolgens batch-up van gegevens, op basis van dit paginaformaat totdat er geen meer records toopull.

Het is mogelijk tooconfigure een pagina grootte met **MSPullSettings** zoals hieronder wordt weergegeven. Hallo standaardpaginaformaat 50 en Hallo in het volgende voorbeeld wordt too3.

U kunt een ander paginaformaat Prestatieoverwegingen configureren. Als er een groot aantal kleine gegevensrecords, vermindert een hoge paginaformaat Hallo aantal retouren van de server.

Deze instelling bepaalt alleen Hallo paginagrootte aan clientzijde Hallo. Als Hallo client om een pagina groter vraagt dan het Hallo Mobile Apps-back-end wordt ondersteund, is het paginaformaat Hallo beperkt tot Hallo maximale Hallo backend geconfigureerde toosupport is.

Deze instelling is ook Hallo *getal* van records met gegevens niet Hallo *bytegrootte*.

Als u Hallo client paginagrootte verhoogt, moet u ook de paginagrootte Hallo op Hallo server verhogen. Zie [' How to: Hallo tabel paginering grootte aanpassen '](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) voor Hallo toodo dit stappen.

**Objective-C**:

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


**SWIFT**:

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <a name="inserting"></a>How to: gegevens invoegen
maken van een nieuwe tabelrij tooinsert een `NSDictionary` en oproepen `table insert`. Als [dynamische Schema] is ingeschakeld, hello Azure App Service mobiele back-end genereert automatisch nieuwe kolommen die zijn gebaseerd op Hallo `NSDictionary`.

Als `id` is niet opgegeven Hallo back-end automatisch een nieuwe unieke ID genereert. Geef uw eigen `id` toouse e-adressen, gebruikersnamen of uw eigen aangepaste waarden als de ID. Uw eigen ID bieden gemakkelijker joins en database zakelijke logica.

Hallo `result` bevat nieuwe Hallo-item dat is ingevoegd. Afhankelijk van de logische server wellicht aanvullende of gewijzigde gegevens vergeleken toowhat toohello server is doorgegeven.

**Objective-C**:

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

**SWIFT**:

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

## <a name="modifying"></a>How to: gegevens wijzigen
een bestaande rij tooupdate wijzigen een item en de aanroep `update`:

**Objective-C**:

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

**SWIFT**:

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

U kunt ook Hallo rij-ID en het Hallo bijgewerkt veld opgeven:

**Objective-C**:

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**SWIFT**:

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

Ten minste Hallo `id` kenmerk moet worden ingesteld bij het maken van updates.

## <a name="deleting"></a>How to: gegevens verwijderen
aanroepen van toodelete een item, `delete` met Hallo item:

**Objective-C**:

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**SWIFT**:

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

U kunt ook verwijderen door op te geven van een rij-ID:

**Objective-C**:

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**SWIFT**:

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

Ten minste Hallo `id` kenmerk moet worden ingesteld wanneer u wordt verwijderd.

## <a name="customapi"></a>How to: aangepaste API aanroepen
Met een aangepaste API kan geen back-end-functies worden blootgesteld. Heeft geen toomap tooa tabel bewerking. Niet alleen doet u meer controle krijgen over messaging, maar u kunt zelfs lezen/set headers en het Hallo-antwoordindeling hoofdtekst wijzigen. hoe toocreate aangepaste API op Hallo backend, lees toolearn [aangepaste API's](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)

toocall aangepaste API aanroepen `MSClient.invokeAPI`. Hallo-aanvraag en -antwoord inhoud worden behandeld als JSON. toouse andere mediatypen [gebruik andere overbelasting van de Hallo `invokeAPI` ] [ 5].  toomake een `GET` aanvragen in plaats van een `POST` aanvraagt, setparameter `HTTPMethod` te`"GET"` en parameter `body` te`nil` (omdat de GET-aanvragen beschikt niet over de berichttekst.) Als uw aangepaste API andere HTTP-termen ondersteunt, wijzigt u `HTTPMethod` op de juiste wijze.

**Objective-C**:

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

**SWIFT**:

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

## <a name="templates"></a>Hoe: Register sjablonen toosend platformoverschrijdende pushmeldingen
tooregister sjablonen, doorgeven sjablonen met uw **client.push registerDeviceToken** methode in uw client-app.

**Objective-C**:

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

**SWIFT**:

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

Uw sjablonen van het type NSDictionary en kunnen meerdere sjablonen in de volgende indeling Hallo bevatten:

**Objective-C**:

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

**SWIFT**:

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

Alle codes zijn verwijderd uit het Hallo-aanvraag voor beveiliging.  tooadd tags tooinstallations of sjablonen binnen installaties, Zie [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps][4].  toosend meldingen met behulp van deze sjablonen geregistreerde werken met [Notification Hubs-API's][3].

## <a name="errors"></a>How to: afhandelen van fouten
Wanneer u een Azure App Service mobiele back-end aanroept, Hallo voltooiing blok bevat een `NSError` parameter. Wanneer er een fout optreedt, wordt met deze parameter niet nul is. U moet deze parameter inschakelt en verwerken Hallo fout indien nodig, zoals wordt beschreven in voorgaande codefragmenten Hallo in uw code.

Hallo bestand [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] definieert Hallo constanten `MSErrorResponseKey`, `MSErrorRequestKey`, en `MSErrorServerItemKey`. tooget toohello fout met betrekking tot meer gegevens:

**Objective-C**:

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

**SWIFT**:

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

Hallo-bestand definieert bovendien constanten voor elke foutcode:

**Objective-C**:

```
if (error.code == MSErrorPreconditionFailed) {
```

**SWIFT**:

```
if (error.code == MSErrorPreconditionFailed) {
```

## <a name="adal"></a>Procedure: verificatie van gebruikers met Active Directory Authentication Library Hallo
U kunt Hallo Active Directory Authentication Library (ADAL) toosign gebruikers in uw toepassing met Azure Active Directory. Clientverificatie-stroom met een id-provider SDK is beter toousing hello `loginWithProvider:completion:` methode.  Stroom clientverificatie biedt een meer systeemeigen UX idee en kunt u extra aanpassingen.

1. Uw mobiele app back-end voor aanmelding bij de AAD configureren door de volgende Hallo [hoe tooconfigure App Service voor Active Directory-aanmelding] [ 7] zelfstudie. Zorg ervoor dat toocomplete Hallo optionele stap voor het registreren van een systeemeigen clienttoepassing van. Voor iOS, raden we aan dat Hallo omleidings-URI Hallo vorm is `<app-scheme>://<bundle-id>`. Zie voor meer informatie, Hallo [ADAL iOS Quick Start][8].
2. Installeren met behulp van Cocoapods ADAL. Uw Podfile tooinclude Hallo definitie te volgen en vervangt bewerken **uw PROJECT** met Hallo-naam van uw Xcode-project:

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   en Hallo schil:

        pod 'ADALiOS'
3. Hallo Terminal uitvoeren met `pod install` uit Hallo directory waarin u uw project en open vervolgens Hallo gegenereerd Xcode-werkruimte (geen Hallo project).
4. Voeg Hallo code tooyour toepassing te volgen, op basis van toohello taal die u gebruikt. In elk, moet u deze vervangingen:

   * Vervang **INSERT-instantie-hier** met de naam van de Hallo van Hallo tenant waarin u uw toepassing hebt ingericht. De indeling moet https://login.microsoftonline.com/contoso.onmicrosoft.com. Deze waarde kan worden gekopieerd Hallo domein tabblad in uw Azure Active Directory in Hallo [klassieke Azure portal].
   * Vervang **INSERT RESOURCE-ID hier** met Hallo client-ID voor uw back-end voor de mobiele app. U kunt de client-ID verkrijgen van Hallo **Geavanceerd** tabblad onder **Azure Active Directory-instellingen** in Hallo-portal.
   * Vervang **INSERT-CLIENT-ID-hier** met client-ID Hallo u hebt gekopieerd uit Hallo native client-toepassing.
   * Vervang **INSERT-OMLEIDINGS-URI-hier** aan uw site */.auth/login/done* eindpunt, met Hallo HTTPS-schema. Deze waarde moet er ongeveer te*https://contoso.azurewebsites.net/.auth/login/done*.

**Objective-C**:

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


**SWIFT**:

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

## <a name="facebook-sdk"></a>Procedure: verificatie van gebruikers met Hallo Facebook SDK voor iOS
U kunt Hallo Facebook SDK voor iOS toosign gebruikers in uw toepassing met Facebook.  Met behulp van een stroom clientverificatie is beter toousing hello `loginWithProvider:completion:` methode.  Hallo-clientverificatie stroom biedt een meer systeemeigen UX idee en kunt u extra aanpassingen.

1. Uw mobiele app back-end voor aanmelding bij Facebook instellen door de [hoe tooconfigure App Service voor Facebook aanmelding] [ 9] zelfstudie.
2. Hallo Facebook SDK voor iOS door de volgende Hallo installeren [Facebook SDK voor iOS - aan de slag] [ 10] documentatie. In plaats van een app maken, kunt u bestaande tooyour-registratie van de Hallo iOS-platform toevoegen.
3. Facebook van documentatie bevat enkele Objective-C-code in Hallo App gemachtigde. Als u **Swift**, kunt u Hallo vertalingen voor AppDelegate.swift te volgen:

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
4. In aanvulling tooadding `FBSDKCoreKit.framework` tooyour project, Voeg een verwijzing ook te`FBSDKLoginKit.framework` in Hallo dezelfde manier.
5. Voeg Hallo code tooyour toepassing te volgen, op basis van toohello taal die u gebruikt.

**Objective-C**:

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

**SWIFT**:

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

## <a name="twitter-fabric"></a>Procedure: verificatie van gebruikers met Twitter Fabric voor iOS
U kunt voor iOS toosign gebruikers Fabric in uw toepassing met Twitter. Clientverificatie voor de stroom is beter toousing hello `loginWithProvider:completion:` methode, zoals deze biedt een meer systeemeigen UX idee en kunt u extra aanpassingen.

1. Uw mobiele app back-end voor aanmelding bij Twitter configureren door de volgende Hallo [hoe tooconfigure App Service voor Twitter aanmelding](app-service-mobile-how-to-configure-twitter-authentication.md) zelfstudie.
2. Voeg Fabric tooyour project met de volgende Hallo [Fabric voor iOS - aan de slag] documentatie en TwitterKit in te stellen.

   > [!NOTE]
   > Standaard Fabric Twitter-toepassing voor u gemaakt. U kunt voorkomen dat het maken van een toepassing registreren Hallo Consumer-sleutel en consumentgeheim eerder met Hallo volgende codefragmenten hebt gemaakt.    U kunt ook kunt u Hallo consumentsleutel vervangen en consumentgeheim waarden op te geven tooApp Service Hello waarden die u hebt ziet in Hallo [Dashboard voor Infrastructuurresources]. Als u deze optie kiest, is ervoor tooset Hallo callback URL tooa tijdelijke aanduiding voor waarde, zoals `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.
   >
   >

    Als u toouse Hallo geheimen die u eerder hebt gemaakt kiest, toevoegen Hallo code tooyour App gemachtigde te volgen:

    **Objective-C**:

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

    **SWIFT**:

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. Voeg Hallo code tooyour toepassing te volgen, op basis van toohello taal die u gebruikt.

**Objective-C**:

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

**SWIFT**:

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

## <a name="google-sdk"></a>Procedure: verificatie van gebruikers met Hallo Google-In SDK voor iOS
U kunt Hallo Google-In SDK voor iOS toosign gebruikers in uw toepassing met behulp van een Google-account gebruiken.  Google aangekondigd onlangs wijzigingen tootheir OAuth-beveiligingsbeleid.  Deze beleidswijzigingen vereist het gebruik van de Google-SDK in toekomstige Hallo Hallo.

1. Uw mobiele app back-end voor Google aanmelding configureren door de volgende Hallo [hoe tooconfigure App Service voor Google aanmelding](app-service-mobile-how-to-configure-google-authentication.md) zelfstudie.
2. Hallo Google SDK voor iOS door de volgende Hallo installeren [Google Sign-In voor iOS - Start integreren](https://developers.google.com/identity/sign-in/ios/start-integrating) documentatie. Hallo verifiëren met een back-end sectie 'Server', kunt u overslaan.
3. Hallo van tooyour gemachtigde na toevoegen `signIn:didSignInForUser:withError:` methode op basis van toohello taal die u gebruikt.

**Objective-C**:

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

**SWIFT**:

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. Zorg ervoor dat u ook de volgende te Hallo toevoegen`application:didFinishLaunchingWithOptions:` delegeren in uw app, "SERVER_CLIENT_ID" vervangen door een Hallo dezelfde ID die u hebt gebruikt tooconfigure App Service in stap 1.

**Objective-C**:

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 **SWIFT**:

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. Hallo na code tooyour toepassing in een UIViewController waarmee Hallo toevoegen `GIDSignInUIDelegate` -protocol op basis van toohello taal die u gebruikt.  U bent afgemeld voordat opnieuw wordt ondertekend en hoewel u niet tooenter uw referenties opnieuw hoeft, ziet u een dialoogvenster toestemming.  Deze methode pas aanroepen wanneer Hallo sessietoken is verlopen.

   **Objective-C**:

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   **SWIFT**:

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
