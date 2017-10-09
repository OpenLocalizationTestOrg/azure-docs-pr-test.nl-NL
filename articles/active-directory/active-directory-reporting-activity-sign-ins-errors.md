---
title: activiteit aaaSign in rapport foutcodes in hello Azure Active Directory-portal | Microsoft Docs
description: Naslaginformatie over foutcodes voor aanmeldactiviteitenrapporten.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: a0ca5b706bfeb0c7ce669712468a083a394712b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-report-error-codes-in-hello-azure-active-directory-portal"></a>Aanmeldingsactiviteiten rapport foutcodes in hello Azure Active Directory-portal

Met Hallo informatie verstrekt door Hallo gebruiker aanmeldingen rapport kunt vinden u antwoorden tooquestions zoals:

- Wie heeft zich aangemeld met Azure Active Directory?
- Bij welke apps hebben gebruikers zich aangemeld?
- Welke aanmeldingen zijn mislukt en waarom?

Dit onderwerp lijsten Hallo foutcodes en beschrijvingen van gerelateerde Hallo. 

## <a name="how-can-i-display-failed-sign-ins"></a>Hoe kan ik mislukte aanmeldingen weergeven? 

Uw eerste vermelding punt tooall aanmelden activiteiten gegevens  **[aanmeldingen](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)**  in Hallo **activiteit** sectie van **Azure Active**.


![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins-errors/61.png "Aanmeldingsactiviteit")


In het aanmeldingenrapport kunt u alle mislukte aanmeldingen weergeven door **Mislukt** te selecteren als **Aanmeldstatus**.


![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins-errors/06.png "Aanmeldingsactiviteit")

Op een item in de lijst Hallo weergegeven, wordt geopend Hallo **Activiteitsdetails: aanmeldingen** blade. Deze weergave biedt u alle Hallo details die Azure Active Directory over aanmeldingen houdt, met inbegrip van Hallo **aanmelden foutcode** en een **reden voor fout**.

![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins-errors/05.png "Aanmeldingsactiviteit")


Als een alternatieve toousing hello Azure portal tooaccess Hallo aanmeldingen gegevens, kunt u ook hello gebruiken [rapportage-API](active-directory-reporting-api-getting-started-azure-portal.md).


Hallo volgende sectie biedt een volledig overzicht van alle mogelijke fouten en Hallo beschrijvingen gerelateerd. 

## <a name="error-codes"></a>Foutcodes

| Fout| Beschrijving |
| --- | --- |
| 50001| Hallo service-principal met de naam X is niet gevonden in met de naam Y Hallo-tenant. Dit kan gebeuren als het Hallo-toepassing is niet geïnstalleerd door de beheerder Hallo van Hallo-tenant. Of Resource-principal is niet gevonden in de map Hallo of is ongeldig|
| 50008| SAML-verklaring zijn ontbreekt of is niet juist geconfigureerd in Hallo-token.|
| 50011| Hallo antwoordadres ontbreekt, onjuist geconfigureerd of komt niet overeen met de antwoordadressen die zijn geconfigureerd voor de toepassing hello.|
| 50053| Account is vergrendeld omdat de gebruiker heeft geprobeerd toosign in te vaak aangemeld met een onjuiste gebruikersnaam of wachtwoord.|
| 50054| Er is een oud wachtwoord gebruikt voor verificatie.|
| 50055| Het opgegeven wachtwoord is ongeldig of verlopen.|
| 50057| Het gebruikersaccount is uitgeschakeld.|
| 50058| Er is geen informatie over de identiteit van de gebruiker is gevonden bij opgegeven referenties of de gebruiker niet in de tenant gevonden is of een achtergrond-in-aanvraag is verzonden, maar er is geen gebruiker is aangemeld of -Service kan geen tooauthenticate Hallo gebruiker is.|
| 50074| Sterke verificatie (tweede factor) is vereist|
| 50079| Gebruiker moet tooenroll voor de tweede factorverificatie|
| 50126| Gebruikersnaam of wachtwoord is ongeldig of on-premises gebruikersnaam of wachtwoord is ongeldig.|
| 50131| Wordt gebruikt voor verschillende fouten voor voorwaardelijke toegang. Ongeldige Windows-apparaat bijvoorbeeld status aanvraag geblokkeerd vanwege toosuspicious activiteit, toegangsbeleid en het beveiligingsbeleid beslissingen te nemen.|
| 50133| Sessie is ongeldig vanwege tooexpiration of recente wachtwoord wijzigen.|
| 50144| Het Active Directory-wachtwoord van de gebruiker is verlopen.|
| 65001| X-toepassing heeft geen machtiging tooaccess toepassing Y of Hallo machtiging is ingetrokken. Of hello gebruiker of beheerder niet heeft ingestemd toouse Hallo toepassing met ID X. Send een interactieve autorisatieaanvraag voor deze gebruiker en de resource. Of het Hallo-gebruiker of beheerder niet toouse Hallo toepassing met ID X. Send een autorisatie aanvraag tooyour tenant admin tooact namens Hallo App heeft ingestemd: Y voor Resource: Z.|
| 65005| Hallo toepassing vereist resource toegangslijst bevat geen toepassingen kunnen worden gedetecteerd door Hallo resource of Hallo clienttoepassing toegang tooresource die niet is opgegeven in de lijst met vereiste bron toegang of grafiek service geretourneerd onjuiste heeft aangevraagd aanvraag of bron is niet gevonden.|
| 70001| Hallo-toepassing met de naam X is niet gevonden in met de naam Y Hallo-tenant. Dit kan gebeuren als Hallo toepassing nog niet is geïnstalleerd door Hallo beheerder van de tenant Hallo of instemming tooby elke gebruiker in het Hallo-tenant. Hebt misschien u uw tenant toohello verkeerde van authenticatie-aanvraag verzonden.|
| 80001| Er is geen verificatieagent beschikbaar.|
| 80002| Er is een time-out opgetreden bij de wachtwoordvalidatie voor de verificatieagent.|
| 80003| Ongeldig antwoord ontvangen door de verificatieagent.|
| 80004| Onjuiste UPN (user principal name) gebruikt voor aanmeldingsaanvraag.|
| 80005| Verificatieagent: er is een fout opgetreden.|
| 80007| Verificatie-Agent kan geen tooconnect tooActive Directory.|
| 80010| Wachtwoord voor de Agent kan geen toodecrypt verificatie.|
| 81001| Kerberos-ticket van de gebruiker is te groot.|
| 81002| Kerberos-ticket van de gebruiker kan niet toovalidate.|
| 81003| Kerberos-ticket van de gebruiker kan niet toovalidate.|
| 81004| Poging tot Kerberos-verificatie is mislukt.|
| 81008| Kerberos-ticket van de gebruiker kan niet toovalidate.|
| 81009| Kerberos-ticket van de gebruiker kan niet toovalidate.|
| 81010| Naadloze eenmalige aanmelding is mislukt omdat van Hallo gebruiker Kerberos-ticket is verlopen of ongeldig is.|
| 81011| Kan geen toofind gebruikersobject op basis van de informatie in de Kerberos-ticket Hallo van de gebruiker.|
| 81012| Hallo gebruiker probeert toosign in tooAzure AD wijkt af van Hallo gebruiker is aangemeld bij het Hallo-apparaat.|
| 81013| Kan geen toofind gebruikersobject op basis van de informatie in de Kerberos-ticket Hallo van de gebruiker.|
| 90014| In verschillende gevallen gebruikt wanneer een veld met het verwachte niet aanwezig in het Hallo-referentie is.|
| 90093| Een grafiek met niet-toegestane foutcode voor de aanvraag Hallo geretourneerd.|



## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie, Hallo [aanmelden activiteitsrapporten in Azure Active Directory-beheerportal Hallo](active-directory-reporting-activity-sign-ins.md).

