---
title: aaaOverview van Azure-Database voor relationele databaseservice voor PostgreSQL | Microsoft Docs
description: Biedt een overzicht van Azure-Database voor relationele databaseservice voor PostgreSQL.
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.custom: mvc
ms.service: postgresql
ms.topic: overview
ms.date: 08/01/2017
ms.openlocfilehash: fd6821b56e5295b8b341d87b14d113f7a4b247c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-postgresql"></a>Wat is Azure Database voor PostgreSQL?

Azure PostgreSQL-Database is een relationele database-service in de Microsoft cloud gebouwd voor ontwikkelaars op basis van de community-versie van de open-source Hallo Hallo [PostgreSQL](https://www.postgresql.org/) database-engine. Deze service is in de openbare preview. Azure PostgreSQL-Database biedt:
- Voorspelbare prestaties op meerdere serviceniveaus
- Dynamische schaalbaarheid zonder uitvaltijd van toepassing
- Ingebouwde hoge beschikbaarheid
- Gegevensbeveiliging

Alle deze mogelijkheden nodig bijna geen beheer en alle vindt u zonder extra kosten. Deze mogelijkheden kunnen u toofocus op snelle ontwikkeling van toepassingen en uw toomarket tijd versnellen, plaats u kostbare tijd en bronnen toomanaging virtuele machines en infrastructuur. U kunt bovendien toodevelop uw toepassing Hello open source hulpprogramma's en het platform van uw keuze en leveren Hallo-snel en efficiënt uw bedrijf nodig is zonder nieuwe vaardigheden toolearn blijven. 

Dit artikel bevat een inleiding tooAzure Database voor PostgreSQL belangrijkste concepten en functies gerelateerde tooperformance, schaalbaarheid en beheerbaarheid. Zie dat deze quick start tooget die u gestart:

- [Een Azure-Database maken voor PostgreSQL met Azure portal](quickstart-create-server-database-portal.md)
- [Een Azure-Database maken voor PostgreSQL hello Azure CLI gebruiken](quickstart-create-server-database-azure-cli.md)

Zie de volgende artikelen voor een reeks Azure CLI- en PowerShell-voorbeelden:

- [Azure CLI-voorbeelden voor Azure-Database voor PostgreSQL](./sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>Prestaties en schaal aanpassen zonder uitvaltijd

Azure-Database voor PostgreSQL-service biedt momenteel twee Servicelagen: Basic en Standard. Elke servicelaag biedt [verschillende niveaus van prestaties, garanties IOP's en mogelijkheden](concepts-service-tiers.md) toosupport lightweight tooheavyweight database werkbelastingen. U kunt uw eerste app ontwikkelen op een kleine server voor slechts enkele euro's per maand en vervolgens [Hallo prestatieniveau wijzigen](scripts/sample-scale-server-up-or-down.md) servicetier binnen de service handmatig of programmatisch op elk moment toomeet Hallo behoeften van uw oplossing. U kunt dit doen zonder uitvaltijd tooyour aanvraag of tooyour klanten. Dynamische schaalbaarheid Hiermee kunt u uw database tootransparently reageren toorapidly resourcevereisten en schakelt u tooonly betalen voor Hallo resources dat u nodig hebt wanneer u deze nodig wijzigen.

## <a name="monitoring-and-alerting"></a>Bewaking en waarschuwingen
Hoe bepaal u wanneer toodial omhoog en omlaag? U gebruikt Hallo ingebouwde prestatiebewaking en -functies, gecombineerd met Hallo prestatieclassificaties op basis van eenheden Compute waarschuwingen. Met behulp van deze hulpprogramma's, u kunt snel inzicht in de Hallo impact van Compute eenheden omhoog schalen of naar beneden op basis van de prestatiebehoeften van uw huidige of de verwachte. Zie voor meer informatie [Azure-Database voor PostgreSQL-opties en prestaties: inzicht in wat er beschikbaar is in elke servicelaag](./concepts-service-tiers.md).

## <a name="keep-your-app-and-business-running"></a>Continuïteit van uw app en uw bedrijf
Azure toonaangevende-99,99% beschikbaarheid (niet beschikbaar in preview) serviceovereenkomst (SLA) mogelijk gemaakt door een wereldwijd netwerk van door Microsoft beheerde datacenters, wordt voorkomen dat uw app met 24/7. Met elke Azure-Database voor PostgreSQL-server is u profiteren van de ingebouwde beveiliging, fouttolerantie en gegevensbeveiliging die u anders hebben zou toobuy of ontwerp, maken en beheren. Met Azure-Database voor PostgreSQL biedt elke servicelaag een uitgebreide set functies voor zakelijke continuïteit en opties die u tooget up kunt en wordt uitgevoerd en blijf op deze manier. U kunt [punt in tijd terugzetten](howto-restore-server-portal.md) tooreturn een tooan database eerder vermeld, tot 35 dagen geleden. Als Hallo datacenter die als host fungeert voor uw databases een storing optreedt, kunt u bovendien databases terugzetten van geografisch redundante exemplaren van recente back-ups.

## <a name="secure-your-data"></a>Uw gegevens beveiligen
Azure-database-services hebben een traditie van gegevensbeveiliging dat Azure-Database voor PostgreSQL, met functies die de toegang wordt beperkt, gegevens in rust en in beweging beveiligen en activiteitsbewaking. Ga naar Hallo [Azure Vertrouwenscentrum](https://www.microsoft.com/TrustCenter/Security/default.aspx) voor informatie over de beveiliging van de Azure platform.

Hello Azure Database voor PostgreSQL-service gebruikt de versleuteling van opslag voor gegevens in rust. Gegevens met inbegrip van back-ups worden op schijf (met uitzondering van Hallo van tijdelijke bestanden, gemaakt door Hallo-engine tijdens het uitvoeren van query's) versleuteld. Hallo-service gebruikt AES 256-bits codering die is opgenomen in Azure storage-versleuteling en Hallo sleutels zijn beheerd door het systeem. Versleuteling van opslag is altijd ingeschakeld en kan niet worden uitgeschakeld.

Standaard hello Azure Database voor PostgreSQL-service geconfigureerd toorequire is [SSL verbindingsbeveiliging](./concepts-ssl-connection-security.md) voor gegevens in beweging via Hallo-netwerk. Afdwingen van SSL-verbindingen tussen uw database-server en client-toepassingen beschermt tegen 'man-in Hallo middle'-aanvallen door het versleutelen van de gegevensstroom Hallo tussen Hallo-server en uw toepassing.  Desgewenst kunt u uitschakelen dat SSL vereist voor het verbinden van tooyour database-service als de clienttoepassing biedt geen ondersteuning voor SSL-verbindingen.

## <a name="next-steps"></a>Volgende stappen
- Zie Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/postgresql/) kosten vergelijkingen en rekenmachines.
- Aan de slag door [maken van uw eerste Azure-Database voor PostgreSQL](./quickstart-create-server-database-portal.md).
- Bouw uw eerste app in Python, PHP, Ruby, C\#, Java, Node.js: [verbindingsbibliotheken](./concepts-connection-libraries.md)
