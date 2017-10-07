---
title: aaaBack van een Exchange server tooAzure back-up met Azure Backup-Server | Microsoft Docs
description: Meer informatie over hoe tooback van een Exchange server-tooAzure back met behulp van Azure Backup-Server
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: e46557e8-2eaf-4ee0-99ea-00fbb8687dca
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: db874161151fc57c5b79c41531e18d577f567f66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-azure-backup-server"></a>Back-up van een Exchange server tooAzure back-up met Azure Backup-Server
Dit artikel wordt beschreven hoe tooconfigure Microsoft Azure Backup-Server (MABS) tooback van een Microsoft Exchange server-tooAzure.  

## <a name="prerequisites"></a>Vereisten
Voordat u doorgaat, zorg ervoor dat Azure Backup-Server [geïnstalleerd en voorbereid](backup-azure-microsoft-azure-backup.md).

## <a name="mabs-protection-agent"></a>De beveiligingsagent MABS
tooinstall hello MABS-beveiligingsagent op Hallo Exchange-server als volgt te werk:

1. Zorg ervoor dat firewalls Hallo correct zijn geconfigureerd. Zie [firewall-uitzonderingen voor Hallo agent configureren](https://technet.microsoft.com/library/Hh758204.aspx).
2. Hallo-agent op Hallo Exchange-server installeren door te klikken op **Management > Agents > installeren** MABS Administrator-console. Zie [installeren Hallo MABS beveiligingsagent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) voor gedetailleerde stappen.

## <a name="create-a-protection-group-for-hello-exchange-server"></a>Maak een beveiligingsgroep voor Hallo Exchange-server
1. In Hallo MABS Administrator-Console, klikt u op **beveiliging**, en klik vervolgens op **nieuw** op Hallo hulpprogramma lint tooopen hello **nieuwe beveiligingsgroep maken** wizard.
2. Op Hallo **Welkom** scherm van de wizard klikt u op Hallo **volgende**.
3. Op Hallo **type beveiligingsgroep selecteren** scherm, selecteert u **Servers** en klik op **volgende**.
4. Selecteer Hallo Exchange server-database dat u wilt dat tooprotect en klikt u op **volgende**.

   > [!NOTE]
   > Als u Exchange 2013 beveiligt, controleert u Hallo [Exchange 2013-vereisten](https://technet.microsoft.com/library/dn751029.aspx).
   >
   >

    In Hallo voorbeeld te volgen, is Hallo Exchange 2010-database geselecteerd.

    ![Groepsleden selecteren](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. Hallo methode voor gegevensbeveiliging selecteren.

    Naam van de beveiligingsgroep Hallo en selecteer vervolgens beide Hallo volgende opties:

   * Ik wil kortetermijnbeveiliging met schijf.
   * Ik wil online beveiliging.
6. Klik op **Volgende**.
7. Selecteer Hallo **Eseutil uitvoeren toocheck gegevensintegriteit** optie als u toocheck Hallo integriteit van Hallo Exchange Server-databases.

    Nadat u deze optie selecteert, back-consistentiecontrole wordt uitgevoerd op een MABS tooavoid Hallo i/o-verkeer dat wordt gegenereerd door het uitvoeren van Hallo **eseutil** opdracht op Hallo Exchange-server.

   > [!NOTE]
   > toouse deze optie, moet u Hallo Ese.dll en Eseutil.exe bestanden toohello C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin map op Hallo mal server kopiëren. Anders de volgende fout hello wordt geactiveerd:  
   > ![Eseutil-fout](./media/backup-azure-backup-exchange-server/eseutil-error.png)
   >
   >
8. Klik op **Volgende**.
9. Selecteer Hallo-database voor **kopieback-up**, en klik vervolgens op **volgende**.

   > [!NOTE]
   > Als u 'Volledige back-up' voor ten minste één DAG kopie van een database niet selecteert, wordt de logboeken worden niet afgekapt.
   >
   >
10. Configureer Hallo doelstellingen voor **kortetermijnback-up**, en klik vervolgens op **volgende**.
11. Bekijk de beschikbare schijfruimte Hallo en klik vervolgens op **volgende**.
12. Selecteer de tijd Hallo op welke Hallo mal Server Hallo initiële replicatie maken en klik vervolgens op **volgende**.
13. Opties voor consistentiecontrole Hallo selecteren en klik vervolgens op **volgende**.
14. Kies Hallo-database wilt tooback up tooAzure en klik vervolgens op **volgende**. Bijvoorbeeld:

    ![Gegevens voor online beveiliging opgeven](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. Definieer de planning Hallo voor **Azure Backup**, en klik vervolgens op **volgende**. Bijvoorbeeld:

    ![Onlineback-upschema opgeven](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > Houd er rekening mee Online herstelpunten zijn gebaseerd op snelle volledige herstelpunten. Daarom moet u plannen Hallo online herstelpunt worden gemaakt na het Hallo-tijd die opgegeven voor Hallo express volledige herstelpunt.
    >
    >
16. Configureer Hallo bewaarbeleid voor **Azure Backup**, en klik vervolgens op **volgende**.
17. Kies een replicatieoptie online en klikt u op **volgende**.

    Als er een grote database, kan het lang duren voor Hallo eerste back-toobe via Hallo netwerk gemaakt. tooavoid dit probleem, kunt u een offline back-up maken.  

    ![Onlinebewaarbeleid opgeven](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. Hallo-instellingen bevestigen en klik vervolgens op **groep maken**.
19. Klik op **Sluiten**.

## <a name="recover-hello-exchange-database"></a>Hallo Exchange-database herstellen
1. toorecover een Exchange-database, klikt u op **herstel** in Hallo MABS Administrator-Console.
2. Hallo Exchange-database die u wilt dat toorecover vinden.
3. Selecteer een online herstelpunt gemaakt in Hallo *hersteltijd* vervolgkeuzelijst.
4. Klik op **herstellen** toostart hello **Herstelwizard**.

Er zijn vijf herstel-typen voor online herstelpunten:

* **Herstellen van Exchange Server-locatie toooriginal:** Hallo gegevens worden hersteld toohello oorspronkelijke Exchange server.
* **Herstel de database op een Exchange Server tooanother:** Hallo gegevens worden tooanother herstelde database op een andere Exchange-server.
* **Tooa hersteldatabase herstellen:** Hallo gegevens worden hersteld tooan Exchange Recovery Database (RDB).
* **Kopiëren tooa netwerkmap:** Hallo gegevens worden hersteld tooa netwerkmap.
* **Kopieer tootape:** als u een tapewisselaar hebt of een zelfstandig tapestation aangesloten en geconfigureerd op MABS, Hallo herstelpunt is tooa vrije tape gekopieerd.

    ![Kies onlinereplicatie](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a>Volgende stappen
* [Veelgestelde vragen over Azure Backup](backup-azure-backup-faq.md)
