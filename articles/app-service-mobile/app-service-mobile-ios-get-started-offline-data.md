---
title: offline synchronisatie van aaaEnable met mobiele iOS-apps | Microsoft Docs
description: Meer informatie over hoe toouse Azure App Service mobile apps toocache en sync offline gegevens in iOS-toepassingen.
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: eb5b9520-0f39-4a09-940a-dadb6d940db8
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 570ea7cf6694ab7317c977331038929b64508ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a>Offline synchronisatie met de mobiele iOS-apps inschakelen
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Overzicht
Deze zelfstudie wordt behandeld offline synchronisatie met de functie van Azure App Service Mobile Apps voor iOS Hallo. Met offline synchroniseert eindgebruikers kunnen communiceren met een mobiele app tooview, toevoegen of wijzigen van gegevens, zelfs wanneer er geen netwerkverbinding. Wijzigingen worden opgeslagen in een lokale database. Nadat het Hallo-apparaat weer online is, worden Hallo wijzigingen gesynchroniseerd met de Hallo externe back-end.

Als dit uw eerste ervaring met Mobile Apps is, moet u eerst Hallo zelfstudie uitvoeren [maken van een iOS-App]. Als u snel starten-serverproject Hallo gedownload niet gebruikt, moet u Hallo gegevenstoegang pakketten tooyour extensieproject toevoegen. Zie voor meer informatie over server extensiepakketten [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn meer informatie over Hallo offlinesynchronisatie functie, Zie [Offline synchroniseren van gegevens in mobiele Apps].

## <a name="review-sync"></a>Hallo-clientcode sync controleren
Hallo client-project dat u hebt gedownload voor Hallo [maken van een iOS-App] zelfstudie bevat al de code die ondersteuning biedt voor offlinesynchronisatie met behulp van een lokale database op basis van gegevens van de Core. Deze sectie bevat een overzicht van wat is al opgenomen in de zelfstudie Hallo-code. Zie voor een conceptueel overzicht van de functie Hallo [Offline synchroniseren van gegevens in mobiele Apps].

Met de functie voor het offline synchroniseren van gegevens van Hallo van Mobile Apps, kunnen eindgebruikers communiceren met een lokale database zelfs wanneer het Hallo-netwerk is niet toegankelijk. toouse wanneer u Hallo sync context van deze functies in uw app initialiseren `MSClient` en verwijzen naar een lokaal archief. Vervolgens u verwijzen naar de tabel via Hallo **MSSyncTable** interface.

In **QSTodoService.m** (Objective-C) of **ToDoTableViewController.swift** (Swift), u ziet dat het type van lid Hallo Hallo **syncTable** is  **MSSyncTable**. Offline synchronisatie maakt gebruik van deze synchronisatie tabel interface in plaats van **MSTable**. Wanneer een synchronisatietabel wordt gebruikt, alle bewerkingen gaat u het lokale archief toohello en zijn gesynchroniseerd met de Hallo externe back-end met expliciete push en pull-bewerkingen.

 tooget een tooa sync verwijzingstabel, gebruik Hallo **syncTableWithName** methode op `MSClient`. functie voor het offline synchroniseren van tooremove, gebruik **tableWithName** in plaats daarvan.

Voordat u tabelbewerkingen kunnen uitvoeren, moet het lokale archief Hallo worden geïnitialiseerd. Dit is de relevante code Hallo:

* **Objective-C**. In Hallo **QSTodoService.init** methode:

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* **SWIFT**. In Hallo **ToDoTableViewController.viewDidLoad** methode:

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   Deze methode maakt u een lokaal archief met behulp van Hallo `MSCoreDataStore` interface, waardoor Hallo Mobile Apps SDK biedt. U kunt ook een ander lokaal archief opgeven door het implementeren van Hallo `MSSyncContextDataSource` protocol. Bovendien Hallo eerste parameter van **MSSyncContext** gebruikte toospecify is een conflict-handler. Omdat we hebt doorgegeven `nil`, krijgen we Hallo standaard conflict handler, die niet bij een conflict.

Nu gaan we de werkelijke synchronisatiebewerking Hallo uitvoeren en gegevens ophalen uit externe back-end van Hallo:

* **Objective-C**. `syncData`eerst pushes nieuwe wijzigingen en roept vervolgens **pullData** tooget gegevens van Hallo externe back-end. Op zijn beurt Hallo **pullData** methode haalt nieuwe gegevens die overeenkomt met een query:

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in hello sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from hello remote server into hello local table.
       // We're pulling all items and filtering in hello view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets hello caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* **SWIFT**:
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via hello MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep hello server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation tooitem \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting tooserver's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

Hallo Objective-C-versie in `syncData`, noemen we eerst **pushWithCompletion** op Hallo sync context. Deze methode maakt deel uit van `MSSyncContext` (en niet Hallo synchronisatietabel zelf) omdat deze wijzigingen pushes in alle tabellen. Alleen de records die zijn gewijzigd op een bepaalde manier lokaal (via CUD bewerkingen) worden toohello server verzonden. Vervolgens Hallo helper **pullData** wordt genoemd, welke aanroepen **MSSyncTable.pullWithQuery** tooretrieve externe gegevens en op te slaan in de lokale database Hallo.

Hallo Swift versie, omdat het Hallo-push-bewerking is niet strikt noodzakelijk is, er is geen aanroep te**pushWithCompletion**. Als er wijzigingen in behandeling in Hallo sync context voor Hallo-tabel die een push-bewerking doet zijn, pull-altijd problemen met een push eerst. Als er meer dan één synchronisatietabel, is het beste tooexplicitly aanroep push tooensure dat alles consistent is voor alle gerelateerde tabellen.

In Hallo Objective-C en Swift versies, kunt u Hallo **pullWithQuery** methode toospecify een query toofilter Hallo gewenste tooretrieve records. In dit voorbeeld Hallo query haalt u alle records in externe Hallo `TodoItem` tabel.

tweede parameter van Hallo **pullWithQuery** een query-id die wordt gebruikt voor *incrementele synchronisatie*. Incrementele synchronisatie alleen records die zijn gewijzigd sinds de laatste synchronisatie hello, met behulp van de record Hallo haalt `UpdatedAt` tijdstempel (aangeroepen `updatedAt` in Hallo lokale opslag.) Hallo query-ID moet een beschrijvende tekenreeks die uniek is voor elke logische query uw app. tooopt incrementele synchroon doorgeven `nil` zoals Hallo query-ID. Deze methode kan worden mogelijk inefficiënt, omdat het ophalen van alle records op elk pull-bewerking.

Hallo Objective-C-app wordt gesynchroniseerd wanneer u wijzigen of toevoegen van gegevens, wanneer een gebruiker Hallo vernieuwen gebaar uitvoert, en op starten.

Hallo Swift app wordt gesynchroniseerd wanneer Hallo gebruiker Hallo vernieuwen gebaar uitvoert en op starten.

Omdat hello app wordt gesynchroniseerd wanneer de gegevens zijn gewijzigd (Objective-C) of wanneer het Hallo-app gestart (Objective-C en Swift), Hallo-app wordt ervan uitgegaan dat die gebruiker Hallo online. In een volgende sectie wordt u Hallo app bijwerken zodat gebruikers bewerken kunnen, zelfs als ze offline zijn.

## <a name="review-core-data"></a>Bekijk Hallo Core-gegevensmodel
Wanneer u Hallo Core offline gegevensarchief gebruikt, moet u bepaalde tabellen en velden definiëren in het gegevensmodel. Hallo voorbeeld-app bevat al een gegevensmodel met de juiste notatie Hallo. In deze sectie bekijken we deze tabellen tooshow hoe ze worden gebruikt.

Open **QSDataModel.xcdatamodeld**. Vier tabellen zijn gedefinieerd--drie die worden gebruikt door de SDK Hallo en één die wordt gebruikt voor de taak Hallo zelf-items:
  * MS_TableOperations: Houdt Hallo items die u toobe gesynchroniseerd met de Hallo-server moet.
  * MS_TableOperationErrors: Houdt eventuele fouten die tijdens het offline synchroniseren optreden.
  * MS_TableConfig: Houdt Hallo laatst bijgewerkt voor de laatste synchronisatiebewerking Hallo voor alle pull-bewerkingen.
  * Takentabel: Slaat Hallo taakitems. Hallo systeemkolommen **createdAt**, **updatedAt**, en **versie** zijn optionele Systeemeigenschappen.

> [!NOTE]
> Hallo Mobile Apps SDK reserveert kolomnamen die met beginnen '**``**'. Dit voorvoegsel niet gebruiken voor iets anders dan systeemkolommen. Anders wordt uw kolomnamen gewijzigd wanneer u Hallo externe back-end.
>
>

Wanneer u Hallo offlinesynchronisatie functie gebruikt, definiëren Hallo drie tabellen en Hallo gegevenstabel.

### <a name="system-tables"></a>Systeemtabellen

**MS_TableOperations**  

![MS_TableOperations tabelkenmerken][defining-core-data-tableoperations-entity]

| Kenmerk | Type |
| --- | --- |
| id | Geheel getal 64 |
| itemId | Tekenreeks |
| properties | Binaire gegevens |
| Tabel | Tekenreeks |
| tableKind | Geheel getal 16 |


**MS_TableOperationErrors**

 ![MS_TableOperationErrors tabelkenmerken][defining-core-data-tableoperationerrors-entity]

| Kenmerk | Type |
| --- | --- |
| id |Tekenreeks |
| operationId |Geheel getal 64 |
| properties |Binaire gegevens |
| tableKind |Geheel getal 16 |

 **MS_TableConfig**

 ![][defining-core-data-tableconfig-entity]

| Kenmerk | Type |
| --- | --- |
| id |Tekenreeks |
| sleutel |Tekenreeks |
| KeyType |Geheel getal 64 |
| Tabel |Tekenreeks |
| waarde |Tekenreeks |

### <a name="data-table"></a>Gegevenstabel

**Takentabel**

| Kenmerk | Type | Opmerking |
| --- | --- | --- |
| id | Tekenreeks is gemarkeerd als vereist |primaire sleutel in externe opslag |
| Voltooien | Booleaanse waarde | Taak itemveld |
| Tekst |Tekenreeks |Taak itemveld |
| CreatedAt | Date | (optioneel) Toegewezen te**createdAt** systeemeigenschap |
| updatedAt | Date | (optioneel) Toegewezen te**updatedAt** systeemeigenschap |
| Versie | Tekenreeks | (optioneel) Gebruikte toodetect conflicten, maps tooversion |

## <a name="setup-sync"></a>Hallo sync-gedrag Hallo app wijzigen
In deze sectie maakt wijzigen u Hallo app zodat deze wordt niet gesynchroniseerd op app starten of als u invoegen en items bijwerken. Synchronisatie alleen wanneer de knop voor vernieuwen gebaar hello wordt uitgevoerd.

**Objective-C**:

1. In **QSTodoListViewController.m**, Hallo wijzigen **viewDidLoad** methode tooremove Hallo aanroep te`[self refresh]` achter Hallo Hallo-methode. Hallo-gegevens is nu niet gesynchroniseerd met de server Hallo op app starten. In plaats daarvan wordt deze gesynchroniseerd met inhoud van het lokale archief Hallo Hallo.
2. In **QSTodoService.m**, Wijzig definitie van Hallo `addItem` zodat deze niet synchroniseren nadat het Hallo-item is ingevoegd. Hallo verwijderen `self syncData` blokkeren en vervang deze door de volgende Hallo:

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. Wijzigen van de definitie van Hallo `completeItem` zoals eerder is vermeld. Hallo-blokkering voor verwijderen `self syncData` en vervang deze door de volgende Hallo:
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

**SWIFT**:

In `viewDidLoad`in **ToDoTableViewController.swift**, commentaar Hallo twee regels hier, toostop synchroniseren bij starten van de app weergegeven. Op moment van schrijven van dit Hallo Hallo Swift Todo-app niet Hallo-service bijgewerkt wanneer iemand toevoegt of een item is voltooid. Hallo-service alleen op app starten wordt bijgewerkt.

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <a name="test-app"></a>Test Hallo app
In deze sectie maakt verbinding u tooan ongeldige URL toosimulate een offline-scenario. Wanneer u gegevens toevoegt, zijn ze ondergebracht in Hallo lokale Core gegevens opslaan, maar ze zijn niet gesynchroniseerd met de Hallo back-end van mobile app.

1. Wijzig Hallo mobiele app-URL in **QSTodoService.m** tooan ongeldige URL en opnieuw uitvoeren Hallo-app:

   **Objective-C**. In QSTodoService.m:
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   **SWIFT**. In ToDoTableViewController.swift:
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. Sommige taakitems toevoegen. Sluit simulator hello (of geforceerd sluiten Hallo app) af en start deze opnieuw. Controleer of uw wijzigingen blijven behouden.

3. Hallo-inhoud van de externe Hallo weergeven **TodoItem** tabel:
   * Ga voor Node.js-back-end toohello [Azure-portal](https://portal.azure.com/) en op uw mobiele app back-end, **gemakkelijk tabellen** > **TodoItem**.  
   * Voor een .NET terug beëindigen, gebruikt u een SQL-hulpprogramma, zoals SQL Server Management Studio of een REST-client, zoals Fiddler of Postman.  

4. Controleer of de nieuwe items Hallo hebt *niet* is gesynchroniseerd met de Hallo-server.

5. Wijziging Hallo URL back toohello corrigeren in **QSTodoService.m**, en Voer Hallo-app.

6. Hallo vernieuwen gebaar uitvoeren met het binnenhalen van Hallo lijst met items.  
Een spinner voortgang wordt weergegeven.

7. Weergave Hallo **TodoItem** gegevens opnieuw. nieuwe en gewijzigde taakitems Hallo moeten nu worden weergegeven.

## <a name="summary"></a>Samenvatting
toosupport hello offlinesynchronisatie functie we Hallo gebruikt `MSSyncTable` interface en geïnitialiseerd `MSClient.syncContext` met een lokaal archief. In dit geval is het lokale archief Hallo een database op basis van gegevens van de Core.

Wanneer u een Core lokale gegevensarchief gebruikt, moet u verschillende tabellen met Hallo definiëren [corrigeren Systeemeigenschappen](#review-core-data).

Hallo normaal maken, lezen, bijwerken en verwijderen (CRUD)-bewerkingen voor mobiele apps werken alsof Hallo app nog steeds is verbonden, maar alle Hallo acties moeten worden uitgevoerd tegen Hallo lokale opslag.

Wanneer we het lokale archief Hallo gesynchroniseerd met de Hallo-server, hebben we Hallo gebruikt **MSSyncTable.pullWithQuery** methode.

## <a name="additional-resources"></a>Aanvullende bronnen
* [Offline synchroniseren van gegevens in mobiele Apps]
* [Cloud behandeld: Offlinesynchronisatie in Azure Mobile Services] \(Hallo video gaat over Mobile Services, maar Mobile Apps offline synchronisatie werkt op een vergelijkbare manier.\)

<!-- URLs. -->


[maken van een iOS-App]: app-service-mobile-ios-get-started.md
[Offline synchroniseren van gegevens in mobiele Apps]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[Cloud behandeld: Offlinesynchronisatie in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
