---
title: Met behulp van Windows 10-apparaten in uw werkplek | Microsoft Docs
description: Biedt een momentopname van de mogelijkheden voor gebruikers en IT, het contrast van de verschillende manieren een apparaat kan worden ingericht en gebruikt in een onderneming met Windows 10.
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
ms.openlocfilehash: 451842f764898af65dd7300e8b48442d256cea7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-windows-10-devices-in-your-workplace"></a>Met behulp van Windows 10-apparaten in uw werkplek
Van toepassing op: Windows 10-pc's

Windows 10 biedt drie modellen voor organisaties die gebruikers toegang geven tot bronnen op het werk in een veilige en handige manier.

* **Azure Active Directory Join** (Azure AD Join), voor werknemers die toegang resources, zoals Office 365 voornamelijk in de cloud tot. Azure AD Join is selfservice werk ervaring die is er nieuw in Windows 10-inrichting.
* **Aan domein toevoegen**, voor organisaties die investeringen in lokale apps en resources hebben. Aan domein toevoegen biedt een betere ervaring in Windows 10 bij verbinding met Azure AD.
* **Een nieuwe vereenvoudigd BYOD ervaring**voor gebruikers die u wilt toevoegen van een werk- of school bij Windows en eenvoudig toegang krijgen tot bronnen op persoonlijke apparaten.

De volgende tabel geeft een momentopname van de mogelijkheden voor gebruikers en IT-beheerders de verschillende manieren een apparaat kan worden ingericht en gebruikt in een onderneming met Windows 10 contrast:

|  | Aan domein toevoegen | Azure AD Join | Persoonlijk apparaat |
| --- | --- | --- | --- |
| Windows-apparaat aanmelden voor werk of school-accounts. |Ja |Ja |Nee |
| Gebruiker eenmalige aanmelding (SSO) voor Office 365 en Azure AD-apps. Eenmalige aanmelding is de mogelijkheid slechts één keer aanmelden bij het toegang krijgen tot organisatieresources. |Ja |Ja |Ja |
| Gebruiker SSO Kerberos/NTLM-apps. |Ja |Beperkt |Ja, via VPN |
| Sterke verificatie- en handige aanmelden voor werk of school accounts met Microsoft Passport en Windows Hello. |Ja |Ja |Ja |
| Toegang tot Windows Store enterprise met een werk- of schoolaccount (dus niet door een Microsoft-account). |Ja |Ja |Ja |
| Enterprise-compatibele roaming van gebruikersinstellingen op apparaten met werk of school-accounts. |Ja |Ja |Ja |
| De mogelijkheid toegang te beperken tot de organisatie-apps naar apparaten die compatibel met beleidsregels voor organisatie-apparaten zijn. |Ja |Ja |Ja |
| Gebruiker selfservice inrichting van apparaten voor "werk overal." |Nee |Ja |Ja |
| De mogelijkheid om apparaten te beheren. |Ja, via GP/SCCM |Ja |Ja |

## <a name="use-work-owned-devices-with-azure-ad-join-and-domain-join-in-windows-10"></a>Gebruik werk eigendom apparaten met Azure AD Join en het domein koppelen in Windows 10
Windows 10 biedt twee manieren om zakelijke eigendom apparaten hebben toegang tot bronnen op het werk:

* Azure AD Join
* Aan domein toevoegen
  
  Geldige opties zijn afhankelijk van de behoeften en de vereisten van een organisatie kan zijn. In sommige gevallen kunnen organisaties kunnen gebruikmaken van het inschakelen van beide methoden van de implementatie van.

## <a name="when-to-use-azure-active-directory-join"></a>Het gebruik van Azure Active Directory Join
Azure AD Join is een nieuwe werk selfservice inrichting ervaring in Windows 10.  Het is gericht op werknemers die toegang hebben tot bronnen op het werk zoals Office 365 voornamelijk in de cloud. Het is een eenvoudige manier voor het configureren van computers, tablets en telefoons voor de onderneming. Apparaten worden beheerd via beheer van mobiele apparaten met behulp van consistente besturingselementen in verschillende Windows-platforms.

**Azure AD Join gebruikt om een van deze redenen**:

* Wilt u de selfservice inrichting inschakelen van apparaten voor werknemers onderweg.
* U opgeven gebruikers met mobiele apparaten zoals tablets en telefoons eigendom van het werk.
* Wilt u een set gebruikers beheren in Azure AD in plaats van in Active Directory, zoals de seizoensgebonden werknemers, contractanten of studenten.
* Wilt u gekoppelde mogelijkheden bieden aan werknemers in externe filialen met beperkte on-premises infrastructuur.
* U beschikt niet over een lokale Active Directory.

Sommige organisaties gebruikt Azure AD Join als de belangrijkste manier voor het implementeren van apparaten die eigendom zijn werk, vooral als ze de meeste of alle van hun bronnen naar de cloud migreren. Hybride organisaties met Active Directory en Azure AD kunnen ook kiezen voor het implementeren van een methode of een ander, afhankelijk van de gebruiker of afdeling.

Scholen en universiteiten, bijvoorbeeld kunnen worden beheerd in Active Directory-personeel en studenten in Azure AD. Sommige bedrijven wilt externe kantoren of verkoopafdeling beheren in Azure AD. Koppelen aan Azure AD zowel domain join methoden kunnen worden gebruikt binnen een organisatie hybride. Azure AD Join mag een geweldige aanvulling op het domein voor het implementeren van apparaten in een werkomgeving.

**Als de meest gangbare toegang tot bedrijfsbronnen via de cloud, uw organisatie kan profiteren van extra voordelen als**:

* U kunt de afhankelijkheden van on-premises identity infrastructuur verwijderen.
* U kunt uw implementatiemodel apparaten vereenvoudigen weg imaging-oplossingen doordat de configuratie van self-service ophalen.
* Beheer van mobiele apparaten kunt u al uw apparaten beheren op verschillende platforms.

Zie voor meer informatie over Azure AD Join [cloudfuncties uitbreiden naar Windows 10-apparaten via Azure Active Directory Join](active-directory-azureadjoin-overview.md).

## <a name="when-to-use-domain-join-or-keep-using-it"></a>Wanneer gebruikt u lid worden van het domein (of blijven gebruiken deze)
Voor de afgelopen 15 jaar hebben veel organisaties aan domein toevoegen gebruikt om werk apparaten te verbinden. Deze kan gebruikers zich aanmelden bij hun apparaten met het Active Directory-werk of school accounts. Lid van domein kan ook IT centraal en volledig beheer van deze apparaten. Organisaties zijn gewoonlijk afhankelijk van de installatiekopieën methoden voor het inrichten van apparaten en vaak gebruik van System Center Configuration Manager (SCCM) of Group Policy (GP) om deze te beheren.

**Uw bedrijf moet domain join (of blijven gebruiken deze) gebruiken voor een van de volgende redenen**:

* U hebt de Win32-apps die zijn geïmplementeerd op deze apparaten die gebruikmaken van NTLM of Kerberos.
* U wilt GP of SCCM/DCM om apparaten te beheren.
* U wilt blijven gebruiken imaging-oplossingen voor het configureren van apparaten voor uw werknemers.

**Aan domein toevoegen in Windows 10 biedt u ook de volgende voordelen wanneer verbonden met Azure AD**:

* Sterke verificatie van het apparaat is gebonden en handige aanmelden voor werk of school accounts met Microsoft Passport en Windows Hello.
* Toegang tot de onderneming Windows Store voor apparaten die werk- of schoolaccounts (Er is geen Microsoft-account vereist).
* Enterprise-compatibele roaming van gebruikersinstellingen op apparaten die gebruikmaken van werk of school accounts (Er is geen Microsoft-account vereist).
* De mogelijkheid toegang te beperken tot de organisatie-apps naar apparaten die compatibel met beleidsregels voor organisatie-apparaten zijn.

Zie voor meer informatie over Azure AD Join [cloudfuncties uitbreiden naar Windows 10-apparaten via Azure Active Directory Join](active-directory-azureadjoin-overview.md).

## <a name="enable-joining-of-personally-owned-devices-for-work-or-school"></a>Koppelen van hun eigen apparaten voor werk of school inschakelen
Ter ondersteuning van BYOD in de onderneming, biedt Windows 10 de gebruiker de mogelijkheid een account voor werk of school toevoegen aan hun computer, tablet of telefoon. Nadat de gebruiker een account voor werk of school toevoegt, wordt het apparaat geregistreerd bij Azure AD en eventueel geregistreerd in het beheersysteem voor mobiele apparaten die de organisatie heeft geconfigureerd. De map wordt deze apparaten weergegeven als 'Geregistreerde' vs. 'Azure AD lid'. IT-beheerders kunnen verschillende soorten beleid op basis van deze informatie toepassen die een lichter aanraakfunctionaliteit op hun eigen apparaten dan op apparaten die eigendom zijn van werk indien gewenst.

Gebruikers kunnen toevoegen van een werk- of schoolaccount op hun persoonlijke apparaten zeer eenvoudig. Ze kunnen dit doen bij het openen van een werktoepassing voor de eerste keer of ze kunnen dit handmatig doen via het menu instellingen. Dit account biedt eenmalige aanmelding met organisatie-bronnen.

Zie voor meer informatie over Azure AD Join [domein apparaten verbinden met Azure AD voor Windows 10 optreedt](active-directory-azureadjoin-devices-group-policy.md).

## <a name="enable-domain-join-or-azure-ad-join"></a>Aan domein toevoegen of koppelen aan Azure AD inschakelen
Alle methoden die eerder zijn beschreven (lid van domein, koppelen aan Azure AD en toevoegen werk of school-account) hebben toegangspunten in de gebruikerservaring van Windows 10. Alle vereisen echter een IT-beheerder voor het inschakelen van de functionaliteit in de infrastructuur voordat de ervaring werkt.

## <a name="requirements-for-deploying-azure-ad-join"></a>Vereisten voor het implementeren van Azure AD Join
Voor het implementeren van Azure AD Join voor elke set van gebruikers moet u het volgende:

* Een Azure AD-abonnement.
* Een Azure AD Premium-abonnement, zoals mobiele apparaat management automatische inschrijving, als u meer mogelijkheden nodig hebt.
* Beheer van mobiele apparaten--bijvoorbeeld een abonnement op Microsoft Intune, mobile device management voor Office 365, of een van de partner mobiele apparaat management leveranciers met Azure AD integreren. (Zie de [sectie Veelgestelde vragen over](#frequently-asked-questions) in de buurt van het einde van dit artikel voor meer informatie).

Als uw faciliteiten hybride, raden we het implementeren van Azure AD Connect om uit te breiden de on-premises directory naar Azure AD.

## <a name="requirements-for-using-domain-join-with-azure-ad"></a>Vereisten voor het gebruik van domein met Azure AD
Aan domein toevoegen blijft werken zoals altijd heeft. Echter, als u de voordelen van Azure AD u het volgende nodig:

* Een Azure AD-abonnement.
* Een implementatie van Azure AD Connect uit te breiden de on-premises directory naar Azure AD.
* Een beleid waarmee apparaten domein voorwaardelijke toegang hebben tot Azure AD.
* Een beleid waarmee toegang tot apparaten 'domein' als u wilt kunnen beperken van toegang voor sommige apparaten.
* System Center Configuration Manager versie 1509 voor Technical Preview, zodat de regels voor het vereisen van compatibele apparaten. (Zie het TechNet-documentatie en blogbericht).

Zie voor meer informatie over domein in Windows 10- [domein apparaten verbinden met Azure AD voor Windows 10 optreedt](active-directory-azureadjoin-devices-group-policy.md)

## <a name="requirements-for-using-byod-and-add-a-work-or-school-account"></a>Vereisten voor het gebruik van BYOD en 'Een account voor werk of school toevoegen'
Om in te schakelen 'bring your own device' (BYOD) met een account voor werk of school, moet u het volgende:

* Een Azure AD-abonnement.
* Een Azure AD Premium-abonnement, zoals mobiele apparaat management automatische inschrijving, als u meer mogelijkheden nodig hebt.

## <a name="requirements-for-using-microsoft-passport"></a>Vereisten voor het gebruik van Microsoft Passport
Als u wilt Microsoft Passport inschakelen, moet u het volgende:

* Een openbare-sleutelinfrastructuur (PKI) voor de ondersteuning voor verificatie op basis van certificaten die gebruikmaakt van Microsoft Passport.
* Een Intune-abonnement voor de ondersteuning voor verificatie op basis van certificaten die gebruikmaakt van Microsoft Passport for Azure AD Join en werk-of schoolaccounts.
* System Center Configuration Manager versie 1509 voor Technical Preview (Zie het TechNet-documentatie en blogbericht) voor de ondersteuning voor verificatie op basis van certificaten die gebruikmaakt van Microsoft Passport voor domeindeelname.
* Een beleid voor het Microsoft Passport inschakelen in de organisatie.

U kunt als alternatief voor het gebruik van een PKI op basis van sleutels Microsoft Passport inschakelen door het volgende te doen:

* Implementeer Windows Server 2016 'Productie Preview 1' DC's (niet nodig voor de functionele niveaus van domein of forest; enkele DC's voor redundantie voor die elk Active Directory-site is voldoende).
* Stel beleid in Microsoft Passport inschakelen in de organisatie.

Zie < link-to-MS-Passport-and-Windows-Hello-document > voor meer informatie over Microsoft Passport en Windows Hello in Windows 10.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen
### <a name="which-partner-mobile-device-management-products-integrate-with-azure-ad"></a>Welke producten partner mobiele apparaat management integreren met Azure AD?
De volgende leveranciersproducten integreren met Azure AD voor unified inschrijving en voorwaardelijke toegang in Windows 10:

* AirWatch VMware
* Citrix Xenmobile
* Lightspeed Mobile Manager
* SOTI lokaal beheer van mobiele apparaten
* MobileIron

### <a name="what-about-workplace-join-in-windows-10"></a>Hoe zit het met Workplace Join in Windows 10?
Werkplek koppelen is in Windows 8.1 gebruikt om BYOD te kunnen. BYOD is ingeschakeld via "toevoegen van een werk- of schoolaccount in Windows 10, zoals eerder in dit document wordt uitgelegd. Voor organisaties die hun beheer van mobiele apparaten niet met Azure AD integreren, kunnen gebruikers het apparaat registreren bij het beheer handmatig via **instellingen** > **Accounts**  >  **Via het werknetwerk**.

### <a name="can-users-connect-their-microsoft-account-to-their-domain-account-in-windows-10"></a>Kunnen gebruikers hun Microsoft-account koppelen aan hun domeinaccount in Windows 10
Niet in Windows 10. In Windows 8.1-gebruikers van apparaten die lid zijn van een domein kunnen "verbinding maken' hun Microsoft-account (bijvoorbeeld Hotmail, Live, Outlook, Xbox, enz.) met een domeinaccount waarmee bepaalde ervaringen zoals het eenmalige aanmelding voor Live-services, het gebruik van de Windows Store en roaming van gebruiker de instellingen op apparaten. In Windows 10, het Microsoft-account 'verbinding' functionaliteit is buiten gebruik gesteld. De gebruiker kan een of meer Microsoft-accounts toevoegen als extra accounts eenmalige aanmelding inschakelen bij consumer services, zoals de Windows Store. Dit wordt gedaan **instellingen** > **Accounts** > **uw account**.

Gebruikers die een upgrade van Windows 8.1-apparaten domein en die hun Microsoft-account was verbonden, wordt automatisch toegevoegd aan de lijst van extra accounts die ze gebruiken hun gekoppelde Microsoft-account hebben.

## <a name="additional-information"></a>Aanvullende informatie
* [Windows 10 for the enterprise: Ways to use devices for work](active-directory-azureadjoin-windows10-devices-overview.md) (Windows 10 voor de onderneming: manieren om apparaten voor werk te gebruiken)
* [Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md) (Cloudmogelijkheden uitbreiden naar Windows 10-apparaten met behulp van Azure Active Directory Join)
* [Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)
* [Connect domain-joined devices to Azure AD for Windows 10 experiences](active-directory-azureadjoin-devices-group-policy.md) (Apparaten die lid zijn van een domein verbinden met Azure AD voor Windows 10-ervaringen)
* [Azure AD Join instellen](active-directory-azureadjoin-setup.md)

