---
title: aaaCreate en beheren van Azure-Database voor firewallregels MySQL hello Azure-portal met | Microsoft Docs
description: Maken en beheren van Azure-Database voor firewallregels MySQL met hello Azure-portal
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a>Maken en beheren van Azure-Database voor firewallregels MySQL met hello Azure-portal
Firewallregels op serverniveau inschakelen beheerders tooaccess een Azure-Database voor MySQL-Server uit een opgegeven IP-adres of een bereik van IP-adressen. 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Maken van een firewallregel op serverniveau in hello Azure-portal

1. Op Hallo MySQL serverblade onder de instellingen voor kop, klikt u op **verbindingsbeveiliging** tooopen Hallo verbindingsbeveiliging blade voor hello Azure voor MySQL-Database.

   ![Azure-portal - Klik op de beveiliging van de verbinding](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Klik op **Mijn IP toevoegen** op Hallo werkbalk toocreate een regel met Hallo IP-adres van uw computer, zoals waargenomen door hello Azure systeem.

   ![Azure-portal - Klik op toevoegen Mijn IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Controleer of uw IP-adres voordat u opslaat Hallo-configuratie. In sommige situaties Hallo IP-adres door Azure-portal waargenomen verschilt Hallo IP-adres dat wordt gebruikt wanneer toegang tot Hallo internet en Azure-servers. Daarom moet u toochange Hallo eerste IP- en eind-IP-toomake Hallo regel functie zoals verwacht.

   Gebruik een zoekmachine of andere toocheck online hulpprogramma uw eigen IP-adres (Zoek bijvoorbeeld naar 'Wat is Mijn IP-adres').

   ![Bing voor Mijn IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Voeg aanvullende adresbereiken. In het Hallo-regels voor hello Azure Database voor MySQL firewall, kunt u één IP-adres of een bereik aan adressen opgeven. Als u wilt dat toolimit Hallo regel tooone één IP-adres, type Hallo dezelfde in Hallo veld voor het eerste IP- en eind-IP-adres. Hallo firewall openen kan beheerders en gebruikers tooaccess alle databases op Hallo MySQL server toowhich ze geldige referenties bevatten.

   ![Azure portal - firewall-regels ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. Klik op **opslaan** op Hallo werkbalk toosave deze firewallregel op serverniveau. Wacht op bevestiging van Hallo Hallo update toohello firewallregels is geslaagd.

   ![Azure-portal - Klik op Opslaan](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Bestaande serverniveau firewallregels via hello Azure-portal beheren
Herhaal Hallo stappen toomanage Hallo firewall-regels.
* tooadd hello huidige computer, klikt u op **+ Mijn IP toevoegen**.
* tooadd extra IP-adressen, typt u Hallo **REGELNAAM**, **eerste IP-**, en **END-IP**.
* een bestaande regel toomodify klikt u op een van de velden in de regel Hallo Hallo en wijzigen.
* een bestaande toodelete sluiten, klikt u op Hallo weglatingsteken [...] en klik op **verwijderen**.
* Klik op **opslaan** toosave Hallo wijzigingen.

## <a name="next-steps"></a>Volgende stappen
- Zie voor informatie over tooan Azure Database voor de MySQL-server verbinding [verbindingsbibliotheken voor Azure-Database voor MySQL](./concepts-connection-libraries.md)
