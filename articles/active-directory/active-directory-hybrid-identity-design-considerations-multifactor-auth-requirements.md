---
title: ontwerpoverwegingen voor aaaAzure Active Directory hybride identiteit - bepalen vereisten voor multi-factor authentication-server
description: "Met voorwaardelijk toegangsbeheer controleert de Azure Active Directory Hallo bepaalde voorwaarden die u bij het verifiëren van de gebruiker Hallo en alvorens deze toegang toohello toepassing kiezen. Als deze voorwaarden is voldaan, wordt Hallo gebruiker geverifieerd en toegang toohello toepassing toegestaan."
documentationcenter: 
services: active-directory
author: femila
manager: billmath
editor: 
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 49fa7b43772fb3a2d6664747477c60a34cddde2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a>Vereisten multi-factor authentication voor uw oplossing voor hybride identiteit bepalen
In deze wereld van mobility met gebruikers die toegang tot gegevens en toepassingen in de cloud Hallo en vanaf elk apparaat is voor het beveiligen van deze informatie geworden vooral gekeken naar.  Elke dag wordt er een nieuwe kop over een inbreuk op de beveiliging is.  Hoewel er is geen garantie tegen dergelijke schendingen, meervoudige verificatie biedt een extra laag van beveiliging toohelp te voorkomen dat deze inbreuk.
Start Hallo organisaties vereisten voor multi-factor authentication evalueren. Wat is Hallo organisatie poging toosecure.  Deze evaluatie is belangrijk toodefine Hallo technische vereisten voor het instellen en inschakelen van Hallo organisaties gebruikers voor multi-factor authentication.

> [!NOTE]
> Als u niet bekend met MFA en wat het doet bent, is het raadzaam dat u lees Hallo artikel [wat is Azure multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) voorafgaande toocontinue lezen van deze sectie.
> 
> 

Zorg ervoor dat tooanswer Hallo volgende:

* Is uw bedrijf probeert toosecure Microsoft-apps? 
* Hoe deze apps worden gepubliceerd?
* Uw bedrijf biedt externe toegang tooallow werknemers tooaccess lokale apps?

Zo ja, welk type externe toegang? U moet ook tooevaluate waar Hallo-gebruikers die toegang deze toepassingen tot geplaatst worden. Deze evaluatie is een andere belangrijke stap toodefine Hallo juiste multi-factor authentication-strategie. Zorg ervoor dat tooanswer Hallo vragen te volgen:

* Waar bevinden de Hallo gebruikers gaan toobe zich?
* Ze zijn locatie overal?
* Wil uw bedrijf tooestablish beperkingen op basis van de locatie van de gebruiker toohello?

Als u weet dat deze vereisten voldoet, is het belangrijk tooalso evalueren van de gebruiker van het Hallo-vereisten voor multi-factor authentication. Deze evaluatie is belangrijk omdat het Hallo-vereisten definieert voor het implementeren van multi-factor authentication-server. Zorg ervoor dat tooanswer Hallo vragen te volgen:

* Hallo gebruikers bekend bent met multi-factor authentication-server?
* Enkele aanvullende authenticatie vereist tooprovide worden?  
  * Zo ja, alle Hallo tijd, wanneer die afkomstig is van externe netwerken of toegang tot specifieke toepassingen of andere voorwaarden?
* Hallo gebruikers training in nodig toosetup en implementeer multi-factor authentication-server?
* Wat zijn Hallo belangrijke scenario's dat uw bedrijf wil tooenable multi-factor authentication voor hun gebruikers?

Na het Hallo vorige vragen beantwoorden, kunt u zich kunt toounderstand als er meerdere factoren verificatie al geïmplementeerd op locatie. Deze evaluatie is belangrijk toodefine Hallo technische vereisten voor het instellen en inschakelen van Hallo organisaties gebruikers voor multi-factor authentication. Zorg ervoor dat tooanswer Hallo vragen te volgen:

* Heeft uw bedrijf behoefte aan tooprotect bevoegde accounts met MFA?
* Heeft uw bedrijf behoefte tooenable MFA voor bepaalde toepassing om wettelijke redenen?
* Heeft uw bedrijf tooenable MFA nodig voor alle in aanmerking komende gebruikers van deze toepassing of alleen beheerders
* Hebt u nog moet MFA altijd ingeschakeld of alleen wanneer Hallo gebruikers zijn aangemeld buiten uw bedrijfsnetwerk?

## <a name="next-steps"></a>Volgende stappen
[Een strategie voor hybride identiteit acceptatie definiëren](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a>Zie ook
[Overzicht ontwerpoverwegingen](active-directory-hybrid-identity-design-considerations-overview.md)

