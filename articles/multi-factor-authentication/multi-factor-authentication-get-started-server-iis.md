---
title: aaaIIS verificatie en Azure MFA-Server | Microsoft Docs
description: Dit is hello Azure multi-factor authentication-pagina die u helpt bij het implementeren van IIS-verificatie en Azure multi-factor Authentication-Server.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d1bf1c8a-2c10-4ae6-9f4b-75f0c3df43eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017,it-pro
ms.openlocfilehash: 74bd39c2644e2bca0880baea3824cad4c9215111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-iis-web-apps"></a>Azure Multi-Factor Authentication-server configureren voor IIS-webtoepassingen

Hallo IIS-verificatiesectie van hello Azure multi-factor Authentication (MFA) Server tooenable gebruiken en configureren van IIS-verificatie voor integratie met Microsoft IIS-webtoepassingen. Hello Azure MFA-Server installeert een invoegtoepassing die u kunt filteren van aanvragen wordt toohello IIS web server tooadd Azure multi-factor Authentication. Hallo IIS-invoegtoepassing biedt ondersteuning voor verificatie op basis van een formulier en geïntegreerde Windows-verificatie voor HTTP. Goedgekeurde dat IP-adressen kan ook worden geconfigureerd tooexempt interne IP-adressen van tweeledige verificatie.

![IIS-authenticatie](./media/multi-factor-authentication-get-started-server-iis/iis.png)

## <a name="using-form-based-iis-authentication-with-azure-multi-factor-authentication-server"></a>IIS-verificatie samen gebruiken met Azure Multi-Factor Authentication-server
toosecure een IIS-webtoepassing die gebruikmaakt van verificatie op basis van formulieren, hello Azure multi-factor Authentication-Server op Hallo van IIS-webserver installeren en configureren Hallo Server per Hallo procedure te volgen:

1. Klik in hello Azure multi-factor Authentication-Server, op Hallo verificatie van IIS-pictogram in het linkermenu Hallo.
2. Klik op Hallo **op basis van formulieren** tabblad.
3. Klik op **Add**.
4. variabelen voor de gebruikersnaam, wachtwoord en domein toodetect automatisch Hallo aanmeldings-URL (bijvoorbeeld https://localhost/contoso/auth/login.aspx) in het dialoogvenster Hallo-formulier-gebaseerde Website invoeren en op **OK**.
5. Controleer Hallo **overeenkomende multi-factor Authentication-gebruiker vereisen** vak als alle gebruikers zijn of worden geïmporteerd in hello Server- en onderwerp toomulti-factorverificatie. Als een groot aantal gebruikers nog niet is geïmporteerd in Hallo Server en/of vrijgesteld van multi-factor authentication zijn zal, laat u Hallo vakje uitgeschakeld.
6. Als de paginavariabelen Hallo kunnen niet automatisch worden gedetecteerd, klikt u op **handmatig opgeven** in het dialoogvenster van Hallo formulier-gebaseerde Website.
7. Hallo URL toohello aanmeldingspagina invoeren in het veld van de indienings-URL Hallo Hallo formulier-gebaseerde Website in het dialoogvenster en voer een toepassingsnaam in (optioneel). de naam van de toepassing Hello wordt weergegeven in de Azure multi-factor Authentication-rapporten en kan worden weergegeven in verificatieberichten via SMS of mobiele App.
8. Selecteer de juiste Aanvraagindeling Hallo. Dit is te ingesteld**POST of GET** voor de meeste webtoepassingen.
9. Voer Hallo gebruikersnaamvariabele en wachtwoordvariabele domeinvariabele (als deze wordt weergegeven op de aanmeldingspagina Hallo). toofind Hallo namen van Hallo invoer vakken, gaat de aanmeldingspagina toohello in een webbrowser, met de rechtermuisknop op de pagina Hallo en selecteert **bron weergeven**.
10. Controleer Hallo **gebruikersovereenkomst vereist Azure multi-factor Authentication** vak als alle gebruikers zijn of worden geïmporteerd in hello Server- en onderwerp toomulti-factorverificatie. Als een groot aantal gebruikers nog niet is geïmporteerd in Hallo Server en/of vrijgesteld van multi-factor authentication zijn zal, laat u Hallo vakje uitgeschakeld.
11. Klik op **Geavanceerd** tooreview geavanceerde instellingen, met inbegrip van:

  - Een aangepast bestand voor de weigeringspagina selecteren
  - Cache geslaagde verificaties toohello website voor een bepaalde periode met behulp van cookies
  - Selecteer of tooauthenticate Hallo primaire referenties op basis van een Windows-domein, LDAP-adreslijst. of RADIUS-server.

12. Klik op **OK** tooreturn in het dialoogvenster toohello formulier-gebaseerde Website.
13. Klik op **OK**.
14. Eenmaal Hallo URL en paginavariabelen zijn gedetecteerd of ingevoerd, Hallo websitegegevens weergegeven in Hallo paneel op formulier gebaseerd.

## <a name="using-integrated-windows-authentication-with-azure-multi-factor-authentication-server"></a>Geïntegreerde Windows-verificatie met Azure Multi-Factor Authentication-server gebruiken
toosecure een IIS-webtoepassing die gebruikmaakt van geïntegreerde Windows-HTTP-verificatie, hello Azure MFA-Server op Hallo van IIS-webserver installeren en configureren Hallo Server Hello stappen te volgen:

1. Klik in hello Azure multi-factor Authentication-Server, op Hallo verificatie van IIS-pictogram in het linkermenu Hallo.
2. Klik op Hallo **HTTP** tabblad.
3. Klik op **Add**.
4. In dialoogvenster Hallo basis-URL toevoegen, Voer Hallo-URL voor Hallo-website waar de HTTP-verificatie wordt uitgevoerd (zoals http://localhost/owa) en geef een toepassingsnaam in (optioneel). de naam van de toepassing Hello wordt weergegeven in de Azure multi-factor Authentication-rapporten en kan worden weergegeven in verificatieberichten via SMS of mobiele App.
5. Pas de Hallo inactiviteit en voor maximale sessieduur als Hallo standaard niet voldoende is.
6. Controleer Hallo **overeenkomende multi-factor Authentication-gebruiker vereisen** vak als alle gebruikers zijn of worden geïmporteerd in hello Server- en onderwerp toomulti-factorverificatie. Als een groot aantal gebruikers nog niet is geïmporteerd in Hallo Server en/of vrijgesteld van multi-factor authentication zijn zal, laat u Hallo vakje uitgeschakeld.
7. Controleer de Hallo **cookiecache** vak indien gewenst.
8. Klik op **OK**.

## <a name="enable-iis-plug-ins-for-azure-multi-factor-authentication-server"></a>IIS-invoegtoepassingen inschakelen voor Azure Multi-Factor Authentication-server
Na het configureren van Hallo formulier-gebaseerde of HTTP-verificatie-URL's en -instellingen, selecteert Hallo locaties waar hello Azure multi-factor Authentication IIS-invoegtoepassingen moet worden geladen en ingeschakeld in IIS. Gebruik Hallo procedure te volgen:

1. Als wordt uitgevoerd op IIS 6, klikt u op Hallo **ISAPI** tabblad. Selecteer Hallo-website die Hallo webtoepassing wordt uitgevoerd onder (bijvoorbeeld standaardwebsite) tooenable hello Azure multi-factor Authentication ISAPI-filter invoegtoepassing voor die site.
2. Als uitgevoerd op IIS 7 of hoger, klikt u op Hallo **systeemeigen Module** tabblad. Selecteer Hallo-server, websites of toepassingen tooenable Hallo IIS-invoegtoepassing op Hallo gewenste niveaus.
3. Klik op Hallo **inschakelen IIS-verificatie** vak Hallo boven aan het welkomstscherm. Azure multi-factor Authentication is nu de beveiliging van de IIS-toepassing hello geselecteerd. Zorg ervoor dat gebruikers in Hallo Server zijn geïmporteerd.

## <a name="trusted-ips"></a>Goedgekeurde IP-adressen
Hallo kunnen goedgekeurde IP-adressen gebruikers toobypass Azure multi-factor Authentication voor websiteaanvragen die afkomstig zijn van specifieke IP-adressen of subnetten. U kunt bijvoorbeeld tooexempt gebruikers van Azure multi-factor Authentication bij het aanmelden van Hallo office. Hiervoor geeft u het subnet van kantoor Hallo als een goedgekeurde IP-adressen. tooconfigure vertrouwde IP-adressen, gebruikt u Hallo procedure te volgen:

1. In de sectie IIS-verificatie hello, klikt u op Hallo **goedgekeurde IP-adressen** tabblad.
2. Klik op **Add**.
3. Wanneer Hallo toevoegen goedgekeurde IP-adressen van het dialoogvenster wordt weergegeven, selecteert u Hallo **één IP-adres**, **IP-bereik**, of **Subnet** keuzerondje.
4. Voer Hallo IP-adres, bereik van IP-adressen of subnet op dat u wilt plaatsen. Als een subnet, selecteer Hallo invoert netmasker geschikte en klikt u op **OK**. Hallo goedgekeurde IP-adressen is toegevoegd.
