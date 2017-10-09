---
title: aaaAudit activiteit rapporten in Azure Active Directory-beheerportal Hallo | Microsoft Docs
description: Inleiding toohello audit activiteitsrapporten in hello Azure Active Directory-portal
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a>Activiteitsrapporten in Azure Active Directory-beheerportal Hallo controleren 

Met rapportage in Azure Active Directory (Azure AD), kunt u de gewenste toodetermine hoe uw omgeving doet Hallo-informatie ophalen.

architectuur van rapportage in Azure AD Hallo bestaat uit Hallo volgende onderdelen:

- **Activiteit** 
    - **Aanmelden activiteiten** – informatie over het gebruik van Hallo van beheerde toepassingen en gebruikersactiviteiten aanmelden
    - **Controlelogboeken**: informatie over systeemactiviteit van gebruikers, groepsbeheer, uw beheerde toepassingen en directory-activiteiten.
- **Beveiliging** 
    - **Riskant aanmeldingen** -een riskante aanmelden is een indicator voor een aanmeldingspoging die mogelijk zijn uitgevoerd door iemand die niet Hallo legitieme eigenaar van een gebruikersaccount. Zie Riskante aanmeldingen voor meer informatie.
    - **Gebruikers van wie wordt aangegeven dat ze risico lopen** - Een riskante gebruiker is een indicator van een gebruikersaccount dat mogelijk is aangetast. Zie Gebruikers van wie wordt aangegeven dat ze risico lopen voor meer informatie.

In dit onderwerp biedt een overzicht van Hallo audit activiteiten.
 
## <a name="who-can-access-hello-data"></a>Wie toegang heeft tot Hallo gegevens?
* Gebruikers met de rol beheerder beveiliging of beveiliging Reader Hallo
* Globale beheerders
* Afzonderlijke gebruikers (niet-beheerders) kunnen hun eigen activiteiten zien


## <a name="audit-logs"></a>Controlelogboeken

Hallo controlelogboeken in Azure Active Directory bieden records van het systeemactiviteiten voor naleving.  
Uw eerste vermelding punt tooall controle van gegevens is **controlelogboeken** in Hallo **activiteit** sectie van **Azure Active Directory**.

![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/61.png "Controlelogboeken")

Een controlelogboek heeft een standaardlijstweergave die het volgende laat zien:

- Hallo-datum en tijd van Hallo-instantie
- Hallo initiator / actor (*die*) van een activiteit 
- Hallo activiteit (*wat*) 
- Hallo-doel

![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/18.png "Controlelogboeken")

U kunt de lijstweergave Hallo aanpassen door te klikken op **kolommen** op Hallo-werkbalk.

![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/19.png "Controlelogboeken")

Dit kunt u aanvullende velden toodisplay of verwijderen van de velden die al worden weergegeven.

![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/21.png "Controlelogboeken")


Door te klikken op een item in de lijstweergave hello, moet u alle beschikbare details over het ophalen.

![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/22.png "Controlelogboeken")


## <a name="filtering-audit-logs"></a>Controlelogboeken filteren

toonarrow omlaag Hallo tooa gegevensniveau dat geldt voor u, kunt u Hallo audit gegevens filteren met behulp van de volgende velden Hallo gerapporteerd:

- Datumbereik
- Gestart door (actor)
- Category
- Resourcetype van activiteit
- Activiteit

![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/23.png "Controlelogboeken")


Hallo **datumbereik** filter schakelt tooyou toodefine een tijdsspanne voor Hallo gegevens geretourneerd.  
Mogelijke waarden zijn:

- 1 maand
- 7 dagen
- 24 uur
- Aangepast telefoonnummer

Wanneer u een aangepast tijdsbestek selecteert, kunt u een begintijd en eindtijd configureren.

Hallo **gestart door** filter kunt u toodefine een actor-naam of de UPN (User Principal Name).

Hallo **categorie** filter kunt u tooselect Hallo filter te volgen:

- Alle
- Hoofdcategorie
- Hoofddirectory
- Wachtwoordbeheer via selfservice
- Groepsbeheer via selfservice
- Account inrichten - Automatische wachtwoordoverschakeling
- Uitgenodigde gebruikers
- MIM-service
- Identiteitsbeveiliging
- B2C

Hallo **activiteit brontype** filter kunt u een van de volgende Hallo filtert tooselect:

- Alle 
- Groep
- Directory
- Gebruiker
- Toepassing
- Beleid
- Apparaat
- Overige

Wanneer u selecteert **groep** als **activiteit brontype**, dat u een extra filtercategorie waarmee u tooalso bieden een **bron**:

- Azure AD
- O365


Hallo **activiteit** filter is gebaseerd op het Hallo-categorie en activiteit resource type selectie die u maakt. U kunt een bepaalde activiteit of wilt u toosee Kies alle selecteren. 

U kunt Hallo lijst van alle activiteiten van de Audit ophalen met behulp van Hallo Graph API https://graph.windows.net/$ activiteiten-tenantdomain/auditActivityTypes? api-versie = Bèta, waarbij $tenantdomain = uw domeinnaam of Raadpleeg toohello artikel [rapport van de audit gebeurtenissen](active-directory-reporting-audit-events.md).


## <a name="audit-logs-shortcuts"></a>Snelkoppelingen naar controlelogboeken

Bovendien te**Azure Active Directory**, hello Azure-portal biedt u twee extra toegangspunten tooaudit gegevens:

- Gebruikers en groepen
- Bedrijfstoepassingen

### <a name="users-and-groups-audit-logs"></a>Controlelogboeken voor gebruikers en groepen

Met gebruikers en groepen gebaseerde controlerapporten, kun je antwoorden tooquestions zoals:

- Welke typen updates zijn toegepast Hallo gebruikers?

- Hoeveel gebruikers zijn gewijzigd?

- Hoeveel wachtwoorden zijn gewijzigd?

- Wat heeft een beheerder in een directory gedaan?

- Wat zijn Hallo-groepen die zijn toegevoegd?

- Zijn er groepen met wijzigingen in het lidmaatschap?

- Hallo-eigenaars van groep zijn gewijzigd?

- Welke licenties zijn toegewezen tooa groep of een gebruiker?

Als u wilt dat alleen tooreview controle van de gegevens die zijn gerelateerd toousers en groepen, vindt u een gefilterde weergave onder **controlelogboeken** in Hallo **activiteit** sectie Hallo **gebruikers en groepen**. Dit beginpunt heeft **Gebruikers en groepen** als vooraf geselecteerd **Type activiteitsresource**.

![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/93.png "Controlelogboeken")

### <a name="enterprise-applications-audit-logs"></a>Controlelogboeken voor bedrijfstoepassingen

Controleren op basis van een toepassing met de rapporten, kunt u antwoorden tooquestions zoals krijgen:

* Wat zijn Hallo-toepassingen die zijn toegevoegd of bijgewerkt?
* Wat zijn Hallo-toepassingen die zijn verwijderd?
* Is de service-principal van een toepassing gewijzigd?
* Hallo-namen van toepassingen zijn gewijzigd?
* Wie heeft toestemming tooan toepassing?

Als u wilt dat alleen tooreview controle van de gegevens die zijn gerelateerd tooyour toepassingen, kunt u vinden in een gefilterde weergave onder **controlelogboeken** in Hallo **activiteit** sectie Hallo **bedrijfstoepassingen**  blade. Dit beginpunt heeft **Bedrijfstoepassingen** als vooraf geselecteerd **Type activiteitsresource**.

![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/134.png "Controlelogboeken")

U kunt deze weergave verder omlaag toojust filteren **groepen** of alleen **gebruikers**.

![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/25.png "Controlelogboeken")


## <a name="next-steps"></a>Volgende stappen

Zie voor een overzicht van reporting Hallo [rapportage van Azure Active Directory](active-directory-reporting-azure-portal.md).

