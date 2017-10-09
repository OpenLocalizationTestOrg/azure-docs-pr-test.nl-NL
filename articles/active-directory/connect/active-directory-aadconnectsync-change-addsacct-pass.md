---
title: 'Azure AD Connect-synchronisatie: veranderende Hallo AD DS-accountwachtwoord | Microsoft Docs'
description: Dit document onderwerp beschrijft hoe tooupdate Azure AD Connect na het wachtwoord op Hallo van Hallo AD DS-account wordt gewijzigd.
services: active-directory
keywords: AD DS-account, Active Directory-account, wachtwoord
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a>Hallo AD DS accountwachtwoord wijzigen
Hallo AD DS-account verwijst toohello gebruikersaccount gebruikt door Azure AD Connect toocommunicate met lokale Active Directory. Als u een wachtwoord op Hallo van Hallo AD DS-account wijzigt, moet u Azure AD Connect-synchronisatieservice bijwerken met het nieuwe wachtwoord Hallo. Anders Hallo die synchronisatie niet meer correct met Hallo synchroniseren kan on-premises Active Directory en u tegenkomt Hallo volgende fouten:

* In Hallo Synchronization Service Manager, een importeren of exporteren bewerking met de lokale AD mislukt **Nee-begin-referenties** fout.

* Onder de functie Logboeken van Windows hello toepassingslogboek bevat een fout opgetreden bij **gebeurtenis-ID 6000** en het bericht **'hello beheeragent 'contoso.com' mislukte toorun omdat Hallo referenties ongeldig zijn'** .


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a>Hoe tooupdate synchronisatieservice Hallo met een nieuw wachtwoord voor AD DS-account
tooupdate hello Synchronization Service met het nieuwe wachtwoord Hallo:

1. Hallo Synchronization Service Manager (START → Synchronization Service) starten.
</br>![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  

2. Ga toohello **Connectors** tabblad.

3. Selecteer Hallo **AD-Connector** die overeenkomt met toohello AD DS-account waarvoor u het wachtwoord is gewijzigd.

4. Onder **acties**, selecteer **eigenschappen**.

5. Selecteer in het pop-upvenster hello, **tooActive Directory-Forest verbinding**:

6. Geef de nieuwe wachtwoord Hallo van Hallo AD DS-account in Hallo **wachtwoord** textbox.

7. Klik op **OK** toosave Hallo nieuw wachtwoord en sluiten Hallo pop-upvenster.

8. Opnieuw opstarten hello Azure AD Connect-synchronisatieservice onder Windows Service Control Manager. Dit is tooensure die een verwijzing toohello oude wachtwoord is verwijderd uit cachegeheugen Hallo.

## <a name="next-steps"></a>Volgende stappen
**Overzichtsonderwerpen**

* [Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen](active-directory-aadconnectsync-whatis.md)

* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
