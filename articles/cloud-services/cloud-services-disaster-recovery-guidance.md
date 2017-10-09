---
title: aaaWhat toodo in geval van een onderbreking van de Azure-service die van invloed is op Azure Cloud Services Hallo | Microsoft Docs
description: Meer informatie over welke toodo in Hallo-gebeurtenis van een onderbreking van de Azure-service die van invloed is op Azure Cloud Services.
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: e52634ab-003d-4f1e-85fa-794f6cd12ce4
ms.service: cloud-services
ms.workload: cloud-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: mmccrory
ms.openlocfilehash: bb1f1835fc91a23772f81801b67d5786c190ba19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-of-an-azure-service-disruption-that-impacts-azure-cloud-services"></a>Welke toodo in Hallo-gebeurtenis van een onderbreking van de Azure-service die van invloed is op Azure Cloud Services
Bij Microsoft werken we harde toomake zorgen dat onze services altijd beschikbaar tooyou wanneer u deze nodig. Dwingt buiten ons wil soms invloed hebben op ons op een manier die niet-geplande serviceonderbrekingen veroorzaken.

Microsoft biedt een Service Level Agreement (SLA) voor de services als een toezegging voor bedrijfstijd en connectiviteit. Hallo SLA voor afzonderlijke Azure-services kan worden gevonden op [Azure Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).

Azure heeft al veel ingebouwde platformfuncties die ondersteuning bieden voor maximaal beschikbare toepassingen. Lees voor meer informatie over deze services, [herstel na noodgevallen en hoge beschikbaarheid voor Azure-toepassingen](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

In dit artikel bevat informatie over waar noodherstelscenario wanneer een hele regio optreedt in een storing vervaldatum toomajor natuurramp of wijdverbreid service wordt onderbroken. Dit zeldzame instanties zijn, maar u moet voorbereiden voor Hallo kans dat er een storing van een hele regio is. Als een hele regio optreedt in een service wordt onderbroken, Hallo lokaal redundante exemplaren van uw gegevens tijdelijk niet beschikbaar. Als u geo-replicatie hebt ingeschakeld, worden de drie extra kopieën van uw Azure Storage-blobs en tabellen opgeslagen in een andere regio. In geval van een volledige regionale uitval of een noodsituatie in welke Hallo primaire regio kan niet worden hersteld hello remaps Azure alle Hallo DNS-vermeldingen toohello geogerepliceerde regio.

> [!NOTE]
> Let erop dat u geen controle over dit proces hebt en alleen voor het hele datacenter serviceonderbrekingen kunnen ontstaan geldt. Daarom moet u ook zijn afhankelijk van andere back-strategieën toepassingsspecifieke tooachieve Hallo hoogste niveau van beschikbaarheid. Zie voor meer informatie [herstel na noodgevallen en hoge beschikbaarheid voor Microsoft Azure-toepassingen](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md). Indien kunnen tooaffect toobe gewenst uw eigen failover, kunt u tooconsider Hallo gebruik van [geografisch redundante opslag met leestoegang (RA-GRS)](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage), waarbij automatisch een alleen-lezen kopie van uw gegevens in een andere regio.
>
>


## <a name="option-1-use-a-backup-deployment-through-azure-traffic-manager"></a>Optie 1: Een back-implementatie via Azure Traffic Manager gebruiken
Hallo meest robuuste noodherstel omvat het onderhouden van meerdere implementaties van uw toepassing in verschillende regio's en klik vervolgens met behulp van [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) toodirect verkeer tussen hen. Azure Traffic Manager biedt meerdere [methoden voor het doorsturen](../traffic-manager/traffic-manager-routing-methods.md), zodat u kiezen kunt of toomanage uw implementaties met een primaire/back-model of toosplit verkeer tussen hen.

![Azure Cloud Services te verdelen over regio's met Azure Traffic Manager](./media/cloud-services-disaster-recovery-guidance/using-azure-traffic-manager.png)

Hallo snelste antwoord toohello verlies van een gebied, is het belangrijk dat u de Traffic Manager configureert [eindpuntcontrole](../traffic-manager/traffic-manager-monitoring.md).

## <a name="option-2-deploy-your-application-tooa-new-region"></a>Optie 2: Uw toepassing tooa nieuwe regio implementeren
Meerdere actieve implementaties behouden, zoals beschreven in de vorige optie Hallo leidt ertoe dat aanvullende lopende kosten. Als uw beoogde hersteltijd (RTO) flexibel genoeg is en u de oorspronkelijke code Hallo of gecompileerde Cloud Services-pakket hebt, kunt u een nieuw exemplaar van uw toepassing in een andere regio maken en bijwerken van uw DNS-records toopoint toohello nieuwe implementatie.

Voor meer informatie over het toocreate en implementeren van een servicetoepassing cloud, Zie [hoe toocreate en implementeren van een cloudservice](cloud-services-how-to-create-deploy-portal.md).

Afhankelijk van uw toepassing gegevensbronnen moet u mogelijk toocheck Hallo herstelprocedures voor de gegevensbron van uw toepassing.

* Zie voor gegevensbronnen voor Azure Storage, [Azure Storage-replicatie](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage) toocheck op Hallo-opties die beschikbaar op basis van Hallo zijn replicatiemodel voor uw toepassing hebt gekozen.
* Lees voor de bronnen van de SQL-Database, [overzicht: Cloud zakelijke continuïteit en database noodherstel met SQL Database](../sql-database/sql-database-business-continuity.md) toocheck op Hallo-opties die beschikbaar zijn op basis van Hallo gekozen replicatiemodel voor uw toepassing.


## <a name="option-3-wait-for-recovery"></a>Optie 3: Wacht voor herstel
In dit geval is geen actie ondernemen vereist, maar de service is niet beschikbaar totdat Hallo regio is hersteld. Ziet u de huidige servicestatus Hallo op Hallo [Azure Service Health Dashboard](https://azure.microsoft.com/status/).

## <a name="next-steps"></a>Volgende stappen
meer informatie over hoe tooimplement een herstel na noodgevallen en de strategie van hoge beschikbaarheid, Zie toolearn [herstel na noodgevallen en hoge beschikbaarheid voor Azure-toepassingen](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

Zie voor een gedetailleerde technische kennis van de mogelijkheden van een cloudplatform, toodevelop [technische richtlijnen voor Azure tolerantie](../resiliency/resiliency-technical-guidance.md).
