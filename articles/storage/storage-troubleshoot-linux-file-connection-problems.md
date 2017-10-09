---
title: problemen met aaaTroubleshoot Azure File storage in Linux | Microsoft Docs
description: Problemen met Azure File storage in Linux
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: genli
ms.openlocfilehash: 3dc537d714244451a5ff8e01f4a27f03873cf2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a>Problemen met Azure File storage in Linux

Dit artikel worden veelvoorkomende problemen die gerelateerde tooMicrosoft Azure File storage zijn wanneer u verbinding vanaf een Linux-clients maakt. Het bevat ook mogelijke oorzaken en oplossingen voor deze problemen.

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a>"[toegang geweigerd] schijfquotum is overschreden" wanneer u probeert een bestand tooopen

U ontvangt een foutbericht weergegeven dat lijkt op de volgende Hallo in Linux:

**<filename>[toegang geweigerd] Schijfquotum is overschreden**

### <a name="cause"></a>Oorzaak

Hallo bovenlimiet van gelijktijdige open ingangen die zijn toegestaan voor een bestand is bereikt.

### <a name="solution"></a>Oplossing

Het aantal gelijktijdige open ingangen Hallo verminderen door te sluiten van een aantal ingangen en probeer Hallo opnieuw. Zie voor meer informatie [controlelijst voor prestaties en schaalbaarheid van Microsoft Azure Storage](storage-performance-checklist.md).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a>Trage bestand tooand kopiëren van Azure File storage in Linux

-   Als u een specifieke i/o-grootte minimumvereiste hebt, raden wij 1 MB te gebruiken, zoals Hallo i/o-grootte voor optimale prestaties.
-   Als u weet dat de uiteindelijke omvang Hallo van een bestand dat u met behulp van schrijfbewerkingen uitbreidt en de software niet compatibiliteitsproblemen ervaren wanneer een unwritten tail op Hallo bestand nullen bevat, klikt u vervolgens de bestandsgrootte Hallo van tevoren in plaats van het maken van een uitbreiding van elke schrijfbewerking instellen schrijven.
-   Hallo rechts copy-methode gebruiken:
    -   Gebruik [AzCopy](storage-use-azcopy.md#file-copy) de overdracht tussen twee bestandsshares.
    -   Gebruik [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) tussen bestandsshares op een on-premises computer.

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a>' Error(112) koppelen: Host is niet beschikbaar ' vanwege een time-out van de nieuwe verbindingen

Een '112' mount-fout treedt op Hallo Linux-client als Hallo client gedurende een lange periode niet actief is geweest. Na de uitgebreide niet-actieve tijd, Hallo-client de verbinding verbreekt en Hallo verbinding een time-out optreedt.  

### <a name="cause"></a>Oorzaak

Hallo-verbinding tot stand kan worden gedurende de volgende redenen Hallo:

-   Communicatie netwerkfouten die voorkomen dat het herstellen van een TCP-verbinding toohello server wanneer de standaardoptie mount 'soft' hello wordt gebruikt
-   Recente opnieuw verbinden met oplossingen die niet aanwezig in oudere kernels zijn

### <a name="solution"></a>Oplossing

Dit probleem opnieuw verbinding te maken in Linux-kernel Hallo is nu opgelost als onderdeel van de volgende wijzigingen Hallo:

- [FIX verbinding toonot smb3-sessie uit te stellen verbinding lang nadat socket opnieuw verbinding maken](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [Echo-service aanroepen onmiddellijk nadat de socket opnieuw verbinding maken](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [CIFS: Een geheugenbeschadiging van de mogelijke tijdens reconnect oplossen](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [CIFS: Los een mogelijke dubbele vergrendeling van mutex tijdens reconnect (voor kernel v4.9 en hoger)](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

Deze wijzigingen kunnen echter niet worden overgezet nog tooall Hallo Linux-distributies. Deze oplossing en andere correcties voor nieuwe verbindingen zijn aangebracht in Hallo populaire Linux kernels te volgen: 4.4.40 4.8.16 en 4.9.1. U kunt deze oplossing ophalen door het upgraden van tooone van deze aanbevolen kernel-versies.

### <a name="workaround"></a>Tijdelijke oplossing

U kunt dit probleem omzeilen door te geven van een harde koppeling. Hallo client toowait wordt gedwongen totdat een verbinding tot stand is gebracht of totdat deze expliciet wordt onderbroken en gebruikte tooprevent fouten vanwege netwerk time-outs kan worden. Deze tijdelijke oplossing kan echter de onbepaalde wachttijd veroorzaken. Voorbereide toostop verbindingen zoals die nodig zijn.

Als u de meest recente kernel-versies toohello niet bijwerken, kunt u dit probleem omzeilen door een bestand in hello Azure-bestandsshare die u tooevery 30 seconden schrijft of minder. Dit moet een schrijfbewerking zoals herschrijven Hallo op gemaakt of gewijzigd datum Hallo-bestand. Anders krijgt u mogelijk de resultaten in het cachegeheugen en uw bewerking mogelijk opnieuw verbinden met Hallo niet activeren.

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a>' Error(115) koppelen: Bezig met bewerking ' bij het koppelen van Azure File storage met behulp van SMB 3.0

### <a name="cause"></a>Oorzaak

Sommige Linux-distributies nog ondersteunen geen versleutelingsfuncties in SMB 3.0 en gebruikers mogelijk foutbericht '115' als ze toomount Azure File storage proberen met behulp van SMB 3.0 vanwege een ontbrekend onderdeel.

### <a name="solution"></a>Oplossing

Coderingsfunctie voor SMB 3.0 voor Linux is geïntroduceerd in 4.11 kernel. Deze functie kunt koppelen van de bestandsshare in Azure vanaf on-premises of andere Azure-regio. Op Hallo moment van publicatie is deze functionaliteit backported tooUbuntu 17.04 en Ubuntu 16,10. Als uw Linux SMB-client geen ondersteuning biedt voor versleuteling, koppelt u Azure File storage met behulp van SMB 2.1 van een Azure Linux VM die zich in hetzelfde datacenter Hallo zoals Hallo File storage-account.

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a>Langzame prestaties van een Azure-bestandsshare die is gekoppeld aan een Linux-VM

### <a name="cause"></a>Oorzaak

Een mogelijke oorzaak van vertragingen bij het opslaan in cache is uitgeschakeld.

### <a name="solution"></a>Oplossing

toocheck of opslaan in cache is uitgeschakeld, zoekt u naar Hallo **cache =** vermelding. 

**Cache = geen** geeft aan dat opslaan in cache is uitgeschakeld.  Koppelen Hallo share met Hallo standaard koppelpunt opdracht of door expliciet toe te voegen Hallo **cache = strikte** optie toohello koppelpunt opdracht tooensure die standaard in het cachegeheugen of 'strict' cache-modus is ingeschakeld.

In sommige gevallen Hallo **serverino** mount-optie kan leiden tot Hallo **ls** opdracht toorun stat tegen elke directory-vermelding. Dit gedrag leidt tot verminderde prestaties wanneer u een grote directory aangeboden. U kunt opties voor het koppelen van Hallo controleren uw **/etc/fstab** post:

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

U kunt ook controleren of de juiste opties hello worden gebruikt door Hallo uitgevoerd **sudo koppelen | grep cifs** opdracht en de uitvoer, zoals de volgende voorbeelduitvoer hello te controleren:

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

Als hello **cache = strikte** of **serverino** optie is niet aanwezig zijn, ontkoppelen en opnieuw koppelen van Azure File storage door Hallo koppelpunt opdracht vanaf Hallo [documentatie](storage-how-to-use-files-linux.md). Vervolgens controleren die Hallo **/etc/fstab** vermelding heeft Hallo juiste opties.

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a>Tijdstempels verloren zijn gegaan bij het kopiëren van bestanden van Windows tooLinux

Op Linux/Unix-platforms Hallo **cp -p** opdracht mislukt als de 1 en 2 bestand eigendom zijn van andere gebruikers.

### <a name="cause"></a>Oorzaak

Hallo vlag force **f** in COPYFILE resulteert in het uitvoeren van **cp -p -f** op Unix. Deze opdracht mislukt ook toopreserve Hallo tijdstempel van Hallo-bestand dat u niet de eigenaar.

### <a name="workaround"></a>Tijdelijke oplossing

Hallo storage accountgebruiker voor het kopiëren van bestanden hello gebruiken:

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.

Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget snel uw probleem is opgelost.
