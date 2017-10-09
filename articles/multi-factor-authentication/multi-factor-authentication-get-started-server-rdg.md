---
title: aaaRDG en Azure MFA-Server met behulp van RADIUS | Microsoft Docs
description: Dit is hello Azure multi-factor authentication-pagina die u helpt bij de implementatie van extern bureaublad (RD)-Gateway en Azure multi-factor Authentication-Server met behulp van RADIUS.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f2354ac4-a3a7-48e5-a86d-84a9e5682b42
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: fd280e9b6ff90c82927cffe593c4f1fda7047842
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="remote-desktop-gateway-and-azure-multi-factor-authentication-server-using-radius"></a>Extern bureaublad-gateway en Azure Multi-Factor Authentication-server met behulp van RADIUS
Extern bureaublad (RD) Gateway gebruikt vaak Hallo lokale Services NPS (Network Policy) tooauthenticate gebruikers. Dit artikel wordt beschreven hoe tooroute RADIUS-aanvragen uit van Hallo extern bureaublad-Gateway (via lokale NPS Hallo) toohello multi-factor Authentication-Server. Hallo combinatie van Azure MFA en extern bureaublad-gatewayserver betekent dat uw gebruikers toegang krijgen hun werkomgevingen vanaf elke locatie tot tijdens het uitvoeren van sterke verificatie. 

Omdat Windows-verificatie voor terminal services wordt niet ondersteund voor Server 2012 R2, gebruikt u RD-Gateway en de RADIUS-toointegrate met MFA-Server. 

Hello Azure multi-factor Authentication-Server installeren op een afzonderlijke server, welke proxy's Hallo RADIUS-aanvragen back-toohello NPS op Hallo van extern bureaublad-gatewayserver. Nadat u NPS valideert Hallo gebruikersnaam en wachtwoord, wordt een antwoord toohello multi-factor Authentication-Server. Vervolgens Hallo MFA-Server voert Hallo tweede factor van de verificatie en retourneert een resultaat toohello gateway.

## <a name="prerequisites"></a>Vereisten

- Een in een domein opgenomen Azure MFA-server. Als u niet geïnstalleerd hebt, stappen Hallo in [aan de slag met Azure multi-factor Authentication-Server Hallo](multi-factor-authentication-get-started-server.md).
- Een Extern bureaublad-gateway die verifieert met behulp van Network Policy Services.

## <a name="configure-hello-remote-desktop-gateway"></a>Hallo extern bureaublad-Gateway configureren
Hallo RD-Gateway toosend RADIUS-verificatie tooan Azure multi-factor Authentication-Server configureren. 

1. In RD-gatewaybeheer met de rechtermuisknop op het Hallo-servernaam en selecteer **eigenschappen**.
2. Ga toohello **RD CAP-archief** tabblad en selecteer **centrale server met NPS**. 
3. Een of meer Azure multi-factor Authentication-Servers als RADIUS-servers toevoegen door te voeren Hallo naam of IP-adres van elke server. 
4. Maak een gedeeld geheim voor elke server.

## <a name="configure-nps"></a>NPS configureren
Hallo RD-Gateway gebruikt NPS toosend Hallo RADIUS-aanvraag tooAzure multi-factor Authentication. tooconfigure NPS, u wijzigt u eerst Hallo time-outinstellingen tooprevent Hallo RD-Gateway van een time-out optreedt voordat de verificatie in twee stappen Hallo is voltooid. U kunt vervolgens NPS tooreceive RADIUS-verificaties bijwerken van uw MFA-Server. Hallo te volgen procedure tooconfigure NPS gebruiken:

### <a name="modify-hello-timeout-policy"></a>Hallo time-out beleid wijzigen

1. Open in NPS Hallo **RADIUS-Clients en Server** menu in en selecteert u links Hallo **externe RADIUS-servergroepen**. 
2. Selecteer Hallo **groep TS-GATEWAYSERVER**. 
3. Ga toohello **Load Balancing** tabblad. 
4. Wijzigen van beide Hallo **verwijderd van het aantal seconden zonder reactie voordat de aanvraag wordt beschouwd als** en Hallo **aantal seconden tussen aanvragen wanneer de server wordt geïdentificeerd als niet beschikbaar** toobetween 30 en 60 seconden. (Als u die server Hallo nog steeds een time-out optreedt tijdens de verificatie vindt, u kunt kun je hier en verhoog het aantal seconden Hallo.)
5. Ga toohello **verificatie/Account** tabblad en controleer of Hallo RADIUS-poorten overeenkomen Hallo-poorten die multi-Factor Authentication-Server luistert op Hallo opgegeven.

### <a name="prepare-nps-tooreceive-authentications-from-hello-mfa-server"></a>NPS tooreceive verificaties van Hallo MFA-Server voorbereiden

1. Met de rechtermuisknop op **RADIUS-Clients** onder RADIUS-Clients en Servers in en selecteert u links Hallo **nieuw**.
2. Hello Azure multi-factor Authentication-Server als een RADIUS-client toevoegen. Kies een beschrijvende naam en geef een gedeeld geheim op.
3. Open Hallo **beleid** menu in en selecteert u links Hallo **beleid voor verbindingsaanvragen**. Hier moet een beleid met de naam TS-GATEWAY-AUTORISATIEBELEID worden vermeld dat tijdens de configuratie van RD-gateway is gemaakt. Dit beleid stuurt RADIUS-aanvragen toohello multi-factor Authentication-Server.
4. Klik met de rechtermuisknop op **TS-GATEWAY-AUTORISATIEBELEID** en selecteer **Beleid dupliceren**. 
5. Open de nieuwe beleid en Ga naar toohello Hallo **voorwaarden** tabblad.
6. Een voorwaarde die overeenkomt met de Hallo beschrijvende naam van de Client met de beschrijvende naam Hallo instellen in stap 2 voor hello Azure multi-factor Authentication-Server RADIUS-client toevoegen. 
7. Ga toohello **instellingen** tabblad en selecteer **verificatie**.
8. Hallo verificatieprovider ook wijzigen**aanvragen op deze server verifiëren**. Dit beleid zorgt ervoor dat als een RADIUS-aanvraag NPS van hello Azure MFA-Server ontvangt, Hallo verificatie vindt plaats lokaal verzenden in plaats van een RADIUS-aanvraag back toohello Azure multi-factor Authentication-Server dit tot een voorwaarde voor de lus leiden zou. 
9. tooprevent een voorwaarde voor de lus, zorg ervoor dat Hallo nieuwe beleid boven het oorspronkelijke beleid in Hallo Hallo is geordend **beleid voor verbindingsaanvragen** deelvenster.

## <a name="configure-azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication configureren

Hello Azure multi-factor Authentication-Server is geconfigureerd als een RADIUS-proxy tussen RD-Gateway en NPS.  Het moet worden geïnstalleerd op een domein-server die is gescheiden van Hallo extern bureaublad-gatewayserver. Hallo te volgen procedure tooconfigure hello Azure multi-factor Authentication-Server gebruiken.

1. Open hello Azure multi-factor Authentication-Server en selecteert u het pictogram van Hallo RADIUS-verificatie. 
2. Controleer de Hallo **RADIUS-verificatie inschakelen** selectievakje.
3. Op tabblad Clients Hallo Controleer Hallo poorten overeenkomen met wat in NPS is geconfigureerd en selecteer vervolgens **toevoegen**.
4. Hallo RD-Gateway-server IP-adres, de naam van de toepassing is (optioneel) en een gedeeld geheim toevoegen. Hallo gedeeld geheim moet toobe Hallo dezelfde op Hallo Azure multi-factor Authentication-Server en extern bureaublad-Gateway.
3. Ga toohello **doel** tabblad en selecteer Hallo **RADIUS-servers** keuzerondje.
4. Selecteer **toevoegen** en Voer Hallo IP-adres, het gedeelde geheim en poorten van Hallo NPS-server. Tenzij u een centrale NPS gebruikt, zijn hello RADIUS-client- en RADIUS-doel in kwestie dezelfde Hallo. Hallo gedeeld geheim moet overeenkomen met de Hallo één instelling in Hallo sectie van de RADIUS-client van Hallo NPS-server.

![RADIUS-verificatie](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="next-steps"></a>Volgende stappen

- Azure MFA en [IIS Web Apps](multi-factor-authentication-get-started-server-iis.md) integreren

- Vind antwoorden in Hallo [Veelgestelde vragen over Azure multi-factor Authentication](multi-factor-authentication-faq.md)
