---
title: Het herstellen van een Server in Azure-Database voor MySQL | Microsoft Docs
description: Dit artikel wordt beschreven hoe u een server in Azure-Database herstelt voor MySQL met de Azure portal.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 8c06dce534b628a602127fd02b152c8e04e02cc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-mysql-using-the-azure-portal"></a>Het back-up en herstellen van een server in Azure-Database voor MySQL met de Azure portal

## <a name="backup-happens-automatically"></a>Back-up automatisch wordt uitgevoerd
Wanneer u Azure-Database voor MySQL, wordt de database-service automatisch een back-up van de service om de 5 minuten. 

De back-ups zijn beschikbaar voor de zeven dagen bij gebruik van Basisstaffel en 35 dagen bij gebruik van de Standard-laag. Zie voor meer informatie [Azure Database voor de Servicelagen MySQL](concepts-service-tiers.md)

Met deze functie voor automatische back-up kan u de server en alle bijbehorende databases herstellen naar een nieuwe server aan een eerder punt in tijd.

## <a name="restore-in-the-azure-portal"></a>Herstellen in de Azure portal
Azure MySQL-Database kunt u de server weer terugzetten naar een punt in tijd en in op een nieuwe kopie van de server. U kunt deze nieuwe server gebruiken om uw gegevens te herstellen. 

Bijvoorbeeld, als een tabel per ongeluk is kan verwijderd op twaalf uur 's middags vandaag de dag u herstellen en de tijd net vóór twaalf uur 's middags en ophalen van de ontbrekende tabel en de gegevens van die nieuwe kopie van de server.

De volgende stappen uit voor het herstellen van de voorbeeldserver naar een punt in tijd:

1. Meld u aan bij de [Azure-portal](https://portal.azure.com/)

2. Ga naar uw Azure-Database voor de MySQL-server. Selecteer in het linkerdeelvenster **alle resources**, selecteer uw server uit de lijst.

3.  Klik boven aan de overzichtsblade van server **herstellen** op de werkbalk. De Restore-blade wordt geopend.
![Klik op de knop herstellen](./media/howto-restore-server-portal/click-restore-button.png)

4. Vul het formulier terugzetten met de vereiste informatie in:

- **Herstelpunt (UTC)**: Selecteer een point-in-time om naar te herstellen met de objectkiezer datum en tijd kiezen. De opgegeven tijd is in UTC-notatie, dus u waarschijnlijk moet worden de lokale tijd geconverteerd naar UTC.
- **Herstellen naar de nieuwe server**: Geef een nieuwe naam van de server om de bestaande server naar te herstellen.
- **Locatie**: de keuze regio automatisch gevuld met de server bron regio en kan niet worden gewijzigd.
- **Prijscategorie**: de prijscategorie laag keuze automatisch gevuld met de dezelfde prijscategorie als de bronserver en kan hier niet worden gewijzigd. 
![PITR terugzetten](./media/howto-restore-server-portal/pitr-restore.png)

5. Klik op **OK** om de server te herstellen naar een punt in tijd te herstellen. 

6. Nadat het herstel is voltooid, zoekt u de nieuwe server die is gemaakt om te controleren of dat de databases zijn teruggezet zoals verwacht.

## <a name="next-steps"></a>Volgende stappen
- [Verbindingsbibliotheken voor Azure-Database voor MySQL](concepts-connection-libraries.md)