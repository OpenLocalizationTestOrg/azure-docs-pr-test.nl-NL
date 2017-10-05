---
title: Cloudfunctionaliteit uitbreiden naar Windows 10-apparaten via Azure Active Directory Join | Microsoft Docs
description: Biedt een gedetailleerd overzicht van hoe Windows 10-apparaten kunnen gebruikmaken van Azure AD Join ophalen op Azure Active Directory geregistreerd.
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
ms.openlocfilehash: d3a3d3efe1c43caff3b8d2956c14e8c90d05d22b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="extending-cloud-capabilities-to-windows-10-devices-through-azure-active-directory-join"></a>Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join (Engelstalig)
## <a name="what-is-azure-active-directory-join"></a>Wat is Azure Active Directory Join?
Azure Active Directory Join (Azure AD Join) is de functionaliteit waarmee een apparaat in bedrijfseigendom in Azure Active Directory inschakelen gecentraliseerd beheer van het apparaat wordt geregistreerd. Maakt het mogelijk voor gebruikers, zoals werknemers en studenten verbinding maken met de enterprise cloud via Azure Active Directory. Hierdoor kunnen vereenvoudigde implementaties van Windows en toegang tot de organisatie-apps en resources vanaf elk apparaat met Windows, beide Bedrijfseigendom en persoonlijke (BYOD).

Azure AD Join is bedoeld voor ondernemingen die eerste/cloud-cloudconfiguratie zijn--doorgaans kleine en middelgrote bedrijven die geen een on-premises Windows Server Active Directory-infrastructuur. Die gezegd, koppelen aan Azure AD en wordt ook worden gebruikt door grote organisaties op apparaten die niet kan tijdens het doorzoeken van traditionele domein (bijvoorbeeld mobiele apparaten) of voor gebruikers die voornamelijk waarvoor toegang tot Office 365 of andere SaaS-apps worden geïntegreerd met Azure AD.

Hoewel de traditionele domeindeelname nog steeds dat de beste biedt on-premises-ervaring op apparaten die kunnen lid worden van domein, is koppelen aan Azure AD geschikt voor apparaten die niet aan domein toevoegen. Azure AD Join is ook geschikt voor het beheren van gebruikers in de cloud. Dit gebeurt met mogelijkheden voor mobile device management in plaats van via traditionele domein beheerprogramma's zoals Groepsbeleid en System Center Configuration Manager (SCCM).

![Overzicht van de apparaten het bedrijf en persoonlijke apparaten met de lokale Active Directory en Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-overview.png)

## <a name="why-should-enterprises-adopt-azure-ad-join"></a>Waarom moeten ondernemingen vast Azure AD Join
* **Bedrijven die grotendeels in de cloud**: als u hebt verplaatst of verplaatst naar een model waarin u vermindert de footprint van uw lokale en wilt werken in de cloud, Azure AD Join kan voordelen. Mogelijk hebt u Azure AD-accounts handmatig of via het synchroniseren van uw lokale Active Directory gemaakt. In beide gevallen moet u een account hebben in Azure AD en kunt u deze aan te melden bij Windows 10. Uw gebruikers kunnen hun computers toevoegen aan Azure AD via ofwel de out of box experience (OOBE) of via het menu instellingen. Na toevoeging aan, kunnen profiteren van (eenmalige aanmelding SSO) toegang tot cloudbronnen zoals Office 365, in de browser of in de Office-toepassingen.
* **Onderwijsinstellingen**: een van de scenario's die we vaak gehoord is dat onderwijsinstellingen twee gebruikerstypen: onderwijsmedewerkers en studenten. Onderwijsmedewerkers leden worden beschouwd als van langere leden van de organisatie, waardoor on-premises-accounts maken voor deze wenselijk is. Maar studenten korterlopende lid zijn van de organisatie en dus kunnen worden beheerd in Azure AD. Dit betekent dat directory scale kan worden geactiveerd in de cloud in plaats van lokaal opgeslagen. Het betekent ook dat studenten kunnen bij Windows met hun Azure AD-accounts aanmelden en toegang tot Office 365-resources in hun browser of in de Office-toepassingen krijgen.
* **Bedrijven Retail**: een ander scenario ons bekend van klanten is hun wil seizoensgebonden werknemers eenvoudiger beheren.  Accounts voor langere termijn, fulltime werknemers worden opnieuw, meestal gemaakt als op een lokale accounts op domein-machines. Maar seizoensgebonden werknemers korterlopende lid zijn van de organisatie, dus is het wenselijk is om deze waar gebruikerslicenties kunnen eenvoudiger kan worden verplaatst om te beheren. Deze gebruikersaccounts maken in de cloud met Office 365-licenties kan de gebruikers om op te halen van de voordelen van aanmelding bij Windows en Office-toepassingen met een Azure AD-account. Ondertussen u meer flexibiliteit met de licenties worden onderhouden nadat ze verlaten.
* **Andere bedrijven**: zelfs als u gebruikers in uw lokale Active Directory onderhoudt, kunt u nog steeds profiteren van dat gebruikers worden toegevoegd met Azure AD. Dat komt doordat Azure AD biedt een vereenvoudigde gekoppelde ervaring, efficiënte Apparaatbeheer, inschrijving voor beheer van automatische mobiele apparaten en mogelijkheden voor eenmalige aanmelding voor Azure AD en on-premises resources.  

## <a name="what-capabilities-does-azure-ad-join-offer"></a>Welke mogelijkheden biedt Azure AD Join?
Met Azure AD Join beschikt u over het volgende:

* **Automatisch inrichten van apparaten in Bedrijfseigendom**: met Windows 10, kunnen gebruikers een geheel nieuwe, krimp apparaat configureren in de ervaring van de out-of-box, zonder tussenkomst van de IT.
* **Ondersteuning voor moderne vormfactoren**: koppelen aan Azure AD werkt op apparaten die niet de traditionele domein deelnemen aan mogelijkheden.  
* **Ondersteuning voor bestaande organisatieaccounts**: gebruikers niet langer hoeft te maken en te onderhouden een persoonlijk Microsoft-account voor de beste ervaring op bedrijf uitgegeven apparaten, zoals met Windows 8. Ze kunnen hun bestaande werkaccount in plaats daarvan gebruiken in Azure AD. Voor veel organisaties betekent dit in feite dat gebruikers kunnen instellen en aanmelden bij Windows met dezelfde referenties die ze voor toegang tot Office 365 gebruiken.
* **Inschrijving van automatische mobiele apparaten management**: apparaten kunnen automatisch worden geregistreerd in het beheer van mobiele apparaten wanneer verbonden met Azure AD. Dit proces werkt met Microsoft Intune en partner beheeroplossingen voor mobiele apparaten. Als het beheer van apparaten met Intune is voltooid, IT-beheerders kunnen monitor/Azure die lid zijn van AD apparaten beheren naast domein apparaten in de SCCM-beheerconsole.
* **Eenmalige aanmelding tot bedrijfsbronnen**: Profiteer van gebruikers eenmalige aanmelding vanaf het bureaublad van Windows-apps en resources in de cloud, zoals Office 365 en duizenden business-toepassingen die afhankelijk van Azure AD voor verificatie via zijn [Azure AD Connect](active-directory-azureadjoin-deployment-aadjoindirect.md). Apparaten in Bedrijfseigendom die zijn gekoppeld aan Azure AD ook Profiteer van eenmalige aanmelding tot lokale bronnen wanneer het apparaat zich in een bedrijfsnetwerk en vanaf elke locatie wanneer deze resources beschikbaar worden gesteld de [Azure AD-toepassingsproxy](https://msdn.microsoft.com/library/azure/Dn768219.aspx).
* **OS State Roaming**: toegankelijkheidsinstellingen, websites, Wi-Fi-wachtwoorden en andere instellingen worden gesynchroniseerd tussen de apparaten in Bedrijfseigendom zonder een persoonlijk Microsoft-account.
* **Enterprise-ready Windows Store**: de Windows Store ondersteunt de aanschaf van de app en licentieverlening met Azure AD-accounts. Organisaties kunnen volumelicentie-apps en beschikbaar maken voor de gebruikers in hun organisatie.

## <a name="how-do-different-devices-work-with-azure-ad-join"></a>Hoe verschillende apparaten werkt met Azure AD Join?
| Bedrijfsapparaten (lid is van het lokale domein) | Bedrijfsapparaten (lid is van de cloud) | Persoonlijk apparaat |
| --- | --- | --- |
| Kunnen gebruikers zich aanmelden in Windows met werkreferenties (zoals ze vandaag doen). |Gebruikers kunnen zich aanmelden bij Windows met zakelijke referenties die worden beheerd in Azure AD. Dit is van belang voor zakelijke apparaten in drie gevallen: <ol><li>De organisatie heeft geen on-premises (bijvoorbeeld een klein bedrijf) Active Directory.</li><li>De organisatie alle gebruikersaccounts in Active Directory niet maken (bijvoorbeeld gebruikersaccounts voor studenten, adviseurs of seizoensgebonden werknemers worden gemaakt in Active Directory).</li><li>De organisatie heeft zakelijke apparaten die aan een domein (op locatie), zoals telefoons of tablets met een mobiele-SKU (bijvoorbeeld een secundaire apparaat uitgevoerd om een verdieping factory/retail) kunnen niet worden gekoppeld.</li></ol> Azure AD Join ondersteunt het verbinden van apparaten voor zowel beheerde als federatieve organisaties het bedrijf. |Gebruikers met hun persoonlijke Microsoft-accountreferenties (geen wijzigen), moet u zich aanmelden bij Windows. |
| Gebruikers hebben toegang tot de instellingen voor zwerven en het enterprise Windows Store. Deze services werkt met werkaccounts en een persoonlijk Microsoft-account niet vereist. Hiervoor moeten organisaties hun lokale Active Directory verbinden met Azure AD. |Setup selfservice u kunt doen. Kunnen ze via de eerste sessie (FRX) via zijn werkaccount als alternatief voor IT-inrichten met de apparaten, hoewel beide methoden worden ondersteund. |Gebruikers kunnen eenvoudig met het toevoegen van een werkaccount dat wordt beheerd in Active Directory of Azure AD. |
| Gebruikers hebben SSO mogelijkheid vanaf het bureaublad te werken van apps, websites en bronnen--waaronder zowel lokale bronnen en cloud-apps die Azure AD voor verificatie gebruiken. |Apparaten worden automatisch geregistreerd in de enterprise-directory (Azure AD) en automatisch bij het beheer van mobiele apparaten geregistreerd. (Azure AD Premium-functie). |Gebruikers hebben de mogelijkheid voor eenmalige aanmelding via apps en websites/bronnen aan dit werkaccount. |
| Gebruikers kunnen hun persoonlijke Microsoft-accounts voor toegang tot hun eigen foto's en bestanden zonder enige impact op Ondernemingsgegevens toevoegen. (Instellingen zwervend blijven werken met hun werkaccount.) Het Microsoft-account kunt van eenmalige aanmelding en niet langer stations de roaming van instellingen. |U kunt doen een selfservice voor wachtwoordherstel (SSPR) op winlogon, wat betekent dat ze een vergeten wachtwoord opnieuw kunnen instellen. (Azure AD Premium-functie). |Gebruikers hebben toegang tot de onderneming Windows Store, zodat ze kunnen verkrijgen en line-of-business-apps op hun persoonlijke apparaten gebruiken. |

## <a name="additional-information"></a>Aanvullende informatie
* [Windows 10 for the enterprise: Ways to use devices for work](active-directory-azureadjoin-windows10-devices-overview.md) (Windows 10 voor de onderneming: manieren om apparaten voor werk te gebruiken)
* [Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md) (Cloudmogelijkheden uitbreiden naar Windows 10-apparaten met behulp van Azure Active Directory Join)
* [Identiteiten zonder wachtwoorden via Microsoft Passport verifiëren](active-directory-azureadjoin-passport.md)
* [Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)
* [Connect domain-joined devices to Azure AD for Windows 10 experiences](active-directory-azureadjoin-devices-group-policy.md) (Apparaten die lid zijn van een domein verbinden met Azure AD voor Windows 10-ervaringen)
* [Azure AD Join instellen](active-directory-azureadjoin-setup.md)

