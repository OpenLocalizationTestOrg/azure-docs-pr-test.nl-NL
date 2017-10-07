---
title: aaaAzure back-up voor SQL Server-werkbelastingen met behulp van DPM | Microsoft Docs
description: Een inleiding toobacking van SQL Server-databases met hello Azure Backup-service
services: backup
documentationcenter: 
author: adigan
manager: Nkolli
editor: 
ms.assetid: 59df5bec-d959-457d-8731-7b20f7f1013e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: ba78dbf1c7934a259a7bd0bdb7d4467ac75d05a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-sql-server-tooazure-as-a-dpm-workload"></a>Back-up van SQL Server-tooAzure als een werklast DPM
In dit artikel begeleidt u bij de configuratiestappen Hallo voor back-up van SQL Server-databases met Azure Backup.

tooback van SQL Server-databases tooAzure, moet u een Azure-account. Als u geen account hebt, kunt u een gratis proefaccount maken in slechts enkele minuten. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.

Hallo-beheer van back-tooAzure voor SQL Server-database en herstel van Azure omvat drie stappen:

1. Maak een back-upbeleid tooprotect SQL Server-databases tooAzure.
2. Back-ups op aanvraag tooAzure maken.
3. Hallo-database herstellen van Azure.

## <a name="before-you-start"></a>Voordat u begint
Voordat u begint, zorg ervoor dat alle Hallo [vereisten](backup-azure-dpm-introduction.md#prerequisites) voor het gebruik van Microsoft Azure Backup tooprotect werkbelastingen is voldaan. Hallo-vereisten zoals taken besproken: maken van een back-upkluis, referenties voor de kluis, installatie downloaden hello Azure Backup Agent en registreren Hallo-server met Hallo kluis.

## <a name="create-a-backup-policy-tooprotect-sql-server-databases-tooazure"></a>Maak een back-upbeleid tooprotect SQL Server-databases tooAzure
1. Klik op Hallo DPM-server op Hallo **beveiliging** werkruimte.
2. Klik op het lint Hallo **nieuw** toocreate een nieuwe beveiligingsgroep.

    ![Beveiligingsgroep maken](./media/backup-azure-backup-sql/protection-group.png)
3. DPM toont Hallo startscherm met Hallo richtlijnen over het maken van een **beveiligingsgroep**. Klik op **Volgende**.
4. Selecteer **Servers**.

    ![Type beveiligingsgroep - 'Servers' selecteren](./media/backup-azure-backup-sql/pg-servers.png)
5. Vouw Hallo SQL Server-computer waar de back-up gemaakt van Hallo databases toobe aanwezig zijn. DPM bevat verschillende gegevensbronnen die u kunnen een back-up van die server. Vouw Hallo **alle SQL-Shares** en selecteer hello (in dit geval we geselecteerde databases ReportServer$ MSDPM2012 en ReportServer$ MSDPM2012TempDB) toobe back-up gemaakt. Klik op **Volgende**.

    ![SQL-database selecteren](./media/backup-azure-backup-sql/pg-databases.png)
6. Geef een naam voor de beveiligingsgroep Hallo en selecteer Hallo **ik wil online beveiliging** selectievakje.

    ![Methode voor gegevensbeveiliging - kortetermijnbeveiliging op schijf en Online Azure](./media/backup-azure-backup-sql/pg-name.png)
7. In Hallo **Kortetermijndoelen opgeven** scherm, Hallo nodig invoer toocreate back-uppunten toodisk bevatten.

    Hier ziet u dat **bewaartermijn** te is ingesteld*5 dagen*, **Synchronisatiefrequentie** tooonce is ingesteld om *15 minuten* namelijk Hallo de frequentie waarmee back-up is gemaakt. **Snelle volledige back-up** te is ingesteld,*20:00 uur*.

    ![Doelen voor de korte termijn](./media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > Op 20:00 uur (op basis van toohello scherm invoer) een back-uppunt elke dag wordt gemaakt door het overdragen van Hallo-gegevens die zijn gewijzigd van Hallo back-up van de vorige dag 8:00 PM-punt. Dit proces wordt genoemd **snelle volledige back-up**. Tijdens het Hallo-transactielogboeken zijn gesynchroniseerd snelle elke 15 minuten, als er een database moeten toorecover Hallo op 9:00 PM- wordt gemaakt door Hallo logboeken van Hallo Hallo punt laatste volledige back-up punt (8 pm in dit geval).
   >
   >

8. Klik op **Volgende**

    DPM geeft Hallo totale opslagruimte beschikbaar is en Hallo potentiële ruimte schijfgebruik.

    ![Toegewezen schijfruimte](./media/backup-azure-backup-sql/pg-storage.png)

    DPM maakt standaard één volume per gegevensbron (SQL Server-database) dat wordt gebruikt voor de eerste back-up Hallo. Met deze benadering beperkt Hallo Logical Disk Manager (LDM) gegevensbronnen (SQL Server-databases) voor de DPM-beveiliging too300. toowork om deze beperking, selecteer Hallo **dezelfde gegevens in de DPM-opslaggroep plaatsen**, optie. Als u deze optie gebruikt, worden gebruikt één volume voor meerdere gegevensbronnen waarmee DPM tooprotect van too2000 SQL-databases.

    Als **worden Hallo volumes automatisch vergroot** optie is geselecteerd, DPM kunt account voor de back-volume Hallo verhoogd wanneer Hallo productiegegevens groeit. Als **worden Hallo volumes automatisch vergroot** optie niet is geselecteerd, DPM Hallo back-upopslag gebruikt toohello gegevensbronnen in de beveiligingsgroep Hallo beperkt.
9. Beheerders krijgen Hallo keuze van het overdragen van deze eerste back-up handmatig (uit netwerk) tooavoid bandbreedte congestie of via Hallo-netwerk. Ze kunnen ook configureren Hallo tijd op welke Hallo overdracht kan zich voordoen. Klik op **Volgende**.

    ![Methode voor eerste replicatie](./media/backup-azure-backup-sql/pg-manual.png)

    de eerste back-up Hallo vereist overdracht van Hallo gehele gegevensbron (SQL Server-database) van productie-server (SQL Server-machine) toohello DPM-server. Deze gegevens mogelijk te groot worden en gegevens worden overgebracht Hallo via Hallo-netwerk kan groter zijn dan bandbreedte. Om deze reden beheerders kunnen kiezen om tootransfer Hallo eerste back-up: **handmatig** (met behulp van verwijderbare media) tooavoid bandbreedte congestie, of **automatisch via netwerk Hallo** (op een opgegeven tijd).

    Zodra de Hallo eerste back-up is voltooid, zijn Hallo rest Hallo back-ups van incrementele back-ups op Hallo van de eerste back-up. Incrementele back-ups hebben vaak toobe klein en eenvoudig via Hallo-netwerk worden overgedragen.
10. Kies de gewenste Hallo consistentie selectievakje toorun en klik op **volgende**.

    ![Consistentiecontrole](./media/backup-azure-backup-sql/pg-consistent.png)

    DPM kan een consistentiecontrole selectievakje toocheck Hallo integriteit van de back-uppunt Hallo uitvoeren. Hallo controlesom van Hallo back-upbestand op Hallo productieserver (SQL Server-machine in dit scenario) en gegevens van de back-up Hallo voor het bestand op DPM wordt berekend. In geval van een conflict hello wordt ervan uitgegaan dat Hallo back-upbestand op DPM is beschadigd. DPM herstelt Hallo back-upgegevens door te sturen Hallo blokken overeenkomt toohello checksum komt niet overeen. Hallo consistentiecontrole is een prestatie-intensieve bewerking, hebt beheerders Hallo optie Hallo consistentiecontrole plannen of er wordt automatisch uitgevoerd.
11. toospecify online beveiliging van gegevensbronnen hello, selecteer Hallo databases toobe beveiligd tooAzure en klikt u op **volgende**.

    ![Selecteer de gegevensbronnen](./media/backup-azure-backup-sql/pg-sqldatabases.png)
12. Beheerders kunnen kiezen voor back-upschema en bewaarbeleidsregels die aan de behoeften van de beleidsregels van hun organisatie.

    ![Planning en retentie](./media/backup-azure-backup-sql/pg-schedule.png)

    In dit voorbeeld worden back-ups eenmaal per dag uitgevoerd op 12:00 uur en 20: 00 (onderste gedeelte van het welkomstscherm)

    > [!NOTE]
    > Het is een goede gewoonte toohave een aantal herstelpunten op korte termijn op schijf voor een snel herstel. Deze herstelpunten worden gebruikt voor 'operationeel herstel'. Azure fungeert als een goede externe locatie met hogere Sla's en beschikbaarheid gegarandeerd.
    >
    >

    **Kunt u beter**: Zorg ervoor dat Azure back-ups zijn gepland na voltooiing van de Hallo van de lokale schijf back-ups met behulp van DPM. Hierdoor Hallo nieuwste schijf back-toobe gekopieerd tooAzure.

13. Hallo beleid bewaarschema kiezen. Hallo details over de werking van het bewaarbeleid Hallo zijn beschikbaar op [gebruik Azure Backup tooreplace uw tape-infrastructuur artikel](backup-azure-backup-cloud-as-tape.md).

    ![Bewaarbeleid](./media/backup-azure-backup-sql/pg-retentionschedule.png)

    In dit voorbeeld:

    * Back-ups eenmaal per dag worden uitgevoerd op 12:00 uur en 20: 00 (onderste gedeelte van het welkomstscherm) en 180 dagen worden bewaard.
    * Hallo back-up elke zaterdag om 12:00 uur 104 weken wordt bewaard
    * Hallo back-up op laatste zaterdag om 12:00 uur 60 maanden bewaard
    * Hallo back-up op laatste zaterdag maart om 12:00 uur tien jaar worden bewaard
14. Klik op **volgende** en selecteer Hallo relevante optie voor het overdragen van Hallo eerste back-up tooAzure. U kunt kiezen **automatisch via netwerk Hallo** of **Offline back-up**.

    * **Automatisch via netwerk Hallo** overdrachten Hallo back-upgegevens tooAzure volgens Hallo-schema voor back-up is gekozen.
    * Hoe **Offline back-up** works wordt uitgelegd op [Offlineback-upwerkstroom in Azure Backup](backup-azure-backup-import-export.md).

    Kies Hallo relevante overdracht mechanisme toosend Hallo eerste back-up tooAzure en op **volgende**.
15. Zodra u de details van het beleid in Hallo Hallo bekijken **samenvatting** scherm, klikt u op Hallo **groep maken** knop toocomplete Hallo werkstroom. U kunt klikken op Hallo **sluiten** knop en de monitor Hallo taak uitgevoerd in de werkruimte bewaking.

    ![Maken van een beveiligingsgroep In uitvoering](./media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a>Op aanvraag back-up van een SQL Server-database
Tijdens de vorige stappen Hallo een back-upbeleid gemaakt, wordt 'herstelpunt' alleen gemaakt als Hallo eerste back-up plaatsvindt. In plaats van te wachten op Hallo scheduler tookick in, Hallo stappen hieronder trigger Hallo maken van een herstel handmatig verwijzen.

1. Wacht totdat de ziet u de status van de groep beveiliging Hallo **OK** voor Hallo-database voordat u Hallo herstelpunt maakt.

    ![Leden van beveiligingsgroep](./media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. Met de rechtermuisknop op het Hallo-database en selecteer **herstelpunt maken**.

    ![Online herstelpunt maken](./media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. Kies **Onlinebeveiliging** in de vervolgkeuzelijst Hallo en klik op **OK**. Hiermee start u Hallo aanmaak van een herstelpunt in Azure.

    ![Herstelpunt maken](./media/backup-azure-backup-sql/sqlbackup-azure.png)
4. U kunt de voortgang van de taak Hallo weergeven in Hallo **bewaking** werkruimte vindt u een onderhanden zoals een beschreven in de volgende figuur Hallo Hallo taak.

    ![Bewaking van console](./media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a>Een SQL Server-database herstellen van Azure
Hallo zijn volgende stappen vereist toorecover een beveiligde entiteit (SQL Server-database) van Azure.

1. Open Hallo DPM-server-beheerconsole. Navigeer te**herstel** werkruimte waarin u Hallo servers zien kunt een back-up door DPM. Blader Hallo vereiste database (in dit geval ReportServer$ MSDPM2012). Selecteer een **herstel vanaf** die eindigt op **Online**.

    ![Herstelpunt selecteren](./media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. Met de rechtermuisknop op het Hallo-databasenaam en klik op **herstellen**.

    ![Herstellen van Azure](./media/backup-azure-backup-sql/sqlbackup-recover.png)
3. DPM Hallo worden details weergegeven van Hallo herstelpunt. Klik op **Volgende**. hersteltype selecteren Hallo-database Hallo toooverwrite **herstellen toooriginal exemplaar van SQL Server**. Klik op **Volgende**.

    ![TooOriginal locatie herstellen](./media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    In dit voorbeeld maakt DPM het herstellen van Hallo database tooanother SQL Server-exemplaar of tooa zelfstandige netwerkmap.
4. In Hallo **herstelopties opgeven** scherm kunt u opties voor herstel van Hallo zoals netwerkbandbreedtegebruik toothrottle Hallo bandbreedte die wordt gebruikt door de herstelbewerking. Klik op **Volgende**.
5. In Hallo **samenvatting** scherm ziet u alle configuraties voor Hallo herstel tot nu toe is opgegeven. Klik op **herstellen**.

    Hallo herstelstatus toont Hallo-database wordt hersteld. U kunt klikken op **sluiten** tooclose Hallo wizard en bekijkt hello voortgang op Hallo **bewaking** werkruimte.

    ![Proces voor accountherstel initiëren](./media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    Zodra Hallo herstel is voltooid, is hersteld Hallo database consistent-toepassing.

### <a name="next-steps"></a>Volgende stappen
• [Veelgestelde vragen over azure Backup](backup-azure-backup-faq.md)
