---
title: aaaData beveiligings- en aanbevolen procedures voor versleuteling | Microsoft Docs
description: In dit artikel biedt een set met aanbevolen procedures voor beveiliging van gegevens en ingebouwde mogelijkheden van Azure met behulp van versleuteling.
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 17ba67ad-e5cd-4a8f-b435-5218df753ca4
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: yurid
ms.openlocfilehash: 5057c85ed3107921462a40045e716675ea41e4bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-security-and-encryption-best-practices"></a>Best Practices voor beveiliging van gegevens van Azure en versleuteling
Een van de Hallo sleutels toodata beveiliging in de cloud Hallo is accounting voor Hallo mogelijke statussen in die uw gegevens zich kunnen voordoen, en welke besturingselementen beschikbaar zijn voor die status. Voor doel van Azure data encryption best practices voor beveiliging en Hallo zijn Hallo aanbevelingen rond Hallo statussen van gegevens te volgen:

* In rust: Dit omvat alle informatie opslagobjecten, containers en typen die statisch bestaan op de fysieke media, worden deze magnetische of optische schijf.
* In Transit: Wanneer gegevens worden overgebracht tussen onderdelen, locaties of programma's, zoals via Hallo-netwerk via een servicebus (van lokale toocloud en vice versa, inclusief hybride verbindingen zoals ExpressRoute) of tijdens een i/o proces, dit wordt beschouwd als wordt in beweging.

In dit artikel wordt een verzameling van Azure data encryption best practices voor beveiliging en besproken. Deze aanbevolen procedures zijn afgeleid van onze ervaring met beveiliging van gegevens van Azure en versleuteling en Hallo ervaringen van klanten zoals zelf.

Voor elke aanbevolen procedure wordt uitgelegd:

* Welke beste Hallo
* Waarom u wilt dat tooenable die best practices
* Wat zijn Hallo resultaat als u niet tooenable Hallo aanbevolen
* Mogelijke alternatieven toohello best practices
* Hoe meer u tooenable Hallo best practices

In dit artikel Azure-gegevensbeveiliging en Best Practices voor versleuteling is gebaseerd op een advies consensus en mogelijkheden van Azure-platform en functiesets, als deze bestaan in Hallo tijd die in dit artikel is geschreven. Adviezen en technologieën op den duur veranderen en dit artikel worden de wijzigingen op een tooreflect regelmatig wordt bijgewerkt.

Azure data beveiligings- en aanbevolen procedures in dit artikel wordt beschreven, zijn onder andere:

* Multi-factor authentication afdwingen
* Gebruik rollen gebaseerd toegangsbeheer (RBAC)
* Virtuele machines van Azure versleutelen
* Hardware security modellen gebruiken
* Met beveiligde werkstations beheren
* SQL-gegevensversleuteling inschakelt
* De gegevens onderweg te beschermen
* Bestand niveau gegevensversleuteling afdwingen

## <a name="enforce-multi-factor-authentication"></a>Multi-factor Authentication afdwingen
Hallo eerste stap bij het toegang tot gegevens en beheer in Microsoft Azure is tooauthenticate Hallo gebruiker. [Azure multi-factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md) is een methode voor het verifiëren van de identiteit van gebruiker met een andere methode dan alleen een gebruikersnaam en wachtwoord. Deze verificatiemethode helpt beveiliging toegang toodata en toepassingen en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden.

Als u Azure MFA inschakelt voor uw gebruikers, voegt u een tweede beveiligingslaag beveiliging toouser aanmeldingen en transacties. In dit geval een transactie kan toegang krijgen tot een document dat zich in een bestandsserver of op uw SharePoint Online. Azure MFA helpt ook bij IT tooreduce Hallo kans op een verdachte referenties heeft toegang tot tooorganization van gegevens.

Bijvoorbeeld: als u Azure MFA voor uw gebruikers afdwingen en configureert u toouse een telefoongesprek of SMS-bericht naar deze verificatie bij een aanval op Hallo gebruikersreferenties, niet het Hallo aanvaller geval kunnen tooaccess worden alle bronnen omdat hij geen toegang tot toouser van telefoon. Organisaties die deze extra beschermingslaag identiteit niet toevoegt, zijn vatbaar voor referentie diefstal aanval, wat toodata inbreuk leiden kan.

Een alternatief voor organisaties die tookeep Hallo verificatiemethoden willen lokale is toouse [Azure multi-factor Authentication-Server](../multi-factor-authentication/multi-factor-authentication-get-started-server.md), ook wel MFA lokale. Met deze methode wordt u nog steeds kunnen tooenforce multi-factor authentication-server, terwijl de Hallo MFA server on-premises, zijn.

Lees voor meer informatie over Azure MFA Hallo artikel [aan de slag met Azure multi-factor Authentication in de cloud Hallo](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

## <a name="use-role-based-access-control-rbac"></a>Gebruik rollen gebaseerd toegangsbeheer (RBAC)
Beperken van toegang op basis van Hallo [moet tooknow](https://en.wikipedia.org/wiki/Need_to_know) en [minimale bevoegdheden](https://en.wikipedia.org/wiki/Principle_of_least_privilege) beveiligingsprincipes. Dit is noodzakelijk voor organisaties die tooenforce beveiligingsbeleid voor toegang tot gegevens willen. Azure op rollen gebaseerde toegangsbeheer (RBAC) kan worden gebruikt tooassign machtigingen toousers, groepen en toepassingen op een bepaalde scope. Hallo-bereik van een roltoewijzing kan dit een abonnement, een resourcegroep of één resource.

U kunt gebruikmaken van [ingebouwde RBAC-rollen](../active-directory/role-based-access-built-in-roles.md) in Azure tooassign toousers bevoegdheden. Overweeg het gebruik van *Storage Account Inzender* voor cloudoperators die toomanage storage-accounts nodig en *klassieke Storage Account Inzender* rol toomanage klassieke opslagaccounts. Voor cloudoperators die behoeften toomanage VM's en storage-account, kunt u deze toe te voegen te*Virtual Machine Contributor* rol.

Organisaties die niet afgedwongen door toegangsbeheer gegevens dankzij het gebruik van mogelijkheden, zoals RBAC mogelijk meer bevoegdheden beschikt dan nodig is voor hun gebruikers geven. Dit kan ertoe leiden toodata inbreuk door sommige gebruikers hebben toegang toodata die de eerste plaats Hallo mag niet nodig hebben.

U kunt meer informatie over Azure RBAC Hallo artikel lezen [rollen gebaseerd toegangsbeheer](../active-directory/role-based-access-control-configure.md).

## <a name="encrypt-azure-virtual-machines"></a>Virtuele Machines van Azure versleutelen
Voor veel organisaties [gegevensversleuteling in rust](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) is een verplichte stap naar privacy, naleving en gegevens onafhankelijkheid van gegevens. Azure Disk Encryption kunnen IT-beheerders tooencrypt Windows en Linux IaaS virtuele Machine (VM)-schijven. Azure Disk Encryption maakt gebruik van Hallo bedrijfstak standaard BitLocker-functie van Windows hello DM-Crypt functie en van Linux tooprovide volumeversleuteling voor Hallo OS en Hallo gegevensschijven.

U kunt gebruikmaken van Azure Disk Encryption toohelp beveiligen en uw toomeet gegevens beveiligt uw organisatorische vereisten voor beveiliging en naleving. Organisaties moeten ook rekening houden met behulp van versleuteling toohelp beperken van toegang tot de gegevens van de risico's gerelateerde toounauthorized. Het is ook raadzaam toothem van stations voorafgaande toowriting gevoelige gegevens te coderen.

Zorg ervoor tooencrypt gegevensvolumes van de VM en opstartvolume in volgorde tooprotect gegevens in rust in uw Azure storage-account. Hallo-sleutels en geheimen beveiligen door gebruik te [Azure Key Vault](../key-vault/key-vault-whatis.md).

Houd rekening met Hallo na versleuteling aanbevolen procedures voor de lokale Windows-Servers:

* Gebruik [BitLocker](https://technet.microsoft.com/library/dn306081.aspx) voor gegevensversleuteling
* Sla de herstelgegevens in AD DS.
* Als er een probleem dat BitLocker-sleutels zijn aangetast, wordt u aangeraden ofwel Hallo station tooremove alle instanties van Hallo BitLocker metagegevens uit het Hallo-station of dat u ontsleutelen en opnieuw versleutelen van het hele station hello te formatteren.

Organisaties die niet gegevensversleuteling afdwingen zijn geneigd toobe blootgesteld toodata problemen met de gegevensintegriteit, zoals schadelijke of rogue gebruikers gegevens stelen, en accounts krijgen van toegang door onbevoegden toodata wissen indeling waarmee is geknoeid. Naast deze risico's, moeten bedrijven die toocomply met regelgeving vanuit de sector, hebben ze zijn toegewijd en Hallo juiste besturingselementen tooenhance gegevensbeveiliging gebruikt bewijzen.

U kunt meer informatie over Azure Disk Encryption Hallo artikel lezen [Azure Disk Encryption for Windows en Linux IaaS VM's](azure-security-disk-encryption.md).

## <a name="use-hardware-security-modules"></a>Gebruik van Hardware Security Modules
Codering-oplossingen geheime codes tooencrypt gegevens gebruikt. Het is daarom essentieel dat deze sleutels veilig worden opgeslagen. Sleutelbeheer wordt een integraal onderdeel van gegevensbeveiliging, omdat deze over toostore geheime codes die gebruikte tooencrypt gegevens zijn.

Maakt gebruik van Azure schijfversleuteling [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) toohelp u beheren en een schijf-sleutels en geheimen in uw abonnement sleutelkluis terwijl u ervoor zorgt dat alle gegevens in de schijven van de virtuele machine Hallo zijn versleuteld in rust in uw Azure beheren opslag. U moet Azure Key Vault tooaudit sleutels en gebruik van beleidsregels.

Er zijn veel risico's gerelateerde toonot met geschikte beveiligingscontroles voorhanden in place tooprotect Hallo geheime codes die gebruikte tooencrypt waren uw gegevens. Als aanvallers toegang hebben toohello geheime codes, ze kunnen toodecrypt Hallo gegevens worden en mogelijk hebben toegang tot tooconfidential informatie.

U meer informatie over algemene aanbevelingen voor certificaatbeheer in Azure door te lezen Hallo artikel [Certificate Management in Azure: tips](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/).

Lees voor meer informatie over Azure Sleutelkluis [aan de slag met Azure Key Vault](../key-vault/key-vault-get-started.md).

## <a name="manage-with-secure-workstations"></a>Met beveiligde werkstations beheren
Sinds Hallo overgrote deel van de eindgebruiker van Hallo aanvallen doel hello wordt Hallo-eindpunt een van de primaire punten Hallo van een aanval. Als een aanvaller wordt aangetast Hallo eindpunt, kan hij gebruikmaken van Hallo van de gebruiker referenties toogain toegang tooorganization van gegevens. De meeste endpoint-aanvallen zijn tootake kunnen profiteren van Hallo feit dat eindgebruikers beheerders in hun lokale werkstations zijn.

U kunt deze risico's verminderen met behulp van een beveiligd beheerwerkstation. Het is raadzaam dat u een [Privileged Access Workstations (PAW)](https://technet.microsoft.com/library/mt634654.aspx) tooreduce Hallo kwetsbaarheid in werkstations. Deze beveiligde beheerwerkstations kunnen helpen u bij het beperken van enkele van deze aanvallen zodat uw gegevens is veiliger. Zorg ervoor dat toouse PAW tooharden en vergrendelen omlaag uw werkstation. Dit is een belangrijke stap tooprovide hoge beveiliging garantie voor gevoelige accounts, taken en gegevensbeveiliging.

Gebrek van endpoint protection mogelijk risico voor uw gegevens, zorg ervoor dat tooenforce beveiligingsbeleid op alle apparaten die gebruikt tooconsume gegevens, ongeacht de locatie van gegevens voor hello (cloud of on-premises zijn).

U kunt meer informatie over de juiste rechten toegang krijgen tot werkstation Hallo artikel lezen [bevoegde toegang beveiligen](https://technet.microsoft.com/library/mt631194.aspx).

## <a name="enable-sql-data-encryption"></a>SQL-gegevensversleuteling inschakelt
[Azure SQL Database transparante gegevensversleuteling](https://msdn.microsoft.com/library/dn948096.aspx) (TDE) beschermt tegen Hallo dreiging van schadelijke activiteiten door te voeren realtime versleuteling en ontsleuteling van Hallo-database, gekoppelde back-ups en transactielogbestanden in rust zonder wijzigingen toohello toepassing vereisen.  TDE versleutelt Hallo opslag van een volledige database met behulp van een symmetrische sleutel opgeroepen Hallo databaseversleutelingssleutel.

Zelfs wanneer Hallo volledige opslag wordt gecodeerd, is het belangrijk tooalso versleutelen van uw database zelf. Dit is een implementatie van Hallo ingrijpende diepte benadering voor gegevensbescherming. Als u [Azure SQL Database](https://msdn.microsoft.com/library/0bf7e8ff-1416-4923-9c4c-49341e208c62.aspx) en tooprotect gevoelige gegevens zoals creditcard of burgerservicenummers, kunt u databases met FIPS 140-2-gevalideerde 256 bits AES-versleuteling dat voldoet aan de vereisten van een groot aantal Hallo versleutelen industrienormen (bijv, HIPAA, PCI).

Het is belangrijk toounderstand die bestanden gerelateerd te[uitbreiding van de buffer](https://msdn.microsoft.com/library/dn133176.aspx) (BPE) worden niet versleuteld wanneer een database worden versleuteld met TDE. Moet u versleuteling op bestandsniveau hulpprogramma's zoals BitLocker of Hallo [Encrypting File System](https://technet.microsoft.com/library/cc700811.aspx) (EFS) voor de BPE gerelateerde bestanden.

Omdat een geautoriseerde gebruiker zoals een beveiligingsbeheerder of een databasebeheerder toegankelijk Hallo gegevens zelfs als het Hallo-database is versleuteld met TDE, moet u ook volgen Hallo aanbevelingen hieronder:

* SQL-verificatie op databaseniveau Hallo
* Azure AD-verificatie met behulp van RBAC-rollen
* Gebruikers en toepassingen moeten afzonderlijke accounts tooauthenticate gebruiken. Deze manier kunt u Hallo machtigingen toousers en toepassingen beperken en Hallo risico's van schadelijke activiteiten te verminderen
* Beveiliging van de database op gebruikersniveau implementeren met behulp van de vaste databaserollen (zoals db_datareader of db_datawriter), of u kunt aangepaste rollen maken voor uw toepassing toogrant expliciete machtigingen tooselected databaseobjecten

Organisaties die geen gebruik van niveau versleuteling van de database maakt mogelijk gevoeliger voor aanvallen kunnen leiden die gegevens in SQL-databases.

U meer informatie over SQL TDE versleuteling door te lezen Hallo artikel [Transparent Data Encryption met Azure SQL Database](https://msdn.microsoft.com/library/0bf7e8ff-1416-4923-9c4c-49341e208c62.aspx).

## <a name="protect-data-in-transit"></a>De gegevens onderweg te beschermen
Beveiligen van gegevens die onderweg moet essentieel onderdeel van uw strategie voor gegevensbescherming. Omdat de gegevens wordt heen en weer worden verplaatst vanaf verschillende locaties, is algemeen aanbeveling Hallo SSL/TLS-protocollen tooexchange gegevens altijd te gebruiken op verschillende locaties. In sommige gevallen kunt u tooisolate Hallo gehele communicatiekanaal tussen uw on-premises en cloud infrastructuur met behulp van een virtueel particulier netwerk (VPN).

Gegevens verplaatsen tussen uw on-premises infrastructuur en Azure, moet u passende beveiligingsmaatregelen zoals HTTPS- of VPN.

Gebruik voor organisaties die toegang vanuit meerdere werkstations zich lokaal tooAzure toosecure nodig, [Azure site-naar-site VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md).

Voor organisaties die toosecure toegang vanaf één werkstation moeten zich op de lokale tooAzure, gebruik [punt-naar-Site VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md).

Grotere gegevenssets kan worden verplaatst via een speciale snelle WAN-verbinding, zoals [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Als u ervoor toouse ExpressRoute kiest, kunt u ook gegevens op het niveau van de toepassing met behulp van Hallo Hallo coderen [SSL/TLS](https://support.microsoft.com/kb/257591) of andere protocollen voor extra beveiliging.

Als u met Azure Storage via hello Azure Portal communiceert, worden alle transacties plaatsvinden via HTTPS. [REST API voor Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx) via HTTPS kan ook worden gebruikt toointeract met [Azure Storage](https://azure.microsoft.com/services/storage/) en [Azure SQL Database](https://azure.microsoft.com/services/sql-database/).

Organisaties die niet voldoen aan tooprotect gegevens die onderweg zijn vatbaar voor [man-in-the-middle-aanvallen](https://technet.microsoft.com/library/gg195821.aspx), [afgeluisterd](https://technet.microsoft.com/library/gg195641.aspx) en sessiehijacking. Deze aanvallen kunnen Hallo eerste stap bij het krijgen van toegang tot tooconfidential gegevens zijn.

U kunt meer informatie over Azure VPN-optie Hallo artikel lezen [Planning en ontwerp voor VPN-Gateway](../vpn-gateway/vpn-gateway-plan-design.md).

## <a name="enforce-file-level-data-encryption"></a>Bestand niveau gegevensversleuteling afdwingen
Een andere beschermingslaag die Hallo beveiligingsniveau voor uw gegevens kunt verhogen ontsleutelt Hallo-bestand zelf, ongeacht de locatie van Hallo-bestand.

[Azure RMS](https://technet.microsoft.com/library/jj585026.aspx) maakt gebruik van versleuteling, identiteit en verificatie beleid toohelp beveiligen van uw bestanden en e-mail. Azure RMS werkt op meerdere apparaten, telefoons, tablets en pc's voor beveiliging binnen uw organisatie en buiten uw organisatie. Deze mogelijkheid is mogelijk omdat Azure RMS wordt toegevoegd een beveiligingsniveau dat met Hallo gegevens, resteert zelfs wanneer deze de fysieke grenzen van uw organisatie.

Wanneer u uw bestanden tooprotect Azure RMS gebruikt, gebruikt u industriestandaard cryptografie met volledige ondersteuning van [FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/standards.html). Wanneer u Azure RMS-gegevensbeveiliging gebruikmaken, hebt u zelfs als deze gekopieerde toostorage die niet onder het beheer van Hallo Hallo zekerheid dat Hallo beveiliging blijft van toepassing op Hallo-bestand, IT, zoals een cloudopslagservice. Hallo dezelfde vindt plaats voor bestanden die worden gedeeld via e-mail, Hallo-bestand is beveiligd als een bijlage tooan e-mailbericht met instructies hoe tooopen Hallo beveiligde bijlage.

Bij het plannen van de overstap op Azure RMS wordt aangeraden Hallo volgende:

* Hallo installeren [app RMS sharing](https://technet.microsoft.com/library/dn339006.aspx). Deze app kan worden geïntegreerd met Office-toepassingen door installatie van een Office-invoegtoepassing zodat gebruikers kunnen bestanden eenvoudig rechtstreeks beveiligen.
* Configureer toepassingen en services toosupport Azure RMS
* Maak [aangepaste sjablonen](https://technet.microsoft.com/library/dn642472.aspx) die overeenstemming met uw zakelijke vereisten. Bijvoorbeeld: een sjabloon voor bovenste geheime gegevens die moet worden toegepast op alle bovenste geheim gerelateerde e-mailberichten.

Organisaties die zich op zwakke [gegevensclassificatie](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) en bestandsbeveiliging mogelijk vatbaarder toodata lekken. Zonder de juiste Bestandsbeveiliging, geen organisaties kunnen tooobtain worden zakelijke inzichten, controleren op misbruik en te voorkomen dat schadelijke toegang toofiles.

U kunt meer informatie over Azure RMS Hallo artikel lezen [aan de slag met Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx).
