---
title: Azure Backup-Server v2 aaaInstall | Microsoft Docs
description: Azure back-upserver v2 biedt verbeterde back-mogelijkheden voor het beveiligen van virtuele machines, bestanden en mappen en werkbelastingen. Meer informatie over hoe tooAzure tooinstall of upgrade van de back-upserver van v2.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a>V2 voor Azure Backup-Server installeren

Azure Backup-Server beveiligt uw virtuele machines (VM's), werkbelastingen, bestanden en mappen en meer. Azure back-upserver van v2 bouwt voort op Azure Backup-Server v1- en biedt u de nieuwe functies die niet beschikbaar in v1. Zie voor een vergelijking van functies tussen v1- en v2 [Azure Backup-Server protection matrix](backup-mabs-protection-matrix.md). 

Hallo aanvullende functies in de back-upserver van v2 zijn een upgrade van de back-upserver van v1. Back-upserver van v1 is echter niet vereist voor de installatie van de back-upserver van v2. Als u tooupgrade van back-upserver van v1 tooBackup Server v2, installeert u de back-upserver van v2 op Hallo back-upserver protection-server. Uw bestaande back-upserver instellingen blijven behouden.

U kunt back-upserver van v2 installeren op Windows Server 2012 R2 of Windows Server 2016. tootake profiteren van nieuwe functies, zoals System Center 2016 Data Protection Manager moderne back-up opslag, moet u back-upserver van v2 installeren op Windows Server 2016. Vóór de upgrade van tooor installeren back-upserver van v2 lezen over Hallo [installatievereisten](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).

> [!NOTE]
> Azure Backup-Server heeft Hallo dezelfde codebasis als System Center Data Protection Manager. Back-Server v1 gelijkwaardige tooData Protection Manager 2012 R2 is en back-upserver van v2 gelijkwaardige tooData Protection Manager 2016. In dit artikel wordt soms verwijst naar Hallo Data Protection Manager-documentatie.
>
>

## <a name="upgrade-backup-server-toov2"></a>Back-upserver toov2 upgraden
tooupgrade van back-upserver van v1 tooBackup Server v2, Controleer of de installatie heeft Hallo vereiste updates:

- [Bijwerken van beveiligingsagents Hallo](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) op Hallo beveiligde servers.
- Windows Server 2012 R2 tooWindows Server 2016 upgraden.
- Azure Backup-serverbeheerder voor extern bijwerken op alle productieservers.
- Zorg ervoor dat de back-ups toocontinue zonder opnieuw opstarten van de productieserver zijn ingesteld.


### <a name="upgrade-steps-for-backup-server-v2"></a>Stappen voor de upgrade voor back-upserver van v2

1. In Hallo Download Center [Hallo upgrade installatieprogramma downloaden](https://go.microsoft.com/fwlink/?LinkId=626082).

2. Nadat u de wizard setup Hallo hebt uitgepakt, zorg ervoor dat **setup.exe uitvoeren** is geselecteerd en selecteer vervolgens **voltooien**.

  ![Installatieprogramma van de Setup - setup uitvoeren](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. In de wizard back-upserver van Microsoft Azure Hallo onder **installeren**, selecteer **Microsoft Azure Backup-Server**.

  ![Installatieprogramma van de Setup - Selecteer installeren](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. Op Hallo **Welkom** pagina, Hallo waarschuwingen bekijken en selecteer vervolgens **volgende**.

  ![Installatieprogramma van de Setup - welkomstpagina](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. Hallo-installatiewizard voert controles van vereisten toomake ervoor dat uw omgeving een upgrade kunt uitvoeren. Op Hallo **vereiste controleert** pagina **controleren**.

  ![Installatieprogramma van de Setup - vereisten controleert pagina](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. De vereiste controles Hallo moet voldoen aan uw omgeving. Als uw omgeving niet Hallo controles slaagt, houd er rekening mee Hallo problemen en los ze. Selecteer **opnieuw controleren**. Nadat u de vereiste controles Hallo doorgeven, selecteert u **volgende**.

  ![Installatieprogramma van de Setup - opnieuw controleren](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. Op Hallo **SQL-instellingen** pagina, selecteert u de relevante optie Hallo voor uw installatie van SQL en selecteer vervolgens **controleren en installeren**.

  ![Installatieprogramma van de Setup - pagina van de SQL-instellingen](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  Hallo controles kunnen enkele minuten duren. Wanneer Hallo controles zijn voltooid, selecteer **volgende**.

  ![Installatieprogramma van de Setup - SQL-instellingen controleren en knop installeren](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. Op Hallo **installatie-instellingen** eventuele wijzigingen toohello locatie waar back-up-Server is geïnstalleerd of toohello scratchruimte locatie maken. Selecteer **volgende**.

  ![Installatieprogramma van de Setup - pagina installatie-instellingen](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. toofinish hello setup wizard selecteert u **voltooien**.

  ![Installatieprogramma van de Setup - voltooien](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a>Opslag toevoegen voor moderne back-up-opslag

back-upserver v2-efficiëntie back-upopslag tooimprove voegt ondersteuning toe voor volumes. Zoals back-upserver van v1 ondersteunt v2 back-upserver schijven.

### <a name="add-volumes-and-disks"></a>Volumes en schijven toevoegen
Als u back-upserver v2 op Windows Server 2016 uitvoert, kunt u volumes toostore back-upgegevens. Volumes bieden opslagbesparing en snellere back-ups. Omdat volumes nieuwe tooBackup Server, moet u ze toevoegen. 

Wanneer u een volume tooBackup Server toevoegt, kunt u Hallo volume een beschrijvende naam geven. Klik op Hallo **beschrijvende naam** kolom Hallo volume dat u wilt dat tooname. U kunt Hallo naam later, indien nodig wijzigen. U kunt ook gebruik van PowerShell tooadd of beschrijvende namen voor volumes wijzigen.

tooadd een volume in Hallo Administrator-Console:

1. Selecteer in hello Azure back-up Server Administrator-Console, **Management** > **schijfopslag** > **toevoegen**.

    ![Open Hallo schijfopslag toevoegen-wizard](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    Hiermee opent u Hallo schijfopslag toevoegen-wizard.

2. Op Hallo **schijfopslag toevoegen** pagina in Hallo **beschikbare volumes** vak en selecteer vervolgens selecteert u een volume **toevoegen**.
3. In Hallo **volumes geselecteerd** vak en selecteer vervolgens een beschrijvende naam voor Hallo volume **OK**.

      ![Schijfopslag wizard Add - volume toevoegen](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  Desgewenst kunt u een schijf tooadd behoren Hallo schijf tooa beveiligingsgroep met de oude opslag. Deze schijven kunnen alleen worden gebruikt voor deze beveiligingsgroepen. Als back-upserver geen bronnen die oudere beveiliging, wordt niet Hallo schijf weergegeven.

  Zie voor meer informatie over het toevoegen van schijven [toe te voegen schijven tooincrease oude opslag](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage). U kan een schijf een beschrijvende naam geven.


### <a name="assign-workloads-toovolumes"></a>Werkbelastingen toovolumes toewijzen

Back-up-server kunt u opgeven welke workloads toowhich volumes zijn toegewezen. U kunt bijvoorbeeld dure volumes die ondersteuning bieden voor een groot aantal i/o-bewerkingen per tweede (IOPS) toostore alleen werkbelastingen waarvoor frequente, hoog volume back-ups instellen. Een voorbeeld is SQL Server met de transactielogboeken.

#### <a name="update-dpmdiskstorage"></a>Update DPMDiskStorage

tooupdate hello eigenschappen van een volume in de opslaggroep Hallo in back-upserver Hallo PowerShell-cmdlet Update-DPMDiskStorage gebruiken.

Syntaxis:

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

Alle wijzigingen die u maakt met behulp van PowerShell worden doorgevoerd in Hallo gebruikersinterface.


## <a name="protect-data-sources"></a>Gegevensbronnen beveiligen
toobegin het beschermen van de gegevensbronnen, maakt een beveiligingsgroep. Hallo stappen markeren wijzigingen of toevoegingen toohello wizard nieuwe beveiligingsgroep te volgen.

toocreate een beveiligingsgroep:

1. Selecteer in de beheerdersconsole van back-up Server Hallo, **beveiliging**.

2. Selecteer op het lint Hallo **nieuw**.

    Hiermee opent u de wizard voor Hallo nieuwe beveiligingsgroep maken.

  ![Wizard nieuwe beveiligingsgroep maken](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. Op Hallo **Welkom** pagina **volgende**.
4. Op Hallo **Type beveiligingsgroep selecteren** pagina, selecteert u Hallo type beveiligingsgroep die u wilt toocreate en selecteer vervolgens **volgende**.

  ![De pagina Type beveiligingsgroep selecteren](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. Op Hallo **groepsleden selecteren** pagina in Hallo **beschikbare leden** deelvenster, Hallo leden met protection agents worden weergegeven. Bijvoorbeeld, selecteert u volume D:\ en E:\ en voeg ze toohello **leden geselecteerd** deelvenster. Selecteer **volgende**.

  ![De pagina leden groep selecteren](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. Op Hallo **methode voor gegevensbeveiliging selecteren** pagina, voert u een **naam beveiligingsgroep**, selecteer de beveiligingsmethode Hallo en selecteer vervolgens **volgende**. Als u beveiliging op korte termijn wilt, moet u Hallo **schijf** back-up van methode.

  ![De pagina methode voor gegevensbeveiliging selecteren](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. Op Hallo **Kortetermijndoelen opgeven** pagina, selecteer Hallo details voor **bewaartermijn** en **Synchronisatiefrequentie**. Selecteer **volgende**. Eventueel toochange Hallo planning voor wanneer herstelpunten genomen, selecteer zijn **wijzigen**.

  ![Pagina Kortetermijndoelen opgeven](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. Op Hallo **toewijzing van schijfopslag controleren** pagina bekijkt u meer informatie over het Hallo-gegevensbronnen die u hebt geselecteerd, hun grootte en de waarden voor Hallo ruimte toobe ingericht en Hallo doel opslagvolume.

  ![Pagina van de toewijzing van schijfopslag controleren](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  Opslagvolumes zijn gebaseerd op Hallo werkbelasting volume toewijzing (ingesteld met behulp van PowerShell) en Hallo beschikbare opslag. U kunt Hallo opslagvolumes wijzigen door het selecteren van andere volumes in de vervolgkeuzelijst Hallo. Als u de waarde voor Hallo wijzigt **Doelopslag**, Hallo waarde voor **beschikbaar schijfopslag** dynamisch gewijzigd tooreflect waarden onder **vrije ruimte** en **Underprovisioned ruimte**.

  Als gegevensbronnen Hallo toenemen als gepland, de waarde voor Hallo Hallo **Underprovisioned ruimte** kolom in **beschikbaar schijfopslag** weerspiegelt Hallo hoeveelheid extra opslagruimte die nodig is. Gebruik deze waarde toohelp plan uw opslag nodig voor goede back-ups. Als het Hallo-waarde nul is, moet u er geen mogelijke problemen met opslag in de nabije toekomst Hallo zijn. Als Hallo een getal dan nul is, u hoeft niet voldoende opslag die is toegewezen (op basis van uw beveiliging beleid en Hallo gegevensgrootte van uw beveiligde leden).

  ![Onderbezette schijfopslag](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   toofinish maken van de wizard beveiligingsgroep groeperen en volledige Hallo.

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a>Verouderde opslag tooModern back-up opslag migreren
Na de upgrade tooor installeren back-upserver van v2 en upgrade Hallo besturingssysteem tooWindows Server 2016, werk uw beveiliging groepen toouse moderne back-up-opslag. Standaard zijn beveiligingsgroepen niet gewijzigd. Ze blijven toofunction als ze in eerste instantie zijn ingesteld. 

Bijwerken van beveiliging groepen toouse moderne back-up-opslag is optioneel. beveiligingsgroep tooupdate hello, stop de beveiliging van alle gegevensbronnen met behulp van Hallo behouden gegevensoptie. Vervolgens voegt u Hallo gegevensbronnen tooa nieuwe beveiligingsgroep.

1. Selecteer in de Hallo Administrator-Console, Hallo **beveiliging** functie. In Hallo **Beveiligingsgroepslid** lijst en selecteer vervolgens met de rechtermuisknop op Hallo lid **beveiliging van lid stoppen**.

  ![Beveiliging van lid stoppen](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. In Hallo **verwijderen uit groep** in het dialoogvenster, bekijk Hallo gebruikt schijfruimte vrij en Hallo beschikbare vrije ruimte voor Hallo-opslaggroep. Hallo standaard tooleave Hallo herstelpunten op schijf Hallo is en dat deze tooexpire per hun bijbehorende bewaarbeleid. Klik op **OK**.

  Als u tooimmediately return Hallo gebruikt ruimte toohello gratis schijfopslaggroep wilt, selecteert u Hallo **replica op schijf verwijderen** selectievakje toodelete Hallo back-upgegevens (en herstelpunten) die zijn gekoppeld aan dit lid.

  ![Dialoogvenster groep verwijderen](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. Maak een beveiligingsgroep die gebruik maakt van opslag voor moderne back-up. Hallo onbeveiligd gegevensbronnen bevatten.


## <a name="add-disks-tooincrease-legacy-storage"></a>Schijven tooincrease oude opslag toevoegen

Als u oude opslag met back-upserver toouse wilt, moet u mogelijk tooadd schijven tooincrease oude opslag. 

schijfopslag tooadd:

1. Selecteer in de Hallo Administrator-Console, **Management** > **schijfopslag** > **toevoegen**.

    ![Schijfopslag dialoogvenster toevoegen](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. In Hallo **schijfopslag toevoegen** dialoogvenster Selecteer **schijven toevoegen**.

5. Selecteer in Hallo lijst met beschikbare schijven Hallo schijven die u wilt dat tooadd, selecteer **toevoegen**, en selecteer vervolgens **OK**.

## <a name="update-hello-data-protection-manager-protection-agent"></a>Hallo Data Protection Manager protection agent bijwerken

Back-upserver maakt gebruik van System Center Data Protection Manager-beveiligingsagent Hallo voor updates. Als u een beveiligingsagent dat geen netwerk verbonden toohello bijwerkt, kunt u Hallo toocomplete Data Protection Manager Administrator-Console de upgrade van een verbonden agent niet gebruiken. De beveiligingsagent Hallo in een niet-actieve domeinomgeving, moet u upgraden. Tot Hallo-clientcomputer verbonden toohello netwerk is, is Hallo die Data Protection Manager Administrator-Console ziet u dat Hallo update van de beveiligingsagent in behandeling.

Hallo volgende secties wordt beschreven hoe de beveiligingsagents tooupdate voor clientcomputers die zijn verbonden en clientcomputers die niet zijn verbonden.

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a>Een beveiligingsagent voor een verbonden clientcomputer bijwerken

1. Selecteer in de beheerdersconsole van back-up Server Hallo, **Management** > **Agents**.

2. Selecteer in weergavepaneel Hallo Hallo clientcomputers waarvoor u tooupdate Hallo-beveiligingsagent wilt.

  > [!NOTE]
  > Hallo **agentupdates** kolom wordt aangegeven wanneer een update van de beveiligingsagent beschikbaar is voor elke beveiligde computer. In Hallo **acties** deelvenster, Hallo **Update** actie is alleen beschikbaar wanneer een beveiligde computer is geselecteerd en er updates beschikbaar zijn.
  >
  >

3. tooinstall bijgewerkt beveiligingsagents op geselecteerde Hallo-computers in Hallo **acties** deelvenster **Update**.

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a>Een beveiligingsagent op een clientcomputer die niet verbonden bijwerken

1. Selecteer in de beheerdersconsole van back-up Server Hallo, **Management** > **Agents**.

2. Selecteer in weergavepaneel Hallo Hallo clientcomputers waarvoor u tooupdate Hallo-beveiligingsagent wilt.

  > [!NOTE]
   > Hallo **agentupdates** kolom wordt aangegeven wanneer een update van de beveiligingsagent beschikbaar is voor elke beveiligde computer. In Hallo **acties** deelvenster, Hallo **Update** actie is niet beschikbaar wanneer een beveiligde computer is geselecteerd tenzij er updates beschikbaar zijn.
  >
  >

3. tooinstall bijgewerkt beveiligingsagents op computers met Hallo geselecteerd, selecteer **Update**.

4. Voor een clientcomputer die niet netwerk toohello, verbonden totdat het Hallo-computer is verbonden toohello netwerk, Hallo **agentstatus** kolom ziet u de status van **Update in behandeling**.

  Nadat een clientcomputer verbonden toohello netwerk is, Hallo **agentupdates** kolom voor de clientcomputer Hallo ziet u de status van **Updating**.
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a>Verouderde beveiligingsgroepen van oude en nieuwe versie van synchronisatie Hallo met Azure verplaatsen

Wanneer zowel Azure Backup-Server en Hallo OS worden bijgewerkt, bent u klaar tooprotect nieuwe gegevensbronnen moderne back-up-opslag. Echter al beveiligde gegevensbronnen blijft toobe beveiligd in de verouderde Hallo manier zoals ze in Azure Backup-Server waren maar alle nieuwe bescherming moderne back-up-opslag gebruikt.

Onderstaande stappen zijn toomigrate gegevensbronnen van de legacy-modus van beveiliging tooModern back-upopslag.

• Hallo nieuwe volumes toohello DPM-opslaggroep toevoegen en beschrijvende namen en data source-labels toewijzen indien gewenst.
• Voor elke gegevensbron die in de legacy-modus, stop de beveiliging van gegevensbronnen van Hallo en 'Beveiligde gegevens behouden'.  Hierdoor kan herstel van de oude herstelpunten na de migratie.

• Maken van een nieuwe pagina en selecteer Hallo gegevensbronnen die zijn opgeslagen met behulp van de nieuwe indeling toobe.
• DPM wordt een kopie van de replica doen vanuit oudere back-upopslag Hallo in Hallo moderne back-upopslag volume lokaal.
Opmerking: Deze wordt gezien als een na een herstelbewerking wordt uitgevoerd taak • alle nieuwe punten voor synchronisatie en herstel vervolgens worden opgeslagen in moderne back-up-opslag.
• Oude herstelpunten worden verwijderd uit als ze verlopen en uiteindelijk Hallo-schijfruimte vrij.
• Zodra alle Hallo verouderde volumes zijn verwijderd uit de oude opslag hello, Hallo schijf kunnen worden verwijderd uit Azure back-up en het Hallo-systeem.
• Maak een back-up van hello Azure DPMDB.

Deel 2:-belangrijke zaken > Hallo nieuwe server moet toobe met de dezelfde naam als Hallo oorspronkelijke Azure Backup-server. U kunt Hallo-naam van Hallo nieuwe Azure Backup-server niet wijzigen als u wilt dat oude opslaggroep toouse en DPMDB tooretain-herstelpunten -, is de back-up van DPMDB hebt moet zoals toobe hersteld moet

1) Afsluiten Hallo oorspronkelijke Azure Backup-server of weghalen Hallo-kabel.
2) Hallo-computeraccount in active directory herstellen.
3) Server 2016 op nieuwe machine en de naam van het Hallo dezelfde computernaam als Hallo oorspronkelijke Azure Backup-server installeren.
4) Hallo domein koppelen
5) Installeer Azure Backup-server V2 (verplaatsen DPM-opslaggroepschijven van de oude server en importeer)
6) Hallo DPMDB overgenomen uit het einde van deel 2 herstellen
7) Hallo opslag van Hallo oorspronkelijke back-upserver toohello nieuwe server koppelen.
8) Hallo DPMDB van SQL herstellen
9) Installeren vanaf de opdrachtregel beheerder op de nieuwe server cd tooMicrosoft Azure Backup-locatie en de bin-map

Voorbeeld van pad: C:\windows\system32 > cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\
back-up tooAzure Voer DPMSYNC-SYNC

10) Voer DPMSYNC-SYNC-Opmerking Als u nieuwe schijven toohello DPM opslaggroep in plaats van de oude versie Hallo verplaatsen hebt toegevoegd Voer DPMSYNC - reallocatereplica uit

## <a name="new-powershell-cmdlets-in-v2"></a>Nieuwe PowerShell-cmdlets in v2

Wanneer u v2 voor Azure Backup-Server installeert, zijn twee nieuwe cmdlets zijn beschikbaar: 
* [Koppelpunt DPMRecoveryPoint](https://technet.microsoft.com/library/mt787159.aspx)
* [Ontkoppeling DPMRecoveryPoint](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe tooprepare uw server of met het beveiligen van een werkbelasting beginnen:
- [Back-upserver van werkbelastingen voorbereiden](backup-azure-microsoft-azure-backup.md)
- [Back-upserver tooback van een VMware-server gebruiken](backup-azure-backup-server-vmware.md)
- [Back-upserver tooback van SQL Server gebruiken](backup-azure-sql-mabs.md)
- [Moderne back-upopslag met back-upserver gebruiken](backup-mabs-add-storage.md)

