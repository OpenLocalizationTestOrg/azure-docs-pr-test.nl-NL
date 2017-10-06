---
title: 'Azure Backup: Bestanden en mappen herstellen van een virtuele machine van Azure back-up | Microsoft Docs'
description: Bestanden herstellen vanaf een herstelpunt voor virtuele machine van Azure
services: backup
documentationcenter: dev-center-name
author: pvrk
manager: shivamg
keywords: herstel op itemniveau; Bestandsherstel van back-up van virtuele machine van Azure. bestanden herstellen van de virtuele machine in Azure
ms.assetid: f1c067a2-4826-4da4-b97a-c5fd6c189a77
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pullabhk;markgal
ms.openlocfilehash: 1a62a0ed83d61272c032ac0377a54099ed118db4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="recover-files-from-azure-virtual-machine-backup"></a>Bestanden herstellen vanuit back-up van virtuele machine van Azure

Azure backup biedt Hallo mogelijkheid toorestore [Azure VM's en schijven](./backup-azure-arm-restore-vms.md) vanuit back-ups van virtuele machine van Azure. Nu in dit artikel wordt uitgelegd hoe u items zoals bestanden en mappen kunt herstellen vanaf een back-up van virtuele machine van Azure.

> [!Note]
> Deze functie is beschikbaar voor virtuele Azure-machines geïmplementeerd met Resource Manager-model Hallo en beveiligde tooa Recovery services-kluis.
> Herstel van bestanden vanuit een versleutelde VM back-up wordt niet ondersteund.
>

## <a name="mount-hello-volume-and-copy-files"></a>Hallo volume en kopieer de bestanden koppelen

1. Meld u aan bij Hallo [Azure-portal](http://portal.Azure.com). Hallo relevante Recovery services-kluis en back-upitems Hallo vereist zoeken.

2. Klik op de blade back-up Item Hallo **bestandsherstel**

    ![Recovery Services-kluis back-item openen](./media/backup-azure-restore-files-from-vm/open-vault-item.png)

    Hallo **bestandsherstel** blade wordt geopend.

    ![Bestand herstel blade](./media/backup-azure-restore-files-from-vm/file-recovery-blade.png)

3. Van Hallo **herstelpunt selecteren** vervolgkeuzelijst, selecteer Hallo herstelpunt dat Hallo bestanden bevat die u wilt. Standaard is de meest recente herstelpunt Hallo al geselecteerd.

4. Klik op **uitvoerbaar bestand downloaden** (voor Windows Azure VM) of **downloadscript** (voor Linux Azure VM) toodownload Hallo software die u toocopy bestanden vanaf het herstelpunt hello wilt gebruiken.

  Hallo executable/script maakt een verbinding tussen de lokale computer Hallo en Hallo opgegeven herstelpunt.

5. U moet een wachtwoord toorun Hallo gedownload script/uitvoerbaar bestand. U kunt wachtwoord Hallo van Hallo-portal met behulp van Hallo kopie-knop naast Hallo gegenereerd wachtwoord kopiëren

    ![Gegenereerd wachtwoord](./media/backup-azure-restore-files-from-vm/generated-pswd.png)

6. Voer op Hallo computer waar u toorecover Hallo bestanden Hallo executable/script. U moet uitvoeren met beheerdersreferenties. Als u Hallo script op een computer met beperkte toegang uitvoert, moet u zorgen er toegang tot:

    - Download.Microsoft.com
    - Azure-eindpunten die wordt gebruikt voor back-ups van virtuele machine in Azure
    - uitgaande poort 3260

   Voor Linux script Hallo 'open-iscsi' en 'lshw' onderdelen vereist tooconnect toohello herstelpunt. Als deze niet bestaan op Hallo machine waar het wordt uitgevoerd, vraagt de voor machtiging tooinstall Hallo relevante onderdelen en installeert ze na toestemming.
   
   Voer Hallo wachtwoord gekopieerd uit Hallo-portal als u wordt gevraagd. Zodra Hallo geldig wachtwoord is ingevoerd verbindt Hallo scripts toohello herstelpunt.
      
    ![Bestand herstel blade](./media/backup-azure-restore-files-from-vm/executable-output.png)
    
   
   U kunt Hallo-script uitvoeren op een machine met Hallo hetzelfde (of compatibel)-besturingssysteem als Hallo back-up VM. Zie Hallo [compatibel besturingssysteem tabel](backup-azure-restore-files-from-vm.md#compatible-os) voor compatibele besturingssystemen. Als Hallo beveiligd Azure virtuele machine maakt gebruik van Windows Storage Spaces (voor Windows Azure VM's) of LVM/RAID-Arrays(for Linux VMs), dan hebt u Hallo executable/script niet uitvoeren op de Hallo dezelfde virtuele machine. In plaats daarvan het uitvoeren op een andere machine met een compatibel besturingssysteem.

### <a name="compatible-os"></a>Compatibel besturingssysteem

#### <a name="for-windows"></a>Voor Windows

Hallo volgend tabel toont Hallo compatibiliteit tussen besturingssystemen-server en computers. Tijdens het herstellen van bestanden, kunt u bestanden tussen incompatibel besturingssystemen niet terugzetten.

|Serverbesturingssysteem | Compatibel clientbesturingssysteem  |
| --------------- | ---- |
| Windows Server 2012 R2 | Windows 8.1 |
| Windows Server 2012    | Windows 8  |
| Windows Server 2008 R2 | Windows 7   |

#### <a name="for-linux"></a>Voor Linux

In Linux, Hallo fundamenteel vereiste is die Hallo OS van Hallo machine waar het Hallo-script wordt uitgevoerd moet ondersteunen Hallo bestandssysteem Hallo bestanden aanwezig zijn in Hallo back-up Linux VM. Bij het selecteren van het script van een machine toorun hello, zorg ervoor dat het Hallo compatibele OS en Hallo versies zoals vermeld in de onderstaande tabel voor Hallo.

|Linux OS | Versies  |
| --------------- | ---- |
| Ubuntu | 12.04 en hoger |
| CentOS | 6.5 en hoger  |
| RHEL | 6.7 en hoger |
| Debian | 7 en hoger |
| Oracle Linux | 6.4 en hoger |

Hallo script ook vereist python en onderdelen tooexecute bash en veilige verbinding toohello herstelpunt.

|Onderdeel | Versie  |
| --------------- | ---- |
| Bash | 4 en hoger |
| python | 2.6.6 en hoger  |


### <a name="identifying-volumes"></a>Identificeren van Volumes

#### <a name="for-windows"></a>Voor Windows

Wanneer u Hallo exectuable uitvoert, wordt besturingssysteem Hallo Hallo nieuwe volumes koppelt en stationsletters worden toegewezen. U kunt Windows Verkenner of Verkenner toobrowse deze stations gebruiken. Hallo stationsletters toegewezen toohello volumes mogelijk niet Hallo dezelfde letters zoals hello oorspronkelijke virtuele machine echter Hallo volumenaam blijft behouden. Bijvoorbeeld, als hello volume op de oorspronkelijke virtuele machine Hallo is ' gegevensschijf (E:\)', dat het volume kan worden gekoppeld als ' gegevensschijf ('Alle stationsletters beschikbaar':\) op Hallo lokale computer. Door alle volumes die worden vermeld in de uitvoer van het script Hallo totdat u de bestanden/map bladeren.  
       
   ![Bestand herstel blade](./media/backup-azure-restore-files-from-vm/volumes-attached.png)
           
#### <a name="for-linux"></a>Voor Linux

Hallo-volumes van het herstelpunt Hallo zijn in Linux, gekoppelde toohello map waar het Hallo-script wordt uitgevoerd. Hallo gekoppeld schijven, volumes en bijbehorende koppelpunt Hallo paden dienovereenkomstig worden weergegeven. Deze paden koppelen zichtbaar toousers hebben toegang tot de hoofdmap niveau zijn. Blader door Hallo volumes in de uitvoer van het script Hallo genoemd.

  ![Linux-bestand herstel blade](./media/backup-azure-restore-files-from-vm/linux-mount-paths.png)
  

## <a name="closing-hello-connection"></a>Hallo-verbinding wordt gesloten

Na identificatie Hallo bestanden en locatie voor de lokale opslag tooa te kopiëren, verwijderen of ontkoppelen Hallo extra stations. toounmount hello stations op Hallo **bestandsherstel** blade in hello Azure-portal, klikt u op **schijven ontkoppelen**.

![Ontkoppel de schijven](./media/backup-azure-restore-files-from-vm/unmount-disks3.png)

Zodra het Hallo-schijven zijn ontkoppeld, krijgt u een bericht laten weten dat goed is verlopen. Het duurt enkele minuten duren voordat Hallo verbinding toorefresh zodat u Hallo schijven kunt verwijderen.

In Linux, nadat Hallo verbinding toohello herstelpunt dat is verbroken, verwijderen Hallo OS niet Hallo bijbehorende koppelpunt paden automatisch. Deze bestaan als 'zwevende' volumes en ze worden weergegeven maar genereert een fout wanneer u toegang schrijftijd Hallo-bestanden. Ze kunnen handmatig worden verwijderd. Hallo-script, wanneer uitgevoerd, worden dergelijke volumes bestaande uit de vorige herstelpunten identificeert en ruimt bij toestemming.

## <a name="special-configurations"></a>Speciale configuraties

### <a name="dynamic-disks"></a>Dynamische schijven

Als volumes waarop span meerdere schijven (spanned en striped volumes) en/of fouttolerante volumes (volumes mirrored en RAID-5) op dynamische schijven hello Azure virtuele machine die een back-up u Hallo uitvoerbaar script niet uitvoeren heeft op Hallo dezelfde virtuele machine. In plaats daarvan Hallo uitvoerbare script uitvoeren op een andere machine met een compatibel besturingssysteem.

### <a name="windows-storage-spaces"></a>Windows-opslagruimten

Windows Storage Spaces is een technologie in Windows-opslag waarmee u toovirtualize opslag. U kunt met Windows Storage Spaces industriestandaard schijven te groeperen in opslaggroepen en vervolgens virtuele schijven, opslagruimten, aangeroepen vanuit Hallo beschikbare ruimte in de opslaggroepen maken.

Als hello Azure virtuele machine die een back-up maakt gebruik van Windows Storage Spaces vervolgens Hallo uitvoerbaar script kan niet worden uitgevoerd op Hallo dezelfde virtuele machine. In plaats daarvan Hallo uitvoerbare script uitvoeren op een andere machine met een compatibel besturingssysteem.

### <a name="lvmraid-arrays"></a>LVM/RAID-Arrays

In Linux, logische volumebeheer (LVM) en/of software zijn RAID-Arrays gebruikte toomanage logische volumes over meerdere schijven. Als een back-up Linux VM Hallo LVM en/of RAID-matrices gebruikt, kunt u Hallo-script niet uitvoeren op Hallo dezelfde virtuele machine. In plaats daarvan Hallo-script uitvoeren op een andere machine met compatibel besturingssysteem en die ondersteuning biedt voor filesystem Hallo een back-up VM.

Hallo scriptuitvoer worden Hallo LVM en/of RAID-matrices schijven en volumes Hallo met Hallo partitietype zoals hieronder wordt weergegeven

   ![Blade Linux LVM uitvoer](./media/backup-azure-restore-files-from-vm/linux-LVMOutput.png)
   
Hallo na de opdrachten hoeft toobe uit te voeren door Hallo gebruiker toobring deze partities online. 

**Voor LVM partities**

```
$ pvs <volume name as shown above in hello script output> 
```
Hiermee worden namen van volume Hallo onder een fysiek volume.

```
$ lvdisplay <volume-group-name from hello pvs command’s results> 
```
Hiermee worden alle logische volumes, namen en de paden in de groep van een volume.

```
$ mount <LV path> </mountpath>
```
toomount hello logische volumes toohello pad van uw keuze.


**Voor RAID-Arrays**

```
$ mdadm –detail –scan
```
Dit geeft details weer over alle raid-schijven. Hallo relevante RAID schijf wordt weergegeven als`/dev/mdm/<RAID array name in hello backed up VM>`

Hallo mount-opdracht gebruiken als Hallo RAID schijf fysieke volumes heeft.
```
$ mount [RAID Disk Path] [/mounthpath]
```

Als deze schijf RAID heeft een andere LVM geconfigureerd in het Volg dezelfde procedure Hallo als hierboven beschreven voor LVM partities met Hallo volumenaam wordt de naam van de Hallo-RAID-schijf

## <a name="troubleshooting"></a>Problemen oplossen

Als u problemen ondervindt tijdens het herstellen van bestanden vanuit Hallo virtuele machines, Controleer Hallo volgende tabel voor meer informatie.

| Foutbericht / Scenario | Mogelijke oorzaak | Aanbevolen actie |
| ------------------------ | -------------- | ------------------ |
| Exe-uitvoer: *uitzondering toohello doel verbinding te maken* |Er is geen script kunnen tooaccess Hallo herstelpunt | Controleer of Hallo machine Hallo toegangsvereisten bovengenoemde vervult|  
|   Exe-uitvoer: *Hallo doel is al aangemeld via een iSCSI-sessie.* |   Hallo script is al uitgevoerd op dezelfde computer en de Hallo stations zijn gekoppeld Hallo |   Hallo-volumes van het herstelpunt Hallo zijn al gekoppeld. Ze kunnen niet worden gekoppeld met dezelfde stationsletters van Hallo Hallo oorspronkelijke VM. Blader door alle beschikbare Hallo-volumes in de Verkenner Hallo voor het bestand |
| Exe-uitvoer: *dit script is ongeldig omdat het Hallo-schijven hebt ontkoppeld via de portal/overschreden Hallo 12 hr limiet. Download een nieuw script vanaf Hallo-portal.* |    Hallo schijven hebt ontkoppeld van het Hallo-portal of Hallo 12 uur is overschreden |  Deze bepaalde exe is nu ongeldig en kan niet worden uitgevoerd. Als u wilt dat tooaccess Hallo-bestanden van die recovery point-in-time, gaat u naar Hallo-portal voor een nieuwe exe-bestand|
| Op Hallo machine waar Hallo exe wordt uitgevoerd: Hallo nieuwe volumes zijn niet ontkoppeld nadat Hallo ontkoppeling knop wordt geklikt |    Hallo iSCSI-initiator op Hallo machine niet reageert/vernieuwen van het doel van de toohello verbinding en onderhouden van Hallo-cache |    Wacht enkele minuten nadat Hallo ontkoppeling knop wordt ingedrukt. Als Hallo nieuwe volumes worden nog steeds niet ontkoppeld, moet u bladeren door alle Hallo volumes. Deze dwingt Hallo initiator toorefresh Hallo verbinding en Hallo volume wordt ontkoppeld met een foutbericht dat Hallo schijf is niet beschikbaar|
| Exe-uitvoer: Script met succes is uitgevoerd, maar 'Nieuwe volumes gekoppeld' wordt niet weergegeven op Hallo scriptuitvoer |   Dit is een tijdelijke fout   | Hallo volumes zou zijn al gekoppeld. Open Verkenner toobrowse. Als u dezelfde machine Hallo voor het uitvoeren van scripts elke keer gebruikt, overweeg Hallo machine opnieuw te starten en Hallo lijst moet worden weergegeven in Hallo daaropvolgende exe wordt uitgevoerd. |
| Linux-specifieke: Er kan geen tooview Hallo gewenst volumes | Hallo OS van Hallo machine waar het Hallo-script wordt uitgevoerd kan onderliggende bestandssysteem Hallo Hallo een back-up VM wordt niet herkend | Controleer is of het Hallo van het herstelpunt crash consistent of bestandsconsistente. Als het bestand consistente, Voer Hallo script op een andere computer waarvan OS Hallo herkent een back-up van de virtuele machine bestandssysteem |
| Windows-specifieke: Er kan geen tooview Hallo gewenst volumes | Hallo schijven zijn gekoppeld, maar Hallo volumes zijn niet geconfigureerd | Identificeren van welkomstscherm schijf management, Hallo extra schijven gerelateerde toohello herstelpunt. Als een van deze schijven offline status kunt u ze online door met de rechtermuisknop op het Hallo-schijf maken en klik op 'Online'|
