---
title: aaaBack van een Exchange server tooAzure back-up met System Center 2012 R2 DPM | Microsoft Docs
description: Meer informatie over hoe tooback van een Exchange server-tooAzure back met System Center 2012 R2 DPM
services: backup
documentationcenter: 
author: MaanasSaran
manager: NKolli1
editor: 
ms.assetid: 13f32256-888e-416e-a78b-40c2a26a5939
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: masaran;jimpark;delhan;trinadhk;markgal
ms.openlocfilehash: fa99296d095c180333474b6d419ebc5ec727547a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-system-center-2012-r2-dpm"></a>Back-up van een Exchange server tooAzure back-up met System Center 2012 R2 DPM
Dit artikel wordt beschreven hoe tooconfigure een System Center 2012 R2 Data Protection Manager (DPM) server tooback van een Microsoft Exchange-server te Azure Backup.  

## <a name="updates"></a>Updates
toosuccessfully registreren Hallo DPM-server met Azure Backup, moet u Hallo nieuwste updatepakket voor System Center 2012 R2 DPM en Hallo meest recente versie van hello Azure Backup Agent installeren. De meest recente updatepakket Hallo ophalen uit Hallo [Microsoft catalogus](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).

> [!NOTE]
> Voor Hallo voorbeelden in dit artikel, versie 2.0.8719.0 van hello Azure Backup Agent is geïnstalleerd en Update Rollup 6 op System Center 2012 R2 DPM is geïnstalleerd.
>
>

## <a name="prerequisites"></a>Vereisten
Voordat u doorgaat, controleert u of alle Hallo [vereisten](backup-azure-dpm-introduction.md#prerequisites) voor het gebruik van Microsoft Azure Backup tooprotect werkbelastingen is voldaan. Deze vereisten zijn Hallo volgende:

* Een back-upkluis op Hallo Azure site is gemaakt.
* Agent en de kluisreferenties hebben gedownloade toohello DPM-server is.
* Hallo-agent is geïnstalleerd op Hallo DPM-server.
* Hallo kluisreferenties zijn gebruikte tooregister Hallo DPM-server.
* Als u Exchange 2016 beveiligt, voer een upgrade uit tooDPM 2012 R2 UR9 of hoger

## <a name="dpm-protection-agent"></a>DPM-beveiligingsagent
tooinstall hello DPM-beveiligingsagent op Hallo Exchange-server als volgt te werk:

1. Zorg ervoor dat firewalls Hallo correct zijn geconfigureerd. Zie [firewall-uitzonderingen voor Hallo agent configureren](https://technet.microsoft.com/library/Hh758204.aspx).
2. Hallo-agent op Hallo Exchange-server installeren door te klikken op **Management > Agents > installeren** in DPM Administrator-Console. Zie [installeren Hallo DPM-beveiligingsagent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) voor gedetailleerde stappen.

## <a name="create-a-protection-group-for-hello-exchange-server"></a>Maak een beveiligingsgroep voor Hallo Exchange-server
1. In Hallo DPM Administrator-Console, klikt u op **beveiliging**, en klik vervolgens op **nieuw** op Hallo hulpprogramma lint tooopen hello **nieuwe beveiligingsgroep maken** wizard.
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

    Nadat u deze optie selecteert, back-consistentiecontrole wordt uitgevoerd op Hallo DPM server tooavoid Hallo i/o-verkeer die wordt gegenereerd door het uitvoeren van Hallo **eseutil** opdracht op Hallo Exchange-server.

   > [!NOTE]
   > toouse deze optie, moet u Hallo Ese.dll en Eseutil.exe bestanden toohello C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory op Hallo DPM-server kopiëren. Anders de volgende fout hello wordt geactiveerd:  
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
12. Selecteer de tijd Hallo op welke Hallo DPM server Hallo initiële replicatie maken en klik vervolgens op **volgende**.
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
1. toorecover een Exchange-database, klikt u op **herstel** in Hallo DPM Administrator-Console.
2. Hallo Exchange-database die u wilt dat toorecover vinden.
3. Selecteer een online herstelpunt gemaakt in Hallo *hersteltijd* vervolgkeuzelijst.
4. Klik op **herstellen** toostart hello **Herstelwizard**.

Er zijn vijf herstel-typen voor online herstelpunten:

* **Herstellen van Exchange Server-locatie toooriginal:** Hallo gegevens worden hersteld toohello oorspronkelijke Exchange server.
* **Herstel de database op een Exchange Server tooanother:** Hallo gegevens worden tooanother herstelde database op een andere Exchange-server.
* **Tooa hersteldatabase herstellen:** Hallo gegevens worden hersteld tooan Exchange Recovery Database (RDB).
* **Kopiëren tooa netwerkmap:** Hallo gegevens worden hersteld tooa netwerkmap.
* **Kopieer tootape:** als u een tapewisselaar hebt of een zelfstandig tapestation aangesloten en geconfigureerd op Hallo DPM-server Hallo herstelpunt is tooa vrije tape gekopieerd.

    ![Kies onlinereplicatie](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a>Volgende stappen
* [Veelgestelde vragen over Azure Backup](backup-azure-backup-faq.md)
