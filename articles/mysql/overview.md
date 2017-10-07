---
title: aaaOverview van Azure-Database voor relationele databaseservice voor MySQL | Microsoft Docs
description: Overzicht van hello Azure Database voor relationele databaseservice voor MySQL.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 08/02/2017
ms.custom: mvc
ms.openlocfilehash: f02493e2c3c38ccab408a718f98861600481812d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-mysql-service-introduction"></a>Wat is Azure voor MySQL-Database? Inleiding voor service
Azure MySQL-Database is een relationele database-service in Microsoft-cloud op basis van Hallo [MySQL Community Edition](https://www.mysql.com/products/community/) database-engine.  Azure MySQL-Database biedt:

- Voorspelbare prestaties op meerdere serviceniveaus
- Dynamische schaalbaarheid zonder uitvaltijd van toepassing
- Ingebouwde hoge beschikbaarheid
- Gegevensbeveiliging

Deze mogelijkheden nodig bijna geen beheer en alle vindt u zonder extra kosten. Hiermee kunt u toofocus op sneller ontwikkelen en uw toomarket tijd versnellen, plaats u kostbare tijd en bronnen toomanaging virtuele machines en infrastructuur. U kunt bovendien toodevelop uw toepassing Hello open source hulpprogramma's en het platform van uw keuze en leveren Hallo-snel en efficiënt uw bedrijf nodig is zonder nieuwe vaardigheden toolearn blijven.

![Azure conceptueel diagram van MySQL-Database](media/overview/1-azure-db-for-mysql-conceptual-diagram.png)

Dit artikel bevat een inleiding tooAzure Database voor MySQL belangrijkste concepten en functies gerelateerde tooperformance, schaalbaarheid en beheerbaarheid, met koppelingen tooexplore details. Zie dat deze quick start tooget die u gestart:
- [Een Azure-database voor een MySQL-server maken met behulp van Azure Portal](quickstart-create-mysql-server-database-using-azure-portal.md)
- [Een Azure-database voor een MySQL-server maken met behulp van Azure CLI](quickstart-create-mysql-server-database-using-azure-cli.md)

Zie voor een set van Azure CLI-voorbeelden:
- [Azure CLI-voorbeelden voor Azure-Database voor MySQL](sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>Prestaties en schaal aanpassen zonder uitvaltijd
Azure-Database voor de MySQL-service biedt twee Servicelagen: Basic en Standard. Elke laag biedt verschillende prestaties en mogelijkheden toosupport lightweight tooheavyweight database werkbelastingen. U kunt uw eerste app ontwikkelen op een kleine database voor een paar bedragen een maand en klik vervolgens op de service tier tooscale met de behoeften van uw oplossing zonder uitvaltijd wijzigen. Dynamische schaalbaarheid kunt uw database tootransparently reageren toorapidly resourcevereisten wijzigen. U betaalt alleen voor Hallo-resources die u nodig hebt, wanneer u deze nodig.

## <a name="monitoring-and-alerting"></a>Bewaking en waarschuwingen
Hoe weet u Hallo stoppen wanneer u omhoog en omlaag? Gebruik Hallo ingebouwde prestaties bewaken en waarschuwen van functies, gecombineerd met Hallo prestatieclassificaties op basis van de Compute-eenheid. Deze functies gebruikt, kunt u snel beoordelen Hallo gevolgen van de schaal omhoog of omlaag op basis van uw huidige of project prestatievereisten past. Zie [concepten: Servicelagen](concepts-service-tiers.md) voor meer informatie.

## <a name="keep-your-app-and-business-running"></a>Continuïteit van uw app en uw bedrijf
Azure toonaangevende-99,99% beschikbaarheid serviceovereenkomst (SLA) mogelijk gemaakt door een wereldwijd netwerk van door Microsoft beheerde datacenters, wordt voorkomen dat uw app met 24/7. Met elke Azure-Database voor de MySQL-server is u profiteren van de ingebouwde beveiliging, fouttolerantie en gegevensbeveiliging die u anders hebben zou toobuy of ontwerp, maken en beheren. Met Azure-Database voor MySQL, kunt u punt in tijd terugzetten toorecover een tooan server eerder vermeld, tot 35 dagen geleden.

## <a name="secure-your-data"></a>Uw gegevens beveiligen
Azure-database-services hebben een traditie van gegevensbeveiliging dat Azure-Database voor MySQL, met functies die de toegang wordt beperkt, gegevens in rust en in beweging beveiligen en activiteitsbewaking. Ga naar Hallo [Azure Vertrouwenscentrum](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) voor informatie over de beveiliging van de Azure platform.

Hello Azure Database voor de MySQL-service gebruikt de versleuteling van opslag voor gegevens in rust. Back-ups, inclusief gegevens worden versleuteld op de schijf (met uitzondering van Hallo van tijdelijke bestanden, gemaakt door Hallo-engine tijdens het uitvoeren van query's). Hallo-service gebruikt AES 256-bits codering die is opgenomen in Azure storage-versleuteling en Hallo sleutels zijn beheerd door het systeem. Versleuteling van opslag is altijd ingeschakeld en kan niet worden uitgeschakeld.

Standaard hello Azure Database voor de MySQL-service is geconfigureerd toorequire [SSL verbindingsbeveiliging](./concepts-ssl-connection-security.md) voor gegevens in beweging via Hallo-netwerk. Afdwingen van SSL-verbindingen tussen uw database-server en client-toepassingen beschermt tegen 'man-in Hallo middle'-aanvallen door het versleutelen van de gegevensstroom Hallo tussen Hallo-server en uw toepassing.  Desgewenst kunt u uitschakelen dat SSL vereist voor het verbinden van tooyour database-service als de clienttoepassing biedt geen ondersteuning voor SSL-verbindingen.

## <a name="next-steps"></a>Volgende stappen
Nu dat u hebt een inleiding tooAzure Database voor MySQL lees- en beantwoord Hallo vraag 'Wat is Azure MySQL-Database?', kunt u nu naar:
- Zie Hallo pagina kosten vergelijkingen en rekenmachines met prijzen. [Prijzen](https://azure.microsoft.com/pricing/details/mysql/)
- Aan de slag door het maken van uw eerste server. [Een Azure-database voor een MySQL-server maken met behulp van Azure Portal](quickstart-create-mysql-server-database-using-azure-portal.md)
- Bouw uw eerste app in Python, PHP, Ruby, C\#, Java, Node.js: [bibliotheken voor databaseconnectiviteit tooconnect tooAzure Database gebruikt voor MySQL](concepts-connection-libraries.md)
