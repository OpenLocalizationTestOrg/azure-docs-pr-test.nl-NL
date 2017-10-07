---
title: aaaExtending cloud mogelijkheden tooWindows 10 apparaten via Azure Active Directory Join | Microsoft Docs
description: Biedt een gedetailleerd overzicht van hoe Windows 10-apparaten van Azure AD Join tooget op Azure Active Directory geregistreerd gebruikmaken kunnen.
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 0cd4942f-7d54-474e-bd12-8e6764b0d42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: db9ae9caeb3951d1fdd1d2477827012fd10ace60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="extending-cloud-capabilities-toowindows-10-devices-through-azure-active-directory-join"></a>Cloud-mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join uitbreiden
## <a name="what-is-azure-active-directory-join"></a>Wat is Azure Active Directory Join?
Azure Active Directory Join (Azure AD Join) is Hallo-functionaliteit die een apparaat in bedrijfseigendom in Azure Active Directory tooenable gecentraliseerd beheer van Hallo apparaat registreert. Maakt het mogelijk voor gebruikers, zoals werknemers en studenten tooconnect toohello enterprise cloud via Azure Active Directory. Hierdoor kunnen vereenvoudigde implementaties van Windows en toegang tooorganizational apps en resources van een Windows-apparaat, beide Bedrijfseigendom en persoonlijke (BYOD).

Azure AD Join is bedoeld voor ondernemingen die eerste/cloud-cloudconfiguratie zijn--doorgaans kleine en middelgrote bedrijven die geen een on-premises Windows Server Active Directory-infrastructuur. Dat genoemde, Azure AD Join kan en ook worden gebruikt door grote organisaties op apparaten die niet in staat van de traditionele domein (bijvoorbeeld mobiele apparaten) of voor gebruikers die voornamelijk tooaccess Office 365 of andere geïntegreerd met Azure AD SaaS-apps nodig zijn.

Hoewel Hallo traditionele domein biedt nog steeds Hallo best lokale-ervaring op apparaten die kunnen lid worden van domein, koppelen aan Azure AD is geschikt voor apparaten die niet aan domein toevoegen. Azure AD Join is ook geschikt is voor het beheren van gebruikers in de cloud Hallo. Dit gebeurt met mogelijkheden voor mobile device management in plaats van via traditionele domein beheerprogramma's zoals Groepsbeleid en System Center Configuration Manager (SCCM).

![Overzicht van de apparaten het bedrijf en persoonlijke apparaten met de lokale Active Directory en Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-overview.png)

## <a name="why-should-enterprises-adopt-azure-ad-join"></a>Waarom moeten ondernemingen vast Azure AD Join
* **Bedrijven die grotendeels in de cloud Hallo**: als u hebt verplaatst of tooa model waarin u vermindert de footprint van uw lokale en u wilt meer in de cloud Hallo toooperate verplaatst, Azure AD Join kan voordelen. Mogelijk hebt u Azure AD-accounts handmatig of via het synchroniseren van uw lokale Active Directory gemaakt. In beide gevallen moet u een account hebben in Azure AD en kunt u deze toosign in tooWindows 10. Uw gebruikers kunnen hun computers tooAzure AD via beide Hallo out-of-box experience (OOBE) of via het menu Hallo-instellingen toevoegen. Na toevoeging aan, kunnen profiteren van eenmalige aanmelding (SSO) toegang tot toocloud bronnen zoals Office 365 in hun browser of in de Office-toepassingen.
* **Onderwijsinstellingen**: een Hallo-scenario's die we vaak gehoord is dat onderwijsinstellingen twee gebruikerstypen: onderwijsmedewerkers en studenten. Onderwijsmedewerkers leden worden beschouwd als van langere leden van de organisatie hello, waardoor on-premises-accounts maken voor deze wenselijk is. Maar studenten korterlopende lid zijn van de organisatie Hallo en dus kunnen worden beheerd in Azure AD. Dit betekent dat directory scale kan worden geactiveerd toohello cloud in plaats van lokaal opgeslagen. Het betekent ook dat studenten kunnen tooWindows met hun Azure AD-accounts aanmelden en toegang tooOffice 365 bronnen, in de browser of in de Office-toepassingen krijgen.
* **Bedrijven Retail**: een ander scenario ons bekend van klanten hun behoefte toomanage seizoensgebonden werknemers eenvoudiger is.  Accounts voor langere termijn, fulltime werknemers worden opnieuw, meestal gemaakt als op een lokale accounts op domein-machines. Maar seizoensgebonden werknemers korterlopende lid zijn van Hallo org, dus is het wenselijk toomanage ze waar gebruikerslicenties kunnen eenvoudiger kan worden verplaatst om. Deze gebruikersaccounts maakt in de cloud met Office 365-licenties Hallo, Hallo gebruikers tooget Hallo voordelen van aanmelding tooWindows en Office-toepassingen met een Azure AD-account. Ondertussen u meer flexibiliteit met de licenties worden onderhouden nadat ze verlaten.
* **Andere bedrijven**: zelfs als u gebruikers in uw lokale Active Directory onderhoudt, kunt u nog steeds profiteren van dat gebruikers worden toegevoegd met Azure AD. Dat komt doordat Azure AD biedt een vereenvoudigde gekoppelde ervaring, efficiënte Apparaatbeheer, inschrijving voor beheer van automatische mobiele apparaten en mogelijkheden voor eenmalige aanmelding voor Azure AD en on-premises resources.  

## <a name="what-capabilities-does-azure-ad-join-offer"></a>Welke mogelijkheden biedt Azure AD Join?
Met Azure AD Join krijgt u de volgende Hallo:

* **Automatisch inrichten van apparaten in Bedrijfseigendom**: met Windows 10, gebruikers kunnen configureren voor een nieuwe, krimp apparaat Hallo out-of-box experience zonder tussenkomst van de IT.
* **Ondersteuning voor moderne vormfactoren**: koppelen aan Azure AD werkt op apparaten waarvoor geen Hallo traditionele domein deelnemen aan mogelijkheden.  
* **Ondersteuning voor bestaande organisatieaccounts**: gebruikers niet langer moet toocreate en onderhouden van een een persoonlijk Microsoft-account tooget Hallo beste ervaring op bedrijf uitgegeven apparaten, zoals met Windows 8. Ze kunnen hun bestaande werkaccount in plaats daarvan gebruiken in Azure AD. Voor veel organisaties dit in feite betekent dat gebruikers kunnen instellen en meld u aan tooWindows Hello dezelfde referenties die ze tooaccess Office 365 gebruiken.
* **Inschrijving van automatische mobiele apparaten management**: apparaten kunnen automatisch worden geregistreerd in het beheer van mobiele apparaten wanneer verbonden tooAzure AD. Dit proces werkt met Microsoft Intune en partner beheeroplossingen voor mobiele apparaten. Als het beheer van apparaten met Intune is voltooid, IT-beheerders kunnen monitor/Azure die lid zijn van AD apparaten beheren naast domeinapparaten Hallo SCCM-beheerconsole.
* **Eenmalige aanmelding toocompany resources**: Profiteer van gebruikers eenmalige aanmelding van Hallo Windows desktop tooapps en bronnen in Hallo cloud, zoals Office 365 en duizenden business-toepassingen die afhankelijk van Azure AD voor verificatie via zijn[Azure AD Connect](active-directory-azureadjoin-deployment-aadjoindirect.md). Apparaten in Bedrijfseigendom die gekoppeld tooAzure AD zijn Profiteer ook eenmalige aanmelding tooon lokale bronnen wanneer Hallo-apparaat is op een bedrijfsnetwerk en vanaf elke locatie wanneer deze resources beschikbaar worden gesteld via Hallo [Azure AD-toepassingsproxy](https://msdn.microsoft.com/library/azure/Dn768219.aspx).
* **OS State Roaming**: toegankelijkheidsinstellingen, websites, Wi-Fi-wachtwoorden en andere instellingen worden gesynchroniseerd tussen de apparaten in Bedrijfseigendom zonder een persoonlijk Microsoft-account.
* **Enterprise-ready Windows Store**: Hallo Windows Store ondersteunt app overname en licentieverlening met Azure AD-accounts. Organisaties kunnen volumelicentie-apps en zodat ze beschikbaar toohello gebruikers in hun organisatie.

## <a name="how-do-different-devices-work-with-azure-ad-join"></a>Hoe verschillende apparaten werkt met Azure AD Join?
| Bedrijfsapparaten (gekoppelde tooon lokale domein) | Bedrijfsapparaten (gekoppelde toohello cloud) | Persoonlijk apparaat |
| --- | --- | --- |
| Kunnen gebruikers zich aanmelden in Windows met werkreferenties (zoals ze vandaag doen). |Kunnen gebruikers zich aanmelden in tooWindows met zakelijke referenties die worden beheerd in Azure AD. Dit is van belang voor zakelijke apparaten in drie gevallen: <ol><li>Hallo organisatie heeft geen on-premises (bijvoorbeeld een klein bedrijf) Active Directory.</li><li>Hallo organisatie alle gebruikersaccounts in Active Directory niet maken (bijvoorbeeld gebruikersaccounts voor studenten, adviseurs of seizoensgebonden werknemers worden gemaakt in Active Directory).</li><li>Hallo organisatie heeft zakelijke apparaten die niet lid tooan (lokale)-domein, zoals telefoons of tablets met een mobiele-SKU (bijvoorbeeld een secundair apparaat genomen tooa factory/retail verdieping).</li></ol> Azure AD Join ondersteunt het verbinden van apparaten voor zowel beheerde als federatieve organisaties het bedrijf. |Gebruikers zich aanmelden tooWindows met hun persoonlijke Microsoft-accountreferenties (geen wijzigen). |
| Gebruikers hebben toegang tooroaming instellingen en Hallo enterprise, Windows Store. Deze services werkt met werkaccounts en een persoonlijk Microsoft-account niet vereist. Hiervoor moet de lokale Active Directory tooAzure AD tooconnect organisaties. |Setup selfservice u kunt doen. Ze kunnen doorlopen Hallo eerste sessie (FRX) via zijn werkaccount als een alternatieve toohaving IT apparaten inrichten hello, hoewel beide methoden worden ondersteund. |Gebruikers kunnen eenvoudig met het toevoegen van een werkaccount dat wordt beheerd in Active Directory of Azure AD. |
| Gebruikers hebben de mogelijkheid voor SSO van hello bureaublad toowork apps, websites en bronnen--waaronder zowel lokale bronnen en cloud-apps die Azure AD voor verificatie gebruiken. |Apparaten worden automatisch geregistreerd bij Hallo enterprise directory (Azure AD) en automatisch bij het beheer van mobiele apparaten geregistreerd. (Azure AD Premium-functie). |Gebruikers hebben de mogelijkheid voor eenmalige aanmelding via apps en toowebsites/resources aan dit werkaccount. |
| Gebruikers kunnen toevoegen hun persoonlijke Microsoft-accounts tooaccess hun eigen foto's en bestanden zonder enige impact op Ondernemingsgegevens. (Instellingen zwervend doorgaan toowork met hun werkaccount). Hallo Microsoft-account kunt van eenmalige aanmelding en niet langer stations Hallo roaming van instellingen. |U kunt doen een selfservice voor wachtwoordherstel (SSPR) op winlogon, wat betekent dat ze een vergeten wachtwoord opnieuw kunnen instellen. (Azure AD Premium-functie). |Gebruikers hebben toegang tot toohello enterprise Windows Store, zodat ze kunnen verkrijgen en line-of-business-apps op hun persoonlijke apparaten gebruiken. |

## <a name="additional-information"></a>Aanvullende informatie
* [Windows 10 voor Hallo ondernemingen: manieren toouse apparaten for work.](active-directory-azureadjoin-windows10-devices-overview.md)
* [Cloud-mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join uitbreiden](active-directory-azureadjoin-user-upgrade.md)
* [Identiteiten zonder wachtwoorden via Microsoft Passport verifiëren](active-directory-azureadjoin-passport.md)
* [Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)
* [Verbinding maken met domein apparaten tooAzure AD voor Windows 10-ervaring](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD Join instellen](active-directory-azureadjoin-setup.md)

