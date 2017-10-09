---
title: aaaImport en exporteren van gegevens in Azure Redis-Cache | Microsoft Docs
description: Meer informatie over hoe gegevens tooand van tooimport en exporteren van blob-opslag met de exemplaren van uw premium Azure Redis-Cache
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 4a68ac38-87af-4075-adab-569d37d7cc9e
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: sdanie
ms.openlocfilehash: f17464b207f1c652952f4da63ca147473fee2759
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-data-in-azure-redis-cache"></a>Importeren en exporteren van gegevens in Azure Redis-Cache
Import/Export is een Azure Redis-Cache gegevensbewerking voor het beheer, waarmee u tooimport gegevens in Azure Redis-Cache of het exporteren van gegevens van Azure Redis-Cache door te importeren en exporteren van een momentopname van een Redis-Cache Database (RDB) van een blob premium cache tooa in een Azure Storage-Account. 

- **Exporteren** -kunt u uw Azure Redis-Cache RDB momentopnamen tooa pagina-Blob exporteren.
- **Importeren** -u kunt de momentopnamen van uw Redis-Cache RDB importeren uit een pagina-Blob of een blok-Blob.

Voor importeren/exporteren kunt u toomigrate tussen verschillende exemplaren van Azure Redis-Cache of vullen Hallo cache met gegevens voor het gebruik.

In dit artikel bevat richtlijnen voor het importeren en exporteren van gegevens met Azure Redis-Cache en vindt u antwoorden Hallo toocommonly vragen.

> [!IMPORTANT]
> Import/Export is Preview-versie en is alleen beschikbaar voor [premium-laag](cache-premium-tier-intro.md) in de cache opslaat.
>
>

## <a name="import"></a>Importeren
Importeren kan gebruikte toobring Redis compatibele RDB bestanden vanaf een willekeurige Redis-server uitgevoerd in een cloud of de omgeving, inclusief Redis uitgevoerd op Linux, Windows of elke cloudprovider zoals Amazon Web Services en andere zijn. Het importeren van gegevens is een eenvoudige manier toocreate een cache met vooraf ingestelde gegevens. Tijdens het importproces Hallo, Azure Redis-Cache Hallo RDB bestanden uit Azure storage in het geheugen geladen en vervolgens ingevoegd Hallo sleutels in Hallo-cache.

> [!NOTE]
> Voordat u de importbewerking Hallo begint, controleert u of uw Redis-Database (RDB) of meer bestanden zijn geüpload naar de pagina of blok-blobs in Azure-opslag in Hallo dezelfde regio en abonnement als uw Azure Redis-Cache-exemplaar. Zie voor meer informatie [aan de slag met Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Als u uw RDB-bestand met behulp van Hallo geëxporteerd [exporteren van Azure Redis-Cache](#export) functie, het bestand RDB is al opgeslagen in een pagina-blob en is gereed om te importeren.
>
>

1. tooimport een of meer blobs, cache, geëxporteerd [tooyour cache Bladeren](cache-configure.md#configure-redis-cache-settings) in hello Azure-portal en klikt u op **gegevens importeren** van Hallo **Resource menu**.

    ![Gegevens importeren][cache-import-data]
2. Klik op **kiezen Blob(s)** en selecteer Hallo storage-account dat Hallo gegevens tooimport bevat.

    ![Opslagaccount kiezen][cache-import-choose-storage-account]
3. Klik op Hallo-container die Hallo gegevens tooimport bevat.

    ![Kies container][cache-import-choose-container]
4. Selecteer een of meer blobs tooimport door te klikken op Hallo gebied toohello links van Hallo blob-naam en klik vervolgens op **Selecteer**.

    ![Kies BLOB 's][cache-import-choose-blobs]
5. Klik op **importeren** toobegin Hallo importproces.

   > [!IMPORTANT]
   > Hallo-cache is niet toegankelijk is voor cacheclients tijdens het importeren van Hallo en alle bestaande gegevens in cache Hallo is verwijderd.
   >
   >

    ![Importeren][cache-import-blobs]

    U kunt voortgang Hallo van importbewerking Hallo door volgende Hallo meldingen van hello Azure-portal of door het Hallo-gebeurtenissen weergeven in Hallo [controlelogboek](../azure-resource-manager/resource-group-audit.md).

    ![Voortgang importeren][cache-import-data-import-complete]

## <a name="export"></a>Exporteren
Exporteren kunt u tooexport Hallo opgeslagen gegevens in Azure Redis-Cache tooRedis compatibel RDB bestanden. U kunt deze functie toomove op gegevens uit een Azure Redis-Cache-exemplaar tooanother of tooanother Redis-server gebruiken. Tijdens het exportproces hello, wordt een tijdelijk bestand op Hallo VM dat hosts Hallo server-exemplaar van Azure Redis-Cache en Hallo bestand geüploade toohello aangewezen storage-account is gemaakt. Wanneer de exportbewerking Hallo is voltooid met de status van slagen of mislukken, wordt Hallo tijdelijk bestand verwijderd.

1. tooexport hello huidige inhoud van Hallo cache toostorage, [tooyour cache Bladeren](cache-configure.md#configure-redis-cache-settings) in hello Azure-portal en klikt u op **gegevens exporteren** van Hallo **Resource menu**.

    ![Kies de opslagcontainer][cache-export-data-choose-storage-container]
2. Klik op **Opslagcontainer Kies** en selecteer de gewenste Hallo storage-account. Hallo storage-account moet zich in Hallo hetzelfde abonnement en dezelfde regio bevinden als uw cache.

   > [!IMPORTANT]
   > Werkt met pagina-blobs, die worden ondersteund door zowel klassieke als Resource Manager storage-accounts, maar worden niet ondersteund door exporteren [Blob storage-accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts) op dit moment.
   >
   >

    ![Storage-account][cache-export-data-choose-account]
3. Kies Hallo blob-container en klik op de gewenste **Selecteer**. toouse nieuwe container, klikt u op **Container toevoegen** tooadd het eerste en selecteer vervolgens het uit de lijst Hallo.

    ![Kies de opslagcontainer][cache-export-data-container]
4. Typ een **Blob voorvoegsel** en klik op **exporteren** toostart Hallo exportproces. Hallo blob-voorvoegsel is gebruikte tooprefix Hallo namen van bestanden die door deze bewerking uitvoer gegenereerd.

    ![Exporteren][cache-export-data]

    U kunt voortgang Hallo van de exportbewerking Hallo door volgende Hallo meldingen van hello Azure-portal of door het Hallo-gebeurtenissen weergeven in Hallo [controlelogboek](../azure-resource-manager/resource-group-audit.md).

    ![Gegevens exporteren voltooien][cache-export-data-export-complete]

    Caches blijven beschikbaar voor gebruik tijdens het exportproces Hallo.

## <a name="importexport-faq"></a>Veelgestelde vragen over het importeren/exporteren
Deze sectie bevat veelgestelde vragen over Hallo Import/Export-functie.

* [Welke prijzen lagen kunt importeren/exporteren?](#what-pricing-tiers-can-use-importexport)
* [Kan ik gegevens importeren vanaf een willekeurige Redis-server?](#can-i-import-data-from-any-redis-server)
* [Welke versies RDB kan ik importeren?](#what-rdb-versions-can-i-import)
* [Mijn cache is beschikbaar tijdens een bewerking voor importeren/exporteren?](#is-my-cache-available-during-an-importexport-operation)
* [Kan ik voor importeren/exporteren met Redis-cluster gebruiken?](#can-i-use-importexport-with-redis-cluster)
* [Hoe werkt voor importeren/exporteren met een aangepaste databases instellen?](#how-does-importexport-work-with-a-custom-databases-setting)
* [Hoe verschilt voor importeren/exporteren van Redis-persistentie?](#how-is-importexport-different-from-redis-persistence)
* [Kan ik automatiseren met behulp van PowerShell, CLI of andere clients management voor importeren/exporteren?](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [Ik heb ontvangen een time-outfout tijdens de Import/Export-bewerking. Wat betekent dit?](#i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean)
* [Ik krijg een fout opgetreden bij het exporteren van mijn gegevens tooAzure Blob Storage. Wat is er gebeurd?](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a>Welke prijzen lagen kunt importeren/exporteren?
Import/Export is alleen beschikbaar in Hallo premium-prijscategorie.

### <a name="can-i-import-data-from-any-redis-server"></a>Kan ik gegevens importeren vanaf een willekeurige Redis-server?
Ja, Daarnaast tooimporting gegevens van exemplaren van Azure Redis-Cache hebt geëxporteerd, kunt u importeren RDB bestanden vanaf een willekeurige Redis-server in een cloud of de omgeving, zoals Linux, Windows of cloudproviders zoals Amazon Web Services wordt uitgevoerd. toodo dit uploaden Hallo RDB bestand van Hallo gewenst Redis-server naar een pagina of het blok-blob in een Azure Storage-Account en vervolgens importeren deze naar uw premium Azure Redis-Cache-exemplaar. U kunt bijvoorbeeld wilt tooexport Hallo gegevens uit uw productie-cache en importeren in een cache die wordt gebruikt als onderdeel van een testomgeving voor testdoeleinden of migratie.

> [!IMPORTANT]
> toosuccessfully gegevens geëxporteerd van Redis-servers dan de Azure Redis-Cache wanneer met behulp van een pagina-blob, Hallo blob paginaformaat moet worden afgestemd op de grens van een sectorgrootte van 512 bytes importeren. Voor een voorbeeld code tooperform vereist een byte opvulling, Zie [voorbeeld pagina blog uploaden](https://github.com/JimRoberts-MS/SamplePageBlobUpload).
> 
> 

### <a name="what-rdb-versions-can-i-import"></a>Welke versies RDB kan ik importeren?

Azure Redis-Cache ondersteunt RDB importeren tot via RDB versie 7.

### <a name="is-my-cache-available-during-an-importexport-operation"></a>Mijn cache is beschikbaar tijdens een bewerking voor importeren/exporteren?
* **Exporteren** - Caches beschikbaar blijven en u kunt toouse uw cache blijven tijdens een exportbewerking.
* **Importeren** - Caches niet beschikbaar wanneer een importbewerking wordt gestart en worden beschikbaar voor gebruik wanneer Hallo importbewerking is voltooid.

### <a name="can-i-use-importexport-with-redis-cluster"></a>Kan ik voor importeren/exporteren met Redis-cluster gebruiken?
Ja, en u kunt importeren/exporteren tussen een geclusterde cache en een niet-geclusterde cache. Sinds de Redis-cluster [alleen ondersteunt database 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), alle gegevens in databases dan 0 is niet geïmporteerd. Wanneer geclusterde cache-gegevens worden geïmporteerd, wordt Hallo sleutels herverdeeld over Hallo shards van Hallo-cluster.

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a>Hoe werkt voor importeren/exporteren met een aangepaste databases instellen?
Sommige Prijscategorieën hebben verschillende [databases limieten](cache-configure.md#databases), dus er enkele overwegingen zijn bij het importeren als u een aangepaste waarde voor Hallo geconfigureerd `databases` instellen tijdens het maken van de cache.

* Bij het importeren van tooa prijscategorie met een lagere `databases` limiet dan Hallo laag die u hebt geëxporteerd:
  * Als u van Hallo standaardaantal gebruikmaakt `databases`, namelijk 16 voor alle Prijscategorieën, gegevens niet verloren.
  * Als u een aangepaste aantal `databases` dat servicetier valt binnen de grenzen Hallo voor Hallo toowhich die u wilt importeren, gegevens niet verloren.
  * Als de geëxporteerde gegevens gegevens in een database die overschrijdt de grenzen van de nieuwe laag Hallo hello bevat, Hallo gegevens uit deze hogere databases niet geïmporteerd.

### <a name="how-is-importexport-different-from-redis-persistence"></a>Hoe verschilt voor importeren/exporteren van Redis-persistentie?
Azure Redis-Cache-persistentie kunt u toopersist opgeslagen gegevens in Redis tooAzure opslag. Wanneer de persistentie is geconfigureerd, persistente Azure Redis-Cache een momentopname van Hallo Redis-cache in een Redis-binaire indeling toodisk op basis van een back-upfrequentie die kunnen worden geconfigureerd. Als er een onherstelbare gebeurtenis optreedt die zowel Hallo primaire en replica cache uitgeschakeld, wordt automatisch met de meest recente momentopname Hallo Hallo cachegegevens teruggezet. Zie voor meer informatie [hoe tooconfigure gegevenspersistentie voor een Premium Azure Redis-Cache](cache-how-to-premium-persistence.md).

Import / Export kunt u gegevens toobring in of exporteren uit Azure Redis-Cache. Deze niet configureren, back-up en herstellen met behulp van Redis-persistentie.

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a>Kan ik automatiseren met behulp van PowerShell, CLI of andere clients management voor importeren/exporteren?
Ja, voor PowerShell instructies raadpleegt u [tooimport een Redis-cache](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) en [tooexport een Redis-cache](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a>Ik heb ontvangen een time-outfout tijdens de Import/Export-bewerking. Wat betekent dit?
Als u op Hallo blijven **gegevens importeren** of **gegevens exporteren** blade langer dan 15 minuten voordat u begint Hallo bewerking er een foutbericht met een fout bericht vergelijkbaar toohello voorbeeld te volgen:

    hello request tooimport data into cache 'contoso55' failed with status 'error' and error 'One of hello SAS URIs provided could not be used for hello following reason: hello SAS token end time (se) must be at least 1 hour from now and hello start time (st), if given, must be at least 15 minutes in hello past.

tooresolve dit initiëren Hallo import- of exportbewerking voordat 15 minuten is verstreken.

### <a name="i-got-an-error-when-exporting-my-data-tooazure-blob-storage-what-happened"></a>Ik krijg een fout opgetreden bij het exporteren van mijn gegevens tooAzure Blob Storage. Wat is er gebeurd?
Export werkt alleen met RDB-bestanden die zijn opgeslagen als pagina-blobs. Andere typen blob worden momenteel niet ondersteund, met inbegrip van blob storage-accounts met hot en cool lagen. Zie voor meer informatie [Blob storage-accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).

## <a name="next-steps"></a>Volgende stappen
Meer informatie over hoe meer premium toouse functies in de cache.

* [Inleiding toohello Azure Redis-Cache Premium-laag](cache-premium-tier-intro.md)    

<!-- IMAGES -->
[cache-settings-import-export-menu]: ./media/cache-how-to-import-export-data/cache-settings-import-export-menu.png
[cache-export-data-choose-account]: ./media/cache-how-to-import-export-data/cache-export-data-choose-account.png
[cache-export-data-choose-storage-container]: ./media/cache-how-to-import-export-data/cache-export-data-choose-storage-container.png
[cache-export-data-container]: ./media/cache-how-to-import-export-data/cache-export-data-container.png
[cache-export-data-export-complete]: ./media/cache-how-to-import-export-data/cache-export-data-export-complete.png
[cache-export-data]: ./media/cache-how-to-import-export-data/cache-export-data.png
[cache-import-data]: ./media/cache-how-to-import-export-data/cache-import-data.png
[cache-import-choose-storage-account]: ./media/cache-how-to-import-export-data/cache-import-choose-storage-account.png
[cache-import-choose-container]: ./media/cache-how-to-import-export-data/cache-import-choose-container.png
[cache-import-choose-blobs]: ./media/cache-how-to-import-export-data/cache-import-choose-blobs.png
[cache-import-blobs]: ./media/cache-how-to-import-export-data/cache-import-blobs.png
[cache-import-data-import-complete]: ./media/cache-how-to-import-export-data/cache-import-data-import-complete.png
