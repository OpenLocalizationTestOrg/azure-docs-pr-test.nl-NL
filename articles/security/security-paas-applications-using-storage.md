---
title: aaaSecuring PaaS-toepassingen met behulp van Azure Storage | Microsoft Docs
description: " Meer informatie over Azure Storage security best practices voor het beveiligen van uw PaaS-web- en mobiele toepassingen. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: TomShinder
ms.openlocfilehash: 3fed75cb121e7f32eb8b948ee12ca35fb25eca7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-storage"></a>Beveiligen van PaaS-webtoepassingen en mobiele toepassingen met behulp van Azure Storage
In dit artikel bespreken we een verzameling van Azure Storage aanbevolen beveiligingsprocedures voor het beveiligen van uw PaaS-webtoepassingen en mobiele toepassingen. Deze aanbevolen procedures zijn afgeleid van onze ervaring met Azure en Hallo ervaringen van klanten, zoals zelf.

Hallo [Azure Storage-beveiligingshandleiding](../storage/common/storage-security-guide.md) bevat een schat voor gedetailleerde informatie over Azure Storage en beveiliging.  In dit artikel worden op hoog niveau enkele Hallo concepten gevonden in het Hallo-beveiligingshandleiding en koppelingen toohello beveiligingshandleiding, evenals andere bronnen voor meer informatie.

## <a name="azure-storage"></a>Azure Storage
Azure maakt het mogelijk toodeploy en gebruik opslag op manieren niet eenvoudig haalbare lokale. U kunt een hoge mate van schaalbaarheid en beschikbaarheid met relatief weinig moeite bereiken met Azure storage. Is Azure storage Hallo foundation niet alleen voor Windows en Linux Azure Virtual Machines, kan het ook grote gedistribueerde toepassingen ondersteunen.

Azure storage biedt Hallo volgende vier services: Blob storage, Table storage, Queue storage en File storage. toolearn meer, Zie [tooMicrosoft inleiding Azure Storage](../storage/storage-introduction.md).

## <a name="best-practices"></a>Aanbevolen procedures
In dit artikel komen Hallo aanbevolen procedures te volgen:

- Beveiliging:
   - Shared Access Signatures (SAS)
   - Beheerde schijven
   - RBAC (op rollen gebaseerd toegangsbeheer)

- Versleuteling van opslag:
   - Versleuteling aan de clientzijde voor waardevolle gegevens
   - Azure Disk Encryption voor virtuele machines (VM's)
   - Storage Service-versleuteling

## <a name="access-protection"></a>Netwerktoegangsbeveiliging
### <a name="use-shared-access-signature-instead-of-a-storage-account-key"></a>Shared Access Signature gebruiken in plaats van de sleutel van een opslagaccount

In een IaaS-oplossing, meestal met Windows Server of Linux virtuele machines met bestanden beveiligd tegen openbaarmaking en beveiligingsactiviteiten bedreigingen met behulp van de toegangsmechanismen. U wilt gebruiken op Windows [toegangsbeheerlijsten (ACL)](../virtual-network/virtual-networks-acl.md) en op Linux, u waarschijnlijk gebruikt [type chmod](https://en.wikipedia.org/wiki/Chmod). In wezen, dit is precies wat u zou doen als u bestanden op een server in uw eigen datacenter vandaag zijn beveiligt.

PaaS verschilt. Een van Hallo meest voorkomende manieren toostore bestanden in Microsoft Azure is toouse [Azure Blob storage](../storage/storage-dotnet-how-to-use-blobs.md). Een verschil tussen de Blob storage en andere bestandsopslag is Hallo bestand i/o- en Hallo beveiligingsmethoden die worden geleverd met i/o bestand.

Toegangsbeheer is essentieel. toohelp beheren van toegang tot tooAzure opslag, Hallo wordt gegenereerd twee 512-bits opslagaccountsleutels (SAKs) wanneer u [een opslagaccount maken](../storage/common/storage-create-storage-account.md). Hallo redundantieniveau voor sleutel maakt het mogelijk voor u tooavoid service interrupts tijdens routinematige sleutel worden gedraaid.

Toegangssleutels voor opslag moeten hoge prioriteit geheimen zijn en alleen toegankelijk toothose verantwoordelijk voor het toegangsbeheer voor opslag. Als mensen met verkeerde Hallo toegang toothese sleutels, kan ze hebben volledige controle over opslag en vervangen, verwijderen of bestanden toostorage toevoegen. Dit omvat malware en andere typen inhoud die u kunt niet optimaal van uw organisatie of voor uw klanten.

U moet nog steeds een tooobjects manier tooprovide toegang in de opslag. meer gedetailleerde tooprovide toegang tot u kunt profiteren van [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS). Hallo SAS maakt het mogelijk voor u tooshare specifieke objecten in de opslag voor een vooraf gedefinieerde tijdsinterval en met specifieke machtigingen. Een Shared Access Signature kunt u toodefine:

- via welke Hallo SAS geldig is, met inbegrip van de begin- en verlooptijd Hallo Hallo Hello-interval.
- Hallo machtigingen verleend door Hallo SAS. Bijvoorbeeld, kan een SAS voor een blob verlenen gebruiker lezen en schrijven machtigingen toothat blob, maar niet verwijderen machtigingen.
- Een optionele IP-adres of het bereik van IP-adressen waaruit Azure Storage accepteert Hallo SAS. U kunt bijvoorbeeld een bereik met IP-adressen die behoren tooyour organisatie opgeven. Dit biedt een andere meting van beveiliging voor uw SAS.
- Hallo-protocol gedurende welke Azure Storage Hallo SAS accepteert. U kunt deze optionele parameter toorestrict toegang tooclients via HTTPS gebruiken.

SAS kunt u de gewenste tooshare van tooshare inhoud Hallo manier zonder het vrijgeven van uw toegangscodes voor opslag. Altijd via SAS in uw toepassing is een veilige manier tooshare uw opslagresources zonder uw opslagaccountsleutels gevaar te brengen.

toolearn meer, Zie [handtekeningen voor gedeelde toegang met behulp van](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS). Zie voor meer informatie over mogelijke risico's en aanbevelingen toomitigate toolearn die risico's, [Best practices wanneer via SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

### <a name="use-managed-disks-for-vms"></a>Beheerde schijven voor virtuele machines gebruiken

Wanneer u de optie [Azure beheerd schijven](../storage/storage-managed-disks-overview.md), Azure beheert Hallo storage-accounts die u voor uw VM-schijven gebruikt. Toodo hoeft u Hallo-type van de schijf (Premium of standaard) en de schijfgrootte Hallo; kiezen Azure-opslag doet Hallo rest. U hebt geen tooworry over schaalbaarheidsbeperkingen die mogelijk anders tooyou toomultiple storage-accounts vereist.

toolearn meer, Zie [Veelgestelde vragen over beheerde en onbeheerde premium-schijven](../storage/storage-faq-for-disks.md).

### <a name="use-role-based-access-control"></a>Op rollen gebaseerde toegangsbeheer gebruiken

Eerder besproken met behulp van Shared Access Signature (SAS) toogrant beperkte toegang tooobjects in uw storage-account tooother-clients zonder dat de sleutel van uw account-opslagaccount. Soms is Hallo risico's die zijn gekoppeld aan een bepaalde bewerking op basis van uw opslagaccount opwegen tegen Hallo voordelen van SAS. Soms is het eenvoudiger toomanage toegang op andere manieren.

Een andere manier toomanage toegang is toouse [rollen gebaseerd toegangsbeheer](../active-directory/role-based-access-control-what-is.md) (RBAC). Met RBAC, richten op uw werknemers Hallo exacte machtigingen die ze nodig hebben, op basis van Hallo nodig tooknow en minimale bevoegdheden beveiligingsprincipes. Te veel machtigingen kunnen een account tooattackers worden blootgesteld. Te weinig machtigingen betekent dat werknemers hun werk efficiënt kunnen niet ophalen. RBAC kunt u dit probleem oplossen door het aanbieden van Geavanceerd toegangsbeheer voor Azure. Dit is noodzakelijk voor organisaties die tooenforce beveiligingsbeleid voor toegang tot gegevens willen.

U kunt gebruikmaken van ingebouwde RBAC-rollen in Azure tooassign bevoegdheden toousers. Overweeg het gebruik van Storage Account Inzender voor cloudoperators die toomanage storage-accounts en klassieke Storage Account Inzender rol toomanage klassieke opslagaccounts nodig. Voor cloudoperators die moeten toomanage VM's, maar niet Hallo virtueel netwerk of opslag account toowhich die ze zijn verbonden, kunt u deze rol van de virtuele Machine Inzender toohello toe te voegen.

Organisaties die niet afgedwongen door toegangsbeheer gegevens dankzij het gebruik van mogelijkheden, zoals RBAC mogelijk meer bevoegdheden beschikt dan nodig is voor hun gebruikers geven. Dit kan ertoe leiden toodata inbreuk doordat bepaalde gebruikers toegang toodata ze in de eerste plaats Hallo mag geen.

toolearn Zie informatie over RBAC:

- [Op rollen gebaseerde toegangsbeheer van Azure](../active-directory/role-based-access-control-configure.md)
- [Ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md)
- [Azure Storage-beveiligingshandleiding](../storage/common/storage-security-guide.md) voor informatie over hoe toosecure uw storage-account met RBAC

## <a name="storage-encryption"></a>Versleuteling van opslag
### <a name="use-client-side-encryption-for-high-value-data"></a>Client-side '-versleuteling gebruiken voor waardevolle gegevens

Hiermee schakelt u versleuteling aan clientzijde tooprogrammatically u gegevens die onderweg voordat u uploadt tooAzure opslag versleutelen en ontsleutelen van gegevens via een programma bij het ophalen van het uit de opslag.  Dit biedt versleuteling van gegevens die worden verzonden, maar het biedt ook versleuteling van gegevens in rust.  Versleuteling aan clientzijde is de veiligste methode Hallo van het versleutelen van uw gegevens maar toomake programmatische wijzigingen tooyour toepassing, moet u en opgezet Sleutelbeheer processen.

Versleuteling aan clientzijde kunt u ook toohave enige controle over uw versleutelingssleutels.  U kunt genereren en beheren van uw eigen versleutelingssleutels.  Versleuteling aan clientzijde maakt gebruik van een techniek envelop waar hello Azure storage-clientbibliotheek genereert een inhoud versleutelingssleutel (CEK) die wordt vervolgens verpakt (versleuteld) met de belangrijkste versleutelingssleutel hello (KEK-sleutel). Hallo KEK wordt aangeduid met een sleutel-id en kan een asymmetrisch sleutelpaar of een symmetrische sleutel en kunnen worden beheerd lokaal of opgeslagen [Azure Key Vault](../key-vault/key-vault-whatis.md).

Versleuteling aan clientzijde is ingebouwd in Hallo Java en Hallo-opslagclientbibliotheken voor .NET.  Zie [Client-Side-versleuteling en Azure Key Vault voor Microsoft Azure Storage](../storage/storage-client-side-encryption.md) voor informatie over het coderen van gegevens binnen clienttoepassingen en genereren en beheren van uw eigen versleutelingssleutels.

### <a name="azure-disk-encryption-for-vms"></a>Azure Disk Encryption voor virtuele machines
Azure Disk Encryption is een functie waarmee u uw Windows- en Linux IaaS-schijven voor virtuele machine versleutelen. Azure Disk Encryption maakt gebruik van Hallo bedrijfstak standaard BitLocker-functie van Windows hello DM-Crypt functie en van Linux tooprovide volumeversleuteling voor Hallo OS en Hallo gegevensschijven. Hallo-oplossing is geïntegreerd met Azure Key Vault toohelp u controleren en beheren van Hallo schijfversleuteling sleutels en geheimen in uw abonnement sleutelkluis. Hallo oplossing zorgt er ook voor dat alle gegevens op schijven van de virtuele machine Hallo zijn versleuteld in rust in uw Azure-opslag.

Zie [Azure Disk Encryption for Windows and Linux IaaS VM's](azure-security-disk-encryption.md).

### <a name="storage-service-encryption"></a>Storage Service-versleuteling
Wanneer [Service Opslagversleuteling](../storage/storage-service-encryption.md) voor File storage is ingeschakeld, Hallo gegevens worden versleuteld automatisch met AES-256-versleuteling. Microsoft verwerkt alle Hallo versleuteling, ontsleuteling en sleutelbeheer. Deze functie is beschikbaar voor LRS- en GRS redundantie typen.

## <a name="next-steps"></a>Volgende stappen
In dit artikel geïntroduceerd tooa verzameling van Azure Storage aanbevolen beveiligingsprocedures voor het beveiligen van uw PaaS-webtoepassingen en mobiele toepassingen. toolearn meer informatie over het beveiligen van uw PaaS-implementaties, Zie:

- [PaaS-implementaties beveiligen](security-paas-deployments.md)
- [PaaS-webtoepassingen en mobiele toepassingen met Azure App Services beveiligen](security-paas-applications-using-app-services.md)
- [PaaS-databases in Azure beveiligen](security-paas-applications-using-sql.md)
