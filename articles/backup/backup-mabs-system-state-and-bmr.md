---
title: aaaAzure back-upserver van systeemstatus beveiligt en herstelt toobare metal | Microsoft Docs
description: Azure Backup-Server tooback gebruik van de systeemstatus en bare metal recovery (BMR) beveiligen.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
keywords: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.targetplatform: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: markgal,masaran
ms.openlocfilehash: d34c8bbdc7cc24c905f81ceaf199698c1ee923db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-system-state-and-restore-toobare-metal-with-azure-backup-server"></a>Back-up van systeemstatus en toobare metal met Azure Backup-Server herstellen

Azure Backup-Server maakt een back-up van systeemstatus en bare metal recovery (BMR) beschermt.

*   **Systeemstatusback-up**: back-ups van besturingssysteembestanden, zodat u herstellen kunt wanneer een computer wordt gestart, maar systeem- en registerbestanden Hallo gaan verloren. Een systeemstatusback-up bevat:
    * Lid van domein: bestanden, registratiedatabase van COM +-klasse, register opstarten
    * Domeincontroller: Windows Server Active Directory (NTDS), bestanden, registratiedatabase van COM +-klasse, register, systeemvolume (SYSVOL) opstarten
    * Computer met clusterservices: clusterservermetagegevens
    * Computer die certificaatservices uitvoert: gegevens van het certificaat
* **Bare metal-back-up**: back-ups van besturingssysteembestanden en alle gegevens op essentiële volumes (met uitzondering van gebruikersgegevens). Een BMR back-up bevat per definitie een systeemstatusback-up. Het biedt beveiliging wanneer een computer start niet en er toorecover alles.

Hallo volgende tabel geeft een overzicht van wat u kunt back-up en herstellen. Zie voor gedetailleerde informatie over app-versies die kunnen worden beveiligd met systeemstatus en BMR [wat Azure Backup-Server doet een back-up?](backup-mabs-protection-matrix.md).

|Back-up|Probleem|Herstellen vanuit back-up van Azure Backup-Server|Herstellen van een systeemstatusback-up|BMR|
|----------|---------|---------------------------|------------------------------------|-------|
|**Bestandsgegevens**<br /><br />Regelmatig back-up<br /><br />BMR/systeemstatus|Verloren bestandsgegevens|J|N|N|
|**Bestandsgegevens**<br /><br />Azure Backup-Server back-up van gegevens uit een bestand<br /><br />BMR/systeemstatus|Verloren of beschadigd besturingssysteem|N|J|J|
|**Bestandsgegevens**<br /><br />Azure Backup-Server back-up van gegevens uit een bestand<br /><br />BMR/systeemstatus|Verloren server (gegevensvolumes intact)|N|N|J|
|**Bestandsgegevens**<br /><br />Azure Backup-Server back-up van gegevens uit een bestand<br /><br />BMR/systeemstatus|Verloren server (gegevensvolumes verloren)|J|Nee|Ja (BMR, gevolgd door normaal herstel van back-up bestandsgegevens)|
|**SharePoint-gegevens**:<br /><br />Azure Backup-Server back-up van Farmgegevens<br /><br />BMR/systeemstatus|Verloren site, lijsten, lijstitems, documenten|J|N|N|
|**SharePoint-gegevens**:<br /><br />Azure Backup-Server back-up van Farmgegevens<br /><br />BMR/systeemstatus|Verloren of beschadigd besturingssysteem|N|J|J|
|**SharePoint-gegevens**:<br /><br />Azure Backup-Server back-up van Farmgegevens<br /><br />BMR/systeemstatus|Herstel na noodgevallen|N|N|N|
|Windows Server 2012 R2 Hyper-V<br /><br />Azure Backup-Server back-up van de Hyper-V-host of Gast<br /><br />BMR/systeemstatusback-up van host|Verloren VM|J|N|N|
|Hyper-V<br /><br />Azure Backup-Server back-up van de Hyper-V-host of Gast<br /><br />BMR/systeemstatusback-up van host|Verloren of beschadigd besturingssysteem|N|J|J|
|Hyper-V<br /><br />Azure Backup-Server back-up van de Hyper-V-host of Gast<br /><br />BMR/systeemstatusback-up van host|Verloren Hyper-V-host (virtuele machines intact)|N|N|J|
|Hyper-V<br /><br />Azure Backup-Server back-up van de Hyper-V-host of Gast<br /><br />BMR/systeemstatusback-up van host|Verloren Hyper-V-host (virtuele machines verloren)|N|N|J<br /><br />BMR, gevolgd door normaal herstel van de Azure Backup-Server|
|SQL Server/Exchange<br /><br />Back-up van Azure back-upserver van app<br /><br />BMR/systeemstatus|Verloren app-gegevens|J|N|N|
|SQL Server/Exchange<br /><br />Back-up van Azure back-upserver van app<br /><br />BMR/systeemstatus|Verloren of beschadigd besturingssysteem|N|Y|J|
|SQL Server/Exchange<br /><br />Back-up van Azure back-upserver van app<br /><br />BMR/systeemstatus|Verloren server (database-transactie logboeken intact)|N|N|J|
|SQL Server/Exchange<br /><br />Back-up van Azure back-upserver van app<br /><br />BMR/systeemstatus|Verloren server (database-transactie logboeken verloren)|N|N|J<br /><br />BMR-herstel, gevolgd door normaal herstel van de Azure Backup-Server|

## <a name="how-system-state-backup-works"></a>De werking van de systeemstatusback-up

Wanneer een systeemstatusback-up wordt uitgevoerd, back-Server communiceert met Windows Server back-up toorequest een back-up van systeemstatus Hallo-server. Gebruik Hallo-station met de meeste beschikbare vrije ruimte Hallo standaard back-up-Server en Windows Server back-up. Informatie over dit station is opgeslagen in Hallo PSDataSourceConfig.xml bestand. Dit is Hallo-station dat gebruikmaakt van Windows Server back-up voor back-ups.

Hallo-station dat gebruikmaakt van back-upserver voor Hallo systeemstatusback-up, kunt u aanpassen. Ga tooC:\Program Files\Microsoft Data Protection Manager\MABS\Datasources op Hallo beveiligde server. Hallo PSDataSourceConfig.xml bestand openen voor bewerking. Wijziging Hallo \<FilesToProtect\> waarde voor de stationsletter Hallo. Opslaan en sluiten Hallo-bestand. Als er dat een beveiligingsgroep instellen tooprotect Hallo status van computer hello, voer een consistentiecontrole uit. Als u een waarschuwing wordt gegenereerd, selecteert u **beveiligingsgroep wijzigen** in de wizard vervolgens voltooit Hallo en Hallo waarschuwing. Voer vervolgens nog een consistentiecontrole uit.

Houd er rekening mee dat als Hallo protection-server zich in een cluster bevindt, is het mogelijk dat een clusterstation wordt geselecteerd als het station met de meeste vrije ruimte Hallo Hallo. Als eigendom van het station uitgeschakeld tooanother knooppunt is en een systeemstatusback-up wordt uitgevoerd, Hallo station is niet beschikbaar en Hallo back-up mislukt. In dit scenario wijzigen PSDataSourceConfig.xml toopoint tooa lokale schijf.

Windows Server back-up maakt vervolgens een map met de naam WindowsImageBackup in de hoofdmap Hallo van Hallo terugzetmap. Omdat Windows Server back-up maakt Hallo back-up, wordt alle Hallo-gegevens in deze map geplaatst. Wanneer Hallo back-up is voltooid, is Hallo bestand overgebrachte toohello back-Server-computer. Houd er rekening mee Hallo volgende informatie:

* Deze map en de inhoud ervan worden niet opgeschoond wanneer Hallo back-up of overdracht is voltooid. Hallo aanbevolen manier toothink hiervan is dat Hallo ruimte wordt gereserveerd voor Hallo volgende keer dat een back-up is voltooid.
* Hallo-map wordt gemaakt telkens wanneer een back-up wordt gemaakt. Hallo-datum en tijd stempel geven Hallo-tijd van de laatste systeemstatusback-up.

## <a name="bmr-backup"></a>BMR-back-up

Voor BMR (met inbegrip van een systeemstatusback-up), Hallo back-uptaak rechtstreeks tooa share op Hallo back-upserver computer opgeslagen. Tooa map wordt niet opgeslagen op Hallo beveiligde server.

Back-upserver van Windows Server back-up-aanroepen en deelt Hallo replicavolume voor BMR back-up. In dit geval duidelijk niet Windows Server Backup toouse Hallo station met de meeste vrije ruimte Hallo. In plaats daarvan het Hallo-share die is gemaakt voor Hallo taak gebruikt.

Wanneer Hallo back-up is voltooid, is Hallo bestand overgebrachte toohello back-Server-computer. Logboeken worden opgeslagen in C:\Windows\Logs\WindowsServerBackup.

## <a name="prerequisites-and-limitations"></a>Vereisten en beperkingen

-   BMR wordt niet ondersteund voor computers met Windows Server 2003 of voor computers waarop een client-besturingssysteem wordt uitgevoerd.

-   BMR kunnen niet worden beveiligd en system-status voor Hallo dezelfde computer in verschillende beveiligingsgroepen.

-   Een back-up-Server-computer beveiligen niet zelf voor BMR.

-   Korte termijn beveiliging tootape (schijf naar tape of D2T) wordt niet ondersteund voor BMR. Langdurige opslag tootape (schijf-naar-schijf-naar-tape of D2D2T) wordt ondersteund.

-   Voor BMR-beveiliging moet Windows Server back-up op Hallo beveiligde computer worden geïnstalleerd.

-   Voor BMR-beveiliging, in tegenstelling tot voor beveiliging van de systeemstatus, back-up-Server heeft geen geen schijfruimtevereisten op Hallo beveiligde computer. Windows Server Backup overdraagt rechtstreeks back-ups toohello back-up-servercomputer. de back-overdrachtstaak Hallo niet weergegeven in de Hallo back-upserver **taken** weergeven.

-   Back-upserver reserveert 30 GB aan ruimte op Hallo replicavolume voor BMR. U kunt dit wijzigen op Hallo **Schijftoewijzing** pagina in de wizard Modify Protection Group Hallo of met behulp van Hallo Get-DatasourceDiskAllocation en Set-DatasourceDiskAllocation PowerShell-cmdlets. Op het herstelpuntvolume hello vereist BMR-beveiliging ongeveer 6 GB voor een bewaarperiode van vijf dagen.
    * Houd er rekening mee dat u Hallo replica volume grootte tooless dan 15 GB niet reduceren.
    * Back-upserver berekenen niet Hallo grootte van BMR-gegevensbron Hallo. Er wordt vanuit gegaan 30 GB voor alle servers. Hallo-waarde op basis van de grootte van BMR-back-ups die u verwacht in uw omgeving dat Hallo wijzigen. Hallo-grootte van een BMR back-up kan ongeveer worden berekend als Hallo som van de gebruikte ruimte op alle essentiële volumes. Essentiële volumes = opstartvolume + systeemvolume + volume die als host fungeert voor systeemstatusgegevens zoals Active Directory.

-   Als u van systeemstatusbeveiliging beveiliging tooBMR wijzigt, vereist BMR-beveiliging minder ruimte op Hallo *herstelpuntvolume*. Echter is hello extra ruimte op Hallo volume niet vrijgemaakt. U kunt de volumegrootte Hallo op Hallo handmatig verkleinen **Schijftoewijzing wijzigen** pagina van de wizard Modify Protection Group Hallo of met behulp van Hallo Get-DatasourceDiskAllocation en Set-DatasourceDiskAllocation PowerShell-cmdlets.

    Als u van systeemstatusbeveiliging beveiliging tooBMR wijzigt, vereist BMR-beveiliging meer ruimte op Hallo *replicavolume*. Hallo-volume wordt automatisch uitgebreid. Als u toochange hello standaardruimtetoewijzingen wilt, gebruikt u Hallo Modify-DiskAllocation PowerShell-cmdlet.

-   Als u van beveiliging voor BMR-beveiliging toosystem wijzigt, moet u meer ruimte op het herstelpuntvolume Hallo. Back-upserver proberen tooautomatically toename Hallo volume. Als er onvoldoende ruimte in opslaggroep hello, wordt er een fout optreedt.

    Als u van beveiliging voor BMR-beveiliging toosystem wijzigt, moet u ruimte op Hallo beveiligde computer. Dit is omdat de systeemstatusbeveiliging eerst Hallo replica toohello lokale computer schrijft en brengt deze toohello back-up-servercomputer.

## <a name="before-you-begin"></a>Voordat u begint

1.  **Azure Backup-Server implementeren**. Controleer of de back-upserver correct is geïmplementeerd. Zie voor meer informatie:
    * [Systeemvereisten voor Azure Backup-Server](http://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites)
    * [Matrix van back-Server-beveiliging](backup-mabs-protection-matrix.md)

2.  **Opslag instellen**. U kunt back-upgegevens opslaan op schijf op de tape en in Hallo cloud met Azure. Zie voor meer informatie [voorbereiden gegevensopslag](https://docs.microsoft.com/system-center/dpm/plan-long-and-short-term-data-storage).

3.  **Hallo-beveiligingsagent instellen**. Hallo-beveiligingsagent op Hallo-computer die u tooback-up wilt installeren. Zie voor meer informatie [implementeren Hallo DPM-beveiligingsagent](http://docs.microsoft.com/system-center/dpm/deploy-dpm-protection-agent).

## <a name="back-up-system-state-and-bare-metal"></a>Back-up van systeemstatus en bare metal
Instellen van een beveiligingsgroep, zoals beschreven in [implementeren beveiligingsgroepen](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups). BMR kunnen niet worden beveiligd en system state voor Hallo dezelfde computer in verschillende groepen. Ook als u BMR selecteert, wordt systeemstatus automatisch ingeschakeld.


1.  tooopen hello nieuwe beveiligingsgroep maken wizard in Hallo back-up Server Administrator-Console selecteert **beveiliging** > **acties** > **beveiliging maken Groep**.

2.  Op Hallo **Type beveiligingsgroep selecteren** pagina **Servers**, en selecteer vervolgens **volgende**.

3.  Op Hallo **groepsleden selecteren** pagina, vouw Hallo computer uit en selecteer vervolgens **BMR** of **systeemstatus**.

    Houd er rekening mee dat zowel BMR en systeemstatus status voor Hallo kunnen niet worden beveiligd dezelfde computer in verschillende groepen. Ook als u BMR selecteert, wordt systeemstatus automatisch ingeschakeld. Zie voor meer informatie [implementeren beveiligingsgroepen](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups).

4.  Op Hallo **methode voor gegevensbeveiliging selecteren** pagina, selecteer de gewenste toohandle korte en lange termijn back-up. Kortetermijnback-up is eerst altijd toodisk, met de optie Hallo van een back-up van Hallo schijf toohello Azure cloud met behulp van Azure Backup (korte of lange). Een back-toohello alternatieve toolong termijn cloud is tooset up op lange termijn back-tooa zelfstandige apparaat of tape tapewisselaar die tooBackup Server is verbonden.

5.  Op Hallo **Kortetermijndoelen selecteren** pagina, selecteer de gewenste tooback tooshort-termijn opslag op schijf installeren:
    1. Voor **bewaartermijn**, hoe lang u tookeep Hallo gegevens op schijf wilt selecteren. 
    2. Voor **Synchronisatiefrequentie**, selecteer hoe vaak u een incrementele back-toodisk toorun. Als u niet tooset een back-interval wilt, kunt u controleren Hallo **net vóór een herstelpunt** optie. Back-upserver wordt een snelle volledige back-up uitgevoerd net voordat elk herstelpunt is gepland.

6.  Als u wilt dat toostore gegevens op tape voor langdurige opslag op Hallo **langetermijndoelen weergeven** te selecteren hoe lang u wilt dat tookeep tapegegevens (1-99 jaar). 
    1. Voor **frequentie van back-up**, selecteer hoe vaak tootape back-up moet worden uitgevoerd. Hallo frequentie is gebaseerd op Hallo-bewaartermijn die u hebt geselecteerd:
        * Wanneer de bewaartermijn Hallo 1-99 jaar is, kunt u toooccur back-ups dagelijks, wekelijks, tweewekelijks, maandelijks, elk kwartaal, half jaar of jaarlijkse selecteren.
        * Wanneer de bewaartermijn Hallo 1-11 maanden is, kunt u back-ups toooccur dagelijks, wekelijks, tweewekelijks of maandelijks selecteren.
        * Wanneer de bewaartermijn Hallo 1-4 weken is, kunt u back-ups toooccur dagelijks of wekelijks.

    2. Op Hallo **Details selecteren Tape en bibliotheek** pagina, selecteer Hallo tape en tapewisselaar toouse en of de gegevens moeten worden gecomprimeerd en versleuteld.

7.  Op Hallo **Schijftoewijzing controleren** pagina, bekijkt hello opslaggroepschijfruimte die voor het Hallo-beveiligingsgroep toegewezen.

    1. **Totale grootte van de gegevens** is Hallo grootte van de gewenste tooback up Hallo-gegevens.
    2. **Schijfruimte toobe ingericht op Azure Backup-Server** Hallo ruimte die back-upserver voor Hallo-beveiligingsgroep aanbeveelt. Back-upserver kiest Hallo ideaal back-volume op basis van Hallo-instellingen. U kunt echter Hallo back-upvolume keuzes in bewerken **schijf van de gegevens van schijfopslagtoewijzing**. 
    3. Voor werkbelastingen in de vervolgkeuzelijst hello, Hallo voorkeur opslag selecteren. Uw bewerkingen Hallo waarden wijzigen voor **totale opslag** en **vrije opslagruimte** in Hallo **beschikbaar schijfopslag** deelvenster. Underprovisioned ruimte is Hallo en de hoeveelheid opslagruimte back-upserver wordt voorgesteld dat u toohello volume, tooensure goede back-ups toevoegen.

8.  Op Hallo **methode voor maken van selecteren Replica** pagina, selecteer de gewenste toohandle Hallo initiële volledige gegevensreplicatie. Als u tooreplicate via Hallo netwerk kiest, wordt u aangeraden een tijdstip buiten de piekuren te kiezen. Voor grote hoeveelheden gegevens of netwerkomstandigheden die minder dan optimale, overweeg het Hallo-gegevens offline repliceren met behulp van verwijderbare media.

9. Op Hallo **kiest u opties voor consistentiecontrole** pagina, selecteert u hoe u consistentiecontroles tooautomate wilt. U kunt de toorun een controle alleen wanneer replicagegevens inconsistent, of volgens een schema wordt. Als u niet tooconfigure automatische consistentiecontrole wilt, kunt u een handmatige controle uitvoeren op elk gewenst moment. een handmatige controle, in Hallo toorun **beveiliging** gebied Hallo back-up Server Administrator-Console met de rechtermuisknop op Hallo beveiliging groep en selecteert u vervolgens **consistentiecontrole uitvoeren**.

10. Als u tooback up toohello cloud geselecteerde met behulp van Azure Backup op Hallo **gegevens voor Online beveiliging opgeven** pagina, zorg ervoor dat u de gewenste tooback up tooAzure Hallo-werkbelastingen selecteert.

11. Op Hallo **Online back-upschema opgeven** pagina, selecteert u hoe vaak incrementele back-ups tooAzure wordt uitgevoerd. U kunt back-ups toorun elke dag, week, maand en jaar plannen en selecteer Hallo datum en tijd waarop ze moeten worden uitgevoerd. Back-ups kunnen van tootwice per dag optreden. Telkens wanneer een back-up wordt uitgevoerd, een herstelpunt van gegevens wordt gemaakt in Azure vanaf Hallo kopie van Hallo back-upgegevens op Hallo back-upserver schijf opgeslagen.

12. Op Hallo **Online bewaarbeleid opgeven** te selecteren hoe Hallo herstelpunten die zijn gemaakt vanuit Hallo dagelijkse, wekelijkse, maandelijkse en jaarlijkse back-ups blijven behouden in Azure.

13. Op Hallo **Onlinereplicatie kiezen** te selecteren hoe Hallo initiële volledige replicatie van gegevens plaatsvindt. U kunt repliceren via Hallo netwerk of komen een offline back-up (offline seeding). Offline back-ups maakt gebruik van de functie Azure Import Hallo. Zie voor meer informatie [Offline back-werkstroom in Azure Backup](backup-azure-backup-import-export.md).

14. Op Hallo **samenvatting** pagina, Controleer uw instellingen. Nadat u hebt geselecteerd **groep maken**, vindt initiële replicatie van gegevens Hallo plaats. Wanneer replicatie is voltooid, op Hallo **Status** pagina status van de groep Hallo bescherming is **OK**. Back-up vindt plaats per Hallo beveiliging vervolgens groepsinstellingen.

## <a name="recover-system-state-or-bmr"></a>Systeemstatus- of BMR herstellen
U kunt de status tooa netwerklocatie BMR of systeemstatus herstellen. Als u hebt een back-up BMR, gebruikt u Windows Recovery Environment (WinRE) toostart uw systeem en het toohello netwerk verbinden. Vervolgens gebruikt u Windows Server Backup toorecover van Hallo netwerklocatie. Als u hebt een back-up van systeemstatus, gebruikt u Windows Server Backup toorecover van Hallo netwerklocatie.

### <a name="restore-bmr"></a>BMR herstellen
Herstel op Hallo back-upserver computer uitgevoerd:

1.  In Hallo **herstel** deelvenster, zoek Hallo computer u wilt toorecover en selecteer vervolgens **Bare Metal Recovery**.

2.  Beschikbare herstelpunten worden vet in Hallo kalender. Hallo-datum en tijd voor Hallo herstelpunt dat u wilt dat toouse selecteren.

3.  Op Hallo **Type herstelbewerking selecteren** pagina **kopie tooa netwerkmap.**

4.  Op Hallo **bestemming opgeven** pagina waar u toocopy Hallo gegevens. Houd er rekening mee dat geselecteerde bestemming Hallo toohave moet voldoende ruimte. U wordt aangeraden dat u een nieuwe map maken.

5.  Op Hallo **herstelopties opgeven** pagina, selecteer Hallo beveiliging instellingen tooapply. Selecteer of u toouse storage area network (SAN wilt)-gebaseerde hardwaremomentopnamen voor sneller herstel. (Dit is een optie alleen als u een SAN met deze functionaliteit beschikbaar is, en mogelijkheid toocreate Hallo en een kloon toomake splitsen deze beschrijfbaar. In Addition, hello beveiligde computer en de servercomputer van de back-up moeten worden verbonden toohello hetzelfde netwerk.)

6.  Meldingsopties instellen. Op Hallo **bevestiging** pagina **herstellen**.

Hallo sharelocatie instellen:

1.  Ga in de locatie hello, toohello-map met de Hallo back-up.

2.  Hallo-map die zich één niveau boven WindowsImageBackup, zodat hello basis van de gedeelde map Hallo Hallo WindowsImageBackup map delen. Als u dit doet, kan herstel Hallo back-up niet gevonden. tooconnect met behulp van Windows Recovery Environment (WinRE), moet u een share die u in WinRE Hallo juiste IP-adres en referenties openen kunt.

Hallo systeem herstellen:

1.  Start Hallo de computer waarop de toorestore Hallo installatiekopie met behulp van Windows-DVD hello voor Hallo systeem die u wilt herstellen.

2.  Controleer of de taal en landinstellingen op Hallo eerste pagina. Op Hallo **installeren** pagina **uw computer herstellen**.

3.  Op Hallo **opties voor Systeemherstel** pagina **herstellen van de computer met behulp van een installatiekopie die u eerder hebt gemaakt**.

4.  Op Hallo **Selecteer een systeemkopieback-up** pagina **een systeemkopie selecteren** > **Geavanceerd** > **zoeken naar een systeem de installatiekopie op Hallo netwerk**. Als u een waarschuwing wordt weergegeven, selecteert u **Ja**. Ga toohello sharepad, Hallo referenties invoeren en selecteer Hallo herstelpunt. Dit scant naar specifieke back-ups die beschikbaar in dat herstelpunt zijn. Hallo herstelpunt dat u wilt dat toouse selecteren.

5.  Op Hallo **kiezen hoe toorestore Hallo back-** pagina **schijven formatteren en opnieuw partitioneren**. Controleer de instellingen op de volgende pagina Hallo. 

6.  toobegin hello herstel, selecteer **voltooien**. Opnieuw opstarten is vereist.

### <a name="restore-system-state"></a>Systeemstatus herstellen

Voer het herstel in de back-upserver van:

1.  In Hallo **herstel** deelvenster, zoek Hallo computer dat u toorecover wilt en selecteer vervolgens **Bare Metal Recovery**.

2.  Beschikbare herstelpunten worden vet in Hallo kalender. Hallo-datum en tijd voor Hallo herstelpunt dat u wilt dat toouse selecteren.

3.  Op Hallo **Type herstelbewerking selecteren** pagina **kopie tooa netwerkmap**.

4.  Op Hallo **bestemming opgeven** pagina waar u toocopy Hallo gegevens. Houd er rekening mee dat geselecteerde bestemming Hallo moet voldoende ruimte. U wordt aangeraden dat u een nieuwe map maken.

5.  Op Hallo **herstelopties opgeven** pagina, selecteer Hallo beveiliging instellingen tooapply. Selecteer vervolgens of u toouse SAN-gebaseerde hardwaremomentopnamen voor sneller herstel wilt. (Dit is een optie alleen als u een SAN met deze functionaliteit en mogelijkheid toocreate Hallo en een kloon toomake splitsen deze beschrijfbaar. In Addition, Hallo beveiligde computer en back-upserver server moet verbonden toohello hetzelfde netwerk.)

6.  Meldingsopties instellen. Op Hallo **bevestiging** pagina **herstellen**.

Windows Server back-up uitvoeren:

1.  Selecteer **acties** > **herstellen** > **deze Server** > **volgende**.

2.  Selecteer **een andere Server**, selecteer Hallo **Type locatie opgeven** pagina en selecteer vervolgens **externe gedeelde map**. Voer Hallo pad toohello map met de Hallo herstelpunt.

3.  Op Hallo **Type herstelbewerking selecteren** pagina **systeemstatus**. 

4. Op Hallo **locatie voor Systeemtoestandherstel selecteren** pagina **oorspronkelijke locatie**.

5.  Op Hallo **bevestiging** pagina **herstellen**. Na het terugzetten van Hallo door Hallo-server opnieuw te starten.

6.  U kunt ook Hallo systeemstatusherstel uitvoeren bij een opdrachtprompt. toodo deze, start Windows Server back-up op de computer Hallo gewenste toorecover. Voer in tooget Hallo versie-id, bij een opdrachtprompt:```wbadmin get versions -backuptarget \<servername\sharename\>```

    Hallo versie-id toostart Hallo systeemstatusherstel gebruiken. Voer het volgende achter de opdrachtprompt Hallo:```wbadmin start systemstaterecovery -version:<versionidentified> -backuptarget:<servername\sharename>```

    U wilt bevestigen dat toostart Hallo herstel. Hallo-proces in het opdrachtpromptvenster hello, kunt u zien. Er wordt een herstellogboek gemaakt. Na het terugzetten van Hallo door Hallo-server opnieuw te starten.

