---
title: aaaAutomated SaaS app gebruikers inrichten in Azure AD | Microsoft Docs
description: Een inleiding toohow kunt u Azure AD tooautomatically inrichten, inrichten ongedaan, en werk continu gebruikersaccounts voor meerdere derde SaaS-toepassingen.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 58c5fa2d-bb33-4fba-8742-4441adf2cb62
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: curtand
ms.openlocfilehash: a1f3ecdd513e2b603f8ad9901e9f551b3b982b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-user-provisioning-and-deprovisioning-toosaas-applications-with-azure-active-directory"></a>Gebruiker inrichting en het opheffen van inrichting tooSaaS toepassingen met Azure Active Directory automatiseren
## <a name="what-is-automated-user-provisioning-for-saas-apps"></a>Wat is geautomatiseerde gebruikersinrichting voor SaaS-apps?
Azure Active Directory (Azure AD) kunt u tooautomate Hallo maken, onderhouden en verwijderen van de gebruikers-id's in de cloud ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) toepassingen zoals Dropbox, Salesforce en ServiceNow.

**Hieronder volgen enkele voorbeelden van wat deze functie u toodo kunt:**

* Automatisch nieuwe accounts maken in Hallo juiste SaaS-apps voor nieuwe gebruikers wanneer ze bij uw team.
* Accounts van SaaS-apps automatisch deactiveren wanneer gebruikers onvermijdelijk Hallo-team laten.
* Ervoor dat Hallo identiteiten in uw SaaS-apps van toodate op basis van wijzigingen in de map Hallo worden gehouden.
* Voorzien in een niet-gebruikers objecten, zoals groepen, tooSaaS-apps die deze ondersteunen.

**Geautomatiseerde gebruikersinrichting bevat ook Hallo functionaliteit te volgen:**

* Hallo mogelijkheid toomatch bestaande identiteiten tussen Azure AD en SaaS-apps.
* Aanpassing opties toohelp Azure AD passen Hallo huidige configuraties van Hallo SaaS-apps die momenteel wordt gebruikt door uw organisatie.
* Optionele e-mailwaarschuwingen voor fouten bij het inrichten.
* Rapportage- en activiteit logboeken toohelp met bewaking en probleemoplossing.

## <a name="why-use-automated-provisioning"></a>Waarom een geautomatiseerde inrichting gebruiken?
Sommige algemene motivaties voor het gebruik van deze functie zijn onder andere:

* tooavoid hello kosten, inefficiënte en menselijke fouten die zijn gekoppeld aan de handmatige Inrichtingsmethode processen.
* toosecure uw organisatie door het verwijderen van onmiddellijk identiteit van gebruikers van de belangrijkste SaaS-apps wanneer ze Hallo organisatie verlaten.
* een aantal bulksgewijs gebruikers tooeasily importeren in een bepaalde SaaS-toepassing.
* tooenjoy hello gemak van uw oplossing uitvoeren op Hallo dezelfde app-beleidsregels die u hebt gedefinieerd voor Azure AD eenmalige aanmelding.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen
**Hoe vaak directory wijzigingen toohello SaaS-app in Azure AD schrijven?**

Azure AD gecontroleerd op wijzigingen om tooten de vijf minuten. Als Hallo SaaS app retourneert verschillende fouten (zoals net als bij Hallo ongeldige beheerdersreferenties), klikt u vervolgens in Azure AD geleidelijk de frequentie tooup tooonce per dag totdat Hallo fouten zijn opgelost vertragen.

**Hoe lang duurt tooprovision Mijn gebruikers?**

Incrementele wijzigingen gebeuren bijna onmiddellijk maar als u tooprovision probeert de meeste van uw directory en vervolgens deze afhankelijk is van Hallo aantal gebruikers en groepen die u hebt. Kleine mappen slechts een paar minuten duren, middelgrote mappen kunnen enkele minuten duren en zeer grote directory's kunnen enige uren duren.

**Hoe kan ik de voortgang van de huidige inrichtingstaak Hallo Hallo bijhouden**

Hallo-Account wordt ingericht rapport onder Hallo rapporten gedeelte van uw directory, kunt u bekijken. Een andere optie is toovisit Hallo dashboardtabblad voor Hallo SaaS-toepassing die u inrichting tot en zoek onder aan de onderkant Hallo van Hallo pagina in de sectie 'integratiestatus' Hallo.

**Hoe weet ik als gebruikers tooget correct ingericht mislukt?**

Hallo einde van Hallo is configuratiewizard inrichting er een optie toosubscribe tooemail meldingen voor het inrichten van fouten. U kunt ook controleren Hallo foutenrapport inrichting toosee welke gebruikers toobe ingericht is mislukt en waarom.

**Azure AD kan schrijven wijzigingen uit Hallo SaaS app back toohello directory?**

Voor de meeste SaaS-apps is inrichting alleen uitgaand, wat betekent dat gebruikers van Hallo directory toohello toepassing worden geschreven en wijzigingen van de toepassing hello kunnen niet worden teruggeschreven toohello directory. Voor [Workday](https://msdn.microsoft.com/library/azure/dn762434.aspx)echter inrichting is inkomend alleen-lezen, wat inhoudt dat dat gebruikers geïmporteerd in de directory Hallo uit Workday zijn en ook wijzigingen in de directory Hallo doen niet ophalen teruggeschreven naar werkdag.

**Hoe kan ik feedback toohello engineeringteam verzenden?**

Neem contact met ons opnemen via Hallo [forum met feedback van Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/).

## <a name="how-does-automated-provisioning-work"></a>Hoe werkt geautomatiseerde inrichting?
Azure AD levert gebruikers tooSaaS apps door verbinding te maken tooprovisioning eindpunten geleverd door de leverancier van elke toepassing. Deze eindpunten dat Azure AD-tooprogrammatically maken, bijwerken en verwijderen van gebruikers. Hieronder volgt een kort overzicht van Hallo verschillende stappen dat nodig is Azure AD tooautomate inrichting.

1. Wanneer u inrichting voor een toepassing voor Hallo eerst inschakelen, worden Hallo van de volgende activiteiten uitgevoerd:
   * Azure AD probeert toomatch alle bestaande gebruikers in Hallo SaaS-app met hun overeenkomstige identiteiten in Hallo-directory. Wanneer een gebruiker is gekoppeld, zijn ze *niet* automatisch ingeschakeld voor eenmalige aanmelding. Om een gebruiker toohave access toohello-toepassing, moeten ze worden expliciet toegewezen toohello app in Azure AD rechtstreeks of via een groepslidmaatschap.
   * Als u al hebt opgegeven welke gebruikers toohello toepassing moeten worden toegewezen, en als Azure AD mislukt toofind bestaande accounts voor gebruikers, Azure AD wordt geen nieuwe accounts inrichten voor hen in Hallo-toepassing.
2. Zodra het Hallo initiële synchronisatie is voltooid zoals hierboven beschreven, wordt in Azure AD elke 10 minuten voor de volgende wijzigingen Hallo controleren:
   * Als u nieuwe gebruikers zijn toegewezen toohello toepassing (rechtstreeks of via een groepslidmaatschap), dan wordt een nieuwe account in de SaaS-app Hallo ingericht.
   * Als een gebruiker toegang is verwijderd, wordt hun account in Hallo SaaS-app wordt gemarkeerd als uitgeschakeld (gebruikers nooit volledig verwijderd, u te beschermen tegen gegevensverlies in geval van een onjuiste configuratie Hallo).
   * Als een gebruiker onlangs toohello toepassing toegewezen is en al een account in Hallo SaaS-app was, dat account wordt gemarkeerd als ingeschakeld en bepaalde gebruikerseigenschappen kunnen worden bijgewerkt als ze verouderd in vergelijking toohello directory zijn.
   * Als de informatie van een gebruiker (zoals telefoonnummer, kantoorlocatie, enzovoort) is gewijzigd in Hallo directory, wordt er ook die informatie in de SaaS-toepassing hello worden bijgewerkt.

Voor meer informatie over hoe kenmerken tussen Azure AD zijn toegewezen en uw SaaS-app, Zie Hallo artikel op [kenmerktoewijzingen aanpassen](active-directory-saas-customizing-attribute-mappings.md).

## <a name="list-of-apps-that-support-automated-user-provisioning"></a>Lijst met Apps die ondersteuning bieden voor het automatisch inrichten van gebruiker
Alle Hallo 'Aanbevolen' apps in Azure AD-toepassingsgalerie Hallo ondersteunen geautomatiseerde gebruikersinrichting. [Hallo-lijst met aanbevolen apps kan hier worden weergegeven.](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)

In de volgorde voor een toepassing toosupport automatisch gebruikers inrichten, moet deze eerst bieden Hallo nodig eindpunten voor het maken van het externe programma's tooautomate hello, onderhoud en verwijdering van gebruikers. Er zijn daarom niet alle SaaS-apps compatibel met deze functie. Voor apps die dit ondersteunen, Hallo engineering-team van Azure AD wordt vervolgens kunnen toobuild een inrichting connector toothose apps, en dit werk is geplaatst door Hallo vereisten van de huidige en potentiële klanten.

toocontact hello Azure AD-engineering toorequest inrichting ondersteuning voor aanvullende toepassingen in een team, verzend een bericht via Hallo [forum met feedback van Azure Active Directory](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/category/172035-user-provisioning).

## <a name="related-articles"></a>Verwante artikelen
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [Kenmerktoewijzingen voor gebruikers inrichten aanpassen](active-directory-saas-customizing-attribute-mappings.md)
* [Expressies voor kenmerktoewijzingen schrijven](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Bereikfilters voor gebruikers inrichten](active-directory-saas-scoping-filters.md)
* [Met behulp van SCIM tooenable automatische inrichting van gebruikers en groepen van Azure Active Directory-tooapplications](active-directory-scim-provisioning.md)
* [Meldingen inrichten van een account](active-directory-saas-account-provisioning-notifications.md)
* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps](active-directory-saas-tutorial-list.md)

