---
title: aaaRisky aanmeldingen rapport in Azure Active Directory-beheerportal Hallo | Microsoft Docs
description: Meer informatie over Hallo riskant aanmeldingen rapport in hello Azure Active Directory-portal
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a>Rapport van riskante aanmeldingen in hello Azure Active Directory-portal

Met de Hallo beveiligingsrapporten in Azure Active Directory (Azure AD) krijgt u inzicht in de kans op Hallo van verdachte gebruikersaccounts in uw omgeving. 

Azure AD detecteert verdachte acties die gerelateerd tooyour gebruikersaccounts zijn. Voor elke gedetecteerde activiteit wordt een record met de naam *risicogebeurtenis* gemaakt. Zie [Risicogebeurtenissen in Azure Active Directory](active-directory-identity-protection-risk-events.md) voor meer informatie. 

Hallo gedetecteerd risicogebeurtenissen gebruikte toocalculate zijn:

- **Riskant aanmeldingen** -een riskante aanmelden is een indicator voor een aanmeldingspoging die mogelijk zijn uitgevoerd door iemand die niet Hallo legitieme eigenaar van een gebruikersaccount. Zie [Riskante aanmeldingen](active-directory-identityprotection.md#risky-sign-ins) voor meer informatie. 

- **Gebruikers voor wie wordt aangegeven dat ze risico lopen** - Een riskante gebruiker is een indicator van een gebruikersaccount dat mogelijk is aangetast. Zie [Gebruikers voor wie wordt aangegeven dat ze risico lopen](active-directory-identityprotection.md#users-flagged-for-risk) voor meer informatie.  

In [hello Azure-portal](https://portal.azure.com), vindt u Hallo beveiliging rapporten over Hallo **Azure Active Directory** blade in Hallo **beveiliging** sectie. 

![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>Welke Azure AD-licentie hebt u een beveiligingsrapport tooaccess nodig?  

Alle edities van Azure Active Directory bieden rapporten over riskante aanmeldingen.  
Hallo-niveau van rapportgranulatie is echter van Hallo edities: 

- In Hallo **edities Azure Active Directory gratis en Basic**, u al een lijst van riskante aanmeldingen. 

- Hallo **Azure Active Directory Premium 1** edition wordt dit model uitgebreid doordat ook u tooexamine aantal Hallo onderliggende risico's die zijn gedetecteerd voor elk rapport. 

- Hallo **Azure Active Directory Premium 2** editie biedt u Hello meest gedetailleerde informatie weer over alle onderliggende risicogebeurtenissen en ook kunt u beveiligingsbeleid tooconfigure die automatisch tooconfigured reageren risiconiveaus.



## <a name="azure-active-directory-free-and-basic-edition"></a>Gratis en Basic edities van Azure Active Directory

Hello Azure Active Directory gratis edities en basic bieden u een lijst van riskante aanmeldingen die zijn gedetecteerd voor uw gebruikers. Dit rapport bevat:

- **Gebruiker** - hello naam van het Hallo-gebruiker die is gebruikt tijdens het Hallo-in bewerking
- **IP** -Hallo IP-adres van het Hallo-apparaat dat gebruikt tooconnect tooAzure Active Directory is
- **Locatie** -Hallo-locatie gebruikt tooconnect tooAzure Active Directory
- **Tijd van aanmelden** -Hallo tijd wanneer dat aanmeldingspagina Hallo is uitgevoerd
- **Status** -status van de aanmeldingspagina Hallo Hallo


![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/01.png)

Op basis van uw onderzoek van riskante aanmelden hello, kunt u feedback tooAzure Active Directory in de vorm van de volgende activiteiten Hallo bieden:

- Oplossen
- Markeren als fout-positief
- Negeren
- Opnieuw activeren

![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/21.png)

Zie voor meer informatie [Risico's handmatig sluiten](active-directory-identityprotection.md#closing-risk-events-manually).

Dit rapport biedt de volgende mogelijkheden:

- Resources zoeken
- Hallo rapportgegevens downloaden


![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a>Premium edities van Azure Active Directory

Hallo riskant aanmeldingen rapport in Azure Active Directory premium-edities Hallo beschikt u over:

- Informatie over Hallo geaggregeerd [risico gebeurtenistypen](active-directory-identity-protection-risk-events.md) die zijn gedetecteerd

- Een optie toodownload Hallo-rapport


![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/456.png)


Wanneer u een risicogebeurtenis selecteert, krijgt u een gedetailleerde rapportweergave voor deze risicogebeurtenis waarmee u het volgende kunt:

- Een optie tooconfigure een [gebruikersbeleid risico herstel](active-directory-identityprotection.md#user-risk-security-policy)  

- Hallo detectie tijdlijn voor Hallo risicogebeurtenis bekijken  

- Een lijst met gebruikers bekijken waarvoor deze risicogebeurtenis is gedetecteerd

- [Risicogebeurtenissen handmatig sluiten](active-directory-identityprotection.md#closing-risk-events-manually) of een handmatig gesloten risicogebeurtenis opnieuw activeren. 


![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/457.png)

Wanneer u een gebruiker selecteert, krijgt u een gedetailleerde rapportweergave voor deze gebruiker waarmee u het volgende kunt:

- Open Hallo alle aanmeldingen weergeven

- Hallo gebruikerswachtwoord opnieuw instellen

- Alle gebeurtenissen sluiten

- Onderzoek gemelde risicogebeurtenissen voor Hallo-gebruiker. 


![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/324.png)


een risicogebeurtenis tooinvestigate geselecteerd in de lijst Hallo.  
Hiermee opent u Hallo **Details** blade voor deze risicogebeurtenis. Op Hallo **Details** blade hebt Hallo optie tooeither [handmatig sluit een risicogebeurtenis](active-directory-identityprotection.md#closing-risk-events-manually) of opnieuw activeren van een risicogebeurtenis handmatig gesloten. 


![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a>Volgende stappen

- Zie [Azure Active Directory Identity Protection](active-directory-identityprotection.md) voor meer informatie over Azure Active Directory Identity Protection.

