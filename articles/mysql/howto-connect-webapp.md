---
title: aaaConnect bestaande Azure App Service tooAzure Database voor MySQL | Microsoft Docs
description: Instructies voor hoe tooproperly verbinding maken met een bestaande Database van de Azure App Service-tooAzure voor MySQL
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a>Verbinding maken met een bestaande Azure App Service-tooAzure Database voor de MySQL-server
Dit document wordt uitgelegd hoe u een bestaande Azure App Service-tooyour tooconnect Azure-Database voor MySQL-server.

## <a name="before-you-begin"></a>Voordat u begint
Meld u bij toohello [Azure-portal](https://portal.azure.com). Maak een Azure-Database voor de MySQL-server. Voor meer informatie, Raadpleeg te[hoe toocreate Azure-Database voor MySQL-server van de Portal](quickstart-create-mysql-server-database-using-azure-portal.md) of [hoe toocreate Azure-Database voor MySQL-server met CLI](quickstart-create-mysql-server-database-using-azure-cli.md).

Er zijn momenteel twee oplossingen tooenable toegang van een Azure App Service-tooan Azure Database voor MySQL. Beide oplossingen hebben betrekking op serverniveau firewallregels instellen.

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a>Oplossing 1: Maak een regel firewall tooallow alle IP-adressen
Azure MySQL-Database biedt toegang tot beveiliging op basis van een firewall tooprotect uw gegevens. Als u verbinding maakt vanaf een Azure App Service-tooAzure Database MySQL-server, houd er rekening mee dat Hallo uitgaande zijn IP-adressen van App Service dynamisch karakter. 

tooensure hello beschikbaarheid van uw Azure App Service, wordt u aangeraden deze oplossing tooallow alle IP-adressen.

> [!NOTE]
> Microsoft werkt voor een lange termijn oplossing tooavoid waardoor alle IP-adressen voor Azure-services tooconnect tooAzure Database MySQL.

1. Op Hallo MySQL serverblade onder de instellingen voor kop, klikt u op **verbindingsbeveiliging** tooopen Hallo verbindingsbeveiliging blade voor hello Azure voor MySQL-Database.

   ![Azure-portal - Klik op de beveiliging van de verbinding](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Voer **REGELNAAM**, **START IP**, en **END-IP**. Klik vervolgens op **Opslaan**.
   - Regelnaam: toestaan-All-IP-adressen
   - Start-IP: 0.0.0.0
   - End-IP: 255.255.255.255

   ![Azure-portal - alle IP-adressen toevoegen](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a>Oplossing 2: Maak een firewall regel tooexplicitly uitgaande IP-adressen toestaan
U kunt expliciet toevoegen dat alle Hallo uitgaande IP-adressen van uw Azure App Service.

1. Hallo-App Service-eigenschappen blade voor de weergave uw **uitgaande IP-adres**.

   ![Azure portal - weergave uitgaande IP-adressen](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. Voeg op Hallo MySQL verbinding beveiliging blade uitgaande IP-adressen één voor één.

   ![Azure-portal - expliciete IP-adressen toevoegen](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. Houd er rekening mee te**opslaan** uw firewallregels.

Hoewel het Hallo-Azure App service probeert tookeep IP-adressen constante gedurende een bepaalde periode, zijn er ook gevallen waarbij Hallo IP-adressen mag wijzigen. Bijvoorbeeld wanneer Hallo app recyclet of een schaalaanpassing deze gebeurtenis treedt op wanneer nieuwe machines worden toegevoegd in Azure regionale data centers tooincrease Hallo capaciteit. Wanneer Hallo IP-wijzigen adressen, Hallo app uitvaltijd in deze niet langer verbinding kan maken Hallo-gebeurtenis kan optreden toohello MySQL-server. U kunt dit potentieel bij het kiezen van een van de voorgaande oplossingen Hallo.

## <a name="ssl-configuration"></a>SSL-configuratie
Azure MySQL-Database heeft SSL ingeschakeld. Als uw toepassing niet van SSL tooconnect toohello database gebruikmaakt, moet u toodisable SSL op MySQL-server. Voor meer informatie over het tooconfigure SSL, Zie [met behulp van SSL met Azure-Database voor MySQL](howto-configure-ssl.md).

## <a name="next-steps"></a>Volgende stappen
Raadpleeg te voor meer informatie over verbindingsreeksen[verbindingsreeksen](howto-connection-string.md).
