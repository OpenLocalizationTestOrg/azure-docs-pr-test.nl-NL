---
title: 'aaaAdmins beheren van gebruikers en apparaten: Azure MFA | Microsoft Docs'
description: Hier wordt beschreven hoe Hallo toochange gebruikersinstellingen zoals het forceren van Hallo gebruikers toodo bewijs-up-proces opnieuw.
documentationcenter: 
services: multi-factor-authentication
author: kgremban
manager: femila
ms.assetid: aac3b922-7cc1-428c-9044-273579aa7b5a
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8c35435e4f6504014d9a4f6f1b837639c3b53481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-user-settings-with-azure-multi-factor-authentication-in-hello-cloud"></a>Gebruikersinstellingen met Azure multi-factor Authentication in de cloud Hallo beheren
Als beheerder, kunt u Hallo gebruiker-en apparaatinstellingen volgende beheren:

* Gebruikers tooprovide contactmethoden opnieuw vereisen
* App-wachtwoorden verwijderen
* MFA is vereist op alle vertrouwde apparaten 

## <a name="require-users-tooprovide-contact-methods-again"></a>Gebruikers tooprovide contactmethoden opnieuw vereisen
Deze instelling dwingt Hallo gebruiker toocomplete Hallo-registratieproces opnieuw. Niet-browsertoepassingen blijven toowork als Hallo gebruiker app-wachtwoorden voor hen heeft.  U kunt Hallo gebruikers app-wachtwoorden verwijderen doordat u tevens **verwijdert alle bestaande app-wachtwoorden die worden gegenereerd door gebruikers Hallo geselecteerd**.

### <a name="how-toorequire-users-tooprovide-contact-methods-again"></a>Hoe toorequire gebruikers tooprovide contact opnemen met methoden opnieuw
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Selecteer aan de linkerkant Hallo **Azure Active Directory** > **gebruikers en groepen** > **alle gebruikers**.
3. Selecteer **multi-Factor Authentication**. Hallo multi-factor authentication-pagina wordt geopend. 
4. Controleer Hallo vak volgende toohello of meer gebruikers desgewenst toomanage. Een lijst met snelle stap opties weergegeven op de juiste Hallo. 
5. Selecteer **gebruikersinstellingen beheren**.
6. Hallo selectievakje voor **vereisen dat geselecteerde gebruikers tooprovide opnieuw contactmethoden**.
   ![Contactmethoden opgeven](./media/multi-factor-authentication-manage-users-and-devices/reproofup.png)
7. Klik op **Opslaan**.
8. Klik op **sluiten**.

## <a name="delete-users-existing-app-passwords"></a>App-wachtwoorden bestaande gebruikers verwijderen
Deze instelling verwijdert alle app-wachtwoorden voor Hallo die een gebruiker heeft gemaakt. Niet-browsertoepassingen die gekoppeld aan deze app-wachtwoorden zijn uitgeschakeld totdat een nieuwe appwachtwoord is gemaakt.

### <a name="how-toodelete-users-existing-app-passwords"></a>Hoe toodelete gebruikers bestaande app-wachtwoorden
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Selecteer aan de linkerkant Hallo **Azure Active Directory** > **gebruikers en groepen** > **alle gebruikers**.
3. Selecteer **multi-Factor Authentication**. Hallo multi-factor authentication-pagina wordt geopend. 
6. Controleer Hallo vak volgende toohello of meer gebruikers desgewenst toomanage. Een lijst met snelle stap opties weergegeven op de juiste Hallo. 
7. Selecteer **gebruikersinstellingen beheren**.
8. Hallo selectievakje voor **verwijdert alle bestaande app-wachtwoorden die worden gegenereerd door gebruikers Hallo geselecteerd**.
   ![App-wachtwoorden verwijderen](./media/multi-factor-authentication-manage-users-and-devices/deleteapppasswords.png)
9. Klik op **Opslaan**.
10. Klik op **sluiten**.

## <a name="restore-mfa-on-all-remembered-devices-for-a-user"></a>MFA op alle onthouden apparaten voor een gebruiker herstellen
Een van de configureerbare functies Hallo van Azure multi-factor Authentication geeft uw gebruikers Hallo optie toomark apparaten als vertrouwd. Zie voor meer informatie [Azure multi-factor Authentication configureren instellingen](multi-factor-authentication-whats-next.md#remember-multi-factor-authentication-for-devices-that-users-trust).

Gebruikers kunnen de verificatie in twee stappen voor een configureerbare aantal dagen op hun apparaten reguliere afmelden. Als een account wordt aangetast of een vertrouwd apparaat verloren is, u moet toobe kunnen tooremove Hallo vertrouwde status en opnieuw verificatie in twee stappen vereist.

Hallo **terugzetten meervoudige verificatie op alle onthouden apparaten** instelling betekent dat die gebruiker Hallo tooperform gecontroleerd in twee stappen verificatie Hallo volgende keer dat ze zich aanmelden, ongeacht of ze hebt gekozen toomark hun het apparaat als vertrouwd. 

### <a name="how-toorestore-mfa-on-all-suspended-devices-for-a-user"></a>Hoe toorestore MFA op alle onderbroken apparaten voor een gebruiker
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Selecteer aan de linkerkant Hallo **Azure Active Directory** > **gebruikers en groepen** > **alle gebruikers**.
3. Selecteer **multi-Factor Authentication**. Hallo multi-factor authentication-pagina wordt geopend. 
6. Controleer Hallo vak volgende toohello of meer gebruikers desgewenst toomanage. Een lijst met snelle stap opties weergegeven op de juiste Hallo. 
7. Selecteer **gebruikersinstellingen beheren**.
8. Hallo selectievakje voor **terugzetten meervoudige verificatie op alle onthouden apparaten**
   ![app-wachtwoorden verwijderen](./media/multi-factor-authentication-manage-users-and-devices/rememberdevices.png)
9. Klik op **Opslaan**.
10. Klik op **sluiten**.

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over het te verkrijgen[instellingen van Azure multi-factor Authentication configureren](multi-factor-authentication-whats-next.md)

- Als uw gebruikers hulp nodig hebt, wijst u ze naar Hallo [gebruikershandleiding voor de verificatie in twee stappen](./end-user/multi-factor-authentication-end-user.md)
