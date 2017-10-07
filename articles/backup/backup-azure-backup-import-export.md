---
title: back-up - Offline back-ups of het gebruik van eerste seeding aaaAzure hello Azure Import/Export-service | Microsoft Docs
description: Meer informatie over hoe Azure Backup kunt u gegevens toosend Hallo-netwerk met behulp van hello Azure Import/Export-service. Dit artikel wordt uitgelegd Hallo offline seeding van de eerste back-upgegevens Hallo met hello Azure importeren exporteren service.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: ada19c12-3e60-457b-8a6e-cf21b9553b97
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/20/2017
ms.author: saurse;nkolli;trinadhk
ms.openlocfilehash: f1696957c3e9684b800c8d030131255905459f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="offline-backup-workflow-in-azure-backup"></a>Werkstroom voor offline back-ups maken in Azure Backup
Azure Backup heeft diverse ingebouwde efficiency die netwerk- en kosten tijdens Hallo eerste volledige back-ups van gegevens tooAzure besparen. Eerste volledige back-ups brengen grote hoeveelheden gegevens doorgaans en meer netwerkbandbreedte vergelijking toosubsequent back-ups waarbij alleen Hallo delta's / incrementele worden overgedragen. Azure back-up comprimeren Hallo eerste back-ups. Door Hallo proces van het offline seeding kunt Azure Backup schijven tooupload Hallo gecomprimeerd eerste back-upgegevens offline tooAzure.  

Hallo proces offline seeding van Azure Backup is nauw geïntegreerd met Hallo [Azure Import/Export-service](../storage/common/storage-import-export-service.md) waarmee u tootransfer gegevens tooAzure met behulp van schijven. Als u terabyte (TBs) van de eerste back-upgegevens die toobe overgedragen via een netwerk met hoge latentie en een lage bandbreedte nodig hebt, kunt u Hallo offline seeding werkstroom tooship Hallo eerste back-up op een of meer harde schijven tooan Azure-datacenter. Dit artikel bevat een overzicht van stappen Hallo die deze werkstroom worden voltooid.

## <a name="overview"></a>Overzicht
Met Hallo offline seeding mogelijkheden van Azure Backup en Azure Import/Export is het eenvoudig tooupload Hallo gegevens offline tooAzure met behulp van schijven. In plaats van de eerste volledige kopie van de Hallo via Hallo netwerk wordt overgedragen, back-upgegevens Hallo tooa wordt geschreven *faseringslocatie*. Nadat Hallo kopiëren toohello faseringslocatie met hello Azure Import/Export-hulpprogramma is voltooid, kan deze gegevens worden geschreven tooone of meer SATA-schijven, afhankelijk van de hoeveelheid gegevens Hallo. Deze stations zijn uiteindelijk verzonden toohello dichtstbijzijnde Azure-datacenter.

Hallo [augustus 2016 bijwerken van Azure Backup (en hoger)](http://go.microsoft.com/fwlink/?LinkID=229525) Hallo omvat *hulpprogramma voor systeemvoorbereiding van Azure-schijf*, AzureOfflineBackupDiskPrep, met de naam die:

* Helpt bij het voorbereiden van uw schijven van Azure Import via hello Azure Import/Export-hulpprogramma.
* Maakt automatisch een Azure Import-taak voor hello Azure Import/Export-service op Hallo [klassieke Azure-portal](https://manage.windowsazure.com) als tegengestelde toocreating Hallo dezelfde handmatig met oudere versies van Azure Backup.

Nadat het uploaden van Hallo back-upgegevens tooAzure Hallo is voltooid, Azure Backup kopieert Hallo back-upgegevens toohello back-upkluis en Hallo incrementele back-ups zijn gepland.

> [!NOTE]
> toouse Hallo-hulpprogramma voor systeemvoorbereiding van Azure-schijf, zorg ervoor dat u Hallo augustus 2016 update van Azure Backup (of hoger) hebt geïnstalleerd en stappen voor alle Hallo van Hallo werkstroom met het uitvoeren. Als u een oudere versie van Azure Backup gebruikt, kunt u Hallo SATA harde schijf voorbereiden via hello Azure Import/Export zoals beschreven in latere secties van dit artikel.
>
>

## <a name="prerequisites"></a>Vereisten
* [Maak uzelf bekend met hello Azure Import/Export werkstroom](../storage/common/storage-import-export-service.md).
* Voordat het Hallo-werkstroom is gestart, moet u de volgende Hallo:
  * Een Azure Backup-kluis is gemaakt.
  * Referenties voor de kluis zijn gedownload.
  * Hello Azure backup-agent is geïnstalleerd op Windows Server/Windows client- of System Center Data Protection Manager en Hallo-computer is geregistreerd bij hello Azure Backup-kluis.
* [Downloadinstellingen hello Azure publiceren bestand](https://manage.windowsazure.com/publishsettings) op Hallo computer van waaruit u van plan tooback van uw gegevens bent.
* Bereid de faseringslocatie, dit is mogelijk een netwerkshare of een extra schijf op Hallo-computer. Hallo tijdelijke locatie is tijdelijke opslag en tijdelijk tijdens deze werkstroom wordt gebruikt. Zorg ervoor dat Hallo tijdelijke locatie heeft onvoldoende ruimte schijf toohold uw eerste kopie. Bijvoorbeeld, als u tooback van een bestandsserver van 500 GB probeert, zorg ervoor dat faseringsgebied Hallo ten minste 500 GB. (Een lager bedrag wordt gebruikt vanwege toocompression.)
* Zorg ervoor dat u een ondersteunde station. Alleen 2,5 inch SSD of 2.5 of 3.5-inch SATA III-II interne harde schijven worden ondersteund voor gebruik met Hallo Import/Export-service. U kunt harde schijven van too10 TB. Controleer Hallo [documentatie van de service Azure Import/Export](../storage/common/storage-import-export-service.md#hard-disk-drives) voor de meest recente set Hallo schijven die Hallo ondersteunt.
* BitLocker inschakelen op Hallo computer toowhich Hallo SATA station writer is verbonden.
* [Download hello Azure Import/Export hulpprogramma](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409) toohello computer toowhich Hallo SATA station writer is verbonden. Deze stap is niet vereist als u hebt gedownload en geïnstalleerd Hallo augustus 2016 update van Azure Backup (of hoger).

## <a name="workflow"></a>Werkstroom
Hallo-informatie in deze sectie helpt u Hallo offline back-up-werkstroom voltooien, zodat uw gegevens kunt tooan Azure-datacenter worden geleverd en tooAzure opslag geüpload. Als u vragen over importservice hello of een aspect van Hallo proces hebt, raadpleegt u Hallo [importeren Serviceoverzicht](../storage/common/storage-import-export-service.md) documentatie waarnaar wordt verwezen eerder.

### <a name="initiate-offline-backup"></a>Offline back-up starten
1. Als u een back-up plannen, ziet u Hallo scherm (in Windows Server, Windows-client of System Center Data Protection Manager) te volgen.

    ![Scherm importeren](./media/backup-azure-backup-import-export/offlineBackupscreenInputs.png)

    Hier volgt bijbehorende welkomstscherm in System Center Data Protection Manager: <br/>
    ![DPM-importscherm](./media/backup-azure-backup-import-export/dpmoffline.png)

    Beschrijving van de invoerwaarden Hallo Hallo is als volgt:

    * **Tijdelijke locatie**: Hallo tijdelijke opslag locatie toowhich Hallo eerste back-up is geschreven. Dit kan zijn op een netwerkshare of een lokale computer. Als Hallo kopie computer en de broncomputer verschillend zijn, kunt u het aangeraden Hallo volledig netwerkpad Hallo tijdelijke locatie op te geven.
    * **Azure Import-taaknaam**: Hallo unieke naam op welke Azure Import-service en Azure Backup Hallo overdracht van gegevens die worden verzonden op schijven tooAzure bijhouden.
    * **Azure Publish Settings**: een XML-bestand dat informatie over het profiel van uw abonnement bevat. Het bevat ook beveiligde referenties die gekoppeld aan uw abonnement zijn. U kunt [Hallo-bestand downloaden](https://manage.windowsazure.com/publishsettings). Geef Hallo lokaal pad toohello bestand publicatie-instellingen.
    * **Azure-abonnements-ID**: hello Azure-abonnement-ID voor Hallo abonnement waarbij u van plan tooinitiate hello Azure Import-taak bent. Als u meerdere Azure-abonnementen hebt, gebruikt u Hallo-ID van Hallo-abonnement dat u wilt dat tooassociate met Hallo import-taak.
    * **Azure Storage-Account**: Hallo klassieke type opslagaccount in Hallo opgegeven Azure-abonnement gekoppeld aan hello Azure Import-taak worden.
    * **Azure Storage-Container**: Hallo-naam van Hallo bestemmings-blob voor opslag in hello Azure storage-account waarin gegevens van deze taak worden geïmporteerd.

    > [!NOTE]
    > Als u uw server tooan geregistreerd Azure Recovery Services-kluis van Hallo [Azure-portal](https://portal.azure.com) voor uw back-ups en zich niet op een abonnement Cloud Solution Provider (CSP) u kunt nog steeds een klassieke type opslagaccount maken van Hallo Azure-portal en deze gebruiken voor Hallo offline back-up-werkstroom.
    >
    >

     Al deze gegevens worden opgeslagen omdat u tooenter moet deze opnieuw in de volgende stappen. Alleen Hallo *faseringslocatie* is vereist als u hello Azure schijfvoorbereiding hulpprogramma tooprepare Hallo schijven gebruikt.    
2. Hallo werkstroom voltooien en selecteer vervolgens **Back-Up uit** in hello Azure Backup management console tooinitiate Hallo offline back-up-exemplaar. de eerste back-up Hallo geschreven toohello faseringsgebied als onderdeel van deze stap.

    ![Nu reservekopie maken](./media/backup-azure-backup-import-export/backupnow.png)

    toocomplete hello bijbehorende werkstroom in System Center Data Protection Manager, met de rechtermuisknop op Hallo **beveiligingsgroep**, en kies vervolgens Hallo **herstelpunt maken** optie. Kies vervolgens Hallo **Onlinebeveiliging** optie.

    ![DPM back-up nu](./media/backup-azure-backup-import-export/dpmbackupnow.png)

    Nadat het Hallo-bewerking is voltooid, is Hallo faseringslocatie gereed toobe gebruikt voor de schijfvoorbereiding van de.

    ![Voortgang van de back-up](./media/backup-azure-backup-import-export/opbackupnow.png)

### <a name="prepare-a-sata-drive-and-create-an-azure-import-job-by-using-hello-azure-disk-preparation-tool"></a>Bereid een SATA harde schijf en Azure Import-taak maken met behulp van Hallo-hulpprogramma voor systeemvoorbereiding van Azure-schijf
Hallo-hulpprogramma voor systeemvoorbereiding van Azure-schijf is beschikbaar in de installatiemap van Hallo Recovery Services-agent (augustus 2016 bijwerken en hoger) in pad Hallo.

   *\Microsoft* *azure* *herstel* *Services* * Agent\Utils\*

1. Ga toohello directory en de kopie Hallo **AzureOfflineBackupDiskPrep** directory tooa kopie-computers op welke Hallo stations toobe voorbereid zijn gekoppeld. Zorg ervoor dat Hallo volgende inachtneming toohello kopie computer:

    * Hallo kopiëren computer kunt toegang krijgen tot tijdelijke locatie voor Hallo offline seeding werkstroom met behulp van dezelfde netwerkpad die is opgegeven in Hallo HALLO hallo **offline back-up starten** werkstroom.
    * BitLocker is ingeschakeld op Hallo-computer.
    * Hallo-computer, hebben toegang tot hello Azure-portal.

    Indien nodig kunt Hallo kopie computer hetzelfde als de broncomputer Hallo worden Hallo.
2. Open een opdrachtprompt met verhoogde bevoegdheid op Hallo kopie computer met hello Azure schijfvoorbereiding hulpprogramma directory als de huidige map Hallo en Voer Hallo volgende opdracht uit:

    `*.\AzureOfflineBackupDiskPrep.exe*   s:<*Staging Location Path*>   [p:<*Path tooPublishSettingsFile*>]`

    | Parameter | Beschrijving |
    | --- | --- |
    | s:&lt;*locatiepad fasering*&gt; |Verplichte invoer die is gebruikt tooprovide Hallo pad toohello tijdelijke locatie die u hebt ingevoerd in Hallo **offline back-up starten** werkstroom. |
    | p:&lt;*pad tooPublishSettingsFile*&gt; |Optionele invoer die is gebruikt tooprovide Hallo pad toohello **Azure Publish Settings** -bestand dat u hebt ingevoerd in Hallo **offline back-up starten** werkstroom. |

    > [!NOTE]
    > Hallo &lt;pad tooPublishSettingFile&gt; waarde is verplicht wanneer Hallo kopie computer en de broncomputer verschillen.
    >
    >

    Als u Hallo-opdracht uitvoert, vraagt Hallo hulpprogramma Hallo selectie van hello Azure Import-taak die overeenkomt met toohello stations die toobe voorbereid moeten. Als er slechts een enkele import-taak gekoppeld aan de opgegeven faseringslocatie hello is, ziet u een scherm zoals Hallo een die volgt.

    ![Azure schijfvoorbereiding hulpprogramma invoer](./media/backup-azure-backup-import-export/azureDiskPreparationToolDriveInput.png) <br/>
3. Voer Hallo stationsletter zonder volgspaties dubbele punt voor de gekoppelde schijf hello wilt u tooprepare voor overdracht tooAzure Hallo. Geeft u de bevestiging voor Hallo opmaak van Hallo station wanneer u wordt gevraagd.

    Hallo hulpprogramma begint vervolgens tooprepare Hallo schijf met de Hallo back-upgegevens. U moet mogelijk extra schijven tooattach wanneer u wordt gevraagd door Hallo hulpprogramma geval Hallo voorwaarde schijf niet voldoende ruimte voor back-upgegevens Hallo. <br/>

    Een of meer schijven die u hebt opgegeven zijn Hallo na voltooiing van uitvoering van Hallo hulpprogramma voorbereid voor back-upfunctie voor tooAzure. Bovendien een import-taak met de naam van de Hallo u hebt opgegeven tijdens Hallo **offline back-up starten** werkstroom op Hallo klassieke Azure-portal is gemaakt. Ten slotte Hallo hulpprogramma geeft Hallo back-upfunctie adres toohello Azure-datacenter waar Hallo schijven toobe verzonden moeten en Hallo koppeling toolocate Hallo import-taak op Hallo klassieke Azure-portal.

    ![De voorbereiding van de Azure-schijf is voltooid](./media/backup-azure-backup-import-export/azureDiskPreparationToolSuccess.png)<br/>

4. Verzend Hallo schijven toohello dat Hallo hulpprogramma opgegeven adres en houden Hallo volgnummer voor toekomstig gebruik.<br/>

5. Wanneer u gaat toohello koppelen dat Hallo hulpprogramma weergegeven, ziet u hello Azure storage-account die u hebt opgegeven in Hallo **offline back-up starten** werkstroom. Hier ziet u de importtaak Hallo nieuw gemaakt op Hallo **voor importeren/EXPORTEREN** tabblad van het Hallo-opslagaccount.

    ![Gemaakte import-taak](./media/backup-azure-backup-import-export/ImportJobCreated.png)<br/>

6. Klik op **back-UPFUNCTIE INFO** Hallo Hallo pagina tooupdate onderaan in uw contactpersoon details, zoals weergegeven in het volgende scherm Hallo. Microsoft gebruikt deze gegevens tooship uw vorige tooyou schijven nadat Hallo taak importeren is voltooid.

    ![Contactgegevens](./media/backup-azure-backup-import-export/contactInfoAddition.PNG)<br/>

7. Geef details van de back-upfunctie in het volgende scherm Hallo Hallo. Hallo bieden **levering Carrier** en **volgnummer** details die overeenkomen met toohello schijven dat u Azure-datacenter toohello verzonden.

    ![Back-ups van gegevens](./media/backup-azure-backup-import-export/shippingInfoAddition.PNG)<br/>

### <a name="complete-hello-workflow"></a>Volledige Hallo-werkstroom
Hallo import-taak is voltooid, is eerste back-upgegevens beschikbaar in uw opslagaccount. Hallo Recovery Services-agent vervolgens Hallo de inhoud van het Hallo-gegevens van dit account toohello Backup-kluis of een Recovery Services-kluis, afhankelijk van wat van toepassing is. In de volgende gepland Hallo back-tijd voert hello Azure Backup agent Hallo incrementele back-up via Hallo eerste back-up.

> [!NOTE]
> Hallo toepassing volgende secties toousers van eerdere versies van Azure Backup die geen toegang tot toohello Azure schijfvoorbereiding hulpprogramma.
>
>

### <a name="prepare-a-sata-drive"></a>Een SATA-station voorbereiden
1. Hallo downloaden [Microsoft Azure-hulpprogramma voor importeren/exporteren](http://go.microsoft.com/fwlink/?linkid=301900&clcid=0x409) toohello kopie-computer. Zorg ervoor dat Hallo tijdelijke locatie toegankelijk is vanaf Hallo computer waarin u van plan toorun Hallo volgende reeks opdrachten bent. Indien nodig kunt Hallo kopie computer hetzelfde als de broncomputer Hallo worden Hallo.

2. Hallo WAImportExport.zip bestand uitpakken. Hallo WAImportExport hulpprogramma die Hallo SATA harde schijf wordt geformatteerd en versleutelt Hallo back-upgegevens toohello SATA harde schijf schrijft uitvoeren. Voordat u de volgende opdracht Hallo uitvoert, zorg ervoor dat BitLocker is ingeschakeld op Hallo-computer. <br/>

    `*.\WAImportExport.exe PrepImport /j:<*JournalFile*>.jrn /id: <*SessionId*> /sk:<*StorageAccountKey*> /BlobType:**PageBlob** /t:<*TargetDriveLetter*> /format /encrypt /srcdir:<*staging location*> /dstdir: <*DestinationBlobVirtualDirectory*>/*`

    > [!NOTE]
    > Als u Hallo augustus 2016 update van Azure Backup (of hoger) hebt geïnstalleerd, zorg ervoor dat Hallo tijdelijke locatie die u hebt ingevoerd is hetzelfde als één op Hallo HALLO hallo **Back-Up uit** scherm en AIB en Base Blob bestanden bevat.
    >
    >

| Parameter | Beschrijving |
| --- | --- |
| /j: <*JournalFile*> |Hallo pad toohello journal-bestand. Elk station moet precies één journaalbestand hebben. Hallo journaal-bestand moet niet op het Hallo-doelstation. Hallo journaal bestandsextensie .jrn is en wordt gemaakt als onderdeel van deze opdracht uit te voeren. |
| /ID: <*sessie-id*> |sessie-ID Hallo identificeert een kopieersessie. Het is gebruikte tooensure nauwkeurige herstel van een sessie onderbroken exemplaar. Bestanden die zijn gekopieerd in een kopieersessie worden opgeslagen in een map met de naam van sessie-ID op het doelstation Hallo Hallo. |
| /SK: <*StorageAccountKey*> |Hallo-toegangssleutel voor Hallo storage account toowhich Hallo-gegevens worden geïmporteerd. Hallo basisbehoeften toobe hello dezelfde manier als tijdens het maken van back-beleid/beveiligingsgroep is ingevoerd. |
| / BlobType |Hallo-type van de blob. Deze werkstroom slaagt alleen als **PageBlob** is opgegeven. Dit is geen Hallo standaardoptie en moet het worden vermeld in deze opdracht. |
| / t: <*TargetDriveLetter*> |Hallo stationsletter zonder volgspaties dubbele punt van Hallo doel harde schijf voor het huidige exemplaar sessie Hallo Hallo. |
| / Format |Hallo optie tooformat Hallo station. Geef deze parameter als Hallo station toobe geformatteerd moet. anders weglaten. Voordat Hallo hulpprogramma Hallo station indelingen verzocht een bevestiging van Hallo-console. toosuppress Hallo bevestiging Hallo /silentmode parameter opgeven. |
| / versleutelen |Hallo optie tooencrypt Hallo station. Deze parameter opgeven wanneer Hallo station nog niet zijn versleuteld met BitLocker en behoeften toobe versleuteld door Hallo-hulpprogramma. Hallo station al is versleuteld met BitLocker, deze parameter, Hallo /bk parameter opgeven als Hallo bestaande BitLocker-sleutel opgeven. Als u Hallo/Format parameter opgeeft, moet u ook opgeven Hallo / versleutelen van parameter. |
| /srcdir: <*SourceDirectory*> |Hallo-bronmap met bestanden toobe toohello doelstation gekopieerd. Zorg ervoor dat Hallo opgegeven mapnaam is een volledige in plaats van relatieve pad. |
| /dstdir: <*DestinationBlobVirtualDirectory*> |Hallo pad toohello bestemming virtuele map in uw Azure storage-account. Niet zeker toouse geldig containernamen wanneer u Hallo doel-virtuele mappen of blobs opgeeft. Houd er rekening mee dat de namen van containers in kleine letters moeten zijn.  De containernaam van deze moet Hallo die u hebt opgegeven tijdens het maken van back-beleid en/of beveiligingsgroep. |

> [!NOTE]
> Een journal-bestand is gemaakt in Hallo WAImportExport map waarmee volledige gegevens van de werkstroom Hallo Hallo worden vastgelegd. U moet dit bestand als u een import-taak in hello Azure-portal maken.
>
>

  ![PowerShell-resultaat](./media/backup-azure-backup-import-export/psoutput.png)

### <a name="create-an-import-job-in-hello-azure-portal"></a>Maken van een import-taak in hello Azure-portal
1. Ga tooyour storage-account in Hallo [klassieke Azure-portal](https://manage.windowsazure.com/), klikt u op **voor importeren/exporteren**, en vervolgens **Import-taak maken** in het taakvenster Hallo.

    ![Tabblad in hello Azure-portal voor importeren/exporteren](./media/backup-azure-backup-import-export/azureportal.png)

2. In stap 1 van de wizard Hallo aangeven dat u de schijf hebt voorbereid en u Hallo station journaal-bestand beschikbaar hebt.

3. In stap 2 van de wizard Hallo contactgegevens voor Hallo persoon die verantwoordelijk voor deze import-taak is te bevatten.

4. In stap 3 Hallo station journaal bestanden uploaden die u hebt verkregen in de vorige sectie Hallo.

5. Voer een beschrijvende naam voor Hallo import-taak die u hebt opgegeven tijdens het maken van back-beleid/beveiligingsgroep in stap 4. Hallo-naam die u invoert mogen alleen kleine letters, cijfers, afbreekstreepjes en onderstrepingstekens bevatten, moet beginnen met een letter en mag geen spaties bevatten. Hallo-naam die u gebruikte tootrack is uw taken kiest terwijl ze zijn uitgevoerd en nadat ze zijn voltooid.

6. Selecteer vervolgens de regio van uw datacenter in Hallo-lijst. Hallo datacenter regio geeft Hallo-toowhich datacenter en het adres van uw pakket moet worden verzonden.

    ![Selecteer de regio van het datacenter](./media/backup-azure-backup-import-export/dc.png)

7. In stap 5, selecteer het geretourneerde telecombedrijf uit Hallo lijst en voer het nummer van uw carrier-account. Microsoft gebruikt deze account tooship stations back tooyou nadat de import-taak is voltooid.

8. Verzend Hallo schijf en Voer Hallo nummer tootrack Hallo status van de verzending Hallo bijhouden. Nadat het Hallo-schijf in Hallo datacenter ontvangt, is het opslagaccount toohello gekopieerd en Hallo status is bijgewerkt.

    ![Voltooide status](./media/backup-azure-backup-import-export/complete.png)

### <a name="complete-hello-workflow"></a>Volledige Hallo-werkstroom
Nadat de eerste back-upgegevens Hallo beschikbaar in uw opslagaccount hello Microsoft Azure Recovery Services agent Hallo inhoud van Hallo gegevens gekopieerd van dit account toohello Backup-kluis of een Recovery Services-kluis is, is afhankelijk van wat van toepassing. In de volgende planning Hallo voert back-uptijd, hello Azure Backup agent Hallo incrementele back-up via Hallo eerste back-up.

## <a name="next-steps"></a>Volgende stappen
* Raadpleeg te voor vragen over de Azure Import/Export-werkstroom hello,[Hallo Microsoft Azure Import/Export-service tootransfer gegevens tooBlob opslag gebruiken](../storage/common/storage-import-export-service.md).
* Raadpleeg de sectie van de toohello offline back-up van hello Azure Backup [Veelgestelde vragen over](backup-azure-backup-faq.md) voor vragen over Hallo-werkstroom.
