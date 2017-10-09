---
title: (HTTP/2)-verificatie op basis van aaaToken voor APNS in Azure Notification Hubs | Microsoft Docs
description: Dit onderwerp wordt uitgelegd hoe tooleverage Hallo nieuwe tokenverificatie voor APNS
services: notification-hubs
documentationcenter: .net
author: kpiteira
manager: erikre
editor: 
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 05/17/2017
ms.author: kapiteir
ms.openlocfilehash: 3353d7f16033ce0b68edec9ee9aeb98f47faa1fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="token-based-http2-authentication-for-apns"></a>Verificatie op basis van tokens (HTTP/2) voor APNS
## <a name="overview"></a>Overzicht
Dit artikel wordt uitgelegd hoe toouse Hallo nieuwe APNS HTTP/2-protocol met tokens gebaseerde verificatie.

Hallo belangrijke voordelen van het gebruik van nieuwe Hallo-protocol zijn:
-   Token genereren is relatief probleemloos vrije (vergeleken toocertificates)
-   Er is geen meer vervaldatums – zijn controle over uw verificatietokens en hun intrekken
-   Nettoladingen kunnen nu worden up too4 KB
- Synchrone feedback
-   U bent op de meest recente protocol van Apple-certificaten gebruiken nog steeds Hallo binaire protocol, dat is gemarkeerd voor afschaffing

Met deze nieuwe mechanisme kan worden uitgevoerd in twee stappen in een paar minuten:
1.  Hallo benodigde informatie verkrijgen van Hallo Apple Developer-accountportal
2.  Uw notification hub configureren met de nieuwe informatie Hallo

Notification Hubs is nu alle set toouse Hallo nieuwe verificatiesysteem met APNS. 

Houd er rekening mee dat als u een migratie van met referenties van certificaat voor APNS:
- Hallo token eigenschappen overschrijven uw certificaat in ons systeem
- maar uw toepassing blijft tooreceive meldingen naadloos.

## <a name="obtaining-authentication-information-from-apple"></a>Verificatie-informatie verkrijgen van Apple
tooenable op tokens gebaseerde verificatie, moet u Hallo volgende eigenschappen uit uw Apple Developer-Account:
### <a name="key-identifier"></a>Sleutel-id
Hallo sleutel-id kan worden verkregen via Hallo 'Sleutels' pagina in uw Apple Developer-Account

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a>Toepassings-id & toepassingsnaam
de naam van de toepassing Hello is beschikbaar via Hallo App-id's pagina in Hallo Developer-Account. 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

Hallo-toepassings-id is beschikbaar via de pagina voor de details van Hallo lidmaatschap in Hallo Developer-Account.
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a>Verificatietoken
Hallo-verificatietoken kan worden gedownload nadat u een token voor uw toepassing genereren. Raadpleeg voor informatie over hoe toogenerate dit token, te[van Apple-documentatie voor ontwikkelaars](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a>Uw notification hub toouse op tokens gebaseerde verificatie configureren
### <a name="configure-via-hello-azure-portal"></a>Via hello Azure-portal configureren
tooenable token gebaseerde verificatie in Hallo-portal aanmelden toohello Azure-portal en gaat u tooyour Notification Hub > Notification Services > APNS Configuratiescherm. 

Er is een nieuwe eigenschap – *verificatiemodus*. Token kunt u tooupdate uw hub met alle eigenschappen voor relevante Hallo-token.

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- Hallo-eigenschappen die u hebt opgehaald via het Apple developer-account invoeren 
- Kies uw toepassingsmodus (productie of Sandbox) 
- Klik op Opslaan tooupdate uw APNS-referenties. 

### <a name="configure-via-management-api-rest"></a>Configureren via beheer-API (REST)

U kunt onze [management API's](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate uw notification hub toouse op tokens gebaseerde verificatie.
Afhankelijk van of Hallo-toepassing die u configureert is een Sandbox of productie-app (opgegeven in uw ontwikkelaarsaccount Apple), een van de bijbehorende eindpunten hello te gebruiken:

- Sandboxeindpunt: [3-https://api.development.push.apple.com:443-apparaat](https://api.development.push.apple.com:443/3/device)
- Productie-eindpunt: [3-https://api.push.apple.com:443-apparaat](https://api.push.apple.com:443/3/device)

> [!IMPORTANT]
> Verificatie op basis van tokens vereist een API-versie van: **2017 04 of hoger**.
> 
> 

Hier volgt een voorbeeld van een PUT-aanvraag tooupdate een hub met verificatie op basis van tokens:


        PUT https://{namespace}.servicebus.windows.net/{Notification Hub}?api-version=2017-04
          "Properties": {
            "ApnsCredential": {
              "Properties": {
                "KeyId": "<Your Key Id>",
                "Token": "<Your Authentication Token>",
                "AppName": "<Your Application Name>",
                "AppId": "<Your Application Id>",
                "Endpoint":"<Sandbox/Production Endpoint>"
              }
            }
          }
        

### <a name="configure-via-hello-net-sdk"></a>Configureren via Hallo .NET SDK
U kunt uw hub toouse token gebaseerde authenticatie met onze [nieuwste client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8). 

Hier volgt een voorbeeld van code ter illustratie van Hallo correct te gebruiken:


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a>Omzetten toousing certificaat gebaseerde verificatie
U kunt herstellen op een tijd toousing certificaat gebaseerde verificatie met behulp van een voorgaande methode en geven Hallo certificaat in plaats van token Hallo-eigenschappen. Dat actie Hallo overschrijft eerder opgeslagen referenties.
