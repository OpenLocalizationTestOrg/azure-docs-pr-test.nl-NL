---
title: aaaRestore gegevens tooa Windows Server of Windows-Client van het gebruik van Azure Hallo klassieke implementatiemodel | Microsoft Docs
description: Meer informatie over hoe toorestore van een Windows Server of Windows-Client.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 85585dfc-c764-4e8c-8f0e-40b969640ac2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 4d1458d5233c4f55004ecfa95cbf7b3b18a03dde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-hello-classic-deployment-model"></a>Herstellen van bestanden tooa WindowsServer of Windows client-computer met het klassieke implementatiemodel Hallo
> [!div class="op_single_selector"]
> * [Klassieke portal](backup-azure-restore-windows-server-classic.md)
> * [Azure Portal](backup-azure-restore-windows-server.md)
>
>

Dit artikel wordt uitgelegd hoe toorecover gegevens uit een back-up-kluis en herstel hem tooa server of computer. U start in maart 2017, kunt u niet langer maken back-upkluizen in de klassieke portal Hallo.

> [!IMPORTANT]
> U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden. Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.<br/> **15 oktober 2017**, u niet langer kunnen toouse PowerShell toocreate Backup-kluizen. <br/> **Vanaf 1 november 2017**:
>- Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.
>- U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo. In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.
>

toorestore gegevens, gebruikt u Hallo gegevens herstellen wizard in Hallo Microsoft Azure Recovery Services (MARS)-agent. Wanneer u gegevens herstelt, is het mogelijk om te:

* Terugzetten van gegevens toohello dezelfde machine uit welke Hallo back-ups zijn uitgevoerd.
* Gegevens tooan alternatieve machine herstellen.

Microsoft uitgebracht in januari 2017 een Preview update toohello MARS-agent. Samen met oplossingen voor problemen, deze update kan direct herstellen, zodat u toomount een momentopname van een beschrijfbare herstelpunt als een volume herstel. U kunt vervolgens Hallo herstel volume en kopieert u bestanden tooa lokale computer waardoor selectief terugzetten bestanden verkennen.

> [!NOTE]
> Hallo [januari 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is vereist als u gegevens van toouse toorestore direct herstellen. Back-upgegevens Hallo moeten ook worden beveiligd in kluizen in de landinstellingen die worden vermeld in artikel Hallo-ondersteuning. Raadpleeg Hallo [januari 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) voor de meest recente lijst Hallo van landinstellingen die ondersteuning bieden voor chatberichten te herstellen. Direct herstellen is **niet** momenteel in alle landen beschikbaar.
>

Chatberichten terugzetten is beschikbaar voor gebruik in de Recovery Services-kluizen in hello Azure-portal en Backup-kluizen in de klassieke portal Hallo. Als u toouse direct herstellen wilt, Hallo MARS update downloaden en Hallo procedures volgen die vermeld direct herstellen.


## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a>Direct herstellen toorecover gegevens toohello gebruiken dezelfde machine

Als u een bestands- en desgewenst toorestore per ongeluk hebt verwijderd deze toohello dezelfde machine (vanaf welke Hallo back-up is gemaakt), Hallo te volgen stappen vindt u een Hallo-gegevens herstellen.

1. Open Hallo **Microsoft Azure Backup** uitlijnen in. Als u niet waar Hallo-module is geïnstalleerd weet, zoekt u Hallo computer of server voor **Microsoft Azure Backup**.

    Hallo bureaublad-app moet worden weergegeven in zoekresultaten Hallo.

2. Klik op **gegevens herstellen** toostart Hallo-wizard.

    ![Gegevens herstellen](./media/backup-azure-restore-windows-server/recover.png)

3. Op Hallo **aan de slag** deelvenster, toorestore Hallo gegevens toohello dezelfde server of computer, selecteer **deze server (`<server name>`)** en klik op **volgende**.

    ![Kies deze server optie toorestore Hallo gegevens toohello dezelfde machine](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. Op Hallo **herstelmodus Selecteer** deelvenster kiezen **afzonderlijke bestanden en mappen** en klik vervolgens op **volgende**.

    ![Blader door bestanden](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. Op Hallo **Volume selecteert en datum** deelvenster, selecteer Hallo-volume dat Hallo bestanden en/of mappen die u wilt dat toorestore bevat.

    Selecteer een herstelpunt op Hallo-kalender. U kunt vanaf elk willekeurig herstelpunt herstellen in de tijd. Datums **vet** Hallo beschikbaarheid van ten minste één herstelpunt aangeven. Wanneer u een datum selecteren als er meerdere herstelpunten beschikbaar zijn, kiest u Hallo specifiek herstelpunt van Hallo **tijd** vervolgkeuzelijst.

    ![Volume en datum](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. Nadat u Hallo herstel punt toorestore hebt gekozen, klikt u op **koppelen**.

    Azure Backup Hallo lokale herstelpunt koppelt en gebruikt als een volume herstel.

7. Op Hallo **bladeren en bestanden herstellen** deelvenster, klikt u op **Bladeren** tooopen Windows Verkenner en zoek Hallo bestanden en mappen die u wilt.

    ![Opties voor herstel](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. In Windows Verkenner, Hallo-bestanden kopiëren en/of mappen wilt toorestore en plak ze tooany locatie toohello lokale server of computer. U kunt openen of stream Hallo-bestanden rechtstreeks vanuit Hallo herstel volume en controleer of Hallo juist versies zijn hersteld.

    ![Kopiëren en plakken van bestanden en mappen van gekoppelde volume toolocal locatie](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. Als u klaar bent herstellen Hallo bestanden en/of mappen op Hallo **bladeren en herstelbestanden** deelvenster, klikt u op **ontkoppelen**. Klik vervolgens op **Ja** tooconfirm dat u wilt dat toounmount Hallo volume.

    ![Hallo volume ontkoppelen en bevestigen](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > Als u niet ontkoppelen op, blijft Hallo herstel Volume gekoppelde gedurende zes uur van Hallo tijd wanneer deze is gekoppeld. Er is geen back-upbewerkingen wordt uitgevoerd tijdens het Hallo-volume is gekoppeld. Een back-upbewerking gepland toorun tijdens Hallo wanneer Hallo volume is gekoppeld, wordt uitgevoerd nadat Hallo herstel volume is ontkoppeld.
    >


## <a name="recover-data-toohello-same-machine"></a>Herstellen van gegevens toohello dezelfde machine
Als u een bestands- en desgewenst toorestore per ongeluk hebt verwijderd deze toohello dezelfde machine (vanaf welke Hallo back-up is gemaakt), Hallo te volgen stappen vindt u een Hallo-gegevens herstellen.

1. Open Hallo **Microsoft Azure Backup** uitlijnen in.
2. Klik op **gegevens herstellen** tooinitiate Hallo werkstroom.

    ![Gegevens herstellen](./media/backup-azure-restore-windows-server-classic/recover.png)
3. Selecteer Hallo  **deze server (*yourmachinename*) ** optie toorestore Hallo een back-up-bestand op Hallo dezelfde machine.

    ![Dezelfde machine](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. Kies te**zoeken naar bestanden** of **zoeken naar bestanden**.

    Laat Hallo standaardoptie als u van plan toorestore bent een of meer bestanden waarvan het pad is bekend. Als u niet zeker van de mapstructuur Hallo bent maar toosearch voor een bestand, kies Hallo **zoeken naar bestanden** optie. Voor Hallo doel van deze sectie gaat we nu verder met de standaardoptie Hallo.

    ![Blader door bestanden](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. Selecteer Hallo volume van waaruit u wilt dat toorestore Hallo-bestand.

    U kunt herstellen vanaf elk punt in tijd. Datums die worden weergegeven in **vet** Hallo kalenderbesturingselement duiden op Hallo beschikbaarheid van een herstelpunt. Nadat een datum is geselecteerd, op basis van uw back-upschema (en het Hallo slagen van een back-upbewerking), kunt u een punt in tijd van Hallo **tijd** vervolgkeuzelijst.

    ![Volume en datum](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. Selecteer Hallo items toorecover. U kunt meerdere mappen/bestanden desgewenst toorestore.

    ![Bestanden selecteren](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. Geef parameters op Hallo herstel.

    ![Opties voor herstel](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * Hebt u een optie van het terugzetten van de oorspronkelijke locatie toohello (in welke Hallo bestand/map zou worden overschreven) of tooanother locatie in Hallo dezelfde machine.
   * Als Hallo bestand/map gewenst toorestore bestaat in de doellocatie hello, kunt u kopieën (twee versies van Hallo hetzelfde bestand), Hallo-bestanden in de doellocatie Hallo overschrijven, of het Hallo-herstel van Hallo-bestanden die aanwezig zijn in Hallo doel overslaan.
   * Het is raadzaam dat u de standaardoptie Hallo Hallo ACL's op Hallo-bestanden die zijn hersteld terugzetten van laat.
8. Zodra deze invoer zijn opgegeven, klikt u op **volgende**. Hallo herstelwerkstroom, die Hallo bestanden toothis machine herstelt, wordt gestart.

## <a name="recover-tooan-alternate-machine"></a>Alternatieve tooan-machine herstellen
Als uw hele server verbroken wordt, kunt u nog steeds gegevens herstellen vanaf de Azure Backup tooa andere machine. Hallo stappen te volgen illustreren Hallo-werkstroom.  

Hallo-terminologie die wordt gebruikt in deze stap omvat het volgende:

* *Bronmachine* : de oorspronkelijke machine Hallo van welke Hallo back-up is gemaakt en die momenteel niet beschikbaar is.
* *Doelcomputer* – Hallo machine toowhich Hallo gegevens worden hersteld.
* *Voorbeeld kluis* – Hallo Backup-kluis toowhich hello *bronmachine* en *doelmachine* zijn geregistreerd. <br/>

> [!NOTE]
> Back-ups die van een virtuele machine kunnen niet worden teruggezet op een computer waarop een eerdere versie van het Hallo-besturingssysteem wordt uitgevoerd. Bijvoorbeeld, als back-ups worden gemaakt van een machine met Windows 7, kan deze worden hersteld op een Windows 8 of hoger machine. Hallo vice versa biedt echter geen houdt true.
>
>

1. Open Hallo **Microsoft Azure Backup** uitlijnen in op Hallo *doelmachine*.
2. Zorg ervoor dat Hallo *doelmachine* en Hallo *bronmachine* geregistreerde toohello zijn dezelfde back-upkluis.
3. Klik op **gegevens herstellen** tooinitiate Hallo werkstroom.

    ![Gegevens herstellen](./media/backup-azure-restore-windows-server-classic/recover.png)
4. Selecteer **een andere server**

    ![Een andere Server](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. Hallo-kluisreferentiebestand die overeenkomt met toohello bieden *voorbeeld kluis*. Als het kluisreferentiebestand Hallo is ongeldig (of verlopen) het downloaden van een nieuw kluisreferentiebestand van Hallo *voorbeeld kluis* in Hallo klassieke Azure-portal. Zodra het Hallo-kluisreferentiebestand is opgegeven, wordt back-upkluis tegen kluisreferentiebestand Hallo Hallo weergegeven.
6. Selecteer Hallo *bronmachine* uit Hallo lijst met computers weergegeven.

    ![Lijst met computers](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. Selecteer beide Hallo **zoeken naar bestanden** of **zoeken naar bestanden** optie. Voor Hallo doel van deze sectie, gebruiken we Hallo **zoeken naar bestanden** optie.

    ![Search](./media/backup-azure-restore-windows-server-classic/search.png)
8. Selecteer Hallo volume en datum in het volgende scherm Hallo. Zoekactie voor de naam van de map/bestand Hallo gewenste toorestore.

    ![Zoeken naar objecten](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. Selecteer Hallo-locatie waar Hallo-bestanden toobe hersteld moeten.

    ![Locatie herstellen](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. Hallo-wachtwoordzin voor versleuteling dat is opgegeven tijdens de bieden *van de bronmachine* registratie te*voorbeeld kluis*.

    ![Versleuteling](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. Zodra het Hallo-invoer is opgegeven, klikt u op **herstellen**, welke triggers Hallo terugzetten van een back-up bestanden toohello bestemming Hallo.

## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a>Direct herstellen toorestore gegevens tooan alternatieve machine gebruiken
Als uw hele server verbroken wordt, kunt u nog steeds gegevens herstellen vanaf de Azure Backup tooa andere machine. Hallo stappen te volgen illustreren Hallo-werkstroom.

Hallo-terminologie die wordt gebruikt in deze stap omvat het volgende:

* *Bronmachine* : de oorspronkelijke machine Hallo van welke Hallo back-up is gemaakt en die momenteel niet beschikbaar is.
* *Doelcomputer* – Hallo machine toowhich Hallo gegevens worden hersteld.
* *Voorbeeld kluis* – Hallo Recovery Services-kluis toowhich hello *bronmachine* en *doelmachine* zijn geregistreerd. <br/>

> [!NOTE]
> Back-ups niet herstelde tooa doelcomputer met een eerdere versie van besturingssysteem Hallo. Bijvoorbeeld, een back-up van een Windows 7 computer kan worden hersteld op een Windows 8 of hoger, computer. Een back-up van een Windows 8-computer niet tooa Windows 7 van de herstelde computer.
>
>

1. Open Hallo **Microsoft Azure Backup** uitlijnen in op Hallo *doelmachine*.

2. Zorg ervoor dat Hallo *doelmachine* en Hallo *bronmachine* zijn geregistreerde toohello dezelfde Recovery Services-kluis.

3. Klik op **gegevens herstellen** tooopen hello **wizard gegevens herstellen**.

    ![Gegevens herstellen](./media/backup-azure-restore-windows-server/recover.png)

4. Op Hallo **aan de slag** deelvenster **een andere server**

    ![Een andere Server](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. Hallo-kluisreferentiebestand die overeenkomt met toohello bieden *voorbeeld kluis*, en klik op **volgende**.

    Als het kluisreferentiebestand Hallo is ongeldig (of verlopen), het downloaden van een nieuw kluisreferentiebestand van Hallo *voorbeeld kluis* in hello Azure-portal. Zodra u de referenties van een geldige kluis opgeeft, wordt de naam Hallo Hallo Backup-kluis overeenkomt weergegeven.

6. Op Hallo **back-up-Server selecteren** deelvenster, selecteer Hallo *bronmachine* uit Hallo lijst met weergegeven machines en Hallo wachtwoordzin opgeven. Klik op **Volgende**.

    ![Lijst met computers](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. Op Hallo **herstelmodus Selecteer** deelvenster Selecteer **afzonderlijke bestanden en mappen** en klik op **volgende**.

    ![Search](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. Op Hallo **Volume selecteert en datum** deelvenster, selecteer Hallo-volume dat Hallo bestanden en/of mappen die u wilt dat toorestore bevat.

    Selecteer een herstelpunt op Hallo-kalender. U kunt vanaf elk willekeurig herstelpunt herstellen in de tijd. Datums **vet** Hallo beschikbaarheid van ten minste één herstelpunt aangeven. Wanneer u een datum selecteren als er meerdere herstelpunten beschikbaar zijn, kiest u Hallo specifiek herstelpunt van Hallo **tijd** vervolgkeuzelijst.

    ![Zoeken naar objecten](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. Klik op **koppelen** toolocally Hallo herstel koppelpunt als een volume herstel op uw *doelmachine*.

10. Op Hallo **bladeren en bestanden herstellen** deelvenster, klikt u op **Bladeren** tooopen Windows Verkenner en zoek Hallo bestanden en mappen die u wilt.

    ![Versleuteling](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. In Windows Verkenner Hallo bestanden en/of mappen van Hallo herstel volume kopiëren en plakken tooyour *doelmachine* locatie. U kunt openen of stream Hallo-bestanden rechtstreeks vanuit Hallo herstel volume en controleer of Hallo juist versies zijn hersteld.

    ![Versleuteling](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. Als u klaar bent herstellen Hallo bestanden en/of mappen op Hallo **bladeren en herstelbestanden** deelvenster, klikt u op **ontkoppelen**. Klik vervolgens op **Ja** tooconfirm dat u wilt dat toounmount Hallo volume.

    ![Versleuteling](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > Als u niet ontkoppelen op, blijft Hallo herstel Volume gekoppelde gedurende zes uur van Hallo tijd wanneer deze is gekoppeld. Er is geen back-upbewerkingen wordt uitgevoerd tijdens het Hallo-volume is gekoppeld. Een back-upbewerking gepland toorun tijdens Hallo wanneer Hallo volume is gekoppeld, wordt uitgevoerd nadat Hallo herstel volume is ontkoppeld.
    >


## <a name="next-steps"></a>Volgende stappen
* [Veelgestelde vragen over Azure Backup](backup-azure-backup-faq.md)
* Ga naar Hallo [Azure back-up-Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933).

## <a name="learn-more"></a>Meer informatie
* [Overzicht van Azure Backup](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [Back-virtuele machines in Azure](backup-azure-vms-introduction.md)
* [Back-up van de werkbelasting van Microsoft](backup-azure-dpm-introduction.md)
