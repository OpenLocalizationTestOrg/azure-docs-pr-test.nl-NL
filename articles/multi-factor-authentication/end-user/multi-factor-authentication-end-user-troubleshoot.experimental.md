---
title: Verificatie in twee stappen oplossen | Microsoft Docs
description: Dit document bevatten gebruikers informatie over wat te doen als ze worden uitgevoerd in een probleem met de Azure multi-factor Authentication.
services: multi-factor-authentication
keywords: multifactor-verificatie-client, verificatieprobleem, correlatie-ID
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 8f3aef42-7f66-4656-a7cd-d25a971cb9eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: end-user
ms.openlocfilehash: 9dbe88a59b68bfb424c43dd89acf55d8c73fdf39
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="get-help-with-two-step-verification"></a>Hulp bij de verificatie in twee stappen
Dit artikel worden de meest voorkomende vragen over verificatie in twee stappen. 

## <a name="why-do-i-have-to-perform-two-step-verification-can-i-turn-it-off"></a>Waarom heb ik verificatie in twee stappen uitvoeren? Kan ik uitschakelen?

Verificatie in twee stappen is een beveiligingsfunctie waarmee uw organisatie gebruiken wilt voor het beveiligen van uw accounts. Het is veiliger dan alleen een wachtwoord, omdat deze afhankelijk van twee soorten verificatie is: iets u kent en iets u bij u hebben. Er is iets die u weet dat uw wachtwoord. Iets die u bij u hebben nu een telefoonnummer of het apparaat die u doorgaans bij u hebben. Wanneer uw account is beveiligd met verificatie in twee stappen, kan niet een kwaadwillende persoon aanmelden als u zelfs als ze uw wachtwoord ophalen. Ze kunnen zich aanmelden omdat ze geen toegang tot uw telefoon hebt. 

Microsoft biedt verificatie in twee stappen, maar uw organisatie kiest voor de functie. U kunt geen opt-out als uw IT-afdeling van u, vereist net zoals u kunnen zich niet afmelden met een wachtwoord op uw account te beschermen. 

Als u verificatie in twee stappen ingeschakeld voor uw persoonlijke Microsoft-account hebt en wilt uw instellingen wijzigen, lezen [over verificatie in twee stappen](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification) in plaats daarvan. 

## <a name="i-dont-have-my-phone-with-me-today"></a>Ik heb geen mijn telefoon met mij vandaag

Een aantal dagen dat u uw telefoon bij u thuis, maar nog steeds laat moeten zich aanmelden op het werk. Het eerste wat dat u moet proberen is aanmelden met een andere verificatiemethode. Bij de registratie voor verificatie in twee stappen stelt u meer dan één telefoonnummer? Aanmelden met een andere methode, Ga als volgt te werk:

1. Meld u aan als u dat gewend bent.
2. Wanneer de pagina van de verificatie in twee stappen is geopend, klikt u **gebruik een andere verificatieoptie**.

   ![Andere verificatie](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)

3. Selecteer de verificatieoptie die u wilt gebruiken. 
  - Als u geen toegang tot uw alternatieve methoden ofwel hebt, neem dan contact op met uw IT-afdeling voor hulp bij het aanmelden bij uw account.
  - Als u toegang tot uw alternatieve methoden hebt, gaat u verder met verificatie in twee stappen.

Als er geen de **gebruik een andere verificatieoptie** koppelen, en dit betekent u hebt alternatieve methoden ingesteld dat toen u het eerst geregistreerd voor verificatie in twee stappen. Neem contact op met uw IT-afdeling voor hulp bij het aanmelden bij uw account. Nadat u bent aangemeld, zorg ervoor dat u [de instellingen beheren](multi-factor-authentication-end-user-manage-settings.md) extra verificatiemethoden voor de volgende keer toevoegen. 

## <a name="i-lost-my-phone-or-got-a-new-number"></a>Ik mijn telefoon verlies of hebt u een nieuw nummer
Er zijn twee manieren om terug te gaan bij uw account. De eerste is aan te melden met uw telefoonnummer alternatieve verificatie als u een hebt ingesteld. De tweede is het vraag uw IT-afdeling om uw instellingen te wissen.

Als uw telefoon is kwijtgeraakt of gestolen is, wordt ook aangeraden dat u uw IT-afdeling zien. Moet u uw appwachtwoorden opnieuw instellen en wis alle onthouden apparaten. 

### <a name="use-an-alternate-phone-number"></a>Een alternatief telefoonnummer gebruiken
Als u meerdere verificatie-opties, zoals een tweede telefoonnummer of een verificator-app op een ander apparaat instellen gebruikt u een van deze aan te melden.

Om aan te melden met behulp van de alternatief telefoonnummer, de volgende stappen uit:

1. Meld u aan als u dat gewend bent.
2. Wanneer u wordt gevraagd naar uw account verder verifiëren, kiezen **gebruik een andere verificatieoptie**.
   
   ![Andere verificatie](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)

3. Selecteer het telefoonnummer of een apparaat dat u toegang tot hebt.
4. Nadat u zich weer in uw account [de instellingen beheren](multi-factor-authentication-end-user-manage-settings.md) om het telefoonnummer van uw verificatie te wijzigen.

### <a name="clear-your-settings"></a>Uw instellingen verwijderen.
Als u een telefoonnummer van de secundaire verificatie niet hebt geconfigureerd, hebt u contact op met uw IT-afdeling voor hulp. Schakel laten uw instellingen zodat de volgende keer aanmelden, wordt u gevraagd naar [registreren voor verificatie in twee stappen](multi-factor-authentication-end-user-first-time.md) opnieuw.

## <a name="i-am-not-receiving-a-text-or-call-on-my-phone"></a>Ik ben niet ontvangen van een tekst of bel op mijn telefoon
Er zijn diverse redenen waarom u wilt mogelijk aanmelden, maar niet ontvangen van de tekst of telefoongesprek. Als je hebt ontvangen teksten of telefoontjes naar uw telefoon in het verleden, wordt dit probleem waarschijnlijk een probleem met de telefoon-provider niet uw account. Zorg ervoor dat er een signaal goed cel. En als u probeert een SMS-bericht ontvangen, zorg ervoor dat u zich kunt tekstberichten ontvangen. Vraag een vriend aan te roepen u of de tekst die u als een test. 

Als u enkele minuten een tekstbericht of telefoongesprek hebt gewacht, is de snelste manier om toegang te krijgen tot uw account om te proberen een andere optie.

1. Selecteer **gebruik een andere verificatieoptie** op de pagina die op uw verificatie wachten.
   
    ![Andere verificatie](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)
2. Selecteer de telefoon nummer of elk leveringsmodel methode die u wilt gebruiken.
   
    Als u meerdere verificatiecodes ontvangen, gebruikt u de nieuwste.

Als u een andere methode geconfigureerd hebt, neem contact op met uw IT-afdeling en vraag ze om uw instellingen te wissen. De volgende keer dat u zich aanmeldt, wordt u gevraagd naar [meervoudige verificatie instellen](multi-factor-authentication-end-user-first-time.md) opnieuw.

Als u vaak vertragingen vanwege ongeldige cel signaal hebt, raden wij aan u de [Microsoft Authenticator-app](microsoft-authenticator-app-how-to.md) op je smartphone. De app kan genereren willekeurige beveiligingscodes die u aan te melden en deze codes geen elke cel signaal of via internet verbinding vereist.

## <a name="app-passwords-are-not-working"></a>App-wachtwoorden werken niet
Controleer eerst of u het app-wachtwoord correct hebt ingevoerd. Het gegenereerde app-wachtwoord wordt vervangen door uw normale wachtwoord, maar alleen voor oudere desktoptoepassingen die verificatie in twee stappen niet ondersteunen. Als deze nog steeds niet werkt, probeer aanmelden en [een nieuw appwachtwoord maken](multi-factor-authentication-end-user-app-passwords.md).  Als deze nog steeds niet werkt, neem contact op met uw IT-afdeling en hebben ze [verwijderen van uw bestaande app-wachtwoorden](../multi-factor-authentication-manage-users-and-devices.md) en vervolgens maakt u een nieuwe.

## <a name="i-didnt-find-an-answer-to-my-problem"></a>Ik vinden een antwoord op mijn probleem niet.
Als u deze stappen hebt geprobeerd, maar wordt nog steeds uitgevoerd op problemen, neem dan contact op met uw IT-afdeling. Ze moeten mogelijk om u te helpen.

## <a name="related-topics"></a>Verwante onderwerpen
* [De instellingen voor verificatie in twee stappen beheren](multi-factor-authentication-end-user-manage-settings.md)  
* [Veelgestelde vragen over Microsoft Authenticator-toepassing](microsoft-authenticator-app-faq.md)

