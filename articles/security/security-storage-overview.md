---
title: aaaSecurity-functies die kunnen worden gebruikt met Azure Storage | Microsoft Docs
description: " Dit artikel bevat een overzicht van hello Azure-beveiliging kernfuncties die kunnen worden gebruikt met Azure Storage. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 521180dc-2cc9-43f1-ae87-2701de7ca6b8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 663cd2705527957d21ff9475a6322b42a16c95e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-overview"></a>Overzicht van Azure-opslag-beveiliging
Azure-opslag is Hallo cloud opslagoplossing voor moderne toepassingen die afhankelijk van duurzaamheid, beschikbaarheid en schaalbaarheid toomeet Hallo behoeften van klanten zijn. Azure Storage biedt een uitgebreide reeks beveiligingsmogelijkheden:

* Hallo-opslagaccount kan worden beveiligd met op rollen gebaseerde toegangsbeheer en Azure Active Directory.
* Gegevens kunnen worden beveiligd tijdens de overdracht tussen een toepassing en Azure met behulp van versleuteling van de Client-Side-, HTTPS- of SMB 3.0.
* Gegevens kunnen worden ingesteld op toobe automatisch versleuteld wanneer geschreven tooAzure opslag met versleuteling van de opslagruimte.
* Besturingssysteem en gegevensschijven die worden gebruikt door virtuele machines kunnen worden ingesteld als toobe versleuteld met Azure Disk Encryption.
* Gedelegeerde toegang toohello gegevensobjecten in Azure Storage kunnen worden verleend met behulp van handtekeningen voor gedeelde toegang.
* Hallo-verificatiemethode die door iemand wordt gebruikt wanneer ze toegang hebben tot opslag kan worden bijgehouden met Storage analytics.

Zie voor meer gedetailleerde kijken beveiliging in Azure Storage, Hallo [Azure Storage-beveiligingshandleiding](../storage/common/storage-security-guide.md). Deze handleiding biedt een diepgaand in Hallo beveiligingsfuncties van Azure Storage zoals toegangscodes voor opslag, gegevensversleuteling onderweg en op rest en storage analytics.

Dit artikel bevat een overzicht van Azure-beveiligingsfuncties die kunnen worden gebruikt met Azure Storage. Tooarticles waarmee details van elk onderdeel, zodat u meer informatie vindt u koppelingen.

Hier volgen Hallo core functies toobe die in dit artikel:

* Op rollen gebaseerd toegangsbeheer
* Gedelegeerde toegang toostorage objecten
* Codering in transit
* Versleuteling op rest/Storage-Service: versleuteling
* Azure Disk Encryption
* Azure Key Vault

## <a name="role-based-access-control-rbac"></a>RBAC (op rollen gebaseerd toegangsbeheer)
U kunt uw storage-account met op rollen gebaseerde toegangsbeheer (RBAC) beveiligen. De toegang beperken op basis van Hallo [moet tooknow](https://en.wikipedia.org/wiki/Need_to_know) en [minimale bevoegdheden](https://en.wikipedia.org/wiki/Principle_of_least_privilege) beveiligingsprincipes is van cruciaal belang voor organisaties die tooenforce beveiligingsbeleid voor toegang tot gegevens willen. Deze toegangsrechten worden verleend door Hallo juiste RBAC-rol toogroups en toepassingen op een bepaalde scope. U kunt [ingebouwde RBAC-rollen](../active-directory/role-based-access-built-in-roles.md), zoals opslag Account Inzender, tooassign toousers bevoegdheden.

Meer informatie:

* [Toegangsbeheer op basis van rollen in Azure Active Directory](../active-directory/role-based-access-control-configure.md)

## <a name="delegated-access-toostorage-objects"></a>Gedelegeerde toegang toostorage objecten
Een shared access signature (SAS) biedt tooresources gedelegeerde toegang in uw opslagaccount. Hallo SAS betekent dat u een client beperkte machtigingen tooobjects in uw storage-account gedurende een bepaalde tijd en met een opgegeven set machtigingen kunt verlenen. U kunt deze beperkte rechten verlenen zonder tooshare de toegangssleutels van uw account. Hallo SAS is een URI die in de queryparameters alle Hallo gegevens die nodig zijn voor geverifieerde toegang tooa storage resource omvat. opslagbronnen tooaccess Hello SAS, Hallo-client moet alleen tooprovide Hallo SAS toohello geschikte constructor of methode.

Meer informatie:

* [Understanding Hallo SAS-model](../storage/common/storage-dotnet-shared-access-signature-part-1.md)
* [Maken en gebruiken van een SAS met Blob-opslag](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)

## <a name="encryption-in-transit"></a>Codering in transit
Versleuteling onderweg is een mechanisme om gegevens te beveiligen wanneer deze worden verzonden via netwerken. U kunt beveiligen met behulp van gegevens met Azure Storage:

* [Versleuteling transportniveau](../storage/common/storage-security-guide.md#encryption-in-transit), zoals HTTPS wanneer u gegevens van of naar Azure Storage overbrengen.
* [Versleuteling Wire](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), zoals versleuteling door SMB 3.0 voor Azure-bestandsshares.
* [Versleuteling aan clientzijde](../storage/common/storage-security-guide.md#using-client-side-encryption-to-secure-data-that-you-send-to-storage), tooencrypt Hallo gegevens voordat deze in opslag en toodecrypt Hallo gegevens overgedragen wordt nadat deze zijn overgebracht buiten een opslag.

Meer informatie over client-side '-versleuteling:

* [Client-Side-versleuteling voor opslag op Microsoft Azure](https://blogs.msdn.microsoft.com/windowsazurestorage/2015/04/28/client-side-encryption-for-microsoft-azure-storage-preview/)
* [Cloud-beveiligingsmaatregelen reeks: versleutelen van gegevens die onderweg](http://blogs.microsoft.com/cybertrust/2015/08/10/cloud-security-controls-series-encrypting-data-in-transit/)

## <a name="encryption-at-rest"></a>Versleuteling 'at rest'
Voor veel organisaties [gegevensversleuteling in rust](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) is een verplichte stap naar privacy, naleving en gegevens onafhankelijkheid van gegevens. Er zijn drie Azure-functies waarmee de codering van gegevens die zich 'in rust':

* [Versleuteling van de opslagruimte](../storage/common/storage-security-guide.md#encryption-at-rest) kunt u toorequest dat Hallo storage-service automatisch coderen van gegevens bij het schrijven van tooAzure opslag.
* [Versleuteling aan clientzijde](../storage/common/storage-security-guide.md#client-side-encryption) biedt ook de functie Hallo van versleuteling in rust.
* [Azure Disk Encryption](../storage/common/storage-security-guide.md#using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) kunt u tooencrypt Hallo OS schijven en gegevensschijven die wordt gebruikt door een virtuele machine voor IaaS.

Meer informatie over versleuteling van de opslagruimte:

* [Azure Storage-Service: versleuteling](https://azure.microsoft.com/services/storage/) is beschikbaar voor [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/). Zie voor informatie over andere typen Azure-opslag, [bestand](https://azure.microsoft.com/services/storage/files/), [schijf (Premium-opslag)](https://azure.microsoft.com/services/storage/premium-storage/), [tabel](https://azure.microsoft.com/services/storage/tables/), en [wachtrij](https://azure.microsoft.com/services/storage/queues/).
* [Azure Storage-Service: versleuteling voor gegevens in rust](../storage/common/storage-service-encryption.md)

## <a name="azure-disk-encryption"></a>Azure Disk Encryption
Azure Disk Encryption voor virtuele machines (VM's) kunt u bedrijfsbeveiligingsbeleid adres- en nalevingsvereisten door uw VM-schijven (inclusief opstart- en gegevensschijven) te versleutelen met sleutels en beleidsregels die u beheert in [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).

Schijfversleuteling voor virtuele machines werkt voor Linux en Windows-besturingssystemen. Sleutelkluis toohelp beveiligt, beheren en het gebruik van uw schijf versleutelingssleutels controleren worden ook gebruikt. Alle Hallo-gegevens in uw VM-schijven in rust versleuteld met behulp van technologie voor bestandsversleuteling industriestandaard in uw Azure Storage-accounts. Hallo schijfversleuteling oplossing voor Windows is gebaseerd op [Microsoft BitLocker-stationsversleuteling](https://technet.microsoft.com/library/cc732774.aspx), en Hallo Linux-oplossing is gebaseerd op [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt).

Meer informatie:

* [Azure Disk Encryption for Windows and Linux IaaS virtuele Machines](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)

## <a name="azure-key-vault"></a>Azure Key Vault
Maakt gebruik van Azure Disk Encryption [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) toohelp u beheren en een schijf-sleutels en geheimen in uw abonnement sleutelkluis terwijl u ervoor zorgt dat alle gegevens in de schijven van de virtuele machine Hallo zijn versleuteld in rust in uw Azure beheren Opslag. U moet Sleutelkluis tooaudit sleutels en gebruik van beleidsregels.

Meer informatie:

* [Wat is Azure Sleutelkluis?](../key-vault/key-vault-whatis.md)
* [Aan de slag met Azure Sleutelkluis](../key-vault/key-vault-get-started.md)
