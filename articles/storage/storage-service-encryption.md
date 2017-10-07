---
title: Service-versleuteling van opslag voor gegevens in rust aaaAzure | Microsoft Docs
description: 'Gebruik hello Azure Storage-Service: versleuteling functie tooencrypt uw Azure-blobopslag op Hallo servicezijde bij het opslaan van gegevens Hallo en ontsleutelen als Hallo gegevens worden opgehaald.'
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: edabe3ee-688b-41e0-b34f-613ac9c3fdfd
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: robinsh
ms.openlocfilehash: 304f1c21200f86f2084ce98788b2fc7ca893d1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-service-encryption-for-data-at-rest"></a>Azure Storage Service-versleuteling voor inactieve gegevens
Azure Storage Service versleuteling (SSE) voor gegevens in rust helpt u bij het beveiligen en uw toomeet gegevens beveiligt uw organisatie beveiliging en naleving verplichtingen. Met deze functie van Azure Storage automatisch versleutelt uw gegevens voorafgaande toopersisting toostorage en ontsleutelt voorafgaande tooretrieval. Hallo-versleuteling, ontsleuteling en sleutelbeheer zijn volledig transparant toousers.

Hallo volgende secties geven de gedetailleerde instructies over hoe toouse Hallo versleuteling van opslag-functies, evenals Hallo ondersteund scenario's en gebruikerservaringen.

## <a name="overview"></a>Overzicht
Azure Storage biedt een uitgebreide reeks beveiligingsmogelijkheden die samen ontwikkelaars kunnen toobuild beveiligde toepassingen. Gegevens onderweg tussen een toepassing en Azure kunnen worden beveiligd met behulp van [versleuteling van de Client-Side](storage-client-side-encryption.md), HTTPs- of SMB 3.0. Versleuteling van opslag-Service biedt versleuteling in rust, verwerking versleuteling, ontsleuteling en Sleutelbeheer op een compleet transparante wijze. Alle gegevens worden versleuteld met behulp van 256-bits [AES-versleuteling](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), een van de sterkste blok Hallo coderingen beschikbaar.

SSE werkt Hallo door gegevens te coderen wanneer deze tooAzure opslag geschreven wordt en kan worden gebruikt voor Azure Blob Storage en File Storage. De Tool werkt voor Hallo volgende:

* Standard-opslag: Algemeen opslagaccounts die voor Blobs en File storage en Blob storage-accounts
* Premium Storage 
* Alle redundantie niveaus (LRS, ZRS, GRS en RA-GRS)
* Azure Resource Manager opslagaccounts (maar niet klassiek) 
* Alle regio's.

toolearn meer, Raadpleeg Veelgestelde vragen over toohello.

tooenable of schakelt u versleuteling van opslag-Service voor een opslagaccount, meld u aan bij Hallo [Azure-portal](https://portal.azure.com) en selecteer een opslagaccount. Blade beleidinstellingen Hallo Hallo sectie van de Blob-Service zoekt, zoals weergegeven in deze schermafbeelding en klik op versleuteling.

![De optie versleuteling Portal schermopname](./media/storage-service-encryption/image1.png)
<br/>*Afbeelding 1: SSE inschakelen voor Blob-Service (stap 1)*

![De optie versleuteling Portal schermopname](./media/storage-service-encryption/image3.png)
<br/>*Afbeelding 2: SSE inschakelen voor File-Service (stap 1)*

Nadat u op de instelling voor wachtwoordversleuteling hello, kunt u in- of uitschakelen van de versleuteling van de opslagruimte.

![Eigenschappen van de portal schermopname van versleuteling](./media/storage-service-encryption/image2.png)
<br/>*Afbeelding 3: SSE inschakelen voor Blob en File-Service (stap 2)*

## <a name="encryption-scenarios"></a>Versleuteling scenario 's
Versleuteling van opslag-Service kan worden ingeschakeld op een niveau storage-account. Eenmaal is ingeschakeld, wordt de klanten ervoor kiezen welke tooencrypt services. Het ondersteunt Hallo klant scenario's te volgen:

* Versleuteling van Blob Storage en File Storage in Resource Manager-accounts.
* Versleuteling van Blob en File-Service in de klassieke opslagaccounts eenmaal gemigreerd tooResource Manager storage-accounts.

SSE heeft Hallo volgende beperkingen:

* Versleuteling van klassieke opslagaccounts wordt niet ondersteund.
* Bestaande gegevens - SSE alleen nieuwe gegevens worden gecodeerd nadat Hallo versleuteling is ingeschakeld. Als u bijvoorbeeld een nieuwe Resource Manager-opslagaccount maken maar versleuteling niet inschakelen en vervolgens het uploaden van BLOB's of gearchiveerde VHD's toothat storage-account en schakelt u SSE, wordt deze blobs niet versleuteld tenzij ze zijn herschreven of gekopieerd.
* Ondersteuning voor Marketplace - versleuteling van virtuele machines gemaakt op basis van inschakelen met behulp van Hallo Marketplace Hallo [Azure-portal](https://portal.azure.com), PowerShell en Azure CLI. Hallo VHD basisinstallatiekopie blijft niet-versleutelde; maar wordt er geen schrijfbewerkingen uitgevoerd worden nadat Hallo VM heeft ingezette versleuteld.
* Tabel en gegevens wachtrijen wordt niet versleuteld.

## <a name="getting-started"></a>Aan de slag
### <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>Stap 1: [maken van een nieuw opslagaccount](storage-create-storage-account.md).
### <a name="step-2-enable-encryption"></a>Stap 2: Versleuteling inschakelen.
U kunt met behulp van Hallo versleuteling inschakelen [Azure-portal](https://portal.azure.com).

> [!NOTE]
> Als u tooprogrammatically inschakelen of Hallo versleuteling van de opslagruimte op een storage-account uitschakelen, kunt u Hallo [REST API van Azure Storage Resource Provider](https://msdn.microsoft.com/library/azure/mt163683.aspx), Hallo [Storage Resource Provider-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/mt131037.aspx), [Azure PowerShell](/powershell/azureps-cmdlets-docs), of Hallo [Azure CLI](storage-azure-cli.md).
> 
> 

### <a name="step-3-copy-data-toostorage-account"></a>Stap 3: Kopieer data toostorage-account
Als u SSE voor Hallo Blob-service inschakelt, worden alle bestaande blobs geschreven toothat storage-account wordt versleuteld. Alle blobs die zich al in de betreffende storage-account worden niet versleuteld totdat ze opnieuw worden geschreven. U kunt Hallo gegevens kopiëren van een storage account tooone met SSE versleuteld, of zelfs SSE- en Hallo blobs kopiëren uit een container tooanother toosure dat eerdere gegevens worden versleuteld. U kunt een van de volgende hulpprogramma's voor tooaccomplish Hallo deze gebruiken. Dit is ook hetzelfde gedrag Hallo voor File Storage.

#### <a name="using-azcopy"></a>Met behulp van AzCopy
AzCopy is een Windows-opdrachtregelprogramma ontworpen voor het kopiëren van gegevens tooand van Microsoft Azure Blob-, bestands- en tabel opslag met behulp van eenvoudige opdrachten met optimale prestaties. U kunt deze toocopy uw blobs of bestanden vanuit een tooanother van de storage-account dat SSE ingeschakeld heeft. 

toolearn meer, gaat u naar [gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md).

#### <a name="using-smb"></a>Gebruik van SMB-
Azure File storage biedt bestandsshares in de cloud van Hallo Hallo standaard SMB-protocol gebruiken. U kunt een bestandsshare koppelen van een client on-premises of in Azure. Zodra gekoppeld, kunnen hulpprogramma's zoals Robocopy gebruikte toocopy bestanden worden via tooAzure bestandsshares. Zie voor meer informatie [hoe toomount Azure-bestandsshare op Windows](storage-file-how-to-use-files-windows.md) en [hoe toomount Azure File share op Linux](storage-how-to-use-files-linux.md).


#### <a name="using-hello-storage-client-libraries"></a>Met behulp van de Opslagclientbibliotheken Hallo
U kunt gegevens tooand voor blob of een bestand kopiëren van blob-opslag of tussen opslagaccounts met behulp van onze uitgebreide set Opslagclientbibliotheken waaronder .NET, C++, Java, Android, Node.js, PHP, Python en Ruby.

toolearn meer, gaat u naar onze [aan de slag met Azure Blob storage met .NET](storage-dotnet-how-to-use-blobs.md).

#### <a name="using-a-storage-explorer"></a>Met behulp van een Opslagverkenner
U kunt een Storage explorer toocreate storage-accounts gebruiken, uploaden en downloaden van gegevens, inhoud van BLOB's weergeven en navigeren door mappen. U kunt een van deze tooupload blobs tooyour storage-account gebruiken met versleuteling ingeschakeld. Sommige Opslagverkenner kunt u gegevens van bestaande blob storage tooa verschillende-container in Hallo storage-account of een nieuw opslagaccount met SSE ingeschakeld ook kopiëren.

toolearn meer, gaat u naar [Azure Storage Explorers](storage-explorers.md).

### <a name="step-4-query-hello-status-of-hello-encrypted-data"></a>Stap 4: De status van de Hallo Hallo versleutelde gegevens
Een bijgewerkte versie van Hallo opslag clientbibliotheken er is geïmplementeerd waarmee u tooquery Hallo status van een object toodetermine als ze zijn versleuteld of niet. Dit is momenteel alleen beschikbaar voor Blob-opslag. Er is ondersteuning voor File storage op Hallo roadmap. 

In Hallo kunt u tussentijd aanroepen [accounteigenschappen ophalen](https://msdn.microsoft.com/library/azure/mt163553.aspx) tooverify die Hallo storage-account is versleuteling ingeschakeld of weergave Hallo eigenschappen van het opslagaccount in hello Azure-portal.

## <a name="encryption-and-decryption-workflow"></a>Versleuteling en ontsleuteling werkstroom
Hier volgt een korte beschrijving van Hallo tokenversleuteling /-ontsleuteling werkstroom:

* Hallo klant schakelt u versleuteling op Hallo storage-account.
* Wanneer de klant schrijfbewerkingen nieuwe gegevens (Blob plaatsen, blok plaatsen, pagina plaatsen, plaatsen bestand enz.) tooBlob Hallo of bestandsopslag; elke schrijfbewerking is versleuteld met 256-bits [AES-versleuteling](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), een van de sterkste blok Hallo coderingen beschikbaar.
* Wanneer Hallo klant moet tooaccess gegevens (Blob ophalen, enzovoort), worden gegevens automatisch ontsleuteld voordat er wordt teruggekeerd toohello gebruiker.
* Als versleuteling is uitgeschakeld, nieuwe schrijfbewerkingen zijn niet langer gecodeerd en bestaande versleutelde gegevens blijven versleuteld totdat herschreven door Hallo-gebruiker. Terwijl versleuteling is ingeschakeld, schrijft tooBlob of opslag van bestanden, worden versleuteld. Hallo-status van de gegevens wijzigen niet met Hallo gebruiker schakelen tussen in-/ uitschakelen versleuteling voor Hallo storage-account.
* Alle versleutelingssleutels zijn opgeslagen, gecodeerd en beheerd door Microsoft.

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>Veelgestelde vragen over Service-versleuteling van opslag voor gegevens in rust
**V: ik heb een bestaande klassieke storage-account. Kan ik SSE deze functie inschakelen?**

A: Nee, SSE wordt alleen ondersteund op Resource Manager storage-accounts.

**V: hoe kan ik gegevens coderen in mijn klassieke storage-account?**

A: u kunt een nieuwe Resource Manager-opslagaccount maken en kopieer uw gegevens met [AzCopy](storage-use-azcopy.md) van uw bestaande klassieke opslagaccount tooyour nieuw Resource Manager storage-account gemaakt. 

Als u migreert uw klassieke storage account tooa Resource Manager storage-account, deze onmiddellijk wordt, wordt het Hallo-type van uw account wordt gewijzigd, maar heeft geen invloed op uw bestaande gegevens. Kan geen nieuwe gegevens geschreven wordt versleuteld alleen na het inschakelen van versleuteling. Zie voor meer informatie [Platform ondersteund migratie van IaaS Resources van klassieke tooResource Manager](https://azure.microsoft.com/blog/iaas-migration-classic-resource-manager/). Houd er rekening mee dat dit wordt alleen ondersteund voor Blob- en -services.

**V: ik heb een bestaand Resource Manager-opslagaccount. Kan ik SSE deze functie inschakelen?**

Ja, maar alleen nieuwe gegevens geschreven A: wordt versleuteld. Deze niet teruggaan en gegevens versleutelen die al aanwezig is. Dit is nog niet ondersteund voor Hallo bestandsvoorbeeld opslag.

**V: ik wil tooencrypt Hallo huidige gegevens in een bestaand opslagaccount van Resource Manager?**

A: u kunt de SSE inschakelen op elk gewenst moment in een Resource Manager-opslagaccount. Gegevens die al aanwezig waren wordt echter niet versleuteld. tooencrypt bestaande gegevens, kunt u ze kopiëren tooanother naam of een andere container en vervolgens verwijdert u niet-versleuteld Hallo-versies.

**V: ik gebruik Premium-opslag; kan ik SSE gebruiken?**

A: Ja, de SSE op zowel Standard-opslag- en Premium-opslag wordt ondersteund.  Premium-opslag wordt niet ondersteund voor Hallo File-Service.

**V: als ik een nieuw opslagaccount maken en inschakelen van SSE en vervolgens een nieuwe virtuele machine maken met dit opslagaccount, betekent dit dat mijn VM is versleuteld?**

A: Ja. Alle schijven gemaakt die gebruikmaken van nieuw opslagaccount Hallo worden versleuteld, zolang ze worden gemaakt nadat de SSE is ingeschakeld. Als de virtuele machine is gemaakt met Azure-marktplaats, Hallo VHD basisinstallatiekopie Hallo blijft niet-versleutelde; maar wordt er geen schrijfbewerkingen uitgevoerd worden nadat Hallo VM heeft ingezette versleuteld.

**V: kan ik nieuwe storage-accounts maken met de SSE ingeschakeld met behulp van Azure PowerShell en Azure CLI**

A: Ja.

**V: hoe veel meer kost Azure Storage als SSE is ingeschakeld?**

A: Er is geen extra kosten.

**V: die Hallo versleutelingssleutels beheert?**

A: Hallo sleutels worden beheerd door Microsoft.

**V: kan ik mijn eigen versleutelingssleutels gebruiken?**

A: Wij werken op het bieden van mogelijkheden voor toobring klanten hun eigen versleutelingssleutels.

**V: kan ik toegang toohello versleutelingssleutels intrekken?**

A: niet op dit moment; Hallo-sleutels worden volledig beheerd door Microsoft.

**V: is SSE standaard ingeschakeld wanneer ik een nieuw opslagaccount maken?**

A: SSE is niet standaard; hello Azure portal tooenable kunt u deze. U kunt deze functie met Hallo REST-API van Storage Resource Provider ook programmatisch inschakelen.

**V: hoe verschilt dit van Azure Disk Encryption?**

A: deze functie is gebruikte tooencrypt gegevens in Azure Blob storage. Hello Azure Disk Encryption is gebruikte tooencrypt besturingssysteem en de gegevensschijven in IaaS VM's. Ga voor meer informatie naar onze [opslag beveiligingshandleiding](storage-security-guide.md).

**V: Wat gebeurt er als ik SSE, inschakelen en vervolgens in te gaan en Azure Disk Encryption op Hallo schijven inschakelen?**

A: dit werkt naadloos. Uw gegevens worden versleuteld door beide methoden.

**V: Mijn storage-account is ingesteld in toobe geo-redundante gerepliceerd. Als ik SSE inschakelt, worden mijn redundante kopie ook versleuteld?**

A: Ja, alle exemplaren van Hallo storage-account zijn versleuteld en alle redundantieopties voor, Zone-redundante opslag (ZRS) lokaal redundante opslag (LRS) Geo-Redundant Storage (GRS) en geografisch redundante opslag met leestoegang (RA-GRS), worden ondersteund.

**V: ik inschakelen niet codering voor mijn storage-account.**

A: is het een Resource Manager-storage-account? Klassieke opslagaccounts worden niet ondersteund. 

**V: is SSE alleen toegestaan in specifieke gebieden?**

A: Hallo SSE is beschikbaar in alle regio's voor Blob-opslag. Neem contact op Hallo Beschikbaarheidssectie voor File storage. 

**V: hoe neem ik iemand als ik problemen hebt of tooprovide feedback wilt?**

A: neemt contact op met [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) van eventuele tooStorage versleuteling van de Service problemen.

## <a name="next-steps"></a>Volgende stappen
Azure Storage biedt een uitgebreide reeks beveiligingsmogelijkheden die samen ontwikkelaars kunnen toobuild beveiligde toepassingen. Voor meer informatie gaat u naar Hallo [opslag beveiligingshandleiding](storage-security-guide.md).

