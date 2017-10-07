---
title: aaaSet van verificatie in twee stappen voor mijn werk of school-account | Microsoft Docs
description: 'Wanneer uw bedrijf Azure multi-factor Authentication configureert, kunt u zich na vragen aan gebruiker toosign voor verificatie in twee stappen. Meer informatie over hoe tooset het. '
services: multi-factor-authentication
keywords: hoe toouse azure directory, active directory in de cloud hello, active directory-zelfstudie
documentationcenter: 
author: kgremban
manager: femila
editor: pblachar
ms.assetid: 46f83a6a-dbdd-4375-8dc4-e7ea77c16357
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2d0348081eefa42c23de2047044688879dcb5966
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-my-account-for-two-step-verification"></a>Mijn account voor verificatie in twee stappen instellen
Verificatie in twee stappen is een extra beveiligingsstap die voorkomen dat uw account door waardoor het moeilijker voor andere mensen toobreak in. Als u dit artikel leest ontvangen u waarschijnlijk een e-mailbericht van uw werk of school-beheerder over meervoudige verificatie. Of misschien heeft geprobeerd toosign in en krijg een bericht waarin u wordt gevraagd tooset up aanvullende beveiligingsverificatie. Als dat Hallo-geval **je niet aanmelden totdat u Hallo-proces voor automatische inschrijving hebt voltooid**.

Dit artikel helpt u bij het instellen van uw **werk- of schoolaccount**. Als u wilt dat de verificatie in twee stappen tooenable voor uw eigen persoonlijke Microsoft-account, Zie [over verificatie in twee stappen](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).

## <a name="set-up-your-account"></a>Instellen van uw account

Als uw IT-afdeling vereist dat u toostart met verificatie in twee stappen, een scherm de melding **uw beheerder heeft ingesteld dat u dit account voor aanvullende beveiligingsverificatie ingesteld** wordt weergegeven:

![Instellen](./media/multi-factor-authentication-end-user-first-time/first.png)

tooget gestart, selecteer **het nu instellen.**

Als u een scherm als volgt wanneer u zich aanmeldt niet ziet, volgt u de aanwijzingen Hallo in [beheren van uw instellingen voor verificatie in twee stappen](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page) toofind Hallo instellingenpagina waar u uw opties voor verificatie kunt beheren. 

## <a name="decide-how-you-want-tooverify-your-sign-ins"></a>Bepalen hoe u tooverify uw aanmeldingen

de eerste vraag Hallo in Hallo inschrijvingsproces is hoe u wilt dat ons toocontact u. Kijk eens naar Hallo opties in de tabel Hallo en Hallo koppelingen toogo toohello setup stappen voor elke methode gebruiken.

| Contactmethode | Beschrijving |
| --- | --- |
| [Mobiele app](#use-a-mobile-app-as-the-contact-method) |- **Meldingen voor verificatie ontvangen.** Deze optie wordt een melding toohello verificator-app op uw smartphone of tablet. Hallo melding weergeven en als deze geldig is, selecteert u **verifiëren** in Hallo-app. Uw werk of school verlangen dat u een PINCODE invoeren voordat u gaat verifiëren.<br>- **Verificatiecode gebruiken.** In deze modus genereert Hallo verificator-app een bevestigingscode die updates van elke 30 seconden. Voer de verificatiecode voor meest recente-Hallo in Hallo-aanmelden-interface.<br>Hallo Microsoft Authenticator-app is beschikbaar voor [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), en [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |
| [Mobiele telefoon telefoongesprek of tekstbericht](#use-your-mobile-phone-as-the-contact-method) |- **Telefoonoproep** plaatst een geautomatiseerde stem aanroep toohello telefoonnummer dat u opgeeft. Hallo-oproep wordt beantwoord en druk op # in Hallo phone toetsenblok tooauthenticate.<br>- **SMS-bericht** eindigt een SMS-bericht met een verificatiecode. Na de prompt in de tekst hello Hallo toohello tekstbericht te beantwoorden of Voer de verificatiecode Hallo opgegeven in Hallo-aanmelden-interface. |
| [Office-telefoongesprek](#use-your-office-phone-as-the-contact-method) |Een geautomatiseerde stem aanroep toohello telefoonnummer dat die u opgeeft, wordt geplaatst. Antwoord Hallo aanroepen en drukt # in op Hallo phone toetsenblok tooauthenticate. |

## <a name="use-a-mobile-app-as-hello-contact-method"></a>Een mobiele app gebruiken als primaire contactmethode Hallo
Met deze methode is vereist dat u een verificator-app op uw telefoon of tablet installeren. Hallo stappen in dit artikel zijn gebaseerd op Hallo Microsoft Authenticator-app, die beschikbaar is voor [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), en [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

1. Selecteer **mobiele app** uit de vervolgkeuzelijst Hallo.
2. Selecteer een **ontvangen van meldingen voor verificatie** of **verificatiecode gebruiken**, selecteer daarna **instellen**.

   ![Extra beveiliging verificatie scherm](./media/multi-factor-authentication-end-user-first-time/mobileapp.png)

3. Open Hallo-app op uw telefoon of tablet, en selecteer  **+**  tooadd een account. (Op Android-apparaten Hallo Selecteer drie punten vervolgens **account toevoegen**.)
4. Geef een account voor werk of school tooadd. Hallo QR-code scanner op uw telefoon wordt geopend. Als uw camera niet goed werkt is, kunt u tooenter gegevens van uw bedrijf handmatig. Zie voor meer informatie [handmatig toevoegen van een account](#add-an-account-manually).  
5. Hallo QR-Codeafbeelding die werden weergegeven met Hallo scherm voor het configureren van de mobiele app Hallo scannen.  Selecteer **gedaan** tooclose QR-code welkomstscherm.  

   ![QR-code scherm](./media/multi-factor-authentication-end-user-first-time/scan2.png)

6. Wanneer de activering is voltooid op Hallo telefoon, selecteert u **Contact met mij opnemen**.  Deze stap wordt een melding of een verificatie code tooyour telefoon verzonden. Selecteer **controleren**.  
7. Als uw bedrijf een PINCODE voor het goedkeuren van aanmelden verificatie vereist, voert u.

   ![Vak voor het invoeren van een PINCODE](./media/multi-factor-authentication-end-user-first-time/scan3.png)

8. Nadat de pincode is voltooid, selecteert u **sluiten**. Op dit moment is uw verificatie voltooid.
9. Het is raadzaam dat u uw mobiele telefoonnummer invoeren als u toegang tooyour mobiele app verliest. Geef uw land op in de vervolgkeuzelijst Hallo en voer uw mobiele telefoonnummer in Hallo volgende toohello landnaam. Selecteer **volgende**.
10. Op dit moment bent u na vragen aan gebruiker tooset van app-wachtwoorden voor niet-browsertoepassingen zoals Outlook 2010 of ouder of Hallo systeemeigen e-mail-app op apparaten van Apple. Deze actie is omdat sommige apps bieden geen ondersteuning voor verificatie in twee stappen. Als u deze apps niet gebruikt, klikt u op **gedaan** en Hallo rest van deze stappen overslaan.
11. Als u deze apps gebruikt, worden de kopie Hallo app-wachtwoord opgegeven en plak deze in uw toepassing in plaats van uw normale wachtwoord. U kunt Hallo hetzelfde appwachtwoord voor meerdere apps. Voor meer informatie [help met app-wachtwoorden].
12. Klik op **Gereed**.

### <a name="add-an-account-manually"></a>Handmatig toevoegen van een account
Ga als volgt te werk als u wilt dat een account toohello mobiele app tooadd handmatig, in plaats van Hallo QR-lezer.

1. Selecteer Hallo **account handmatig invoeren** knop.  
2. Voer Hallo code en URL Hallo die zijn opgegeven op Hallo Hallo dezelfde pagina waarin u een streepjescode. Deze gegevens gaat in Hallo **Code** en **URL** vakken op Hallo mobiele app.

    ![Instellen](./media/multi-factor-authentication-end-user-first-time/barcode2.png)
3. Wanneer het Hallo-activering is voltooid, selecteert u **Contact met mij opnemen**. Deze stap wordt een melding of een verificatie code tooyour telefoon verzonden. Selecteer **controleren**.

## <a name="use-your-mobile-phone-as-hello-contact-method"></a>Uw mobiele telefoon gebruiken als primaire contactmethode Hallo
1. Selecteer **telefoon voor authenticatie** uit de vervolgkeuzelijst Hallo.  

    ![Instellen](./media/multi-factor-authentication-end-user-first-time/phone.png)  
2. Uw land kiezen uit de vervolgkeuzelijst Hallo en voer uw mobiele telefoonnummer.
3. Selecteer Hallo-methode die u liever toouse met uw mobiele telefoon - tekstbericht of telefoongesprek.
4. Selecteer **Contact met mij opnemen** tooverify uw telefoonnummer. Afhankelijk van Hallo door u geselecteerde modus, we sturen je een tekst of u bellen. Volg Hallo instructies op het welkomstscherm en selecteer vervolgens **controleren**.
5. Op dit moment bent u na vragen aan gebruiker tooset van app-wachtwoorden voor niet-browsertoepassingen zoals Outlook 2010 of ouder of Hallo systeemeigen e-mail-app op apparaten van Apple. Deze actie is omdat sommige apps bieden geen ondersteuning voor verificatie in twee stappen. Als u deze apps niet gebruikt, klikt u op **gedaan** en rest Hallo Hallo stappen overslaan.
6. Als u deze apps gebruikt, worden de kopie Hallo app-wachtwoord opgegeven en plak deze in uw toepassing in plaats van uw normale wachtwoord. U kunt Hallo hetzelfde appwachtwoord voor meerdere apps. Voor meer informatie [help met app-wachtwoorden].
7. Klik op **Gereed**.

## <a name="use-your-office-phone-as-hello-contact-method"></a>Uw telefoon (werk) gebruiken als primaire contactmethode Hallo
1. Selecteer **telefoon (werk)** in de vervolgkeuzelijst Hallo  

    ![Instellen](./media/multi-factor-authentication-end-user-first-time/office.png)  
2. Hallo vak telefoonnummer wordt automatisch gevuld met de contactgegevens van uw bedrijf. Als het Hallo-nummer is onjuist of ontbreekt, vraag uw beheerder toomake wijzigingen.
3. Selecteer **Contact met mij opnemen** tooverify uw telefoonnummer en wij belt het nummer van uw. Volg Hallo instructies op het welkomstscherm en selecteer vervolgens **controleren**.
4. Op dit moment bent u na vragen aan gebruiker tooset van app-wachtwoorden voor niet-browsertoepassingen zoals Outlook 2010 of ouder of Hallo systeemeigen e-mail-app op apparaten van Apple. Deze actie is omdat sommige apps bieden geen ondersteuning voor verificatie in twee stappen. Als u deze apps niet gebruikt, klikt u op **gedaan** en rest Hallo Hallo stappen overslaan.
5. Als u deze apps gebruikt, worden de kopie Hallo app-wachtwoord opgegeven en plak deze in uw toepassing in plaats van uw normale wachtwoord. U kunt Hallo hetzelfde appwachtwoord voor meerdere apps. Zie voor meer informatie [wat zijn App-wachtwoorden](multi-factor-authentication-end-user-app-passwords.md).
6. Klik op **Gereed**.

## <a name="next-steps"></a>Volgende stappen
* Wijzig de gewenste opties en [beheren van uw instellingen voor verificatie in twee stappen](multi-factor-authentication-end-user-manage-settings.md)
* Instellen van [app-wachtwoorden](multi-factor-authentication-end-user-app-passwords.md) voor systeemeigen apparaat-apps die verificatie in twee stappen niet ondersteunen.
* Bekijk Hallo [Microsoft Authenticator-app](microsoft-authenticator-app-how-to.md) veilige authenticatie voor een snelle, zelfs wanneer er geen service van de cel.

