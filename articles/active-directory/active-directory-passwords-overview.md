---
title: aaaAzure AD selfservice voor wachtwoordherstel overzicht | Microsoft Docs
description: Hoe kan selfservice wachtwoordherstel in Azure AD voor uw organisatie?
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 0efc291b1eeec0b7ae33ff5a7d9ed38e70c8be6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-self-service-password-reset-for-hello-it-professional"></a>Azure AD selfservice voor wachtwoordherstel voor Hallo IT-professionals

'Self-service' is een buzzword veroorzaakt rond binnen veel IT-afdelingen over Hallo wereld met verschillende betekenis. Hallo markt is flooded met producten die u toelaten om toomanage lokale groepen, wachtwoorden of gebruikersprofielen van Hallo cloud of on-premises.

Azure Active Directory (Azure AD) selfservice voor wachtwoordherstel (SSPR) stelt zichzelf uit elkaar met gebruiksgemak en implementatie. Azure AD zelf uw wachtwoord opnieuw instellen van een reeks mogelijkheden combineert die:

* Uw toomanage gebruikers kunnen hun eigen wachtwoord
  * Vanaf elk apparaat
  * Op elke locatie
  * Op elk gewenst moment
* Behouden van compatibiliteit met beleidsregels die u als beheerder definiëren

Als u klaar bent, u kunt aan de slag met Azure AD SSPR met onze [snel starten richtlijnen](active-directory-passwords-getting-started.md) en snel hebben uw gebruikers hun eigen wachtwoorden opnieuw instellen.

## <a name="what-is-possible"></a>Wat is er mogelijk

* **Selfservice voor wachtwoordherstel wijziging** kunnen eindgebruikers en beheerders toochange hun wachtwoorden zonder hulp van een beheerder
* **Ontgrendelen van het account selfservice** toounlock voor end-gebruikers kunnen hun eigen account zonder hulp van een beheerder
* **Selfservice voor wachtwoordherstel** kunnen eindgebruikers en beheerders tooreset hun wachtwoorden automatisch zonder hulp van een beheerder. Selfservice voor wachtwoordherstel vereist Azure AD Premium of Basic - [Azure Active Directory-edities](active-directory-editions.md).
* **Beheerder geïnitieerde wachtwoordherstel** kan een beheerder tooreset van de eindgebruiker of een andere beheerder het wachtwoord van binnen Hallo [Azure-portal](https://docs.microsoft.com/azure/azure-portal-overview)
* **Activiteit voor wachtwoord beheerrapporten** geven beheerders inzichten in activiteit voor wachtwoord opnieuw instellen en registratie plaatsvinden binnen hun organisatie - [-rapporten](active-directory-passwords-reporting.md)
* **Wachtwoord terugschrijven** beheer van on-premises wachtwoorden vanuit de cloud Hallo kunt zodat alle Hallo voorgaande scenario's kunnen worden uitgevoerd door of namens Hallo van federatieve of wachtwoord gebruikers gesynchroniseerd. Wachtwoord terugschrijven vereist [Azure AD Premium](active-directory-get-started-premium.md).

## <a name="why-choose-azure-ad-self-service-password-reset"></a>Waarom kiezen voor een Azure AD selfservice voor wachtwoordherstel

* **Kosten te verlagen** als helpdesk en ondersteuning voor assistentie voor wachtwoordherstel doorgaans is 20% van een IT-organisatie besteden
* **Ervaringen van eindgebruikers verbeteren** en **volume van de helpdesk verminderen** door middel van een end gebruikers Hallo power tooresolve hun eigen wachtwoordproblemen in één keer zonder een helpdesk aanroepen of een ondersteuningsaanvraag te openen.
* **Station mobility** als gebruikers hun wachtwoorden op elke willekeurige locatie kunnen herstellen.

## <a name="azure-ad-self-service-password-reset-availability"></a>Azure AD selfservice voor wachtwoordherstel beschikbaarheid

Azure AD zelf uw wachtwoord opnieuw instellen is beschikbaar in drie lagen, afhankelijk van uw abonnement.

* **Azure AD-vrije** – Cloud alleen-lezen beheerders kunnen hun eigen wachtwoorden opnieuw instellen
* **Azure AD Basic** of een **betaald Office 365-abonnement** – alleen in de Cloud-gebruikers en beheerders van cloudconfiguratie hun eigen wachtwoord kunnen herstellen
* **Azure AD Premium** : een gebruiker of beheerder, alleen in de cloud, inclusief federatieve of wachtwoord gebruikers gesynchroniseerd, kunnen hun eigen wachtwoorden opnieuw instellen. On-premises wachtwoorden vereisen wachtwoord terugschrijven toobe is ingeschakeld.

## <a name="azure-ad-self-service-password-reset-a-sum-of-hello-parts"></a>Azure AD selfservice voor wachtwoordherstel opnieuw instelt, wordt de som van Hallo delen

Selfservice voor wachtwoordherstel in Azure AD wordt samengesteld Hallo volgende onderdelen:

* **Management configuration-portal voor wachtwoord** waar u de opties voor de manier waarop wachtwoorden worden beheerd in uw tenant via hello Azure-portal kunt beheren
* **-Registratieportal voor wachtwoordherstel** waarmee gebruikers zelf kunnen registreren voor wachtwoordherstel
* **Portal voor wachtwoordherstel** waar gebruikers kunnen hun wachtwoord met behulp van Hallo uitdagingen die zijn gedefinieerd door Hallo beheerder en Hallo beantwoordt gebruikers hebt opgegeven.
* **Wijziging van de gebruikersportal wachtwoord** waar gebruikers hun eigen wachtwoord kunnen wijzigen door het oude wachtwoord invoeren en het geven van een nieuw wachtwoord
* **Wachtwoord-rapporten** waar beheerders kunnen weergeven en analyseren van de activiteit voor wachtwoord rapporten voor hun tenants in hello Azure-portal
* **Wachtwoord terugschrijven tooon lokale met Azure AD Connect** kunt u tooenable beheer van on-premises gefedereerd, of het wachtwoord gesynchroniseerd gebruikers uit Hallo cloud

## <a name="azure-ad-pricing-sla-updates-and-roadmap"></a>Azure AD-prijzen, SLA, updates en roadmap

Meer details over deze onderwerpen vindt u op Hallo volgende pagina 's

* [**Prijsinformatie voor Azure AD**](https://azure.microsoft.com/pricing/details/active-directory/)
* [**Prijzen van Office 365**](https://products.office.com/compare-all-microsoft-office-products?tab=2)
* [**Azure Service Level Agreements**](https://azure.microsoft.com/support/legal/sla/)
* [**Service Level Agreement voor Microsoft Online Services**](http://go.microsoft.com/fwlink/?LinkID=272026&clcid=0x409)
* [**Azure-Updates**](https://azure.microsoft.com/updates/)
* [**Overzicht van Azure**](https://www.microsoft.com/cloud-platform/roadmap-recently-available)

## <a name="next-steps"></a>Volgende stappen

Hallo volgende koppelingen vindt u aanvullende informatie met betrekking tot het wachtwoord opnieuw instellen met behulp van Azure AD

* [**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD 
* [**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren
* [**Gegevens** ](active-directory-passwords-data.md) - begrijpen Hallo-gegevens die nodig is en hoe deze wordt gebruikt voor wachtwoordbeheer
* [**Implementatie** ](active-directory-passwords-best-practices.md) -plannen en implementeren van SSPR tooyour gebruikers via Hallo richtlijnen hier gevonden
* [**Aanpassen** ](active-directory-passwords-customize.md) -Hallo uiterlijk Hallo SSPR ervaring voor uw bedrijf aanpassen.
* [**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken
* [**Technische diepgaand** ](active-directory-passwords-how-it-works.md) -Ga achter Hallo gordijn toounderstand hoe het werkt
* [**Veelgestelde vragen**](active-directory-passwords-faq.md): hoe? Hoe komt dat? Wat? Waar? Wie? Wanneer? -Beantwoordt tooquestions gewenste altijd tooask
* [**Problemen met** ](active-directory-passwords-troubleshoot.md) -informatie over hoe tooresolve algemene problemen zien we met SSPR

