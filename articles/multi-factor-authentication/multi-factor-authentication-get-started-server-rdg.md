---
title: RDG- en Azure MFA-server gebruiken RADIUS | Microsoft Docs
description: Dit is de pagina Azure Multi-Factor Authentication die u helpt bij het implementeren van RD-gateway (Extern bureaublad) en Azure Multi-Factor Authentication-server met RADIUS.
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: mtillman
ms.assetid: f2354ac4-a3a7-48e5-a86d-84a9e5682b42
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: joflore
ms.reviewer: richagi
ms.custom: it-pro
ms.openlocfilehash: 25ccd54599ce73d2fc24febd98ba1042407b1afc
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/11/2017
---
# <a name="remote-desktop-gateway-and-azure-multi-factor-authentication-server-using-radius"></a>Extern bureaublad-gateway en Azure Multi-Factor Authentication-server met behulp van RADIUS
Extern bureaublad-gateway (RD-gateway) maakt vaak gebruik van de Network Policy Services (NPS) voor het verifiëren van gebruikers. In dit artikel wordt beschreven hoe u RADIUS-aanvragen van de Extern bureaublad-gateway (via de lokale NPS) omleidt naar de Multi-Factor Authentication-server. De combinatie van Azure MFA en RD-gateway zorgt ervoor dat uw gebruikers overal toegang hebben tot hun werkomgevingen terwijl sterke verificatie wordt uitgevoerd. 

Omdat Windows-verificatie voor Terminal Services niet wordt ondersteund voor Server 2012 R2, dient u RD-gateway en RADIUS te gebruiken voor integratie met de MFA-server. 

Installeer de Azure Multi-Factor Authentication-server op een afzonderlijke server. Deze stuurt de RADIUS-aanvraag vervolgens terug naar de NPS op de Extern bureaublad-gatewayserver. Nadat NPS de gebruikersnaam en het wachtwoord heeft gevalideerd, wordt een antwoord naar de Multi-Factor Authentication-server gestuurd. Vervolgens voert de MFA-server de tweede factor van de verificatie uit en retourneert een resultaat naar de gateway.

## <a name="prerequisites"></a>Vereisten

- Een in een domein opgenomen Azure MFA-server. Als u er nog niet een hebt geïnstalleerd, volgt u de stappen in [Aan de slag met de Azure Multi-Factor Authentication-server](multi-factor-authentication-get-started-server.md).
- Een Extern bureaublad-gateway die verifieert met behulp van Network Policy Services.

## <a name="configure-the-remote-desktop-gateway"></a>De Extern bureaublad-gateway configureren
Configureer de RD-gateway om RADIUS-verificatie naar een Azure Multi-Factor Authentication-server te verzenden. 

1. Klik in RD-gatewaybeheer met de rechtermuisknop op de servernaam en selecteer **Eigenschappen**.
2. Ga naar het tabblad **RD CAP-archief** en selecteer **Centrale NPS-server**. 
3. Voeg een of meer Azure Multi-Factor Authentication-servers toe als RADIUS-servers door de naam of het IP-adres van elke server in te voeren. 
4. Maak een gedeeld geheim voor elke server.

## <a name="configure-nps"></a>NPS configureren
De RD-gateway gebruikt NPS om de RADIUS-aanvraag te verzenden naar Azure Multi-Factor Authentication. Als u NPS wilt configureren, wijzigt u eerst de time-outinstellingen om te voorkomen dat er een time-out optreedt op de RD-gateway voordat de verificatie in twee stappen is voltooid. Daarna kunt u NPS bijwerken zodat deze RADIUS-verificaties van uw MFA-server kan ontvangen. Gebruik de volgende procedure om NPS te configureren:

### <a name="modify-the-timeout-policy"></a>Het time-outbeleid wijzigen

1. Open in NPS het menu **RADIUS-clients en -server** in de linkerkolom en selecteer **Externe RADIUS-servergroepen**. 
2. Selecteer de **TS-GATEWAYSERVERGROEP**. 
3. Ga naar het tabblad **Taakverdeling**. 
4. Wijzig het **Aantal seconden zonder reactie voordat een aanvraag als een genegeerde aanvraag wordt beschouwd** en het **Aantal seconden tussen aanvragen wanneer de server is geïdentificeerd als Niet beschikbaar** in 30 tot 60 seconden. (Als op de server nog steeds een time-out optreedt tijdens de verificatie, kunt u teruggaan en het aantal seconden verhogen.)
5. Ga naar het tabblad **Verificatie/Account** en controleer of de opgegeven RADIUS-poorten overeenkomen met de poorten waarnaar de Multi-Factor Authentication-server luistert.

### <a name="prepare-nps-to-receive-authentications-from-the-mfa-server"></a>NPS voorbereiden om verificaties te ontvangen van de MFA-server

1. Klik in de linkerkolom onder RADIUS-clients en -servers met de rechtermuisknop op **RADIUS-clients** en selecteer **Nieuw**.
2. Voeg de Azure Multi-Factor Authentication-server toe als een RADIUS-client. Kies een beschrijvende naam en geef een gedeeld geheim op.
3. Open het menu **Beleid** in de linkerkolom en selecteer **Beleid voor verbindingsaanvragen**. Hier moet een beleid met de naam TS-GATEWAY-AUTORISATIEBELEID worden vermeld dat tijdens de configuratie van RD-gateway is gemaakt. Dit beleid stuurt RADIUS-verzoeken door naar de Multi-Factor Authentication-server.
4. Klik met de rechtermuisknop op **TS-GATEWAY-AUTORISATIEBELEID** en selecteer **Beleid dupliceren**. 
5. Open het nieuwe beleid en ga naar het tabblad **Voorwaarden**.
6. Voeg een voorwaarde toe die de Beschrijvende naam van client koppelt aan de Beschrijvende naam die in stap 2 is ingesteld voor de RADIUS-client voor de Azure Multi-Factor Authentication-server. 
7. Ga naar het tabblad **Instellingen** en selecteer **Verificatie**.
8. De verificatieprovider wijzigen voor het **verifiëren van aanvragen op deze server**. Wanneer NPS een RADIUS-aanvraag ontvangt van de Azure MFA-server, zorgt dit beleid ervoor dat de verificatie lokaal wordt uitgevoerd in plaats van dat er een RADIUS-aanvraag wordt teruggestuurd naar de Azure Multi-Factor Authentication-server, waardoor een oneindige lus zou ontstaan. 
9. Om een lus te voorkomen, zorgt u ervoor dat het nieuwe beleid BOVEN het oorspronkelijke beleid wordt gerangschikt in het deelvenster **Beleid voor verbindingsaanvragen**.

## <a name="configure-azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication configureren

De Azure Multi-Factor Authentication-server is geconfigureerd als een RADIUS-proxy tussen RD-gateway en NPS.  Het moet worden geïnstalleerd op een in het domein opgenomen server die is gescheiden van de RD-gatewayserver. Gebruik de volgende procedure om de Azure Multi-Factor Authentication-server te configureren.

1. Open de Azure Multi-Factor Authentication-server en selecteer het pictogram RADIUS-verificatie. 
2. Schakel het selectievakje **RADIUS-verificatie inschakelen** in.
3. Controleer op het tabblad Clients of de poorten overeenkomen met wat in NPS is geconfigureerd en selecteer **Toevoegen**.
4. Voeg het IP-adres van de RD-gatewayserver, de naam van de toepassing (optioneel) en een gedeeld geheim toe. Het gedeelde geheim moet hetzelfde zijn op de Azure Multi-Factor Authentication-server en de RD-gateway.
3. Ga naar het tabblad **Doel** en selecteer het keuzerondje **RADIUS-server(s)**.
4. Selecteer **Toevoegen** en voer het IP-adres, het gedeeld geheim en de poorten van de NPS-server in. De RADIUS-client en het RADIUS-doel zijn hetzelfde, tenzij u een centrale NPS gebruikt. Het gedeeld geheim moet overeenkomen met het gedeeld geheim dat is ingesteld in de sectie RADIUS-client van de NPS-server.

![RADIUS-verificatie](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="next-steps"></a>Volgende stappen

- Azure MFA en [IIS Web Apps](multi-factor-authentication-get-started-server-iis.md) integreren

- Antwoorden krijgen in de [Veelgestelde vragen Azure Multi-Factor Authentication](multi-factor-authentication-faq.md)
