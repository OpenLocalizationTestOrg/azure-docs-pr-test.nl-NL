---
title: technische beveiligingsmogelijkheden aaaAzure | Microsoft Docs
description: Meer informatie over cloud-gebaseerde computers onder meer services als een groot aantal compute-exemplaren en services die kunnen worden geschaald omhoog en omlaag automatisch toomeet Hallo behoeften van uw toepassing of enterprise.
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/26/2017
ms.author: TomSh
ms.openlocfilehash: a0ef17883be54dab4cb6b597204f3197dc05c28c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-technical-capabilities"></a>Technische mogelijkheden van Azure-beveiliging

tooassist huidige en toekomstige Azure-klanten begrijpen en te gebruiken Hallo verschillende beveiligingsgerelateerde-mogelijkheden beschikbaar in en omringende Hallo Azure-Platform, er is een reeks whitepapers, overzichten van de beveiliging, Best Practices, ontwikkeld en Controlelijsten. bereik van de onderwerpen in termen van breedte en diepte Hallo en regelmatig worden bijgewerkt. Dit document is onderdeel van de reeks zoals samengevat in Hallo abstracte sectie hieronder. Meer informatie over deze reeks Azure-beveiliging kan worden gevonden op (URL).

## <a name="azure-platform"></a>Azure-platform

[Microsoft Azure](https://azure.microsoft.com/overview/what-is-azure/) een cloudplatform bestaat uit de infrastructuur en toepassingsservices met geïntegreerde gegevensservices en geavanceerde analyses en hulpprogramma's voor ontwikkelaars en -services, gehost in Microsoft van openbare cloud data centers. Klanten kunnen Azure gebruiken voor veel verschillende capaciteiten en scenario's van basic compute, netwerk en opslag, toomobile en web-app-services, toofull cloud scenario's zoals Internet der dingen worden gebruikt met open-source technologieën en geïmplementeerd als hybride cloud of gehost binnen het datacenter van de klant. Azure biedt cloud technologie als bouwstenen toohelp bedrijven kosten besparen, snel innoveren en systemen proactief beheren. Wanneer u bouwen op of migreren van IT activa tooa cloudprovider, zijn u afhankelijk te zijn van die organisatie mogelijkheden tooprotect uw toepassingen en gegevens met Hallo services en ze toomanage Hallo beveiliging van uw cloud-gebaseerde activa bieden Hallo-besturingselementen.

Microsoft Azure is Hallo alleen cloud computing provider die een veilige, consistente toepassingsplatform en infrastructuur-as-a-service voor toowork teams binnen hun andere cloud vaardigheden en niveaus van project complexiteit, met geïntegreerde gegevens biedt Services en analyses die onthullen intelligence van gegevens naar waar deze zich voor zowel Microsoft als niet-Microsoft-platforms, open frameworks en hulpprogramma's, biedt opties voor het integreren van cloud met on-premises evenals Azure-cloud-services binnen implementeren een on-premises datacenters. Als onderdeel van Microsoft vertrouwde Cloud hello, zijn klanten afhankelijk van Azure voor toonaangevende beveiliging, betrouwbaarheid, naleving, privacy en Hallo vast netwerk van de mensen, partners en processen toosupport organisaties in Hallo cloud.

U kunt met Microsoft Azure:

- Innovatie Hallo cloud versnellen.

- Power zakelijke beslissingen te nemen en apps met insights.

- Vrij te maken en implementeren van elke locatie.

- Beveiligen van hun bedrijf.

## <a name="scope"></a>Bereik

Hallo contactpunt van dit technisch document betreft beveiligingsfuncties en -functionaliteit ondersteunen de basisonderdelen van Microsoft Azure, namelijk [Microsoft Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction), [Microsoft Azure SQL-Databases](https://docs.microsoft.com/azure/sql-database/), [Van Microsoft Azure virtuele machine model](https://docs.microsoft.com/azure/virtual-machines/  ), en Hallo-hulpprogramma's en infrastructuur die alles beheren. Dit technisch document ligt de nadruk op Microsoft Azure technische mogelijkheden beschikbaar tooyou als klanten toofulfil hun rol binnen het Hallo-beveiliging en privacy van gegevens te beveiligen.

Hallo belang van inzicht in dit model gedeelde verantwoordelijkheid is essentieel voor klanten die toohello cloud verplaatst. Cloudproviders bieden aanzienlijke voordelen voor beveiliging en naleving inspanningen, maar deze voordelen komen niet absolve Hallo klant hun gebruikers, toepassingen en serviceaanbiedingen beveiligen.

Hallo klant verantwoordelijk is of een gedeelde verantwoordelijk is voor het beveiligen en beheren van Hallo-besturingssysteem, netwerkconfiguratie, toepassingen, identiteit, clients en gegevens voor IaaS-oplossingen.  PaaS-oplossingen bouwen op IaaS-implementaties, Hallo klant is nog steeds verantwoordelijk of een gedeelde verantwoordelijk is voor het beveiligen en beheren van toepassingen, identiteit, clients en gegevens. Voor SaaS-oplossingen, Nonetheless, blijft de klant Hallo toobe die verantwoordelijk zijn. Ze moeten ervoor zorgen dat gegevens correct ingedeeld en ze een toomanage verantwoordelijkheid hun gebruikers- en eindpunt-apparaten delen.

Dit document biedt geen gedetailleerde dekking van elk Hallo Microsoft Azure-platform-onderdelen zoals Azure websites, Azure Active Directory, HDInsight, Media Services en andere services die zijn gelaagd op Hallo kernonderdelen gerelateerd. Hoewel een minimaal niveau van algemene informatie is opgegeven, zijn lezers verondersteld bekend bent met Azure basisconcepten, zoals beschreven in andere verwijzingen naar door Microsoft geleverd en opgenomen in de koppelingen in dit document.


## <a name="available-security-technical-capabilities-toofulfil-user-customer-responsibility---big-picture"></a>Beschikbare beveiligingsupdates technische mogelijkheden toofulfil gebruiker (klant) verantwoordelijkheid - grote afbeelding

Microsoft Azure biedt services waarmee klanten kunnen voldoen aan de Hallo beveiliging, privacy en naleving behoeften. Hallo volgende afbeelding kunt uitgelegd verschillende Azure-services beschikbaar voor gebruikers toobuild een infrastructuur voor beveiligd en compatibel zijn op basis van industrienormen.

![Beschikbare beveiligingsupdates technische mogelijkheden Big-afbeelding](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig1.png)

## <a name="manage-and-control-identity-and-user-access-protect"></a>Beheren en beheren van identiteiten en -toegang (beveiligen)

Azure helpt u zakelijke en persoonlijke gegevens beveiligen doordat u toomanage gebruikers-id's en referenties en toegang beheren.

### <a name="azure-active-directory"></a>Azure active directory

Microsoft identiteits- en toegangsbeheer management oplossingen zorgen ervoor dat IT beveiligen toegang tooapplications en bronnen in zakelijke datacenter hello en in de cloud hello, extra niveaus van validatie van de multi-factor Authentication-verificatie en voorwaardelijke inschakelen beleid voor toegang. Bewaking verdachte activiteiten via geavanceerde beveiliging rapportage, controle en waarschuwingen helpt bij het verminderen mogelijke beveiligingsproblemen. [Azure Active Directory Premium](https://docs.microsoft.com/azure/active-directory/active-directory-editions) biedt eenmalige aanmelding toothousands van cloudtoepassingen (SaaS)-apps en toegang tooweb apps u on-premises uitgevoerd.

Beveiligingsvoordelen van Azure Active Directory (AD) omvatten Hallo kunnen:

- Maken en beheren van één identiteit voor elke gebruiker in uw onderneming hybride, gebruikers, groepen en apparaten synchroon te houden.

- Geef één aanmelding toegang tooyour toepassingen, waaronder duizenden vooraf geïntegreerde SaaS-apps.

- Toepassingsbeveiliging toegang inschakelen door het afdwingen van multi-factor Authentication op basis van regels voor zowel on-premises en cloudtoepassingen.

- Inrichten veilige externe toegang tooon-premises webtoepassingen via Azure AD-toepassingsproxy.

[Azure active directory-portal](http://aad.portal.azure.com/) vindt u een deel van de azure-portal. Uit dit dashboard kunt u een overzicht van status van uw organisatie Hallo en eenvoudig Duik in de directory hello, gebruikers of toegang tot toepassingen beheren.

![Azure active directory](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig2.png)

Volgende zijn belangrijkste Azure Identity management mogelijkheden:

- Eenmalige aanmelding

- Multi-Factor Authentication

- Beveiligingsbewaking, waarschuwingen en machine learning gebaseerde rapporten

- Identiteits- en toegangsbeheer van consumenten

- Apparaatregistratie

- Beschermde identiteitsbeheer

- Identiteitsbeveiliging

#### <a name="single-sign-on"></a>Eenmalige aanmelding

[Eenmalige aanmelding (SSO)](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) betekent kunnen tooaccess wordt alle Hallo toepassingen en bronnen die u toodo bedrijven, nodig wanneer u zich aanmeldt bij het gebruik van slechts één keer één gebruikersaccount. Nadat u bent aangemeld, u toegang hebt tot alle Hallo toepassingen zonder de vereiste tooauthenticate wordt (bijvoorbeeld: Typ een wachtwoord) een tweede keer.

Veel organisaties zijn afhankelijk van de software als een dienst (SaaS)-toepassingen zoals Office 365, het selectievakje en Salesforce voor de productiviteit van eindgebruikers. In het verleden hebben IT-personeel nodig tooindividually maken en bijwerken van gebruikersaccounts in elke SaaS-toepassing en moesten gebruikers deze tooremember een wachtwoord op voor elke SaaS-toepassing.

[Azure AD door op de lokale Active Directory in de cloud Hallo](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis), waardoor gebruikers toouse hun primaire organisatie-account toonot alleen aanmelden tootheir domein apparaten en resources van het bedrijf, maar ook alle Hallo web- en SaaS-toepassingen nodig voor hun taak.

Niet alleen hebben gebruikers geen toomanage meerdere sets met gebruikersnamen en wachtwoorden, toegang tot de toepassing kan worden automatisch ingerichte of ongedaan ingerichte op basis van organisatie-groepen en hun status als een werknemer. [Azure AD de beveiliging en toegang governance besturingselementen introduceert](https://docs.microsoft.com/azure/active-directory/active-directory-sso-integrate-saas-apps) waarmee u toocentrally toegang van gebruikers in de SaaS-toepassingen beheren.

#### <a name="multi-factor-authentication"></a>Multi-Factor Authentication

[Azure multi-factor authentication (MFA)](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) is een methode voor verificatie dat Hallo gebruik van meer dan één verificatiemethode vereist en wordt toegevoegd een cruciale tweede beveiligingslaag van beveiliging toouser aanmeldingen en transacties. [MFA helpt safeguard](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-how-it-works) toodata en toepassingen te openen en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden. Levert sterke verificatie via een aantal opties voor verificatie: telefoonoproep, tekstbericht of mobiele app melding of verificatie van code en derden OAuth-tokens.

#### <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>Beveiligingsbewaking, waarschuwingen en machine learning gebaseerde rapporten

Beveiligingsbewaking en waarschuwingen en machine learning gebaseerde rapporten die inconsistente toegangspatronen aangeven kunt u uw bedrijf te beveiligen. U kunt toegang tot Azure Active Directory en gebruik rapporten toogain inzicht in Hallo integriteit en beveiliging van de directory van uw organisatie gebruiken. Met deze informatie kunt kan directory-beheerder beter bepalen waar mogelijk beveiligingsrisico's zodat u ze kunnen toomitigate voldoende plannen die risico's kunnen liggen.

In de klassieke Azure-portal Hallo of via [Azure Active directory-portal](http://aad.portal.azure.com/), [rapporten](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) zijn onderverdeeld in de volgende manieren Hallo:

- Rapporten voor afwijkingsdetectie – bevatten Meld u aan dat we toobe afwijkende gevonden gebeurtenissen. Ons doel is toomake u rekening houden met deze activiteit en kunt u toobe kunnen toodecide of een gebeurtenis verdacht is.

- Geïntegreerde toepassing rapporten – bieden inzicht in hoe cloud-toepassingen in uw organisatie worden gebruikt. Azure Active Directory biedt integratie met duizenden cloud-toepassingen.

- Foutenrapporten – fouten die zich kunnen voordoen bij het inrichten van accounts tooexternal toepassingen aangeven.

- Apparaat/teken weergeven gebruikersspecifieke rapporten – in de activiteitsgegevens voor een specifieke gebruiker.

- Activiteitenlogboeken – bevatten een record van alle controlegebeurtenissen binnen Hallo afgelopen 24 uur en de laatste 7 dagen, of afgelopen 30 dagen en wijzigingen in groep activiteiten en activiteit voor wachtwoord opnieuw instellen en registratie.

#### <a name="consumer-identity-and-access-management"></a>Identiteits- en toegangsbeheer van consumenten

[Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) is een maximaal beschikbare, wereldwijde, identity management-service voor consumententoepassingen die schaalbaar toohundreds miljoenen identiteiten. De service kan worden geïntegreerd in zowel mobiele als webplatforms. Uw consumenten kunnen aanmelden tooall uw toepassingen via aanpasbare ervaringen met behulp van hun bestaande sociale accounts of maken van nieuwe referenties.

In Hallo voorbij toepassingsontwikkelaars wie te wilde[aanmelden en meld u aan consumenten](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview) in hun toepassingen schreven hun eigen code. En ze gebruikten lokale databases of systemen toostore gebruikersnamen en wachtwoorden. Azure Active Directory B2C biedt uw organisatie een betere manier toointegrate identiteitsbeheer van consumenten in toepassingen met help Hallo van een veilige, op standaarden gebaseerd platform en een grote set uitbreidbare beleidsregels.

Wanneer u Azure Active Directory B2C gebruikt, uw consumenten zich registreren voor uw toepassingen met behulp van hun bestaande sociale accounts (Facebook, Google, Amazon, LinkedIn) of door het maken van nieuwe referenties (e-mailadres en wachtwoord of gebruikersnaam en wachtwoord).

Apparaatregistratie

[Azure AD-apparaatregistratie](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-device-registration-overview) is Hallo basis voor apparaatgebaseerde [voorwaardelijke toegang](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-device-registration-overview) scenario's. Wanneer een apparaat is geregistreerd, biedt Azure Active Directory-apparaatregistratie Hallo-apparaat met een identiteit die is gebruikt tooauthenticate Hallo apparaat wanneer Hallo gebruiker zich aanmeldt. vervolgens Hallo geverifieerde apparaat en Hallo kenmerken van Hallo-apparaat, kunnen de gebruikte tooenforce beleidsregels voor voorwaardelijke toegang voor toepassingen die worden gehost in Hallo cloud en on-premises worden.

In combinatie met een [beheer van mobiele apparaten (MDM)](https://www.microsoft.com/itshowcase/Article/Content/588/Mobile-device-management-at-Microsoft) oplossing zoals Intune, Hallo apparaatkenmerken in Azure Active Directory worden bijgewerkt met aanvullende informatie over het Hallo-apparaat. Hiermee kunt u regels voor voorwaardelijke toegang toocreate die toegang van apparaten toomeet afdwingen uw standaarden voor beveiliging en naleving.

#### <a name="privileged-identity-management"></a>Beschermde identiteitsbeheer

[Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure) kunt u beheren, het beheren, en het controleren van bevoegde identiteiten en tooresources openen in Azure AD en ook voor andere Microsoft online services, zoals Office 365 of Microsoft Intune.

Gebruikers moeten soms toocarry bevoorrechte bewerkingen in de resources in Azure of Office 365 of andere SaaS-apps. Dit betekent vaak organisaties hebben toogive ze permanente bevoegde toegang in Azure AD. Dit is een groeiende beveiligingsrisico voor cloud-gebaseerde bronnen omdat organisaties voldoende kunnen niet controleren wat gebruikers doen met hun beheerdersbevoegdheden. Als een gebruikersaccount met uitgebreide toegang is aangetast, kan die een inbreuk bovendien invloed op de algehele beveiliging van de cloud. Azure AD Privileged Identity Management helpt tooresolve dit risico.

Azure AD Privileged Identity Management kunt u:

- Zien welke gebruikers zijn Azure AD-beheerders

- On-demand 'just in time' beheerderstoegang tooMicrosoft Online Services, zoals Office 365 en Intune inschakelen

- Rapporten over beheerder toegang tot geschiedenis en wijzigingen in beheerderstoewijzingen ophalen

- Ontvang waarschuwingen over toegang tooa bevoorrechte rol

#### <a name="identity-protection"></a>Identiteitsbeveiliging

[Azure AD Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) is een beveiligingsservice biedt een geconsolideerde weergave risicogebeurtenissen en mogelijke beveiligingsproblemen die invloed hebben op de identiteiten van uw organisatie. Identity Protection gebruikt bestaande Azure Active Directory van afwijkingsdetectie-detectiemogelijkheden (beschikbaar via Azure AD-rapporten voor afwijkende activiteiten) en introduceert nieuwe risico gebeurtenistypen die afwijkingen in realtime kunnen detecteren.

## <a name="secured-resource-access-in-azure"></a>Toegang tot beveiligde bronnen in Azure

Toegangsbeheer in Azure wordt gestart vanuit het oogpunt van facturering van. Hallo-eigenaar van een Azure-account toegankelijk via Hallo [Azure-Accountcentrum](https://account.windowsazure.com/subscriptions), Hallo Account Administrator (AA) is. Abonnementen zijn een container voor facturering, maar ze ook fungeren als een beveiligingsgrens: elk abonnement heeft een Service Administrator (SA) die u kunt toevoegen, verwijderen en wijzigen van de Azure-resources in het desbetreffende abonnement met behulp van Hallo [klassieke Azure-portal](https://manage.windowsazure.com/). Hallo standaard SA van een nieuw abonnement Hallo AA is, maar Hallo AA Hallo SA in hello Azure Accounts Center kunt wijzigen.

![Toegang tot beveiligde bronnen in Azure](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig3.png)

Abonnementen hebben ook een koppeling naar een map. Hallo directory definieert een set van gebruikers. Deze kunnen gebruikers van Hallo werk of school die Hallo directory gemaakt, of ze kunnen externe gebruikers (dat wil zeggen, een Microsoft-Accounts). Abonnementen zijn toegankelijk voor een subset van de directorygebruikers die zijn toegewezen als Service-beheerder (SA) of Medebeheerder (CA); Hallo alleen uitzondering is dat, omwille van de oudere Microsoft-Accounts (voorheen Windows Live ID) kan worden toegewezen als SA of CA zonder aanwezig is in het Hallo-directory.

Beveiliging gerichte bedrijven moeten zich richten op uw werknemers Hallo exacte machtigingen die ze nodig hebben. Te veel machtigingen kunnen een account tooattackers worden blootgesteld. Te weinig machtigingen betekenen dat werknemers hun werk efficiënt kunnen niet ophalen. [Azure op rollen gebaseerde toegangsbeheer (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) helpt dit probleem oplossen door het aanbieden van Geavanceerd toegangsbeheer voor Azure.

![Toegang tot beveiligde bronnen ](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig4.png)

Met RBAC kunt u taken scheiden binnen uw team en alleen Hallo hoeveelheid toousers toegang verlenen die zij nodig hebben tooperform hun werk. In plaats van iedereen geven onbeperkte machtigingen in uw Azure-abonnement of de bronnen, kunt u alleen bepaalde acties. Bijvoorbeeld gebruik RBAC toolet één werknemer virtuele machines in een abonnement beheren, terwijl andere kunt beheren van SQL-databases binnen Hallo hetzelfde abonnement.

![Toegang tot beveiligde bronnen in Azure(RBAC)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig5.png)

## <a name="azure-data-security-and-encryption-protect"></a>Azure gegevensbeveiliging en -versleuteling (beveiligen)

Een van de Hallo sleutels toodata beveiliging in de cloud Hallo is accounting voor Hallo mogelijke statussen in die uw gegevens zich kunnen voordoen, en welke besturingselementen beschikbaar zijn voor die status. Voor Azure gegevensbeveiliging en versleuteling Hallo aanbevelingen worden rond Hallo statussen van gegevens te volgen.

- In rust: Dit omvat alle informatie opslagobjecten, containers en typen die statisch bestaan op de fysieke media, worden deze magnetische of optische schijf.

- In Transit: Wanneer gegevens worden overgebracht tussen onderdelen, locaties of programma's, zoals via Hallo-netwerk via een servicebus (van lokale toocloud en vice versa, inclusief hybride verbindingen zoals ExpressRoute) of tijdens een i/o proces, dit wordt beschouwd als wordt in beweging.

### <a name="encryption--rest"></a>Versleuteling @ rest

tooachieve versleuteling in rust van Hallo volgende:

Ondersteuning voor ten minste één Hallo aanbevolen versleuteling modellen in detail beschreven op Hallo tooencrypt tabelgegevens te volgen.

| Versleuteling modellen |  |  |  |
| ----------------  | ----------------- | ----------------- | --------------- |
| Server-versleuteling | Server-versleuteling | Server-versleuteling | Client-versleuteling
| Serverzijde codering met sleutels voor Service beheerd | Serverzijde versleuteling met Customer-Managed sleutels in Azure Sleutelkluis | Server-side '-codering met on-premises beheer van de klant sleutels |
| • Azure Resourceproviders Hallo-versleuteling en ontsleuteling bewerkingen uitvoeren <br> • Microsoft beheert Hallo sleutels <br>• Volledige cloud-functionaliteit | • Azure Resourceproviders Hallo-versleuteling en ontsleuteling bewerkingen uitvoeren<br>• Klant bepaalt sleutels via Azure Sleutelkluis<br>• Volledige cloud-functionaliteit | • Azure Resourceproviders Hallo-versleuteling en ontsleuteling bewerkingen uitvoeren <br>• Klant bepaalt sleutels On-premises <br> • Volledige cloud-functionaliteit| • Azure-services te ontsleutelen gegevens niet zien <br>• Klanten houden van sleutels lokale (of in andere secure winkels). Sleutels zijn niet beschikbaar tooAzure services <br>• Verminderd cloud-functionaliteit|

### <a name="enabling-encryption-at-rest"></a>Codering in rust inschakelen

**Uw gegevens opslaat voor alle locaties te identificeren**

Hallo-doel van versleuteling in rust tooencrypt zijn alle gegevens. In dat geval elimineert Hallo mogelijkheid van belangrijke gegevens of alle persistente locaties ontbreekt. Opsomming van alle gegevens die zijn opgeslagen door uw toepassing. 

> [!Note] 
> Niet alleen 'toepassingsgegevens' of ' PII', maar geen gegevens die verband houden met inbegrip van tooapplication account metagegevens (abonnement toewijzingen van contract info, PII).

Houd rekening met wat u slaat toostore gegevens gebruikt. Bijvoorbeeld:

- Externe opslag (bijvoorbeeld SQL Azure, Document-DB, HDInsights, Data Lake, enz.)

- Tijdelijke opslag (een lokale cache met gegevens van de tenant)

- Cache in het geheugen (in kan worden geplaatst wisselbestand Hallo.)

### <a name="leverage-hello-existing-encryption-at-rest-support-in-azure"></a>Gebruikmaken van bestaande versleuteling Hallo op rest-ondersteuning in Azure

Voor elke store die u gebruikt, gebruikmaken van Hallo bestaande versleuteling op Rest-ondersteuning.

- Azure Storage: Zie [Azure Storage-Service: versleuteling voor gegevens in rust](https://docs.microsoft.com/azure/storage/storage-service-encryption),

- SQL Azure: Zie [transparante gegevensversleuteling (TDE), SQL altijd versleuteld.](https://msdn.microsoft.com/library/mt163865.aspx)

- Virtuele machine en de lokale schijf opslag ([Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption))

Gebruik voor de virtuele machine en lokale schijfopslag Azure Disk Encryption indien ondersteund:

IaaS

Services met IaaS VM's (Windows of Linux) moeten gebruiken [Azure Disk Encryption](https://microsoft.sharepoint.com/teams/AzureSecurityCompliance/Security/SitePages/Azure%20Disk%20Encryption.aspx) tooencrypt volumes met gegevens van de klant.

PaaS-v2

Services die worden uitgevoerd op PaaS-v2 met Service Fabric kunt gebruiken Azure disk encryption voor virtuele-Machineschaalset [VMSS] tooencrypt hun PaaS v2 VM's.

PaaS v1

Azure Disk Encryption is momenteel niet ondersteund voor PaaS v1. Daarom moet u toepassingsniveau versleuteling tooencrypt permanente gegevens in rust.  Dit omvat, maar is niet beperkt tot toepassingsgegevens, tijdelijke bestanden, logboeken en crashdumps.

De meeste services moeten proberen tooleverage Hallo versleuteling van een opslagprovider van de resource. Sommige services hebben toodo expliciete versleuteling, bijvoorbeeld een sleutelmateriaal persistent (certificaten, root / de hoofdsleutel van de sleutels) moeten worden opgeslagen in de Sleutelkluis.

Als u ondersteuning bieden voor versleuteling aan servicezijde met sleutels door de klant beheerd moeten er een toobe een manier voor Hallo klant tooget Hallo sleutel toous. Hallo ondersteund en aan te raden manier toodo door de integratie van Azure van met Azure Key Vault (Sleutelkluis). In dit geval kunnen klanten toevoegen en beheren van de sleutels in Azure Sleutelkluis. Een klant leert u hoe toouse Azure Sleutelkluis via [aan de slag met Sleutelkluis](http://go.microsoft.com/fwlink/?linkid=521402).

toointegrate met Azure Sleutelkluis, voegt u code toorequest een sleutel van Azure Sleutelkluis wanneer deze nodig is voor ontsleuteling.

- Zie [Azure Key Vault – stapsgewijze](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) voor informatie over het toointegrate met Azure Sleutelkluis.

Als u beheer van de klant sleutels ondersteunt, moet u een UX tooprovide voor Hallo klant toospecify die welke toouse Sleutelkluis (of Key Vault URI).

Als u versleuteling in rust omvat het Hallo-versleuteling van host, infrastructuur en tenant-gegevens, kan Hallo verlies van Hallo sleutels vervaldatum toosystem fout of schadelijke activiteiten betekenen alle Hallo versleutelde gegevens niet verloren. Het is daarom essentieel dat de versleuteling op Rest-oplossing heeft een uitgebreid noodherstel artikel robuuste toosystem fouten en schadelijke activiteiten.

Services die versleuteling in rust implementeren zijn doorgaans nog steeds gevoelig toohello versleutelingssleutels of gegevens blijft niet-versleuteld op Hallo hoststation (bijvoorbeeld in Hallo wisselbestand van Hallo hostbesturingssysteem.) Services moeten waarborgen Hallo hostvolume voor hun services is versleuteld. toofacilitate dit Compute-team heeft ingeschakeld Hallo-implementatie van de Host-versleuteling gebruikt [Bitlocker](https://technet.microsoft.com/library/dn306081.aspx) NKP en -extensies toohello DCM-service en agent tooencrypt Hallo hostvolume.

De meeste services worden geïmplementeerd op standaard Azure Virtual machines. Dergelijke services krijgt [Host versleuteling](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) automatisch wanneer Compute ingeschakeld. Voor services die worden uitgevoerd in Compute beheerde clusters host versleuteling automatisch ingeschakeld als Windows Server 2016 is geïmplementeerd.

### <a name="encryption-in-transit"></a>Codering in transit

Beveiligen van gegevens die onderweg moet essentieel onderdeel van uw strategie voor gegevensbescherming. Omdat gegevens heen en weer vanaf verschillende locaties verplaatst, is algemeen aanbeveling Hallo SSL/TLS-protocollen tooexchange gegevens altijd te gebruiken op verschillende locaties. In sommige gevallen kunt u tooisolate Hallo gehele communicatiekanaal tussen uw on-premises en cloud infrastructuur met behulp van een virtueel particulier netwerk (VPN).

Gegevens verplaatsen tussen uw on-premises infrastructuur en Azure, moet u passende beveiligingsmaatregelen zoals HTTPS- of VPN.

Gebruik voor organisaties die toegang vanuit meerdere werkstations zich lokaal tooAzure toosecure nodig, [Azure site-naar-site VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-site-to-site-create).

Voor organisaties die toosecure toegang vanaf één werkstation moeten zich op de lokale tooAzure, gebruik [punt-naar-Site VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-point-to-site-create).

Grotere gegevenssets kan worden verplaatst via een speciale snelle WAN-verbinding, zoals [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Als u ervoor toouse ExpressRoute kiest, kunt u ook gegevens op het niveau van de toepassing met behulp van Hallo Hallo coderen [SSL/TLS](https://support.microsoft.com/kb/257591) of andere protocollen voor extra beveiliging.

Als u met Azure Storage via hello Azure Portal communiceert, worden alle transacties plaatsvinden via HTTPS. [REST API voor Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx) via HTTPS kan ook worden gebruikt toointeract met [Azure Storage](https://azure.microsoft.com/services/storage/) en [Azure SQL Database](https://azure.microsoft.com/services/sql-database/).

Organisaties die niet voldoen aan tooprotect gegevens die onderweg zijn vatbaar voor [man-in-the-middle-aanvallen](https://technet.microsoft.com/library/gg195821.aspx), [afgeluisterd](https://technet.microsoft.com/library/gg195641.aspx), en sessiehijacking. Deze aanvallen kunnen Hallo eerste stap bij het krijgen van toegang tot tooconfidential gegevens zijn.

U kunt meer informatie over Azure VPN-optie Hallo artikel lezen [Planning en ontwerp voor VPN-Gateway](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design).

### <a name="enforce-file-level-data-encryption"></a>Bestand niveau gegevensversleuteling afdwingen

[Azure RMS](https://technet.microsoft.com/library/jj585026.aspx) maakt gebruik van versleuteling, identiteit en verificatie beleid toohelp beveiligen van uw bestanden en e-mail. Azure RMS werkt op meerdere apparaten, telefoons, tablets en pc's voor beveiliging binnen uw organisatie en buiten uw organisatie. Deze mogelijkheid is mogelijk omdat Azure RMS wordt toegevoegd een beveiligingsniveau dat met Hallo gegevens, resteert zelfs wanneer deze de fysieke grenzen van uw organisatie.

Wanneer u uw bestanden tooprotect Azure RMS gebruikt, gebruikt u industriestandaard cryptografie met volledige ondersteuning van [FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/standards.html). Wanneer u Azure RMS-gegevensbeveiliging gebruikmaken, hebt u zelfs als deze gekopieerde toostorage die niet onder het beheer van Hallo Hallo zekerheid dat Hallo beveiliging blijft van toepassing op Hallo-bestand, IT, zoals een cloudopslagservice. Hallo dezelfde vindt plaats voor bestanden die worden gedeeld via e-mail, Hallo-bestand is beveiligd als een bijlage tooan e-mailbericht met instructies hoe tooopen Hallo beveiligde bijlage.
Bij het plannen van de overstap op Azure RMS wordt aangeraden Hallo volgende:

- Hallo installeren [app RMS sharing](https://technet.microsoft.com/library/dn339006.aspx). Deze app kan worden geïntegreerd met Office-toepassingen door installatie van een Office-invoegtoepassing zodat gebruikers kunnen bestanden eenvoudig rechtstreeks beveiligen.

- Configureer toepassingen en services toosupport Azure RMS

- Maak [aangepaste sjablonen](https://technet.microsoft.com/library/dn642472.aspx) die overeenstemming met uw zakelijke vereisten. Bijvoorbeeld: een sjabloon voor bovenste geheime gegevens die moet worden toegepast op alle bovenste geheim gerelateerde e-mailberichten.

Organisaties die zich op zwakke [gegevensclassificatie](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) en bestandsbeveiliging mogelijk vatbaarder toodata lekken. Zonder de juiste Bestandsbeveiliging, geen organisaties kunnen tooobtain worden zakelijke inzichten, controleren op misbruik en te voorkomen dat schadelijke toegang toofiles.

> [!Note]
> U kunt meer informatie over Azure RMS Hallo artikel lezen [aan de slag met Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx).

## <a name="secure-your-application-protect"></a>Beveiligen van uw toepassing (beveiligen)
Hoewel Azure verantwoordelijk is voor het beveiligen van Hallo-infrastructuur en platform dat op uw toepassing wordt uitgevoerd, is uw verantwoordelijkheid toosecure uw toepassing zelf. Met andere woorden, moet u toodevelop, implementeren en beheren van uw toepassingscode en inhoud op een veilige wijze. Zonder deze kunt uw toepassingscode of inhoud nog steeds kwetsbaar toothreats.

### <a name="web-application-firewall-waf"></a>Web Application Firewall (WAF)
[Web application firewall (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) is een functie van [Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) die biedt gecentraliseerd beveiliging van uw webtoepassingen van algemene aanvallen en beveiligingsproblemen.

Web application firewall is gebaseerd op regels uit Hallo [regelsets voor OWASP core](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) 3.0 of 2.2.9. Webtoepassingen zijn in toenemende mate het doel van aanvallen die gebruikmaken van veelvoorkomende bekende beveiligingsproblemen. Algemene tussen deze aanvallen zijn SQL-injectieaanvallen, tooname enkele cross-site scripting aanvallen. Zo wordt voorkomen dat dergelijke aanvallen in toepassingscode kan lastig zijn en vereisen mogelijk strengere onderhoud, patchen en de controle op meerdere lagen van Hallo Toepassingstopologie. Een gecentraliseerde web application firewall zorgt er beveiligingsbeheer veel eenvoudiger en biedt betere zekerheid tooapplication beheerders tegen bedreigingen of beveiligingsrisico's. Een WAF oplossing kan ook beveiligingsrisico tooa sneller reageren door een bekend beveiligingsprobleem met een centrale locatie en beveiliging van elk van de afzonderlijke webtoepassingen patchen. Bestaande toepassingsgateways kunnen eenvoudig toepassingsgateway voor geconverteerde tooa web application firewall is ingeschakeld worden.

Aantal Hallo veelvoorkomende web beveiligingslekken welke web application firewall wordt beschermd tegen omvat:

- Beveiliging tegen SQL-injecties

- Beveiliging tegen scripting op meerdere sites

- Beveiliging tegen veelvoorkomende aanvallen via internet, zoals opdrachtinjectie, het smokkelen van HTTP-aanvragen, het uitsplitsen van HTTP-antwoorden en aanvallen waarbij een extern bestand wordt ingesloten

- Beveiliging tegen schendingen van het HTTP-protocol

- Beveiliging tegen afwijkingen van het HTTP-protocol, zoals een gebruikersagent voor de host en Accept-headers die ontbreken

- Beveiliging tegen bots, crawlers en scanners

- Detectie van veelvoorkomende onvolkomenheden in toepassing (dat wil zeggen, Apache, IIS, enz.)

> [!Note]
> Voor een gedetailleerde lijst met regels en hun beschermingsmaatregelen Zie Hallo volgende [regelsets Core](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview#core-rule-sets):

Azure biedt ook diverse functies eenvoudig te gebruiken toohelp beveiliging van binnenkomend en uitgaand verkeer voor uw app. Azure ook helpt klanten hun toepassingscode beveiligen doordat extern opgegeven functionaliteit tooscan uw webtoepassing op beveiligingsproblemen.

- [Beveiligen van uw web-app met behulp van verschillende middelen van verificatie en autorisatie](https://docs.microsoft.com/azure/app-service-web/web-sites-authentication-authorization)

    - [Azure Active Directory-verificatie voor uw app instellen](https://azure.microsoft.com/blog/azure-websites-authentication-authorization/)


- [App voor verkeer tooyour beveiligen doordat Transport Layer Security (TLS/SSL) - HTTPS](https://docs.microsoft.com/azure/app-service-web/web-sites-configure-ssl-certificate)

    - [Alle binnenkomend verkeer via HTTPS-verbinding afdwingen](http://microsoftazurewebsitescheatsheet.info/)

  - [Strikte transportbeveiliging (HSTS) inschakelen](http://microsoftazurewebsitescheatsheet.info/#enable-http-strict-transport-security-hsts)


- [Toegang tooyour app beperken door IP-adres van client](http://microsoftazurewebsitescheatsheet.info/#filtering-traffic-by-ip)

- [Toegang tooyour app beperken door van client probleem - frequentie van de aanvraag en gelijktijdigheid van taken](http://microsoftazurewebsitescheatsheet.info/#dynamic-ip-restrictions)

- [Scannen van uw web-app-code voor beveiligingsproblemen met behulp van Tinfoil Security Scanning](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/)

- [TLS wederzijdse verificatie toorequire client certificaten tooconnect tooyour web-app configureren](https://docs.microsoft.com/azure/app-service-web/app-service-web-configure-tls-mutual-auth)

- [Een clientcertificaat configureren voor gebruik van uw app toosecurely tooexternal resources verbinden met](https://azure.microsoft.com/blog/using-certificates-in-azure-websites-applications/)

- [Standard van SQL server-headers tooavoid's van uw app fingerprinting verwijderen](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/)

- [Uw app veilig verbinding kunnen maken met resources in een particulier netwerk met punt-naar-Site VPN](https://docs.microsoft.com/azure/app-service-web/web-sites-integrate-with-vnet)

- [Uw app veilig verbinding kunnen maken met resources in een particulier netwerk met behulp van hybride verbindingen](https://docs.microsoft.com/azure/app-service-web/web-sites-hybrid-connection-get-started)

Maakt gebruik van Azure App Service Hallo dezelfde antimalwareoplossing uit die worden gebruikt door Azure Cloud Services en virtuele Machines. toolearn meer informatie over dit verwijzen tooour [Antimalware documentatie](https://docs.microsoft.com/azure/security/azure-security-antimalware).

## <a name="secure-your-network-protect"></a>Beveiliging van uw netwerk (beveiligen)
Microsoft Azure omvat een robuuste netwerken infrastructuur toosupport uw toepassing en de vereisten voor service-connectiviteit. Netwerkverbinding is tussen de bronnen in Azure, tussen on-premises en Azure gehoste bronnen, en tooand van Hallo Internet en Azure.

Hallo [Azure netwerkinfrastructuur](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines) schakelt u toosecurely verbinding maken met andere Azure-resources tooeach [virtuele netwerken (vnet's)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview). Een VNet is een weergave van uw eigen netwerk in Hallo cloud. Een VNet is een logische isolatie van hello Azure-cloud netwerk toegewezen tooyour abonnement. U kunt VNets tooyour on-premises netwerken kunt verbinden.

![Beveiliging van uw netwerk (beveiligen)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig6.png)

Als u Basisnetwerk toegangsbeheer op gebruikersniveau moet (op basis van IP-adres en Hallo TCP of UDP-protocollen), dan kunt u [Netwerkbeveiligingsgroepen](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg). Een Netwerkbeveiligingsgroep (NSG) is een eenvoudige filterregels voor pakketten firewall en zorgt ervoor dat u toocontrol toegang op basis van een [5-tuple](https://www.techopedia.com/definition/28190/5-tuple).

Azure-netwerken ondersteunt Hallo mogelijkheid toocustomize Hallo routeringsgedrag voor netwerkverkeer op uw virtuele netwerken van Azure. U kunt dit doen door het configureren van [zelfgedefinieerde Routes](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) in Azure.

[Geforceerde tunneling](https://www.petri.com/azure-forced-tunneling) is een mechanisme kunt u tooensure die uw services niet zijn toegestaan tooinitiate een toodevices verbinding op Hallo Internet.

Azure ondersteunt toegewezen WAN-koppeling connectiviteit tooyour on-premises netwerk en een Azure-netwerk met [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction). Hallo koppeling tussen Azure en uw site maakt gebruik van een speciale verbinding die verloopt niet Hallo via openbaar Internet. Als uw Azure-toepassing wordt uitgevoerd in meerdere datacenters, kunt u [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) tooroute aanvragen van gebruikers op intelligente wijze over exemplaren van de toepassing hello. U kunt ook verkeer tooservices niet wordt uitgevoerd in Azure als ze toegankelijk vanaf Internet Hallo zijn versturen.

## <a name="virtual-machine-security-protect"></a>Beveiliging van de virtuele machine (beveiligen)

[Virtuele Machines in Azure](https://docs.microsoft.com/azure/virtual-machines/) kunt u een breed scala aan oplossingen computergebruik in een flexibele manier te implementeren. Met ondersteuning voor Microsoft Windows, Linux, Microsoft SQL Server, Oracle, IBM, SAP en Azure BizTalk Services kunt u elke workload en elke taal implementeren op vrijwel elk besturingssysteem.

Met Azure, kunt u [antimalwaresoftware](https://docs.microsoft.com/azure/security/azure-security-antimalware) van beveiliging leveranciers zoals Microsoft, Symantec, Trend Micro en Kaspersky tooprotect uw virtuele machines van schadelijke bestanden, adware en andere dreigingen.

Microsoft Antimalware voor Azure Cloud Services en virtuele Machines is een functie real-timebeveiliging die helpt bepalen en virussen, spyware en andere schadelijke software verwijderen. Microsoft Antimalware biedt configureerbare waarschuwingen wanneer bekende schadelijke of ongewenste software probeert tooinstall zelf of uit te op uw Azure-systemen voeren.

[Azure Backup](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) is een schaalbare oplossing die uw toepassingsgegevens met nul investeringen en minimale beschermt bedrijfskosten. Toepassingsfouten kunnen uw gegevens beschadigen, en menselijke fouten kunnen fouten introduceren in uw toepassingen. Uw virtuele machines met Windows en Linux zijn beveiligd met Azure Backup.

[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) helpt bij het indelen replicatie, failovers en herstel van workloads en apps, zodat ze beschikbaar vanaf een secundaire locatie zijn als uw primaire locatie uitvalt.

## <a name="ensure-compliance-cloud-services-due-diligence-checklist-protect"></a>Naleving: Cloudservices vanwege toewijding inzetten Controlelijst (beveiligen)

Microsoft heeft ontwikkeld [Hallo Cloud-Services vanwege toewijding inzetten controlelijst](https://aka.ms/cloudchecklist.download) toohelp organisaties oefenen vanwege toewijding inzetten als ze een verplaatsen toohello cloud overwegen. Dit biedt een structuur voor een organisatie met een grootte en het type: persoonlijke bedrijven en organisaties van openbare-sector, met inbegrip van de overheid op alle niveaus en non-profitorganisaties: tooidentify hun eigen prestaties, service, beheer en toezicht doelstellingen en vereisten. Hierdoor kunnen ze toocompare Hallo aanbiedingen van andere cloudserviceproviders, uiteindelijk die Hallo basis voor een cloud-serviceovereenkomst.

Hallo controlelijst biedt een framework dat component door component met een nieuwe internationale standaard voor cloud serviceovereenkomsten, ISO/IEC 19086 wordt uitgelijnd. Deze standaard biedt een consistente verzameling overwegingen voor organisaties toohelp nemen van beslissingen over de acceptatie van de cloud, en een compleet gemeenschappelijke voor het vergelijken van serviceaanbiedingen cloud maken.

Hallo controlelijst bijdraagt aan een grondig gerenommeerde verplaatsen toohello cloud, bieden gestructureerde richtlijnen en een consistente, herhaalbare aanpak voor het kiezen van een cloud-serviceprovider.

Acceptatie van de cloud is niet langer gewoon een beslissing technologie. Omdat controlelijst vereisten touch op elk aspect van een organisatie, ze bedienen tooconvene alle belangrijke interne-besluitvormers: hello CIO en CISO evenals juridische, bestaat de kans dat professionals beheer- en inkoop en naleving. Dit verhoogt de efficiëntie van Hallo van Hallo besluitvormingsproces en compleet beslissingen ten aanzien van geluid redeneren, waardoor de kans op Hallo van tooadoption onvoorziene problemen.

Bovendien Hallo Controlelijst:

- Beschrijft de bespreking van de belangrijkste onderwerpen voor besluitvormers aan Hallo begin van overstapproces voor Hallo cloud.

- Biedt ondersteuning voor uitgebreide zakelijke discussies over voorschriften en Hallo van organisatie doelstellingen voor privacy, persoonsgegevens (PII) en beveiliging van gegevens.

- Helpt organisaties bij potentiële problemen die invloed kunnen zijn op een cloudproject op te sporen.

- Biedt een consistente set vragen Hello dezelfde voorwaarden, definities, metrische gegevens en producten voor elke provider, toosimplify Hallo proces waarbij de offerings van andere cloudserviceproviders worden vergeleken.

## <a name="azure-infrastructure-and-application-security-validation-detect"></a>Azure-infrastructuur en toepassing beveiligingsvalidatie (detecteren)

[Azure bedrijfsbeveiliging](https://docs.microsoft.com/azure/security/azure-operational-security) toohello services, besturingselementen en functies beschikbaar toousers verwijst voor het beveiligen van hun gegevens, toepassingen en andere elementen in Microsoft Azure.

![mislukte beveiligingsvalidaties (detecteren)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig7.png)

Azure operationele beveiliging is gebaseerd op een framework dat Hallo kennis die is opgedaan met een verschillende mogelijkheden die de unieke tooMicrosoft, met inbegrip van Microsoft Security Development Lifecycle (SDL), Microsoft Security Response Centre Hallo Hallo zijn opgenomen programma en grondige kennis van Hallo cybersecurity threat Liggend.

### <a name="microsoft-operations-management-suiteoms"></a>Microsoft operations management suite(OMS)

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) Hallo IT beheeroplossing voor Hallo hybride cloud is. Alleen wordt gebruikt of uw bestaande System Center-implementatie, OMS biedt u tooextend Hallo maximale flexibiliteit en beheer voor cloud-gebaseerde beheer van uw infrastructuur.

![Microsoft operations management suite(OMS)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig8.png)

Met OMS, kunt u een instantie in een cloud, met inbegrip van lokale, Azure, AWS, Windows Server, Linux, VMware en OpenStack, tegen lagere kosten dan concurrerende oplossingen beheren. Gebouwd voor Hallo cloud eerste wereld, biedt OMS een nieuwe benadering toomanaging uw onderneming die Hallo snelste, meest rendabele manier toomeet nieuwe zakelijke uitdagingen en geschikt voor de nieuwe werkbelastingen, toepassingen en cloudomgevingen.

### <a name="log-analytics"></a>Log Analytics

[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) biedt bewakingsservices voor OMS door in een centrale opslagplaats gegevens te verzamelen van beheerde resources. Deze gegevens kan bevatten gebeurtenissen, prestatiegegevens of aangepaste worden geleverd via Hallo API. Zodra verzameld, zijn Hallo gegevens beschikbaar voor waarschuwingen, analyse en exporteren.

![Log Analytics](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig9.png)

Deze methode kunt u tooconsolidate gegevens uit diverse bronnen, zodat u kunt combineren gegevens van uw Azure-services met uw bestaande lokale omgeving. Ook duidelijk scheidt u Hallo verzamelen van gegevens van de Hallo van Hallo actie op die van die gegevens, zodat alle acties beschikbaar tooall soorten gegevens zijn.

### <a name="azure-security-center"></a>Azure security center

[Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) helpt u te voorkomen, detecteren, en toothreats reageren met een verhoogde zichtbaarheid van en controle over Hallo beveiliging van uw Azure-resources. Het biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen, helpt bedreigingen te detecteren die anders onopgemerkt zouden blijven, en werkt met een uitgebreid ecosysteem van beveiligingsoplossingen.

Security Center analyseert de beveiligingsstatus Hallo van uw Azure-resources tooidentify mogelijke beveiligingsproblemen. Een lijst met aanbevelingen begeleidt u bij het Hallo-proces voor het configureren van benodigde besturingselementen.

Voorbeelden zijn:

- Inrichting van antimalware toohelp identificeren en verwijderen van schadelijke software

- Network security groepen en regels toocontrol tooVMs verkeer configureren

- Inrichting van web application firewalls toohelp beschermen tegen aanvallen die zijn gericht op uw webtoepassingen

- Implementatie van ontbrekende systeemupdates

- Aanpassing van besturingssysteemconfiguraties die niet overeenkomen met de Hallo aanbevolen basislijnen

Security Center automatisch verzamelt, analyseert en integreert logboekgegevens van uw Azure-resources, het Hallo-netwerk en partneroplossingen zoals antimalwareprogramma's en firewalls. Wanneer er dreigingen worden gedetecteerd, wordt een beveiligingswaarschuwing gemaakt. Voorbeelden zijn detectie van:

- Verdachte VM's die communiceren met bekende schadelijke IP-adressen

- Geavanceerde malware die is gedetecteerd met Windows Foutrapportage

- Beveiligingsaanvallen op virtuele machines

- Beveiligingswaarschuwingen van geïntegreerde antimalwareprogramma's en firewalls

### <a name="azure-monitor"></a>Monitor voor Azure

[Monitor voor Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) aanwijzers tooinformation biedt op specifieke typen resources. Biedt visualisatie, query routering, waarschuwingen, automatisch schalen en automatisering op gegevens van hello Azure-infrastructuur (activiteitenlogboek) en elke afzonderlijke Azure-resource (diagnostische logboeken).

Cloud-toepassingen zijn complexe met veel bewegende onderdelen. Monitoring biedt gegevens tooensure die uw toepassing up blijft en wordt uitgevoerd in een foutloze toestand bevindt. Ook kunt u toostave potentiële problemen uitgeschakeld of het oplossen van het verleden zijn.

![Monitor voor Azure](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig10.png) Bovendien kunt u bewaking gegevens toogain uitgebreide statistieken over uw toepassing. Deze kennis kan u helpen de prestaties van toepassingen tooimprove of onderhoud of acties die anders worden handmatige interventie moeten automatiseren.

Controle van de netwerkbeveiliging van uw is het essentieel zijn voor netwerk beveiligingsproblemen detecteren en de naleving van uw IT-beveiliging en regelgeving governance model. Overzicht van de beveiligingsgroep, kunt u Hallo geconfigureerd Netwerkbeveiligingsgroep en beveiliging regels ophalen, evenals Hallo effectieve beveiligingsregels voor verbindingen. Hallo-lijst met regels die zijn toegepast, kunt u bepalen Hallo-poorten die geopend zijn en ss beveiligingsproblemen van het netwerk.

### <a name="network-watcher"></a>Netwerk-watcher

[Netwerk-Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) is een regionale service waarmee u toomonitor en onderzoeken van de voorwaarden op het netwerkniveau van een in, naar en van Azure. Netwerkcontrole en visualisatie hulpprogramma's beschikbaar met de netwerk-Watcher kunnen u begrijpen, diagnoses stellen en krijgen insights tooyour netwerk in Azure. Deze service omvat pakketopname, volgende hop, IP-stroom controleren, groep beveiligingsweergave, NSG stroom Logboeken. Scenario niveau bewaking biedt een end-tooend-weergave van netwerkbronnen in contrast tooindividual resource netwerkbewaking.

### <a name="storage-analytics"></a>Opslaganalyses

[Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) metrische gegevens die samengevoegde statistieken en capaciteit transactiegegevens over aanvragen tooa storage-service zijn kan opslaan. Transacties worden gerapporteerd zowel niveau van de bewerking Hallo API, evenals op niveau van de opslag van Hallo en capaciteit op Hallo opslag serviceniveau wordt gerapporteerd. Metrische gegevens kunt gebruikte tooanalyze service opslaggebruik, vaststellen van problemen met aanvragen tegen Hallo storage-service en tooimprove Hallo prestaties van toepassingen die gebruikmaken van een service.

### <a name="application-insights"></a>Application insights

[Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) is een uitbreidbaar Management APM (Application Performance)-service voor webontwikkelaars op meerdere platforms. Gebruik deze toomonitor uw live-webtoepassing. Afwijkende prestaties worden automatisch gedetecteerd. Dit omvat krachtige analytics extra toohelp onderzoeken van problemen en toounderstand wat gebruikers met uw app doen. Het ontworpen toohelp u continu prestaties en bruikbaarheid verbeteren. De Tool werkt voor apps gehost op een groot aantal verschillende platforms, waaronder .NET, Node.js en J2EE, lokaal of in de cloud Hallo. Het kan worden geïntegreerd met uw devOps-proces en verbinding punten tooa verschillende ontwikkelingsprogramma's heeft.

Met deze service kunt u het volgende controleren:

- **Aantal aanvragen, reactietijden en foutpercentages** - ga na welke pagina's het populairst zijn op welke tijdstippen van de dag en waar uw gebruikers zich bevinden. Ontdek welke pagina's het beste presteren. Als uw reactietijden en foutpercentages omhoog gaan wanneer er meer aanvragen binnenkomen, hebt u mogelijk te weinig resources.

- **Aantal afhankelijkheidsrelaties, reactietijden en foutpercentages** - controleer of externe services zorgen voor vertraging.

- **Uitzonderingen** - analyseren Hallo geaggregeerd statistieken, of Kies specifieke exemplaren en inzoomen Hallo stacktracering en verwante aanvragen. Zowel server- als browseruitzonderingen worden gerapporteerd.

- **Paginaweergaven en de prestaties bij het laden van pagina’s** - deze gegevens worden gerapporteerd door de browsers van uw gebruikers.

- **AJAX-aanroepen van webpagina's** -tarieven responstijden en uitvalpercentage.

- **Gebruikers- en sessiegegevens telt.**

- **Prestatiemeteritems** van uw Windows- of Linux-servers, zoals die voor CPU-, geheugen- en netwerkgebruik.

- **Diagnostische gegevens van hosts** van Docker of Azure.

- **Diagnostische traceerlogboeken** van uw app - met behulp hiervan kunt u de samenhang vaststellen tussen traceergebeurtenissen en aanvragen.

- **Aangepaste gebeurtenissen en metrische gegevens** zelf in Hallo client of server code tootrack zakelijke gebeurtenissen zoals verkochte artikelen of games gewonnen te schrijven.
Hallo-infrastructuur voor uw toepassing wordt normaal gesproken bestaat uit veel onderdelen, zoals een virtuele machine, storage-account en virtueel netwerk of een web-app, database, databaseserver en 3e services van derden. Deze onderdelen moet u niet zien als afzonderlijke entiteiten, maar als onderdelen die één entiteit vormen en aan elkaar zijn gerelateerd en afhankelijk zijn van elkaar. U wilt dat toodeploy, beheren en ze als een groep te controleren. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) kunt u toowork met Hallo resources in uw oplossing als een groep.

U kunt implementeren, bijwerken of verwijderen van alle Hallo resources voor uw oplossing in een enkele, gecoördineerde bewerking. Voor implementatie gebruikt u een sjabloon. Deze sjabloon kan voor verschillende omgevingen worden gebruikt, zoals testen, faseren en productie. Resource Manager biedt beveiliging, controle en functies toohelp tagging u uw resources beheren na implementatie.

**Hallo voordelen van het gebruik van Resource Manager**

Resource Manager biedt diverse voordelen:

- U kunt implementeren, beheren en bewaken van alle Hallo resources voor uw oplossing als een groep in plaats van deze resources afzonderlijk te verwerken.

- U kunt herhaaldelijk implementeren van uw oplossing gedurende de ontwikkelingscyclus Hallo en erop vertrouwen dat uw resources worden geïmplementeerd in een consistente status.

- U kunt uw infrastructuur beheren via declaratieve sjablonen in plaats van scripts.

- U kunt Hallo afhankelijkheden tussen resources, zodat deze zijn geïmplementeerd in de juiste volgorde Hallo definiëren.

- Omdat op rollen gebaseerde toegangsbeheer (RBAC) is geïntegreerd in het beheerplatform hello, kunt u access control-tooall services toepassen in de resourcegroep.

- U kunt tags toepassen tooresources toologically organiseren alle Hallo resources in uw abonnement.

- U kunt facturering voor uw organisatie verduidelijken door het bekijken van de kosten voor een groep resources delen dezelfde tag Hallo.

> [!Note]
> Resource Manager biedt een nieuwe manier toodeploy en beheren van uw oplossingen. Als u hebt gebruikt eerdere implementatiemodel Hallo en toolearn over Hallo wijzigingen, Zie [Understanding Resource Manager-implementatie en klassieke implementatie](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model).

## <a name="next-steps"></a>Volgende stappen

Meer informatie over beveiliging door het lezen van enkele van de onderwerpen over onze uitgebreide beveiliging:

- [Controle en logboekregistratie](https://www.microsoft.com/en-us/trustcenter/security/auditingandlogging)

- [Cybercriminaliteit](https://www.microsoft.com/en-us/trustcenter/security/cybercrime)

- [Ontwerp- en operationele beveiliging](https://www.microsoft.com/en-us/trustcenter/security/designopsecurity)

- [Versleuteling](https://www.microsoft.com/en-us/trustcenter/security/encryption)

- [Identiteits-en toegang](https://www.microsoft.com/en-us/trustcenter/security/identity)

- [Netwerkbeveiliging](https://www.microsoft.com/en-us/trustcenter/security/networksecurity)

- [Beveiligingsbeheer](https://www.microsoft.com/en-us/trustcenter/security/threatmanagement)
