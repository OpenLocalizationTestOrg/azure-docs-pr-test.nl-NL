---
title: aaaMigrate uw oplossing tooSQL Data Warehouse | Microsoft Docs
description: Migratie-instructies voor uw oplossing tooAzure SQL Data Warehouse-platform te brengen.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a>Uw oplossing tooAzure SQL Data Warehouse migreren
Zie wat betrokken bij de migratie van een bestaande database oplossing tooAzure SQL Data Warehouse. 

## <a name="profile-your-workload"></a>De werkbelasting van uw profiel
Voordat u migreert, wilt u toobe bepaalde dat SQL Data Warehouse is Hallo juiste oplossing voor uw workload. SQL Data Warehouse is een gedistribueerd systeem ontworpen tooperform analytics op grote hoeveelheden gegevens.  Migreren tooSQL Data Warehouse is vereist voor sommige ontwerpwijzigingen die niet te moeilijk toounderstand, maar sommige tooimplement tijd kunnen duren. Als uw bedrijf een datawarehouse bedrijfsniveau vereist, zijn Hallo voordelen waard Hallo inspanning. Als u geen power Hallo van SQL Data Warehouse, is het echter meer rendabele toouse SQL Server of Azure SQL Database.

Overweeg het gebruik van SQL Data Warehouse wanneer u:
- Een of meer Terabytes aan gegevens hebben
- Toorun analytics voor grote hoeveelheden gegevens plannen
- Hallo mogelijkheid tooscale berekeningen en opslag nodig 
- Gewenste toosave kosten door onderbreken bronnen berekenen wanneer u ze niet nodig.

Gebruik geen SQL Data Warehouse voor operationele (OLTP-systemen)-werkbelastingen met:
- Hoge frequentie leest en schrijft
- Hiermee selecteert u een groot aantal singleton
- Grote hoeveelheden één rij invoegen
- Rij moet verwerken
- Niet-compatibele indeling (JSON, XML)


## <a name="plan-hello-migration"></a>Hallo-migratie plannen

Zodra u hebt besloten een bestaande oplossing tooSQL Data Warehouse toomigrate, is het belangrijk tooplan Hallo migratie voordat het aan de slag. 

Een doel van de planning is tooensure uw gegevens, het tabelschema en uw code compatibel zijn met SQL Data Warehouse. Er zijn bepaalde verschillen toowork compatibiliteit tussen uw huidige systeem- en SQL Data Warehouse rond. Plus, migreert u grote hoeveelheden gegevens tooAzure vergt tijd. Een zorgvuldige planning versnelt uw tooAzure gegevens ophalen. 

Een ander doel van de planning is toomake ontwerp aanpassingen tooensure die uw oplossing maakt gebruik van hoge queryprestaties Hallo die SQL Data Warehouse tooprovide ontworpen. Ontwerppatronen voor verschillende ontwerpen van datawarehouses voor schaal introduceert en dus traditionele methoden zijn niet altijd Hallo beste. Hoewel na de migratie kunt u bepaalde aanpassingen van het ontwerp, sneller wijzigingen aanbrengen in Hallo-proces op een later tijdstip, worden opgeslagen.

tooperform een geslaagde migratie, moet u toomigrate uw tabelschema, uw code en uw gegevens. Zie voor richtlijnen over deze migratieonderwerpen:

-  [Uw schema's migreren](sql-data-warehouse-migrate-schema.md)
-  [Uw code migreren](sql-data-warehouse-migrate-code.md)
-  [Uw gegevens migreren](sql-data-warehouse-migrate-data.md). 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a>Volgende stappen
Hallo CAT (Customer Advisory Team) heeft ook enkele geweldige SQL Data Warehouse richtlijnen, ze via blogs publiceren.  Kijk eens naar hun artikel [migreren tooAzure SQL Data Warehouse-gegevens in de praktijk] [ Migrating data tooAzure SQL Data Warehouse in practice] voor aanvullende hulp bij de migratie.

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
