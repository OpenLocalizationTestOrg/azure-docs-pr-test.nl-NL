---
title: aaaCreate en beheren van Azure-Database voor firewallregels PostgreSQL hello Azure-portal met | Microsoft Docs
description: Maken en beheren van Azure-Database voor firewallregels PostgreSQL met hello Azure-portal
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a>Maken en beheren van Azure-Database voor firewallregels PostgreSQL met hello Azure-portal
Firewallregels op serverniveau inschakelen beheerders tooaccess een Azure-Database voor PostgreSQL-Server uit een opgegeven IP-adres of een bereik van IP-adressen. 

## <a name="prerequisites"></a>Vereisten
toostep via deze procedure-tooguide die u nodig:
- Een server [PostgreSQL een Azure-Database gemaakt](quickstart-create-server-database-portal.md)

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Maken van een firewallregel op serverniveau in hello Azure-portal
1. Op Hallo PostgreSQL serverblade onder de instellingen voor kop, klikt u op **verbindingsbeveiliging** tooopen Hallo verbindingsbeveiliging blade voor hello Azure voor PostgreSQL-Database.

  ![Azure-portal - Klik op de beveiliging van de verbinding](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Klik op **Mijn IP toevoegen** op Hallo-werkbalk. Hiermee maakt u een regel automatisch met Hallo IP-adres van uw computer, zoals waargenomen door hello Azure systeem.

  ![Azure-portal - Klik op toevoegen Mijn IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Controleer of uw IP-adres voordat u opslaat Hallo-configuratie. In sommige situaties Hallo IP-adres door Azure-portal waargenomen verschilt Hallo IP-adres dat wordt gebruikt wanneer toegang tot Hallo internet en Azure-servers. Daarom moet u toochange Hallo eerste IP- en eind-IP-toomake Hallo regel functie zoals verwacht.
Gebruik een zoekmachine of andere toocheck online hulpprogramma uw eigen IP-adres (bijvoorbeeld Bing zoeken 'Wat is Mijn IP').

  ![Bing zoeken naar wat Mijn IP is](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Voeg aanvullende adresbereiken. In het Hallo-regels voor hello Azure Database voor PostgreSQL firewall, kunt u één IP-adres of een bereik aan adressen opgeven. Als u wilt dat toolimit Hallo regel tooone één IP-adres, type Hallo dezelfde in Hallo veld voor het eerste IP- en eind-IP-adres. Hallo firewall openen kan beheerders en gebruikers toologin tooany-database op Hallo PostgreSQL server toowhich ze geldige referenties bevatten.

  ![Azure portal - firewall-regels ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. Klik op **opslaan** op Hallo werkbalk toosave deze firewallregel op serverniveau. Wacht op bevestiging van Hallo Hallo update toohello firewallregels is geslaagd.

  ![Azure-portal - Klik op Opslaan](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Bestaande serverniveau firewallregels via hello Azure-portal beheren
Herhaal Hallo stappen toomanage Hallo firewall-regels.
* tooadd hello huidige computer, klik op de knop hello te + **Mijn IP toevoegen**. Klik op **opslaan** toosave Hallo wijzigingen.
* tooadd extra IP-adressen, typt u in Hallo regelnaam, eerste IP-adres en laatste IP-adres. Klik op **opslaan** toosave Hallo wijzigingen.
* een bestaande regel toomodify klikt u op een van de velden in de regel Hallo Hallo en wijzigen. Klik op **opslaan** toosave Hallo wijzigingen.
* een bestaande regel toodelete Hallo weglatingsteken [...] en klik op Hallo regel voor het verwijderen van verwijderen. Klik op **opslaan** toosave Hallo wijzigingen.

## <a name="next-steps"></a>Volgende stappen
- Op deze manier kunt in een script te[maken en beheren van Azure-Database voor firewallregels PostgreSQL met Azure CLI](howto-manage-firewall-using-cli.md)
- Zie voor informatie over verbinding tooan Azure Database voor PostgreSQL server [verbindingsbibliotheken voor Azure-Database voor PostgreSQL](concepts-connection-libraries.md)
