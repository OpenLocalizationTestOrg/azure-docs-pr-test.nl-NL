---
title: persoonlijke gegevens met Azure identiteits- en toegangsbeheer besturingselementen aaaProtect | Microsoft Docs
description: Met behulp van Azure identiteits- en toegangsbeheer besturingselementen toohelp beveiligen u uw persoonlijke gegevens
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a>Azure Active Directory en de multi-factor Authentication: persoonlijke gegevens beschermen met besturingselementen voor identiteits- en toegangsbeheer

Dit artikel bevat informatie en procedures kunt u tooprotect persoonlijke gegevens met behulp van Azure Active Directory en de multi-factor authentication-beveiligingsfuncties en -services.

## <a name="scenario"></a>Scenario

Een grote cruise bedrijf, gevestigd in Hallo Verenigde Staten, wordt de bewerkingen toooffer routes in Hallo Middellandse, Adriatische, Baltische veiligheid ook Hallo Florida uitbreiden. toosupport deze inspanningen, heeft deze meerdere kleinere cruise regels op basis van Italië, verkregen Duitsland, Denemarken en Hallo Verenigd Koninkrijk 

Hallo bedrijf maakt gebruik van Microsoft Azure toostore bedrijfsgegevens Hallo cloud. Dit omvat persoonlijk gegevens zoals namen, adressen, telefoonnummers en creditcardgegevens van globale klantendatabase. Dit omvat ook traditionele Human Resources informatie zoals adressen, telefoonnummers, BTW-id's en medische informatie over de werknemers van het bedrijf op alle locaties. Hallo cruise regel onderhoudt ook een grote database van derden en loyaliteit voor leden die persoonlijke gegevens tootrack relaties met de huidige en eerdere klanten bevat.

Zakelijke werknemers toegang tot het Hallo netwerk van de externe kantoren en reizen agents van het bedrijf Hallo wereld Hallo zich toegang tot toosome bedrijfsbronnen hebben.

## <a name="problem-statement"></a>Probleemformulering

Hallo bedrijf moet Hallo privacy van klanten en werknemers persoonlijke gegevens beveiligen tegen kwaadwillende personen toouse geknoeid identiteiten toogain toegang zoeken. Ze ook moeten ervoor zorgen dat toegang toopersonal gegevens door legitieme gebruikers is beperkt tot alleen degenen die u nodig hebt toodo hun werk.

## <a name="company-goal"></a>Bedrijf-doel

doel van het bedrijf Hallo is tooensure die toegang tot gegevens toopersonal strikt worden beheerd. Het is essentieel dat de identiteit van gebruikers met toegang tot toopersonal gegevens door sterke verificatie worden beveiligd. Een beleid van [minimale bevoegdheden] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) moeten worden afgedwongen, zodat legitieme gebruikers hoeven alleen Hallo niveau van toegang hebben en niet meer.

## <a name="solutions"></a>Oplossingen

Microsoft Azure biedt beheerprogramma's voor identiteits- en toegangsbeheer toohelp bedrijven bepalen wie heeft toegang tot tooresources die persoonlijke gegevens bevatten.

### <a name="azure-active-directory"></a>Azure Active Directory

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) beheert identiteiten en beheert de toegang tooAzure evenals andere on-premises en andere cloudbronnen, gegevens en toepassingen. [Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) helpt Azure beheerders toominimize Hallo aantal mensen toegang toocertain informatie zoals persoonlijke gegevens. Deze manier kunnen toodiscover, Beperk en bewaak bevoegde identiteiten en hun access tooresources en tooassign tijdelijke, JIT (Just in time) beheerdersrechten tooeligible-gebruikers. Het bevat ook inzicht in de AAD-beheerdersbevoegdheden hebben.

Hallo-activiteiten die betrokken zijn bij het gebruik van AAD PIM omvatten:

- Privileged Identity Management voor uw directory inschakelen

- Met behulp van Privileged Identity Management admin dashboard toosee belangrijke informatie in een oogopslag

- Hallo bevoegde identiteiten (beheerders) toe te voegen of te verwijderen of de in aanmerking komende beheerders tooeach functie beheren

- Hallo rol activeringsinstellingen configureren

- Rollen activeren

- Rol activiteit controleren

#### <a name="how-do-i-enable-aad-pim"></a>Hoe kan ik AAD PIM inschakelen?

met behulp van PIM voor uw directory toostart Hallo te volgen:

1. Meld u toohello Azure-portal als globale beheerder van uw directory.

2. Als uw organisatie meer dan één map heeft, selecteert u uw gebruikersnaam in Hallo rechterbovenhoek Hallo Azure-portal. Selecteer Hallo map waar u Azure AD Privileged Identity Management gebruikt.

3. Selecteer **meer services** en gebruik Hallo **Filter** textbox toosearch voor Azure AD Privileged Identity Management.

4. Controleer **pincode toodashboard** en klik vervolgens op **maken**. Hallo Privileged Identity Management-toepassing wordt geopend.

Nadat Azure AD Privileged Identity Management is ingesteld, ziet u Hallo navigatie blade wanneer u de toepassing hello opent.

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

Zie voor meer informatie en instructies voor het aan de slag met AAD PIM [Start met behulp van Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)

### <a name="azure-role-based-access-control"></a>Op rollen gebaseerde toegangsbeheer van Azure

[Azure op rollen gebaseerd toegangsbeheer](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) helpt Azure access tooAzure bronnen beheren door in te schakelen Hallo verlenen van toegang op basis van de toegewezen rol van de gebruiker van het Hallo-beheerders. U kunt taken in een team scheiden en verleen alleen Hallo hoeveelheid toegang toousers, groepen en toepassingen die zij nodig hebben tooperform hun werk.

Op rollen gebaseerde toegang kan worden verleend als toousers met hello Azure-portal, Azure-opdrachtregelprogramma's of Azure Management-API's.

Zie voor meer informatie over de basisprincipes van Azure RBAC [aan de slag met toegangsbeheer op basis van rollen in hello Azure-Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a>Hoe beheer ik Azure RBAC met PowerShell

U kunt de PowerShell-cmdlets toomanage Azure RBAC, met inbegrip van de volgende beheertaken Hallo gebruiken:

- Lijst met rollen

- Zien wie toegang heeft

- Toegang verlenen

- Toegang verwijderen

- Een aangepaste beveiligingsrol maken

- Acties voor een Resourceprovider ophalen

- Een aangepaste rol wijzigen

- Een aangepaste rol verwijderen

- Lijst met aangepaste rollen

Voor instructies over hoe toomanage Azure RBAC met PowerShell, Zie [toegang op basis van rollen beheren met Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).

### <a name="azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication

[Azure multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) is een verificatie-oplossing voor in twee stappen waarmee beveiliging toegang toodata en toepassingen, en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden. Het biedt krachtige verificatie via een reeks verificatiemethoden waaronder verificatie per telefoon, sms of mobiele app.

toodeploy MFA in hello Azure-cloud, moet u toofirst inschakelen en schakelt u verificatie in twee stappen voor gebruikers.

#### <a name="how-do-i-enable-azure-toouse-mfa"></a>Hoe kan ik Azure toouse MFA inschakelen?

Als uw gebruikers licenties met Azure multi-factor Authentication hebt, is er niets hoeft toodo tooturn op Azure MFA. Als dat niet het geval is, moet u een multi-factor Authentication-provider toocreate in uw directory. toodo dit als volgt te werk:

1. Selecteer **Active Directory** in Hallo klassieke Azure-portal (aangemeld als beheerder).

2. Selecteer **multi-factor Authentication-Providers.**

3. Selecteer **nieuw** en klik vervolgens onder **App-Services,** Selecteer **multi-factor Authentication-Provider.**

4. Selecteer **snelle invoer.**

5. Vul in het naamveld Hallo en selecteer een gebruiksmodel (per authenticatie of per ingeschakelde gebruiker).

6. Wijst een map aan welke Hallo MFA-Provider gekoppeld is.

7. Klik op Hallo **maken** knop.

![](media/protect-personal-data-identity-access-controls/quick-create.png)

Voor meer instructies voor het toomanage uw multi-factor Authentication-Provider Zie [aan de slag met een Azure multi-factor Authentication-Provider.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a>Hoe schakel ik verificatie in twee stappen voor gebruikers?

U kunt de verificatie in twee stappen voor alle aanmeldingen afdwingen of kunt u verificatie van voorwaardelijk beleid toorequire in twee stappen alleen wanneer bepaalde voorwaarden van toepassing.

Azure MFA inschakelen door het wijzigen van de status van gebruikers is Hallo traditionele aanpak voor het vereisen van verificatie in twee stappen. Alle Hallo-gebruikers die u inschakelt, hebben dezelfde verificatie van vereiste tooperform in twee stappen Hallo telkens wanneer ze zich aanmelden. Alle beleidsregels voor voorwaardelijke toegang die mogelijk gevolgen hebben voor die gebruiker inschakelen van een gebruiker worden onderdrukt.

Azure MFA inschakelen met een beleid voor voorwaardelijke toegang is een flexibelere benadering voor het vereisen van verificatie in twee stappen. U kunt beleid voor voorwaardelijke toegang die van toepassing toogroups zoals afzonderlijke gebruikers maken. Met een hoog risico groepen meer beperkingen dan laag risico groepen kunnen worden opgegeven of verificatie in twee stappen kan worden alleen vereist voor met een hoog risico cloud-apps en voor de laag risico die zijn overgeslagen. Voorwaardelijke toegang is echter een betaald functie van Azure Active Directory.

tooenable MFA door het wijzigen van de status van de gebruiker, Hallo te volgen:

1. Meld u toohello Azure-portal als beheerder.
2. Ga te**Azure Active Directory \> gebruikers en groepen \> alle gebruikers**.
3. Selecteer **multi-Factor Authentication**.
4. Zoeken naar Hallo gebruiker gewenste tooenable voor Azure MFA. Mogelijk moet u toochange weergave boven Hallo Hallo.
5. Controleer de naam van de Hallo vak volgende toohello van gebruiker.
6. Kies op Hallo rechts en onder snelle stappen, **inschakelen**.

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. Bevestig uw selectie in Hallo pop-upvenster dat wordt geopend.  Gebruikers voor wie MFA is ingeschakeld wordt gevraagd tooregister Hallo wanneer die ze zich aanmeldt.

tooenable Azure MFA met beleid voor voorwaardelijke toegang, Hallo te volgen:

1. Meld u toohello Azure-portal als beheerder.

2. Ga te**Azure Active Directory \> voorwaardelijke toegang**.

3. Selecteer **nieuw beleid**.

4. Onder **toewijzingen**, selecteer **gebruikers en groepen**. Gebruik Hallo **opnemen** en **uitsluiten** toospecify welke gebruikers en groepen worden beheerd door beleid Hallo tabbladen.

5. Onder **toewijzingen**, selecteer **Cloud-apps.** Kies te**omvatten alle cloud-apps**.
6.  Onder **toegangscontroles**, selecteer **Grant**. Kies **meervoudige authenticatie**.
7.  Schakel **beleid inschakelen** te**op** en selecteer vervolgens **opslaan**.

Voor informatie over hoe tooconfigure Azure MFA-instellingen tooset van Fraudewaarschuwingen, maakt een eenmalig overslaan, aangepaste spraakberichten gebruiken, caching configureren, goedgekeurde IP-adressen opgeven, app-wachtwoorden maken, onthoud MFA voor apparaten die gebruikers vertrouwt, en selecteer inschakelen verificatiemethoden, Zie [Azure multi-factor Authentication-instellingen configureren.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)

## <a name="next-steps"></a>Volgende stappen

- [Bevoegde toegang beveiligen in Azure AD](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [Veelgestelde vragen over Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [Probleemoplossing voor toegangsbeheer op basis van rollen](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
