---
title: aaaManage eindpunten in Azure Traffic Manager | Microsoft Docs
description: Dit artikel helpt u bij het toevoegen, verwijderen, inschakelen en uitschakelen van eindpunten vanuit Azure Traffic Manager.
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: ade2bbc2-35a7-43c5-8001-4698f7254526
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kumud
ms.openlocfilehash: fc65874ae2eaeb6fca5d8c4f33403c258307bdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-disable-enable-or-delete-endpoints"></a>Eindpunten toevoegen, uitschakelen, inschakelen of verwijderen

functie van de Hallo Web Apps in Azure App Service biedt al failover- en round-robinverkeersroutering voor websites binnen een datacenter, ongeacht de websitemodus Hallo. Azure Traffic Manager kunt u toospecify failover- en round-robinverkeersroutering voor websites en cloud-services in verschillende datacenters. Hallo eerste stap nodig tooprovide dat functionaliteit tooadd Hallo cloud of website-eindpunt tooTraffic Manager is.

U kunt ook afzonderlijke eindpunten uitschakelen die deel uitmaken van een Traffic Manager-profiel. Uitschakelen van een eindpunt blijft deze als onderdeel van het Hallo-profiel, maar Hallo profiel gedraagt zich alsof het Hallo-eindpunt is niet opgenomen in deze. Deze actie is handig als u een eindpunt dat in de onderhoudsmodus staat of opnieuw wordt geïmplementeerd, tijdelijk wilt verwijderen. Zodra het Hallo-eindpunt opnieuw actief is, kan worden ingeschakeld.

> [!NOTE]
> Uitschakelen van een eindpunt heeft niets toodo met de implementatiestatus in Azure. Een gezonde eindpunt blijft up-to-date en kunnen verkeer tooreceive zelfs wanneer uitgeschakeld in Traffic Manager. Bovendien heeft het uitschakelen van een eindpunt in een bepaald profiel geen invloed op de status ervan in een ander profiel.

## <a name="tooadd-a-cloud-service-or-an-app-service-endpoint-tooa-traffic-manager-profile"></a>tooadd een cloudservice of een App service-eindpunt tooa Traffic Manager-profiel

1. Aanmelden via een browser toohello [Azure-portal](http://portal.azure.com).
2. Zoek in de zoekbalk Hallo-portal, op Hallo **Traffic Manager-profiel** naam toomodify wilt en klik vervolgens op Hallo Traffic Manager-profiel in Hallo resulteert dat Hallo weergegeven.
3. In Hallo **Traffic Manager-profiel** blade in Hallo **instellingen** sectie, klikt u op **eindpunten**.
4. In Hallo **eindpunten** blade die wordt weergegeven, klikt u op **toevoegen**.
5. In Hallo **eindpunt toevoegen** blade voltooid zijn als volgt:
    1. Klik bij **Type** op **Azure-eindpunt**.
    2. Geef een **naam** waarop u wilt toorecognize dit eindpunt.
    3. Voor **resource doeltype**, van vervolgkeuzelijst hello, kies de juiste resourcetype Hallo.
    4. Voor **Doelresource**, van vervolgkeuzelijst hello, kies de juiste doelbron hello tooshow Hallo aanbieding resources onder hetzelfde abonnement in Hallo Hallo **Resources blade**. In Hallo **Resource** blade die wordt weergegeven dat het gewenste tooadd als eerste eindpunt Hallo pick Hallo service.
    5. Selecteer bij **Prioriteit** de optie **1**. Dit resulteert in alle verkeer dat hierheen gaat toothis eindpunt als deze is in orde.
    6. Laat **Toevoegen als uitgeschakeld** uit staan.
    7. Klik op **OK**
6.  Herhaal stap 4 en 5 tooadd Hallo volgende Azure-eindpunt. Zorg ervoor dat tooadd deze met de **prioriteit** waarde ingesteld op **2**.
7.  Wanneer Hallo toevoeging van beide eindpunten voltooid is, worden deze weergegeven in Hallo **Traffic Manager-profiel** blade samen met hun status controleren als **Online**.

> [!NOTE]
> Nadat u toevoegen of verwijderen van een eindpunt van een profiel met Hallo *Failover* methode voor het doorsturen van verkeer, mogelijk niet Hallo failover-prioriteitenlijst worden gerangschikt ze zoals u dat wilt. Hallo-volgorde van Hallo Failover-prioriteitenlijst op de configuratiepagina hello, kunt u aanpassen. Zie voor meer informatie [Configure Failover traffic routing](traffic-manager-configure-failover-routing-method.md) (Failover-verkeersroutering configureren).

## <a name="toodisable-an-endpoint"></a>een eindpunt toodisable

1. Aanmelden via een browser toohello [Azure-portal](http://portal.azure.com).
2. Zoek in de zoekbalk Hallo-portal, op Hallo **Traffic Manager-profiel** naam toomodify wilt en klik vervolgens op Hallo Traffic Manager-profiel in Hallo resultaten die worden weergegeven.
3. In Hallo **Traffic Manager-profiel** blade in Hallo **instellingen** sectie, klikt u op **eindpunten**. 
4. Klik op Hallo-eindpunt dat u wilt dat toodisable, en klik vervolgens op Hallo **eindpunt** blade die wordt weergegeven, klikt u op **bewerken**.
5. In Hallo **eindpunt** blade Hallo Eindpuntstatus te wijzigen**uitgeschakelde**, en klik vervolgens op **opslaan**.
6. Clients blijven toosend verkeer toohello eindpunt voor Hallo duur van het Time-to-Live (TTL). U kunt Hallo TTL op de configuratiepagina Hallo Hallo Traffic Manager-profiel wijzigen.

## <a name="tooenable-an-endpoint"></a>een eindpunt tooenable

1. Aanmelden via een browser toohello [Azure-portal](http://portal.azure.com).
2. Zoek in de zoekbalk Hallo-portal, op Hallo **Traffic Manager-profiel** naam toomodify wilt en klik vervolgens op Hallo Traffic Manager-profiel in Hallo resultaten die worden weergegeven.
3. In Hallo **Traffic Manager-profiel** blade in Hallo **instellingen** sectie, klikt u op **eindpunten**. 
4. Klik op Hallo-eindpunt dat u wilt dat toodisable, en klik vervolgens op Hallo **eindpunt** blade die wordt weergegeven, klikt u op **bewerken**.
5. In Hallo **eindpunt** blade Hallo Eindpuntstatus te wijzigen**ingeschakeld**, en klik vervolgens op **opslaan**.
6. Clients blijven toosend verkeer toohello eindpunt voor Hallo duur van het Time-to-Live (TTL). U kunt Hallo TTL op de configuratiepagina Hallo Hallo Traffic Manager-profiel wijzigen.

## <a name="toodelete-an-endpoint"></a>een eindpunt toodelete

1. Aanmelden via een browser toohello [Azure-portal](http://portal.azure.com).
2. Zoek in de zoekbalk Hallo-portal, op Hallo **Traffic Manager-profiel** naam toomodify wilt en klik vervolgens op Hallo Traffic Manager-profiel in Hallo resultaten die worden weergegeven.
3. In Hallo **Traffic Manager-profiel** blade in Hallo **instellingen** sectie, klikt u op **eindpunten**. 
4. Klik op Hallo-eindpunt dat u wilt dat toodisable, en klik vervolgens op Hallo **eindpunt** blade die wordt weergegeven, klikt u op **bewerken**.
5. In Hallo **eindpunt** blade Hallo Eindpuntstatus te wijzigen**ingeschakeld**, en klik vervolgens op **opslaan**.


## <a name="next-steps"></a>Volgende stappen

* [Traffic Manager-profielen beheren](traffic-manager-manage-profiles.md)
* [Routeringsmethoden configureren](traffic-manager-configure-routing-method.md)
* [Problemen met Traffic Manager in gedegradeerde status oplossen](traffic-manager-troubleshooting-degraded.md)
* [Prestatieoverwegingen voor Traffic Manager](traffic-manager-performance-considerations.md)
* [Bewerkingen op Traffic Manager (REST API-referentiemateriaal)](http://go.microsoft.com/fwlink/p/?LinkID=313584)

