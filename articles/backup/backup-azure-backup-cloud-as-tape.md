---
title: Azure Backup-tooreplace aaaUse uw tape-infrastructuur | Microsoft Docs
description: Informatie over hoe Azure Backup biedt tape-achtige-semantiek waardoor u toobackup en het herstellen van gegevens in Azure
services: backup
documentationcenter: 
author: trinadhk
manager: vijayts
editor: 
ms.assetid: 2e1bb67d-986c-4437-8056-3a63169b4214
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 1/10/2017
ms.author: saurse;trinadhk;markgal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4c5b095d95d39267c54b1eed9427bda09658bb94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-your-long-term-storage-from-tape-toohello-azure-cloud"></a>Uw langdurige opslag verplaatsen van tape toohello Azure-cloud
Azure back-up- en System Center Data Protection Manager-klanten kunnen:

* Maak een back-up van gegevens in de schema's die het best past bij Hallo organisatorische behoeften.
* Back-upgegevens Hallo behouden voor langere tijd
* Controleer Azure een deel van hun lange bewaartermijn (in plaats van tape moet).

Dit artikel wordt uitgelegd hoe klanten back-up en retentie beleidsregels kunnen inschakelen. Klanten die gebruikmaken van tapes tooaddress hun lange-termijn-bewaren moet beschikt nu over een krachtige en levensvatbaar alternatief Hallo en de beschikbaarheid van deze functie. Hallo functie is ingeschakeld in de meest recente release Hallo van hello Azure Backup (die beschikbaar is [hier](http://aka.ms/azurebackup_agent)). System Center DPM klanten moeten bijwerken naar, ten minste DPM 2012 R2 UR5 voordat u DPM met hello Azure Backup-service.

## <a name="what-is-hello-backup-schedule"></a>Wat is Hallo back-upschema?
Hallo back-upschema Hallo frequentie van back-upbewerking Hallo aangeeft. Hallo-instellingen in het volgende scherm Hallo bijvoorbeeld aangeven dat de back-ups dagelijks om 18: 00 uur en om middernacht worden genomen.

![Dagelijks schema](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

Klanten kunnen ook een wekelijkse back-up plannen. Bijvoorbeeld hello instellingen in het volgende scherm Hallo aangeven dat de back-ups elke alternatieve zondag & woensdag op 9:30:00 uur en 1:00 uur worden genomen.

![Wekelijkse planning](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-hello-retention-policy"></a>Wat is Hallo bewaarbeleid?
Hallo bewaarbeleid geeft Hallo duur waarvoor Hallo back-up moet worden opgeslagen. In plaats van alleen 'plat beleid' voor alle back-uppunten opgeeft, kunnen klanten opgeven verschillende Bewaarbeleidsregels op basis van wanneer Hallo back-up is gemaakt. Bijvoorbeeld, blijft Hallo back-uppunt dagelijks, genomen die als een operationele herstelpunt maakt fungeert, behouden gedurende 90 dagen. Hallo back-uppunt die is genomen op Hallo einde van elk kwartaal voor auditdoeleinden blijft behouden gedurende een langere periode.

![Bewaarbeleid](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

Hallo totaal aantal 'bewaarpunten' opgegeven in dit beleid is 90 (punten per dag) + 40 (elk kwartaal tien jaar) = 130.

## <a name="example--putting-both-together"></a>Voorbeeld: het samenstellen van beide
![Voorbeeldscherm](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. **Dagelijkse bewaarbeleid**: back-ups dagelijks die zijn opgeslagen voor de zeven dagen.
2. **Wekelijkse bewaarbeleid**: back-ups die elke dag om middernacht en 18: 00 uur zaterdag bewaard voor vier weken
3. **Maandelijkse bewaarbeleid**: back-ups die op middernacht en 18: 00 uur op Hallo Laatste zaterdag van elke maand worden bewaard gedurende 12 maanden
4. **Jaarlijks bewaarbeleid**: back-ups die op Hallo om middernacht Laatste zaterdag van elke maart tien jaar worden bewaard

Totaal aantal 'bewaarpunten' hello (punten waaruit een klant kunt gegevens herstellen) in Hallo voorgaande diagram als volgt berekend:

* twee beheerpunten herstelpunten per dag voor de zeven dagen = 14
* twee beheerpunten per week voor vier weken = 8 herstelpunten
* twee beheerpunten per maand gedurende 12 maanden = 24 herstelpunten
* één punt per jaar per 10 jaar = 10 herstel verwijst

Totaal aantal herstelpunten Hallo is 56.

> [!NOTE]
> Azure backup heeft geen beperking op het aantal herstelpunten.
>
>

## <a name="advanced-configuration"></a>Geavanceerde configuratie
Door te klikken op **wijzigen** in Hallo voorgaande scherm, klanten hebben meer flexibiliteit bij het bewaarschema opgeven.

![Wijzigen](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over Azure Backup:

* [Inleiding tooAzure back-up](backup-introduction-to-azure-backup.md)
* [Azure Backup proberen](backup-try-azure-backup-in-10-mins.md)
