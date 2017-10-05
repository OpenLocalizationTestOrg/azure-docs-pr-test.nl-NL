---
title: Azure AD selfservice voor wachtwoordherstel overzicht | Microsoft Docs
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
ms.openlocfilehash: 3903c53b78e61b380bb812a9d3ade694655b5afb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-self-service-password-reset-for-the-it-professional"></a>Azure AD selfservice voor wachtwoordherstel voor IT-professionals

'Self-service' is een buzzword veroorzaakt rond binnen veel IT-afdelingen overal ter wereld met verschillende betekenis. De markt wordt overspoeld met producten voor het beheren van lokale groepen, wachtwoorden of gebruikersprofielen vanuit de cloud of on-premises.

Azure Active Directory (Azure AD) selfservice voor wachtwoordherstel (SSPR) stelt zichzelf uit elkaar met gebruiksgemak en implementatie. Azure AD zelf uw wachtwoord opnieuw instellen van een reeks mogelijkheden combineert die:

* Toestaan dat gebruikers hun eigen wachtwoord beheren
  * Vanaf elk apparaat
  * Op elke locatie
  * Op elk gewenst moment
* Behouden van compatibiliteit met beleidsregels die u als beheerder definiëren

Als u klaar bent, u kunt aan de slag met Azure AD SSPR met onze [snel starten richtlijnen](active-directory-passwords-getting-started.md) en snel hebben uw gebruikers hun eigen wachtwoorden opnieuw instellen.

## <a name="what-is-possible"></a>Wat is er mogelijk

* **Selfservice voor wachtwoordherstel wijziging** kunnen eindgebruikers en beheerders hun wachtwoorden zonder hulp van een beheerder wijzigen
* **Ontgrendelen van het account selfservice** kunnen eindgebruikers hun eigen account zonder hulp van een beheerder ontgrendelen
* **Selfservice voor wachtwoordherstel** kunnen eindgebruikers en beheerders om in te stellen hun wachtwoorden automatisch zonder hulp van een beheerder. Selfservice voor wachtwoordherstel vereist Azure AD Premium of Basic - [Azure Active Directory-edities](active-directory-editions.md).
* **Beheerder geïnitieerde wachtwoordherstel** kan een beheerder opnieuw instellen van de eindgebruiker of een andere beheerder wachtwoord vanuit de [Azure-portal](https://docs.microsoft.com/azure/azure-portal-overview)
* **Activiteit voor wachtwoord beheerrapporten** geven beheerders inzichten in activiteit voor wachtwoord opnieuw instellen en registratie plaatsvinden binnen hun organisatie - [-rapporten](active-directory-passwords-reporting.md)
* **Wachtwoord terugschrijven** kunt beheer van on-premises wachtwoorden vanuit de cloud zodat alle het voorgaande scenario's kunnen worden uitgevoerd door of namens van federatieve of wachtwoord gebruikers gesynchroniseerd. Wachtwoord terugschrijven vereist [Azure AD Premium](active-directory-get-started-premium.md).

## <a name="why-choose-azure-ad-self-service-password-reset"></a>Waarom kiezen voor een Azure AD selfservice voor wachtwoordherstel

* **Kosten te verlagen** als helpdesk en ondersteuning voor assistentie voor wachtwoordherstel doorgaans is 20% van een IT-organisatie besteden
* **Ervaringen van eindgebruikers verbeteren** en **volume van de helpdesk verminderen** doordat eindgebruikers de stroom op problemen met hun eigen wachtwoord in één keer zonder een helpdesk aanroepen of een ondersteuningsaanvraag te openen.
* **Station mobility** als gebruikers hun wachtwoorden op elke willekeurige locatie kunnen herstellen.

## <a name="azure-ad-self-service-password-reset-availability"></a>Azure AD selfservice voor wachtwoordherstel beschikbaarheid

Azure AD zelf uw wachtwoord opnieuw instellen is beschikbaar in drie lagen, afhankelijk van uw abonnement.

* **Azure AD-vrije** – Cloud alleen-lezen beheerders kunnen hun eigen wachtwoorden opnieuw instellen
* **Azure AD Basic** of een **betaald Office 365-abonnement** – alleen in de Cloud-gebruikers en beheerders van cloudconfiguratie hun eigen wachtwoord kunnen herstellen
* **Azure AD Premium** : een gebruiker of beheerder, alleen in de cloud, inclusief federatieve of wachtwoord gebruikers gesynchroniseerd, kunnen hun eigen wachtwoorden opnieuw instellen. On-premises wachtwoorden vereisen wachtwoord terugschrijven worden ingeschakeld.

## <a name="azure-ad-self-service-password-reset-a-sum-of-the-parts"></a>Azure AD zelf uw wachtwoord opnieuw instelt, wordt de som van de onderdelen

Selfservice voor wachtwoordherstel in Azure AD wordt samengesteld uit de volgende onderdelen:

* **Management configuration-portal voor wachtwoord** waar u de opties voor de manier waarop wachtwoorden worden beheerd in uw tenant via Azure portal kunt beheren
* **-Registratieportal voor wachtwoordherstel** waarmee gebruikers zelf kunnen registreren voor wachtwoordherstel
* **Portal voor wachtwoordherstel** waar gebruikers kunnen hun wachtwoord met behulp van de uitdagingen die zijn gedefinieerd door de beheerder en de antwoorden gebruikers hebt opgegeven.
* **Wijziging van de gebruikersportal wachtwoord** waar gebruikers hun eigen wachtwoord kunnen wijzigen door het oude wachtwoord invoeren en het geven van een nieuw wachtwoord
* **Wachtwoord-rapporten** waar beheerders kunnen weergeven en analyseren van de activiteit voor wachtwoord rapporten voor hun tenants in de Azure portal
* **Wachtwoord terugschrijven naar on-premises met Azure AD Connect** kunt u beheer van on-premises gefedereerd, inschakelen of het wachtwoord gesynchroniseerd gebruikers vanuit de cloud

## <a name="azure-ad-pricing-sla-updates-and-roadmap"></a>Azure AD-prijzen, SLA, updates en roadmap

Meer details over deze onderwerpen vindt u op de volgende pagina 's

* [**Prijsinformatie voor Azure AD**](https://azure.microsoft.com/pricing/details/active-directory/)
* [**Prijzen van Office 365**](https://products.office.com/compare-all-microsoft-office-products?tab=2)
* [**Azure Service Level Agreements**](https://azure.microsoft.com/support/legal/sla/)
* [**Service Level Agreement voor Microsoft Online Services**](http://go.microsoft.com/fwlink/?LinkID=272026&clcid=0x409)
* [**Azure-Updates**](https://azure.microsoft.com/updates/)
* [**Overzicht van Azure**](https://www.microsoft.com/cloud-platform/roadmap-recently-available)

## <a name="next-steps"></a>Volgende stappen

De volgende koppelingen bieden aanvullende informatie over wachtwoordherstel met behulp van Azure AD

* [**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD 
* [**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren
* [**Gegevens**](active-directory-passwords-data.md): informatie over de gegevens die nodig zijn en hoe deze worden gebruikt voor wachtwoordbeheer
* [**Implementatie**](active-directory-passwords-best-practices.md): SSPR plannen en implementeren voor uw gebruikers op basis van de hier gegeven informatie
* [**Aanpassen**](active-directory-passwords-customize.md): het uiterlijk van de ervaring van self-service voor wachtwoordherstel aanpassen voor uw bedrijf.
* [**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken
* [**Gedetailleerde technische informatie**](active-directory-passwords-how-it-works.md): neem een kijkje achter de schermen om te begrijpen hoe het werkt
* [**Veelgestelde vragen**](active-directory-passwords-faq.md): hoe? Hoe komt dat? Wat? Waar? Wie? Wanneer? - Antwoorden op vragen die u altijd wilde stellen
* [**Probleemoplossing**](active-directory-passwords-troubleshoot.md): informatie over het oplossen van algemene problemen die optreden bij de self-service voor wachtwoordherstel

