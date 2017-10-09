---
title: aaaPlan capaciteit en schaal voor VMware replicatie tooAzure met Azure Site Recovery | Microsoft Docs
description: Dit artikel tooplan capaciteit en de schaal gebruiken bij het repliceren van virtuele VMware-machines tooAzure met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: rayne
ms.openlocfilehash: 7ca9147d1b4611f6b4a67c3de3f27fb9878f4c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="plan-capacity-and-scaling-for-vmware-replication-with-azure-site-recovery"></a>Plannen van capaciteit en de schaalbaarheid van VMware-replicatie met Azure Site Recovery

Gebruik dit artikel toofigure uit het plannen van capaciteit en de schaling bij het repliceren van de lokale virtuele VMware-machines en fysieke servers tooAzure met [Azure Site Recovery](site-recovery-overview.md).

## <a name="how-do-i-start-capacity-planning"></a>Hoe start capaciteitsplanning?

Verzamelt informatie over uw replicatieomgeving door Hallo [Azure Site Recovery implementatie Planner](https://aka.ms/asr-deployment-planner-doc) voor VMware-replicatie. [Meer informatie](site-recovery-deployment-planner.md) over dit hulpprogramma. U kunt informatie verzamelen over compatibele en niet-compatibele virtuele machines, schijven per virtuele machine, en gegevens verloop per schijf. Hallo hulpprogramma vallen ook netwerkbandbreedte en hello Azure-infrastructuur die nodig zijn voor een geslaagde failover voor replicatie en test.

## <a name="capacity-considerations"></a>Overwegingen voor capaciteitsplanning

**Onderdeel** | **Details** |
--- | --- | ---
**Replicatie** | **Maximale dagelijkse wijzigingssnelheid:** beveiligde machine kan alleen een van de processerver gebruiken, en een server met een enkel proces een dagelijkse wijzigingssnelheid van too2 TB kan verwerken. 2 TB is dus Hallo maximale dagelijkse gegevens wijzigen die wordt ondersteund voor een beveiligde machine.<br/><br/> **Maximale doorvoer:** een gerepliceerde machine kan deel uitmaken van tooone storage-account in Azure. Standard-opslagaccount kan maximaal 20.000 aanvragen per seconde worden verwerkt en we adviseren dat u het aantal i/o-bewerkingen per seconde (IOPS) Hallo over een bron machine too20, 000. Bijvoorbeeld, als er een bronmachine met 5 schijven en elke schijf 120 IOPS (grootte van 8 kB) op de bronmachine hello genereert, worden binnen hello Azure per schijf-IOPS limiet van 500. (Hallo aantal vereiste opslagaccounts voor is gelijk toohello totale bronmachine IOP's, gedeeld door 20.000.)
**Configuratieserver** | Hallo configuratieserver moet kunnen toohandle Hallo dagelijkse wijziging snelheid capaciteit voor alle werkbelastingen op beveiligde machines uitgevoerd en moet voldoende bandbreedte toocontinuously repliceren gegevens tooAzure opslag.<br/><br/> Als een best practice vinden u Hallo configuratieserver op Hallo hetzelfde netwerk en LAN-segment als Hallo machines gewenste tooprotect. Dit kan zich bevinden op een ander netwerk, maar de machines die u wilt dat tooprotect layer 3-netwerk zichtbaarheid tooit moet hebben.<br/><br/> Aanbevelingen voor de grootte voor de configuratieserver Hallo worden samengevat in de tabel in de volgende sectie Hallo Hallo.
**Processerver** | eerste processerver Hallo is standaard op Hallo configuratieserver geïnstalleerd. U kunt aanvullende processen servers tooscale uw omgeving te implementeren. <br/><br/> Hallo processerver ontvangt replicatiegegevens van beveiligde machines en optimaliseert met caching, compressie en codering. Vervolgens stuurt Hallo gegevens tooAzure. Hallo proces server-machine moet voldoende bronnen tooperform hebben deze taken.<br/><br/> Hallo processerver maakt gebruik van een cache op basis van schijven. Gebruik een afzonderlijke cache 600 GB of meer toohandle gegevenswijzigingen opgeslagen in het Hallo-gebeurtenis van een knelpunt netwerk of een storing.

## <a name="size-recommendations-for-hello-configuration-server"></a>Aanbevelingen voor de grootte voor de configuratieserver Hallo

**CPU** | **Geheugen** | **Cachegrootte van de schijf** | **Snelheid van de gegevens wijzigen** | **Beveiligde machines**
--- | --- | --- | --- | ---
8 vcpu's (2-sockets * 4 kernen @ 2,5 gigahertz [GHz]) | 16 GB | 300 GB | 500 GB of minder | Minder dan 100 machines repliceren.
12 vcpu's (2-sockets * @ 2,5 GHz-6 kernen) | 18 GB | 600 GB | 500 GB too1 TB | 100 tot 150-machines repliceren.
16 vcpu's (2-sockets * @ 2,5 GHz-8 kernen) | 32 GB | 1 TB | 1 TB too2 TB | Repliceren tussen 150 tot 200-machines.
Een andere processerver implementeren | | | > 2 TB | Aanvullende processen servers implementeren als u meer dan 200 machines repliceert, of als Hallo dagelijkse gegevens wijzigen frequentie hoger is dan 2 TB.

Waar:

* Elke bronmachine is geconfigureerd met 3 schijven van 100 GB.
* We gebruiken benchmarking opslag van 8 SAS-schijven van 10 K RPM, RAID 10 voor cache schijf metingen.

## <a name="size-recommendations-for-hello-process-server"></a>Aanbevelingen voor de grootte voor de processerver Hallo

Als u meer dan 200 machines tooprotect moet of dagelijkse wijzigingssnelheid Hallo groter dan 2 TB is, kunt u het proces servers toohandle Hallo replicatie load kunt toevoegen. tooscale out, kunt u:

* Het aantal configuratieservers Hallo verhogen. U kunt bijvoorbeeld van too400 machines met twee configuratieservers beveiligen.
* Meer processervers toevoegen en deze configuratieserver toohandle verkeer in plaats van (of als aanvulling op) hello gebruiken.

Hallo volgende tabel beschrijft een scenario waarin:

* U niet van plan bent toouse Hallo configuratieserver als processerver.
* U hebt een extra processerver ingesteld.
* U kunt beveiligde virtuele machines toouse Hallo aanvullende processerver hebt geconfigureerd.
* Elke machine beveiligde bron is geconfigureerd met drie schijven van 100 GB.

**Configuratieserver** | **Aanvullende processerver** | **Cachegrootte van de schijf** | **Snelheid van de gegevens wijzigen** | **Beveiligde machines**
--- | --- | --- | --- | ---
8 vcpu's (2-sockets * 4 kernen @ 2,5 GHz), 16 GB geheugen | 4 vcpu's (2-sockets * 2 kernen @ 2,5 GHz), 8 GB geheugen | 300 GB | 250 GB of minder | 85 of minder machines repliceren.
8 vcpu's (2-sockets * 4 kernen @ 2,5 GHz), 16 GB geheugen | 8 vcpu's (2-sockets * 4 kernen @ 2,5 GHz), 12 GB geheugen | 600 GB | 250 GB too1 TB | Repliceren tussen 85 150-machines.
12 vcpu's (2-sockets * 6 kernen @ 2,5 GHz), 18 GB geheugen | 12 vcpu's (2-sockets * 6 kernen @ 2,5 GHz) 24 GB geheugen | 1 TB | 1 TB too2 TB | Repliceren tussen 150 225 machines.

Hallo manier waarop u uw servers schalen, is afhankelijk van uw voorkeur voor een model omhoog schalen of scale-out.  Als u door het implementeren van een paar geavanceerde configuratie en processervers opschalen of uitbreiden door het implementeren van meerdere servers met minder bronnen. Bijvoorbeeld, als u tooprotect 220 machines moet, kan u doen van Hallo volgende:

* De configuratieserver Hallo met 12 vCPU, 18 GB geheugen en een extra processerver met 12 vCPU, 24 GB geheugen instellen. Beveiligde machines toouse Hallo aanvullende processerver alleen configureren.
* Twee configuratieservers (2 x 8 vCPU, 16 GB RAM-geheugen) en twee extra processervers (1 x 8 vCPU en 4 vCPU x 1 toohandle 135 + 85 [220] machines) instellen. Beveiligde machines toouse Hallo extra proces alleen servers configureren.


## <a name="control-network-bandwidth"></a>Netwerkbandbreedte

Nadat u hebt gebruikt Hallo [Hallo implementatie Planner hulpprogramma](site-recovery-deployment-planner.md) toocalculate Hallo bandbreedte u nodig hebt voor replicatie (initiële replicatie Hallo en vervolgens delta), kunt u de hoeveelheid bandbreedte die wordt gebruikt voor replicatie met een paar Hallo bepalen van opties:

* **Bandbreedte beperken**: VMware-verkeer dat wordt gerepliceerd tooAzure verloopt via een specifiek proces-server. U kunt de bandbreedte op Hallo machines die worden uitgevoerd als processervers beperken.
* **Netwerkbandbreedte beïnvloeden**: U kunt zelf bepalen hoeveel Hallo bandbreedte gebruikt voor de replicatiegroep met behulp van een aantal registersleutels:
  * Hallo **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** registerwaarde geeft u het aantal threads die worden gebruikt voor gegevensoverdracht (initiële replicatie of deltareplicatie) van een schijf Hallo. Een hogere waarde verhoogt Hallo netwerkbandbreedte gebruikt voor replicatie.
  * Hallo **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** geeft het aantal threads die worden gebruikt voor gegevensoverdracht tijdens failback Hallo.

### <a name="throttle-bandwidth"></a>Bandbreedte beperken

1. Open hello Azure Backup MMC-module op Hallo machine fungeert als processerver Hallo. Een snelkoppeling voor back-up is standaard beschikbaar zijn op Hallo bureaublad of in Hallo volgende map: C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Klik in het Hallo-module op **eigenschappen wijzigen**.

    ![Schermopname van Azure Backup MMC-module optie toochange eigenschappen](./media/site-recovery-vmware-to-azure/throttle1.png)
3. Op Hallo **bandbreedtebeperking** tabblad **inschakelen voor gebruik van internetbandbreedte voor back-upbewerkingen**. Hallo limieten instellen voor werk en niet-werk uren. Geldige bereiken zijn afkomstig van 512 Kbps too102 Mbps per seconde.

    ![Schermopname van Azure back-up eigenschappenvenster](./media/site-recovery-vmware-to-azure/throttle2.png)

U kunt ook Hallo [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset beperking. Hier volgt een voorbeeld:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** geeft aan dat er geen beperking is vereist.

### <a name="influence-network-bandwidth-for-a-vm"></a>Netwerkbandbreedte beïnvloeden voor een virtuele machine

1. In het register Hallo van de virtuele machine, te navigeren**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * tooinfluence hello bandbreedte netwerkverkeer op een schijf replicerende wijzigen Hallo-waarde van **UploadThreadsPerVM**, of maak Hallo sleutel aan als deze niet bestaat.
   * tooinfluence hello bandbreedte voor failbackverkeer vanuit Azure, wijzig de waarde Hallo van **DownloadThreadsPerVM**.
2. Hallo-standaardwaarde is 4. In een netwerk 'overprovisioning', moeten deze registersleutels van Hallo standaardwaarden worden gewijzigd. Hallo maximum is 32. Verkeer toooptimize Hallo waarde bewaken.


## <a name="deploy-additional-process-servers"></a>Aanvullende processen servers implementeren

Als u tooscale uit uw implementatie dan 200 bronmachines, of u hebt een totaal dagelijks verloop in verhouding van meer dan 2 TB, moet u extra proces servers toohandle Hallo-netwerkverkeer. Volg deze instructies tooset Hallo proces server. Na het instellen van Hallo-server, die u migreert bron machines toouse deze.

1. In **siteherstel servers**Hallo configuratieserver op en klik vervolgens op **processerver**.

    ![Schermopname van Site Recovery servers optie tooadd processerver](./media/site-recovery-vmware-to-azure/migrate-ps1.png)
2. In **servertype**, klikt u op **processerver (lokale)**.

    ![Schermafbeelding van de processerver dialoogvenster](./media/site-recovery-vmware-to-azure/migrate-ps2.png)
3. Hallo Site Recovery Unified Setup-bestand downloaden en voer dit tooinstall Hallo processerver. Dit ook geregistreerd in kluis Hallo.
4. In **voordat u begint met**, selecteer **toevoegen van extra proces servers tooscale uit implementatie**.
5. Wizard voltooid Hallo in Hallo dezelfde manier als wanneer u [instellen](#step-2-set-up-the-source-environment) Hallo configuratieserver.

    ![Schermopname van Azure Site Recovery Unified Setup-wizard](./media/site-recovery-vmware-to-azure/add-ps1.png)
6. In **Server configuratiedetails**Hallo IP-adres van de configuratieserver Hallo en Hallo wachtwoordzin. tooobtain hello wachtwoordzin, voeren **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe – n** op Hallo configuratieserver.

    ![Schermopname van Server configuratiedetails pagina](./media/site-recovery-vmware-to-azure/add-ps2.png)

### <a name="migrate-machines-toouse-hello-new-process-server"></a>Machines toouse Hallo nieuwe processerver migreren
1. In **instellingen** > **siteherstel servers**, klikt u op de configuratieserver Hallo uit en vouw vervolgens **servers verwerken**.

    ![Schermafbeelding van de processerver dialoogvenster](./media/site-recovery-vmware-to-azure/migrate-ps2.png)
2. Met de rechtermuisknop op de processerver Hallo momenteel in gebruik en klik op **Switch**.

    ![Schermopname van configuratie in het dialoogvenster van server](./media/site-recovery-vmware-to-azure/migrate-ps3.png)
3. In **proces van Select doelserver**, selecteer Hallo nieuwe processerver u wilt toouse en selecteer vervolgens Hallo virtuele machines die server hello wordt afgehandeld. Klik op Hallo informatie pictogram tooget informatie over het Hallo-server. toohelp u besluiten laden, Hallo gemiddelde ruimte die nodig is tooreplicate elke geselecteerde virtuele machine toohello nieuwe processerver wordt weergegeven. Klik op Hallo vinkje toostart toohello nieuwe processerver repliceren.


## <a name="next-steps"></a>Volgende stappen

Downloaden en uitvoeren van Hallo [Azure Site Recovery-implementatie plannen](https://aka.ms/asr-deployment-planner)
