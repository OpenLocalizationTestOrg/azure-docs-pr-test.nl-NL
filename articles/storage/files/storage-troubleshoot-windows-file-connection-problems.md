---
title: problemen met aaaTroubleshoot Azure File storage in Windows | Microsoft Docs
description: Problemen met Azure File storage in Windows
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
ms.date: 06/28/2017
ms.author: genli
ms.openlocfilehash: 19529d8af5d98790e2e381cd21ad4d0284acb124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a>Problemen met Azure File storage in Windows

Dit artikel worden veelvoorkomende problemen die gerelateerde tooMicrosoft Azure File storage zijn wanneer u verbinding vanaf een Windows-clients maakt. Het bevat ook mogelijke oorzaken en oplossingen voor deze problemen. Bovendien toohello probleemoplossing stappen in dit artikel, kunt u ook [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) om ervoor te zorgen dat Hallo Windows clientomgeving juist vereisten heeft. AzFileDiagnostics automatiseert detectie van de meeste Hallo symptomen die in dit artikel worden vermeld en helpt bij het instellen van uw omgeving tooget optimale prestaties. U kunt deze informatie ook vinden in Hallo [Azure-bestandsshares probleemoplosser](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) stappen tooassist en waarmee u problemen verbinden/toewijzing/koppelen Azure bestandsshares.


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a>Fout 53, fout 67 of fout 87 wanneer u koppelen of ontkoppelen van een Azure-bestandsshare

Wanneer u een bestandsshare van on-premises of vanuit een ander datacenter toomount, verschijnt er Hallo volgende fouten:

- Systeemfout 53 is opgetreden. Hallo netwerkpad is niet gevonden.
- Systeemfout 67 is opgetreden. Hallo-netwerknaam kan niet worden gevonden.
- Systeemfout 87 is opgetreden. Hallo-parameter is onjuist.

### <a name="cause-1-unencrypted-communication-channel"></a>Oorzaak 1: De niet-versleutelde communicatiekanaal

Uit veiligheidsoverwegingen Hallo verbindingen tooAzure bestandsshares worden geblokkeerd als Hallo communicatiekanaal is niet versleuteld en Hallo verbinding wordt niet geprobeerd uit hetzelfde datacenter waar hello Azure-bestandsshares zich bevinden. Alleen als van de gebruiker Hallo clientbesturingssysteem SMB-versleuteling ondersteunt wordt de communicatie kanaalversleuteling geleverd.

Windows 8, Windows Server 2012 en latere versies van elk systeem te onderhandelen over aanvragen met SMB 3.0, die ondersteuning biedt voor versleuteling.

### <a name="solution-for-cause-1"></a>Oplossing voor oorzaak 1

Verbinding maken vanaf een client die een van de volgende Hallo biedt:

- Hallo voldoet aan de vereisten van Windows 8 en Windows Server 2012 of hoger
- Verbinding van een virtuele machine in Hallo dezelfde datacenter zoals Azure storage-account dat wordt gebruikt voor het Azure-bestandsshare Hallo Hallo

### <a name="cause-2-port-445-is-blocked"></a>2 oorzaak: Poort 445 is geblokkeerd

Systeemfout 53 of Systeemfout 67 kan zich voordoen als de poort 445 uitgaande communicatie tooan Azure File storage datacenter wordt geblokkeerd. toosee hello samenvatting van internetproviders die toestaan of weigeren van toegang via poort 445, gaat u te[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).

toounderstand of dit de reden Hallo achter 'Systeemfout 53' het Hallo-bericht is, kunt u Portqry tooquery hello TCP:445 eindpunt. Als Hallo TCP:445 eindpunt wordt weergegeven als gefilterd, is Hallo TCP-poort geblokkeerd. Hier volgt een voorbeeldquery:

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

Als TCP-poort 445 wordt geblokkeerd door een regel langs Hallo netwerkpad, ziet u Hallo volgende uitvoer:

  `TCP port 445 (microsoft-ds service): FILTERED`

Voor meer informatie over het toouse Portqry, Zie [beschrijving van Hallo Portqry.exe opdrachtregelprogramma](https://support.microsoft.com/help/310099).

### <a name="solution-for-cause-2"></a>Oplossing voor oorzaak 2

Werken met uw IT-afdeling tooopen poort 445 uitgaand te[Azure IP-bereiken](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="cause-3-ntlmv1-is-enabled"></a>3 oorzaak: NTLMv1 is ingeschakeld.

Systeemfout 53 of systeemfout 87 kan optreden als NTLMv1-communicatie is ingeschakeld op Hallo-client. Azure File storage ondersteunt alleen NTLMv2-authenticatie. NTLMv1 ingeschakeld met maakt een minder veilige client. Daarom is communicatie geblokkeerd voor Azure File storage. 

toodetermine of dit Hallo oorzaak van Hallo fout, Controleer of dat Hallo volgende subsleutel in het register is ingesteld tooa waarde van 3:

**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**

Zie voor meer informatie, Hallo [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) onderwerp op TechNet.

### <a name="solution-for-cause-3"></a>Oplossing voor oorzaak 3

Hallo terugkeren **LmCompatibilityLevel** toohello standaardwaarde 3 in de volgende registersubsleutel Hallo waarde:

  **HKLM\SYSTEM\CurrentControlSet\Control\Lsa**

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a>Fout 1816 ' Onvoldoende quota beschikbaar tooprocess met deze opdracht is ' wanneer u Azure-bestandsshare tooan kopiëren

### <a name="cause"></a>Oorzaak

Fout 1816 treedt op wanneer u bereiken Hallo bovenlimiet van gelijktijdige open ingangen die zijn toegestaan voor een bestand op Hallo computer waar Hallo-bestandsshare is wordt gekoppeld.

### <a name="solution"></a>Oplossing

Aantal gelijktijdige open ingangen Hallo verminderen door te sluiten van een aantal ingangen en probeer het vervolgens opnieuw. Zie voor meer informatie [controlelijst voor prestaties en schaalbaarheid van Microsoft Azure Storage](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a>Trage bestand tooand kopiëren van Azure File storage in Windows

U kunt trage prestaties tegenkomen wanneer u tootransfer bestanden toohello Azure File-service probeert.

- Als u een specifieke i/o-grootte minimumvereiste hebt, raden wij 1 MB te gebruiken, zoals Hallo i/o-grootte voor optimale prestaties.
-   Als u weet Hallo uiteindelijke omvang van een bestand dat u met uitbreiden schrijft en uw software geen compatibiliteitsproblemen wanneer hello unwritten tail op Hallo-bestand bevat nullen, vervolgens set Hallo bestandsgrootte van tevoren in plaats van elke schrijfbewerking waardoor het terugschrijven van een uitbreiden.
-   Hallo rechts copy-methode gebruiken:
    -   Gebruik [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) de overdracht tussen twee bestandsshares.
    -   Gebruik [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) tussen bestandsshares op een on-premises computer.

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a>Overwegingen voor Windows 8.1 of Windows Server 2012 R2

Voor clients met Windows 8.1 of Windows Server 2012 R2, zorg ervoor dat Hallo [KB3114025](https://support.microsoft.com/help/3114025) hotfix is geïnstalleerd. Deze hotfix verbetert de prestaties van create Hallo en ingangen sluit.

Hallo script toocheck te volgen of Hallo hotfix is geïnstalleerd, kunt u uitvoeren:

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

Als hotfix is geïnstalleerd, hello volgende uitvoer weergegeven:

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> Windows Server 2012 R2-afbeeldingen in Azure Marketplace hebben hotfix KB3114025 standaard geïnstalleerd, vanaf December 2015.

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a>Er is geen map met een stationsletter in **Mijn Computer**

Als u een Azure-bestandsshare als een beheerder met behulp van net gebruik toewijst, Hallo share toobe weergegeven ontbreekt.

### <a name="cause"></a>Oorzaak

Windows Verkenner wordt niet uitgevoerd als beheerder. Als u net gebruik van een administratieve opdrachtprompt uitvoert, wordt het Hallo-netwerkstation toewijzen als beheerder. Omdat netwerkstations gebruikersgerichte zijn, wordt Hallo-gebruikersaccount dat is aangemeld Hallo stations niet weergegeven als ze worden gekoppeld onder een ander gebruikersaccount.

### <a name="solution"></a>Oplossing
Hallo-share koppelen vanuit een opdrachtregel niet-beheerders. U kunt ook kunt u [dit TechNet-onderwerp](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** registerwaarde.

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a>Opdracht net use mislukt als Hallo-opslagaccount een slash bevat

### <a name="cause"></a>Oorzaak

de opdracht net use Hello wordt een slash (/) geïnterpreteerd als een opdrachtregeloptie. Als de naam van uw gebruikersaccount wordt gestart met een slash, mislukt de stationstoewijzing Hallo.

### <a name="solution"></a>Oplossing

U kunt gebruiken Hallo toowork rond Hallo probleem stappen te volgen:

- Hallo volgende PowerShell-opdracht uitvoeren:

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  Vanuit een batchbestand kunt u Hallo-opdracht uitvoeren op deze manier:

  `Echo new-smbMapping ... | powershell -command –`

- Dubbele aanhalingstekens rond Hallo sleutel toowork om dit probleem--geplaatst tenzij de schuine streep Hallo Hallo eerste teken. Als het, Hallo interactieve modus gebruiken en voer uw wachtwoord afzonderlijk of opnieuw genereren van uw sleutels tooget een sleutel die niet met een slash begint.

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a>Toepassing of service heeft geen toegang tot een gekoppelde Azure File storage-station

### <a name="cause"></a>Oorzaak

Schijven zijn per gebruiker gekoppeld. Als uw toepassing of service wordt uitgevoerd onder een ander gebruikersaccount dan Hallo die gekoppeld station hello, ziet Hallo toepassing hello station niet.

### <a name="solution"></a>Oplossing

Gebruik een van de volgende oplossingen Hallo:

-   Hallo-station koppelen vanuit Hallo hetzelfde gebruikersaccount dat de toepassing hello bevat. U kunt een hulpprogramma zoals PsExec gebruiken.
- Hallo opslagaccountnaam en de sleutel in Hallo gebruiker naam en het wachtwoord parameters van de opdracht net use Hallo doorgeven.

Nadat u deze instructies opvolgt, Hallo volgende foutbericht wordt weergegeven tijdens het uitvoeren van net gebruiken voor Hallo system/Netwerkservice-account kan worden weergegeven: 'Systeemfout 1312 is opgetreden. De sessie van een opgegeven gebruiker bestaat niet. Het is mogelijk al beëindigd." Als dit het geval is, zorg ervoor dat Hallo-gebruikersnaam die wordt doorgegeven toonet gebruik domeingegevens bevat (bijvoorbeeld: ' [opslagaccountnaam]. file.core.windows .net ').

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a>'U kopieert een bestand tooa doel geen versleuteling ondersteunt' fout

Als een bestand wordt gekopieerd via Hallo netwerk, is Hallo-bestand op Hallo broncomputer verzonden als leesbare tekst en opnieuw versleuteld op Hallo bestemming te ontsleutelen. Echter, ziet u mogelijk Hallo volgende fout wanneer u een versleuteld bestand toocopy probeert: "Kopieert u Hallo tooa bestemming die geen ondersteuning biedt voor versleuteling."

### <a name="cause"></a>Oorzaak
Dit probleem kan optreden als u van Encrypting File System (EFS gebruikmaakt). BitLocker-versleuteling-bestanden kunnen worden gekopieerd tooAzure File storage. Azure File storage biedt echter geen ondersteuning voor NTFS EFS.

### <a name="workaround"></a>Tijdelijke oplossing
een bestand via Hallo netwerk toocopy, u moet eerst worden gedecodeerd. Een van de volgende methoden hello gebruiken:

- Gebruik Hallo **kopiëren /d** opdracht. Kunt u Hallo versleuteld opgeslagen als de ontsleutelde bestanden op de bestemming Hallo toobe bestanden.
- Stel Hallo volgende registersleutel:
  - Pad = HKLM\Software\Policies\Microsoft\Windows\System
  - Waarde type DWORD =
  - Naam CopyFileAllowDecryptedRemoteDestination =
  - Waarde = 1

Let die instelling Hallo-registersleutel is van invloed op alle kopieerbewerkingen die zijn aangebracht toonetwork shares.

## <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.
Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget snel uw probleem is opgelost.
