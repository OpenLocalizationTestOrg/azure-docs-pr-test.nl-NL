---
title: Hoe een Server in Azure-Database voor PostgreSQL tooRestore | Microsoft Docs
description: Dit artikel wordt beschreven hoe een server in Azure-Database voor het gebruik van PostgreSQL toorestore hello Azure-portal.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: bc7351f384607397806d837afd3e1d7a26575e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-postgresql-using-hello-azure-portal"></a>Hoe tooBackup en terugzetten van een server in Azure-Database voor het gebruik van PostgreSQL hello Azure-portal

## <a name="backup-happens-automatically"></a>Back-up automatisch wordt uitgevoerd
Wanneer u Azure-Database voor PostgreSQL, wordt Hallo database-service automatisch een back-up van Hallo-service om de 5 minuten. 

Hallo back-ups zijn beschikbaar voor de zeven dagen bij gebruik van Basisstaffel en 35 dagen bij gebruik van de Standard-laag. Zie voor meer informatie [Azure Database voor de Servicelagen PostgreSQL](concepts-service-tiers.md)

Met deze functie voor automatische back-up kan u Hallo-server en alle bijbehorende databases herstellen naar een nieuwe server tooan eerder punt in tijd.

## <a name="restore-in-hello-azure-portal"></a>Herstellen in hello Azure-portal
Azure PostgreSQL-Database kunt u toorestore Hallo server back-tooa punt in tijd en in nieuwe versie van de tooa van Hallo-server. U kunt deze nieuwe server toorecover uw gegevens. 

Bijvoorbeeld, als een tabel per ongeluk is kan verwijderd op twaalf uur 's middags vandaag de dag u herstellen toohello tijd net vóór twaalf uur 's middags en Hallo ontbrekende tabel en gegevens van die nieuwe versie van Hallo server ophalen.

Hallo herstelpunt volgt Hallo voorbeeld server tooa in tijd:
1. Meld u aan bij Hallo [Azure-portal](https://portal.azure.com/)
2. Ga naar uw Azure-Database voor PostgreSQL-server. In hello Azure-portal, klikt u op **alle Resources** van links menu Hallo en typt u de naam van de Hallo, zoals **mypgserver 20170401**, toosearch voor uw bestaande server. Klik op Hallo servernaam weergegeven in zoekresultaten Hallo. Hallo **overzicht** pagina voor de server wordt geopend en opties voor verdere configuratie biedt.

   ![Azure-portal - toolocate uw server zoeken](media/postgresql-howto-restore-server-portal/1-locate.png)

3. Klik op Hallo bovenaan Hallo server overzichtsblade **herstellen** op Hallo-werkbalk. Hallo terugzetten blade wordt geopend.

   ![Azure-Database voor herstel PostgreSQL - overzicht - knop](./media/postgresql-howto-restore-server-portal/2_server.png)

4. Hallo terugzetten formulier met Hallo vereiste informatie invullen:

   ![Azure-Database voor PostgreSQL - informatie terugzetten ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - **Herstelpunt**: Selecteer een point-in-time die deze gebeurtenis treedt op voordat het Hallo-server is gewijzigd
  - **Doelserver**: Geef een nieuwe naam van een server toorestore naar gewenste
  - **Locatie**: U kunt geen Hallo regio selecteren, standaard is dit hetzelfde als de bronserver Hallo
  - **Prijscategorie**: U kunt deze waarde niet wijzigen bij het herstellen van een server. Dit is hetzelfde als de bronserver Hallo. 

5. Klik op **OK** toorestore Hallo server toorestore tooa punt in tijd. 

6. Zodra het Hallo terugzetten is voltooid, zoek Hallo nieuwe server die wordt gemaakt tooverify Hallo gegevens is hersteld, zoals verwacht.

## <a name="next-steps"></a>Volgende stappen
- [Verbindingsbibliotheken voor Azure-Database voor PostgreSQL](concepts-connection-libraries.md)
