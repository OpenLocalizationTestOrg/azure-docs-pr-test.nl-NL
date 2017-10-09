---
title: aaaUsing Windows 10-apparaten in uw werkplek | Microsoft Docs
description: Biedt een momentopname van de mogelijkheden voor gebruikers en IT, contrast Hallo verschillende manieren een apparaat kan worden ingericht en gebruikt in een onderneming met Windows 10.
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: 94ccc8fd-b17b-4fda-8d56-9d87aa37a9f9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 8767e1649ced8737d20875f425c24198dcaa7f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-10-devices-in-your-workplace"></a>Met behulp van Windows 10-apparaten in uw werkplek
Van toepassing op: Windows 10-pc's

Windows 10 biedt drie modellen voor organisaties die bronnen op het werk tooaccess gebruikers in een veilige en handige manier inschakelen.

* **Azure Active Directory Join** (Azure AD Join), voor werknemers die toegang resources, zoals Office 365 voornamelijk in Hallo cloud tot. Azure AD Join is selfservice werk ervaring die is er nieuw in Windows 10-inrichting.
* **Aan domein toevoegen**, voor organisaties die investeringen in lokale apps en resources hebben. Aan domein toevoegen biedt een betere ervaring in Windows 10 bij verbinding met tooAzure AD.
* **Een nieuwe vereenvoudigd BYOD ervaring**voor account gebruikers willen tooadd een werk of school tooWindows en eenvoudig toegang krijgen bronnen op persoonlijke apparaten tot.

Hallo geeft volgende tabel een momentopname van de mogelijkheden voor gebruikers en IT-beheerders contrast Hallo verschillende manieren een apparaat kan worden ingericht en gebruikt in een onderneming met Windows 10:

|  | Aan domein toevoegen | Azure AD Join | Persoonlijk apparaat |
| --- | --- | --- | --- |
| Windows-apparaat aanmelden voor werk of school-accounts. |Ja |Ja |Nee |
| Gebruiker eenmalige aanmelding (SSO) tooOffice 365 en Azure AD-apps. Eenmalige aanmelding is Hallo mogelijkheid toosign in slechts één keer tooaccess organisatie-bronnen. |Ja |Ja |Ja |
| Gebruiker SSO tooKerberos/NTLM-apps. |Ja |Beperkt |Ja, via VPN |
| Sterke verificatie- en handige aanmelden voor werk of school accounts met Microsoft Passport en Windows Hello. |Ja |Ja |Ja |
| Toegang tot Windows Store tooenterprise met een werk- of schoolaccount (dus niet door een Microsoft-account). |Ja |Ja |Ja |
| Enterprise-compatibele roaming van gebruikersinstellingen op apparaten met werk of school-accounts. |Ja |Ja |Ja |
| Hallo mogelijkheid toorestrict toegang tooorganizational apps toodevices die compatibel met beleidsregels voor organisatie-apparaten zijn. |Ja |Ja |Ja |
| Gebruiker selfservice inrichting van apparaten voor "werk overal." |Nee |Ja |Ja |
| Mogelijkheid toomanage apparaten. |Ja, via GP/SCCM |Ja |Ja |

## <a name="use-work-owned-devices-with-azure-ad-join-and-domain-join-in-windows-10"></a>Gebruik werk eigendom apparaten met Azure AD Join en het domein koppelen in Windows 10
Windows 10 biedt twee manieren voor apparaten die eigendom zijn van werk tooaccess werkresources:

* Azure AD Join
* Aan domein toevoegen
  
  Geldige opties zijn afhankelijk van de behoeften en de vereisten van een organisatie kan zijn. In sommige gevallen kunnen organisaties kunnen gebruikmaken van het inschakelen van beide methoden van de implementatie van.

## <a name="when-toouse-azure-active-directory-join"></a>Wanneer toouse Azure Active Directory Join
Azure AD Join is een nieuwe werk selfservice inrichting ervaring in Windows 10.  Het is gericht op werknemers die toegang hebben tot bronnen op het werk zoals Office 365 voornamelijk in Hallo cloud. Het is een eenvoudige manier tooconfigure computers, tablets, en voor Hallo enterprise telefoons. Apparaten worden beheerd via beheer van mobiele apparaten met behulp van consistente besturingselementen in verschillende Windows-platforms.

**Azure AD Join gebruikt om een van deze redenen**:

* Wilt u tooenable Hallo selfservice inrichting van apparaten voor werknemers op Hallo gaat.
* U opgeven gebruikers met mobiele apparaten zoals tablets en telefoons eigendom van het werk.
* U toomanage een groep gebruikers in Azure AD in plaats van in Active Directory, zoals de seizoensgebonden werknemers, contractanten of studenten.
* Wilt u gekoppelde mogelijkheden tooworkers tooprovide in externe filialen met beperkte on-premises infrastructuur.
* U beschikt niet over een lokale Active Directory.

Sommige organisaties gebruikt Azure AD Join als Hallo primaire manier toodeploy werk apparaten, vooral als ze de meeste of alle van de cloud-bronnen toohello migreren. Hybride organisaties met Active Directory en Azure AD kunt ook toodeploy één methode of een ander, afhankelijk van het Hallo-gebruiker of afdeling.

Scholen en universiteiten, bijvoorbeeld kunnen worden beheerd in Active Directory-personeel en studenten in Azure AD. Sommige bedrijven kunt toomanage externe kantoren of verkoopafdeling in Azure AD. Koppelen aan Azure AD zowel domain join methoden kunnen worden gebruikt binnen een organisatie hybride. Azure AD Join is een goede aanvulling toodomain join voor het implementeren van apparaten in een werkomgeving.

**Als Hallo meest gangbare toegang tooenterprise resources via de cloud Hallo, uw organisatie kan profiteren van extra voordelen als**:

* U kunt de afhankelijkheden van on-premises identity infrastructuur verwijderen.
* U kunt uw implementatiemodel apparaten vereenvoudigen weg imaging-oplossingen doordat de configuratie van self-service ophalen.
* U kunt mobiele apparaat management toomanage al uw apparaten gebruiken op verschillende platforms.

Zie voor meer informatie over Azure AD Join [cloud uitbreiden mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join](active-directory-azureadjoin-overview.md).

## <a name="when-toouse-domain-join-or-keep-using-it"></a>Wanneer toouse lid worden van domein (of blijven gebruiken)
Voor Hallo hebben laatste vijftien jaar veel organisaties gebruikt domain join tooconnect werk apparaten. Hiermee kunnen gebruikers toosign tootheir apparaten bij hun Active Directory van werk of school accounts. Aan domein toevoegen kunt ook IT toocentrally en volledig beheer van deze apparaten. Organisaties zijn gewoonlijk afhankelijk van de methoden tooprovision apparaten imaging en vaak gebruiken in System Center Configuration Manager (SCCM) of Group Policy (GP) toomanage ze.

**Uw bedrijf moet domain join (of blijven gebruiken deze) gebruiken voor een van de volgende redenen**:

* U hebt Win32-apps geïmplementeerde toothese apparaten die gebruikmaken van NTLM of Kerberos.
* U vereisen GP of SCCM/DCM toomanage apparaten.
* U wilt dat toocontinue toouse imaging oplossingen tooconfigure apparaten voor uw werknemers.

**Aan domein toevoegen in Windows 10 biedt u eveneens Hallo volgende voordelen wanneer verbonden tooAzure AD**:

* Sterke verificatie van het apparaat is gebonden en handige aanmelden voor werk of school accounts met Microsoft Passport en Windows Hello.
* Toegang tot toohello enterprise, Windows Store voor apparaten die werk- of schoolaccounts (Er is geen Microsoft-account vereist).
* Enterprise-compatibele roaming van gebruikersinstellingen op apparaten die gebruikmaken van werk of school accounts (Er is geen Microsoft-account vereist).
* Hallo mogelijkheid toorestrict toegang tooorganizational apps toodevices die compatibel met beleidsregels voor organisatie-apparaten zijn.

Zie voor meer informatie over Azure AD Join [cloud uitbreiden mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join](active-directory-azureadjoin-overview.md).

## <a name="enable-joining-of-personally-owned-devices-for-work-or-school"></a>Koppelen van hun eigen apparaten voor werk of school inschakelen
toosupport BYOD in Hallo enterprise, Windows 10 biedt Hallo gebruiker Hallo mogelijkheid tooadd een werk of school-account tootheir computer, tablet of telefoon. Na het Hallo gebruiker voegt een werk of schoolaccount, Hallo-apparaat is geregistreerd in Azure AD en eventueel geregistreerd in beheersysteem van Hallo mobiel apparaat dat Hallo organisatie is geconfigureerd. Hallo-directory, wordt deze apparaten weergegeven als 'Geregistreerde' vs. 'Azure AD lid'. IT-beheerders kunnen verschillende soorten beleid op basis van deze informatie toepassen die een lichter aanraakfunctionaliteit op hun eigen apparaten dan op apparaten die eigendom zijn van werk indien gewenst.

Gebruikers kunnen toevoegen van een werk of school account tootheir persoonlijk apparaat zeer eenvoudig. Ze kunnen dit doen bij het openen van een werktoepassing voor Hallo eerst of ze kunnen dit handmatig doen via het menu Hallo-instellingen. Dit account gaat SSO tooorganizational bronnen leveren.

Zie voor meer informatie over Azure AD Join [domeinapparaten tooAzure AD Connect voor Windows 10 optreedt](active-directory-azureadjoin-devices-group-policy.md).

## <a name="enable-domain-join-or-azure-ad-join"></a>Aan domein toevoegen of koppelen aan Azure AD inschakelen
Alle methoden die eerder zijn beschreven (lid van domein, koppelen aan Azure AD en toevoegen werk of school-account) hebben toegangspunten in de gebruikerservaring Hallo Windows 10. Alle moeten echter een IT-beheerder tooenable Hallo functionaliteit in Hallo infrastructuur voordat Hallo ervaring werkt.

## <a name="requirements-for-deploying-azure-ad-join"></a>Vereisten voor het implementeren van Azure AD Join
toodeploy Azure AD Join voor elke set van gebruikers, moet u hello te volgen:

* Een Azure AD-abonnement.
* Een Azure AD Premium-abonnement, zoals mobiele apparaat management automatische inschrijving, als u meer mogelijkheden nodig hebt.
* Beheer van mobiele apparaten--bijvoorbeeld een abonnement op Microsoft Intune, mobile device management voor Office 365, of een van de Hallo partner mobiele apparaat management leveranciers die kunnen worden geïntegreerd met Azure AD. (Zie Hallo [sectie Veelgestelde vragen](#frequently-asked-questions) bijna Hallo einde van dit artikel voor meer informatie).

Als uw faciliteiten hybride, raden we dat u Azure AD Connect tooextend Hallo lokale directory tooAzure AD implementeert.

## <a name="requirements-for-using-domain-join-with-azure-ad"></a>Vereisten voor het gebruik van domein met Azure AD
Aan domein toevoegen blijft toowork omdat u altijd. Echter tooget hello Azure AD voordelen moet u hello te volgen:

* Een Azure AD-abonnement.
* Een implementatie van Azure AD Connect tooextend Hallo lokale directory tooAzure AD.
* Een beleid waarmee domeinapparaten toohave voorwaardelijke toegang tooAzure AD.
* Een beleid waarmee u toegang krijgt apparaten te 'domein' als u toobe kunnen toorestrict wordt op sommige apparaten wilt.
* System Center Configuration Manager versie 1509 voor Technical Preview, tooenable regels voor het vereisen van compatibele apparaten. (Zie Hallo TechNet-documentatie en blogbericht, Engelstalig).

Zie voor meer informatie over domein in Windows 10- [domeinapparaten tooAzure AD Connect voor Windows 10 optreedt](active-directory-azureadjoin-devices-group-policy.md)

## <a name="requirements-for-using-byod-and-add-a-work-or-school-account"></a>Vereisten voor het gebruik van BYOD en 'Een account voor werk of school toevoegen'
tooenable 'bring your own device' (BYOD) met werk of school-accounts, moet u de volgende Hallo:

* Een Azure AD-abonnement.
* Een Azure AD Premium-abonnement, zoals mobiele apparaat management automatische inschrijving, als u meer mogelijkheden nodig hebt.

## <a name="requirements-for-using-microsoft-passport"></a>Vereisten voor het gebruik van Microsoft Passport
Microsoft Passport tooenable, moet u de volgende Hallo:

* Een openbare-sleutelinfrastructuur (PKI) voor de ondersteuning voor verificatie op basis van certificaten die gebruikmaakt van Microsoft Passport.
* Een Intune-abonnement voor de ondersteuning voor verificatie op basis van certificaten die gebruikmaakt van Microsoft Passport for Azure AD Join en werk-of schoolaccounts.
* System Center Configuration Manager versie 1509 voor Technical Preview (Zie Hallo TechNet-documentatie en blogbericht, Engelstalig) voor de ondersteuning voor verificatie op basis van certificaten die gebruikmaakt van Microsoft Passport voor domeindeelname.
* Een beleid voor het Microsoft Passport inschakelen in Hallo-organisatie.

Als een alternatieve toousing een PKI, kunt u op basis van sleutels Microsoft Passport inschakelen door Hallo volgende te doen:

* Implementeer Windows Server 2016 'Productie Preview 1' DC's (niet nodig voor de functionele niveaus van domein of forest; enkele DC's voor redundantie voor die elk Active Directory-site is voldoende).
* Stel beleid tooenable Microsoft Passport in Hallo-organisatie.

Zie < link-to-MS-Passport-and-Windows-Hello-document > voor meer informatie over Microsoft Passport en Windows Hello in Windows 10.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen
### <a name="which-partner-mobile-device-management-products-integrate-with-azure-ad"></a>Welke producten partner mobiele apparaat management integreren met Azure AD?
Hallo integreren volgende leveranciersproducten met Azure AD voor unified inschrijving en voorwaardelijke toegang in Windows 10:

* AirWatch VMware
* Citrix Xenmobile
* Lightspeed Mobile Manager
* SOTI lokaal beheer van mobiele apparaten
* MobileIron

### <a name="what-about-workplace-join-in-windows-10"></a>Hoe zit het met Workplace Join in Windows 10?
Werkplek koppelen is gebruikt in Windows 8.1 tooenable BYOD. BYOD is ingeschakeld via "toevoegen van een werk- of schoolaccount in Windows 10, zoals eerder in dit document wordt uitgelegd. Voor organisaties die hun beheer van mobiele apparaten niet met Azure AD integreren, kunnen gebruikers Hallo-apparaat registreren bij het beheer handmatig via **instellingen** > **Accounts**  >  **Via het werknetwerk**.

### <a name="can-users-connect-their-microsoft-account-tootheir-domain-account-in-windows-10"></a>Gebruikers kunnen verbinding maken met hun Microsoft-account tootheir domeinaccount in Windows 10?
Niet in Windows 10. In Windows 8.1-gebruikers van apparaten die lid zijn van een domein kunnen "verbinding maken' hun Microsoft-account (bijvoorbeeld Hotmail, Live, Outlook, Xbox, enz.) tootheir domein account tooenable bepaalde ervaringen zoals SSO tooLive services, het gebruik van Hallo Windows Store en van roaming de instellingen van de gebruiker over verschillende apparaten. In Windows 10, Hallo 'verbinding' functionaliteit van Microsoft-account is buiten gebruik gesteld. Hallo-gebruiker kan een of meer Microsoft-accounts toevoegen als extra accounts tooenable SSO tooconsumer services zoals Hallo Windows Store. Dit wordt gedaan **instellingen** > **Accounts** > **uw account**.

Gebruikers die een upgrade van het domein Windows 8.1-apparaten, en die was hun Microsoft-account zijn verbonden, wordt automatisch hebben hun gekoppelde Microsoft-account toegevoegd toohello lijst met extra accounts die ze gebruiken.

## <a name="additional-information"></a>Aanvullende informatie
* [Windows 10 voor Hallo ondernemingen: manieren toouse apparaten for work.](active-directory-azureadjoin-windows10-devices-overview.md)
* [Cloud-mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join uitbreiden](active-directory-azureadjoin-user-upgrade.md)
* [Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)
* [Verbinding maken met domein apparaten tooAzure AD voor Windows 10-ervaring](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD Join instellen](active-directory-azureadjoin-setup.md)

