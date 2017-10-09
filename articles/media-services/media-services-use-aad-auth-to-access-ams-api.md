---
title: aaaAccess API voor Azure Media Services met Azure Active Directory-verificatie | Microsoft Docs
description: Meer informatie over concepten en stappen tootake toouse Azure Active Directory (Azure AD) tooauthenticate toegang toohello Azure Media Services-API.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: bb8f75f39100dc37098260c24ab4a199ef689d46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="access-hello-azure-media-services-api-with-azure-ad-authentication"></a>Toegang tot hello Azure Media Services-API met Azure AD-verificatie
 
Hello Azure Media Services-API is een RESTful-API. U kunt deze tooperform bewerkingen op mediabronnen met behulp van een REST-API of met behulp van de beschikbare client-SDK's. Azure Media Services biedt een Media Services-client-SDK voor .NET voor Microsoft. toobe geautoriseerd tooaccess Media Services-resources en Hallo Media Services-API, u moet eerst worden geverifieerd. 

Media Services ondersteunt [Azure Active Directory (Azure AD)-gebaseerde verificatie](../active-directory/active-directory-whatis.md). Hello Azure Media REST-service is vereist dat Hallo gebruiker of toepassing waarmee Hallo REST-API-aanvragen hebben beide Hallo **Inzender** of **eigenaar** rol tooaccess Hallo resources. Zie voor meer informatie [aan de slag met toegangsbeheer op basis van rollen in Azure-portal Hallo](../active-directory/role-based-access-control-what-is.md).  

> [!IMPORTANT]
> Media Services ondersteunt momenteel hello Azure Access Control-servicemodel voor verificatie. Access Control-autorisatie wordt echter op 1 juni 2018 afgeschaft. U wordt aangeraden toohello Azure AD authentication model zo snel mogelijk te migreren.

Dit document bevat een overzicht van hoe tooaccess Media Services-API Hallo met behulp van REST- of .NET API's.

## <a name="access-control"></a>Toegangsbeheer

Voor hello Azure Media REST aanvraag toosucceed hebben Hallo aanroepen gebruiker een rol Inzender of -eigenaar voor Hallo deze tooaccess probeert Media Services-account.  
Alleen een gebruiker met de rol van eigenaar Hallo kunt geven media (account) toegang toonew brongebruikers of apps. de rol Inzender Hallo hebben toegang tot alleen Hallo mediabron.
Ongeautoriseerde aanvragen mislukt met de statuscode 401. Als u deze foutcode ziet, controleert u of uw gebruiker Hallo Inzender of rol van eigenaar is toegewezen voor Media Services-account van de gebruiker Hallo heeft. U kunt dit controleren in hello Azure-portal. Zoeken naar uw media-account en klik vervolgens op Hallo **toegangsbeheer** tabblad. 

![Access control-tabblad](./media/media-services-use-aad-auth-to-access-ams-api/media-services-access-control.png)

## <a name="types-of-authentication"></a>Typen verificatie 
 
Wanneer u Azure AD-verificatie met Azure Media Services gebruikt, hebt u twee opties voor verificatie:

- **Gebruikersverificatie**. Verifiëren van een persoon met Hallo app toointeract met Media Services-resources. interactieve toepassing Hello moet eerst Hallo gebruiker gevraagd om Hallo gebruikersreferenties. Een voorbeeld is van een management console-app gebruikt door gemachtigde gebruikers toomonitor codering taken of live te streamen. 
- **Verificatie van de service-principal**. Een service verifiëren. Toepassingen die gebruikmaken van deze verificatiemethode vaak zijn apps die daemon-services, middelste laag services of geplande taken worden uitgevoerd. Voorbeelden zijn web-apps, apps van de functie logic apps, API en microservices.

### <a name="user-authentication"></a>Gebruikersverificatie 

Toepassingen die gebruikmaken van methode voor gebruikersverificatie Hallo moeten zijn management of systeemeigen apps bewaking: mobiele apps, Windows-apps en toepassingen van de Console. Dit type oplossing is handig als u wilt dat menselijke tussenkomst met Hallo-service in een van de volgende scenario's Hallo:

- Dashboard voor uw codering taken bewaken.
- Het bewakingsdashboard voor uw live-stromen.
- Management-toepassing voor pc's of mobiele gebruikers tooadminister resources in een Media Services-account.

> [!NOTE]
> Deze verificatiemethode moet niet worden gebruikt voor consumententoepassingen. 

Een systeemeigen toepassing moet eerst een toegangstoken van Azure AD te verkrijgen en vervolgens worden gebruikt bij het maken van HTTP-aanvragen toohello Media Services REST-API. Hallo access token toohello aanvraagheader toevoegen. 

Hallo volgende diagram toont een typische interactieve toepassing authenticatiestroom: 

![Diagram van systeemeigen apps](./media/media-services-use-aad-auth-to-access-ams-api/media-services-native-aad-app1.png)

In Hallo voorgaande diagram, vertegenwoordigen Hallo cijfers Hallo stroom van Hallo aanvragen in chronologische volgorde.

> [!NOTE]
> Wanneer u een methode voor gebruikersverificatie Hallo gebruikt, alle apps Hallo delen dezelfde (standaard) systeemeigen toepassing client-ID en systeemeigen toepassing omleidings-URI. 

1. Een gebruiker om referenties gevraagd.
2. Een Azure AD-toegangstoken aanvragen Hello volgende parameters:  

    * Azure AD-tenant-eindpunt.

        Hallo tenant gegevens kan worden opgehaald uit hello Azure-portal. Plaats de cursor op de naam van de Hallo van Hallo aangemelde gebruiker in de rechterbovenhoek Hallo.
    * Media Services resource-URI. 

        Deze URI wordt dezelfde voor Media Services-accounts die zich in Hallo Hallo dezelfde Azure-omgeving (bijvoorbeeld https://rest.media.azure.net).

    * Media Services (systeemeigen) toepassingsclient-id.
    * Media Services (systeemeigen)-toepassing omleidings-URI.
    * Resource-URI voor de REST mediaservices.
        
        Hallo URI vertegenwoordigt Hallo REST API-eindpunt (bijvoorbeeld https://test03.restv2.westus.media.azure.net/api/).

    Zie tooget waarden voor deze parameters [hello Azure portal tooaccess Azure AD-verificatie-instellingen gebruiken](media-services-portal-get-started-with-aad.md) Hallo gebruiker verificatie wordt gebruikt.

3. Hello Azure AD-toegangstoken toohello client verzonden.
4. Hallo-client verzendt een aanvraag toohello REST-API van Azure Media met hello Azure AD-toegangstoken.
5. Hallo client terug Hallo gegevens ontvangt uit Media Services.

Zie voor meer informatie over hoe toouse Azure AD authentication toocommunicate met REST verzoeken met behulp van Media Services .NET SDK voor clients in Hallo [met Azure AD authentication tooaccess Hallo Media Services-API met .NET](media-services-dotnet-get-started-with-aad.md). 

Als u Media Services .NET SDK voor clients in Hallo niet gebruikt, moet u handmatig een tokenaanvraag van Azure AD access maken met behulp van Hallo parameters beschreven in stap 2. Zie voor meer informatie [hoe toouse hello Azure AD Authentication Library tooget hello Azure AD-token](../active-directory/develop/active-directory-authentication-libraries.md).

### <a name="service-principal-authentication"></a>Verificatie van service-principal

Toepassingen die gebruikmaken van deze verificatiemethode vaak zijn apps die services van de middelste laag en geplande taken uitvoeren: web-apps, apps van de functie logic apps, API's en microservices. Deze verificatiemethode is ook geschikt zijn voor interactieve toepassingen die u toouse toomanage de resources van een service wilt mogelijk.

Wanneer u Hallo service principal verificatie methode toobuild consumentenscenario's gebruikt, wordt verificatie gewoonlijk uitgevoerd in de middelste laag hello (via een API) en niet rechtstreeks in een toepassing met mobiele of bureaubladtoepassingen. 

toouse deze methode maakt u een Azure AD-toepassing en service-principal in een eigen tenant. Nadat u de toepassing hello maakt, geeft u Hallo app Inzender of eigenaar rol toegang toohello Media Services-account. U kunt dit doen in hello Azure-portal met behulp van Azure CLI of met een PowerShell-script. U kunt ook een bestaande Azure AD-toepassing gebruiken. U kunt registreren en beheren van uw Azure AD-app en service-principal [in hello Azure-portal](media-services-portal-get-started-with-aad.md). U kunt dit ook doen met behulp van [Azure CLI 2.0](media-services-use-aad-auth-to-access-ams-api.md) of [PowerShell](media-services-powershell-create-and-configure-aad-app.md). 

![Middelste laag apps](./media/media-services-use-aad-auth-to-access-ams-api/media-services-principal-service-aad-app1.png)

Nadat u uw Azure AD-toepassing hebt gemaakt, kunt u waarden ophalen voor Hallo instellingen te volgen. U moet deze waarden voor verificatie:

- Client-ID 
- Clientgeheim 

In Hallo voorgaande afbeelding, geven Hallo cijfers Hallo stroom van Hallo aanvragen in chronologische volgorde:
    
1. Een app middelste laag (web-API of webtoepassing) vraagt een Azure AD-toegangstoken dat heeft Hallo volgende parameters:  

    * Azure AD-tenant-eindpunt.

        Hallo tenant gegevens kan worden opgehaald uit hello Azure-portal. Plaats de cursor op de naam van de Hallo van Hallo aangemelde gebruiker in de rechterbovenhoek Hallo.
    * Media Services resource-URI. 

        Deze URI wordt dezelfde voor Media Services-accounts die zich bevinden in Hallo Hallo dezelfde Azure-omgeving (bijvoorbeeld https://rest.media.azure.net).

    * Resource-URI voor de REST mediaservices.

        Hallo URI vertegenwoordigt Hallo REST API-eindpunt (bijvoorbeeld https://test03.restv2.westus.media.azure.net/api/).

    * Waarden van de toepassing Azure AD: Hallo van client-ID en clientgeheim.
    
    Zie tooget waarden voor deze parameters [hello Azure portal tooaccess Azure AD-verificatie-instellingen gebruiken](media-services-portal-get-started-with-aad.md) met behulp van Hallo service principal verificatieoptie.

2. Hello Azure AD-toegangstoken verzonden toohello middelste laag.
4. de middelste laag Hallo verzendt aanvraag toohello REST-API van Azure Media met hello Azure AD-token.
5. de middelste laag Hallo terug Hallo gegevens ontvangt uit Media Services.

Zie voor meer informatie over hoe toouse Azure AD authentication toocommunicate met REST aanvraagt via Hallo Media Services .NET SDK voor clients, [met Azure AD authentication tooaccess API voor Azure Media Services met .NET](media-services-dotnet-get-started-with-aad.md). 

Als u Media Services .NET SDK voor clients in Hallo niet gebruikt, moet u handmatig een Azure AD-tokenaanvraag maken met behulp van de parameters die worden beschreven in stap 1. Zie voor meer informatie [hoe toouse hello Azure AD Authentication Library tooget hello Azure AD-token](../active-directory/develop/active-directory-authentication-libraries.md).

## <a name="troubleshooting"></a>Problemen oplossen

Uitzondering: ' hello externe server heeft een fout geretourneerd: (401) niet geautoriseerd. "

Oplossing: Voor Hallo Media Services REST aanvraag toosucceed Hallo oproepende gebruiker moet een rol Inzender of eigenaar in Hallo deze tooaccess probeert Media Services-account. Zie voor meer informatie, Hallo [toegangsbeheer](media-services-use-aad-auth-to-access-ams-api.md#access-control) sectie.

## <a name="resources"></a>Resources

Hallo volgende artikelen vindt u overzichten van de concepten van Azure AD-verificatie: 

- [Verificatie scenario's voor toepassingsbeheer door Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md#basics-of-authentication-in-azure-ad)
- [Toevoegen, bijwerken of verwijderen van een toepassing in Azure AD](../active-directory/develop/active-directory-integrating-applications.md)
- [Configureren en beheren van rollen gebaseerd toegangsbeheer met behulp van PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)

## <a name="next-steps"></a>Volgende stappen

* Hello Azure-portal te gebruiken[toegang tot Azure AD authentication tooconsume Azure Media Services-API](media-services-portal-get-started-with-aad.md).
* Azure AD-verificatie te gebruiken[toegang tot API voor Azure Media Services met .NET](media-services-dotnet-get-started-with-aad.md).

