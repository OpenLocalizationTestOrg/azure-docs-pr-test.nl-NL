---
title: aaaAzure Advisor kosten aanbevelingen | Microsoft Docs
description: Gebruik Azure Advisor toooptimize Hallo kosten van uw Azure-implementaties.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a>Advisor kosten aanbevelingen

Advisor helpt u te optimaliseren en reduceren uw algehele Azure hoeven te besteden aan met het vaststellen van niet-actieve- en onderbenutte resources. U aanbevelingen van Hallo ophalen kost **kosten** tabblad op Hallo Advisor dashboard.

![Tabblad van Advisor kosten](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a>Optimaliseren door het formaat onderbenutte exemplaren te besteden aan de virtuele machine 
Hoewel bepaalde toepassingsscenario's leiden minder gebruik standaard tot kunnen, kunt u vaak geld besparen door het beheer van Hallo grootte en het aantal van uw virtuele machines. Advisor bewaakt het gebruik van uw virtuele machine 14 dagen en identificeert dan laag gebruik virtuele machines. Virtuele machines waarvan CPU-gebruik 5 is % of minder en netwerkgebruik is 7 MB of minder voor vier of meer dagen worden beschouwd als laag gebruik virtuele machines.

Advisor ziet u Hallo geschatte kosten van continue toorun uw virtuele machine, zodat u tooshut deze omlaag of het formaat kunt kiezen.  

![Advisor kosten aanbevelingen voor het vergroten of verkleinen van virtuele machines](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a>Gebruik een voordelige oplossing toomanage prestatiedoelen van meerdere SQL-databases
Advisor identificeert SQL server-exemplaren die u profiteren kunnen van het maken van pools voor elastische databases. Pools voor elastische databases bieden een eenvoudige en voordelige oplossing toomanage prestatiedoelstellingen Hallo van meerdere databases die verschillende gebruikspatronen hebben. Zie voor meer informatie over Azure elastische pools [wat is er een Azure elastische pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).

![Advisor kosten aanbevelingen voor pools voor elastische databases](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a>Hoe tooaccess aanbevelingen in Azure Advisor kosten

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).

2. Klik in het linkerdeelvenster Hallo **meer services**.

3. Service in Hallo menu deelvenster onder **bewaking en beheer**, klikt u op **Azure Advisor**.  
 Hallo Advisor dashboard wordt weergegeven.

4. Klik op Hallo Advisor dashboard Hallo **kosten** tabblad.

5. Selecteer Hallo abonnement waarvoor u wilt dat tooreceive aanbevelingen en klik vervolgens op **aanbevelingen krijgen**.

> [!NOTE]
> tooaccess aanbevelingen Advisor te ontvangen, moet u eerst *registreren van uw abonnement* met Advisor. Een abonnement is geregistreerd als een *abonnement eigenaar* gestart Hallo dashboard en klikt op Hallo van Advisor **aanbevelingen krijgen** knop. Dit is een *eenmalige bewerking*. Nadat het Hallo-abonnement is geregistreerd, kunt u Advisor aanbevelingen als openen *eigenaar*, *Inzender*, of *lezer* voor een abonnement, een resourcegroep of een bepaalde resource.

## <a name="next-steps"></a>Volgende stappen

toolearn meer informatie over de aanbevelingen van Advisor, Zie:
* [Inleiding tooAdvisor](advisor-overview.md)
* [Aan de slag](advisor-get-started.md)
* [Aanbevelingen van Advisor-prestaties](advisor-cost-recommendations.md)
* [Hoge beschikbaarheid aanbevelingen Advisor te ontvangen](advisor-cost-recommendations.md)
* [Aanbevelingen voor beveiliging van Advisor](advisor-cost-recommendations.md)
