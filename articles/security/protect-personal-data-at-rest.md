---
title: aaaAzure Bescherm persoonlijke gegevens in rust met versleuteling | Microsoft Docs
description: In dit artikel maakt deel uit van een reeks helpt u Azure tooprotect persoonlijke gegevens gebruiken
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a>Azure versleutelingstechnologieën: beveiligen van persoonlijke gegevens in rust met versleuteling

In dit artikel helpt u begrijpen en gebruiken van Azure versleuteling technologieën toosecure gegevens in rust.

Versleuteling van gegevens in rust is essentieel als een best practice tooprotect gevoelige of persoonlijke gegevens en toomeet naleving en gegevens privacy-vereisten.
Codering in rust is ontworpen tooprevent Hallo kwaadwillende persoon toegang krijgen tot gegevens van niet-versleuteld Hallo door ervoor te zorgen Hallo gegevens worden versleuteld op de schijf.

## <a name="scenario"></a>Scenario 

Een bedrijf grote cruise, gevestigd in de Verenigde Staten Hallo breidt de bewerkingen toooffer routes in Hallo Middellandse, en Baltische veiligheid, evenals Hallo Florida. toosupport deze inspanningen, heeft deze meerdere kleinere cruise regels op basis van Italië, Duitsland, Denemarken en Hallo VK verkregen

Hallo bedrijf maakt gebruik van Microsoft Azure toostore bedrijfsgegevens Hallo cloud. Dit kan werknemer en/of klantgegevens zoals omvatten:

- adressen
- telefoonnummers
- BTW-id 's
- medische informatie
- creditcardgegevens

Hallo bedrijf moet Hallo privacy van werknemers en klanten gegevens beveiligen tijdens het maken van gegevens toegankelijk toothose afdelingen die u nodig hebt. (zoals salarissen en -reserveringen afdelingen)

Hallo cruise regel onderhoudt ook een grote database van derden en loyaliteit voor leden die persoonlijke gegevens tootrack relaties met de huidige en eerdere klanten bevat.

### <a name="problem-statement"></a>Probleemformulering

Hallo bedrijf moet Hallo privacy van klanten en werknemers persoonlijke gegevens beveiligen tijdens het maken van gegevens toegankelijk toothose afdelingen die u nodig hebt (zoals salarissen en -reserveringen afdelingen). Deze persoonlijke gegevens buiten Hallo zakelijke beheerde Datacenter wordt opgeslagen en wordt niet beheerd van het bedrijf Hallo fysieke.

### <a name="company-goal"></a>Bedrijf-doel

Als onderdeel van een strategie voor een meerlaagse beveiliging van defense-in-depth is een bedrijf doel tooensure dat alle gegevensbronnen die persoonlijke gegevens bevatten zijn versleuteld, met inbegrip van die zich in de cloud-opslag. Als niet-gemachtigde personen voordeel toegang toohello persoonlijke gegevens, moet deze zich in een formulier dat het onleesbaar verschijnt. Versleuteling toepassen, moet eenvoudig of transparante – voor gebruikers en beheerders.

## <a name="solutions"></a>Oplossingen

Azure-services bieden meerdere hulpprogramma's en technologieën toohelp u persoonlijke gegevens in rust beveiligen door deze te coderen.

### <a name="azure-key-vault"></a>Azure Key Vault

[Azure Sleutelkluis](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) biedt een veilige opslag voor Hallo sleutels tooencrypt gegevens in rust in de Azure-services gebruikt en wordt aanbevolen Hallo basisonderdelen opslag en het beheer van de oplossing. Sleutelbeheer versleuteling is essentieel toosecuring opgeslagen gegevens.

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a>Hoe gebruik ik Azure Key Vault tooprotect sleutels die persoonlijke gegevens te versleutelen?

toouse Azure Sleutelkluis, moet u een abonnement tooan Azure-account. U moet ook Azure PowerShell is geïnstalleerd. Stappen omvatten het gebruik van PowerShell-cmdlets toodo Hallo volgende:

1. Verbinding maken met tooyour abonnementen

2. Een sleutelkluis maken

3. Een sleutel of geheim toohello sleutelkluis toevoegen

4. Toepassingen die van de sleutelkluis Hallo met Azure Active Directory gebruikmaken registreren

5. Autoriseren hello toepassingen toouse Hallo sleutel of geheim

een sleutelkluis toocreate Hallo New-AzureRmKeyVault PowerShell-CmDlt gebruiken. U kunt een kluisnaam, de naam van een resourcegroep en de geografische locatie wordt toegewezen. U gebruikt de kluisnaam Hallo bij het beheren van sleutels via andere Cmdlets. Toepassingen die gebruikmaken van de kluis Hallo via Hallo REST-API wordt Hallo vault URI gebruiken.

Azure Sleutelkluis een softwarematig beveiligde sleutel voor u kunt opgeven of u kunt een bestaande sleutel in importeren een. PFX-bestand. U kunt ook geheimen (wachtwoorden) opslaan in Hallo kluis.

U kunt ook een sleutel in uw lokale HSM genereren en overdragen tooHSMs in Hallo Sleutelkluis-service, zonder Hallo sleutel Hallo HSM-grens verlaat.

Voor gedetailleerde instructies over het gebruik van Azure Sleutelkluis, volg de stappen Hallo in [aan de slag met Azure Sleutelkluis.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)

Zie voor een lijst van PowerShell-Cmdlets gebruikt met Azure Key Vault [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).

### <a name="azure-disk-encryption-for-windows"></a>Azure Disk Encryption voor Windows

[Azure Disk Encryption for Windows en Linux IaaS VM's](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) beschermt persoonlijke gegevens in rust op Azure virtuele machines en kan worden geïntegreerd met Azure Sleutelkluis. Maakt gebruik van Azure Disk Encryption [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows en [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux tooencrypt Hallo beide OS en Hallo gegevensschijven. Azure Disk Encryption wordt ondersteund op Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 en op Windows 8 en Windows 10-clients.

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a>Hoe gebruik ik Azure Disk Encryption tooprotect persoonlijke gegevens?

toouse Azure Disk Encryption, moet u een abonnement tooan Azure-account. tooenable Azure Disk Encryption for Windows en Linux-machines Hallo te volgen:

1. Gebruik hello Azure Disk Encryption Resource Manager-sjabloon, PowerShell of Hallo opdrachtregelinterface (CLI) tooenable schijfversleuteling en geef de configuratie van versleuteling. 

2. Verleen toegang toohello Azure-platform tooread Hallo versleuteling materiaal uit de sleutelkluis.

3. Geef een Azure Active Directory (AAD) toepassing identiteit toowrite Hallo encryption key wezenlijke tooyour sleutelkluis.

Azure Hallo VM en Hallo sleutelkluis configuratie bijwerken en uw versleutelde virtuele machine instellen.

Wanneer u uw sleutelkluis toosupport Azure Disk Encryption instelt, kunt u een sleutel versleutelingssleutel (KEK-sleutel) toevoegen voor extra beveiliging en toosupport back-up van versleutelde virtuele machines.

![](media/protect-personal-data-at-rest/create-key.png)

Gedetailleerde instructies voor het specifieke implementatiescenario's beschreven en gebruikerservaringen zijn opgenomen in [Azure Disk Encryption for Windows en Linux IaaS VM's.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)

### <a name="azure-storage-service-encryption"></a>Azure Storage Service-versleuteling

[Azure Storage Service versleuteling (SSE) voor gegevens in rust](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) helpt u bij het beveiligen en uw toomeet gegevens beveiligt uw organisatie beveiliging en naleving verplichtingen. Azure Storage automatisch versleutelt uw gegevens dankzij 256-bits AES-versleuteling voorafgaande toopersisting toostorage en ontsleutelt deze met een eerdere tooretrieval. Deze service is beschikbaar voor Azure Blobs en bestanden.

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a>Hoe gebruik ik de versleuteling van de opslagruimte tooprotect persoonlijke gegevens?

tooenable Storage-Service: versleuteling, Hallo te volgen:

1. Meld u aan bij hello Azure-portal.

2. Selecteer een opslagaccount.

3. Selecteer in de instellingen onder sectie van de Blob-Service hello, versleuteling.

4. Selecteer onder Hallo sectie File-Service, versleuteling.

Nadat u op de instelling voor wachtwoordversleuteling hello, kunt u in- of uitschakelen van de versleuteling van de opslagruimte.

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

Nieuwe gegevens worden versleuteld. Gegevens in de bestaande bestanden in dit opslagaccount wordt onversleuteld blijven.

Kopieer de gegevens toohello storage-account met een van de volgende methoden Hallo na het inschakelen van versleuteling:

1. Kopieer blobs of bestanden met Hallo [AzCopy-opdrachtregelprogramma](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).

2. [Een gebruik van SMB-bestandsshare koppelen](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) zodat u een hulpprogramma zoals Robocopy toocopy bestanden gebruiken kunt.

3. Kopiëren van blob of bestand gegevens tooand van blob-opslag of tussen opslagaccounts met [Opslagclientbibliotheken zoals .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).

4.  Gebruik een [Opslagverkenner](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload blobs tooyour storage-account met versleuteling ingeschakeld.

### <a name="transparent-data-encryption"></a>Transparante gegevensversleuteling

Transparent Data Encryption (TDE) is een functie in SQL Azure waarmee u gegevens op beide Hallo-database en server niveaus kunt versleutelen. TDE is nu standaard ingeschakeld op alle nieuwe databases. TDE voert realtime i/o-versleuteling en ontsleuteling van Hallo gegevens en logboekbestanden.

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a>Hoe gebruik ik TDE tooprotect persoonlijke gegevens?

U kunt TDE via hello Azure-portal configureren met behulp van Hallo REST-API of met behulp van PowerShell. tooenable TDE op een bestaande database met behulp van hello Azure Portal Hallo te volgen:

1. Ga naar hello Azure portal op <https://portal.azure.com> en meld u met uw Azure-beheerder of bijdrager-account.

2. Klik op tooBROWSE op Hallo links koptekst, en klik op SQL-databases.

3. Met SQL-databases die zijn geselecteerd in het linkerdeelvenster hello, klikt u op de gebruikersdatabase.

4. Klik in de databaseblade hello, alle instellingen.

5. Klik op de blade instellingen hello, Transparent data encryption onderdeel tooopen Hallo Transparent data versleuteling blade.

6. Hallo Data encryption blade verplaatsen Hallo Data encryption knop tooOn en klik op opslaan (bovenaan Hallo Hallo pagina) tooapply Hallo-instelling. Hallo coderingsstatus wordt bij benadering Hallo voortgang van Hallo transparante gegevensversleuteling.

![Inschakelen van gegevensversleuteling](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

Instructies over hoe tooenable TDE en informatie over het decoderen van databases TDE beveiligd en nog veel meer u in Hallo artikel vindt [Transparent Data Encryption met Azure SQL Database.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)

## <a name="summary"></a>Samenvatting

Hallo bedrijf kunt doelstelling van het versleutelen van persoonlijke gegevens die zijn opgeslagen in Azure-cloud Hallo uitvoeren. Ze kunnen dit doen met behulp van Azure Disk Encryption gehele volumes te beveiligen. Dit kan omvatten zowel Hallo besturingssysteem en gegevensbestanden die persoonlijk gegevens en andere gevoelige gegevens bevatten. Versleuteling van Azure Storage-Service kan worden gebruikt tooprotect persoonlijke gegevens die zijn opgeslagen in blobs en bestanden. Voor gegevens die zijn opgeslagen in Azure SQL-databases, beschermt met transparante gegevensversleuteling van niet-geautoriseerde blootstelling van persoonlijke gegevens.

Hallo bedrijf kunt tooprotect Hallo sleutels die gebruikt tooencrypt gegevens in Azure zijn, Azure Sleutelkluis. Dit Hallo beheerproces stroomlijnt en schakelt Hallo bedrijf toomaintain beheer van sleutels die toegang tot en persoonlijke gegevens te versleutelen.

## <a name="next-steps"></a>Volgende stappen

- [Handleiding voor probleemoplossing voor Azure Disk Encryption](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [Een virtuele Machine van Azure versleutelen](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [Versleuteling van gegevens in Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [Versleuteling van Azure DB Cosmos-database in rust](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
