---
title: aaaServer concepten in Azure-Database voor PostgreSQL | Microsoft Docs
description: In dit onderwerp worden overwegingen en richtlijnen gegeven voor het werken met Azure-Database voor PostgreSQL-servers.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 9cc7816992f2ddedd76fdf906075a723b97720a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-servers"></a>Azure-Database voor PostgreSQL-Servers
In dit onderwerp worden overwegingen en richtlijnen gegeven voor het werken met Azure-Database voor PostgreSQL-servers.

## <a name="what-is-an-azure-database-for-postgresql-server"></a>Wat is een Azure-Database voor PostgreSQL-server?
Een Azure-Database voor PostgreSQL-server is een centrale beheerdersrechten voor meerdere databases. Dit is dezelfde constructie van PostgreSQL-server die u mogelijk kent met in Hallo lokale wereld Hallo. In het bijzonder Hallo PostgreSQL-service wordt beheerd, prestaties garanties biedt, beschrijft de toegangs- en -functies op serverniveau.

Een Azure-Database voor PostgreSQL-server:

- In een Azure-abonnement is gemaakt.
- Hallo bovenliggende resource voor databases is.
- Biedt een naamruimte voor databases.
- Is een container met sterke levensduur semantiek - een server verwijderen en Hallo opgenomen databases worden verwijderd.
- Collocates resources in een regio.
- Biedt een eindpunt voor de verbinding voor server en database-toegang (. postgresql.database.azure.com).
- Biedt Hallo bereik voor management-beleidsregels die van toepassing tooits databases: aanmelding, firewall, gebruikers, rollen, configuraties, enzovoort.
- Is beschikbaar in meerdere versies. Zie voor meer informatie [ondersteund PostgreSQL-databaseversies](concepts-supported-versions.md).
- Kan worden uitgebreid door gebruikers. Zie voor meer informatie [PostgreSQL extensies](concepts-extensions.md).

U kunt een of meerdere databases maken binnen een Azure-Database voor PostgreSQL-server. U kunt kiezen toocreate een individuele database per server tooutilize alle Hallo resources of meerdere databases tooshare Hallo resources maken. Hallo prijzen gestructureerde per server, op basis van de configuratie van prijscategorie hello, compute-eenheden, opslag (GB). Zie voor meer informatie [Prijscategorieën](./concepts-service-tiers.md).

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-postgresql-server"></a>Hoe ik verbinding maken en verifiëren van tooan Azure Database voor PostgreSQL-server?
Hallo zorgen volgende elementen veilige toegang tooyour database.

|||
| :-- | :-- |
| **Verificatie en autorisatie** | Azure-Database voor PostgreSQL-server ondersteunt systeemeigen PostgreSQL-verificatie. U kunt verbinding maken en verifiëren van tooserver met Hallo van aanmeldgegevens van serverbeheerder. |
| **Protocol** | Hallo-service ondersteunt een protocol op basis van een bericht dat wordt gebruikt door PostgreSQL. |
| **TCP/IP** | Hallo-protocol wordt ondersteund via TCP/IP en via Unix-domain-sockets. |
| **Firewall** | toohelp uw gegevens beschermen, een firewallregel voorkomt u dat alle toegang tooyour database-server of tooits databases, totdat u welke computers opgeven gemachtigd. Zie [Azure Database voor firewallregels voor PostgreSQL Server](concepts-firewall-rules.md). |
|||

## <a name="how-do-i-manage-a-server"></a>Hoe kan ik een server beheren?
U kunt Azure Database beheren voor PostgreSQL-servers met behulp van Azure portal of Hallo Hallo [Azure CLI](/cli/azure/postgres).

## <a name="next-steps"></a>Volgende stappen
- Zie voor een overzicht van service Hallo [Azure-Database voor PostgreSQL-overzicht](overview.md)
- Voor informatie over specifieke resource quota's en beperkingen op basis van uw **servicelaag**, Zie [Servicelagen](concepts-service-tiers.md)
- Zie voor informatie over het maken van verbinding toohello service, [verbindingsbibliotheken voor Azure-Database voor PostgreSQL](concepts-connection-libraries.md).
