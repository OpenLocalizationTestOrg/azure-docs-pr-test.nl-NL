---
title: Active Directory-rapportage aaaAzure | Microsoft Docs
description: Biedt een algemeen overzicht van Azure Active Directory-rapportage.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a>Azure Active Directory-rapportage

Met Azure Active Directory-rapportage krijgt u inzicht in hoe uw omgeving presteert.  
Hallo opgegeven gegevens kunt u:

- Vaststellen hoe uw apps en services door uw gebruikers worden gebruikt
- Potentiële risico's die invloed hebben op Hallo status van uw omgeving detecteren
- Problemen oplossen waardoor uw gebruikers hun werk niet kunnen doen  

Er is een Hallo reporting architectuur afhankelijk van de twee belangrijkste stijlen:

- Beveiligingsrapporten
- Activiteitsrapporten

![Rapportage](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a>Beveiligingsrapporten

Hallo beveiligingsrapporten in Azure Active Directory kunnen u tooprotect identiteiten van uw organisatie.  
Er zijn in Azure Active Directory twee soorten beveiligingsrapporten:

- **Gebruikers die zijn gemarkeerd voor risico** - van Hallo [gebruikers gemarkeerd voor risico beveiligingsrapport](active-directory-reporting-security-user-at-risk.md), u krijgt u een overzicht van gebruikersaccounts die mogelijk zijn aangetast.

- **Riskant aanmeldingen** - Hello [beveiligingsrapport voor riskante aanmelden](active-directory-reporting-security-risky-sign-ins.md), u een indicator voor aanmeldpogingen die mogelijk zijn uitgevoerd door iemand die niet Hallo rechtmatige eigenaar van een gebruikersaccount niet ophalen. 

**Welke Azure AD-licentie hebt u een beveiligingsrapport tooaccess nodig?**  
Alle edities van Azure Active Directory bieden rapporten over gebruikers voor wie wordt aangegeven dat ze risico lopen en rapporten over riskante aanmeldingen.  
Hallo-niveau van rapportgranulatie is echter van Hallo edities: 

- In Hallo **edities Azure Active Directory gratis en Basic**, u al een lijst met gebruikers die zijn gemarkeerd voor risico en riskant aanmeldingen. 

- Hallo **Azure Active Directory Premium 1** edition wordt dit model uitgebreid doordat ook u tooexamine aantal Hallo onderliggende risico's die zijn gedetecteerd voor elk rapport. 

- Hallo **Azure Active Directory Premium 2** editie biedt u Hello meest gedetailleerde informatie weer over Hallo onderliggende risicogebeurtenissen en ook kunt u beveiligingsbeleid tooconfigure die automatisch tooconfigured reageren risiconiveaus.


## <a name="activity-reports"></a>Activiteitsrapporten

Er zijn in Azure Active Directory twee soorten activiteitsrapporten:

- **Controlelogboeken** - hello [auditlogboeken activiteitenrapport](active-directory-reporting-activity-audit-logs.md) biedt u toegang toohello geschiedenis van elke taak uit te voeren in uw tenant.

- **Aanmeldingen** - Hello [aanmeldingen activiteitenrapport](active-directory-reporting-activity-sign-ins.md), kunt u bepalen, wie Hallo-taken die zijn gerapporteerd door Hallo audit logboeken rapport is uitgevoerd.



Hallo **auditlogboeken rapport** biedt u records van het systeemactiviteiten voor naleving.
Onder andere opgegeven Hallo gegevens kunt u tooaddress algemene scenario's, zoals:

- Iemand in mijn tenants heeft toegang tooan administratorgroep. Wie heeft diegene toegang verleend? 

- Ik wil tooknow Hallo lijst met gebruikers die zich in een specifieke app sinds ik onlangs vrijgegeven Hallo app en wilt tooknow als het goed actief

- Ik wil tooknow hoeveel wachtwoord opnieuw instellen van plaatsvinden in mijn tenants


**Welke Azure AD-licentie hebt u tooaccess Hallo controlerapport logboeken nodig?**  
Hallo-controlerapport Logboeken is beschikbaar voor functies waarvoor u licenties hebt. Als u een licentie voor een specifieke functie hebt, hebt u ook toegang toohello controle-logboekinformatie voor het.

Zie voor meer informatie **algemeen beschikbaar functies van Hallo vrije, Basic en Premium-edities vergelijken** in [Azure Active Directory-functies en mogelijkheden](https://www.microsoft.com/cloud-platform/azure-active-directory-features).   



Hallo **aanmeldingen activiteitenrapport** schakelt tootoofind beantwoordt tooquestions, zoals:

- Wat is Hallo aanmelden patroon van een gebruiker?
- Hoeveel keer hebben gebruikers zich aangemeld gedurende een week?
- Wat is de status van deze aanmeldingen Hallo?


**Welke Azure AD-licentie wilt u moet tooaccess Hallo aanmeldingen activiteitenrapport?**  
tooaccess Hallo activiteitenrapport aanmeldingen, uw tenant moet beschikken over een Azure AD Premium-licentie gekoppeld.


## <a name="programmatic-access"></a>Toegang op programmeerniveau

In de gebruikersinterface voor toevoeging toohello, rapportage van Azure Active Directory biedt u ook met [toegang op programmeerniveau](active-directory-reporting-api-getting-started-azure-portal.md) toohello rapportgegevens. Hallo-gegevens van deze rapporten kunnen zeer nuttig tooyour toepassingen, zoals de SIEM-systemen, controle en hulpprogramma's voor bedrijfsinformatie worden. Hello Azure AD rapportage-API's bieden toegang op programmeerniveau toohello gegevens via een set op basis van REST-API's. U kunt deze API's vanuit een groot aantal computertalen en hulpprogramma's aanroepen. 


## <a name="next-steps"></a>Volgende stappen

Als u meer informatie over Hallo tooknow verschillende rapporttypen in Azure Active Directory wilt, Zie:

- [Rapport voor Gebruikers voor wie wordt aangegeven dat ze risico lopen](active-directory-reporting-security-user-at-risk.md)
- [Rapport voor riskante aanmeldingen](active-directory-reporting-security-risky-sign-ins.md)
- [Rapport voor audittrails](active-directory-reporting-activity-audit-logs.md)
- [Rapport voor aanmeldlogboeken](active-directory-reporting-activity-sign-ins.md)

Als u meer over het openen van Hallo Hallo rapportagegegevens Hallo rapportage-API met tooknow wilt, Zie: 

- [Aan de slag met Azure Active Directory-rapportage API Hallo](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png