---
title: aaaHow toouse App-wachtwoorden in Azure MFA? | Microsoft Docs
description: Deze pagina helpt gebruikers begrijpen wat app-wachtwoorden zijn en wat ze worden gebruikt voor met inachtneming van tooAzure MFA.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 3afa2003d8e87576f035bf9440a1dba67bd85f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a>Wat zijn App-wachtwoorden in Azure multi-factor Authentication?
Bepaalde niet-browsertoepassingen, zoals Hallo Apple systeemeigen e-mailclient die gebruikmaakt van Exchange Active Sync, ondersteunen momenteel geen multi-factor authentication-server. Multi-factor authentication is ingeschakeld per gebruiker.  Dit betekent dat een gebruiker multi-factor authentication-server niet gebruiken als:

- Hallo-gebruiker is ingeschakeld voor multi-factor authentication
- Hallo gebruiker probeert toouse een niet-browsertoepassing.

Een app-wachtwoord kunt Hallo gebruiker toouse Hallo app.

Zodra u een app-wachtwoord hebt, kunt u deze gebruiken in plaats van het oorspronkelijke wachtwoord met deze niet-browsertoepassingen. Wanneer u zich voor verificatie in twee stappen registreert, u bent zorgt ervoor dat Microsoft niet toolet iedereen Meld u aan met uw wachtwoord als ze ook Hallo tweede verificatie niet kunnen uitvoeren. Hallo Apple systeemeigen e-mailclient op uw telefoon kan niet aanmelden als u omdat deze kan niet om verificatie in twee stappen vragen. Hallo oplossing toothis probleem is een veiligere app-wachtwoord die u niet gebruikt toocreate dagelijkse. App-wachtwoorden zijn alleen voor apps die verificatie in twee stappen niet ondersteunt. Hallo app-wachtwoord gebruiken zodat apps kunnen multi-factor authentication overslaan en doorgaan toowork.


> [!NOTE]
> Office 2013-clients (inclusief Outlook) bieden ondersteuning voor nieuwe verificatieprotocollen en kan worden gebruikt met verificatie in twee stappen. App-wachtwoorden zijn niet vereist voor gebruik met Office 2013-clients.  Zie voor meer informatie [Office 2013 modern authentication openbare preview aangekondigd](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).


## <a name="how-toouse-app-passwords"></a>Hoe toouse app-wachtwoorden
Hier volgen enkele dingen tooknow over app-wachtwoorden:

* U kunt uw eigen app-wachtwoorden niet maken. Ze worden automatisch gegenereerd.
* Er is momenteel een limiet van 40 wachtwoorden per gebruiker. 
* Als u een app-wachtwoord toocreate probeert Hallo limiet is bereikt, hebt u toodelete een van uw bestaande app-wachtwoorden voordat u een nieuwe maakt.
* Gebruik één appwachtwoord per apparaat, niet per toepassing. U kunt bijvoorbeeld één app-wachtwoord voor uw laptop maken en dit app-wachtwoord gebruiken voor alle toepassingen op die laptop. Maak vervolgens een tweede app-wachtwoord toouse voor al uw apps op het bureaublad. 
* Krijgt u een app-wachtwoord Hallo eerste keer dat u zich registreert voor verificatie in twee stappen.  Als u aanvullende bepalingen nodig hebt, kunt u ze kunt maken.



## <a name="creating-and-deleting-app-passwords"></a>Maken en het verwijderen van app-wachtwoorden
Tijdens de eerste aanmelden krijgt u een app-wachtwoord die u kunt gebruiken.  U kunt ook maken en verwijderen van app-wachtwoorden later op. Hoe u app-wachtwoorden verwijderen, is afhankelijk van hoe u multi-factor authentication-server gebruiken. Antwoord Hallo volgen vragen toodetermine waar u toomanage app-wachtwoorden moet gaan: 

1. Gebruik je verificatie in twee stappen voor uw persoonlijke Microsoft-account? Zo ja, raadpleegt u toohello [App-wachtwoorden en verificatie in twee stappen](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) artikel voor hulp. Zo Nee, blijven tooquestion twee.

2. OK, zodat u verificatie in twee stappen voor uw werk of school-account gebruiken. Gebruik je deze toosign in tooOffice 365 apps? Zo ja, raadpleegt u te[maken van een app-wachtwoord voor Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) voor hulp. Zo Nee, blijven tooquestion drie. 

3. Gebruik je verificatie in twee stappen met Microsoft Azure? Zo ja, gaan toohello [beheren van appwachtwoorden in hello Azure-portal](#manage-app-passwords-in-the-Azure-portal) sectie van dit artikel. Zo Nee, blijven tooquestion vier.

4. Weet u niet waar u verificatie in twee stappen gebruiken? Doorgaan toohello [beheren van app-wachtwoorden met Hallo MyApps portal](#manage-app-passwords-with-the-myapps-portal) sectie van dit artikel. 


## <a name="manage-app-passwords-in-hello-azure-portal"></a>App-wachtwoorden in hello Azure-portal beheren
Als u verificatie in twee stappen met Azure gebruikt, u toocreate app-wachtwoorden via hello Azure-portal.

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a>app-wachtwoorden toocreate in hello Azure-portal
1. Meld u aan toohello klassieke Azure-portal.
2. Hallo boven aan met de rechtermuisknop op uw gebruikersnaam en aanvullende beveiligingsverificatie.
3. Selecteer op Hallo proofup pagina Hallo boven aan de app-wachtwoorden
4. Klik op **Create**.
5. Voer een naam op voor Hallo app-wachtwoord en klik op **volgende**
6. Hallo app wachtwoord toohello Klembord kopiëren en plakken in uw app.
   
   ![Cloud](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a>app-wachtwoorden toodelete in hello Azure-portal
1. Meld u aan toohello klassieke Azure-portal.
2. Hallo boven aan met de rechtermuisknop op uw gebruikersnaam en aanvullende beveiligingsverificatie.
3. Selecteer boven hello, volgende tooadditional beveiligingsverificatie, **app-wachtwoorden.**
4. Volgende toohello app-wachtwoord gewenste toodelete, selecteer **verwijderen**.
5. Hallo bevestigen door te klikken op **Ja**.
6. Zodra de app-wachtwoord Hallo zijn verwijderd, klikt u op **sluiten**.


## <a name="manage-app-passwords-with-hello-myapps-portal"></a>App-wachtwoorden met Hallo MyApps portal beheren.
Als u niet zeker weet hoe u meervoudige verificatie gebruiken, kunt klikt u altijd maken en verwijderen van app-wachtwoorden via Hallo myapps portal.

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a>een app-wachtwoord met toocreate Hallo Myapps portal
1. Aanmelden te[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. De naam van uw Hallo rechts bovenaan op en kies **profiel**.
3. Selecteer **aanvullende beveiligingsverificatie**.
   ![Selecteer aanvullende beveiligingsverificatie - schermafbeelding](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Selecteer **app-wachtwoorden**.
   ![Selecteer de app-wachtwoorden - schermafbeelding](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Klik op **Create**.
6. Voer een naam op voor Hallo app-wachtwoord en klik op **volgende**.
7. Hallo app wachtwoord toohello Klembord kopiëren en plakken in uw app.
   ![Een app-wachtwoord maken](./media/multi-factor-authentication-end-user-app-passwords/create2.png)

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a>een app-wachtwoord met toodelete Hallo Myapps portal
1. Aanmelden te[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. Selecteer boven Hallo profiel.
3. Selecteer **aanvullende beveiligingsverificatie**.

   ![Selecteer aanvullende beveiligingsverificatie - schermafbeelding](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Selecteer **app-wachtwoorden**.

   ![Selecteer de app-wachtwoorden - schermafbeelding](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Volgende toohello app-wachtwoord gewenste toodelete, klikt u op **verwijderen**.

   ![Verwijderen van een app-wachtwoord](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. U wilt bevestigen dat toodelete dit wachtwoord door te klikken op **Ja**.
7. Zodra de app-wachtwoord Hallo zijn verwijderd, klikt u op **sluiten**.

## <a name="next-steps"></a>Volgende stappen

- [De instellingen van de verificatie in twee stappen beheren](multi-factor-authentication-end-user-manage-settings.md)

- Hallo uitproberen [Microsoft Authenticator-app](microsoft-authenticator-app-how-to.md) tooverify uw aanmeldingen met app-meldingen in plaats van de ontvangen tekst of aanroepen. 
