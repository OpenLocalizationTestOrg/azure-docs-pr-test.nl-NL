---
title: aaaUse Power BI met SQL Data Warehouse | Microsoft Docs
description: Tips voor het gebruik van Power BI met Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a>Power BI gebruiken met SQL datawarehouse
Met de Azure SQL Database kunt SQL Data Warehouse Direct verbinding maken gebruiker tooleverage krachtige logische naar beneden duwen naast Hallo analytische functies van Power BI.  Met Direct Connect's query verzonden back tooyour Azure SQL Data Warehouse in realtime als u Hallo gegevens verkennen.  Deze, in combinatie met de schaal Hallo van SQL Data Warehouse, kunnen gebruikers toocreate dynamische rapporten in minuten op basis van terabytes aan gegevens.  Bovendien Hallo introductie van Hallo openen in Power BI-knop kan gebruikers toodirectly verbinding maken met Power BI tootheir SQL Data Warehouse zonder gegevens te verzamelen uit andere delen van Azure.

Als u Direct Connect Ga Opmerking:

* Geef de volledig gekwalificeerde servernaam Hallo wanneer verbinding wordt gemaakt (Zie hieronder voor meer informatie)
* Zorg ervoor dat de firewallregels voor Hallo database zijn geconfigureerd te 'toestaan toegang tooAzure services'.
* Elke actie zoals een kolom selecteren of een filter toe te voegen rechtstreeks een query uit op Hallo-datawarehouse
* Tegels worden vernieuwd ongeveer elke 15 minuten (vernieuwen hoeft geen toobe gepland)
* Met Q & A is niet beschikbaar voor gegevenssets die Direct Connect
* Wijzigingen in het schema worden niet automatisch opgepikt
* Alle Direct verbinding maken met query's na 2 minuten

Deze beperkingen en -opmerkingen kunnen wijzigen, omdat wij tooimprove Hallo ervaringen. Hallo stappen tooconnect worden hieronder beschreven.  

## <a name="using-hello-open-in-power-bi-button"></a>Met behulp van 'Openen in Power BI' Hallo-knop
Hallo gemakkelijkste manier toomove tussen uw SQL Data Warehouse en Power BI is met hello openen in Power BI-knop. Deze knop kunt u tooseamlessly beginnen met het maken van nieuwe dashboards in Power BI.  

1. tooget gestart Navigeer tooyour SQL Data Warehouse-exemplaar in Hallo klassieke Azure-Portal.
2. Klik op 'Openen in Power BI' Hallo-knop.
3. Als we niet kunnen toosign u rechtstreeks, of als u een Power BI-account niet hebt, moet u toosign in.  
4. U wordt omgeleid toohello SQL Data Warehouse verbindingspagina met de Hallo gegevens van uw SQL Data Warehouse vooraf worden ingevuld.
5. Na het invoeren van uw referenties kunt u zich volledig verbonden tooyour SQL Data Warehouse.

## <a name="connecting-through-hello-power-bi-portal"></a>Verbinding maken via Hallo Power BI-portal
In toevoeging toousing Hallo openen in Power BI-knop, kunnen gebruikers ook tootheir SQL Data Warehouse communiceren via Hallo Power BI-Portal.

1. Klik op gegevens ophalen Hallo Hallo navigatiedeelvenster onderaan in.
2. Selecteer 'Databases'.
3. Selecteer één keer op Hallo Databases pagina 'Azure SQL Data Warehouse' en klik op 'Connect'.
4. Voer de noodzakelijke verbindingsgegevens Hallo.  De servernaam en databasenaam vindt u in hello Azure-Portal.
5. U wordt omgeleid terug hoofdpagina toohello van Power BI en nadat de verbinding wordt gemaakt van een nieuwe vermelding onder 'Gegevenssets' wordt weergegeven met de naam van uw exemplaar Hallo.  
6. U kunt klikken op de nieuwe gegevensset tooexplore Hallo alle Hallo tabellen en weergaven in de database. Als u een kolom selecteert, stuurt query back toohello bron, het visuele element dynamisch te maken. Deze visuele elementen kunnen worden opgeslagen in een nieuw rapport en vastgemaakt terug tooyour dashboard.

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
