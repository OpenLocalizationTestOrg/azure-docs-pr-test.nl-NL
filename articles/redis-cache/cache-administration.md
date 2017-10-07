---
title: aaaHow tooadminister Azure Redis-Cache | Microsoft Docs
description: Informatie over hoe tooperform beheertaken, zoals opnieuw opstarten en schema-updates voor de Azure Redis-Cache
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 8c915ae6-5322-4046-9938-8f7832403000
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: eb24668a3f6264444e7d4daf1ac43b41b12dfe66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadminister-azure-redis-cache"></a>Hoe tooadminister Azure Redis-Cache
Dit onderwerp wordt beschreven hoe tooperform beheer taken zoals [opnieuw wordt opgestart nadat](#reboot) en [updates plannen](#schedule-updates) voor uw Azure Redis-Cache-exemplaren.

## <a name="reboot"></a>Opnieuw opstarten
Hallo **opnieuw opstarten** blade kunt u tooreboot een of meer knooppunten van de cache. Deze mogelijkheid opnieuw opstarten kan tootest u uw toepassing voor tolerantie als er een storing van een cacheknooppunt.

![Opnieuw opstarten](./media/cache-administration/redis-cache-administration-reboot.png)

Selecteer Hallo knooppunten tooreboot en klik op **opnieuw opstarten**.

![Opnieuw opstarten](./media/cache-administration/redis-cache-reboot.png)

Als u een premium-cache hebt met clusteren is ingeschakeld, kunt u selecteren welke shards van Hallo cache tooreboot.

![Opnieuw opstarten](./media/cache-administration/redis-cache-reboot-cluster.png)

tooreboot een of meer knooppunten van de cache Hallo gewenst knooppunten te selecteren en klik op **opnieuw opstarten**. Als u een premium-cache hebt met clustering is ingeschakeld, Hallo gewenst shards tooreboot selecteren en klik vervolgens op **opnieuw opstarten**. Hallo geselecteerde knooppunten opnieuw opstarten na een paar minuten en weer online zijn een paar minuten later.

Hallo gevolgen voor de clienttoepassingen varieert, afhankelijk van welke knooppunten opnieuw te starten.

* **Master** : wanneer Hallo hoofdknooppunt opnieuw opgestart, Azure Redis-Cache mislukt over toohello replica knooppunt is en bijdraagt aan het toomaster. Tijdens deze failover mogelijk zijn er een korte periode waarin verbindingen toohello cache kunnen mislukken.
* **Slave** : wanneer Hallo slave knooppunt opnieuw wordt opgestart, is doorgaans geen invloed toocache-clients.
* **Hoofd- en slave** : wanneer beide knooppunten van de cache worden opgestart, alle gegevens gaan verloren in Hallo cache en verbindingen toohello cache mislukken totdat het primaire knooppunt Hallo weer online wordt gezet. Als u hebt geconfigureerd [gegevenspersistentie](cache-how-to-premium-persistence.md), Hallo meest recente back-up is hersteld wanneer Hallo cache weer online wordt gezet, maar er cache-schrijfbewerkingen die is opgetreden na Hallo meest recente back-up gaan verloren.
* **Knooppunten van een premium in de cache met clustering ingeschakeld** : wanneer u opnieuw opstarten of meer knooppunten van een premium-cache met clustering is ingeschakeld, gedrag voor Hallo geselecteerd Hallo knooppunten is hetzelfde als wanneer u opnieuw opstarten Hallo bijbehorende knooppunt of knooppunten van een niet-geclusterde Hallo cache.

> [!IMPORTANT]
> Opnieuw opstarten is nu beschikbaar voor alle Prijscategorieën.
> 
> 

## <a name="reboot-faq"></a>Veelgestelde vragen over het opnieuw opstarten
* [Welk knooppunt moet ik opnieuw opstarten tootest mijn toepassing?](#which-node-should-i-reboot-to-test-my-application)
* [Kan ik Hallo cache tooclear clientverbindingen opnieuw opstarten?](#can-i-reboot-the-cache-to-clear-client-connections)
* [Ik verliest gegevens uit de cache als een herstart moet ik doen?](#will-i-lose-data-from-my-cache-if-i-do-a-reboot)
* [Kan ik mijn-cache met behulp van PowerShell, CLI of andere beheerhulpprogramma's opnieuw opstarten?](#can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools)
* [Welke prijzen lagen kunt Hallo-functionaliteit voor opnieuw opstarten?](#what-pricing-tiers-can-use-the-reboot-functionality)

### <a name="which-node-should-i-reboot-tootest-my-application"></a>Welk knooppunt moet ik opnieuw opstarten tootest mijn toepassing?
tootest hello tolerantie van uw toepassing tegen fouten van het primaire knooppunt van de cache, opnieuw opstarten Hallo Hallo **Master** knooppunt. tootest hello tolerantie van uw toepassing tegen fouten van Hallo secundair knooppunt opnieuw opstarten Hallo **Slave** knooppunt. tootest hello tolerantie van uw toepassing tegen beschadiging van Hallo cache opnieuw opstarten **beide** knooppunten.

### <a name="can-i-reboot-hello-cache-tooclear-client-connections"></a>Kan ik Hallo cache tooclear clientverbindingen opnieuw opstarten?
Ja, als u opnieuw opstarten Hallo cache die alle clientverbindingen zijn uitgeschakeld. Opnieuw opstarten is handig in geval van Hallo waar alle clientverbindingen vanwege tooa logische fout of een fout in de clienttoepassing hello worden gebruikt. Elke prijscategorie heeft verschillende [client verbindingslimieten](cache-configure.md#default-redis-server-configuration) Hallo voor verschillende grootten en zodra deze limieten zijn bereikt, niet meer clientverbindingen worden geaccepteerd. Opnieuw opstarten Hallo cache biedt een manier tooclear alle clientverbindingen.

> [!IMPORTANT]
> Als u uw cache tooclear client-verbindingen opnieuw opstart, wordt StackExchange.Redis automatisch hersteld zodra de Hallo Redis knooppunt weer online is. Als het onderliggende probleem Hallo niet is opgelost, blijft Hallo clientverbindingen toobe gebruikt.
> 
> 

### <a name="will-i-lose-data-from-my-cache-if-i-do-a-reboot"></a>Ik verliest gegevens uit de cache als een herstart moet ik doen?
Als u beide Hallo opnieuw opstarten **Master** en **Slave** knooppunten, de gegevens in cache hello (of in die shard als u een premium-cache met clusteren is ingeschakeld) worden verwijderd. Als u hebt geconfigureerd [gegevenspersistentie](cache-how-to-premium-persistence.md), Hallo meest recente back-up wordt teruggezet wanneer Hallo cache weer online wordt gezet, maar er cache-schrijfbewerkingen die hebben plaatsgevonden na Hallo back-up is gemaakt, gaan verloren.

Als u slechts een van de knooppunten Hallo opnieuw opstarten, gegevens zijn niet doorgaans verloren, maar nog steeds mogelijk. Bijvoorbeeld als hoofdknooppunt Hallo opnieuw wordt opgestart en een schrijfbewerking cache is gemaakt, Hallo gegevens van Hallo cache schrijven is verloren gegaan. Een ander scenario voor gegevensverlies zou zijn als u één knooppunt opnieuw opstarten en andere Hallo knooppunt toogo gebeurt af vanwege fout tooa op Hallo hetzelfde moment. Zie voor meer informatie over mogelijke oorzaken van gegevensverlies [wat is er gebeurd toomy gegevens in Redis?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)

### <a name="can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools"></a>Kan ik mijn-cache met behulp van PowerShell, CLI of andere beheerhulpprogramma's opnieuw opstarten?
Ja, voor PowerShell instructies raadpleegt u [tooreboot een Redis-cache](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache).

### <a name="what-pricing-tiers-can-use-hello-reboot-functionality"></a>Welke prijzen lagen kunt Hallo-functionaliteit voor opnieuw opstarten?
Opnieuw opstarten is beschikbaar voor alle Prijscategorieën.

## <a name="schedule-updates"></a>Updates plannen
Hallo **updates plannen** blade kunt u een onderhoudsvenster voor uw cache van de laag Premium toodesignate. Wanneer het onderhoudsvenster hello wordt opgegeven, wordt een Redis-server bijgewerkt tijdens dit venster. 

> [!NOTE] 
> Hallo-onderhoudsvenster van toepassing is alleen tooRedis serverupdates en niet tooany Azure-updates of updates toohello besturingssysteem Hallo VM's die als host Hallo-cache fungeren.
> 
> 

![Updates plannen](./media/cache-administration/redis-schedule-updates.png)

een onderhoudsvenster toospecify controleren Hallo gewenst dagen Hallo onderhoud-venster Beginuur voor elke dag opgeven, en klik **OK**. Houd er rekening mee dat de duur van het onderhoudsvenster Hallo ingesteld op UTC is. 

> [!NOTE]
> Hallo standaardonderhoudsvenster voor updates is vijf uur. Deze waarde kan niet worden geconfigureerd uit hello Azure-portal, maar u kunt deze configureren in PowerShell met Hallo `MaintenanceWindow` parameter Hallo [nieuw AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry) cmdlet. Zie voor meer informatie [kan ik geplande updates met behulp van PowerShell, CLI of andere beheerhulpprogramma's beheren?](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)
> 
> 

## <a name="schedule-updates-faq"></a>Veelgestelde vragen over updates plannen
* [Wanneer updates worden uitgevoerd als ik functie Hallo schema-updates niet gebruiken?](#when-do-updates-occur-if-i-dont-use-the-schedule-updates-feature)
* [Welk type updates worden uitgevoerd tijdens het Hallo onderhoudsvenster gepland?](#what-type-of-updates-are-made-during-the-scheduled-maintenance-window)
* [Kan ik geplande updates met behulp van PowerShell, CLI of andere beheerhulpprogramma's beheren?](#can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools)
* [Welke prijzen lagen kan Hallo schema-updates functionaliteit gebruiken?](#what-pricing-tiers-can-use-the-schedule-updates-functionality)

### <a name="when-do-updates-occur-if-i-dont-use-hello-schedule-updates-feature"></a>Wanneer updates worden uitgevoerd als ik functie Hallo schema-updates niet gebruiken?
Als u een onderhoudsvenster niet opgeeft, kunnen updates op elk gewenst moment worden gemaakt.

### <a name="what-type-of-updates-are-made-during-hello-scheduled-maintenance-window"></a>Welk type updates worden uitgevoerd tijdens het Hallo onderhoudsvenster gepland?
Alleen Redis-server updates worden uitgevoerd tijdens het Hallo geplande onderhoudsvenster. Hallo onderhoudsvenster is niet van toepassing op tooAzure updates of updates toohello VM-besturingssysteem.

### <a name="can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools"></a>Kan ik beheerde geplande updates met behulp van PowerShell, CLI of andere beheerhulpprogramma's?
Ja, kunt u uw geplande updates met behulp van PowerShell-cmdlets volgen Hallo beheren:

* [Get-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/get-azurermrediscachepatchschedule)
* [Nieuwe AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/new-azurermrediscachepatchschedule)
* [Nieuwe AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry)
* [Verwijder AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/remove-azurermrediscachepatchschedule)

### <a name="what-pricing-tiers-can-use-hello-schedule-updates-functionality"></a>Welke prijzen lagen kan Hallo schema-updates functionaliteit gebruiken?
Hallo **updates plannen** functie is alleen beschikbaar in Hallo premium-prijscategorie.

## <a name="next-steps"></a>Volgende stappen
* Ontdek meer [premium-laag van Azure Redis-Cache](cache-premium-tier-intro.md) functies.

