---
title: aaaHow tooconfigure Geo-replicatie voor Azure Redis-Cache | Microsoft Docs
description: Meer informatie over hoe tooreplicate uw Azure Redis-Cache-exemplaren in geografische regio's.
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 375643dc-dbac-4bab-8004-d9ae9570440d
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: sdanie
ms.openlocfilehash: edcd6f202b51055d1a4e47ecaf11f9977d50aa81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-geo-replication-for-azure-redis-cache"></a>Hoe tooconfigure Geo-replicatie voor Azure Redis-Cache

Geo-replicatie biedt een mechanisme voor het koppelen van twee exemplaren van Premium-laag Azure Redis-Cache. Een cache is aangewezen als Hallo primaire gekoppelde cache en andere als secundaire gekoppelde cache Hallo Hallo. Hallo secundaire gekoppelde cache wordt alleen-lezen en gegevens die zijn geschreven toohello primaire-cache is gerepliceerd toohello secundaire gekoppelde cache. Deze functionaliteit kan gebruikte tooreplicate een cache in Azure-regio's zijn. Dit artikel bevat een handleiding tooconfiguring Geo-replicatie voor de Premium-laag Azure Redis-Cache-exemplaren.

## <a name="geo-replication-prerequisites"></a>Geo-replicatie-vereisten

tooconfigure Geo-replicatie tussen de twee caches, Hallo volgende vereisten moet worden voldaan:

- Beide caches moet [Premium-laag](cache-premium-tier-intro.md) in de cache opslaat.
- Beide caches moet Hallo hetzelfde Azure-abonnement.
- Hallo secundaire gekoppelde cache moet worden ofwel Hallo dezelfde laag en een grotere prijscategorie dan Hallo primaire gekoppelde cache prijzen.
- Als de primaire gekoppelde cachegeheugen Hallo clusteren is ingeschakeld, secundaire gekoppelde cache Hallo moet hebben clustering ingeschakeld met Hallo hetzelfde aantal shards als Hallo primaire gekoppelde cache.
- Beide caches moeten worden gemaakt en actief is.
- Persistentie moet niet worden ingeschakeld in de cache.
- Geo-replicatie tussen caches in Hallo die hetzelfde VNET wordt ondersteund. Geo-replicatie tussen caches in verschillende VNETs wordt ook ondersteund, zolang Hallo twee VNETs zijn geconfigureerd in zodanig dat resources in Hallo VNETs kunnen tooreach zijn elkaar via TCP-verbindingen.

Nadat Geo-replicatie is geconfigureerd, hello volgende gelden beperkingen tooyour gekoppelde cache paar:

- Hallo secundaire gekoppelde cache is alleen-lezen. kan in lezen, maar u tooit gegevens kan niet schrijven. 
- Alle gegevens die in Hallo secundaire gekoppelde cache was voordat het Hallo-koppeling is toegevoegd, wordt verwijderd. Als hello Geo-replicatie wordt vervolgens verwijderd echter, gerepliceerd Hallo gegevens blijven in Hallo secundaire gekoppelde cache.
- U kan niet starten een [bewerking schalen](cache-how-to-scale.md) in de cache of [Hallo aantal shards wijzigen](cache-how-to-premium-clustering.md) als Hallo cachegeheugen clusteren is ingeschakeld.
- U kunt de persistentie van de cache niet inschakelen.
- Kunt u [exporteren](cache-how-to-import-export-data.md#export) met de cache, maar u kunt alleen [importeren](cache-how-to-import-export-data.md#import) in primaire Hallo gekoppeld cache.
- U kunt gekoppelde cache of resourcegroep Hallo waarin ze, totdat u Hallo Geo-replicatie-koppeling niet verwijderen. Zie voor meer informatie [waarom is Hallo-bewerking mislukt wanneer ik mijn gekoppelde cache toodelete geprobeerd?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- Als er twee caches Hallo zich in verschillende regio's, toepassing kosten voor uitgaand netwerkverkeer toohello gegevens gerepliceerd tussen regio's toohello secundaire gekoppelde cache. Zie voor meer informatie [hoeveel biedt deze kosten tooreplicate mijn gegevens over Azure-regio's?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- Er is geen automatische failover toohello secundaire gekoppelde cache als primaire Hallo-cache (en de replica) uitvallen. In de volgorde toofailover clienttoepassingen, moet u koppeling toomanually verwijderen Hallo-Geo-replicatie en punt Hallo client toepassingen toohello cache die voorheen was Hallo secundaire gekoppelde cache. Zie voor meer informatie [hoe werkt mislukt via toohello secundaire gekoppelde cache?](#how-does-failing-over-to-the-secondary-linked-cache-work)

## <a name="add-a-geo-replication-link"></a>Een Geo-replicatie-koppeling toevoegen

1. toolink twee premium in de cache opgeslagen samen voor geo-replicatie, klikt u op **Geo-replicatie** Hallo Resource menu Hallo-cache is bedoeld als primaire Hallo dat is gekoppeld in de cache, en klik vervolgens op **toevoegen cache replicatiekoppeling**van Hallo **Geo-replicatie** blade.

    ![Koppeling toevoegen](./media/cache-how-to-geo-replication/cache-geo-location-menu.png)

2. Klik op Hallo-naam van de secundaire cache Hallo Hallo gewenst **compatibel caches** lijst. Als de gewenste cache wordt niet in de lijst hello weergegeven, controleert u of die Hallo [Geo-replicatie vereisten](#geo-replication-prerequisites) voor Hallo gewenst secundaire cache wordt voldaan. toofilter hello caches per regio, klikt u op de gewenste regio in Hallo kaart toodisplay alleen die in de cache opslaat in Hallo Hallo **compatibel caches** lijst.

    ![Geo-replicatie compatibel caches](./media/cache-how-to-geo-replication/cache-geo-location-select-link.png)
    
    U kunt ook koppelen of de weergave details over secundaire Hallo-cache met behulp van het contextmenu Hallo Hallo initiëren.

    ![Contextmenu geo-replicatie](./media/cache-how-to-geo-replication/cache-geo-location-select-link-context-menu.png)

3. Klik op **koppeling** toolink Hallo twee caches samen en begin met het Hallo-replicatieproces.

    ![Koppeling caches](./media/cache-how-to-geo-replication/cache-geo-location-confirm-link.png)

4. U kunt de voortgang Hallo van Hallo replicatieproces bekijken op Hallo **Geo-replicatie** blade.

    ![Status koppelen](./media/cache-how-to-geo-replication/cache-geo-location-linking.png)

    U kunt ook de status op Hallo koppelen Hallo weergeven **overzicht** blade voor beide Hallo primaire en secundaire caches.

    ![Status van de cache](./media/cache-how-to-geo-replication/cache-geo-location-link-status.png)

    Zodra het replicatieproces Hallo voltooid is, Hallo **status koppelen** wijzigingen te**geslaagd**.

    ![Status van de cache](./media/cache-how-to-geo-replication/cache-geo-location-link-successful.png)

    Hallo primaire gekoppelde cache blijft beschikbaar voor gebruik tijdens Hallo koppelingsproces, maar Hallo secundaire gekoppelde cache is niet beschikbaar totdat Hallo koppelingsproces is voltooid.

## <a name="remove-a-geo-replication-link"></a>Een koppeling Geo-replicatie verwijderen

1. tooremove hello koppeling tussen twee caches en stop Geo-replicatie, klikt u op **ontkoppelen caches** van Hallo **Geo-replicatie** blade.
    
    ![Ontkoppelen van caches](./media/cache-how-to-geo-replication/cache-geo-location-unlink.png)

    Wanneer Hallo ontkoppelen proces is voltooid, wordt Hallo secundaire cache is beschikbaar voor zowel leest en schrijft.

>[!NOTE]
>Wanneer Hallo Geo-replicatie-koppeling is verwijderd, gerepliceerde Hallo gegevens van secundaire cache Hallo Hallo primaire gekoppelde cache blijft.
>
>

## <a name="geo-replication-faq"></a>Veelgestelde vragen over geo-replicatie

- [Kan ik met een cache van de laag Standard of Basic Geo-replicatie gebruiken?](#can-i-use-geo-replication-with-a-standard-or-basic-tier-cache)
- [Mijn cache beschikbaar is voor gebruik tijdens het Hallo koppelen of ontkoppelen proces?](#is-my-cache-available-for-use-during-the-linking-or-unlinking-process)
- [Kan ik meer dan twee caches aan elkaar koppelen?](#can-i-link-more-than-two-caches-together)
- [Kan ik twee caches van verschillende Azure-abonnementen koppelen](#can-i-link-two-caches-from-different-azure-subscriptions)
- [Kan ik twee caches van verschillende grootten koppelen](#can-i-link-two-caches-with-different-sizes)
- [Kan ik met clustering ingeschakeld Geo-replicatie gebruiken?](#can-i-use-geo-replication-with-clustering-enabled)
- [Kan ik Geo-replicatie met mijn caches in een VNET gebruiken?](#can-i-use-geo-replication-with-my-caches-in-a-vnet)
- [Kan ik PowerShell of Azure CLI toomanage Geo-replicatie gebruiken?](#can-i-use-powershell-or-azure-cli-to-manage-geo-replication)
- [Hoeveel kost het tooreplicate mijn gegevens over Azure-regio's?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- [Waarom is Hallo-bewerking mislukt wanneer ik mijn gekoppelde cache toodelete geprobeerd?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- [Welke regio moet ik voor mijn secundaire gekoppelde cache gebruiken?](#what-region-should-i-use-for-my-secondary-linked-cache)
- [Hoe werkt de storing worden overgenomen toohello secundaire gekoppelde cache?](#how-does-failing-over-to-the-secondary-linked-cache-work)

### <a name="can-i-use-geo-replication-with-a-standard-or-basic-tier-cache"></a>Kan ik met een cache van de laag Standard of Basic Geo-replicatie gebruiken?

Nee, Geo-replicatie is alleen beschikbaar voor Premium-laag caches.

### <a name="is-my-cache-available-for-use-during-hello-linking-or-unlinking-process"></a>Mijn cache beschikbaar is voor gebruik tijdens het Hallo koppelen of ontkoppelen proces?

- Wanneer twee caches aan elkaar koppelen voor Geo-replicatie, Hallo primaire gekoppelde cache blijft beschikbaar voor gebruik maar Hallo secundaire gekoppelde cache is niet beschikbaar totdat Hallo koppelingsproces is voltooid.
- Wanneer u de koppeling Hallo Geo-replicatie tussen twee caches verwijdert, blijven beide caches beschikbaar voor gebruik.

### <a name="can-i-link-more-than-two-caches-together"></a>Kan ik meer dan twee caches aan elkaar koppelen?

Nee, bij gebruik van Geo-replicatie kunt u alleen koppelen twee caches samen.

### <a name="can-i-link-two-caches-from-different-azure-subscriptions"></a>Kan ik twee caches van verschillende Azure-abonnementen koppelen

Nee, beide caches moet Hallo hetzelfde Azure-abonnement.

### <a name="can-i-link-two-caches-with-different-sizes"></a>Kan ik twee caches van verschillende grootten koppelen

Ja, zolang Hallo secundaire gekoppelde cache groter dan Hallo primaire gekoppelde cache is.

### <a name="can-i-use-geo-replication-with-clustering-enabled"></a>Kan ik met clustering ingeschakeld Geo-replicatie gebruiken?

Ja, mits beide caches Hallo hebben hetzelfde aantal shards.

### <a name="can-i-use-geo-replication-with-my-caches-in-a-vnet"></a>Kan ik Geo-replicatie met mijn caches in een VNET gebruiken?

Ja, Geo-replicatie caches in vnet's worden ondersteund. 

- Geo-replicatie tussen caches in Hallo die hetzelfde VNET wordt ondersteund.
- Geo-replicatie tussen caches in verschillende VNETs wordt ook ondersteund, zolang Hallo twee VNETs zijn geconfigureerd in zodanig dat resources in Hallo VNETs kunnen tooreach zijn elkaar via TCP-verbindingen.

### <a name="can-i-use-powershell-or-azure-cli-toomanage-geo-replication"></a>Kan ik PowerShell of Azure CLI toomanage Geo-replicatie gebruiken?

Op dit moment kunt u alleen beheren met behulp van Geo-replicatie hello Azure-portal.

### <a name="how-much-does-it-cost-tooreplicate-my-data-across-azure-regions"></a>Hoeveel kost het tooreplicate mijn gegevens over Azure-regio's?

Wanneer u Geo-replicatie gebruikt, is de gegevens uit de primaire gekoppelde cache Hallo gerepliceerde toohello secundaire gekoppeld-cache. Als twee Hallo gekoppeld caches in Hallo zijn dezelfde Azure-regio, er zijn geen kosten voor gegevensoverdracht Hallo. Als hello twee gekoppeld caches zijn in verschillende Azure-regio's, hello Geo-replicatie gegevensoverdracht kosten Hallo bandbreedte kosten voor het repliceren van die gegevens toohello andere Azure-regio. Zie voor meer informatie [bandbreedte prijsinformatie](https://azure.microsoft.com/pricing/details/bandwidth/).

### <a name="why-did-hello-operation-fail-when-i-tried-toodelete-my-linked-cache"></a>Waarom is Hallo-bewerking mislukt wanneer ik mijn gekoppelde cache toodelete geprobeerd?

Wanneer twee caches zijn gekoppeld, kunt u de cache of Hallo resourcegroep waarin ze totdat u Hallo Geo-replicatie-koppeling niet verwijderen. Als u probeert toodelete Hallo resourcegroep die een of beide Hallo bevat gekoppeld caches, hello andere resources in de resourcegroep Hallo worden verwijderd, maar Hallo resourcegroep blijft in Hallo `deleting` status en gekoppelde caches in Hallo resourcegroep Hallo blijven `running` status. toocomplete hello verwijdering van de resourcegroep Hallo en Hallo gekoppeld caches binnen deze koppeling van verbreken Hallo Geo-replicatie, zoals beschreven in [verwijderen van een Geo-replicatiekoppeling](#remove-a-geo-replication-link).

### <a name="what-region-should-i-use-for-my-secondary-linked-cache"></a>Welke regio moet ik voor mijn secundaire gekoppelde cache gebruiken?

In het algemeen wordt aanbevolen voor uw cache tooexist in Hallo dezelfde Azure-regio als Hallo-toepassing die toegang heeft tot het. Als uw toepassing een primaire en terugval regio heeft, moeten uw primaire en secundaire caches bestaan in dezelfde regio's. Zie voor meer informatie over de gekoppelde regio [Best Practices – gekoppelde Azure-regio's](../best-practices-availability-paired-regions.md).

### <a name="how-does-failing-over-toohello-secondary-linked-cache-work"></a>Hoe werkt de storing worden overgenomen toohello secundaire gekoppelde cache?

In de eerste release Hallo van Geo-replicatie ondersteunt Azure Redis-Cache geen automatische failover tussen Azure-regio's. Geo-replicatie wordt voornamelijk gebruikt in een noodherstelscenario. In een herstelscenario distater klanten moeten online zetten van Hallo gehele toepassing stack in een back-regio in gecoördineerde wijze in plaats van afzonderlijke toepassingsonderdelen bepalen wanneer laten tooswitch tootheir back-ups op hun eigen. Dit is vooral van belang tooRedis. Een van de belangrijkste voordelen van Redis Hallo is dat het is een zeer lage latentie-archief. Als Redis gebruikt door een toepassing mislukt via tooa andere Azure-regio maar Hallo compute laag niet het geval, Hallo toegevoegd round trip time kan een merkbare invloed hebben op de prestaties. Om deze reden, willen we graag tooavoid Redis mislukt via automatisch vanwege problemen met de beschikbaarheid tootransient.

Op dit moment tooinitiate Hallo failover, moet u tooremove Hallo Geo-replicatie koppelen in hello Azure-portal en wijzig vervolgens Hallo verbinding eindpunt in Hallo Redis-client van Hallo primaire gekoppelde cache toohello (voorheen gekoppeld) secundaire cache. Wanneer twee caches zijn ontkoppeld, Hallo Hallo replica wordt weergegeven als een gewone lezen-schrijven cache opnieuw en -aanvragen rechtstreeks vanuit de Redis-clients accepteert.


## <a name="next-steps"></a>Volgende stappen

Meer informatie over Hallo [Azure Redis-Cache Premium-laag](cache-premium-tier-intro.md).

