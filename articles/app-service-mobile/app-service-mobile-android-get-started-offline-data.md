---
title: aaaEnable offlinesynchronisatie voor uw Azure Mobile Apps (Android)
description: Meer informatie over hoe toouse App Service Mobile Apps toocache en sync offline gegevens in uw Android-toepassing
documentationcenter: android
author: ggailey777
manager: syntaxc4
services: app-service\mobile
ms.assetid: 32a8a079-9b3c-4faf-8588-ccff02097224
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 34508c7394610cf9127e1753637940826b8fd06a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a>Offlinesynchronisatie voor uw mobiele Android-app inschakelen
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Overzicht
Deze zelfstudie behandelt Hallo offlinesynchronisatie-functie van Azure Mobile Apps voor Android. Offlinesynchronisatie kunnen eindgebruikers gebruikers toointeract met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding. Wijzigingen worden opgeslagen in een lokale database. Zodra Hallo apparaat weer online is, worden deze wijzigingen gesynchroniseerd met Hallo externe back-end.

Als dit uw eerste ervaring met Azure Mobile Apps is, moet u eerst Hallo zelfstudie uitvoeren [maken van een Android-App]. Als u geen gebruik Hallo snel starten-serverproject gedownload, moet u Hallo data access-extensie pakketten tooyour project toevoegen. Zie voor meer informatie over server extensiepakketten [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn meer informatie over Hallo offlinesynchronisatie functie, Zie Hallo onderwerp [Offline synchroniseren van gegevens in Azure Mobile Apps].

## <a name="update-hello-app-toosupport-offline-sync"></a>Hallo app toosupport offlinesynchronisatie bijwerken
Met het offline synchroniseren die u lezen tooand schrijven van een *synchronisatietabel* (met behulp van Hallo *IMobileServiceSyncTable* interface), die deel uitmaakt van een **SQLite** database op het apparaat.

toopush en pull wijzigingen tussen Hallo-apparaat en Azure Mobile Services die u gebruikt een *synchronisatiecontext* (*MobileServiceClient.SyncContext*), die u met de lokale database Hallo initialiseren lokaal toostore gegevens.

1. In `TodoActivity.java`, commentaar Hallo bestaande definitie van `mToDoTable` en verwijder het commentaarteken Hallo tabel synchronisatieversie:
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. In Hallo `onCreate` methode, commentaar Hallo bestaande initialisatie van `mToDoTable` en het commentaar verwijderen van deze definitie voor:
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. In `refreshItemsFromTable` commentaar Hallo definitie van `results` en het commentaar verwijderen van deze definitie voor:
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. Commentaar Hallo definitie van `refreshItemsFromMobileServiceTable`.
5. Verwijder de definitie van Hallo opmerkingen `refreshItemsFromMobileServiceTableSyncTable`:
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. Verwijder de definitie van Hallo opmerkingen `sync`:
   
        private AsyncTask<Void, Void, Void> sync() {
            AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
                @Override
                protected Void doInBackground(Void... params) {
                    try {
                        MobileServiceSyncContext syncContext = mClient.getSyncContext();
                        syncContext.push().get();
                        mToDoTable.pull(null).get();
                    } catch (final Exception e) {
                        createAndShowDialogFromTask(e, "Error");
                    }
                    return null;
                }
            };
            return runAsyncTask(task);
        }

## <a name="test-hello-app"></a>Test Hallo app
In deze sectie kunt u testen Hallo gedrag met Wi-Fi op, en schakelt u vervolgens Wi-Fi toocreate een offline-scenario.

Wanneer u gegevens toevoegt, ze worden beheerd in Hallo lokale SQLite archief, maar niet gesynchroniseerde toohello mobiele service, totdat u op Hallo **vernieuwen** knop. Andere apps kunnen verschillende vereisten met betrekking tot wanneer gegevens toobe gesynchroniseerd moet, maar voor demonstratiedoeleinden in deze zelfstudie heeft Hallo gebruiker deze aanvragen.

Wanneer u op deze knop klikt, wordt er een nieuwe achtergrondtaak gestart. Deze duwt eerst alle wijzigingen toohello lokale archief met synchronisatiecontext, wordt de gegevens worden gewijzigd van Azure toohello lokale tabel.

### <a name="offline-testing"></a>Offline testen
1. Plaats Hallo apparaat of emulator in *vliegtuigmodus*. Hiermee maakt u een offline-scenario.
2. Voeg enkele toe *ToDo* items of bepaalde items als voltooid markeren. Hallo apparaat of emulator (of geforceerd sluiten Hallo app) afsluiten en opnieuw starten. Controleer of dat uw wijzigingen zijn opgeslagen op Hallo apparaat omdat ze worden beheerd in Hallo lokale SQLite-archief.
3. Hallo-inhoud van hello Azure *TodoItem* tabel met een SQL-hulpprogramma zoals *SQL Server Management Studio*, of een REST-client, zoals *Fiddler* of  *Postman*. Controleer of de nieuwe items Hallo hebt *niet* is gesynchroniseerde toohello server
   
       + Ga voor een Node.js-end toohello [Azure-portal](https://portal.azure.com/), en in uw Mobile App back-end op **gemakkelijk tabellen** > **TodoItem** tooview Hallo inhoud Hallo `TodoItem` tabel.
       + Voor een .NET-backend weergave Hallo tabel inhoud met een SQL-hulpprogramma zoals *SQL Server Management Studio*, of een REST-client, zoals *Fiddler* of *Postman*.
4. Wi-Fi inschakelen in Hallo-apparaat of simulator. Klik vervolgens op Hallo **vernieuwen** knop.
5. Hallo takentabel gegevens weer in hello Azure-portal. Hallo die nieuwe en gewijzigde taken wordt nu weergegeven.

## <a name="additional-resources"></a>Aanvullende resources
* [Offline synchroniseren van gegevens in Azure Mobile Apps]
* [Cloud behandeld: Offlinesynchronisatie in Azure Mobile Services] \(Opmerking: Hallo video in Mobile Services, maar offlinesynchronisatie werkt op een vergelijkbare manier als in Azure Mobile Apps\)

<!-- URLs. -->

[Offline synchroniseren van gegevens in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md

[maken van een Android-App]: app-service-mobile-android-get-started.md

[Cloud behandeld: Offlinesynchronisatie in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

