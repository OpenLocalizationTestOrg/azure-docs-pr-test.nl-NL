---
title: aaaLimitations in Azure-Database voor MySQL | Microsoft Docs
description: Preview-beperkingen in Azure-Database voor MySQL beschrijft.
services: mysql
author: jasonh
ms.author: kamathsun
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 9c877c592bf640f62182d8761c9c51363882d706
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-mysql-preview"></a>Beperkingen in Azure-Database voor MySQL (Preview)
Hello Azure Database voor de MySQL-service is in de openbare preview. Hallo volgende secties beschrijven capaciteit en functionele limieten in Hallo database-service.

## <a name="service-tier-maximums"></a>Service Tier maximumwaarden
Azure MySQL-Database heeft meerdere Servicelagen die u kiezen kunt uit bij het maken van een server. Zie voor meer informatie [begrijpen wat er beschikbaar is in elke servicelaag](concepts-service-tiers.md).  

Er is een maximum aantal verbindingen, compute-eenheden en opslag in elke servicelaag tijdens Hallo service preview, als volgt: 

|                            |                   |
| :------------------------- | :---------------- |
| **Maximum aantal verbindingen**        |                   |
| Basic 50 Compute-eenheden     | 50-verbindingen    |
| Basic 100 Compute-eenheden    | 100-verbindingen   |
| Standaard 100 Compute-eenheden | 200-verbindingen   |
| Standaard 200 Compute-eenheden | 300-verbindingen   |
| Standaard 400 Compute-eenheden | 400-verbindingen   |
| Standaard 800 Compute-eenheden | 500-verbindingen   |
| **Maximale Compute-eenheden**      |                   |
| Basisservicelaag         | 100 compute-eenheden |
| Standaardservicelaag      | 800 compute-eenheden |
| **Maximale opslag**            |                   |
| Basisservicelaag         | 1 TB              |
| Standaardservicelaag      | 1 TB              |

Wanneer er te veel verbindingen zijn bereikt, wordt het foutbericht Hallo volgende fout:
> FOUT (08004) 1040: Te veel verbindingen

## <a name="preview-functional-limitations"></a>Preview functionele beperkingen:
### <a name="scale-operations"></a>Schaalbewerkingen:
1.  Dynamische schaalbaarheid van servers in Servicelagen is momenteel niet ondersteund. Dat wil zeggen, schakelen tussen servicecategorieën Basic en Standard.
2.  Dynamische toename mogelijk op aanvraag van opslag op vooraf gemaakte server is momenteel niet ondersteund.
3.  Verkleinen storage server wordt niet ondersteund.

### <a name="server-version-upgrades"></a>Versie-upgrades voor server:
- Automatische migratie tussen versies van de primaire database-engine is momenteel niet ondersteund.

### <a name="subscription-management"></a>Beheer van abonnementen:
- Dynamisch vooraf gemaakte servers verplaatsen tussen abonnement en resourcegroep is momenteel niet ondersteund.

### <a name="point-in-time-restore"></a>Punt-in-time-terugzetten:
1.  Herstellen van de servicelaag toodifferent en/of Compute-eenheden en de opslaggrootte is niet toegestaan.
2.  Herstellen van een uitgevallen server wordt niet ondersteund.

## <a name="next-steps"></a>Volgende stappen
[Wat is beschikbaar in elke servicelaag](concepts-service-tiers.md)
[MySQL-Database-versies ondersteund](concepts-supported-versions.md)
