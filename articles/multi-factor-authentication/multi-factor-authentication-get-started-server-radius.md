---
title: aaaRADIUS verificatie en Azure MFA-Server | Microsoft Docs
description: Dit is hello Azure multi-factor authentication-pagina die u helpt bij het implementeren van RADIUS-verificatie en Azure multi-factor Authentication-Server.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f4ba0fb2-2be9-477e-9bea-04c7340c8bce
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: dac061b83f2657c67192a7aa9c5de63ffeffaaa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-radius-authentication-with-azure-multi-factor-authentication-server"></a>RADIUS-verificatie integreren met Azure Multi-Factor Authentication-server
Gebruik van Hallo RADIUS-verificatiesectie van tooenable Azure MFA-Server en RADIUS-verificatie configureren. RADIUS is een standaard protocol tooaccept verificatieaanvragen en tooprocess deze aanvragen. Hello Azure multi-factor Authentication-Server fungeert als een RADIUS-server. Invoegen tussen uw RADIUS-client (VPN-apparaat) en het verificatiedoel, wat erop kan Active Directory (AD), een LDAP-adreslijst of een andere RADIUS-server tooadd Azure multi-factor Authentication. Voor Azure multi-factor Authentication (MFA) toofunction, moet u hello Azure MFA-Server configureren zodat deze met zowel Hallo clientservers en verificatiedoel Hallo communiceren kan. Hello Azure MFA-Server accepteert aanvragen van een RADIUS-client, controleert referenties met behulp van het verificatiedoel hello, voegt Azure multi-factor Authentication toe en stuurt een reactie terug toohello RADIUS-client. Hallo-verificatieaanvraag slaagt alleen als zowel de primaire verificatie Hallo als hello Azure multi-factor Authentication slaagt.

> [!NOTE]
> Hallo MFA-Server ondersteunt alleen PAP (wachtwoord authenticatieprotocol) en MSCHAPv2 (Microsoft Challenge Handshake Authentication Protocol) RADIUS-protocollen wanneer die fungeert als een RADIUS-server.  Andere protocollen, zoals EAP (extensible authentication protocol), kunnen worden gebruikt wanneer Hallo MFA-server fungeert als een RADIUS-proxy tooanother RADIUS-server die ondersteuning biedt voor dat protocol.
>
> In deze configuratie werken eenzijdige SMS- en OATH-tokens niet omdat Hallo MFA-Server kan een geslaagd RADIUS Challenge-antwoord met behulp van alternatieve protocollen niet starten.

![RADIUS-verificatie](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="add-a-radius-client"></a>Een RADIUS-client toevoegen
tooconfigure RADIUS-verificatie, installatie hello Azure multi-factor Authentication-Server op een WindowsServer. Als u een Active Directory-omgeving hebt, is het Hallo-server moet lid toohello domein binnen Hallo-netwerk. Hallo te volgen procedure tooconfigure hello Azure multi-factor Authentication-Server gebruiken:

1. Klik in hello Azure multi-factor Authentication-Server, op Hallo RADIUS-verificatie-pictogram in het linkermenu Hallo.
2. Controleer de Hallo **RADIUS-verificatie inschakelen** selectievakje.
3. Op tabblad Clients Hallo wijzigen hello verificatie- en accountingpoorten als hello Azure MFA RADIUS-service toolisten voor RADIUS-aanvragen op niet-standaardpoorten moet.
4. Klik op **Add**.
5. Voer Hallo IP-adres van Hallo toestel of de server die moet worden geverifieerd toohello Azure multi-factor Authentication-Server, een toepassingsnaam in (optioneel) en een gedeeld geheim.

  de naam van de toepassing Hello wordt weergegeven in de Azure multi-factor Authentication-rapporten en kan worden weergegeven in verificatieberichten via SMS of mobiele App.

  Hallo gedeelde geheime behoeften toobe Hallo op beide hello Azure multi-factor Authentication-Server hetzelfde en toestel of de server.

6. Controleer Hallo **overeenkomende multi-factor Authentication-gebruiker vereisen** vak als alle gebruikers zijn of worden geïmporteerd in hello Server- en onderwerp toomulti-factorverificatie. Als een groot aantal gebruikers nog niet is geïmporteerd in Hallo Server en/of vrijgesteld van verificatie in twee stappen zijn zal, laat u Hallo vakje uitgeschakeld.
7. Controleer Hallo **terugval OATH-token inschakelen** vak als u wilt gebruiken toouse OATH-toegangscodes van verificatie van mobiele apps als een alternatieve toohello out-of-band telefonische oproep, SMS, of push-melding.
8. Klik op **OK**.

Herhaal stap 4 tot en met 8 tooadd zo veel extra RADIUS-clients als u nodig hebt.

## <a name="configure-your-radius-client"></a>De RADIUS-client configureren

1. Klik op Hallo **doel** tabblad.
2. Als hello Azure MFA-Server is geïnstalleerd op een server domein in een Active Directory-omgeving, selecteert u de Windows-domein.
3. Selecteer **LDAP-binding** als gebruikers moeten worden geverifieerd aan de hand van een LDAP-adreslijst.

  toouse LDAP-binding, klik op het pictogram Adreslijstintegratie hello en Hallo LDAP-configuratie op tabblad Hallo-instellingen bewerken zodat hello Server verbinding kan maken tooyour directory. Instructies voor het configureren van LDAP vindt u in Hallo [configuratiehandleiding voor LDAP-Proxy](multi-factor-authentication-get-started-server-ldap.md).

4. Selecteer RADIUS-server(s) als gebruikers moeten worden geverifieerd aan de hand van een andere RADIUS-server.
5. Klik op **toevoegen** tooconfigure hello toowhich hello Azure MFA-Server wordt proxy Hallo van server RADIUS-aanvragen.
6. Voer Hallo RADIUS-Server toevoegen in het dialoogvenster Hallo IP-adres van Hallo RADIUS-server en een gedeeld geheim.

  Hallo gedeeld geheim moet toobe Hallo dezelfde op beide hello Azure multi-factor Authentication-Server en RADIUS-server. Hallo-verificatiepoort en accountingpoort wijzigen als andere poorten worden gebruikt door Hallo RADIUS-server.

7. Klik op **OK**.
8. Hello Azure MFA-Server als een RADIUS-client in toevoegen Hallo andere RADIUS-server zodat toegangsaanvragen verzonden tooit van hello Azure MFA-Server kan worden verwerkt. Hallo die hetzelfde geheim dat is geconfigureerd in hello Azure multi-factor Authentication-Server gedeelde gebruiken.

Herhaal deze stappen tooadd meer RADIUS-servers en configureer Hallo volgorde in welke hello Azure MFA-Server ze Hello aanroept **omhoog** en **omlaag** knoppen.

Hiermee hello Azure multi-factor Authentication-Server-configuratie is voltooid. Hallo Server luistert nu op Hallo geconfigureerd poorten voor RADIUS-aanvragen van clients Hallo geconfigureerd.   

## <a name="radius-client-configuration"></a>RADIUS-clientconfiguratie
tooconfigure hello RADIUS-client, gebruikt u Hallo richtlijnen:

* Configureer uw toestel/server tooauthenticate via toohello Azure multi-factor Authentication van RADIUS-Server IP-adres, als Hallo RADIUS-server fungeren zal.
* Gebruik hello die hetzelfde gedeelde geheim dat eerder is geconfigureerd.
* Hallo RADIUS time-out too30 tot 60 seconden zo configureren dat er tijd toovalidate Hallo gebruikersreferenties, verificatie in twee stappen uitvoeren, hun reactie ontvangen en vervolgens te reageren toohello RADIUS-toegangsaanvraag.
