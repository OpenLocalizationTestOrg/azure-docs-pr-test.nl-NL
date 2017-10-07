---
title: Azure AD authentication tooaccess Azure Media Services-API met REST aaaUse | Microsoft Docs
description: Meer informatie over hoe tooaccess API voor Azure Media Services met Azure Active Directory-verificatie met behulp van REST.
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 114f7bdde3a8f5fe6189d712e05b6afdc8a8787a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-hello-azure-media-services-api-with-rest"></a>Gebruik Azure AD authentication tooaccess hello Azure Media Services-API met REST

Hello Azure Media Services-team heeft Azure Active Directory (Azure AD) authenticatie biedt ondersteuning voor Azure Media Services toegang uitgebracht. Deze ook heeft plannen toodeprecate Azure Access Control service-verificatie voor Media Services toegang. Omdat elke Azure-abonnement en elke Media Services-account aangesloten tooan Azure AD-tenant is, biedt ondersteuning voor Azure AD-verificatie veel voordelen voor beveiliging. Zie voor meer informatie over deze wijziging en de migratie (als u Hallo Media Services .NET SDK voor uw app gebruiken), Hallo volgende blog plaatst en artikelen:

- [Azure Media Services introduceert ondersteuning voor Azure AD en afschaffing van toegangsbeheer verificatie](https://azure.microsoft.com/blog/azure%20media%20service%20aad%20auth%20and%20acs%20deprecation)
- [Toegang tot Azure Media Services-API met behulp van Azure AD-verificatie](media-services-use-aad-auth-to-access-ams-api.md)
- [Azure AD authentication tooaccess Azure Media Services-API met behulp van Microsoft .NET te gebruiken](media-services-dotnet-get-started-with-aad.md)
- [Aan de slag met Azure AD-verificatie met behulp van hello Azure-portal](media-services-portal-get-started-with-aad.md)

Sommige klanten moeten toodevelop hun oplossingen Media Services onder Hallo volgende beperkingen:

*   Gebruik van een programmeertaal die geen Microsoft .NET of C# of Hallo runtime-omgeving is niet Windows.
*   Azure AD-bibliotheken, zoals Active Directory Authentication Libraries zijn niet beschikbaar voor Hallo programmeertaal of kunnen niet worden gebruikt voor hun runtimeomgeving.

Sommige klanten hebben toepassingen ontwikkeld met behulp van REST-API voor toegangsbeheer, verificatie en Azure Media Services-toegang. Voor deze klanten, moet u een manier toouse alleen Hallo REST-API voor Azure AD-verificatie en daaropvolgende Azure Media Services toegang tot. U moet toonot vertrouwen op een van de bibliotheken hello Azure AD of op Hallo Media Services .NET SDK. In dit artikel we wordt beschreven een oplossing en voorbeeldcode in dit scenario. Omdat Hallo code alle REST-API-aanroepen, met geen afhankelijkheid van een Azure AD of Azure Media Services-bibliotheek Hallo code kan eenvoudig worden vertaalde tooany andere programmeertaal.

> [!IMPORTANT]
> Media Services ondersteunt momenteel hello Azure Access Control-servicemodel voor verificatie. Access Control-verificatie wordt echter 1 juni 2018 afgeschaft. U wordt aangeraden toohello Azure AD authentication model zo snel mogelijk te migreren.


## <a name="design"></a>Ontwerpen

In dit artikel gebruiken we Hallo na verificatie en autorisatie-ontwerp:

*  Autorisatie protocol: OAuth 2.0. OAuth 2.0 is een Webstandaard die betrekking heeft op zowel de verificatie en autorisatie. Dit wordt ondersteund door Google, Microsoft, Facebook en PayPal-nummer. Het is oktober 2012 bekrachtigd. Microsoft ondersteunt goed OAuth 2.0 en OpenID Connect. Beide van deze standaarden worden ondersteund in meerdere services en clientbibliotheken, waaronder Azure Active Directory, Open Web Interface voor .NET (OWIN)-Katana en Azure AD-bibliotheken.
*  Type verlenen: clientreferenties type verlenen. Clientreferenties is een van de Hallo grant vier typen in OAuth 2.0. Dit wordt vaak gebruikt voor toegang tot Azure AD Microsoft Graph API.
*  Verificatiemodus: Service-principal. Hallo is andere verificatiemodus gebruiker of interactieve verificatie.

Een totaal van vier toepassingen of services, betrokken zijn bij hello Azure AD- en autorisatiestroom voor het gebruik van Media Services. Hallo-toepassingen en -services en Hallo-stroom worden beschreven in de volgende tabel Hallo:

|Toepassingstype |Toepassing |Stroom|
|---|---|---|
|Client | Klant-app of oplossing | Deze app (daadwerkelijk, de proxy) is geregistreerd in Azure AD-tenant Hallo in welke hello Azure-abonnement en Hallo media serviceaccount zich bevinden. Hallo service-principal van Hallo geregistreerd app vervolgens krijgt met de rol van eigenaar of bijdrager in Hallo Access Control (IAM) van Hallo media service-account. Hallo-service-principal wordt vertegenwoordigd door Hallo app-ID en client clientgeheim. |
|ID-Provider (IDP) | Azure AD als IDP | Hallo geregistreerde app service-principal (client-ID en clientgeheim) is geverifieerd door Azure AD als Hallo IDP. Deze verificatie wordt uitgevoerd, intern en impliciet. Net zoals in de clientreferentiestroom, Hallo-client in plaats van Hallo gebruiker geverifieerd. |
|Secure Token Service (STS) / OAuth-server | Azure AD als STS | Na verificatie door Hallo IDP (of de OAuth-Server in termen van OAuth 2.0), een JSON Web Token (JWT) of een toegangstoken is uitgegeven door Azure AD als STS/OAuth-Server voor toegang tot toohello middelste laag resource: in ons geval Hallo Media Services REST API-eindpunt. |
|Resource | Media Services REST-API | Elke Media Services REST API-aanroep is geautoriseerd door een toegangstoken dat is uitgegeven door Azure AD als STS of Hallo OAuth-server. |

Als u de voorbeeldcode Hallo uitvoeren en vastleggen van een JWT of een toegangstoken, heeft Hallo JWT Hallo volgende kenmerken:

    aud: "https://rest.media.azure.net",

    iss: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    iat: 1497146280,

    nbf: 1497146280,
    exp: 1497150180,

    aio: "Y2ZgYDjuy7SptPzO/muf+uRu1B+ZDQA=",

    appid: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6",

    appidacr: "1",

    idp: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    oid: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    sub: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    tid: "72f988bf-86f1-41af-91ab-2d7cd011db47",

Hier volgen Hallo toewijzingen tussen Hallo kenmerken in de Hallo JWT en Hallo vier toepassingen of services in de voorgaande tabel Hallo:

|Toepassingstype |Toepassing |JWT-kenmerk |
|---|---|---|
|Client |Klant-app of oplossing |toepassings-id: '02ed1e8e-af8b-477e-af3d-7e7219a99ac6'. Hallo client-ID van een toepassing wordt u tooAzure AD registreren in de volgende sectie Hallo. |
|ID-Provider (IDP) | Azure AD als IDP |IDP: 'https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/'.  Hallo GUID is Hallo-ID van Microsoft-tenant (microsoft.onmicrosoft.com). Elke tenant heeft zijn eigen, unieke ID. |
|Secure Token Service (STS) / OAuth-server |Azure AD als STS | iss: 'https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/'. Hallo GUID is Hallo-ID van Microsoft-tenant (microsoft.onmicrosoft.com). |
|Resource | Media Services REST-API |AUD: 'https://rest.media.azure.net'. Hallo ontvanger of doelgroep van het toegangstoken Hallo. |

## <a name="steps-for-setup"></a>Stappen voor installatie

tooregister en stelt u een Azure AD-toepassing voor Azure AD-verificatie en tooobtain een toegangstoken voor het aanroepen van Hallo REST-API van Azure Media Services-eindpunt, volledige Hallo stappen te volgen:

1.  In Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), registreren van een Azure AD-toepassing (bijvoorbeeld wzmediaservice) toohello Azure AD-tenant (bijvoorbeeld microsoft.onmicrosoft.com). Het maakt niet uit of u geregistreerd als web-app of systeemeigen app. U kunt ook kiezen eventuele aanmeldings-URL en de antwoord-URL (bijvoorbeeld http://wzmediaservice.com voor beide).
2. In Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), gaat u toohello **configureren** tabblad van uw toepassing. Opmerking Hallo **client-ID**. Klik vervolgens onder **sleutels**, genereren een **clientsleutel** (clientgeheim). 

    > [!NOTE] 
    > Let op Hallo clientgeheim. Deze worden niet meer weergegeven.
    
3.  In Hallo [Azure-portal](http://ms.portal.azure.com), gaat u toohello Media Services-account. Selecteer Hallo **toegangsbeheer** deelvenster (IAM). Een nieuw lid Hallo eigenaar of de rol Inzender Hallo toevoegt. Zoek op de naam van de toepassing hello die u in stap 1 (in dit voorbeeld wzmediaservice) geregistreerd voor Hallo-principal.

## <a name="info-toocollect"></a>Info toocollect

tooprepare REST-codering, verzamelen Hallo gegevenspunten tooinclude in Hallo code te volgen:

*   Azure AD als een STS-eindpunt: https://login.microsoftonline.com/microsoft.onmicrosoft.com/oauth2/token. Van dit eindpunt, wordt een toegangstoken JWT aangevraagd. Bovendien tooserving als een IDP Azure AD fungeert ook als een STS. Azure AD geeft een JWT voor toegang tot bedrijfsbronnen (een toegangstoken). Een JWT-token heeft verschillende claims.
*   Azure Media Services REST-API als resource of doelgroep: https://rest.media.azure.net.
*   Client-ID: Zie stap 2 in [stappen voor het installatieprogramma](#steps-for-setup).
*   Clientgeheim: Zie stap 2 in [stappen voor het installatieprogramma](#steps-for-setup).
*   REST-API eindpunt van uw Media Services-account in de volgende indeling Hallo:

    https://[media_service_account_name].restv2. [data_center].media.azure.net/API 

    Dit is Hallo-eindpunt met welke alle REST API voor Media Services in uw toepassing worden aangeroepen. Bijvoorbeeld: https://willzhanmswjapan.restv2.japanwest.media.azure.net/API.

Vervolgens kunt u deze vijf parameters plaatsen in uw web.config of app.config-bestand toouse in uw code.

## <a name="sample-code"></a>Voorbeeldcode

U vindt de voorbeeldcode Hallo in [Azure AD-verificatie voor Azure Media Services toegang: beide via REST-API](https://github.com/willzhan/WAMSRESTSoln).

Hallo voorbeeldcode bestaat uit twee delen:

*   Een bibliotheek-project voor het DLL-bestand met alle Hallo REST-API-code voor Azure AD-verificatie en autorisatie. Er wordt ook een methode voor het maken van de REST-API-aanroepen toohello Media Services REST API-eindpunt, met Hallo toegangstoken.
*   Een console testclient, die Azure AD authentication initieert en verschillende Media Services REST-API-aanroepen.

Hallo-voorbeeldproject heeft drie functies:

*   Azure AD-verificaties via Hallo clientreferenties verleent met behulp van alleen Hallo REST-API.
*   Azure Media Services-toegang met behulp van alleen Hallo REST-API.
*   REST-API toegang tot Azure Storage met behulp van alleen Hallo (als gebruikte toocreate een Media Services-account met behulp van REST-API).


## <a name="where-is-hello-refresh-token"></a>Waar bevindt zich Hallo vernieuwingstoken?

Sommige lezers kunnen vragen: waar zich het vernieuwingstoken Hallo? Waarom niet hier een vernieuwingstoken gebruiken?

Hallo-doel van een vernieuwingstoken is niet toorefresh een toegangstoken. In plaats daarvan is ontworpen toobypass tussenkomst van de eindgebruiker verificatie of de gebruiker en een geldig toegangstoken nog steeds wanneer een eerdere token is verlopen. Een betere naam voor een vernieuwingstoken mogelijk iets zoals 'opnieuw-sign-in-gebruikerstoken overslaan'.

Als u Hallo OAuth 2.0 autorisatie verlenen stroom (gebruikersnaam en wachtwoord, fungeert namens een gebruiker) gebruikt, wordt er een vernieuwingstoken helpt u bij een vernieuwde toegangstoken ophalen zonder tussenkomst van de gebruiker vraagt. Echter voor Hallo OAuth 2.0 clientreferenties verlenen stroom die in dit artikel worden beschreven, fungeert Hallo client voor eigen rekening. U tussenkomst van de gebruiker helemaal niet nodig en Hallo autorisatie server hoeft niet te (en won't) kunt u een vernieuwingstoken. Als u fouten Hallo opsporen **GetUrlEncodedJWT** methode, merkt u dat antwoord Hallo van token Hallo-eindpunt een toegangstoken, maar er is geen vernieuwingstoken heeft.

## <a name="next-steps"></a>Volgende stappen

Aan de slag met [tooyour account uploaden van bestanden](media-services-dotnet-upload-files.md).
