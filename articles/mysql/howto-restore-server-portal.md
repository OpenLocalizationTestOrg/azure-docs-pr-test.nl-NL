---
title: aaaHow tooRestore een Server in Azure-Database voor MySQL | Microsoft Docs
description: Dit artikel wordt beschreven hoe een server in Azure-Database voor het gebruik van MySQL toorestore hello Azure-portal.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a>Hoe tooBackup en terugzetten van een server in Azure-Database voor het gebruik van MySQL hello Azure-portal

## <a name="backup-happens-automatically"></a>Back-up automatisch wordt uitgevoerd
Wanneer u Azure-Database voor MySQL, wordt Hallo database-service automatisch een back-up van Hallo-service om de 5 minuten. 

Hallo back-ups zijn beschikbaar voor de zeven dagen bij gebruik van Basisstaffel en 35 dagen bij gebruik van de Standard-laag. Zie voor meer informatie [Azure Database voor de Servicelagen MySQL](concepts-service-tiers.md)

Met deze functie voor automatische back-up kan u Hallo-server en alle bijbehorende databases herstellen naar een nieuwe server tooan eerder punt in tijd.

## <a name="restore-in-hello-azure-portal"></a>Herstellen in hello Azure-portal
Azure MySQL-Database kunt u toorestore Hallo server back-tooa punt in tijd en in nieuwe versie van de tooa van Hallo-server. U kunt deze nieuwe server toorecover uw gegevens. 

Bijvoorbeeld, als een tabel per ongeluk is kan verwijderd op twaalf uur 's middags vandaag de dag u herstellen toohello tijd net vóór twaalf uur 's middags en Hallo ontbrekende tabel en gegevens van die nieuwe versie van Hallo server ophalen.

Hallo herstelpunt volgt Hallo voorbeeld server tooa in tijd:

1. Meld u aan bij Hallo [Azure-portal](https://portal.azure.com/)

2. Ga naar uw Azure-Database voor de MySQL-server. Selecteer in het linkerdeelvenster Hallo **alle resources**, selecteer uw server uit de lijst Hallo.

3.  Klik op Hallo bovenaan Hallo server overzichtsblade **herstellen** op Hallo-werkbalk. Hallo terugzetten blade wordt geopend.
![Klik op de knop herstellen](./media/howto-restore-server-portal/click-restore-button.png)

4. Hallo terugzetten formulier met Hallo vereiste informatie invullen:

- **Herstelpunt (UTC)**: Selecteer een punt in tijd toorestore aan met picker van Hallo datum en tijd kiezen. Hallo-tijd die is opgegeven is in UTC-notatie, dus u waarschijnlijk tooconvert Hallo lokale tijd in UTC moet.
- **Herstellen van toonew server**: Geef een nieuwe server name toorestore Hallo bestaande server in.
- **Locatie**: Hallo regio keuze automatisch gevuld met Hallo bron server regio en kan niet worden gewijzigd.
- **Prijscategorie**: Hallo prijzen laag keuze automatisch gevuld met Hallo prijzen voor dezelfde als de bronserver Hallo servicetier en kan hier niet worden gewijzigd. 
![PITR terugzetten](./media/howto-restore-server-portal/pitr-restore.png)

5. Klik op **OK** toorestore Hallo server toorestore tooa punt in tijd. 

6. Nadat het Hallo terugzetten is voltooid, zoekt u Hallo nieuwe server die is gemaakt tooverify Hallo databases zijn teruggezet zoals verwacht.

## <a name="next-steps"></a>Volgende stappen
- [Verbindingsbibliotheken voor Azure-Database voor MySQL](concepts-connection-libraries.md)