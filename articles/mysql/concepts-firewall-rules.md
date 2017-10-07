---
title: aaaAzure Database voor firewallregels voor server MySQL | Microsoft Docs
description: Beschrijft de firewallregels voor uw Azure-Database voor de MySQL-server.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 1f85310385da947b6c492aa6aa21c1b885c2a97d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-server-firewall-rules"></a>Azure voor firewallregels voor server MySQL-Database
Firewalls verhinderen alle toegang tooyour database-server tot u opgeven welke computers over machtigingen beschikken. Hallo firewall verleent toegang toohello server op basis van Hallo IP-adres van elke aanvraag die afkomstig zijn.

tooconfigure uw firewall hebt u firewallregels die aanvaardbaar IP-adresbereiken opgeven. U kunt firewallregels op serverniveau Hallo maken.

**Firewall-regels:** deze regels inschakelen tooaccess clients de volledige Azure-Database voor de MySQL-server, dat wil zeggen, alle Hallo databases binnen dezelfde logische server Hallo. Firewallregels op serverniveau kunnen worden geconfigureerd met behulp van hello Azure-portal of met Azure CLI-opdrachten. toocreate serverniveau firewallregels, moet u de eigenaar van de Hallo-abonnement of een bijdrager abonnement.

## <a name="firewall-overview"></a>Firewalloverzicht
Alle database toegang tooyour Azure Database voor de MySQL-server is door Hallo firewall standaard geblokkeerd. toobegin met behulp van uw server uit een andere computer, moet u toospecify een of meer serverniveau firewall-regels tooenable-tooyour server. Hallo firewall-regels toospecify welk IP-adres, variërend van Hallo Internet tooallow gebruiken. Toegang toohello Azure portal-website zelf wordt niet beïnvloed door Hallo firewallregels.

Verbindingspogingen van Hallo Internet en Azure moet eerst Hallo firewall passeren voordat ze uw Azure-Database voor de MySQL-database bereiken kunnen, zoals wordt weergegeven in het volgende diagram Hallo:

![Voorbeeld van de stroom van de werking van Hallo-firewall](./media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-hello-internet"></a>Verbinding maken vanaf Internet Hallo
Firewallregels op serverniveau gelden tooall databases op Hallo Azure Database voor de MySQL-server.

Als Hallo IP-adres van de aanvraag Hallo binnen één van de opgegeven in het niveau van de server-firewallregels Hallo Hallo-bereiken, wordt Hallo verbinding verleend.

Als Hallo IP-adres van de aanvraag Hallo valt niet binnen Hallo bereiken opgegeven in een Hallo databaseniveau of serverniveau firewallregels, Hallo-verbindingsaanvraag is mislukt.

## <a name="programmatically-managing-firewall-rules"></a>Firewallregels programmatisch beheren
Bovendien toohello Azure-portal, firewall-regels kunnen worden beheerd via een programma met Azure CLI. Zie ook [maken en beheren van Azure-Database voor firewallregels MySQL met Azure CLI](./howto-manage-firewall-using-cli.md)

## <a name="troubleshooting-hello-database-firewall"></a>Hallo-databasefirewall probleemoplossing
Overweeg de volgende punten wanneer toegang toohello Microsoft Azure-Database voor MySQL server-service niet meer werkt zoals verwacht Hallo:

* **Acceptatielijst toohello wijzigingen zijn niet van kracht:** kunnen er maar liefst vijf minuten uitstellen toohello Azure Database voor MySQL-Server firewall configuratie tootake effect wordt gewijzigd.

* **Hallo-aanmelding is niet gemachtigd of een onjuist wachtwoord is gebruikt:** als een aanmelding heeft geen machtigingen op Hallo Azure Database voor MySQL-server of Hallo wachtwoord onjuist is, Hallo verbinding toohello Azure Database voor de MySQL-server is geweigerd. Maken van een firewallinstelling biedt alleen clients met een kans tooattempt verbinding tooyour server; elke client moet Hallo noodzakelijke beveiligingsreferenties opgeven.

* **Dynamische IP-adres:** als u een internetverbinding met dynamische IP-adressering hebt en u problemen ondervindt bij het ophalen via de firewall Hallo, kunt u een van de volgende oplossingen Hallo kan proberen:

* Vraag uw Internetproviderverbindingen (ISP) voor Hallo IP-adresbereik toegewezen tooyour clientcomputers die toegang hello Azure Database voor de MySQL-server en vervolgens Hallo IP-adresbereik toevoegen als een firewallregel.

* Statische IP-adressen in plaats daarvan voor uw clientcomputers ophalen en voeg vervolgens Hallo IP-adressen als firewallregels.

## <a name="next-steps"></a>Volgende stappen

[Maken en beheren van Azure-Database voor firewallregels MySQL hello Azure-portal met](./howto-manage-firewall-using-portal.md)
[maken en beheren van Azure-Database voor firewallregels MySQL met Azure CLI](./howto-manage-firewall-using-cli.md)
