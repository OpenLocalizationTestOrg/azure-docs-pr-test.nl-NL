---
title: aaaUsers gemarkeerd voor beveiligingsrapport risico's in Azure Active Directory-beheerportal Hallo | Microsoft Docs
description: Meer informatie over het Hallo-gebruikers die zijn gemarkeerd voor risico beveiligingsrapport in hello Azure Active Directory-portal
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a>Gebruikers die zijn gemarkeerd voor risico beveiligingsrapport in hello Azure Active Directory-portal

Met de Hallo beveiligingsrapporten in hello Azure Active Directory (Azure AD) krijgt u inzicht in de kans op Hallo van verdachte gebruikersaccounts in uw omgeving. 

Azure Active Directory detecteert verdachte acties die gerelateerd tooyour gebruikersaccounts zijn. Voor elke gedetecteerde activiteit wordt een record met de naam *risicogebeurtenis* gemaakt. Zie [Risicogebeurtenissen in Azure Active Directory](active-directory-identity-protection-risk-events.md) voor meer informatie. 

Hallo gedetecteerd risicogebeurtenissen gebruikte toocalculate zijn:

- **Riskant aanmeldingen** -een riskante aanmelden is een indicator voor een aanmeldingspoging die mogelijk zijn uitgevoerd door iemand die niet Hallo legitieme eigenaar van een gebruikersaccount. Zie [Riskante aanmeldingen](active-directory-identityprotection.md#risky-sign-ins) voor meer informatie. 

- **Gebruikers voor wie wordt aangegeven dat ze risico lopen** - Een riskante gebruiker is een indicator van een gebruikersaccount dat mogelijk is aangetast. Zie [Gebruikers voor wie wordt aangegeven dat ze risico lopen](active-directory-identityprotection.md#users-flagged-for-risk) voor meer informatie.  

In hello Azure-portal, kunt u vinden Hallo beveiliging rapporten over Hallo **Azure Active Directory** blade in Hallo **beveiliging** sectie.  

![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>Welke Azure AD-licentie hebt u een beveiligingsrapport tooaccess nodig?  

Alle edities van Azure Active Directory bieden rapporten over gebruikers voor wie wordt aangegeven dat ze risico lopen.  
Hallo-niveau van rapportgranulatie is echter van Hallo edities: 

- In Hallo **edities Azure Active Directory gratis en Basic**, u al een lijst met gebruikers die zijn gemarkeerd voor risico's. 

- Hallo **Azure Active Directory Premium 1** edition wordt dit model uitgebreid doordat ook u tooexamine aantal Hallo onderliggende risico's die zijn gedetecteerd voor elk rapport. 

- Hallo **Azure Active Directory Premium 2** -versie Hallo meest gedetailleerde informatie over alle onderliggende risicogebeurtenissen en kunt u beveiligingsbeleid tooconfigure die automatisch tooconfigured risico reageren niveaus.



## <a name="azure-active-directory-free-and-basic-edition"></a>Gratis en Basic edities van Azure Active Directory

Hallo-gebruikers die zijn gemarkeerd voor risico rapport in de gratis en basic-edities van Azure Active Directory Hallo biedt u een lijst met gebruikersaccounts die mogelijk zijn aangetast. 


![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/03.png)

Als u een gebruiker selecteert, wordt Hallo gerelateerde gebruiker gegevens blade geopend.
U kunt voor gebruikers die risico lopen van Hallo gebruiker aanmelden geschiedenis bekijken en Hallo wachtwoord opnieuw instellen als nodig.

![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/46.png)


Dit rapport biedt de volgende mogelijkheden:

- Hallo rapport downloaden

- Gebruikers zoeken

![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a>Premium edities van Azure Active Directory

Hallo-gebruikers die zijn gemarkeerd voor risico rapport in Azure Active Directory premium-edities Hallo beschikt u over:

- Een [lijst met gebruikersaccounts](active-directory-identityprotection.md#users-flagged-for-risk) die mogelijk zijn aangetast 

- Informatie over Hallo geaggregeerd [risico gebeurtenistypen](active-directory-identity-protection-risk-events.md) die zijn gedetecteerd

- Een optie toodownload Hallo-rapport

- Een optie tooconfigure een [gebruikersbeleid risico herstel](active-directory-identityprotection.md#user-risk-security-policy)  


![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/71.png)

Wanneer u een gebruiker selecteert, krijgt u een gedetailleerde rapportweergave voor deze gebruiker waarmee u het volgende kunt:

- Open Hallo alle aanmeldingen weergeven

- Hallo gebruikerswachtwoord opnieuw instellen

- Alle gebeurtenissen sluiten

- Onderzoek gemelde risicogebeurtenissen voor Hallo-gebruiker. 


![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/324.png)


tooinvestigate een risicogebeurtenis, selecteer een optie uit Hallo lijst tooopen hello **Details** blade voor deze risicogebeurtenis. Op Hallo **Details** blade hebt Hallo optie tooeither [handmatig sluit een risicogebeurtenis](active-directory-identityprotection.md#closing-risk-events-manually) of opnieuw activeren van een risicogebeurtenis handmatig gesloten. 


![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a>Volgende stappen

- Zie [Azure Active Directory Identity Protection](active-directory-identityprotection.md) voor meer informatie over Azure Active Directory Identity Protection.

