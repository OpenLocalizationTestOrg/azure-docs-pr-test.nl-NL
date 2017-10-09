---
title: aaaAzure schijfversleuteling voor Windows en Linux IaaS VM's | Microsoft Docs
description: Dit artikel bevat een overzicht van Microsoft Azure Disk Encryption for Windows en Linux IaaS VM's.
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a>Azure Disk Encryption for Windows and Linux IaaS VM 's
Microsoft Azure wordt ten zeerste doorgevoerd tooensuring uw privacy van gegevens, onafhankelijkheid van gegevens en kunt u uw Azure gehoste toocontrol gegevens via een reeks technologieën voor geavanceerde tooencrypt, beheren en beheren van versleutelingssleutels besturingselement & audit toegang van gegevens. Dit biedt Azure-klanten Hallo flexibiliteit toochoose Hallo oplossing die het beste voldoet aan de behoeften van hun bedrijf. In dit artikel, we vindt u tooa nieuwe technologieoplossing 'Azure Disk Encryption for Windows and Linux IaaS VM' toohelp beveiligen en uw toomeet gegevens beveiligt uw organisatie beveiliging en naleving verplichtingen. Hallo artikel biedt gedetailleerde richtlijnen voor hoe toouse-hello Azure disk encryption functies zoals Hallo ondersteund scenario's en Hallo gebruikerservaringen.

> [!NOTE]
> Bepaalde aanbevelingen mogelijk meer gegevens, netwerk of compute-Resourcegebruik, wat leidt tot extra kosten in licentie of abonnement.

## <a name="overview"></a>Overzicht
Azure Disk Encryption is een nieuwe functie waarmee u uw Windows- en Linux IaaS-schijven voor virtuele machine versleutelen. Azure Disk Encryption maakt gebruik van Hallo industrie-initiatief [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) functie van Windows en Hallo [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) functie van Linux tooprovide volumeversleuteling voor hello OS- en gegevensschijven Hallo. Hallo-oplossing is geïntegreerd met [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp u controleren en beheren van Hallo schijfversleuteling sleutels en geheimen in uw abonnement sleutelkluis. Hallo oplossing zorgt er ook voor dat alle gegevens op schijven van de virtuele machine Hallo zijn versleuteld in rust in uw Azure-opslag.

Versleuteling van de schijf van Azure voor Windows en Linux IaaS VM's wordt nu **algemene beschikbaarheid** in alle openbare Azure-regio en AzureGov regio's voor de standaard virtuele machines en virtuele machines met premium-opslag.

### <a name="encryption-scenarios"></a>Versleuteling scenario 's
Hello Azure Disk Encryption-oplossing ondersteunt Hallo klant scenario's te volgen:

* Schakel versleuteling in op de nieuwe IaaS VM's die worden gemaakt op basis van vooraf zijn versleuteld VHD- en versleutelingssleutels
* Schakel versleuteling in op nieuwe gemaakt op basis van installatiekopieën van Hallo ondersteund galerie van Azure IaaS VM 's
* Schakel versleuteling in op bestaande IaaS virtuele machines die worden uitgevoerd in Azure
* Schakel versleuteling in op IaaS VM's van Windows
* Versleuteling op gegevensstations voor Linux IaaS VM's uitschakelen
* Versleuteling van beheerde schijf virtuele machines inschakelen
* Instellingen voor codering van een bestaande versleutelde niet premium-opslag virtuele machine bijwerken
* Back-up en herstel van versleutelde virtuele machines, versleuteld met sleutelcodering sleutel

Hallo-oplossing ondersteunt Hallo volgen scenario's voor IaaS VM's wanneer ze zijn ingeschakeld in Microsoft Azure:

* Integratie met Azure Sleutelkluis
* Standard-laag VMs: [A, D, DS, G, GS, F en enzovoort reeks IaaS VM's](https://azure.microsoft.com/pricing/details/virtual-machines/)
* Versleuteling inschakelen voor Windows en Linux IaaS VM's en beheerde schijf VM's van Hallo ondersteund galerie van Azure-installatiekopieën
* Versleuteling op besturingssysteem en stations voor Windows IaaS VM's en beheerde schijf-VM's uitschakelen
* Versleuteling op gegevensstations voor Linux IaaS VM's en beheerde schijf-VM's uitschakelen
* Schakel versleuteling in op IaaS VM's met Windows Client-besturingssysteem
* Schakel versleuteling in op volumes met koppelpunten paden
* Schakel versleuteling in op Linux VM's zijn geconfigureerd met schijf striping (RAID) met behulp van mdadm
* Schakel versleuteling in op de virtuele Linux-machines met behulp van LVM voor gegevensschijven
* Schakel versleuteling in op Windows VM's zijn geconfigureerd met opslagruimten
* Instellingen voor codering van een bestaande versleutelde niet premium-opslag virtuele machine bijwerken
* Alle openbare Azure en AzureGov regio's worden ondersteund

Hallo-oplossing biedt geen ondersteuning voor Hallo volgen scenario's, functies en -technologie:

* Basisstaffel IaaS VM 's
* Het uitschakelen van Linux IaaS VM's op een station OS versleuteling
* Het uitschakelen van versleuteling op een gegevensstation als Hallo OS station wordt versleuteld voor Linux Iaas VM 's
* IaaS VM's die zijn gemaakt met behulp van Hallo-methode voor het maken van klassieke VM
* Schakel versleuteling in op Windows en Linux-IaaS VM's klanten aangepaste installatiekopieën wordt niet ondersteund. Enccryption inschakelen op Linux-besturingssysteem voor LVM schijf wordt momenteel niet ondersteund. Deze ondersteuning wordt binnenkort worden geleverd.
* Integratie met uw on-premises Key Management Service
* Azure Files (gedeelde bestandssysteem), Network File System (NFS), dynamische volumes en virtuele machines van Windows die zijn geconfigureerd met software gebaseerde RAID-systemen
* Back-up en herstel van versleutelde virtuele machines, zonder sleutelcodering sleutel is gecodeerd.
* Instellingen voor codering van een bestaande versleutelde premium-opslag VM bijwerken.

> [!NOTE]
> Back-up en herstel van versleutelde virtuele machines wordt alleen ondersteund voor virtuele machines die zijn versleuteld met Hallo KEK-configuratie. Dit wordt niet ondersteund op virtuele machines die zijn versleuteld zonder KEK-sleutel. KEK-sleutel is een optionele parameter waarmee de VM-versleuteling. Deze ondersteuning is binnenkort beschikbaar.
> Bijwerken van instellingen voor codering van een bestaande versleutelde premium-opslag virtuele machine worden niet ondersteund. Deze ondersteuning is binnenkort beschikbaar.

### <a name="encryption-features"></a>Coderingsfuncties
Wanneer u inschakelen en implementeren van Azure Disk Encryption voor Azure IaaS VM's, zijn hello volgende mogelijkheden ingeschakeld, afhankelijk van Hallo configuratie die is opgegeven:

* Versleuteling van Hallo OS volume tooprotect Hallo opstartvolume in rust in uw opslagruimte
* Versleuteling van gegevens volumes tooprotect Hallo hoeveelheden gegevens in rust in uw opslagruimte
* Het uitschakelen van versleuteling op Hallo OS en gegevens schijven voor Windows IaaS VM 's
* Versleuteling van gegevens Hallo uitschakelen schijven voor Linux IaaS VM's (alleen als het besturingssysteem IS niet versleuteld station)
* Hallo versleutelingssleutels en geheimen in uw abonnement sleutelkluis beveiligen
* Hallo coderingsstatus van Hallo Reporting versleuteld IaaS VM
* Verwijderen van configuratie-instellingen voor schijf-codering van Hallo IaaS virtuele machine
* Back-up en herstel van versleutelde virtuele machines met behulp van hello Azure Backup-service

> [!NOTE]
> Back-up en herstel van versleutelde virtuele machines wordt alleen ondersteund voor virtuele machines die zijn versleuteld met Hallo KEK-configuratie. Dit wordt niet ondersteund op virtuele machines die zijn versleuteld zonder KEK-sleutel. KEK-sleutel is een optionele parameter waarmee de VM-versleuteling.

Azure Disk Encryption voor IaaS VMS voor Windows en Linux-oplossing omvat:

* Hallo schijfversleuteling extensie voor Windows.
* Hallo schijfversleuteling extensie voor Linux.
* Hallo-schijfversleuteling PowerShell-cmdlets.
* Hallo schijfversleuteling cmdlets van Azure-opdrachtregelinterface (CLI).
* Hallo-schijfversleuteling Azure Resource Manager-sjablonen.

Hello Azure Disk Encryption oplossing wordt ondersteund op IaaS VM's met Windows of Linux-besturingssysteem. Zie voor meer informatie over de besturingssystemen ondersteund Hallo Hallo 'vereisten' sectie.

> [!NOTE]
> Er zijn geen extra kosten voor het versleutelen van VM-schijven met Azure Disk Encryption.

### <a name="value-proposition"></a>Waardevoorstel
Wanneer u hello Azure Disk Encryption-management-oplossing toepast, kunt u voldoen aan Hallo bedrijfsbehoeften te volgen:

* IaaS VM's worden beveiligd in rust, omdat u de gestandaardiseerde technologie tooaddress organisatie beveiliging en naleving versleutelingsvereisten kunt gebruiken.
* Opstarten van IaaS VM's onder de klant beheerde sleutel en beleid en u kunt hun gebruik in de sleutelkluis controleren.

### <a name="encryption-workflow"></a>Codering-werkstroom
schijfversleuteling tooenable voor Windows en Linux-machines Hallo te volgen:

1. Kies een versleutelingsscenario uit Hallo voorafgaand aan scenario's voor versleuteling.
2. Opt-in tooenabling schijfversleuteling via hello Azure Disk Encryption Resource Manager-sjabloon, PowerShell-cmdlets of de opdracht CLI en Hallo versleuteling configuratie opgeven.

   * Hallo klant versleuteld VHD scenario Hallo versleuteld VHD tooyour storage-account en Hallo encryption key wezenlijke tooyour sleutelkluis te uploaden. Vervolgens opgeven configuratie Hallo-tooenable versleuteling op een nieuwe IaaS VM.
   * Nieuwe virtuele machines die zijn gemaakt van Hallo Marketplace en bestaande virtuele machines die al worden uitgevoerd in Azure, bieden configuratie Hallo-tooenable versleuteling op Hallo IaaS VM.

3. Verleen toegang toohello Azure-platform tooread Hallo versleutelingssleutel materiaal (versleutelingssleutels BitLocker voor Windows-systemen) en de wachtwoordzin voor Linux van uw sleutelkluis tooenable versleuteling op Hallo IaaS VM.

4. Geef hello Azure Active Directory (Azure AD) toepassing identiteit toowrite Hallo encryption key wezenlijke tooyour sleutelkluis. In dat geval schakelt u versleuteling op Hallo IaaS VM voor Hallo scenario's die zijn vermeld in stap 2.

5. Azure VM-servicemodel Hallo bijgewerkt met versleuteling en Hallo sleutelkluis configuratie en stelt uw versleutelde VM.

 ![Microsoft Antimalware in Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a>Werkstroom voor ontsleuteling
schijfversleuteling toodisable voor IaaS VM's voltooid Hallo op hoog niveau stappen te volgen:

1. Kies toodisable-versleuteling (decodering) op een actieve IaaS VM in Azure via hello Azure Disk Encryption Resource Manager-sjabloon of PowerShell-cmdlets en Hallo ontsleuteling configuratie opgeven.

 Deze stap schakelt versleuteling van Hallo OS of Hallo gegevensvolume of beide op Hallo Windows IaaS VM uitgevoerd. Echter, zoals vermeld in de vorige sectie hello, uitschakelen van Linux-besturingssysteem schijfversleuteling wordt niet ondersteund. Hallo ontsleuteling stap is alleen toegestaan voor gegevensstations op virtuele Linux-machines, zolang Hallo besturingssysteemschijf is niet versleuteld.
2. Azure-updates Hallo VM-servicemodel en Hallo IaaS VM ontsleutelde gemarkeerd. Hallo-inhoud van Hallo VM zijn niet langer in rust versleuteld.

> [!NOTE]
> Hallo disable-codering bewerking worden niet verwijderd voor uw kluis en Hallo encryption key sleutelmateriaal (versleutelingssleutels BitLocker voor Windows-systemen) of de wachtwoordzin voor Linux.
 > Het uitschakelen van Linux OS schijf-versleuteling wordt niet ondersteund. Hallo ontsleuteling stap is alleen toegestaan voor gegevensstations op virtuele Linux-machines.
Het uitschakelen van de schijf van gegevensversleuteling voor Linux wordt niet ondersteund als Hallo OS station wordt versleuteld.

## <a name="prerequisites"></a>Vereisten
Voordat u Azure Disk Encryption op Azure IaaS VM's voor Hallo ondersteund scenario's die zijn beschreven in de sectie 'Overzicht' hello inschakelen, Zie Hallo volgende vereisten:

* U moet een geldige actief Azure-abonnement toocreate resources in Azure in Hallo ondersteunde regio's hebben.
* Azure Disk Encryption wordt ondersteund op de volgende versies van Windows Server Hallo: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 en Windows Server 2016.
* Azure Disk Encryption wordt ondersteund op Windows-clientversies na Hallo: Windows 8 client en Windows 10-client.

> [!NOTE]
> Voor Windows Server 2008 R2, moet u .NET Framework 4.5 is geïnstalleerd voordat u Azure-versleuteling inschakelen hebben. U kunt deze installeren via Windows Update door Hallo optionele update Microsoft .NET Framework 4.5.2 voor Windows Server 2008 R2 x64 64-systemen te installeren ([KB2901983](https://support.microsoft.com/kb/2901983)).

* Azure Disk Encryption wordt ondersteund op Hallo galerie van Azure te volgen op basis van Linux-server distributies en versies:

| Linux-distributie | Versie | Type van het volume voor de versleuteling wordt ondersteund|
| --- | --- |--- |
| Ubuntu | 16.04-DAGELIJKS-TNS | Besturingssysteem en schijf |
| Ubuntu | 14.04.5-DAILY-LTS | Besturingssysteem en schijf |
| Ubuntu | 12.10 | Gegevensschijf |
| Ubuntu | 12.04 | Gegevensschijf |
| RHEL | 7.3 | Besturingssysteem en schijf |
| RHEL | 7.2 | Besturingssysteem en schijf |
| RHEL | 6.8 | Besturingssysteem en schijf |
| RHEL | 6.7 | Gegevensschijf |
| CentOS | 7.3 | Besturingssysteem en schijf |
| CentOS | 7.2n | Besturingssysteem en schijf |
| CentOS | 6.8 | Besturingssysteem en schijf |
| CentOS | 7.1 | Gegevensschijf |
| CentOS | 7.0 | Gegevensschijf |
| CentOS | 6.7 | Gegevensschijf |
| CentOS | 6.6 | Gegevensschijf |
| CentOS | 6.5 | Gegevensschijf |
| openSUSE | 13.2 | Gegevensschijf |
| SLES | 12 SP1 | Gegevensschijf |
| SLES | 12-SP1 (Premium) | Gegevensschijf |
| SLES | HPC 12 | Gegevensschijf |
| SLES | 11-SP4 (Premium) | Gegevensschijf |
| SLES | 11 SP4 | Gegevensschijf |

* Azure Disk Encryption is vereist dat uw sleutelkluis en de virtuele machines zich in Hallo dezelfde bevinden Azure-regio en -abonnement.

> [!NOTE]
> Hallo-resources configureren in afzonderlijke regio's zorgt ervoor dat een fout opgetreden bij het inschakelen van hello Azure Disk Encryption functie.

* tooset omhoog en uw sleutelkluis configureren voor Azure Disk Encryption, Zie de sectie **instellen boven en uw sleutelkluis configureren voor Azure Disk Encryption** in Hallo *vereisten* sectie van dit artikel.
* tooset omhoog en Azure AD-toepassing in Azure Active directory configureren voor Azure Disk Encryption, Zie de sectie **hello Azure AD-toepassing in Azure Active Directory instellen** in Hallo *vereisten* sectie van dit artikel.
* tooset omhoog en Hallo sleutelkluis toegangsbeleid voor de toepassing hello Azure AD configureren, Zie de sectie **hello sleutelkluis-beleid instellen voor de toepassing hello Azure AD** in Hallo *vereisten* sectie in dit artikel.
* tooprepare een Windows-VHD vooraf zijn versleuteld, Zie de sectie **voorbereiden van een vooraf zijn versleuteld Windows VHD** in Hallo *bijlage*.
* tooprepare een vooraf zijn versleuteld Linux VHD, Zie de sectie **voorbereiden van een vooraf zijn versleuteld Linux VHD** in Hallo *bijlage*.
* Hello Azure-platform moet toegang toohello versleutelingssleutels of geheimen in uw sleutelkluis toomake ze beschikbaar toohello virtuele machine wanneer deze wordt opgestart en Hallo virtuele machine OS volume ontsleutelt. toogrant machtigingen tooAzure platform, set Hallo **EnabledForDiskEncryption** eigenschap in de sleutelkluis Hallo. Zie voor meer informatie **instellen boven en uw sleutelkluis configureren voor Azure Disk Encryption** in Hallo bijlage.
* Uw sleutelkluis geheim en de KEK-URL's moeten samengestelde zijn. Azure zorgt ervoor dat deze beperking versiebeheer. Zie Hallo volgen voorbeelden voor geldige geheim en KEK-URL's:

  * Voorbeeld van een geldige URL geheime: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*
  * Voorbeeld van een geldige KEK-URL: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*

* Azure Disk Encryption biedt geen ondersteuning voor het opgeven van poortnummers als onderdeel van de sleutelkluis geheimen en KEK-URL's. Zie voor voorbeelden van niet-ondersteunde en ondersteunde sleutelkluis-URL's Hallo volgende:

  * Onaanvaardbaar sleutelkluis-URL *https://contosovault.vault.azure.net:443/geheimen/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*
  * Acceptabele sleutelkluis-URL: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*

* tooenable hello Azure Disk Encryption functie Hallo IaaS VM's moet voldoen aan Hallo netwerkvereisten endpoint-configuratie te volgen:
  * een token tooconnect tooyour sleutelkluis, Hallo IaaS VM tooget moet kunnen tooconnect tooan Azure Active Directory-eindpunt \[login.microsoftonline.com\].
  * toowrite hello versleuteling sleutels tooyour sleutelkluis, Hallo IaaS VM moet kunnen tooconnect toohello sleutelkluis-eindpunt.
  * Hallo IaaS VM moet kunnen tooconnect tooan Azure storage-eindpunt dat hosts Hallo extensie Azure-opslagplaats en Azure storage-account dat hosts Hallo VHD-bestanden.

  > [!NOTE]
  > Als uw beveiligingsbeleid beperkt de toegang van Azure Virtual machines toohello Internet, kunt u oplossen Hallo voorafgaand aan de URI en configureren van een specifieke regel tooallow uitgaande verbinding toohello IP-adressen.
  >
  >tooconfigure en toegang tot Azure Key Vault achter een firewall (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)

* Hallo meest recente versie van Azure PowerShell SDK versie tooconfigure Azure Disk Encryption gebruiken. Download de nieuwste versie Hallo van [Azure PowerShell-versie](https://github.com/Azure/azure-powershell/releases)

 > [!NOTE]
  > Azure Disk Encryption wordt niet ondersteund op [Azure PowerShell SDK-versie 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016). Als er een fout gerelateerd toousing Azure PowerShell 1.1.0, Zie [Azure schijf versleuteling fout gerelateerde tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).

* toorun willekeurige opdracht van de Azure CLI en deze koppelen aan uw Azure-abonnement, moet u eerst Azure CLI installeren:
  * tooinstall Azure CLI en deze koppelen aan uw Azure-abonnement, Zie [hoe tooinstall en configureren van Azure CLI](../cli-install-nodejs.md).
  * Zie toouse Azure CLI voor Mac, Linux en Windows gebruiken met Azure Resource Manager [Azure CLI-opdrachten in de modus Resource Manager](../virtual-machines/azure-cli-arm-commands.md).

* Bij het versleutelen van een beheerde schijf is een momentopname van Hallo beheerd schijf of een back-up van schijf Hallo buiten Azure Disk Encryption voorafgaande tooenabling versleuteling verplicht vereiste tootake.  Zonder een back-up in plaats kan een onverwachte fout opgetreden tijdens het versleutelen weergeven Hallo schijf en de VM toegankelijk zijn zonder een hersteloptie.  Set AzureRmVMDiskEncryptionExtension momenteel geen back-up beheerde schijven en wordt fout als op een beheerde schijf gebruikt, tenzij het Hallo - skipVmBackup parameter is opgegeven.  Deze parameter is onveilige toouse tenzij buiten Azure Disk Encryption al een back-up is gemaakt.   Wanneer het Hallo - skipVmBackup parameter wordt opgegeven, wordt Hallo cmdlet een back-ups van eerdere tooencryption van Hallo beheerde schijf niet maken.  Daarom wordt het beschouwd als een verplichte vereisten toomake zeker van te zijn dat een back-up van de beheerde schijf Hallo die VM bevindt zich in de plaats voorafgaande tooenabling Azure Disk Encryption als herstel hoger is vereist.  
> [!NOTE]
 > Hallo - skipVmBackup parameter mag nooit worden gebruikt tenzij een momentopname of een back-up al is gemaakt buiten Azure Disk Encryption. 

* Hallo BitLocker externe-sleutelbeveiliging Hello Azure Disk Encryption oplossing gebruikt voor IaaS VM's van Windows. Push Groepsbeleid dat TPM beveiligingen afdwingen voor domein gekoppelde virtuele machines, niet. Zie voor meer informatie over Groepsbeleid Hallo voor 'Toestaan dat BitLocker zonder een compatibele TPM' [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).
* BitLocker-Groepsbeleid op virtuele machines die lid van domein voor de aangepaste Hallo instelling na moet bevatten: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` Azure Disk Encryption mislukken wanneer aangepaste groepsbeleidsinstellingen voor Bitlocker niet compatibel zijn. Op computers die geen Hallo juist beleidsinstelling Hallo nieuw beleid toepassen forceren Hallo nieuw beleid tooupdate (gpupdate.exe/Force) en start vervolgens opnieuw mogelijk vereist.  
* toocreate een Azure AD-toepassing een sleutelkluis maken of een bestaande sleutelkluis instellen en versleuteling inschakelen, raadpleegt u Hallo [vereiste PowerShell-script voor Azure Disk Encryption](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
* Zie tooconfigure schijfversleuteling vereisten hello Azure CLI met [dit script Bash](https://github.com/ejarvi/ade-cli-getting-started).
* toouse hello Azure Backup-service tooback up en herstel versleuteld virtuele machines, als versleuteling is ingeschakeld met Azure Disk Encryption versleutelen van uw virtuele machines met hello Azure Disk Encryption key configuratie. Hallo Backup-service biedt ondersteuning voor virtuele machines die zijn versleuteld met alleen een KEK-configuratie. Zie [tooback up en herstel versleuteld hoe virtuele machines met Azure Backup-versleuteling](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).

* Bij het versleutelen van een volume met het Linux-besturingssysteem, houd er rekening mee dat VM moet worden opgestart momenteel achter Hallo Hallo-proces. Dit kan worden gedaan via Hallo-portal, powershell of CLI.   tootrack hello voortgang van de versleuteling, pollen periodiek Hallo-statusbericht dat is geretourneerd door Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.  Zodra de codering is voltooid, wordt dit door Hallo Hallo-statusbericht geretourneerd door deze opdracht aangegeven.  Bijvoorbeeld ' ProgressMessage: besturingssysteemschijf is versleuteld, start opnieuw op Hallo VM ' op dit punt Hallo VM kan worden gestart en gebruikt.  

* Azure Disk Encryption voor Linux moet gegevens schijven toohave een gekoppeld bestandssysteem in de voorafgaande tooencryption Linux

* Recursief gekoppelde schijven worden niet ondersteund door Azure Disk Encryption Hallo voor Linux. Bijvoorbeeld, als hello doelsysteem een schijf is gekoppeld op /foo/bar en slaagt op /foo/bar/baz, Hallo versleuteling van /foo/bar/baz, maar versleuteling van foo/balk zal mislukken. 

* Azure Disk Encryption wordt alleen ondersteund op Azure-galerie ondersteund installatiekopieën die voldoen aan de hiervoor genoemde Hallo-vereisten. Klanten aangepaste installatiekopieën worden niet ondersteund vanwege toocustom partitieschema's en het proces gedrag die op deze installatiekopieën kunnen bestaan. Bovendien is zelfs afbeelding op basis van de virtuele machine die in eerste instantie vereisten wordt voldaan, maar zijn gewijzigd nadat het maken van zijn mogelijk niet compatibel.  Voor dat reden Hallo procedure aanbevolen voor het versleutelen van een Linux-VM is toostart vanuit een schone afbeelding, versleutelen Hallo VM en voeg vervolgens aangepaste software of gegevens toohello VM indien nodig.  

> [!NOTE]
> Back-up en herstel van versleutelde virtuele machines wordt alleen ondersteund voor virtuele machines die zijn versleuteld met Hallo KEK-configuratie. Dit wordt niet ondersteund op virtuele machines die zijn versleuteld zonder KEK-sleutel. KEK-sleutel is een optionele parameter waarmee de virtuele machine.

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a>Hallo ingesteld met Azure AD-toepassing in Azure Active Directory
Wanneer u versleuteling toobe ingeschakeld op een actieve virtuele machine in Azure, wordt Azure Disk Encryption genereert en schrijft Hallo versleuteling sleutels tooyour sleutelkluis. Het beheren van versleutelingssleutels in de sleutelkluis vereist Azure AD-verificatie.

Maak een Azure AD-toepassing voor dit doel. U vindt gedetailleerde stappen voor het registreren van een toepassing in 'Een identiteit voor de toepassing hello ophalen' Hallo-sectie van Hallo blogbericht [Azure Sleutelkluis - stapsgewijze](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx). Dit bericht bevat ook een aantal handige voorbeelden voor het instellen en configureren van de sleutelkluis. U kunt op basis van een geheim clientverificatie of clientverificatie Azure AD op basis van certificaten gebruiken voor verificatiedoeleinden.

#### <a name="client-secret-based-authentication-for-azure-ad"></a>Clientverificatie op basis van een geheim voor Azure AD
Hallo secties kunt u een client geheim gebaseerde verificatie voor Azure AD configureren.

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a>Een Azure AD-toepassing maken met behulp van Azure PowerShell
Gebruik de volgende PowerShell-cmdlet toocreate een Azure AD-toepassing hello:

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> $azureAdApplication.ApplicationId hello Azure AD ClientID en $aadClientSecret Hallo-clientgeheim dat u later tooenable Azure Disk Encryption moet gebruiken. Geheim hello Azure AD-client op de juiste wijze beveiligt.

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a>Hello Azure AD-client-ID en geheim instellen vanuit de klassieke Azure-portal Hallo
U kunt ook van uw Azure AD-client-ID en geheim instellen met behulp van Hallo [klassieke Azure-portal]( https://manage.windowsazure.com). tooperform dit taak Hallo te volgen:

1. Klik op Hallo **Active Directory** tabblad.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. Klik op **toepassing toevoegen**, en vervolgens type Hallo toepassingsnaam.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. Klik op de knop pijl Hallo en configureer vervolgens de toepassingseigenschappen Hallo.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. Klik op het vinkje Hallo in Hallo lager zijn linkerhoek toofinish. configuratiepagina Hallo-toepassing wordt weergegeven en hello Azure AD-client-ID wordt weergegeven aan de onderkant Hallo van Hallo pagina.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. Hello Azure AD-clientgeheim opslaan door te klikken op Hallo **opslaan** knop. Houd er rekening mee clientgeheim hello Azure AD in Hallo sleutels tekstvak. Op de juiste wijze beveiligt.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > Hallo voorafgaand aan de stroom wordt niet ondersteund op Hallo klassieke Azure-portal.

##### <a name="use-an-existing-application"></a>Gebruik een bestaande toepassing
tooexecute Hallo van de volgende opdrachten, downloaden en gebruiken van Hallo [Azure AD PowerShell-module](https://technet.microsoft.com/library/jj151815.aspx).

> [!NOTE]
> Hallo moeten volgende opdrachten worden uitgevoerd vanuit een nieuwe PowerShell-venster. Gebruik geen Azure PowerShell of Azure Resource Manager Hallo tooexecute Hallo opdrachten. Deze aanpak wordt aangeraden omdat deze cmdlets in Hallo MSOnline module of Azure AD PowerShell.

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a>Verificatie op basis van certificaten voor Azure AD
> [!NOTE]
> Azure AD gebaseerde verificatie is momenteel niet ondersteund op virtuele Linux-machines.

Hallo secties tonen hoe tooconfigure een op certificaten gebaseerde verificatie voor Azure AD.

##### <a name="create-an-azure-ad-application"></a>Een Azure AD-toepassing maken
toocreate een Azure AD-toepassing hello volgende PowerShell-cmdlets uitvoeren:

> [!NOTE]
> Vervang de volgende Hallo `yourpassword` tekenreeks met beveiligd wachtwoord en beveiliging Hallo wachtwoord.

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

Nadat u deze stap hebt voltooid, uploaden van een sleutelkluis voor PFX-bestand tooyour en Hallo toegang beleid nodig toodeploy dat certificaat tooa VM inschakelen.

##### <a name="use-an-existing-azure-ad-application"></a>Gebruik een bestaande Azure AD-toepassing
Als u verificatie op basis van certificaten voor een bestaande toepassing configureren wilt, gebruikt u Hallo PowerShell-cmdlets die hier worden weergegeven. Ervoor tooexecute worden van een nieuwe PowerShell-venster.

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

Nadat u deze stap hebt voltooid, uploaden van een sleutelkluis voor PFX-bestand tooyour en Hallo toegangsbeleid dat nodig is toodeploy Hallo certificaat tooa VM inschakelen.

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a>Een sleutelkluis voor PFX-bestand tooyour uploaden
Zie voor een gedetailleerde uitleg van dit proces [Hallo officiële Azure Key Vault-teamblog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx). Hallo volgende PowerShell-cmdlets zijn echter alles wat die u nodig hebt voor Hallo-taak. Worden ervoor tooexecute van Azure PowerShell-console.

> [!NOTE]
> Vervang de volgende Hallo `yourpassword` tekenreeks met beveiligd wachtwoord en beveiliging Hallo wachtwoord.

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a>Een certificaat in uw sleutelkluis tooan bestaande virtuele machine implementeren
Nadat u Hallo PFX uploaden, moet u een certificaat in Hallo sleutelkluis tooan bestaande virtuele machine met de volgende Hallo implementeren:
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a>Hallo sleutelkluis-beleid voor hello Azure AD-toepassing instellen
Uw Azure AD-toepassing moet rechten tooaccess Hallo sleutels of geheimen in Hallo kluis. Gebruik Hallo [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant machtigingen toohello toepassing, Hallo client-ID (die is gegenereerd toen de toepassing hello is geregistreerd) als Hallo _– ServicePrincipalName_ waarde voor parameter. toolearn Zie meer Hallo blogbericht [Azure Sleutelkluis - stapsgewijze](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx). Hier volgt een voorbeeld van hoe tooperform dit taak PowerShell:

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> Azure Disk Encryption, moet u tooconfigure Hallo toegang beleid tooyour Azure AD-clienttoepassing te volgen: _WrapKey_ en _ingesteld_ machtigingen.

## <a name="terminology"></a>Terminologie
toounderstand aantal algemene termen Hallo gebruikt door deze technologie, gebruik Hallo volgende terminologie tabel:

| Terminologie | Definitie |
| --- | --- |
| Azure AD | Azure AD [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/). Een Azure AD-account is een vereiste voor verificatie, opslaan en ophalen van geheimen van een sleutelkluis. |
| Azure Key Vault | Sleutelkluis is een cryptografische, key management service die gebaseerd op de Federal Information Processing Standards FIPS-gevalideerde hardware security modules, die ter bescherming van uw cryptografische sleutels en geheimen gevoelige. Zie voor meer informatie [Sleutelkluis](https://azure.microsoft.com/services/key-vault/) documentatie. |
| ARM | Azure Resource Manager |
| BitLocker |[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is een industrie herkend Windows volume versleuteling technologie die tooenable schijfversleuteling op IaaS VM's van Windows is gebruikt. |
| BEK | BitLocker-versleutelingssleutels zijn gebruikte tooencrypt Hallo OS opstartvolume en gegevensvolumes. Hallo BitLocker-sleutels worden beveiligd in een sleutelkluis als geheimen. |
| CLI | Zie [Azure-opdrachtregelinterface](../cli-install-nodejs.md). |
| DM-Crypt |[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is Hallo op basis van Linux, transparant schijfversleuteling subsysteem tooenable schijfversleuteling op Linux IaaS VM's is gebruikt. |
| KEK | Sleutelcodering sleutel is Hallo asymmetrische sleutel (RSA 2048) tooprotect gebruiken of Hallo geheim teruglopen. U kunt bieden een hardware security modules (HSM)-sleutel of met software beschermde sleutel beveiligd. Zie voor meer informatie [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentatie. |
| PS-cmdlets | Zie [Azure PowerShell-cmdlets](/powershell/azure/overview). |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a>Installeren en configureren van de sleutelkluis voor Azure Disk Encryption
Azure Disk Encryption helpt de Hallo schijfversleuteling sleutels en geheimen in de sleutelkluis. tooset van de sleutelkluis voor Azure Disk Encryption voltooid Hallo stappen voor elk Hallo uit te voeren.

#### <a name="create-a-key-vault"></a>Een sleutelkluis maken
een sleutelkluis toocreate gebruik een van Hallo volgende opties:

* [Resource Manager-sjabloon '101-sleutel-kluis-maken'](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [Azure PowerShell-cmdlets voor sleutelkluis](/powershell/module/azurerm.keyvault/#key_vault)
* Azure Resource Manager
* Hoe te[beveiligen van uw sleutelkluis](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)

> [!NOTE]
> Als u hebt al een sleutelkluis ingesteld voor uw abonnement, slaat u de volgende sectie toohello.

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a>Instellen van een coderingssleutel voor de sleutel (optioneel)
Als u toouse een KEK-sleutel voor een extra beveiligingslaag voor Hallo BitLocker versleutelingssleutels wilt, voegt u een KEK tooyour-sleutelkluis. Gebruik Hallo [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate een sleutel sleutelcodering in Hallo sleutelkluis. U kunt ook een KEK importeren uit uw lokale Sleutelbeheer HSM. Zie voor meer informatie [Sleutelkluis documentatie](https://azure.microsoft.com/documentation/services/key-vault/).

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

U kunt Hallo KEK toevoegen door te gaan tooAzure Resource Manager of met behulp van de sleutelkluis-interface.

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a>Sleutelkluis-machtigingen instellen
Hello Azure-platform moet toegang toohello versleutelingssleutels of geheimen in uw sleutelkluis toomake ze beschikbaar toohello VM voor het opstarten en ontsleutelen van Hallo volumes. toogrant machtigingen toohello Azure-platform set Hallo **EnabledForDiskEncryption** eigenschap in Hallo key vault via Hallo sleutelkluis PowerShell-cmdlet:

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

U kunt ook instellen Hallo **EnabledForDiskEncryption** eigenschap via Hallo [Azure Resource Explorer](https://resources.azure.com).

Zoals eerder vermeld, moet u instellen Hallo **EnabledForDiskEncryption** eigenschap in de sleutelkluis. Anders mislukt Hallo implementatie.

U kunt beleidsregels voor toegang instellen voor uw Azure AD-toepassing van de interface van de sleutelkluis hello, zoals hier wordt weergegeven:

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

Op Hallo **geavanceerde toegangsbeleid** tabblad, zorg ervoor dat de sleutelkluis voor Azure Disk Encryption is ingeschakeld:

![Azure sleutelkluis](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a>Implementatiescenario's voor schijf-codering en gebruikerservaringen
Kunt u veel scenario's voor schijf-codering inschakelen en Hallo stappen kunnen variëren volgens toohello scenario. Hallo volgende secties wordt beschreven Hallo scenario's met meer details.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a>Schakel versleuteling in op de nieuwe IaaS VM's die zijn gemaakt van Hallo Marketplace
U kunt schijfversleuteling op de nieuwe IaaS virtuele machine van Windows uit Hallo Marketplace in Azure inschakelen met behulp van Hallo [Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).

1. Op de sjabloon hello Azure snel starten, klikt u op **implementeren tooAzure**, Hallo versleuteling configuratie invoeren op Hallo **Parameters** blade en klik vervolgens op **OK**.

2. Selecteer Hallo abonnement, resourcegroep locatie voor resourcegroep, juridische voorwaarden en overeenkomst en klik vervolgens op **maken** tooenable versleuteling op een nieuwe IaaS VM.

> [!NOTE]
> Deze sjabloon maakt een nieuwe versleutelde Windows virtuele machine die gebruikmaakt van Windows Server 2012 Hallo afbeelding.

U kunt schijfversleuteling op een nieuwe IaaS RedHat Linux 7.2 virtuele machine met een matrix van 200 GB RAID-0 inschakelen met behulp van dit [Resource Manager-sjabloon](https://aka.ms/fde-rhel). Nadat u de sjabloon Hallo hebt geïmplementeerd, Hallo VM versleutelingsstatus controleren via Hallo `Get-AzureRmVmDiskEncryptionStatus` cmdlet, zoals beschreven in [OS versleutelen station op een actieve Linux VM](#encrypting-os-drive-on-a-running-linux-vm). Wanneer Hallo machine status retourneert _VMRestartPending_, Hallo VM starten.

Hallo volgende tabel bevat Hallo Resource Manager-Sjabloonparameters voor nieuwe virtuele machines van Hallo Marketplace scenario met behulp van Azure AD-client-ID:

| Parameter | Beschrijving |
| --- | --- |
| adminUserName | De beheerdersgebruikersnaam voor Hallo virtuele machine. |
| adminPassword | Beheerderswachtwoord voor Hallo virtuele machine. |
| newStorageAccountName | Naam van Hallo storage account toostore OS en gegevens VHD's. |
| vmSize | Grootte van Hallo VM. Op dit moment worden alleen standaard A, D en G reeksen ondersteund. |
| virtualNetworkName | Naam van de VNet die Hallo VM NIC Hallo moet bij horen. |
| subnetName | Naam van het subnet in VNet dat Hallo VM NIC Hallo Hallo moet bij horen. |
| AADClientID | Client-ID van hello Azure AD-toepassing die machtigingen toowrite geheimen tooyour sleutelkluis heeft. |
| AADClientSecret | Clientgeheim van hello Azure AD-toepassing die machtigingen toowrite geheimen tooyour sleutelkluis heeft. |
| keyVaultURL | URL van Hallo key vault die Hallo BitLocker-sleutel moet worden geüpload naar. U kunt dit downloaden met behulp van de cmdlet Hallo `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`. |
| keyEncryptionKeyURL | URL van Hallo sleutel versleutelingssleutel die wordt gebruikt tooencrypt Hallo gegenereerd BitLocker-sleutel (optioneel). |
| keyVaultResourceGroup | De resourcegroep van de sleutelkluis Hallo. |
| vmName | Naam van de virtuele machine die coderingsbewerking Hallo Hallo is toobe uitgevoerd op. |

> [!NOTE]
> _KeyEncryptionKeyURL_ is een optionele parameter. U kunt uw eigen KEK toofurther safeguard Hallo gegevensversleutelingssleutel (geheime wachtwoordzin) zetten in de sleutelkluis.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a>Schakel versleuteling in op de nieuwe IaaS VM's die zijn gemaakt van de klant versleuteld VHD- en versleutelingssleutels
In dit scenario kunt u inschakelen versleutelen met behulp van Resource Manager-sjabloon hello, PowerShell-cmdlets of CLI-opdrachten. Hallo volgende secties wordt uitgelegd in meer detail Hallo Resource Manager-sjabloon en de CLI-opdrachten.

Hallo instructies volgt in een van deze secties voor het voorbereiden van vooraf zijn versleuteld afbeeldingen die kunnen worden gebruikt in Azure. Nadat het Hallo-installatiekopie is gemaakt, kunt u stappen Hallo in Hallo volgende sectie toocreate een versleutelde Azure VM.

* [Een vooraf zijn versleuteld Windows VHD voorbereiden](#preparing-a-pre-encrypted-windows-vhd)
* [Een vooraf zijn versleuteld Linux VHD voorbereiden](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a>Hallo Resource Manager-sjabloon
U kunt schijfversleuteling op uw versleutelde VHD inschakelen met behulp van Hallo [Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).

1. Op de sjabloon hello Azure snel starten, klikt u op **implementeren tooAzure**, Hallo versleuteling configuratie invoeren op Hallo **Parameters** blade en klik vervolgens op **OK**.

2. Selecteer Hallo abonnement, resourcegroep locatie voor resourcegroep, juridische voorwaarden en overeenkomst en klik vervolgens op **maken** tooenable versleuteling op Hallo nieuwe IaaS VM.

Hallo volgende tabel bevat Hallo Resource Manager-Sjabloonparameters voor uw versleutelde VHD:

| Parameter | Beschrijving |
| --- | --- |
| newStorageAccountName | Naam van Hallo storage account toostore Hallo versleuteld OS VHD. Dit opslagaccount moet al zijn gemaakt in Hallo dezelfde resourcegroep en dezelfde locatie als Hallo VM. |
| osVhdUri | De URI van Hallo OS VHD van Hallo storage-account. |
| besturingssysteemtype | Type besturingssysteem product (Windows of Linux). |
| virtualNetworkName | Naam van de VNet die Hallo VM NIC Hallo moet bij horen. Hallo naam moet al zijn gemaakt in Hallo dezelfde resourcegroep en dezelfde locatie als Hallo VM. |
| subnetName | Naam van het Hallo-subnet op Hallo VNet dat Hallo VM NIC moet bij horen. |
| vmSize | Grootte van Hallo VM. Op dit moment worden alleen standaard A, D en G reeksen ondersteund. |
| keyVaultResourceID | Hallo ResourceID waarmee Hallo sleutelkluisresource in Azure Resource Manager. U kunt dit downloaden met behulp van PowerShell-cmdlet Hallo `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`. |
| keyVaultSecretUrl | De URL van Hallo schijfversleuteling sleutel die ingesteld in de sleutelkluis Hallo. |
| keyVaultKekUrl | URL van Hallo sleutelcodering sleutel voor het coderen van Hallo gegenereerd versleutelingssleutel op de schijf. |
| vmName | Naam van Hallo IaaS VM. |

#### <a name="using-powershell-cmdlets"></a>Met behulp van PowerShell-cmdlets
U kunt schijfversleuteling op uw versleutelde VHD inschakelen met behulp van PowerShell-cmdlet Hallo [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).  

#### <a name="using-cli-commands"></a>CLI-opdrachten gebruiken
schijfversleuteling tooenable voor dit scenario met behulp van de CLI-opdrachten Hallo te volgen:

1. Toegangsbeleid instellen in de sleutelkluis:

   * Set Hallo **EnabledForDiskEncryption** vlag:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * Stel machtigingen tooAzure AD toepassing toowrite geheimen tooyour sleutelkluis:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. tooenable versleuteling op een bestaande of actieve virtuele machine, type:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. Versleutelingsstatus ophalen:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. versleuteling op een nieuwe virtuele machine vanaf uw versleutelde VHD, gebruik Hallo volgende parameters Hello tooenable `azure vm create` opdracht:

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a>Schakel versleuteling in op de bestaande of IaaS virtuele Windows-machine in Azure wordt uitgevoerd
In dit scenario kunt u inschakelen versleutelen met behulp van Resource Manager-sjabloon hello, PowerShell-cmdlets of CLI-opdrachten. Hallo volgende secties wordt uitgelegd in meer detail hoe deze met behulp van Resource Manager-sjabloon en de CLI-opdrachten Hallo tooenable.

#### <a name="using-hello-resource-manager-template"></a>Hallo Resource Manager-sjabloon
U kunt schijfversleuteling op de bestaande of IaaS VM's van Windows worden uitgevoerd in Azure met behulp van Hallo inschakelen [Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).

1. Op de sjabloon hello Azure snel starten, klikt u op **implementeren tooAzure**, Hallo versleuteling configuratie invoeren op Hallo **Parameters** blade en klik vervolgens op **OK**.

2. Selecteer Hallo abonnement, resourcegroep locatie voor resourcegroep, juridische voorwaarden en overeenkomst en klik vervolgens op **maken** tooenable versleuteling op Hallo van bestaande of IaaS VM uitgevoerd.

Hallo bevat volgende tabel Hallo Resource Manager-Sjabloonparameters voor bestaande of VM's die gebruikmaken van een client-ID van Azure AD worden uitgevoerd:

| Parameter | Beschrijving |
| --- | --- |
| AADClientID | Client-ID van hello Azure AD-toepassing die machtigingen toowrite geheimen toohello sleutelkluis heeft. |
| AADClientSecret | Clientgeheim van hello Azure AD-toepassing die machtigingen toowrite geheimen toohello sleutelkluis heeft. |
| keyVaultName | Naam van de sleutel Hallo kluis die Hallo BitLocker-sleutel moet worden geüpload naar. U kunt dit downloaden met behulp van de cmdlet Hallo `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`. |
|  keyEncryptionKeyURL | URL van Hallo sleutel versleutelingssleutel die wordt gebruikt tooencrypt Hallo BitLocker-sleutel gegenereerd. Deze parameter is optioneel als u selecteert **nokek** in Hallo UseExistingKek vervolgkeuze-lijst. Als u selecteert **kek** in de lijst vervolgkeuzelijst UseExistingKek hello, moet u Hallo _keyEncryptionKeyURL_ waarde. |
| volumeType | Het type van het volume dat Hallo coderingsbewerking wordt uitgevoerd op. Geldige waarden zijn _OS_, _gegevens_, en _alle_. |
| sequenceVersion | Versie van de reeks van Hallo BitLocker-bewerking. Dit versienummer verhoogd telkens wanneer een schijfversleuteling bewerking wordt uitgevoerd op Hallo dezelfde virtuele machine. |
| vmName | Naam van de virtuele machine die coderingsbewerking Hallo Hallo is toobe uitgevoerd op. |

> [!NOTE]
> _KeyEncryptionKeyURL_ is een optionele parameter. U kunt uw eigen KEK toofurther safeguard Hallo gegevensversleutelingssleutel (geheim BitLocker-versleuteling) in de sleutelkluis Hallo zetten.

#### <a name="using-powershell-cmdlets"></a>Met behulp van PowerShell-cmdlets
Zie voor informatie over het inschakelen van versleuteling met Azure Disk Encryption met behulp van PowerShell-cmdlets Hallo blogberichten [Azure Disk Encryption verkennen met Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) en [Azure Disk Encryption verkennen Deel 2 met Azure PowerShell -](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).

#### <a name="using-cli-commands"></a>CLI-opdrachten gebruiken
tooenable versleuteling op bestaande of IaaS virtuele machine van Windows worden uitgevoerd in Azure CLI-opdrachten met Hallo te volgen:

1. toegangsbeleid in de sleutelkluis hello tooset:
   * Set Hallo **EnabledForDiskEncryption** vlag:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * Stel machtigingen tooAzure AD toepassing toowrite geheimen tooyour sleutelkluis:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. tooenable versleuteling op een bestaande of actieve virtuele machine:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. de coderingsstatus tooget:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. versleuteling op een nieuwe virtuele machine vanaf uw versleutelde VHD, gebruik Hallo volgende parameters Hello tooenable `azure vm create` opdracht:

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a>Schakel versleuteling in op een bestaande of actief IaaS virtuele Linux-machine in Azure
U kunt schijfversleuteling op een bestaande of actief IaaS virtuele Linux-machine in Azure inschakelen met behulp van Hallo [Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).

1. Klik op **implementeren tooAzure** hello Azure snel starten-sjabloon, Voer Hallo versleuteling configuratie op Hallo **Parameters** blade en klik vervolgens op **OK**.

2. Selecteer Hallo abonnement, resourcegroep locatie voor resourcegroep, juridische voorwaarden en overeenkomst en klik vervolgens op **maken** tooenable versleuteling op Hallo van bestaande of IaaS VM uitgevoerd.

Hallo volgende tabel geeft een lijst van Resource Manager-Sjabloonparameters voor bestaande of VM's die gebruikmaken van een client-ID van Azure AD worden uitgevoerd:

| Parameter | Beschrijving |
| --- | --- |
| AADClientID | Client-ID van hello Azure AD-toepassing die machtigingen toowrite geheimen toohello sleutelkluis heeft. |
| AADClientSecret | Clientgeheim van hello Azure AD-toepassing die machtigingen toowrite geheimen tooyour sleutelkluis heeft. |
| keyVaultName | Naam van de sleutel Hallo kluis die Hallo BitLocker-sleutel moet worden geüpload naar. U kunt dit downloaden met behulp van de cmdlet Hallo `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`. |
|  keyEncryptionKeyURL | URL van Hallo sleutel versleutelingssleutel die wordt gebruikt tooencrypt Hallo BitLocker-sleutel gegenereerd. Deze parameter is optioneel als u selecteert **nokek** in Hallo UseExistingKek vervolgkeuze-lijst. Als u selecteert **kek** in de lijst vervolgkeuzelijst UseExistingKek hello, moet u Hallo _keyEncryptionKeyURL_ waarde. |
| volumeType | Het type van het volume dat Hallo coderingsbewerking wordt uitgevoerd op. Geldige ondersteunde waarden zijn _OS_ of _alle_ (voor RHEL 7.2, CentOS 7.2 en Ubuntu 16.04) en _gegevens_ (voor alle andere distributies). |
| sequenceVersion | Versie van de reeks van Hallo BitLocker-bewerking. Dit versienummer verhoogd telkens wanneer een schijfversleuteling bewerking wordt uitgevoerd op Hallo dezelfde virtuele machine. |
| vmName | Naam van de virtuele machine die coderingsbewerking Hallo Hallo is toobe uitgevoerd op. |
| Wachtwoordzin | Typ een sterke wachtwoordzin als Hallo gegevensversleutelingssleutel. |

> [!NOTE]
> _KeyEncryptionKeyURL_ is een optionele parameter. U kunt uw eigen KEK toofurther safeguard Hallo gegevensversleutelingssleutel (geheime wachtwoordzin) zetten in de sleutelkluis.

#### <a name="cli-commands"></a>CLI-opdrachten
U kunt schijfversleuteling inschakelen op uw versleutelde VHD te installeren en gebruiken van Hallo [CLI opdracht](../cli-install-nodejs.md). tooenable versleuteling op bestaande of IaaS Linux VM's worden uitgevoerd in Azure met behulp van de CLI-opdrachten Hallo te volgen:

1. Toegangsbeleid instellen in de sleutelkluis Hallo:

 * Set Hallo **EnabledForDiskEncryption** vlag:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * Stel machtigingen tooAzure AD toepassing toowrite geheimen tooyour sleutelkluis:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. tooenable versleuteling op een bestaande of actieve virtuele machine:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. Versleutelingsstatus ophalen:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. versleuteling op een nieuwe virtuele machine vanaf uw versleutelde VHD, gebruik Hallo volgende parameters Hello tooenable `azure vm create` opdracht:
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a>Hallo coderingsstatus van een versleutelde IaaS VM ophalen
U kunt Hallo coderingsstatus ophalen met behulp van Azure Resource Manager [PowerShell-cmdlets](/powershell/azure/overview), of de CLI-opdrachten. Hallo volgende secties wordt uitgelegd hoe toouse Hallo klassieke Azure-portal en de CLI-opdrachten tooget Hallo coderingsstatus.

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a>Hallo coderingsstatus van een versleutelde Windows VM ophalen met behulp van Azure Resource Manager
U kunt de coderingsstatus Hallo Hallo IaaS VM van Azure Resource Manager krijgen door Hallo volgende te doen:

1. Meld u aan toohello [klassieke Azure-portal](https://portal.azure.com/), en klik vervolgens op **virtuele machines** in Hallo linkerdeelvenster toosee een samenvatting weergegeven van Hallo virtuele machines in uw abonnement. U kunt Hallo virtuele machines weergave filteren Hallo abonnement door naam te selecteren in Hallo **abonnement** vervolgkeuzelijst.

2. Hallo boven aan het Hallo **virtuele machines** pagina, klikt u op **kolommen**.

3. Op Hallo **Kies kolom** blade Selecteer **schijfversleuteling**, en klik vervolgens op **Update**. U ziet Hallo schijfversleuteling kolom tonen Hallo coderingsstatus _ingeschakeld_ of _niet ingeschakeld_ voor elke virtuele machine, zoals wordt weergegeven in de volgende afbeelding Hallo:

 ![Microsoft Antimalware in Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a>Hallo coderingsstatus van een versleutelde (Windows of Linux) IaaS VM ophalen met behulp van Hallo schijfversleuteling PowerShell-cmdlet
Hallo schijfversleuteling PowerShell-cmdlet kunt u de coderingsstatus Hallo Hallo IaaS VM downloaden `Get-AzureRmVMDiskEncryptionStatus`. tooget Hallo-versleutelingsinstellingen voor uw virtuele machine, Voer Hallo volgende in:

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

U kunt de uitvoer van Hallo inspecteren _Get-AzureRmVMDiskEncryptionStatus_ sleutel URL's voor versleuteling.

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

Hallo OSVolumeEncrypted en waarden van DataVolumesEncrypted too_Encrypted_ die aangeeft dat beide volumes zijn versleuteld met behulp van Azure Disk Encryption ingesteld. Zie voor informatie over het inschakelen van versleuteling met Azure Disk Encryption met behulp van PowerShell-cmdlets Hallo blogberichten [Azure Disk Encryption verkennen met Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) en [Azure Disk Encryption verkennen Deel 2 met Azure PowerShell -](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).

> [!NOTE]
> Op Linux virtuele machines, duurt het drie toofour minuten Hallo `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport Hallo coderingsstatus.

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a>De coderingsstatus Hallo Hallo IaaS VM ophalen uit Hallo schijfversleuteling CLI-opdracht
U krijgt Hallo coderingsstatus van Hallo IaaS VM via Hallo schijfversleuteling CLI opdracht `azure vm show-disk-encryption-status`. tooget Hallo-versleutelingsinstellingen voor uw virtuele machine, Voer uw Azure CLI-sessie:

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a>Schakel versleuteling voor het uitvoeren van Windows IaaS VM
U kunt versleuteling op een actieve Windows of Linux IaaS VM via hello Azure Disk Encryption Resource Manager-sjabloon of PowerShell-cmdlets uitschakelen en Hallo ontsleuteling configuratie opgeven.

##### <a name="windows-vm"></a>Windows VM
Hallo disable-codering stap Hiermee schakelt u versleuteling van Hallo OS, Hallo gegevensvolume of beide op Hallo Windows IaaS VM uitgevoerd. U kan uitschakelen Hallo OS volume en laat Hallo gegevensvolume versleuteld. Hallo disable-codering stap wordt uitgevoerd, Hallo klassieke implementatiemodel Azure VM-servicemodel Hallo updates als Hallo Windows IaaS VM ontsleutelde is gemarkeerd. Hallo-inhoud van Hallo VM zijn niet langer in rust versleuteld. Hallo-ontsleuteling worden niet verwijderd voor uw kluis en Hallo encryption key sleutelmateriaal (versleutelingssleutels BitLocker voor Windows en de wachtwoordzin voor Linux).

##### <a name="linux-vm"></a>Virtuele Linux-machine
Hallo disable-codering stap Hiermee schakelt u versleuteling van Hallo gegevensvolume op Hallo IaaS virtuele Linux-machine wordt uitgevoerd. Deze stap werkt alleen als de besturingssysteemschijf Hallo is niet versleuteld.

> [!NOTE]
> Uitschakelen van versleuteling op Hallo besturingssysteemschijf is niet toegestaan op de virtuele Linux-machines.

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>Schakel versleuteling in op een bestaande of actief IaaS VM
U kunt schijfversleuteling op IaaS VM's van Windows worden uitgevoerd met behulp van Hallo uitschakelen [Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).

1. Op de sjabloon hello Azure snel starten, klikt u op **implementeren tooAzure**, Hallo ontsleuteling configuratie invoeren op Hallo **Parameters** blade en klik vervolgens op **OK**.

2. Selecteer Hallo abonnement, resourcegroep locatie voor resourcegroep, juridische voorwaarden en overeenkomst en klik vervolgens op **maken** tooenable versleuteling op een nieuwe IaaS VM.

Virtuele Linux-machines, kunt u versleuteling uitschakelen met behulp van Hallo [uitschakelen van versleuteling op een actieve Linux VM](https://aka.ms/decrypt-linuxvm) sjabloon.

Hallo bevat volgende tabel de sjabloonparameters Resource Manager voor het uitschakelen van versleuteling op een actieve IaaS VM:

| Parameter | Beschrijving |
| --- | --- |
| vmName | Naam van de virtuele machine die coderingsbewerking Hallo Hallo is toobe uitgevoerd op.
| volumeType | Het type van het volume dat een ontsleutelingsbewerking wordt uitgevoerd op. Geldige waarden zijn _OS_, _gegevens_, en _alle_. U kunt versleuteling voor het uitvoeren van Windows IaaS VM OS/opstartvolume zonder het uitschakelen van versleuteling op Hallo niet uitschakelen _gegevens_ volume. Houd er ook rekening mee dat uitschakelen versleuteling op Hallo OS-schijf is niet toegestaan voor virtuele Linux-machines. |
| sequenceVersion | Versie van de reeks van Hallo BitLocker-bewerking. Dit versienummer verhoogd telkens wanneer een ontsleutelingsbewerking schijf wordt uitgevoerd op Hallo dezelfde virtuele machine. |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>Schakel versleuteling in op een bestaande of actief IaaS VM
Zie toodisable versleuteling op een bestaande of actief IaaS-VM met behulp van PowerShell-cmdlet Hallo [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption). Deze cmdlet biedt ondersteuning voor Windows- en Linux-machines. toodisable versleuteling, wordt een uitbreiding op Hallo virtuele machine geïnstalleerd. Als hello _naam_ parameter niet is opgegeven, een uitbreiding met de standaardnaam Hallo _AzureDiskEncryption voor VM's van Windows_ wordt gemaakt.

Op Linux virtuele machines, wordt Hallo AzureDiskEncryptionForLinux uitbreiding gebruikt.

> [!NOTE]
> Deze cmdlet Hallo virtuele machine opnieuw is opgestart.

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a>Schakel versleuteling in op vooraf zijn versleuteld IaaS VM met beheerde Azure-schijf
Hello Azure beheerd schijf ARM-sjabloon toocreate te op een versleutelde virtuele machine van een vooraf zijn versleuteld VHD met Hallo ARM-sjabloon vinden gebruiken   
[Een nieuwe beheerde versleutelde schijf van een vooraf zijn versleuteld VHD/storage-blob maken] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a>Schakel versleuteling in op een nieuwe Linux IaaS-VM met beheerde Azure-schijf
Hello Azure beheerd schijf ARM-sjabloon toocreate die een nieuwe versleuteld Linux IaaS-VM met Hallo zich bevindt op ARM-sjabloon gebruiken   
[Implementatie RHEL 7.2 met volledige schijfversleuteling] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a>Schakel versleuteling in op een nieuwe Windows IaaS-VM met beheerde Azure-schijf
 Hello Azure beheerd schijf ARM-sjabloon toocreate die een nieuwe versleuteld Linux IaaS-VM met Hallo zich bevindt op ARM-sjabloon gebruiken   
 [Een nieuwe versleutelde Windows IaaS beheerd schijf virtuele machine maken van de afbeelding] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)

  > [!NOTE]
  >Het is verplicht toosnapshot en/of back-up een beheerde schijf op basis van VM-instantie buiten en eerdere tooenabling Azure Disk Encryption.  Een momentopname van het Hallo-beheerde schijven kan worden uitgevoerd vanuit de portal Hallo of Azure Backup kan worden gebruikt.  Back-ups zorgen ervoor dat een hersteloptie mogelijk in geval van Hallo van een onverwachte fout opgetreden tijdens het versleutelen.  Nadat u een back-up is gemaakt, kan de cmdlet Set-AzureRmVMDiskEncryptionExtension Hallo gebruikte tooencrypt beheerde schijven worden door Hallo - skipVmBackup parameter te geven.  Met deze opdracht uitvoeren tegen beheerde schijven op basis van de virtuele machine totdat een back-up is gemaakt en deze parameter is opgegeven.    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a>Versleutelingsinstellingen van een bestaande versleutelde niet premium virtuele machine bijwerken
  AAD client-ID/geheime sleutel versleutelingssleutel [KEK] versleutelingssleutel BitLocker voor Windows-VM of de wachtwoordzin voor, zoals Hallo bestaande Azure-schijf codering wordt ondersteund interfaces gebruiken voor het uitvoeren van virtuele machine [PS-cmdlets, CLI of ARM-sjablonen] tooupdate Hallo versleutelingsinstellingen Versleutelingsinstelling voor Linux VM enzovoort Hallo-update wordt alleen ondersteund voor virtuele machines die worden ondersteund door niet-premium-opslag. Het is NNOT ondersteund voor virtuele machines die worden ondersteund door de premium-opslag.

## <a name="appendix"></a>Bijlage
### <a name="connect-tooyour-subscription"></a>Verbinding maken met tooyour abonnement
Lees voordat u doorgaat Hallo *vereisten* sectie in dit artikel. Nadat u ervoor te zorgen dat aan alle vereisten is voldaan, sluit u tooyour abonnement door Hallo volgende te doen:

1. Start een Azure PowerShell-sessie en meld u aan tooyour Azure-account met de volgende opdracht Hallo:

    `Login-AzureRmAccount`

2. Als u meerdere abonnementen hebt en één toouse toospecify, typt u Hallo toosee Hallo abonnementen voor uw account te volgen:

    `Get-AzureRmSubscription`

3. toospecify hello abonnement u wilt dat toouse, type:

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. tooverify hello abonnement geconfigureerd klopt, type:

    `Get-AzureRmSubscription`

5. tooconfirm hello Azure Disk Encryption cmdlets zijn geïnstalleerd, type:

    `Get-command *diskencryption*`

6. Hallo na uitvoer bevestigt hello Azure schijf versleuteling PowerShell-installatie:

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a>Een vooraf zijn versleuteld Windows VHD voorbereiden
Hallo-secties die volgen zijn nodig tooprepare een Windows-VHD voor de implementatie als een gecodeerde VHD in Azure IaaS vooraf zijn versleuteld. Hallo informatie tooprepare gebruiken en een nieuwe Windows VM (VHD) op de Azure Site Recovery of Azure opgestart.

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a>Bijwerken van de Groepsbeleid tooallow zonder TPM voor OS-beveiliging
Hallo groepsbeleidsinstellingen voor BitLocker-instelling configureren **BitLocker-stationsversleuteling**, die u vindt hier onder **lokaal computerbeleid** > **Computerconfiguratie**  >  **Beheersjablonen** > **Windows-onderdelen**. Deze instelling te wijzigen**besturingssysteem stations** > **aanvullende verificatie bij opstarten vereisen** > **BitLocker zonder een compatibele TPMtoestaan**, zoals weergegeven in de volgende afbeelding Hallo:

![Microsoft Antimalware in Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a>BitLocker-onderdelen installeren
Voor Windows Server 2012 en hoger, gebruikt u Hallo volgende opdracht:

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

Gebruik voor Windows Server 2008 R2 Hallo volgende opdracht:

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a>Hallo volume met het besturingssysteem voorbereiden voor BitLocker met behulp van`bdehdcfg`
toocompress Hallo OS partitie en Hallo machine voorbereiden voor BitLocker, Hallo volgende opdracht uitvoeren:

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a>Hallo OS volume beveiligen met behulp van BitLocker
Gebruik Hallo [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) opdracht tooenable versleuteling op Hallo opstartvolume met behulp van een externe sleutelbeveiliging. Ook Hallo externe sleutel (.bek-bestand) op Hallo extern station of volume plaatsen. Versleuteling is ingeschakeld op Hallo system/opstartvolume na Hallo opnieuw opstarten.

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> Hallo VM met een afzonderlijke gegevens/resource VHD voorbereiden voor het ophalen van externe sleutel Hallo met BitLocker.

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a>Versleutelen van een OS-station op een actieve Linux VM
Versleuteling van een OS-station op een actieve Linux VM wordt ondersteund op Hallo distributies te volgen:

* RHEL 7.2
* 7.2 centOS
* Ubuntu 16.04

##### <a name="prerequisites-for-os-disk-encryption"></a>Vereisten voor de OS-schijfversleuteling

* Hallo VM moet worden gemaakt vanuit Hallo Marketplace-installatiekopie in Azure Resource Manager.
* Azure virtuele machine met ten minste 4 GB aan RAM-geheugen (aanbevolen grootte is 7 GB).
* (Voor RHEL en CentOS) SELinux uitschakelen. toodisable SELinux, Zie '4.4.2. Uitschakelen van SELinux' in hello [SELinux van de gebruiker en de Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) op Hallo VM.
* Nadat u SELinux uitgeschakeld, start u ten minste eenmaal Hallo VM opnieuw.

##### <a name="steps"></a>Stappen
1. Een virtuele machine maken met behulp van een Hallo distributies eerder hebt opgegeven.

 Voor CentOS 7.2, OS schijfversleuteling ondersteund via een speciale installatiekopie. toouse dit image, '7.2n' als SKU Hallo bij het maken van VM Hallo opgeven:
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. Hallo VM volgens tooyour moet configureren. Als u tooencrypt gaat alle stations van hello (OS + gegevens), moeten Hallo gegevensstations toobe opgegeven en koppelbaar van /etc/fstab.

 > [!NOTE]
 > Gebruik UUID =... toospecify gegevensstations in/etc/fstab in plaats van Hallo blok apparaatnaam (bijvoorbeeld /dev/sdb1) opgeven. Tijdens het versleutelen kan Hallo volgorde van de stations op Hallo VM gewijzigd. Als uw virtuele machine afhankelijk van een specifieke volgorde van apparaten is, mislukt het toomount ze na versleuteling.

3. Meld u af bij Hallo SSH-sessies.

4. tooencrypt hello OS Geef volumeType als **alle** of **OS** wanneer u [versleuteling inschakelen](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).

 > [!NOTE]
 > Alle gebruikersruimte innemen processen die niet worden uitgevoerd als `systemd` services moeten worden afgesloten met een `SIGKILL`. Opnieuw opstarten Hallo VM. Wanneer u OS schijfversleuteling op een actieve virtuele machine inschakelt, plan op VM uitvaltijd.

5. Periodiek voortgang Hallo van versleuteling met Hallo-instructies in Hallo [volgende sectie](#monitoring-os-encryption-progress).

6. Nadat de Get-AzureRmVmDiskEncryptionStatus toont 'VMRestartPending', start u uw virtuele machine tooit aanmelden of via de portal hello, PowerShell of CLI.
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
Voordat u opnieuw opstart, wordt aangeraden dat u opslaat [opstarten diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) Hallo VM.

#### <a name="monitoring-os-encryption-progress"></a>OS-versleuteling voortgang controleren
U kunt voortgang OS versleuteling op drie manieren:

* Gebruik Hallo `Get-AzureRmVmDiskEncryptionStatus` cmdlet en controleer Hallo ProgressMessage veld:
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 Nadat het Hallo VM bereikt 'OS schijfversleuteling gestart', duurt het ongeveer 40 minuten too50 op een Premium-opslag ondersteund VM.

 Omdat [uitgeven #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` en `DataVolumesEncrypted` worden weergegeven als `Unknown` in een aantal distributies. Met de versie 2.1.5 WALinuxAgent en later kunt dit probleem automatisch opgelost. Als u ziet `Unknown` u kunt in de uitvoer van Hallo schijfversleuteling status controleren met behulp van hello Azure Resource Explorer.

 Ga te[Azure Resource Explorer](https://resources.azure.com/), en vouw vervolgens deze hiërarchie in Hallo selectie Configuratiescherm op links:

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 Ga in Hallo InstanceView, toosee Hallo coderingsstatus van uw schijven.

 ![Instantieweergave van virtuele machine](./media/azure-security-disk-encryption/vm-instanceview.png)

* Bekijk [opstarten diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/). Berichten van Hallo ADE uitbreiding moeten worden voorafgegaan door `[AzureDiskEncryption]`.

* Meld u bij toohello VM via SSH en Hallo extensie logboek vanaf ophalen:

    /var/log/Azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux

 Het is raadzaam dat u niet toohello VM aanmelden zich terwijl OS-versleuteling uitgevoerd wordt. Kopiëren van Logboeken voor Hallo alleen wanneer hello andere twee methoden zijn mislukt.

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a>Een vooraf zijn versleuteld Linux VHD voorbereiden
##### <a name="ubuntu-16"></a>Ubuntu 16
Configureren van versleuteling tijdens de installatie van de distributie Hallo door Hallo volgende te doen:

1. Selecteer **configureren van versleutelde volumes** wanneer het partitioneren van Hallo-schijven.

 ![Ubuntu 16.04 Setup](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. Maak een afzonderlijke opstartstation, moet niet worden versleuteld. Codeer uw basisstation.

 ![Ubuntu 16.04 Setup](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. Geef een wachtwoordzin. Dit is Hallo wachtwoordzin toohello sleutelkluis te uploaden.

 ![Ubuntu 16.04 Setup](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. Voltooi partitioneren.

 ![Ubuntu 16.04 Setup](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. Als u Hallo VM opstart en wordt gevraagd een wachtwoordzin, gebruikt u Hallo wachtwoordzin die u hebt opgegeven in stap 3.

 ![Ubuntu 16.04 Setup](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. Hallo VM voorbereiden voor het uploaden naar Azure met behulp [deze instructies](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/). Hallo laatste stap (inrichting hello VM) niet nog uitgevoerd.

Versleuteling toowork configureren met Azure door Hallo volgende te doen:

1. Maak een bestand onder /usr/local/sbin/azure_crypt_key.sh, met inhoud in het volgende script Hallo Hallo. Betalen aandacht toohello KeyFileName, omdat het Hallo wachtwoordzin-bestandsnaam gebruikt door Azure.

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. Hallo crypt config in wijzigen */etc/crypttab*. Dit ziet er als volgt uit:
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. Als u wilt bewerken *azure_crypt_key.sh* in Windows en u gekopieerd tooLinux, voer `dos2unix /usr/local/sbin/azure_crypt_key.sh`.

4. Uitvoermachtigingen toohello script toevoegen:
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. Bewerken */etc/initramfs-tools/modules* door regels toe te voegen:
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. Voer `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` te laten treden.

7. Nu u kunt inrichting ervan ongedaan Hallo VM.

 ![Ubuntu 16.04 Setup](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. De volgende stap toohello gaan en [uw VHD uploaden](#upload-encrypted-vhd-to-an-azure-storage-account) in Azure.

##### <a name="opensuse-132"></a>openSUSE 13.2
tooconfigure versleuteling tijdens de installatie van de distributie van Hallo Hallo te volgen:
1. Wanneer u Hallo schijven partitioneren, selecteert u **versleutelen Volume groep**, en voer vervolgens een wachtwoord. Dit is Hallo wachtwoord dat u de sleutelkluis tooyour wordt geüpload.

 ![openSUSE 13.2 instellen](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. Hallo VM die gebruikmaakt van uw wachtwoord worden opgestart.

 ![openSUSE 13.2 instellen](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. Prepare Hallo VM voor het uploaden van tooAzure door Hallo-instructies in [een SLES of openSUSE virtuele machine voorbereiden voor Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131). Hallo laatste stap (inrichting hello VM) niet nog uitgevoerd.

tooconfigure versleuteling toowork met Azure, Hallo te volgen:
1. Hallo /etc/dracut.conf bewerken en Hallo volgt regel toe:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. Deze regels door Hallo van Hallo commentaar bestand /usr/lib/dracut/modules.d/90crypt/module-setup.sh:
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. Hallo volgt regel aan Hallo begin van Hallo bestand /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh toevoegen:
 ```
    DRACUT_SYSTEMD=0
 ```
En wijzig alle instanties van:
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
in:
```
    if [ 1 ]; then
```
4. /Usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh bewerken en te toevoegen '# Open LUKS apparaat':

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. Voer `/usr/sbin/dracut -f -v` tooupdate hello initrd.

6. Nu u inrichting ervan ongedaan kunt Hallo VM en [uw VHD uploaden](#upload-encrypted-vhd-to-an-azure-storage-account) in Azure.

##### <a name="centos-7"></a>CentOS 7
tooconfigure versleuteling tijdens de installatie van de distributie van Hallo Hallo te volgen:
1. Selecteer **mijn gegevens versleutelen** wanneer u schijven partitioneren.

 ![CentOS 7 Setup](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. Zorg ervoor dat **versleutelen** is geselecteerd voor de basispartitie.

 ![CentOS 7 Setup](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. Geef een wachtwoordzin. Dit is Hallo wachtwoordzin dat u de sleutelkluis tooyour wordt geüpload.

 ![CentOS 7 Setup](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. Als u Hallo VM opstart en wordt gevraagd een wachtwoordzin, gebruikt u Hallo wachtwoordzin die u hebt opgegeven in stap 3.

 ![CentOS 7 Setup](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. Prepare Hallo VM voor het uploaden naar Azure met behulp van Hallo 'CentOS 7.0 +'-instructies in [een CentOS-virtuele machine voorbereiden voor Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70). Hallo laatste stap (inrichting hello VM) niet nog uitgevoerd.

6. Nu u inrichting ervan ongedaan kunt Hallo VM en [uw VHD uploaden](#upload-encrypted-vhd-to-an-azure-storage-account) in Azure.

tooconfigure versleuteling toowork met Azure, Hallo te volgen:

1. Hallo /etc/dracut.conf bewerken en Hallo volgt regel toe:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. Deze regels door Hallo van Hallo commentaar bestand /usr/lib/dracut/modules.d/90crypt/module-setup.sh:
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. Hallo volgt regel aan Hallo begin van Hallo bestand /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh toevoegen:
```
    DRACUT_SYSTEMD=0
```
En wijzig alle instanties van:
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
tot
```
    if [ 1 ]; then
```
4. Bewerk /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh en dit na '# Open LUKS apparaat' hello toevoegen:
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. Voer Hallo ' / usr/sbin/dracut - f - v ' tooupdate hello initrd.

![CentOS 7 Setup](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a>Versleutelde VHD tooan Azure storage-account uploaden
Nadat BitLocker-versleuteling of DM-Crypt versleuteling is ingeschakeld, gecodeerd Hallo lokale VHD behoeften toobe geüpload tooyour storage-account.

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a>Hallo schijfversleuteling geheim voor Hallo vooraf zijn versleuteld VM tooyour sleutelkluis uploaden
Hallo-schijfversleuteling geheim dat u hebt verkregen moet eerder worden geüpload als een geheim in de sleutelkluis. Hallo sleutelkluis moet toohave schijfversleuteling en machtigingen die zijn ingeschakeld voor uw Azure AD-client.

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a>Schijf versleuteling geheim niet versleuteld met een KEK-sleutel
tooset up Hallo geheim in de sleutelkluis, gebruik [Set AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret). Als u een virtuele Windows-machine hebt, Hallo bek bestand is gecodeerd als een base64-tekenreeks en vervolgens geüpload tooyour sleutelkluis met Hallo `Set-AzureKeyVaultSecret` cmdlet. Voor Linux Hallo wachtwoordzin in als een base64-tekenreeks is gecodeerd en vervolgens geüpload toohello sleutelkluis. Bovendien moet u ervoor zorgen dat Hallo tags te volgen zijn ingesteld bij het maken van Hallo geheim in de sleutelkluis Hallo.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

Gebruik Hallo `$secretUrl` in de volgende stap Hallo voor [koppelen Hallo OS-schijf zonder KEK](#without-using-a-kek).

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a>Schijf versleuteling geheim is versleuteld met een KEK-sleutel
Voordat u Hallo geheime toohello sleutelkluis uploadt, kunt u deze desgewenst met een sleutel versleutelingssleutel coderen. Gebruik Hallo wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst versleutelen met de belangrijkste versleutelingssleutel Hallo Hallo-geheim. Hello uitvoer van deze bewerking wrap is een base64-URL gecodeerde tekenreeks, die u vervolgens als een geheim uploaden kunt via Hallo [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

Gebruik `$KeyEncryptionKey` en `$secretUrl` in de volgende stap Hallo voor [koppelen Hallo OS-schijf met een KEK](#using-a-kek).

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a>Geef een geheime URL wanneer u een besturingssysteemschijf koppelen
#### <a name="without-using-a-kek"></a>Zonder een KEK-sleutel
Terwijl u Hallo OS-schijf toevoegen wilt, moet u toopass `$secretUrl`. Hallo-URL is gegenereerd in Hallo 'schijfversleuteling geheim niet versleuteld met een KEK' sectie.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a>Met behulp van een KEK-sleutel
Wanneer u Hallo OS-schijf toegevoegd, `$KeyEncryptionKey` en `$secretUrl`. Hallo-URL is gegenereerd in Hallo 'schijfversleuteling geheim niet versleuteld met een KEK' sectie.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a>Download deze handleiding
U kunt deze handleiding downloaden van Hallo [TechNet-galerie](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).

## <a name="for-more-information"></a>Voor meer informatie
[Verken Azure Disk Encryption met Azure PowerShell - deel 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[Azure Disk Encryption met Azure PowerShell - deel 2 verkennen](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
