---
title: 'Azure Backup: toepassingsconsistente back-ups van virtuele Linux-machines | Microsoft Docs'
description: Scripts tooguarantee toepassingsconsistente back-ups tooAzure gebruiken voor uw virtuele Linux-machines. Hallo scripts toepassing alleen tooLinux virtuele machines in een Resource Manager-implementatie; Hallo-scripts niet van toepassing tooWindows VM's of de service manager-implementaties. In dit artikel leert u Hallo stappen voor het configureren van Hallo scripts, inclusief het oplossen van problemen.
services: backup
documentationcenter: dev-center-name
author: anuragmehrotra
manager: shivamg
keywords: App-consistente back-up. toepassingsconsistente virtuele machine van Azure back-up. Back-up van Linux-VM. Azure Backup
ms.assetid: bbb99cf2-d8c7-4b3d-8b29-eadc0fed3bef
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/12/2017
ms.author: anuragm;markgal
ms.openlocfilehash: d557dd973364d79bb4d8ce954f648de835dd345f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-consistent-backup-of-azure-linux-vms-preview"></a>Toepassingsconsistente back-up van Azure Linux VM's (preview)

In dit artikel wordt gesproken over Hallo Linux vooraf script en na script framework en hoe deze gebruikt tootake toepassingsconsistente back-ups van Azure Linux VM's kan zijn.

> [!Note]
> Hallo-script voor vóór en na-framework wordt alleen ondersteund voor Linux Azure Resource Manager geïmplementeerde virtuele machines. Scripts voor consistentie van de toepassing worden niet ondersteund voor Service Manager geïmplementeerde virtuele machines of virtuele machines van Windows.
>

## <a name="how-hello-framework-works"></a>De werking van Hallo-framework

Hallo-framework biedt een optie toorun aangepaste scripts voor vóór en na scripts tijdens het maken van VM-momentopnamen. Vooraf scripts worden uitgevoerd voordat u VM-momentopname Hallo en na scripts worden uitgevoerd onmiddellijk nadat u momentopname Hallo VM. Dit biedt u flexibiliteit toocontrol Hallo uw toepassing en de omgeving tijdens het maken van VM-momentopnamen.

In dit scenario is het belangrijk tooensure toepassingsconsistente VM back-up. Hallo vooraf script kunt aanroepen toepassing systeemeigen API's tooquiesce Hallo IOs en in het geheugen inhoud toohello schijf leegmaken. Dit zorgt ervoor dat momentopname Hallo toepassingsconsistente (dat wil zeggen, wanneer die toepassing hello voordoet Hallo VM wordt opgestart na herstellen). Na script kan worden gebruikt toothaw Hallo IOs. Dit gebeurt met behulp van de toepassing-systeemeigen API's zodat de toepassing hello post-VM-momentopname voor normale bewerkingen kunt hervatten.

## <a name="steps-tooconfigure-pre-script-and-post-script"></a>Stappen tooconfigure script voor vóór en na

1. Meld u in Hallo hoofdmap gebruiker toohello Linux VM die u wilt dat tooback up.

2. Download **VMSnapshotScriptPluginConfig.json** van [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig), en kopieer het toohello **/etc/azure** map op alle Hallo-virtuele machines die u tooback up gaat. Hallo maken **/etc/azure** directory als deze niet al bestaat.

3. Kopieer Hallo script vóór en na voor uw toepassing op alle Hallo virtuele machines die u tooback up plannen. U kunt Hallo scripts tooany locatie op Hallo VM kopiëren. Worden ervoor tooupdate Hallo volledige pad van Hallo scriptbestanden in Hallo **VMSnapshotScriptPluginConfig.json** bestand.

4. Zorg ervoor dat Hallo volgende machtigingen voor deze bestanden:

   - **VMSnapshotScriptPluginConfig.json**: machtiging "600." Bijvoorbeeld alleen 'root' gebruiker 'lezen' en 'schrijven' machtigingen toothis bestand moet hebben en geen gebruiker moet beschikken over machtigingen voor ' uitvoeren'.

   - **Vooraf scriptbestand**: machtiging "700."  Alleen 'root' gebruiker moet bijvoorbeeld 'lezen', 'schrijven' en 'uitvoeren' machtigingen toothis bestand.
  
   - **Na script** machtiging "700." Alleen 'root' gebruiker moet bijvoorbeeld 'lezen', 'schrijven' en 'uitvoeren' machtigingen toothis bestand.

   > [!Important]
   > Hallo framework geeft gebruikers veel stroom. Het is belangrijk dat het is veilig en die alleen 'root' de gebruiker toegang toocritical JSON-script en bestanden heeft.
   > Als vorige Hallo-vereisten zijn niet voldaan, Hallo script niet wordt uitgevoerd. Dit resulteert in het bestand system/crash consistente back-up.
   >

5. Configureer **VMSnapshotScriptPluginConfig.json** zoals hier wordt beschreven:
    - **naam invoegtoepassing**: laat dit veld is of uw scripts werkt mogelijk niet zoals verwacht.

    - **preScriptLocation**: volledige pad van de Hallo van Hallo vooraf script opgeven op Hallo VM die gaat toobe back-up gemaakt.

    - **postScriptLocation**: Geef Hallo volledige pad van Hallo na script op Hallo VM die gaat toobe back-up gemaakt.

    - **preScriptParams**: Hallo optionele parameters die toobe toohello vooraf script doorgegeven moeten bieden. Alle parameters moeten tussen aanhalingstekens, en moeten door komma's gescheiden als er meerdere parameters.

    - **postScriptParams**: Hallo optionele parameters die toobe toohello na script doorgegeven moeten bieden. Alle parameters moeten tussen aanhalingstekens, en moeten door komma's gescheiden als er meerdere parameters.

    - **preScriptNoOfRetries**: Stel Hallo aantal keren Hallo vooraf script moet opnieuw worden geprobeerd, als er een fout voordat het wordt beëindigd is. Nul betekent dat slechts één probeer en geen nieuwe poging als er een storing optreedt.

    - **postScriptNoOfRetries**: Stel Hallo aantal keren Hallo na script moet opnieuw worden geprobeerd, als er een fout voordat het wordt beëindigd is. Nul betekent dat slechts één probeer en geen nieuwe poging als er een storing optreedt.
    
    - **Time-outInSeconden**: afzonderlijke time-outs voor na Hallo vooraf script en Hallo opgeven.

    - **continueBackupOnFailure**: Stel deze waarde te**true** als u wilt dat Azure Backup toofall back tooa system consistent/crashconsistente back-up als script vóór of na mislukt script. Te stellen**false** mislukt Hallo back-up in geval van storing script (behalve wanneer u één schijf VM valt back-up terug toocrash consistent ongeacht deze instelling hebt).

    - **fsFreezeEnabled**: Geef op of de Linux-fsfreeze moet worden aangeroepen tijdens het maken van Hallo VM momentopname tooensure consistentie van het bestandssysteem. We raden u deze instelling ingesteld te**true** tenzij uw toepassing een afhankelijkheid heeft van fsfreeze uitschakelen.

6. Hallo script framework is nu geconfigureerd. Hallo VM-back-up al is geconfigureerd, Hallo volgende back-up Hallo scripts roept als toepassingsconsistente back-up wordt geactiveerd. Als back-up van Hallo VM niet is geconfigureerd, configureert u deze met behulp van [Back-up van virtuele machines in Azure tooRecovery Services-kluizen.](https://docs.microsoft.com/azure/backup/backup-azure-vms-first-look-arm)

## <a name="troubleshooting"></a>Problemen oplossen

Zorg ervoor dat u passende logboekregistratie tijdens het schrijven van uw script voor vóór en na toevoegen en controleer uw script logboeken toofix script problemen. Als u nog steeds problemen bij het uitvoeren van scripts hebt, raadpleegt u toohello volgende tabel voor meer informatie.

| Fout | Foutbericht | Aanbevolen actie |
| ------------------------ | -------------- | ------------------ |
| Pre-ScriptExecutionFailed |Hallo vooraf script heeft een fout, dus mogelijk toepassingsconsistente back-up niet. | Bekijkt hello fout logboeken voor uw script toofix Hallo probleem.|  
|   Post-ScriptExecutionFailed |    Hallo na script heeft een fout die voor de toepassingsstatus gevolgen mogelijk. |  Bekijkt hello fout logboeken voor uw probleem script toofix hello en controleer de status van de toepassing hello. |
| Pre-ScriptNotFound |  Hallo vooraf script is niet gevonden op Hallo locatie die opgegeven in Hallo **VMSnapshotScriptPluginConfig.json** config-bestand. | Zorg ervoor dat dat vooraf script is aanwezig op Hallo-pad dat opgegeven in Hallo config bestand tooensure toepassingsconsistente back-up.|
| Post-ScriptNotFound | Hallo is niet na script gevonden op Hallo locatie die opgegeven in Hallo **VMSnapshotScriptPluginConfig.json** config-bestand. | Zorg ervoor dat dat na script is aanwezig op Hallo-pad dat opgegeven in Hallo config bestand tooensure toepassingsconsistente back-up.|
| IncorrectPluginhostFile | Hallo **Pluginhost** bestand, dat wordt geleverd met Hallo VmSnapshotLinux uitbreiding, is beschadigd, dus het script voor vóór en na kunnen niet worden uitgevoerd en Hallo back-up niet toepassingsconsistente.   | Hallo verwijderen **VmSnapshotLinux** , en er wordt automatisch opnieuw geïnstalleerd met Hallo volgende back-toofix Hallo probleem. |
| IncorrectJSONConfigFile | Hallo **VMSnapshotScriptPluginConfig.json** bestand is onjuist, dus vooraf script en na-script kan niet worden uitgevoerd en Hallo back-up niet toepassingsconsistente. | Hallo-exemplaar van downloaden [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig) en opnieuw configureren. |
| InsufficientPermissionforPre-Script | Voor het uitvoeren van scripts 'root' gebruiker Hallo eigenaar van Hallo-bestand moet zijn en Hallo-bestand moet '700' machtigingen hebben (dat wil zeggen, alleen 'eigenaar' moet 'lezen', 'schrijven' en 'uitvoeringsmachtigingen'). | Zorg ervoor dat de gebruiker in 'root' Hallo 'eigenaar' van het scriptbestand Hallo is en dat alleen 'eigenaar' 'leesmachtigingen heeft', 'schrijven' en 'uitvoeren'. |
| InsufficientPermissionforPost-Script | Voor het uitvoeren van scripts moet hoofdgebruiker Hallo eigenaar van Hallo-bestand en Hallo-bestand moet '700' machtigingen hebben (dat wil zeggen, alleen 'eigenaar' moet 'lezen', 'schrijven' en 'uitvoeringsmachtigingen'). | Zorg ervoor dat de gebruiker in 'root' Hallo 'eigenaar' van het scriptbestand Hallo is en dat alleen 'eigenaar' 'leesmachtigingen heeft', 'schrijven' en 'uitvoeren'. |
| Pre-ScriptTimeout | Hallo uitvoering van Hallo toepassingsconsistente back-up vooraf script time-out. | Hallo script controleren en verhogen Hallo time-out in Hallo **VMSnapshotScriptPluginConfig.json** -bestand dat zich bevindt op **/etc/azure**. |
| Post-ScriptTimeout | Er is een time-out opgetreden bij het uitvoeren van de Hallo van Hallo toepassingsconsistente back-na-script. | Hallo script controleren en verhogen Hallo time-out in Hallo **VMSnapshotScriptPluginConfig.json** -bestand dat zich bevindt op **/etc/azure**. |

## <a name="next-steps"></a>Volgende stappen
[Recovery Services-kluis voor VM-back-tooa configureren](https://docs.microsoft.com/azure/backup/backup-azure-arm-vms)
