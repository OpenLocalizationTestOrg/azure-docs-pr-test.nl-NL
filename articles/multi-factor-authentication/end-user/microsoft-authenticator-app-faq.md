---
title: aaaMicrosoft verificator-app help en ondersteuning | Microsoft Docs
description: Geeft een lijst met veelgestelde vragen en antwoorden gerelateerde toohello Microsoft Authentication-app en Azure multi-factor Authentication.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f04d5bce-e99e-4f75-82d1-ef6369be3402
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: afba9b59ccaac60d022e8516fcf573dcfbf68af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-authenticator-app-faq"></a>Veelgestelde vragen over Microsoft Authenticator-app

In dit artikel antwoorden op veelgestelde vragen die we over Hallo Microsoft Authenticator-app ontvangen. Als u een vraag beantwoorden tooyour niet ziet, gaat u toohello [Microsoft Authenticator-app-forum](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp). We hebben ook een andere veelgestelde vragen over een bepaalde functie op Hallo-app [aanmelden met uw telefoon Veelgestelde vragen over](microsoft-authenticator-app-phone-signin-faq.md).

Hallo Microsoft Authenticator-app vervangen hello Azure Authenticator-app en wordt Hallo aanbevolen app bij het gebruik van Azure multi-factor Authentication. Hallo Microsoft Authenticator-app is beschikbaar voor [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), en [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

### <a name="what-are-hello-codes-in-hello-app-for-why-does-hello-number-keep-counting-down"></a>Wat zijn Hallo-codes in Hallo-app voor? Waarom Hallo nummer houden tellen omlaag?

Als u Hallo Microsoft Authenticator-app opent, ziet u Hallo-accounts die u hebt toegevoegd en een nummer 6-cijferige of acht door elk van deze. U ziet een timer die 30 seconden.

Deze codes worden gebruikt wanneer u zich aanmeldt tooyour-account. Nadat u uw gebruikersnaam en wachtwoord hebt ingevoerd, u mogelijk gevraagd tooenter een verificatiecode. Open Hallo Microsoft Authenticator-app en kopieer Hallo code die wordt weergegeven. Voer deze code in Hallo aanmeldingspagina toofinish.

Hallo reden dat Hallo Hallo codes wijziging elke 30 seconden is zodat u nooit gebruikt dezelfde code twee keer. Het is niet als een wachtwoord dat u tooremember verwacht. Hallo idee is dat alleen gebruikers met toegang tooyour phone uw verificatiecode kent.

Hallo-codes nodig geen internet of gegevens, zodat er geen tooworry over een telefoon service toosign in. Wanneer u de app Hallo sluit, wordt niet behouden op Hallo achtergrond uitgevoerd en deze niet verwijderen uit de accu. U kunt Hallo-app sluiten en deze totdat de volgende keer dat u zich aanmeldt Hallo negeren.  

### <a name="i-only-get-notifications-when-i-have-hello-app-open-if-hello-app-isnt-open-i-dont-get-any-notifications"></a>Ik krijg alleen meldingen wanneer ik heb Hallo app openen. Als het Hallo-app niet is geopend, krijg ik geen meldingen.

Als u meldingen krijgt, maar ze niet ruis maken of Trillen ondanks uw belsignaal wordt op, Controleer eerst Hallo app-instellingen. Hallo app toouse geluid inschakelen of Trillen met meldingen.

Als u geen meldingen op alle krijgt, controleert u Hallo volgende gevallen:

- Uw telefoon is niet storen of stille modus? Deze modus kan voorkomen dat apps verzenden van meldingen.
- Kunt u meldingen ontvangen van andere apps? Als dat niet het geval is, kan er een probleem met de netwerkverbindingen Hallo op uw telefoon of Hallo meldingen kanaal van Android- of Apple. U kunt de eerste optie Hallo oplossen in de instellingen van uw telefoon, maar mogelijk moet u tootalk tooyour serviceprovider voor hulp bij de tweede optie Hallo.
- Kunt u meldingen voor sommige accounts op Hallo-app, maar andere niet ontvangen? Zo ja, Hallo problematisch account niet verwijderen uit uw app en voeg deze opnieuw tooenable pushmeldingen. 

Als u probeert deze suggesties voor het oplossen van problemen, maar nog steeds problemen ondervindt, stuur ons uw logboeken voor diagnostische gegevens. Ga toohello app-instellingen en selecteer vervolgens **Help en feedback** en **logboeken verzenden**. Ga vervolgens toohello [Microsoft Authenticator-app-forum](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp) en laat ons weten wat u ziet, probleem- en welke stappen u hebt geprobeerd tot nu toe. 

### <a name="im-already-using-hello-microsoft-authenticator-application-for-verification-codes-how-do-i-switch-tooone-click-push-notifications"></a>Ik gebruik al Hallo Microsoft Authenticator-toepassing voor verificatiecodes. Hoe schakel ik tooone Klik pushmeldingen?
Goedkeuren van een aanmeldingspagina via push-bericht is alleen beschikbaar voor persoonlijke Microsoft-accounts of werken en Microsoft-accounts, niet voor de accounts van derden zoals Google of Facebook school. Als u een werk- of school Microsoft-account hebt, kunt uw organisatie toodisable deze optie.

Als u een Microsoft-account voor uw persoonlijke account gebruiken en tooswitch via toopush meldingen, moet u tooadd je account opnieuw. Hallo-apparaat met je account opnieuw te registreren en pushmeldingen in te stellen.  

Als u Microsoft Authenticator voor de account van uw werk of school gebruiken, moet uw organisatie besluit of tooallow één muisklik meldingen.

### <a name="do-one-click-push-notifications-work-for-non-microsoft-accounts"></a>Werken pushmeldingen met één Klik voor niet-Microsoft-accounts?
Nee, werken pushmeldingen alleen met Microsoft-accounts en Azure Active Directory-accounts. Als uw werk of school gebruikmaakt van Azure AD-accounts, kunnen ze deze functie uitschakelen.  

### <a name="i-restored-my-device-from-a-backup-and-my-account-codes-are-missing-or-not-working-what-happened"></a>Ik mijn apparaat hersteld vanaf een back-up en Mijn accountcodes zijn ontbreekt of niet werkt. Wat is er gebeurd?
Om veiligheidsredenen herstellen niet we accounts vanuit back-ups van app.  Wanneer u Hallo app hebt hersteld, moet uw accounts verwijderen en deze opnieuw toevoegen.

### <a name="i-got-a-new-device-how-do-i-remove-hello-microsoft-authenticator-app-from-my-old-device-and-move-toohello-new-one"></a>Ik heb een nieuw apparaat. Hoe ik Hallo Microsoft Authenticator-app verwijderen uit het oude apparaat en toohello nieuwe verplaatsen?
Toe te voegen Hallo Microsoft Authenticator-app tooa nieuw apparaat wordt niet automatisch verwijderd van alle andere apparaten. toomanage welke apparaten zijn geconfigureerd voor uw account, gaat u naar Hallo dezelfde website gebruik van de verificatie in twee stappen toomanage en tooremove oude apps kiest.

Deze website is voor persoonlijke Microsoft-accounts, uw [accountbeveiliging](https://account.microsoft.com/security) pagina. Voor Microsoft-accounts, werk- of schoolaccount, deze website is mogelijk een [MyApps](https://myapps.microsoft.com) of een aangepaste portal die uw organisatie is ingesteld.

### <a name="how-do-i-remove-an-account-from-hello-app"></a>Hoe verwijder ik een account uit Hallo-app
* iOS: van de belangrijkste welkomstscherm Veeg links op de tegel van een account. Selecteer **Verwijderen**.
* Windows Phone: Belangrijkste welkomstscherm Selecteer in de menuknop hello, vervolgens **accounts bewerken**. Tik op Hallo **X** volgende toohello accountnaam.
* Android: Belangrijkste welkomstscherm Selecteer in de menuknop hello, vervolgens **accounts bewerken**. Tik op Hallo **X** volgende toohello accountnaam.

Als u een apparaat dat is geregistreerd bij uw organisatie hebt, moet u mogelijk een extra stap tooremove toocomplete uw account. Op deze apparaten Hallo Microsoft Authenticator-app automatisch als de apparaatbeheerder van een geregistreerd. Als u wilt dat toocompletely verwijderen Hallo app, moet u toofirst Hallo-app in de instellingen van de app Hallo registratie.

### <a name="why-does-hello-app-request-so-many-permissions"></a>Waarom vraagt Hallo app zo veel machtigingen
Hier volgt een volledige lijst met machtigingen vragen we voor en hoe ze worden gebruikt in Hallo-app. Hallo specifieke machtigingen die u ziet, is afhankelijk van Hallo type telefoon die u hebt.

* **Camera**: We uw camera tooscan QR-codes gebruiken wanneer u een werk-, school- of niet-Microsoft-account toevoegt.
* **Contactpersonen en phone**: wanneer u zich met je persoonlijke Microsoft-account aanmeldt, we toosimplify Hallo proces proberen door te zoeken naar bestaande accounts die u op uw telefoon gebruikt.
* **SMS**: wanneer u zich met je persoonlijke Microsoft-account voor Hallo eerst aanmeldt, hebben we toomake ervoor dat uw telefoon aantal overeenkomsten Hallo een wij in de record hebben. We sturen een SMS-bericht toohello telefoon waar u Hallo app gedownload. Hallo-bericht bevat een 6-8 cijfers-verificatiecode. In plaats van toofind waarin u wordt gevraagd deze code en voer deze in-app Hallo we vinden in Hallo tekstbericht voor u.
* **Tekenen via andere apps**: wanneer u een melding tooverify uw identiteit ontvangt, we dat meldingen worden weergeven via alle andere Apps die kan worden uitgevoerd.
* **Gegevens ontvangen van Hallo internet**: deze machtiging is vereist voor het verzenden van meldingen.
* **Telefoon voorkomen in de slaapstand**: als u uw apparaat bij uw organisatie registreren, kunnen dit beleid op uw telefoon wijzigen.
* **Beheren van trillingen**: U kunt kiezen of u een trillingen dat wilt wanneer u een melding tooverify uw identiteit ontvangt.
* **Vingerafdruk hardware gebruiken**: sommige accounts werk- en schoolaccounts een extra PINCODE is vereist wanneer u uw identiteit verifiëren. toomake hello proces eenvoudiger, kunt u toouse uw vingerafdruk in plaats van het invoeren van Hallo PINCODE.
* **Netwerkverbindingen weergeven**: wanneer u een Microsoft-account toevoegt, Hallo app netwerk/internet connection vereist.
* **Hallo-inhoud van uw opslag lezen**: met deze machtiging wordt alleen gebruikt wanneer u een technisch probleem via de app-instellingen voor Hallo rapporteert. Sommige gegevens van uw opslag wordt verzameld toodiagnose Hallo probleem.
* **Volledige toegang tot het netwerk**: deze machtiging is vereist voor het verzenden van meldingen tooverify uw identiteit.
* **Uitgevoerd bij het opstarten**: als u uw telefoon opstarten, deze machtiging zorgt ervoor dat u blijven ontvangen van meldingen tooverify uw identiteit.

### <a name="why-does-hello-microsoft-authenticator-app-allow-you-tooapprove-a-request-without-unlocking-hello-device"></a>Waarom Hallo Microsoft verificator-App in staat tooapprove een aanvraag zonder ontgrendelen Hallo-apparaat?

U hebt geen toounlock die uw apparaat tooapprove verificatie aanvragen omdat u tooprove hoeft u uw telefoon bij u hebben. Verificatie in twee stappen vereist twee dingen: een ding dat u weet en een dat die u hoeft aan te tonen. Hallo wat die u weet, is uw wachtwoord. Hallo dat die u hoeft is uw telefoon (ingesteld met Hallo Microsoft Authenticator-app en geregistreerd als een bewijs MFA) Daarom hoeven Hallo telefoon en voldoet aan de criteria voor de tweede factor authentication Hallo HALLO hallo-aanvraag goedkeuren. 

### <a name="what-does-hello-lock-icon-in-hello-account-list-mean"></a>Wat betekent Hallo vergrendelingspictogram in de lijst met accounts Hallo?

Hallo hangslot geeft aan dat het Hallo-apparaat is geregistreerd in Azure AD en toohello account geregistreerd. Apparaatregistratie voor iOS-vindt plaats tijdens de inschrijving bij Microsoft Intune.

## <a name="next-steps"></a>Volgende stappen

### <a name="contact-us"></a>Contact opnemen
Als uw vraag hier niet is beantwoord, willen we toohear van u. Ga toohello [Microsoft Authenticator-app-forum](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp) toopost vraag en get help van Hallo-community of een opmerking op deze pagina laat.


### <a name="related-topics"></a>Verwante onderwerpen
* [Over verificatie in twee stappen](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification) voor Microsoft-accounts
* [Problemen met verificatie in twee stappen](multi-factor-authentication-end-user-troubleshoot.md) voor uw werk of school-account?
* [Hallo Microsoft Authenticator toosign in op uw telefoon gebruiken](microsoft-authenticator-app-phone-signin-faq.md)

