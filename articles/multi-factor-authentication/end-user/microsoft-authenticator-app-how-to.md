---
title: aaaMicrosoft verificator-app voor mobiele telefoons | Microsoft Docs
description: Meer informatie over hoe tooupgrade toohello meest recente versie van Azure Authenticator.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: d895d92d89613cbafd9fc09d4ff4810cbf25652e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-microsoft-authenticator-app"></a>Aan de slag met Hallo Microsoft Authenticator-app
Hallo Microsoft Authenticator-app biedt een extra beveiligingsniveau in uw werk of school-account (bijvoorbeeld bsimon@contoso.com) of uw Microsoft-account (bijvoorbeeld bsimon@outlook.com).

Hallo-app werkt op twee manieren:

* **Melding**. Hallo-app kunt u voorkomen dat onbevoegde toegang tooaccounts en frauduleuze transacties stoppen door een melding tooyour smartphone of tablet worden gepusht. Hallo melding alleen kunnen bekijken en als gerechtvaardigd is, selecteert u **controleren**. Anders kunt u **weigeren**. 
* **Verificatiecode**. Hallo-app kan worden gebruikt als een verificatiecode OAuth-token toogenerate een software. Nadat u uw gebruikersnaam en wachtwoord invoert, Voer Hallo code door Hallo-app in het welkomstscherm aanmelden. Hallo verificatiecode biedt een tweede vorm van verificatie.

Hallo Microsoft Authenticator-app vervangt hello Azure Authenticator-app. Hello Azure Authenticator-app werkt nog altijd, maar als u toomove toohello nieuwe Microsoft Authenticator-app besluit, in dit artikel kan u helpen.  

## <a name="opt-in-for-two-step-verification"></a>Opt-in voor verificatie in twee stappen

Hallo Microsoft Authenticator-app werkt niet op zichzelf. Elk van uw accounts tooprompt die u voor een tweede verificatiemethode nadat u zich met uw gebruikersnaam en wachtwoord aanmelden configureren. 

Om een werk- of schoolaccount krijgt u niet meestal toochoose deze functie voor uzelf. In plaats daarvan een beveiligingsbeheerder kiest namens jou en waarschuwt u tooregister verificatiemethoden voor uw account. Meer informatie in dit scenario is van toepassing tooyou, [wat Azure multi-factor Authentication betekent voor mij](multi-factor-authentication-end-user.md).

Voor een persoonlijke account moet u tooset van verificatie in twee stappen voor uzelf. Als u een Microsoft-account hebt, deze stappen zijn beschikbaar in [over verificatie in twee stappen](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification). 

U kunt ook Microsoft Authenticator hello gebruiken met niet-Microsoft-accounts. Ze kunnen Hallo functie iets anders dan verificatie in twee stappen aanroepen, maar u moet kunnen toofind deze onder de instellingen voor beveiliging of aanmelden. 

## <a name="install-hello-app"></a>Hallo-app installeren
Hallo Microsoft Authenticator-app is beschikbaar voor [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), en [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).

## <a name="add-accounts-toohello-app"></a>Accounts toohello app toevoegen
Voor elke account dat u wilt dat tooadd toohello Microsoft Authenticator-app, een Hallo volgen procedures te gebruiken:

### <a name="add-a-personal-microsoft-account-toohello-app"></a>Een persoonlijke toohello app van een Microsoft-account toevoegen

Voor een persoonlijk Microsoft-account (een toosign te gebruiken in tooOutlook.com, Xbox, Skype, enz.), hoeft u deze toodo is tooyour-account in Hallo Microsoft Authenticator-app aanmelden.

### <a name="add-a-work-or-school-account-toohello-app-using-hello-qr-code-scanner"></a>Toevoegen van een werk- of schoolaccount toohello app-account met de scanfunctie van Hallo QR-code
1. Ga scherm toohello beveiliging verificatie-instellingen.  Voor informatie over het scherm tooget toothis, Zie [wijzigen van uw beveiligingsinstellingen](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).
2. Selectievakje Hallo naast te**verificator-app** Selecteer **configureren**.

    ![knop voor Hallo configureren op het welkomstscherm beveiliging verificatie-instellingen](./media/authenticator-app-how-to/azureauthe.png)

    Hiermee wordt een scherm met een QR-code erop.

    ![Scherm waarmee Hallo QR-code](./media/authenticator-app-how-to/barcode2.png)
3. Open Hallo Microsoft Authenticator-app. Op Hallo **accounts** Schakel in het scherm  **+** , en geef vervolgens de gewenste tooadd een account voor werk of school.
4. Hallo camera tooscan Hallo QR-code gebruiken en selecteer vervolgens **gedaan** tooclose QR-code welkomstscherm.

    Als uw camera niet goed werkt is, kunt u [Hallo QR-code en URL handmatig invoeren](#add-an-account-to-the-app-manually).

5. Wanneer het Hallo-app toont de naam van uw account een 6-cijferige code eronder, kunt u klaar bent. 

    ![Accounts scherm](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-manually"></a>Een account toohello app handmatig toevoegen
1. Ga scherm toohello beveiliging verificatie-instellingen.  Voor informatie over het scherm tooget toothis, Zie [wijzigen van uw beveiligingsinstellingen](multi-factor-authentication-end-user-manage-settings.md).
2. Selecteer **configureren**.

    ![knop voor Hallo configureren op het welkomstscherm beveiliging verificatie-instellingen](./media/authenticator-app-how-to/azureauthe.png)

    Hiermee wordt een scherm met een QR-code erop.  Houd er rekening mee Hallo code en URL.

    ![Scherm waarmee Hallo QR-code en URL](./media/authenticator-app-how-to/barcode2.png)
3. Open Hallo Microsoft Authenticator-app. Op Hallo **accounts** Schakel in het scherm  **+** , en geef vervolgens de gewenste tooadd een account voor werk of school.

4. Selecteer in het Hallo-scanner **code handmatig invoeren**.

    ![Scherm voor het scannen van QR-code](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. Hallo-code en Hallo URL invoeren in de desbetreffende vakken Hallo in Hallo-app en selecteer vervolgens **voltooien**.

    ![Scherm voor het invoeren van code en URL](./media/authenticator-app-how-to/manual.png)

6. Wanneer het Hallo-app toont de naam van uw account een 6-cijferige code eronder, kunt u klaar bent.

    ![Accounts scherm](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-using-touch-id"></a>Een account toohello app Touch ID gebruikt toevoegen
Hallo Microsoft Authenticator-app voor iOS ondersteunt Touch-ID.  Azure multi-factor Authentication kunnen organisaties toorequire een PINCODE voor apparaten. Touch ID hoeft de iOS-gebruikers niet tooenter een PINCODE. In plaats daarvan ze kunnen hun vingerafdruk scannen en selecteer **goedkeuren**.

Instellen van Touch ID met Microsoft Authenticator is eenvoudig. Voltooi een challenge normale verificatie met een PINCODE. Als uw apparaat Touch ID ondersteunt, stelt Microsoft Authenticator deze automatisch voor dat account.

![Verificatie van Touch ID setup](./media/authenticator-app-how-to/touchid1.png)

Vanaf dat moment doorsturen, wanneer u klaar tooverify bent aangemeld, vereist u push-melding ontvangen Hallo selecteert en scannen van uw vingerafdruk in plaats van uw pincode.

![Push-melding](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-hello-app-when-you-sign-in"></a>Hallo-app gebruiken wanneer u zich aanmeldt

Als uw account is toegevoegd toohello app, hebt u mogelijk na vragen aan gebruiker toodo toomake van de test-verificatie of dat alles correct is geconfigureerd. Daarna kunt bent nu u klaar! U hoeft niet toodo iets anders tot hello volgende keer dat u zich aanmeldt.

Als u hebt gekozen toouse verificatiecodes in Hallo-app, start u toosee ze op Hallo-startpagina. Ze wijzigen elke 30 seconden zodat u altijd een nieuwe code hebt wanneer u een nodig. Maar u hoeft niet toodo mee totdat u zich aanmeldt, na vragen aan gebruiker tooenter een verificatiecode worden.  
