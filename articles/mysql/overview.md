---
title: Overzicht van Azure-Database voor relationele databaseservice voor MySQL | Microsoft Docs
description: Overzicht van de Azure-Database voor relationele databaseservice voor MySQL.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 08/02/2017
ms.custom: mvc
ms.openlocfilehash: a1becaf8465f68ecac768c5c6b2dbc95e8ff7278
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-azure-database-for-mysql-service-introduction"></a>Wat is Azure voor MySQL-Database? Inleiding voor service
Azure MySQL-Database is een relationele database-service in de Microsoft-cloud op basis van [MySQL Community Edition](https://www.mysql.com/products/community/) database-engine.  Azure MySQL-Database biedt:

- Voorspelbare prestaties op meerdere serviceniveaus
- Dynamische schaalbaarheid zonder uitvaltijd van toepassing
- Ingebouwde hoge beschikbaarheid
- Gegevensbeveiliging

Deze mogelijkheden nodig bijna geen beheer en alle vindt u zonder extra kosten. Hiermee kunt u zich richten op sneller ontwikkelen en de tijd op de markt versnellen, plaats u kostbare tijd en hulpmiddelen voor het beheren van virtuele machines en infrastructuur. U kunt bovendien blijven te ontwikkelen van uw toepassing met de open-source hulpprogramma's en het platform van uw keuze en leveren met de snelheid en uw bedrijf nodig is zonder te leren van nieuwe vaardigheden efficiëntie.

![Azure conceptueel diagram van MySQL-Database](media/overview/1-azure-db-for-mysql-conceptual-diagram.png)

Dit artikel bevat een inleiding tot Azure-Database voor MySQL belangrijkste concepten en functies met betrekking tot prestaties, schaalbaarheid en beheerbaarheid, met koppelingen naar meer gedetailleerde informatie. Zie deze Quick Starts om snel aan de slag te gaan:
- [Een Azure-database voor een MySQL-server maken met behulp van Azure Portal](quickstart-create-mysql-server-database-using-azure-portal.md)
- [Een Azure-database voor een MySQL-server maken met behulp van Azure CLI](quickstart-create-mysql-server-database-using-azure-cli.md)

Zie voor een set van Azure CLI-voorbeelden:
- [Azure CLI-voorbeelden voor Azure-Database voor MySQL](sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>Prestaties en schaal aanpassen zonder uitvaltijd
Azure-Database voor de MySQL-service biedt twee Servicelagen: Basic en Standard. Elke laag biedt verschillende prestaties en mogelijkheden voor lichte tot zware workloads van databases. U kunt uw eerste app ontwikkelen op een kleine database voor een paar bedragen een maand en klik vervolgens op uw servicetier schaal met de behoeften van uw oplossing zonder uitvaltijd wijzigen. Dynamische schaalbaarheid kunt transparant reageren op snel veranderende resourcevereisten van uw database. U betaalt alleen voor de resources die u nodig hebt, wanneer u deze nodig.

## <a name="monitoring-and-alerting"></a>Bewaking en waarschuwingen
Hoe weet u wanneer u moet stoppen met omhoog of omlaag schalen? Gebruik de ingebouwde prestaties bewaken en waarschuwen functies, gecombineerd met de prestatieclassificaties op basis van de Compute-eenheid. Deze functies gebruikt, kunt u snel beoordelen de impact van de schaal omhoog of omlaag op basis van uw huidige of project prestatievereisten past. Zie [concepten: Servicelagen](concepts-service-tiers.md) voor meer informatie.

## <a name="keep-your-app-and-business-running"></a>Continuïteit van uw app en uw bedrijf
Azure toonaangevende-99,99% beschikbaarheid serviceovereenkomst (SLA) mogelijk gemaakt door een wereldwijd netwerk van door Microsoft beheerde datacenters, wordt voorkomen dat uw app met 24/7. Met elke Azure-Database voor de MySQL-server is u profiteren van de ingebouwde beveiliging, fouttolerantie en gegevensbeveiliging die u anders moet kopen of ontwerpen, bouwen en beheren. Met Azure-Database voor MySQL, kunt u herstellen punt in tijd voor het herstellen van een server naar een eerdere toestand, tot 35 dagen geleden.

## <a name="secure-your-data"></a>Uw gegevens beveiligen
Azure-database-services hebben een traditie van gegevensbeveiliging dat Azure-Database voor MySQL, met functies die de toegang wordt beperkt, gegevens in rust en in beweging beveiligen en activiteitsbewaking. Ga naar de [Azure Vertrouwenscentrum](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) voor informatie over de beveiliging van de Azure platform.

De Azure-Database voor de MySQL-service gebruikt de versleuteling van opslag voor gegevens in rust. Back-ups, inclusief gegevens worden versleuteld op de schijf (met uitzondering van tijdelijke bestanden gemaakt door de engine tijdens het uitvoeren van query's). De service gebruikt AES 256-bits codering die is opgenomen in Azure storage-versleuteling en de sleutels zijn beheerd door het systeem. Versleuteling van opslag is altijd ingeschakeld en kan niet worden uitgeschakeld.

De Azure-Database voor de MySQL-service is standaard geconfigureerd om te vereisen [SSL verbindingsbeveiliging](./concepts-ssl-connection-security.md) voor gegevens in beweging via het netwerk. Afdwingen van SSL-verbindingen tussen uw database-server en client-toepassingen beschermt tegen 'man-in het midden'-aanvallen door het versleutelen van de gegevensstroom tussen de server en uw toepassing.  Desgewenst kunt u uitschakelen dat SSL vereist voor het verbinden met uw database-service als de clienttoepassing biedt geen ondersteuning voor SSL-verbindingen.

## <a name="next-steps"></a>Volgende stappen
Nu dat u hebt een inleiding tot Azure-Database voor MySQL lees- en de vraag beantwoord 'Wat is Azure MySQL-Database?', kunt u nu naar:
- Zie de pagina met prijzen kosten vergelijkingen en rekenmachines. [Prijzen](https://azure.microsoft.com/pricing/details/mysql/)
- Aan de slag door het maken van uw eerste server. [Een Azure-database voor een MySQL-server maken met behulp van Azure Portal](quickstart-create-mysql-server-database-using-azure-portal.md)
- Bouw uw eerste app in Python, PHP, Ruby, C\#, Java, Node.js: [bibliotheken voor databaseconnectiviteit verbinding maken met Azure Database MySQL gebruikt](concepts-connection-libraries.md)
