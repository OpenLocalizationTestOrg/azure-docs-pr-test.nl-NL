---
title: aaaRestore gegevens in Azure tooa Windows Server of Windows-computer | Microsoft Docs
description: Meer informatie over hoe toorestore gegevens opgeslagen in Azure tooa Windows Server of Windows-computer.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 11335495e448986a74f1733406f87e04331641d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a>Herstellen van bestanden tooa WindowsServer of Windows client-computer met Resource Manager-implementatiemodel
> [!div class="op_single_selector"]
> * [Azure Portal](backup-azure-restore-windows-server.md)
> * [Klassieke portal](backup-azure-restore-windows-server-classic.md)
>
>

Dit artikel wordt uitgelegd hoe toorestore gegevens uit een back-upkluis. toorestore gegevens, gebruikt u Hallo gegevens herstellen wizard in Hallo Microsoft Azure Recovery Services (MARS)-agent. Wanneer u gegevens herstelt, is het mogelijk om te:

* Terugzetten van gegevens toohello dezelfde machine uit welke Hallo back-ups zijn uitgevoerd.
* Gegevens tooan alternatieve machine herstellen.

Microsoft uitgebracht in januari 2017 een Preview update toohello MARS-agent. Samen met oplossingen voor problemen, deze update kan direct herstellen, zodat u toomount een momentopname van een beschrijfbare herstelpunt als een volume herstel. U kunt vervolgens Hallo herstel volume en kopieert u bestanden tooa lokale computer waardoor selectief terugzetten bestanden verkennen.

> [!NOTE]
> Hallo [januari 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is vereist als u gegevens van toouse toorestore direct herstellen. Back-upgegevens Hallo moeten ook worden beveiligd in kluizen in de landinstellingen die worden vermeld in artikel Hallo-ondersteuning. Raadpleeg Hallo [januari 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) voor de meest recente lijst Hallo van landinstellingen die ondersteuning bieden voor chatberichten te herstellen. Direct herstellen is **niet** momenteel in alle landen beschikbaar.
>

Chatberichten terugzetten is beschikbaar voor gebruik in de Recovery Services-kluizen in hello Azure-portal en Backup-kluizen in de klassieke portal Hallo. Als u toouse direct herstellen wilt, Hallo MARS update downloaden en Hallo procedures volgen die vermeld direct herstellen.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

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
    > Als u niet ontkoppelen op, blijft Hallo herstel Volume gekoppelde gedurende zes uur van Hallo tijd wanneer deze is gekoppeld. Hallo mount-tijd is echter uitgebreide tot aan maximaal 24 uur in het geval van een doorlopende kopiëren van bestanden. Er is geen back-upbewerkingen wordt uitgevoerd tijdens het Hallo-volume is gekoppeld. Een back-upbewerking gepland toorun tijdens Hallo wanneer Hallo volume is gekoppeld, wordt uitgevoerd nadat Hallo herstel volume is ontkoppeld.
    >


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
    > Als u niet ontkoppelen op, blijft Hallo herstel Volume gekoppelde gedurende zes uur van Hallo tijd wanneer deze is gekoppeld. Hallo mount-tijd is echter uitgebreide tot aan maximaal 24 uur in het geval van een doorlopende kopiëren van bestanden. Er is geen back-upbewerkingen wordt uitgevoerd tijdens het Hallo-volume is gekoppeld. Een back-upbewerking gepland toorun tijdens Hallo wanneer Hallo volume is gekoppeld, wordt uitgevoerd nadat Hallo herstel volume is ontkoppeld.
    >

## <a name="troubleshooting"></a>Problemen oplossen
Als Azure Backup Hallo herstel volume niet met succes koppelt zelfs na enkele minuten van het klikken op **koppelen** of mislukt toomount Hallo herstel volume met een of meer fouten Hallo stappen hieronder toobegin normaal herstellen.

1.  Hallo lopende koppelpunt proces annuleren als deze actief is geweest gedurende enkele minuten.

2.  Zorg ervoor dat u zich op de meest recente versie Hallo van hello Azure backup-agent. toofind hello versie-informatie van de Azure Backup-agent, klikt u op **over Microsoft Azure Recovery Services Agent** op Hallo **acties** deelvenster van de Microsoft Azure Backup console en zorg ervoor dat Hallo  **Versie** aantal is gelijk tooor hoger is dan de versie van Hallo vermeld in [in dit artikel](https://go.microsoft.com/fwlink/?linkid=229525). U kunt Hallo nieuwste versie downloaden van [hier](https://go.microsoft.com/fwLink/?LinkID=288905)

3.  Ga te**Apparaatbeheer** -> **opslagcontrollers** en zorg ervoor dat u kunt vinden **Microsoft iSCSI-Initiator**. Als u deze vinden kunt, gaat u rechtstreeks toostep 7 hieronder. 

4.  Als u kunt Microsoft iSCSI Initiator-service niet kunt vinden, zoals vermeld in stap 3, toosee controleren als u een item onder vindt **Apparaatbeheer** -> **opslagcontrollers** aangeroepen  **Onbekend apparaat** met Hardware-ID **ROOT\ISCSIPRT**.

5.  Klik met de rechtermuisknop op **onbekend apparaat** en selecteer **Update stuurprogramma's**.

6.  Hallo-stuurprogramma bijwerken door het Hallo-optie te selecteren **zoeken voor bijgewerkte stuurprogramma's automatisch**. Voltooiing van Hallo update moet worden gewijzigd **onbekend apparaat** te**Microsoft iSCSI-Initiator** zoals hieronder wordt weergegeven. 

    ![Versleuteling](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  Ga te**Taakbeheer** -> **Services (lokaal)** -> **Microsoft iSCSI Initiator-Service**. 

    ![Versleuteling](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  Hallo Microsoft iSCSI Initiator-service opnieuw starten met de rechtermuisknop op het Hallo-service, te klikken op **stoppen** en verdere rechtermuisknop opnieuw te klikken en te klikken op **Start**.

9.  Probeer herstellen met behulp van directe herstellen. 

Als het Hallo-herstel nog steeds mislukt, start opnieuw op uw server /-client. Als een opnieuw opstarten niet wenselijk is of Hallo herstel nog steeds niet zelfs na het Hallo-server opnieuw opstarten, vanaf een andere virtuele Machine en neem contact op met ondersteuning van Azure door te gaan[Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) en een ondersteuningsaanvraag indienen.

## <a name="next-steps"></a>Volgende stappen
* Nu dat u uw bestanden en mappen hebt hersteld, kunt u [beheren van uw back-ups](backup-azure-manage-windows-server.md).
