---
title: activiteit aaaSign in rapporten in Azure Active Directory-beheerportal Hallo | Microsoft Docs
description: Inleiding activiteit toosign in rapporten in hello Azure Active Directory-portal
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
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a>Rapporten in Azure Active Directory-beheerportal Hallo aanmeldingsactiviteiten

Met Azure Active Directory (Azure AD) rapportage in Hallo [Azure-portal](https://portal.azure.com), krijgt u Hallo-informatie die u nodig hebt toodetermine hoe uw omgeving doet.

Hallo-architectuur in Azure Active Directory reporting bestaat uit Hallo volgende onderdelen:

- **Activiteit** 
    - **Aanmelden activiteiten** – informatie over het gebruik van Hallo van beheerde toepassingen en gebruikersactiviteiten aanmelden
    - **Controlelogboeken**: informatie over systeemactiviteit van gebruikers, groepsbeheer, uw beheerde toepassingen en directory-activiteiten.
- **Beveiliging** 
    - **Riskant aanmeldingen** -een riskante aanmelden is een indicator voor een aanmeldingspoging die mogelijk zijn uitgevoerd door iemand die niet Hallo legitieme eigenaar van een gebruikersaccount. Zie Riskante aanmeldingen voor meer informatie.
    - **Gebruikers van wie wordt aangegeven dat ze risico lopen** - Een riskante gebruiker is een indicator van een gebruikersaccount dat mogelijk is aangetast. Zie Gebruikers van wie wordt aangegeven dat ze risico lopen voor meer informatie.

In dit onderwerp biedt een overzicht van Hallo aanmelden activiteiten.

## <a name="pre-requisite"></a>Vereiste

### <a name="who-can-access-hello-data"></a>Wie toegang heeft tot Hallo gegevens?
* Gebruikers met de rol beheerder beveiliging of beveiliging Reader Hallo
* Globale beheerders
* Alle gebruiker (niet-beheerders) hebben toegang tot hun eigen aanmeldingen 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a>Welke Azure AD-licentie moet u de aanmeldingsactiviteiten tooaccess?
* Uw tenant moet beschikken over een Azure AD Premium-licentie gekoppeld toosee Hallo alles op aanmeldingsactiviteiten rapport


## <a name="signs-in-activities"></a>Aanmeldactiviteiten

Hallo informatie verstrekt door de gebruiker aanmelden rapport hello, ziet u de antwoorden tooquestions zoals:

* Wat is Hallo aanmelden patroon van een gebruiker?
* Hoeveel keer hebben gebruikers zich aangemeld gedurende een week?
* Wat is de status van deze aanmeldingen Hallo?

Uw eerste vermelding punt tooall aanmelden activiteiten gegevens **aanmeldingen** in Hallo activiteit sectie van **Azure Active**.


![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/61.png "Aanmeldingsactiviteit")


Een controlelogboek heeft een standaardlijstweergave die het volgende laat zien:

- Hallo gerelateerde gebruiker
- Hallo toepassing hello gebruiker is aangemeld bij
- Hallo-in status
- tijd van aanmelden Hallo

![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/41.png "Aanmeldingsactiviteit")

U kunt de lijstweergave Hallo aanpassen door te klikken op **kolommen** op Hallo-werkbalk.

![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/19.png "Aanmeldingsactiviteit")

Dit kunt u aanvullende velden toodisplay of verwijderen van de velden die al worden weergegeven.

![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/42.png "Aanmeldingsactiviteit")

Door te klikken op een item in de lijstweergave hello, moet u alle beschikbare details over het ophalen.

![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/43.png "Aanmeldingsactiviteit")


## <a name="filtering-sign-in-activities"></a>Aanmeldingsactiviteiten filteren

toonarrow omlaag Hallo tooa gegevensniveau dat geldt voor u, kunt u Hallo aanmeldingen gegevens filteren met behulp van de volgende velden Hallo gerapporteerd:

- Tijdsinterval
- Gebruiker
- Toepassing
- Client
- Aanmeldingsstatus

![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/44.png "Aanmeldingsactiviteit")


Hallo **tijdsinterval** filter schakelt tooyou toodefine een tijdsspanne voor Hallo gegevens geretourneerd.  
Mogelijke waarden zijn:

- 1 maand
- 7 dagen
- 24 uur
- Aangepast telefoonnummer

Wanneer u een aangepast tijdsbestek selecteert, kunt u een begintijd en eindtijd configureren.

Hallo **gebruiker** filter kunt u toospecify Hallo naam of het Hallo UPN (user Principal name) van Hallo-gebruiker die u interesseren.

Hallo **toepassing** filter kunt u de naam van de toospecify Hallo van Hallo-toepassing die u interesseren.

Hallo **client** filter kunt u toospecify informatie over het Hallo-apparaat die u interesseren.

Hallo **aanmeldingsstatus** filter kunt u tooselect Hallo filter te volgen:

- Alle
- Geslaagd
- Fout


## <a name="sign-in-activities-shortcuts"></a>Snelkoppelingen voor aanmeldingsactiviteiten

Bovendien tooAzure Active Directory, hello Azure-portal biedt twee extra post punten toosign in activiteiten gegevens:

- Gebruikers en groepen
- Bedrijfstoepassingen


### <a name="users-and-groups-sign-ins-activities"></a>Aanmeldingsactiviteiten van gebruikers en groepen

Hallo informatie verstrekt door de gebruiker aanmelden rapport hello, ziet u de antwoorden tooquestions zoals:

- Wat is Hallo aanmelden patroon van een gebruiker?
- Hoeveel keer hebben gebruikers zich aangemeld gedurende een week?
- Wat is de status van deze aanmeldingen Hallo?



Punt toothis postgegevens is gebruiker aanmelden grafiek Hallo in Hallo **overzicht** onder sectie **gebruikers en groepen**.

![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/45.png "Aanmeldingsactiviteit")

Hallo gebruiker aanmelden grafiek toont wekelijkse aggregaties van de registratie-modules voor alle gebruikers in een bepaalde periode. Hallo-standaardwaarde voor Hallo is periode 30 dagen.

![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/46.png "Aanmeldingsactiviteit")

Als u op een dag in Hallo aanmelden grafiek klikt, krijgt u een gedetailleerde lijst met Hallo aanmelden activiteiten voor deze dag.

![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/41.png "Aanmeldingsactiviteit")

Elke rij in Hallo aanmelden activiteiten lijst kunt die u gedetailleerde informatie over Hallo geselecteerd aanmelden zoals Hallo:

* Wie heeft zich aangemeld?
* Wat was Hallo gerelateerde UPN?
* Welke toepassing hello doel van de aanmeldingspagina Hallo was?
* Wat is Hallo IP-adres van de aanmeldingspagina Hallo?
* Wat is Hallo status van Hallo aanmelden?

Hallo **aanmeldingen** optie biedt u een volledig overzicht van alle gebruikersaanmeldingen.

![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/51.png "Aanmeldingsactiviteit")



## <a name="usage-of-managed-applications"></a>Het gebruik van beheerde toepassingen

Met een toepassingsgerichte weergave van uw aanmeldingsgegevens kunt u antwoord vinden op vragen zoals:

* Wie gebruikt mijn toepassingen?
* Wat zijn de eerste Hallo 3 toepassingen in uw organisatie?
* Ik heb onlangs een toepassing geïmplementeerd. Hoe gaat het ermee?

Punt toothis postgegevens is Hallo eerste 3 toepassingen in uw organisatie binnen de laatste 30 dagen rapport in Hallo Hallo **overzicht** onder sectie **bedrijfstoepassingen**.

![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/64.png "Aanmeldingsactiviteit")

Hallo-app-gebruik grafiek wekelijkse aggregaties van aanmeldingen voor uw top-3-toepassingen in een bepaalde periode. Hallo-standaardwaarde voor Hallo is periode 30 dagen.

![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/47.png "Aanmeldingsactiviteit")

Als u wilt, kunt u Hallo focus instellen op een specifieke toepassing.


![Rapportage](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Rapportage")

Als u op een dag in Hallo app gebruiksgrafiek klikt, krijgt u een gedetailleerde lijst met Hallo aanmelden activiteiten.


![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/48.png "Aanmeldingsactiviteit")


Hallo **aanmeldingen** optie biedt u een volledig overzicht van alle gebeurtenissen aanmelden tooyour toepassingen.

![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/49.png "Aanmeldingsactiviteit")



## <a name="next-steps"></a>Volgende stappen

Als u meer informatie over foutcodes aanmeldingsactiviteiten tooknow wilt, raadpleegt u Hallo [aanmelden activiteit rapport-foutcodes in Azure Active Directory-beheerportal Hallo](active-directory-reporting-activity-sign-ins-errors.md).

