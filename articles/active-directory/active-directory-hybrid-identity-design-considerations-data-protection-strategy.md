---
title: "ontwerpoverwegingen voor aaaAzure Active Directory hybride identiteit - strategie voor gegevensbescherming definiëren | Microsoft Docs"
description: Strategie voor gegevensbescherming Hallo definieert u voor hybride identiteit toomeet Hallo zakelijke vereisten van uw oplossing die u hebt gedefinieerd.
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e76fd1f4-340a-492a-84d9-e05f3b7cc396
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 8fd7ab364a09de3b60293a4a1cbb6e0fa4a3295d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="define-data-protection-strategy-for-your-hybrid-identity-solution"></a>Definieer de strategie voor gegevensbescherming voor uw oplossing voor hybride identiteit
In deze taak definieert u de strategie voor gegevensbescherming Hallo voor hybride identiteit toomeet Hallo zakelijke vereisten van uw oplossing die u hebt gedefinieerd in:

* [Bepalen van de beveiligingsvereisten voor gegevens](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)
* [Vereisten voor inhoudsbeheer bepalen](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)
* [Vereisten voor toegangsbeheer bepalen](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)
* [Vereisten voor respons op incidenten bepalen](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="define-data-protection-options"></a>Definieer de opties voor beveiliging
Zoals wordt uitgelegd [directory-synchronisatievereisten bepalen](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md), Microsoft Azure AD kan worden gesynchroniseerd met uw Active Directory Domain Services (AD DS) die zich op lokaal bevinden. Dankzij deze integratie kunnen organisaties tooleverage Azure AD tooverify gebruikersreferenties wanneer ze tooaccess bedrijfsbronnen probeert. Dit kan worden gedaan voor beide scenario's: gegevens in rust lokale en bij Hallo cloud.  Toodata in Azure AD Access vereist verificatie van de gebruiker via een beveiligingstokenservice (STS).

Zodra geverifieerd, Hallo UPN (user Principal name) wordt gelezen uit het Hallo-verificatietoken en Hallo gerepliceerd partitie en de bijbehorende van container wordt toohello gebruikersdomein bepaald. Informatie over de bestaan, de ingeschakelde status en de rol van Hallo gebruiker wordt gebruikt door Hallo autorisatie system toodetermine of Hallo aangevraagde toegang toohello doel tenant voor deze gebruiker is gemachtigd in deze sessie. Bepaalde geautoriseerde acties (gebruiker, het wachtwoord opnieuw instellen wordt in het bijzonder maken) maken van een audittrail die kan worden gebruikt door een tenant administrator toomanage naleving inspanningen of onderzoeken.

Zwevend gegevens uit uw on-premises datacentrum in Azure Storage via een internetverbinding altijd mogelijk niet mogelijk vanwege toodata volume, beschikbare bandbreedte of andere overwegingen. Hallo [Azure Storage Import/Export-Service](../storage/common/storage-import-export-service.md) biedt een optie op basis van hardware voor plaatsen/ophalen van grote hoeveelheden gegevens in blob storage. Hiermee kunt u toosend [BitLocker-versleuteling](https://technet.microsoft.com/library/dn306081#BKMK_BL2012R2) harde schijven rechtstreeks tooan Azure-datacenter waar cloudoperators Hallo inhoud tooyour storage-account wordt geüpload, of ze kunnen uw Azure data tooyour downloaden tooreturn stations tooyou. Alleen versleutelde schijven worden voor dit proces (met een BitLocker-sleutel die is gegenereerd door Hallo-service zelf tijdens de installatie van de taak Hallo) geaccepteerd. Hallo BitLocker-sleutel wordt aangeleverd tooAzure afzonderlijk, zodat de buiten-band sleutel delen.

Omdat gegevens die onderweg kunnen worden uitgevoerd in verschillende scenario's, is ook relevant tooknow die gebruikmaakt van Microsoft Azure [virtuele netwerken](https://azure.microsoft.com/documentation/services/virtual-network/) tooisolate tenants verkeer van elkaar, zoals host - en gastniveau maatregelen nemen firewalls, pakketfilters IP-poorten blokkeren en HTTPS-eindpunten. De meeste interne communicatie van Azure, inclusief infrastructuur-infrastructuur- en infrastructuur klant (lokaal), zijn echter ook versleuteld. Een ander belangrijk scenario is Hallo communicatie binnen de Azure-datacenters; Microsoft beheert tooassure met netwerken die geen virtuele machine kan worden geïmiteerd of afluisteren op Hallo IP-adres van een andere. TLS/SSL wordt gebruikt bij het openen van Azure Storage of de SQL-Databases, of wanneer u verbinding maakt tooCloud Services. In dit geval is Hallo klant beheerder verantwoordelijk voor het verkrijgen van een TLS/SSL-certificaat en de implementatie daarvan tootheir tenant-infrastructuur. Gegevensverkeer verplaatsen tussen virtuele Machines in dezelfde implementatie Hallo of tussen de tenants in een enkele implementatie via Microsoft Azure Virtual Network via gecodeerde communicatieprotocollen zoals HTTPS, SSL/TLS of anderen kunnen worden beveiligd.

Afhankelijk van hoe u de vragen in Hallo beantwoord [gegevensbeveiligingsvereisten bepalen](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md), moet u kunnen toodetermine hoe u wilt dat tooprotect gegevens en hoe Hallo hybride identiteitsoplossing u op dat helpt. Hallo tabel toont ondersteund door Azure Hallo-opties die beschikbaar voor elk scenario van data protection zijn.

| Opties voor beveiliging van gegevens | In rust in Hallo | Op de rest lokale | Onderweg |
| --- | --- | --- | --- |
| BitLocker-stationsversleuteling |X |X | |
| SQL Server-databases voor tooencrypt |X |X | |
| VM-VM-versleuteling | | |X |
| SSL/TLS | | |X |
| VPN | | |X |

> [!NOTE]
> Lees [naleving door functie](https://azure.microsoft.com/support/trust-center/services/) op [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/) tooknow meer over Hallo certificeringen die voldoet aan elke Azure-service.
> Omdat Hallo opties voor bescherming van een gelaagde benadering, vergelijking tussen deze opties zijn niet geldig voor deze taak. Zorg ervoor dat u gebruik van alle opties die beschikbaar zijn voor elke status die Hallo-gegevens.
>
>

## <a name="define-content-management-options"></a>Definieer de opties voor inhoudbeheer
Een voordeel van het gebruik van Azure AD-toomanage een infrastructuur voor hybride identiteit is dat Hallo-proces volledig transparant vanuit Hallo van de eindgebruiker perspectief is. Hallo gebruiker probeert een gedeelde bron tooaccess, Hallo resource vereist verificatie, Hallo gebruiker toosend een verificatie aanvraag tooAzure AD in volgorde tooobtain Hallo token en toegang tot de resource Hallo heeft. Dit gehele proces wordt uitgevoerd op de achtergrond, zonder tussenkomst van de gebruiker. Het is ook mogelijk toogrant machtiging tooa [groep](active-directory-manage-groups.md#getting-started-with-access-management) van gebruikers in de volgorde tooallow ze tooperform bepaalde algemene acties.

Organisaties die zorgen te maken over de privacy van gegevens meestal zijn vereisen gegevensclassificatie voor hun oplossing. Als hun huidige on-premises infrastructuur gegevensclassificatie al wordt gebruikt, is het mogelijk tooleverage Azure AD als Hallo belangrijkste opslagplaats voor de identiteit van gebruiker. Een algemene hulpprogramma dat het gebruikte lokaal is voor gegevensclassificatie heet [Data Classification Toolkit](https://msdn.microsoft.com/library/Hh204743.aspx) voor Windows Server 2012 R2. Dit hulpprogramma kunt tooidentify help, classificeren en beveiligen van gegevens op bestandsservers in uw privécloud. Het is ook mogelijk tooleverage hello [automatische Bestandsclassificatie](https://technet.microsoft.com/library/hh831672.aspx) in Windows Server 2012 tooaccomplish dit.

Als uw organisatie geen gegevensclassificatie aanwezig maar tooprotect vertrouwelijke bestanden moet zonder nieuwe Servers lokale toe te voegen, kunnen ze gebruiken Microsoft [Azure Rights Management Service](https://technet.microsoft.com/library/JJ585026.aspx).  Azure RMS-versleuteling, identiteit en autorisatie beleidsregels van beveiligde toohelp gebruikt uw bestanden en e-mail en het werkt op meerdere apparaten, telefoons, tablets en pc's. Omdat Azure RMS een cloudservice is, is niet nodig tooexplicitly vertrouwensrelaties met andere organisaties configureren voordat u beveiligde inhoud met hen kunt delen. Als ze al een Office 365 of Azure AD-directory, wordt samenwerking tussen verschillende organisaties automatisch ondersteund. U kunt ook synchroniseren NET Hallo mapkenmerken die Azure RMS nodig toosupport een algemene identiteit voor uw lokale Active Directory-accounts heeft met behulp van Azure Active Directory-Synchronisatieservices (AAD Sync) of Azure AD Connect.

Een essentieel onderdeel van inhoudsbeheer toounderstand wie toegang heeft tot welke resource, een uitgebreide logboekregistratie kunnen is daarom belangrijk voor de oplossing voor identiteitsbeheer Hallo. Azure AD levert logboek meer dan 30 dagen, met inbegrip van:

* Wijzigingen in het rollidmaatschap (ex: gebruiker tooGlobal beheerdersrol toegevoegd)
* Referentie-updates (ex: wachtwoordwijzigingen)
* Domeinbeheer (ex: een aangepast domein, verwijderen van een domein controleren)
* Het toevoegen of verwijderen van toepassingen
* Gebruikersbeheer (ex: toevoegen, verwijderen, het bijwerken van een gebruiker)
* Het toevoegen of verwijderen van licenties

> [!NOTE]
> Lees [Microsoft Azure-beveiliging en Audit Log-beheer](http://download.microsoft.com/download/B/6/C/B6C0A98B-D34A-417C-826E-3EA28CDFC9DD/AzureSecurityandAuditLogManagement_11132014.pdf) tooknow meer informatie over mogelijkheden voor logboekregistratie in Azure.
> Afhankelijk van hoe u de vragen in Hallo beantwoord [inhoudsbeheer vereisten bepalen](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md), moet u kunnen toodetermine gewenste Hallo inhoud toobe beheerd in uw oplossing voor hybride identiteit. Hoewel alle opties die beschikbaar zijn in tabel 6 kan worden geïntegreerd met Azure AD zijn, is het belangrijk toodefine die meer geschikt is voor uw zakelijke behoeften.
>
>

| Opties voor inhoudbeheer | Voordelen | Nadelen |
| --- | --- | --- |
| Gecentraliseerd op locatie (Active Directory Rights Management Server) |Volledige controle over Hallo serverinfrastructuur verantwoordelijk voor het classificeren van Hallo-gegevens <br> Ingebouwde mogelijkheden in Windows Server is niet nodig om extra licentie of abonnement <br> Kan worden geïntegreerd met Azure AD in een hybride scenario <br> Ondersteunt mogelijkheden voor information rights management (IRM) in Microsoft Online services, zoals Exchange Online en SharePoint Online, evenals Office 365 <br> Biedt ondersteuning voor lokale Microsoft server-producten, zoals Exchange Server, SharePoint Server en bestandsservers waarop Windows Server en infrastructuur voor Bestandsclassificatie (FCI). |Hogere, onderhoud (gelijke tred houden met updates, configuratie en mogelijke upgrades), sinds IT eigenaar is van Hallo Server <br> Vereist een serverinfrastructuur lokale<br> Doesn'tleverage mogelijkheden van Azure systeemeigen |
| Gecentraliseerd in Hallo cloud (Azure RMS) |Eenvoudiger toomanage vergeleken toohello lokale oplossing <br> Kan worden geïntegreerd met AD DS in een hybride scenario <br>  Volledig geïntegreerd met Azure AD <br> Een server vereist lokale in volgorde toodeploy Hallo-service <br> Ondersteunt on-premises Microsoft server-producten zoals Exchange Server, SharePoint Server en bestandsservers waarop Windows Server en File Classification, Infrastructure (FCI) <br> IT, kan volledige controle over hun tenantsleutel met BYOK-functionaliteit hebben. |Uw organisatie moet een cloudabonnement hebben met RMS ondersteunt <br> Uw organisatie moet een Azure AD directory toosupport-gebruikersverificatie voor RMS hebben |
| Hybride (Azure RMS is geïntegreerd met, On-Premises Active Directory Rights Management Server) |Dit scenario stelt Hallo voordelen van beide, gecentraliseerd op locatie en in de cloud Hallo samen. |Uw organisatie moet een cloudabonnement hebben met RMS ondersteunt <br> Uw organisatie moet een Azure AD directory toosupport-gebruikersverificatie voor RMS, hebben <br> Vereist een verbinding tussen Azure-cloudservice en on-premises infrastructuur |

## <a name="define-access-control-options"></a>Definieer de opties voor toegangsbeheer
Dankzij het gebruik van Hallo-verificatie, beheren autorisatie en toegang mogelijkheden beschikbaar zijn in Azure AD kunt u zich kunt tooenable uw bedrijf toouse een centrale identiteitsopslagplaats en tegelijkertijd gebruikers en partners toouse eenmalige aanmelding (SSO) zoals in Hallo de afbeelding hieronder:

![](./media/hybrid-id-design-considerations/centralized-management.png)

Gecentraliseerd beheer en volledig integratie met andere directory 's

Azure Active Directory biedt toothousands voor eenmalige aanmelding van de SaaS-toepassingen en lokale webtoepassingen. Lees Hallo [federatiecompatibiliteitslijst van Azure Active Directory: van derden id-providers die gebruikt tooimplement worden kunnen eenmalige aanmelding](https://msdn.microsoft.com/library/azure/jj679342.aspx) artikel voor meer informatie over Hallo SSO van derden die zijn getest door Microsoft Corporation. Deze mogelijkheid kan organisatie tooimplement tal van B2B-scenario's terwijl de controle van Hallo identiteits- en toegangsbeheer management. Tijdens Hallo B2B ontwerpen proces is het echter belangrijk toounderstand Hallo-verificatiemethode die wordt gebruikt door de partner Hallo en valideren van deze methode wordt ondersteund door Azure. Dit zijn momenteel methoden die worden ondersteund door Azure AD:

* Security Assertion Markup Language (SAML)
* OAuth
* Kerberos
* Tokens
* Certificaten

> [!NOTE]
> Lees [Azure Active Directory-verificatieprotocollen](https://msdn.microsoft.com/library/azure/dn151124.aspx) tooknow om meer details over elk protocol en de mogelijkheden ervan in Azure.
>
>

Met de ondersteuning van hello Azure AD, mobiele, zakelijke toepassingen gebruikmaken van kunnen dezelfde eenvoudig Mobile Services-verificatie-ervaring tooallow werknemers toosign Hallo met hun mobiele toepassingen met hun zakelijke Active Directory-referenties. Met deze functie van Azure AD wordt ondersteund als een id-provider in Mobile Services naast Hello andere id-providers die wij bieden al ondersteuning (waaronder Microsoft-Accounts, Facebook-ID, ID van Google en Twitter-ID). Als Hallo on-premises apps maakt gebruik van referenties van de gebruiker zich bevindt op Hallo van het bedrijf AD DS Hallo moet Hallo toegang van partners en gebruikers die afkomstig zijn van de cloud Hallo niet transparant zijn. U kunt beheren van de gebruiker voorwaardelijke toegang besturingselement too(cloud-based) webtoepassingen, web-API, Microsoft cloud-services, 3e SaaS-toepassingen van derden en systeemeigen (mobiele) clienttoepassingen en Hallo voordelen van beveiliging, controle en de rapportage-alles in één plaats. Het is echter toovalidate aanbevolen dit in een niet-productieomgeving of met een beperkte hoeveelheid gebruikers.

> [!TIP]
> het is belangrijk toomention dat Azure AD geen groepsbeleid heeft zoals AD DS heeft. In de volgorde tooenforce beleid voor apparaten moet u een beheersysteem voor mobiele apparaten, zoals [Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx).
>
>

Zodra het Hallo-gebruiker is geverifieerd met behulp van Azure AD, is het belangrijk tooevaluate Hallo toegangsniveau dat Hallo gebruiker heeft deze. Hallo toegangsniveau dat Hallo gebruiker hebben via een resource kan variëren, Azure AD kunt u een extra beveiligingslaag toevoegen door de controle over toegang tot toosome bronnen, u moet ook rekening houden Hallo resource zelf kan ook een eigen toegangsbeheerlijst hebben afzonderlijk, zoals Hallo toegangsbeheer voor bestanden in een bestandsserver. Hallo afbeelding hieronder bevat een overzicht van Hallo niveaus van toegangsbeheer dat u in een hybride scenario opnemen kunt:

![](./media/hybrid-id-design-considerations/accesscontrol.png)

Elke interactie in Hallo diagram weergegeven zoals in afbeelding X vertegenwoordigt een access control-scenario die kan worden volstaan met Azure AD. Hieronder hebt u een beschrijving van elk scenario:

1. Voorwaardelijke toegang tooapplications die worden gehost op de lokale: U kunt geregistreerde apparaten met toegangsbeleid voor toepassingen die zijn geconfigureerd toouse AD FS met Windows Server 2012 R2. Zie [Setting up On-premises Conditional Access using Azure Active Directory Device Registration](active-directory-conditional-access.md) (Engelstalig) voor meer informatie over het instellen van on-premises voorwaardelijke toegang.

2. Access Control toohello Azure-portal: Azure kunt u ook beheer toegang toohello portal met behulp van op rollen gebaseerde toegangsbeheer (RBAC)). Deze methode kunt Hallo bedrijf toorestrict Hallo hoeveelheid bewerkingen die een persoon in hello Azure-portal kunt uitvoeren. Met behulp van RBAC toocontrol toegang toohello portal, kunnen IT-beheerders toegang delegeren met behulp van de volgende access management benaderingen Hallo:

* Op basis van een groep roltoewijzing: U toegang kunt geven tooAzure AD-groepen die kunnen worden gesynchroniseerd vanuit uw lokale Active Directory. Hiermee kunt u tooleverage Hallo bestaande investeringen die uw organisatie heeft aangebracht in tooling en processen voor het beheren van groepen. U kunt ook Hallo overgedragen groep management-functie van Azure AD Premium.
* Gebruik de ingebouwde rollen in Azure: kunt u drie rollen: eigenaar, bijdrager en Reader tooensure dat gebruikers en groepen machtiging toodo alleen Hallo taken die ze toodo hun werk nodig hebt.
* Gedetailleerde toegang tooresources: U kunt toewijzen toousers rollen en groepen voor een bepaald abonnement, resourcegroep of een afzonderlijke Azure resource, zoals een website of de database. Op deze manier kunt u ervoor zorgen dat gebruikers hebben toegang tot tooall Hallo-bronnen die ze nodig hebben en geen toegang tot tooresources dat ze niet toomanage hoeven.

> [!NOTE]
> Als u toepassingen bouwt en toegangsbeheer voor toocustomize hello wilt, maar het is ook mogelijk toouse Azure AD-toepassing-functies voor autorisatie. Bekijk dit [WebApp-RoleClaims-DotNet voorbeeld](https://github.com/AzureADSamples/WebApp-RoleClaims-DotNet) over het toobuild uw app toouse deze mogelijkheid.
>
>

3. Voorwaardelijke toegang voor Office 365-toepassingen met Microsoft Intune: IT-beheerders kunnen voorwaardelijke toegang apparaat beleid toosecure bedrijfsbronnen, inrichten terwijl op Hallo dezelfde toestaan informatiemedewerkers op compatibele apparaten tooaccess Hallo tijdstip Services. Zie [Conditional Access Device Policies for Office 365 services (Engelstalig)](active-directory-conditional-access-device-policies.md) voor meer informatie.

4. Voorwaardelijke toegang voor Saas-apps: [deze functie](http://blogs.technet.com/b/ad/archive/2015/06/25/azure-ad-conditional-access-preview-update-more-apps-and-blocking-access-for-users-not-at-work.aspx) kunt u toegangsregels voor tooconfigure per toepassing multi-factor authentication-server en Hallo mogelijkheid tooblock toegang voor gebruikers niet op een vertrouwd netwerk. U kunt Hallo multi-factorauthenticatie regels tooall gebruikers die zijn toegewezen toohello toepassing, of alleen voor gebruikers binnen de opgegeven beveiligingsgroepen kunt toepassen. Gebruikers kunnen worden uitgesloten van Hallo multi-factorauthenticatie vereiste als ze toegang hebben tot de toepassing hello van een IP-adres dat in binnen bedrijfsnetwerk Hallo.

Omdat Hallo opties voor toegangsbeheer gebruiken een gelaagde benadering, vergelijking tussen deze opties zijn niet geldig voor deze taak. Zorg ervoor dat u gebruik van alle beschikbare opties voor elk scenario dat vereist dat u toocontrol toegang tot tooyour bronnen.

## <a name="define-incident-response-options"></a>Definieer de opties voor respons op incidenten
Azure AD kan IT tooidentity potentiële beveiligingsrisico's in de omgeving Hallo door de bewaking van de activiteit van de gebruiker, kan IT gebruikmaken van Azure AD Access en gebruiksrapporten mogelijkheid toogain zichtbaarheid van Hallo integriteit en beveiliging van de directory van uw organisatie helpen. Met deze informatie kunt kan IT-beheerder beter bepalen waar mogelijk beveiligingsrisico's zodat u ze kunnen toomitigate voldoende plannen die risico's kunnen liggen.  [Azure AD Premium-abonnement](active-directory-get-started-premium.md) beschikt over een reeks beveiligingsrapporten die IT tooobtain deze informatie kunt inschakelen. [Azure AD-rapporten](active-directory-view-access-usage-reports.md) worden gecategoriseerd zoals hieronder wordt weergegeven:

* **Rapporten voor afwijkingsdetectie**: Meld u aan dat we toobe afwijkende gevonden gebeurtenissen bevatten. Ons doel is toomake u rekening houden met deze activiteit en kunt u toobe kunnen toomake om te bepalen of een gebeurtenis verdacht is.
* **Rapport van de toepassing geïntegreerde**: biedt inzicht in hoe cloud-toepassingen in uw organisatie worden gebruikt. Azure Active Directory biedt integratie met duizenden cloud-toepassingen.
* **Foutenrapporten**: fouten die zich voordoen kunnen bij het inrichten van accounts tooexternal toepassingen aangeven.
* **Rapporten van de gebruiker gedefinieerde**: apparaat/teken weergeven in de activiteitsgegevens voor een specifieke gebruiker.
* **Activiteitenlogboeken**: bevatten een record van alle controlegebeurtenissen binnen Hallo afgelopen 24 uur, de afgelopen 7 dagen of de laatste 30 dagen, evenals wijzigingen in groep activiteiten en activiteit voor wachtwoord opnieuw instellen en registratie.

> [!TIP]
> Een ander rapport waarmee u kunt ook Hallo Incident Response-team werkt aan een aanvraag wordt Hallo [gebruiker met gelekte referenties](http://blogs.technet.com/b/ad/archive/2015/06/15/azure-active-directory-premium-reporting-now-detects-leaked-credentials.aspx) rapport.  Dit rapport geeft alle resultaten weer tussen deze lijst gelekte aanmeldingsreferenties en uw tenant.
>
>

Andere belangrijke ingebouwd in rapporten in Azure AD dat kan worden gebruikt tijdens een onderzoek respons op incidenten en zijn:

* **Activiteit voor wachtwoordherstel**: Hallo beheerder voorzien van inzicht in hoe vaak opnieuw instellen van wachtwoorden in Hallo organisatie wordt gebruikt.
* **Registratie-activiteit wachtwoord opnieuw instellen**: biedt inzicht in dat gebruikers hun methoden voor het wachtwoord opnieuw instellen, hebt geregistreerd en welke methoden ze hebt geselecteerd.
* **Groep activiteit**: biedt een overzicht van de groep toohello wijzigingen (ex: gebruikers toegevoegd of verwijderd) die zijn gestart in Hallo Toegangsvenster.

Bovendien toohello core rapportagemogelijkheid beschikbaar zijn in Azure AD Premium die kan worden gebruikt tijdens een Incident Response onderzoek, kan IT ook gebruikmaken van controlerapport tooobtain informatie, zoals:

* Wijzigingen in het rollidmaatschap (ex: gebruiker tooGlobal beheerdersrol toegevoegd)
* Referentie-updates (ex: wachtwoordwijzigingen)
* Domeinbeheer (ex: een aangepast domein, verwijderen van een domein controleren)
* Het toevoegen of verwijderen van toepassingen
* Gebruikersbeheer (ex: toevoegen, verwijderen, het bijwerken van een gebruiker)
* Het toevoegen of verwijderen van licenties

Omdat Hallo opties voor respons op incidenten een gelaagde benadering, vergelijking tussen deze opties zijn niet geldig voor deze taak. Zorg ervoor dat u gebruik van alle beschikbare opties voor elk scenario dat vereist dat u toouse Azure AD-rapportagemogelijkheid als onderdeel van uw bedrijf respons op incidenten.

## <a name="next-steps"></a>Volgende stappen
[Beheertaken voor hybride identiteit bepalen](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)

## <a name="see-also"></a>Zie ook
[Overzicht ontwerpoverwegingen](active-directory-hybrid-identity-design-considerations-overview.md)
