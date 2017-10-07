---
title: 'Licentieverlening: Azure AD SSPR | Microsoft Docs'
description: Azure AD selfservice voor wachtwoordherstel licentievereisten
services: active-directory
keywords: 
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
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a>Licentievereisten voor selfservicegebruikers Azure AD-wachtwoord opnieuw instellen

Toofunction Azure AD-wachtwoord opnieuw instellen zodat u **moet ten minste één licentie is toegewezen in uw organisatie hebben**. We afdwingen per gebruiker licentieverlening op Hallo wachtwoord opnieuw instellen van ervaring niet. toomaintain compatibiliteit met uw Microsoft-licentieovereenkomst, moet u tooassign licenties tooany gebruikers die gebruikmaken van premium-functies.

* **Alleen gebruikers cloud** -Office 365 (O365) een betaald SKU of Azure AD Basic
* **Cloud** en/of **on-premises gebruikers** -Azure AD Premium-P1 of P2, Enterprise Mobility + Security (EMS) of Secure productief Enterprise (Gebeurtenisspe)

## <a name="licenses-required-for-password-writeback"></a>Licenties die vereist zijn voor write-back van wachtwoord

toouse wachtwoord terugschrijven, kunt u een van de licenties die zijn toegewezen in uw tenant te volgen Hallo moet hebben.

* Azure AD Premium P1
* Azure AD Premium P2
* Enterprise Mobility + Security E3
* Enterprise Mobility + Security E5
* Secure Productive Enterprise E3
* Secure Productive Enterprise E5

> [!NOTE]
> Zelfstandige Office 365-abonnementen licentieverlening **bieden geen ondersteuning voor write-back van wachtwoord** en een van de voorgaande plannen voor deze functionaliteit toowork Hallo vereisen.

Aanvullende licenties informatie, inclusief kosten vindt u op Hallo volgende pagina 's

* [Azure Active Directory-prijzen site](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Beveiligde productief Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a>Groep of gebruiker gebaseerde licentieverlening inschakelen

Azure AD nu ondersteunt op basis van een groep licentieverlening zodat beheerders tooassign licenties in bulk tooa groep gebruikers in plaats van één voor één toewijzen. [Toewijzen, controleren en oplossen van problemen met licenties](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

Sommige Microsoft-services zijn niet beschikbaar op alle locaties. Voordat u een licentie kan tooa gebruiker worden toegewezen, moet de Hallo beheerder Hallo 'Gebruikslocatie'-eigenschap op Hallo gebruiker opgeven. Toewijzing van licenties kan worden uitgevoerd onder User > profiel > sectie Settings in hello Azure-portal. **Wanneer u de licentietoewijzing van de groep, neemt alle gebruikers zonder een gebruikslocatie opgegeven Hallo-locatie van Hallo-map.**

## <a name="next-steps"></a>Volgende stappen

Hallo volgende koppelingen vindt u aanvullende informatie met betrekking tot het wachtwoord opnieuw instellen met behulp van Azure AD

* [**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD 
* [**Gegevens** ](active-directory-passwords-data.md) - begrijpen Hallo-gegevens die nodig is en hoe deze wordt gebruikt voor wachtwoordbeheer
* [**Implementatie** ](active-directory-passwords-best-practices.md) -plannen en implementeren van SSPR tooyour gebruikers via Hallo richtlijnen hier gevonden
* [**Aanpassen** ](active-directory-passwords-customize.md) -Hallo uiterlijk Hallo SSPR ervaring voor uw bedrijf aanpassen.
* [**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken
* [**Technische diepgaand** ](active-directory-passwords-how-it-works.md) -Ga achter Hallo gordijn toounderstand hoe het werkt
* [**Veelgestelde vragen**](active-directory-passwords-faq.md): hoe? Hoe komt dat? Wat? Waar? Wie? Wanneer? -Beantwoordt tooquestions gewenste altijd tooask
* [**Problemen met** ](active-directory-passwords-troubleshoot.md) -informatie over hoe tooresolve algemene problemen zien we met SSPR

