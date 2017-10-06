---
title: aaaBranding richtlijnen voor toepassingen | Microsoft Docs
description: Een uitgebreide handleiding toodeveloper gerichte resources voor Azure Active Directory
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 72f4e464-1352-4a49-a18f-c37f58e7d5c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: e43f884c736a0dcb2e6e51293962ef1e2636ad70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="branding-guidelines-for-applications"></a>Huisstijlrichtlijnen voor toepassingen
Dit onderwerp wordt besproken Hallo huisstijl richtlijnen die moet u bij het ontwikkelen van toepassingen met Azure Active Directory (Azure AD). Deze richtlijnen helpt uw klanten directe wanneer ze toouse willen hun werk- of schoolaccount die worden beheerd in Azure AD of een persoonlijk account voor de toepassing zich kunnen registreren en aanmelden tooyour.

## <a name="personal-accounts-vs-work-or-school-accounts-from-microsoft"></a>Persoonlijke accounts versus werk- of schoolaccounts van Microsoft
Microsoft beheert de twee typen gebruikersaccounts:

* **Persoonlijke accounts** (voorheen Windows Live ID). Deze accounts vertegenwoordigen Hallo relatie tussen *afzonderlijke* gebruikers en Microsoft en zijn tooaccess consumentenapparaten en services van Microsoft gebruikt. Deze accounts zijn bedoeld voor persoonlijk gebruik.
* **Werk- of schoolaccount accounts.** Deze accounts worden beheerd door Microsoft namens organisaties die gebruikmaken van Azure Active Directory. Deze accounts zijn gebruikte toosign in tooOffice 365 en andere zakelijke services van Microsoft.

Microsoft werk-of schoolaccounts meestal zijn tooend gebruikers (werknemers, studenten, federal werknemers) toegewezen door hun organisatie (bedrijf, school, overheidsinstelling). Deze accounts zijn dat ofwel master rechtstreeks in de cloud hello, in hello Azure AD-platform of gesynchroniseerde tooAzure AD uit een on-premises adreslijst, zoals Windows Server Active Directory. Microsoft is Hallo *vallen* Hallo werk of schoolaccounts, maar Hallo accounts zijn eigendom en wordt beheerd door Hallo-organisatie.

## <a name="referring-tooazure-ad-accounts-in-your-application"></a>Verwijzende tooAzure AD-accounts in uw toepassing
Microsoft biedt geen tonen eindgebruikers toohello Azure of Hallo Active Directory-merken en geen van beide moet u.

* Nadat gebruikers zijn aangemeld, moet u de naam en het logo zoveel mogelijk van Hallo organisatie. Dit is beter dan het gebruik van algemene voorwaarden zoals 'uw organisatie'.
* Wanneer gebruikers niet bent aangemeld, raadpleegt u de accounts tootheir als ' werk- of schoolaccounts ' en gebruik Hallo Microsoft-logo tooconvey dat deze accounts worden beheerd door Microsoft. Gebruik geen voorwaarden zoals 'enterprise-account', 'business-account' of 'zakelijke account' die gebruiker verwarring.

## <a name="user-account-pictogram"></a>Pictogram voor gebruiker-account
In een eerdere versie van deze richtlijnen raden wij met behulp van een pictogram 'blue badge'. Op basis van feedback van gebruikers- en developer, nu het beste Hallo gebruik van Microsoft-logo Hallo in plaats daarvan. Dit helpt gebruikers begrijpen die ze Hallo-account die ze met Office 365 of andere Microsoft business services toosign in tooyour app gebruiken opnieuw kunnen gebruiken.

## <a name="signing-up-and-signing-in-with-azure-ad"></a>Aanmelden en aanmelden met Azure AD
Uw app moet u wellicht afzonderlijke paden voor aanmelden en aanmelden en Hallo uit te voeren bieden een visuele richtlijn voor beide scenario's.

**Als uw app eindgebruiker aanmelden (bijvoorbeeld vrije-tootrial of freemium model) ondersteunt**: U ziet een **aanmelden** knop waarmee gebruikers tooaccess uw app voor hun werk- of een persoonlijk account. Azure AD wordt een toestemming vragen Hallo ze toegang krijgen uw app tot eerst weergegeven.

**Als uw app vereist machtigingen die alleen Administrators met instemmen kunnen of dat uw app vereist organisatie licentieverlening**: scheidt u overname van de beheerder van de gebruiker zich aanmelden. Hallo **knop 'ophalen deze app'** zal leiden admins toosign in vervolgens vraagt u ze toogrant toestemming namens gebruikers in hun organisatie. Dit is een bijkomend voordeel van het onderdrukken van eindgebruikers toestemming prompts tooyour app Hallo.

## <a name="visual-guidance-for-app-acquisition"></a>Visual richtlijnen voor de aanschaf van app
De koppeling 'hello app ophalen' hello gebruiker toohello Azure AD verlenen toegang moet omleiden (autoriseren) pagina, tooallow tooauthorize voor een organisatie-beheerder toegang tot uw app toohave van tootheir organisatie gegevens die wordt gehost door Microsoft. Meer informatie over hoe toorequest toegang worden besproken in Hallo [toepassingen integreren met Azure Active Directory](active-directory-integrating-applications.md) artikel.

Nadat beheerders tooyour app instemt, kunnen ze tooadd kiezen het tootheir Office 365 app linksboven gebruikerservaring (toegankelijk uit Hallo waffle en [https://portal.office.com/myapps](https://portal.office.com/myapps)). Als u deze mogelijkheid tooadvertise wilt, kunt u voorwaarden zoals 'Deze app tooyour organisatie toevoegen' en een knop als volgt weergegeven:

![Toepassingstypen en scenario 's](./media/active-directory-branding-guidelines/add-to-my-org.png)

We raden echter aan dat u schrijft verklarende tekst in plaats van knoppen. Bijvoorbeeld:

> *Als u al Office 365 of andere zakelijke services van Microsoft gebruikt, verleent u gewoon < your_app_name > toegang tooyour organisatiegegevens. Hierdoor kan uw gebruikers tooaccess < your_app_name > met hun bestaande werkaccounts.*
> 
> 

## <a name="visual-guidance-for-sign-in"></a>Visuele aanwijzingen voor aanmelden
Uw app een aanmelding moet worden weergegeven op de knop waarmee gebruikers toohello aanmelden eindpunt dat overeenkomt met toohello protocol waarmee u toointegrate met Azure AD worden omgeleid. Hallo volgende sectie worden details weergegeven over wat die knop als eruitzien moet.

### <a name="pictogram-and-sign-in-with-microsoft"></a>Pictogram en 'Aanmelden met Microsoft'
Het Hallo-koppeling van Microsoft-logo Hallo en Hallo 'Aanmelding in met Microsoft' voorwaarden die een unieke vertegenwoordigt Azure AD onder andere id-providers die kan ondersteuning voor uw app's. Als u geen voldoende ruimte voor 'Aanmelding in met Microsoft', is het ok tooshorten deze te 'aanmelden'.

![Toepassingstypen en scenario 's](./media/active-directory-branding-guidelines/sign-in-with-microsoft-light.png)

![Toepassingstypen en scenario 's](./media/active-directory-branding-guidelines/sign-in-light.png)

U kunt ook een donker kleurenschema voor Hallo knoppen.

![Toepassingstypen en scenario 's](./media/active-directory-branding-guidelines/sign-in-with-microsoft-dark.png)

![Toepassingstypen en scenario 's](./media/active-directory-branding-guidelines/sign-in-dark.png)

## <a name="branding-dos-and-donts"></a>De huisstijl van taken en niet moet doen
**Voer** gebruik 'werk of school-account' in combinatie met Hallo 'Aanmelding in met Microsoft' knop tooprovide aanvullende uitleg toohelp eindgebruikers herkennen of software kan worden gebruikt. **Geen** gebruiken van andere voorwaarden zoals 'enterprise-account', 'business-account' of 'zakelijke account'.

**Geen** 'Office 365-ID' of 'Azure-ID' gebruiken. Office 365 is ook Hallo-naam van een consumer aanbieding van Microsoft Azure AD niet voor verificatie gebruiken.

**Geen** alter Hallo Microsoft-logo.

**Geen** eindgebruikers toohello Azure of Active Directory merken blootstellen. Het is echter wel ok toouse deze voorwaarden met ontwikkelaars, IT-professionals en beheerders.

## <a name="navigation-dos-and-donts"></a>Tips voor navigatie
**Voer** bieden een manier voor gebruikers toosign uit en schakel tooanother gebruikersaccount. Hoewel de meeste mensen één persoonlijke account van Microsoft/Facebook/Google/Twitter, zijn vaak mensen gekoppeld aan meer dan één organisatie. Ondersteuning voor meerdere gebruikers aangemeld is binnenkort beschikbaar.

