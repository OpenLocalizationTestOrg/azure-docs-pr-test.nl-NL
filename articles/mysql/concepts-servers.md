---
title: aaaServer concepten in Azure-Database voor MySQL | Microsoft Docs
description: In dit onderwerp worden overwegingen en richtlijnen gegeven voor het werken met Azure-Database voor de MySQL-servers.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 4d994cbdbde93ac5af3f4a2a7375b5851bebb1cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="server-concepts-in-azure-database-for-mysql"></a>Concepten van de server in Azure voor MySQL-Database
In dit onderwerp worden overwegingen en richtlijnen gegeven voor het werken met Azure-Database voor de MySQL-servers.

## <a name="what-is-an-azure-database-for-mysql-server"></a>Wat is een Azure-Database voor de MySQL-server?

Een Azure-Database voor de MySQL-server is een centrale beheerdersrechten voor meerdere databases. Dit is dezelfde constructie van MySQL-server die u mogelijk kent met in Hallo lokale wereld Hallo. In het bijzonder hello Azure Database voor de MySQL-service wordt beheerd, prestaties garanties biedt, beschrijft de toegangs- en -functies op serverniveau.

Een Azure-Database voor de MySQL-server:

- In een Azure-abonnement is gemaakt.
- Hallo bovenliggende resource voor databases is.
- Biedt een naamruimte voor databases.
- Is een container met sterke levensduur semantiek - een server verwijderen en Hallo opgenomen databases worden verwijderd.
- Collocates resources in een regio.
- Biedt een eindpunt voor de verbinding voor server en toegang tot de database.
- Biedt Hallo bereik voor management-beleidsregels die van toepassing tooits databases: aanmelding, firewall, gebruikers, rollen, configuraties, enzovoort.
- Is beschikbaar in meerdere versies. Zie voor meer informatie [Azure-Database wordt ondersteund voor versies van MySQL-database](./concepts-supported-versions.md).

Op een Azure Database voor MySQL-server kunt u een of meerdere databases maken. U kunt kiezen toocreate een individuele database per server tooutilize alle Hallo resources of meerdere databases tooshare Hallo resources maken. Hallo prijzen gestructureerde per server, op basis van de configuratie van prijscategorie hello, compute-eenheden, opslag (GB). Zie voor meer informatie [Prijscategorieën](./concepts-service-tiers.md).

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-mysql-server"></a>Hoe ik verbinding maken en verifiëren van tooan Azure Database voor de MySQL-server?

Hallo zorgen volgende elementen veilige toegang tooyour database.

|||
| :-- | :-- |
| **Verificatie en autorisatie** | Azure-Database voor de MySQL-server ondersteunt systeemeigen MySQL-verificatie. U kunt verbinding maken en verifiëren van tooserver met Hallo van aanmeldgegevens van serverbeheerder. |
| **Protocol** | Hallo-service ondersteunt een protocol op basis van een bericht dat wordt gebruikt door MySQL. |
| **TCP/IP** | Hallo-protocol wordt ondersteund via TCP/IP en via Unix-domain-sockets. |
| **Firewall** | toohelp uw gegevens beschermen, een firewallregel voorkomt u dat alle toegang tooyour database-server of tooits databases, totdat u welke computers opgeven gemachtigd. Zie [Azure Database voor firewallregels voor MySQL Server](./concepts-firewall-rules.md). |
| **SSL** | Hallo-service ondersteunt afdwingen SSL-verbindingen tussen uw toepassingen en uw database-server.  Zie [configureren van SSL-verbindingen in uw toepassing toosecurely tooAzure Database connect voor MySQL](./howto-configure-ssl.md). |
|||

## <a name="how-do-i-manage-a-server"></a>Hoe kan ik een server beheren?
U kunt Azure-Database voor de MySQL-servers beheren met behulp van hello Azure-portal of Azure CLI Hallo.

## <a name="next-steps"></a>Volgende stappen
- Zie voor een overzicht van service Hallo [Azure-Database voor MySQL-overzicht](./overview.md)
- Voor informatie over specifieke resource quota's en beperkingen op basis van uw **servicelaag**, Zie [Servicelagen](./concepts-service-tiers.md)
- Zie voor meer informatie over het maken van verbinding toohello service [verbindingsbibliotheken voor Azure-Database voor MySQL](./concepts-connection-libraries.md).
