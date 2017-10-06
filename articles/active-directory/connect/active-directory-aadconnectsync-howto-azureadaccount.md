---
title: 'Azure AD Connect-synchronisatie: hoe toomanage hello Azure AD-serviceaccount | Microsoft Docs'
description: In dit onderwerp wordt beschreven hoe toorestore hello Azure AD-serviceaccount.
services: active-directory
keywords: AADSTS70002, AADSTS50054, hello hoe tooreset Hallo wachtwoord voor Azure AD Connect-synchronisatie Connector-serviceaccount
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a>Azure AD Connect-synchronisatie: hoe toomanage hello Azure AD-serviceaccount
Hallo-serviceaccount die wordt gebruikt door hello Azure AD-Connector moet toobe service gratis. Als u tooreset de referenties moet, wordt de in dit onderwerp voor u. Bijvoorbeeld, als een globale beheerder heeft door fout-wachtwoord opnieuw instellen Hallo Hallo serviceaccount met behulp van PowerShell.

## <a name="reset-hello-credentials"></a>Hallo referenties opnieuw instellen
Als het Hallo-serviceaccount is gedefinieerd op Hallo Azure AD-Connector geen contact met Azure AD vanwege problemen met tooauthentication, Hallo wachtwoord opnieuw kan worden ingesteld.

1. Meld u aan toohello Azure AD Connect sync-server en start PowerShell.
2. Voer `Add-ADSyncAADServiceAccount` uit.  
   ![PowerShell-cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)
3. Geef referenties op globale beheerder Azure AD.

Deze cmdlet Hallo wachtwoord voor serviceaccount Hallo opnieuw instellen en in Azure AD en in de synchronisatie-engine Hallo bijwerken.

## <a name="known-issues-these-steps-can-solve"></a>Bekende problemen met die deze stappen kunnen worden opgelost
Deze sectie is een lijst met fouten die zijn gerapporteerd door klanten die door een gebruikersreferenties instellen op Hallo Azure AD-serviceaccount zijn opgelost.

- - -
Gebeurtenis 6900  
Hallo-server een onverwachte fout opgetreden tijdens het verwerken van een wijzigingsmelding wachtwoord:  
AADSTS70002: Fout bij valideren referenties. AADSTS50054: Oude wachtwoord wordt gebruikt voor verificatie.

- - -
Gebeurtenis 659  
Fout bij het ophalen van wachtwoord-beleidsconfiguratie synchronisatie. Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:  
AADSTS70002: Fout bij valideren referenties. AADSTS50054: Oude wachtwoord wordt gebruikt voor verificatie.

## <a name="next-steps"></a>Volgende stappen
**Overzichtsonderwerpen**

* [Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen](active-directory-aadconnectsync-whatis.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)

