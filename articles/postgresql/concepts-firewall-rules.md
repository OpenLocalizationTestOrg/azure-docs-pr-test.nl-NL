---
title: Azure-Database voor firewallregels voor PostgreSQL Server | Microsoft Docs
description: Beschrijft de firewallregels voor uw Azure-Database voor PostgreSQL-server.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 1d46a4434c483c3612a9a7b4cdef718d6dc3e765
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-server-firewall-rules"></a>Azure voor firewallregels voor PostgreSQL Server-Database
Firewalls verhinderen alle toegang tooyour database-server tot u opgeven welke computers over machtigingen beschikken. Hallo firewall verleent toegang toohello server op basis van Hallo IP-adres van elke aanvraag die afkomstig zijn.
tooconfigure uw firewall hebt u firewallregels die aanvaardbaar IP-adresbereiken opgeven. U kunt firewallregels op serverniveau Hallo maken.

**Firewall-regels:** deze regels inschakelen clients tooaccess van uw volledige Azure-Database voor PostgreSQL-Server, dat wil zeggen, alle Hallo databases binnen dezelfde logische server Hallo. Firewallregels op serverniveau kunnen worden geconfigureerd met behulp van hello Azure-portal of met Azure CLI-opdrachten. toocreate serverniveau firewallregels, moet u de eigenaar van de Hallo-abonnement of een bijdrager abonnement.

## <a name="firewall-overview"></a>Firewalloverzicht
Alle database toegang tooyour Azure Database voor PostgreSQL-server is door Hallo firewall standaard geblokkeerd. toobegin met behulp van uw server uit een andere computer, moet u toospecify een of meer serverniveau firewall-regels tooenable-tooyour server. Hallo firewall-regels toospecify welk IP-adres, variërend van Hallo Internet tooallow gebruiken. Toegang toohello Azure portal-website zelf wordt niet beïnvloed door Hallo firewallregels.
Verbindingspogingen van Hallo Internet en Azure moet eerst Hallo firewall passeren voordat ze uw PostgreSQL-Database kunnen bereiken zoals weergegeven in het volgende diagram Hallo:

![Voorbeeld van de stroom van de werking van Hallo-firewall](media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-hello-internet"></a>Verbinding maken vanaf Internet Hallo
Firewallregels op serverniveau gelden tooall databases op Hallo Azure Database voor PostgreSQL-server. Als Hallo IP-adres van de aanvraag Hallo binnen één van de opgegeven in het niveau van de server-firewallregels Hallo Hallo-bereiken, wordt Hallo verbinding verleend.
Als Hallo IP-adres van de aanvraag Hallo valt niet binnen Hallo bereiken opgegeven in een Hallo databaseniveau of serverniveau firewallregels, Hallo-verbindingsaanvraag is mislukt.
Bijvoorbeeld, als uw toepassing verbinding met JDBC-stuurprogramma voor PostgreSQL maakt, u deze fout kan optreden tooconnect probeert wanneer Hallo firewall Hallo-verbinding blokkeert.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATALE: Er is geen pg\_hba.conf-vermelding voor de host ": 123.45.67.890", gebruiker 'adminuser', database 'postgresql', SSL

## <a name="programmatically-managing-firewall-rules"></a>Firewallregels programmatisch beheren
Bovendien toohello Azure-portal, firewall-regels kunnen worden beheerd via een programma met Azure CLI.
Zie ook [maken en beheren van Azure-Database voor firewallregels PostgreSQL met Azure CLI](howto-manage-firewall-using-cli.md)

## <a name="troubleshooting-hello-database-firewall"></a>Hallo-databasefirewall probleemoplossing
Overweeg de volgende punten wanneer toegang toohello Microsoft Azure-Database voor PostgreSQL Server-service niet meer werkt zoals verwacht Hallo:

* **Acceptatielijst toohello wijzigingen zijn niet van kracht:** kunnen er maar liefst vijf minuten uitstellen toohello Azure Database voor PostgreSQL Server firewall configuratie tootake effect wordt gewijzigd.

* **Hallo-aanmelding is niet gemachtigd of een onjuist wachtwoord is gebruikt:** als een aanmelding heeft geen machtigingen op Hallo Azure Database voor PostgreSQL-server of Hallo wachtwoord onjuist is, verbinding toohello Azure Database Hallo voor PostgreSQL-server is geweigerd. Maken van een firewallinstelling biedt alleen clients met een kans tooattempt verbinding tooyour server; elke client moet Hallo noodzakelijke beveiligingsreferenties opgeven.

Bijvoorbeeld met behulp van een client JDBC Hallo volgende fout kan worden weergegeven.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATALE: wachtwoordverificatie is mislukt voor gebruiker 'uwgebruikersnaam'

* **Dynamische IP-adres:** als u een internetverbinding met dynamische IP-adressering hebt en u problemen ondervindt bij het ophalen via de firewall Hallo, kunt u een van de volgende oplossingen Hallo kan proberen:

* Vraag uw Internetproviderverbindingen (ISP) voor Hallo IP-adresbereik toegewezen tooyour clientcomputers die toegang hello Azure Database voor PostgreSQL-Server en vervolgens Hallo IP-adresbereik toevoegen als een firewallregel.

* Statische IP-adressen in plaats daarvan voor uw clientcomputers ophalen en voeg vervolgens Hallo IP-adressen als firewallregels.

## <a name="next-steps"></a>Volgende stappen
Zie voor artikelen over het maken van server- en databaseniveau firewall-regels:
* [Maken en beheren van Azure-Database voor firewallregels PostgreSQL met hello Azure-portal](howto-manage-firewall-using-portal.md)
* [Maken en beheren van Azure-Database voor firewallregels PostgreSQL met Azure CLI](howto-manage-firewall-using-cli.md)