---
title: overzicht van de versleuteling aaaAzure | Microsoft Docs
description: Meer informatie over verschillende opties voor codering in Azure
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/18/2017
ms.author: barclayn
ms.openlocfilehash: ef9ab46de32b857e99e8fe628a61386b95cf197f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-overview"></a>Overzicht van Azure-versleuteling

Dit artikel bevat een overzicht van hoe de versleuteling wordt gebruikt in Microsoft Azure. Deze heeft Hallo belangrijke gebieden van versleuteling, zoals versleuteling in rust, versleuteling in vlucht en sleutelbeheer met Sleutelkluis. Elke sectie bevat koppelingen voor meer gedetailleerde informatie.

## <a name="encryption-of-data-at-rest"></a>Versleuteling van data-at-rest

Gegevens in rust bevat informatie die zich in de permanente opslag op de fysieke media, in een willekeurige digitale indeling bevindt. Het gaat hierbij om bestanden op magnetische of optische media, gearchiveerde gegevens en gegevens back-ups. Microsoft Azure biedt een verscheidenheid aan gegevens storage solutions toomeet verschillende behoeften, waaronder een bestand, de schijf, blobs en tabelopslag. Microsoft biedt ook versleuteling tooprotect [Azure SQL Database](../sql-database/sql-database-technical-overview.md), [CosmosDB](../cosmos-db/introduction.md), en Azure Data Lake.

Gegevensversleuteling in rust is beschikbaar voor services via hello Azure Software-as-a-Service (SaaS)-Platform-as-a-Service (PaaS), en cloud-modellen Infrastructure-as-a-Service (IaaS). Dit document bevat een overzicht van en resources toohelp biedt u opties voor Azure versleuteling gebruiken.

Zie voor meer discussie gedetailleerde over hoe de gegevens in rust is versleuteld in Azure, Hallo-document met de titel [Azure Data Encryption in rust](azure-security-encryption-atrest.md)

## <a name="azure-encryption-models"></a>Azure versleuteling modellen

Azure ondersteunt verschillende versleuteling modellen, met inbegrip van serverzijde versleuteling met sleutels die service beheerd, met behulp van de klant beheerd sleutels in Azure Key Vault of met behulp van de klant beheerd sleutels op door de klant bewaakte hardware. Versleuteling aan clientzijde kunt u toomanage en store sleutels on-premises of in een andere beveiligde locatie.

### <a name="client-side-encryption"></a>Clientversleuteling

Client-side '-versleuteling wordt buiten Azure uitgevoerd. Versleuteling aan clientzijde omvat:

- Gegevens versleuteld door een toepassing die wordt uitgevoerd in het datacenter van de klant Hallo of door een servicetoepassing
- Gegevens die al is versleuteld wanneer het is ontvangen door Azure.

Met client-side '-versleuteling Hallo cloudserviceprovider heeft geen toegang tot toohello coderingssleutels en deze gegevens niet ontsleutelen. U onderhouden volledige controle over Hallo sleutels.

### <a name="server-side-encryption"></a>Server-side '-versleuteling

Hallo drie serverzijde versleuteling modellen bieden verschillende Sleutelbeheer kenmerken, die per uw vereisten kunnen worden gekozen.

- **Service beheerd sleutels** voorzien van een combinatie van het besturingselement en het gemak weinig overhead

- **De klant beheerd sleutels** kunt u bepalen Hallo-sleutels, met inbegrip van Hallo mogelijkheid toobring uw eigen sleutels (BYOK) of toogenerate nieuwe.

- **Service beheerd sleutels in ccustomer controlledhardware** kunt u toomanage sleutels in uw eigen opslagplaats die buiten het beheer van Microsoft. Dit wordt Host uw eigen sleutel (HYOK) genoemd. Configuratie is echter complexe, en de meeste Azure services geen ondersteuning voor dit model.

### <a name="azure-disk-encryption"></a>Azure Disk Encryption

Windows- en Linux virtuele machines kunnen worden beveiligd met [Azure Disk Encryption](azure-security-disk-encryption.md), die gebruikmaakt van Hallo [Windows BitLocker](https://technet.microsoft.com/library/cc766295(v=ws.10).aspx) technologie- en Linux [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) tooprotect schijven besturingssysteem en gegevensschijven met volledige versleuteling voor volumes.

Versleutelingssleutels en geheimen worden beveiligd uw [Azure Key Vault](../key-vault/key-vault-whatis.md) abonnement. U kunt back-up en herstel van versleutelde virtuele machines die zijn versleuteld met Hallo KEK configuratie via hello Azure Backup-service.

### <a name="azure-storage-service-encryption"></a>Versleuteling van Azure Storage-service

Gegevens in rust in Azure storage (Blob en -bestand) kunnen in zowel server- en clientzijde scenario's worden versleuteld.

[Azure Storage-Service: versleuteling](../storage/storage-service-encryption.md) (SSE) kunt automatisch gegevens versleutelen voordat deze wordt opgeslagen en automatisch ontsleuteld wanneer u ophaalt, waardoor Hallo volledig transparant gebruikers verwerken. Versleuteling van de opslagruimte gebruikmaakt van 256-bits [AES-versleuteling](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), die is een Hallo sterkste blokcodering beschikbaar en versleuteling, ontsleuteling en Sleutelbeheer op transparante wijze worden verwerkt.

### <a name="client-side-encryption-of-azure-blobs"></a>Versleuteling aan clientzijde van Azure blobs

Versleuteling aan clientzijde van Azure blobs kan op verschillende manieren worden uitgevoerd.

U kunt hello Azure Storage-clientbibliotheek voor .NET-NuGet-pakket tooencrypt gegevens binnen uw client toepassingen voorafgaande toouploading het tooAzure opslag.

meer informatie over toolearn en downloaden hello Azure Storage-clientbibliotheek voor .NET-NuGet-pakket, raadpleegt u Hallo-document met de titel [Windows Azure-opslagservice 8.3.0](https://www.nuget.org/packages/WindowsAzure.Storage)

Wanneer u versleuteling aan clientzijde met Azure Sleutelkluis gebruikt, wordt uw gegevens versleuteld met een eenmalige symmetrische inhoud versleuteling sleutel (CEK) die wordt gegenereerd door hello Azure Storage client SDK. Hallo CEK is versleuteld met behulp van een versleuteling KEK Key Key (), wat een symmetrische sleutel of een asymmetrisch sleutelpaar kan zijn. U kunt lokaal beheren of opslaan in Azure Sleutelkluis. Hallo versleutelde gegevens is vervolgens tooAzure Storage-service geüpload.

meer informatie over client-side '-codering met Azure Sleutelkluis toolearn en aan de slag met het tooinstructions, Zie Hallo-document met de titel [zelfstudie: blobs in Microsoft Azure Storage met Azure Key Vault versleutelen en ontsleutelen](../storage/storage-encrypt-decrypt-blobs-key-vault.md)

Ten slotte kunt u ook hello Azure Storage-clientbibliotheek gebruiken voor Java tooperform clientzijde versleuteling voordat het uploaden van gegevens tooAzure opslag en toodecrypt Hallo gegevens bij het downloaden van toohello client. Deze bibliotheek ondersteunt ook integratie met [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) voor sleutelbeheer storage-account.

### <a name="encryption-of-data-at-rest-with-azure-sql-database"></a>Versleuteling van gegevens in rust met Azure SQL database

[Azure SQL Database](../sql-database/sql-database-technical-overview.md) is een algemene relationele database-service in Microsoft Azure die ondersteuning biedt voor structuren zoals relationele gegevens, JSON ruimtelijke, en XML. Azure SQL ondersteunt zowel versleuteling serverzijde via Hallo Transparent Data Encryption (TDE) functie als versleuteling aan clientzijde via de functie voor Hallo altijd versleuteld.

#### <a name="transparent-data-encryption"></a>Transparent Data Encryption

[TDE transparante gegevensversleuteling](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde) gebruikte tooencrypt is [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016), [Azure SQL Database](../sql-database/sql-database-technical-overview.md), en [Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) gegevensbestanden in realtime met behulp van een databaseversleutelingssleutel (DEK) dat is opgeslagen in Hallo databaserecord opstarten voor beschikbaarheid tijdens het herstel.

TDE beschermt gegevens en logboekbestanden bestanden, met behulp van AES en 3DES versleutelingsalgoritmen. Versleuteling van het databasebestand hello wordt uitgevoerd op paginaniveau Hallo; Hallo-pagina's in een versleutelde database worden versleuteld voordat ze toodisk worden geschreven en wanneer ze zijn gelezen in het geheugen worden ontsleuteld. TDE is nu ingeschakeld standaard op de zojuist gemaakte Azure SQL-databases.

#### <a name="always-encrypted"></a>Altijd versleuteld

Hallo [altijd versleuteld](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine) functie in Azure SQL kunt u tooencrypt gegevens binnen client toepassingen voorafgaande toostoring in Azure SQL Database en kunt u de overdracht van de lokale database beheer toothird tooenable partijen en onderhouden van de scheiding tussen degenen met een eigenaar en Hallo gegevens en degenen die het beheren, maar mag geen toegang tot tooit kunt bekijken.

#### <a name="cellcolumn-level-encryption"></a>Cel/kolom: versleuteling op bestandsniveau

Azure SQL Database kunt u tooapply symmetrische codering tooa kolom van gegevens met behulp van Transact-SQL. Dit heet [cel versleuteling op bestandsniveau of kolom: versleuteling op bestandsniveau](https://docs.microsoft.com/sql/relational-databases/security/encryption/encrypt-a-column-of-data) (wissen), omdat u deze tooencrypt specifieke kolommen of zelfs specifieke cellen van gegevens met verschillende versleutelingssleutels. Hiermee krijgt u meer gedetailleerde mogelijkheid van stationsversleuteling dan TDE waarmee gegevens op pagina's worden gecodeerd.

WISSEN bevat ingebouwde functies waarmee u met behulp van zowel symmetrisch als asymmetrisch sleutels kunt, Hallo openbare sleutel van een certificaat of met een wachtwoordzin met 3DES tooencrypt-gegevens.

### <a name="cosmos-db-database-encryption"></a>Versleuteling van de cosmos DB-database

[Azure Cosmos DB](../cosmos-db/database-encryption-at-rest.md) database is globaal gedistribueerd en modellen van Microsoft. Gegevens van de gebruiker opgeslagen in Cosmos DB in niet-vluchtige opslag (solid-state-schijven) is versleuteld standaard; Er zijn geen tooturn besturingselementen het in- of uitschakelen. Codering in rust wordt geïmplementeerd met behulp van een aantal beveiligingstechnologieën, met inbegrip van beveiligde sleutel opslagsystemen, gecodeerde netwerken en cryptografische API's. Coderingssleutels worden beheerd door Microsoft en worden gedraaid per interne richtlijnen van Microsoft.

### <a name="at-rest-encryption-in-azure-data-lake"></a>Codering in rust in Azure Data Lake

[Azure Data Lake](../data-lake-store/data-lake-store-encryption.md) is een ondernemingsbrede opslagplaats van elk type gegevens verzameld in een formele definitie van één plaats eerdere tooany van vereisten of het schema. Biedt ondersteuning voor Azure Data Lake Store ' op standaard ' transparante versleuteling van gegevens in rust, die is ingesteld tijdens het maken van Hallo van uw account. Standaard, beheert Data Lake Store Hallo sleutels voor u, maar u hebt Hallo optie toomanage ze zelf.

Drie typen sleutels worden gebruikt in het versleutelen en ontsleutelen van gegevens: Hallo Master versleuteling sleutel (MEK), Gegevensversleutelingsleutel (DEK) en blok versleuteling sleutel (BEK). Hallo MEK gebruikte tooencrypt Hallo DEK, die is opgeslagen op permanente media, en Hallo BEK is afgeleid van Hallo DEK en Hallo gegevensblok. Als u uw eigen sleutels beheert, kunt u Hallo MEK draaien.

## <a name="encryption-of-data-in-transit"></a>Versleuteling van gegevens die onderweg

Azure biedt veel mechanismen voor het bewaren van gegevens persoonlijke vanaf één locatie tooanother beweegt.

### <a name="tlsssl-encryption-in-azure"></a>TLS/SSL-versleuteling in Azure

Microsoft gebruikt Hallo [Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) protocol tooprotect gegevens als deze wordt onderweg tussen het Hallo-cloudservices en -klanten. Datacenters van Microsoft te onderhandelen over de TLS-verbinding met clientsystemen die verbinding maken met tooAzure services. TLS bevat sterke verificatie, privacy van berichten en integriteit (waardoor de detectie van bericht knoeien, onderschept en kunnen worden vervalst), interoperabiliteit, algoritmeflexibiliteit, gebruiksgemak en gebruik.

[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) is de verbindingen tussen clientsystemen klanten en Microsoft cloudservices worden beschermd door unieke sleutels. Verbindingen ook sleutellengten op basis van RSA 2048-bits codering gebruiken. Deze combinatie maakt het moeilijker voor iemand toointercept en toegang tot gegevens die in de doorvoer.

### <a name="azure-storage-transactions"></a>Azure Storage-transacties

Wanneer u met Azure Storage via hello Azure-portal werken, hebben alle transacties plaatsvinden via HTTPS. U kunt ook Hallo REST API voor Storage via HTTPS toointeract gebruiken met Azure Storage. Bij het aanroepen van Hallo REST-API's tooaccess objecten in opslagaccounts doordat veilige overdracht vereist voor Hallo storage-account, kunt u gebruik van HTTPS Hallo afdwingen.

Shared Access Signatures ([SAS](../storage/storage-dotnet-shared-access-signature-part-1.md)), wat kan gebruikte toodelegate zijn tooAzure opslagobjecten krijgen, bevatten een optie toospecify die alleen Hallo HTTPS-protocol kan worden gebruikt bij het gebruik van handtekeningen voor gedeelde toegang. Dit zorgt ervoor dat iedereen koppelingen met SAS-tokens verstuurt het juiste protocol Hallo gebruikt.

[SMB 3.0](https://technet.microsoft.com/library/dn551363(v=ws.11).aspx#BKMK_SMBEncryption) versleuteling gebruikt tooaccess Azure-bestandsshares ondersteunt en is beschikbaar in Windows Server 2012 R2, Windows 8, Windows 8.1 en Windows 10, regio-overschrijdende toegang, en zelfs op Hallo bureaublad openen.

Versleuteling aan clientzijde versleutelt Hallo gegevens voordat deze heeft verzonden tooAzure opslag, zodat ze zijn versleuteld als ze via Hallo-netwerk.

### <a name="smb-encryption-over-azure-virtual-networks"></a>SMB-versleuteling via virtuele netwerken in Azure 

[SMB 3.0](https://support.microsoft.com/help/2709568/new-smb-3-0-features-in-the-windows-server-2012-file-server) in Azure VM's met Windows Server 2012 en hoger kunt u de mogelijkheid toomake gegevens overdrachten beveiligen door het versleutelen van gegevens tijdens de overdracht via Azure Virtual Networks Hallo tooprotect tegen knoeien en afgeluisterd aanvallen. Beheerders kunnen SMB-versleuteling inschakelen voor de hele server Hallo of alleen bepaalde shares.

Standaard zodra SMB-versleuteling is ingeschakeld voor een share of een zijn SMB-3-clients toegestaan tooaccess Hallo versleuteld shares.

## <a name="in-transit-encryption-in-azure-virtual-machines"></a>Codering in Azure virtuele Machines in transit

Gegevens die onderweg naar, van, en tussen Azure VM's waarop Windows wordt uitgevoerd is versleuteld in een aantal verschillende manieren, afhankelijk van de aard Hallo van Hallo-verbinding.

### <a name="rdp-sessions"></a>RDP-sessies

U kunt verbinding maken en logboekbestanden op tooan Azure VM die gebruikmaakt van Hallo [Remote Desktop Protocol](https://msdn.microsoft.com/library/aa383015(v=vs.85).aspx) (RDP) vanuit een Windows-clientcomputer of vanuit een Mac met een RDP-client is geïnstalleerd. Gegevens die onderweg via Hallo-netwerk in het RDP-sessies kunnen worden beveiligd door TLS.

U kunt Extern bureaublad tooconnect tooa Linux VM ook gebruiken in Azure.

### <a name="secure-access-toolinux-vms-with-ssh"></a>Toegang tot virtuele machines tooLinux met SSH beveiligde

U kunt [Secure Shell](../virtual-machines/linux/ssh-from-windows.md) (SSH) tooconnect tooLinux virtuele machines in Azure wordt uitgevoerd voor extern beheer. SSH is een versleutelde verbindingsprotocol waarmee beveiligde aanmeldingen via niet-beveiligde verbindingen. Is het Hallo standaardverbindingsprotocol voor virtuele Linux-machines gehost in Azure. Met behulp van SSH-sleutels voor verificatie, moet u Hallo nodig voor wachtwoorden toolog in elimineren. SSH maakt gebruik van een openbaar/persoonlijk sleutelpaar (asymmetrische versleuteling) voor verificatie.

## <a name="azure-vpn-encryption"></a>Azure VPN-versleuteling

U kunt tooAzure verbinden via een virtueel particulier netwerk dat wordt gemaakt van een beveiligde tunnel tooprotect Hallo privacy van gegevens van Hallo via Hallo-netwerk worden verzonden.

### <a name="azure-vpn-gateway"></a>Azure VPN Gateway

[Azure VPN-gateway](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md) gebruikte toosend versleuteld verkeer tussen het virtuele netwerk en uw on-premises locatie via een openbare verbinding of toosend verkeer tussen virtuele netwerken.

Site-naar-site VPN maakt gebruik van [IPsec](https://en.wikipedia.org/wiki/IPsec) voor transport-versleuteling. Azure VPN-gateways gebruiken een reeks standaard voorstellen. U kunt Azure VPN-gateways toouse een aangepaste IPsec/IKE-beleid configureren met specifieke cryptografische algoritmen en de belangrijkste sterkte, plaats hello Azure standaard beleid sets.

### <a name="point-to-site-vpn"></a>Punt-naar-site VPN

Punt-naar-Site VPN-verbindingen kunnen afzonderlijke clientcomputers toegang krijgen tot tooan Azure Virtual Network. [Hallo Secure Socket Tunneling Protocol](https://technet.microsoft.com/library/2007.06.cableguy.aspx) (SSTP) is gebruikt toocreate Hallo VPN-tunnel en firewalls (Hallo tunnel wordt weergegeven als een HTTPS-verbinding) kunnen passeren. Voor punt-naar-site-verbindingen kunt u uw eigen interne PKI basis-CA.

U kunt een punt-naar-site VPN-verbinding tooa virtueel netwerk met hello Azure-portal en zonder certificaatverificatie PowerShell configureren.

toolearn meer informatie over punt-naar-site VPN-verbindingen tooAzure VNets, Zie: [een punt-naar-Site-verbinding tooa VNet configureren met behulp van certificaatverificatie: Azure-portal](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md) en

[Een punt-naar-Site-verbinding tooa VNet configureren met behulp van verificatie via certificaat: PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="site-to-site-vpn"></a>Site-naar-site VPN 

Een Site-naar-Site VPN-gatewayverbinding gebruikte tooconnect is uw on-premises netwerk tooan virtuele Azure-netwerk via een VPN-IPsec/IKE (IKEv1 of IKEv2)-tunnel. Dit type verbinding vereist een VPN-zich on-premises apparaten met een extern gericht openbaar IP-adres toegewezen tooit.

U kunt een site-naar-site VPN-verbinding tooa virtueel netwerk met hello Azure-portal, PowerShell of hello Azure-opdrachtregelinterface (CLI) configureren.

Lees deze voor meer informatie:

[Een Site-naar-Site-verbinding maken in hello Azure-portal](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

[Maak een Site-naar-Site-verbinding](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

[Een virtueel netwerk maken met een site-naar-site VPN-verbinding met CLI](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="in-transit-encryption-in-azure-data-lake"></a>Codering in Azure Data Lake in transit

Gegevens tijdens overdracht (ook wel gegevens in beweging genoemd) worden ook altijd versleuteld in Data Lake Store. Bovendien tooencrypting gegevens voorafgaande toostoring toopersistent media Hallo gegevens is ook altijd onderweg via HTTPS beveiligd. HTTPS is alleen Hallo-protocol dat wordt ondersteund voor Hallo die Data Lake Store REST-interfaces.

toolearn meer informatie over het coderen van gegevens tijdens de overdracht in Azure Data Lake Zie Hallo-document met de titel [versleuteling van gegevens in Azure Data Lake Store.](../data-lake-store/data-lake-store-encryption.md)

## <a name="key-management-with-azure-key-vault"></a>Sleutelbeheer met Azure Sleutelkluis

Zonder de juiste beveiliging en beheer van sleutels hello, wordt versleuteling onbruikbaar gerenderd. Azure Sleutelkluis is de aanbevolen oplossing van Microsoft voor het beheren en beheren van toegang tooencryption sleutels die door cloudservices worden gebruikt. Machtigingen tooaccess sleutels kunnen worden toegewezen tooservices of toousers via Azure Active Directory-accounts.

Azure Sleutelkluis hoge organisaties van Hallo nodig tooconfigure, patch en onderhouden van Hardware Security Modules (HSM's) en sleutelbeheer software. Met Azure Key Vault Microsoft uw sleutels nooit ziet en toepassingen hebt u niet direct toegang toothem; u onderhouden besturingselement. U kunt ook importeren of genereren van sleutels in HSM's.

## <a name="next-steps"></a>Volgende stappen

- [Overzicht van Azure-beveiliging](security-get-started-overview.md)
- [Overzicht van Azure-netwerk-beveiliging](security-network-overview.md)
- [Overzicht van Azure-database-beveiliging](azure-database-security-overview.md)
- [Overzicht van virtuele machines in Azure-beveiliging](security-virtual-machines-overview.md)
- [Versleuteling van inactieve gegevens](azure-security-encryption-atrest.md)
- [Aanbevolen procedures voor gegevensbeveiliging en -versleuteling](azure-security-data-encryption-best-practices.md)
