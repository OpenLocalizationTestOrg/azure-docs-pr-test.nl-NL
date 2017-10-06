---
title: 'Azure AD Connect-synchronisatie: AD-Prullenbak inschakelen | Microsoft Docs'
description: In dit onderwerp adviseert Hallo gebruik van AD-Prullenbak-functie met Azure AD Connect.
services: active-directory
keywords: Prullenbak van AD, per ongeluk verwijderen, bronanker
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a>Azure AD Connect-synchronisatie: AD-Prullenbak inschakelen
Het verdient aanbeveling dat u voor uw lokale Active Directory's die gesynchroniseerd tooAzure AD zijn Hallo AD-Prullenbak-functie inschakelen. 

Als u een on-premises per ongeluk hebt verwijderd AD-gebruiker-object maken en terugzetten met de functie hello, Azure AD worden hersteld Hallo bijbehorende Azure AD-gebruikersobject.  Raadpleeg voor informatie over de functie Prullenbak Hallo AD tooarticle [Scenario-overzicht voor het herstellen van verwijderde Active Directory-objecten](https://technet.microsoft.com/library/dd379542.aspx).

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a>Prullenbak van de voordelen van het Hallo AD inschakelen
Deze functie helpt bij het herstellen van objecten voor Azure AD-gebruiker door Hallo volgende te doen:

* Als u een on-premises per ongeluk hebt verwijderd AD-gebruiker object, bijbehorende Azure AD-gebruikersobject Hallo verwijderd in Hallo volgende synchronisatiecyclus. Standaard houdt Azure AD verwijderd hello Azure AD-gebruikersobject voorlopig verwijderde status heeft voor 30 dagen.

* Als u beschikt over on-premises AD-Prullenbak-functie is ingeschakeld, kunt u Hallo verwijderd herstellen lokale AD-gebruiker-object zonder dat u de waarde Bronanker wijzigt. Wanneer Hallo hersteld lokale AD-gebruiker-object is gesynchroniseerd tooAzure AD, Azure AD wordt hersteld Hallo overeenkomt voorlopig verwijderde Azure AD-gebruiker-object. Raadpleeg voor informatie over Bronanker kenmerk tooarticle [Azure AD Connect: concepten ontwerpen](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).

* Als u geen lokale AD Recycle Bin functie is ingeschakeld, hebt u mogelijk vereist toocreate een AD-object tooreplace Hallo verwijderde gebruikersobject. Als Azure AD Connect-synchronisatieservice geconfigureerde toouse systeem gegenereerde AD kenmerk is (zoals ObjectGuid) voor Hallo Bronanker kenmerk, wordt hello gemaakte AD-gebruiker-object niet hebben Hallo dezelfde Bronanker-waarde als Hallo AD-gebruikersobject verwijderd. Wanneer hello gemaakte object voor AD-gebruiker gesynchroniseerd tooAzure AD is, Azure AD maakt een nieuw object van de Azure AD-gebruiker in plaats van Azure AD-gebruikersobject Hallo voorlopig verwijderde herstellen.

> [!NOTE]
> Standaard verwijderd Azure AD houdt objecten van Azure AD-gebruiker in staat voorlopig verwijderde voor 30 dagen voordat ze worden permanent verwijderd. Beheerders kunnen echter Hallo verwijderen van dergelijke objecten te versnellen. Zodra het Hallo-objecten worden permanent verwijderd, kunnen ze niet meer worden hersteld, zelfs als lokale AD-Prullenbak-functie is ingeschakeld.



## <a name="next-steps"></a>Volgende stappen
**Overzichtsonderwerpen**

* [Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen](active-directory-aadconnectsync-whatis.md)

* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
