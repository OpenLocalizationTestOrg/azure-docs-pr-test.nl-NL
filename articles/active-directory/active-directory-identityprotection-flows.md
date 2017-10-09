---
title: aaaSign in ervaringen met Azure AD Identity Protection | Microsoft Docs
description: Biedt een overzicht van de gebruikerservaring Hallo wanneer Identity Protection heeft verholpen of een gebruiker of wanneer de multi-factor authentication-server is vereist voor een beleid dat is hersteld.
services: active-directory
keywords: beveiliging in Azure active directory-identiteit, cloud app discovery, het beheren van toepassingen, beveiliging, risico, risiconiveau, beveiligingsprobleem, beveiligingsbeleid
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a>Aanmelden-ervaring met Azure AD Identity Protection
U kunt met Azure Active Directory: Identity Protection:

* gebruikers tooregister voor meervoudige verificatie vereisen
* riskant aanmeldingen en verdachte gebruikers verwerken

antwoord Hallo Hallo system toothese problemen heeft een invloed op de aanmeldingservaring van een gebruiker omdat alleen rechtstreeks aanmelden met een gebruikersnaam en een wachtwoord niet mogelijk meer zijn. Er zijn extra stappen vereist tooget een gebruiker terug veilig in bedrijf.

In dit onderwerp biedt een overzicht van de aanmeldingservaring van een gebruiker in alle gevallen die zich kunnen voordoen.

**Multi-factor authentication**

* Registratie voor meervoudige verificatie

**Meld u aan risico**

* Herstel voor riskante aanmelden
* Riskant aanmelden geblokkeerd
* Registratie van de multi-factor authentication-server tijdens een riskante aanmelden

**Gebruiker risico**

* Verdacht accountherstel
* Verdacht account geblokkeerd

## <a name="multi-factor-authentication-registration"></a>Registratie voor meervoudige verificatie
Hallo beste gebruikerservaring voor beide, Hallo verdacht account recovery stroom en Hallo riskant aanmelden stroom, is wanneer de gebruiker Hallo zelf kunt herstellen. Als gebruikers zijn geregistreerd voor multi-factor authentication, hebben ze al een telefoonnummer dat is gekoppeld aan hun account die kan worden gebruikt toopass beveiligingsproblemen met zich mee. Er is geen help helpdesk of beheerder betrokkenheid is benodigde toorecover tegen inbreuk account. Dus het is raadzaam tooget uw gebruikers geregistreerd voor multi-factor authentication. 

Beheerders kunnen:

* een beleid instellen dat gebruikers tooset van hun account voor aanvullende beveiligingsverificatie vereist. 
* Multi-factor authentication-registratie voor too30 dagen, wordt overgeslagen als ze toogive gebruikers willen toestaan een respijtperiode voordat u registreert.

**Hallo-registratie voor multi-factor authentication-server heeft drie stappen:**

1. In de eerste stap Hallo opgehaald Hallo gebruiker een melding over Hallo vereiste tooset Hallo account voor multi-factor authentication. 
   
    ![Herstel](./media/active-directory-identityprotection-flows/140.png "herstel")
2. up tooset multi-factor Authentication-verificatie, moet u toolet Hallo system weet hoe u toobe bereikt.
   
    ![Herstel](./media/active-directory-identityprotection-flows/141.png "herstel")
3. Hallo system verzendt een challenge tooyou en moet u toorespond.
   
    ![Herstel](./media/active-directory-identityprotection-flows/142.png "herstel")

## <a name="risky-sign-in-recovery"></a>Herstel voor riskante aanmelden
Wanneer een beheerder heeft een beleid voor aanmelden risico's geconfigureerd, Hallo van invloed op een gebruikers een melding krijgen wanneer ze proberen toosign in. 

**riskant Hallo aanmelden stroom bestaat uit twee stappen:** 

1. Hallo-gebruiker wordt geïnformeerd dat ongewone activiteit over hun aanmelden gevonden is, zoals het aanmelden vanaf een nieuwe locatie, apparaat of app. 
   
    ![Herstel](./media/active-directory-identityprotection-flows/120.png "herstel")
2. Hallo-gebruiker is vereist tooprove hun identiteit met een beveiligingsvraag op te lossen. Als het Hallo-gebruiker is geregistreerd voor multi-factor authentication moet een telefoonnummer beveiliging code tootheir tooround-reis. Aangezien dit een zojuist een riskante aanmelden en verdacht account, Hallo gebruiker geen toochange Hallo wachtwoord in deze stroom. 
   
    ![Herstel](./media/active-directory-identityprotection-flows/121.png "herstel")

## <a name="risky-sign-in-blocked"></a>Riskant aanmelden geblokkeerd
Beheerders kunnen tooset ook kiezen een aanmeldingspagina risico beleid tooblock gebruikers bij het aanmelden, afhankelijk van het risiconiveau Hallo. tooget gedeblokkeerd, eindgebruikers moet contact opnemen met een beheerder of de helpdesk of proberen ze aanmelden vanaf een vertrouwde locatie of het apparaat. Automatisch herstellen door het oplossen van multi-factor authentication-server kan niet worden gebruikt in dit geval.

![Herstel](./media/active-directory-identityprotection-flows/200.png "herstel")

## <a name="compromised-account-recovery"></a>Verdacht accountherstel
Wanneer een gebruiker risico-beveiligingsbeleid is geconfigureerd, gebruikers die voldoen aan de gebruiker Hallo risiconiveau opgegeven in het Hallo-beleid (en zijn daarom aangenomen geknoeid) moet doorlopen inbreuk Hallo-herstel gebruikersstroom voordat ze kunnen aanmelden. 

**inbreuk op Hallo-herstel gebruikersstroom heeft drie stappen:**

1. Hallo-gebruiker wordt geïnformeerd dat de accountbeveiliging van hun risico vanwege verdachte activiteiten loopt of referenties gelekte.
   
    ![Herstel](./media/active-directory-identityprotection-flows/101.png "herstel")
2. Hallo-gebruiker is vereist tooprove hun identiteit met een beveiligingsvraag op te lossen. Hallo-gebruiker is geregistreerd voor multi-factor authentication kunnen zichzelf herstellen van wordt aangetast. Ze moet een telefoonnummer beveiliging code tootheir tooround-reis. 
   
   ![Herstel](./media/active-directory-identityprotection-flows/110.png "herstel")
3. Ten slotte Hallo gebruiker is toochange gedwongen hun wachtwoord, omdat iemand anders tootheir-toegangsaccount heeft gehad. 
   Schermopnamen van deze ervaring zijn hieronder.
   
   ![Herstel](./media/active-directory-identityprotection-flows/111.png "herstel")

## <a name="compromised-account-blocked"></a>Verdacht account geblokkeerd
tooget een gebruiker die is geblokkeerd door een gebruiker risico beveiligingsbeleid gedeblokkeerd, Hallo gebruiker, moet contact opnemen met een netwerkbeheerder of de helpdesk. Automatisch herstellen door het oplossen van multi-factor authentication-server kan niet worden gebruikt in dit geval.

![Herstel](./media/active-directory-identityprotection-flows/104.png "herstel")

## <a name="reset-password"></a>Wachtwoord opnieuw instellen
Als verdachte gebruikers hebben geen toegang tot het aanmelden, kan een beheerder een tijdelijk wachtwoord genereren voor deze. Hallo hebben gebruikers toochange hun wachtwoord tijdens een volgende keer aanmelden.

![Herstel](./media/active-directory-identityprotection-flows/160.png "herstel")

## <a name="see-also"></a>Zie ook
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md) 

