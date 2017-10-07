---
title: aaaUse Azure AD authentication tooaccess API voor Azure Media Services met .NET | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe toouse Azure Active Directory (Azure AD) verificatie tooaccess Azure Media Services (AMS) API met .NET.
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
ms.openlocfilehash: 2f750e460d9e476ad92e96adeac6500cb692cd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a>Azure AD authentication tooaccess API voor Azure Media Services gebruiken met .NET

Beginnen met windowsazure.mediaservices 4.0.0.4, Azure Media Services biedt ondersteuning voor verificatie op basis van Azure Active Directory (Azure AD). Dit onderwerp leest u hoe toouse Azure AD authentication tooaccess API voor Azure Media Services met Microsoft .NET.

## <a name="prerequisites"></a>Vereisten

- Een Azure-account. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie. 
- Een Media Services-account. Zie voor meer informatie [een Azure Media Services-account maken met Azure-portal Hallo](media-services-portal-create-account.md).
- meest recente Hallo [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) pakket.
- Bekend bent met de Hallo onderwerp [toegang tot Azure Media Services-API met AAD verificatie-overzicht](media-services-use-aad-auth-to-access-ams-api.md). 

Wanneer u Azure AD-verificatie met Azure Media Services gebruikt, kunt u verifiëren op twee manieren:

- **Gebruikersverificatie** verifieert van een persoon met Hallo app toointeract met Azure Media Services-resources. interactieve toepassing Hello moet eerst Hallo gebruiker gevraagd om referenties. Een voorbeeld is een management console-app die wordt gebruikt door gemachtigde gebruikers toomonitor codering taken of live streamen. 
- **Verificatie van de service-principal** verifieert u een service. Toepassingen die veel deze verificatiemethode gebruiken zijn apps die worden uitgevoerd daemon-services, middelste laag services of geplande taken, zoals web-apps, apps van de functie, logische apps, API's of microservices.

>[!IMPORTANT]
>Azure Media Service ondersteunt momenteel een model van Azure Access Control Service-verificatie. Access Control-autorisatie gaat echter toobe op 1 juni 2018 is afgeschaft. U wordt aangeraden tooan Azure Active Directory-verificatiemodel zo snel mogelijk te migreren.

## <a name="get-an-azure-ad-access-token"></a>De toegang van een Azure AD-token ophalen

tooconnect toohello API voor Azure Media Services met Azure AD-verificatie, Hallo client-app moet toorequest een Azure AD-toegangstoken. Wanneer u Media Services .NET SDK, veel Hallo meer informatie over hoe tooacquire een toegangstoken van Azure AD zijn ingepakt en vereenvoudigd voor u in Hallo voor clients in Hallo gebruikt [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) en [AzureAdTokenCredentials ](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) klassen. 

Bijvoorbeeld, u hoeft niet tooprovide hello Azure AD-instantie, Media Services resource-URI of systeemeigen Azure AD-App-details. Dit zijn bekende waarden die al zijn geconfigureerd door hello Azure AD-tokenprovider klasse. 

Als u geen van .NET-SDK van Azure Media gebruikmaakt, raden wij aan dat u Hallo [Azure AD-Verificatiebibliotheek](../active-directory/develop/active-directory-authentication-libraries.md). Zie tooget waarden voor Hallo parameters moet u toouse met Azure AD Authentication Library [hello Azure portal tooaccess Azure AD-verificatie-instellingen gebruiken](media-services-portal-get-started-with-aad.md).

U hebt ook de optie Hallo van het vervangen van de standaardimplementatie Hallo Hallo **AzureAdTokenProvider** met uw eigen implementatie.

## <a name="install-and-configure-azure-media-services-net-sdk"></a>Installeren en configureren van Azure Media Services .NET SDK

>[!NOTE] 
>toouse Azure AD authentication Hello Media Services .NET SDK, moet u toohave Hallo nieuwste [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) pakket. Een verwijzing toohello ook toe te voegen **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly. Als u van een bestaande app gebruikmaakt, opnemen Hallo **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly. 

1. Maak een nieuwe C#-consoletoepassing in Visual Studio.
2. Gebruik Hallo [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet-pakket tooinstall **Azure Media Services .NET SDK**. 

    tooadd verwijzingen via NuGet, nemen Hallo stappen te volgen: in **Solution Explorer**, met de rechtermuisknop op de projectnaam Hallo en selecteer vervolgens **beheren NuGet-pakketten**. Zoek vervolgens naar **windowsazure.mediaservices** en selecteer **installeren**.
    
    -of-

    Voer hello volgende opdracht in **Package Manager Console** in Visual Studio.

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. Voeg **met** tooyour broncode.

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a>Verificatie van gebruiker gebruiken

tooconnect toohello, Azure Media Service API met Hallo gebruiker verificatieoptie Hallo client-app moet toorequest een Azure AD-token met behulp van Hallo volgende parameters:  

- Azure AD-tenant-eindpunt. Hallo tenant gegevens kan worden opgehaald uit hello Azure-portal. Beweeg de muisaanwijzer over Hallo aangemelde gebruiker in de rechterbovenhoek Hallo.
- Media Services resource-URI.
- Media Services (systeemeigen) toepassingsclient-id. 
- Media Services (systeemeigen)-toepassing omleidings-URI. 

Hallo-waarden voor deze parameters vindt u in **AzureEnvironments.AzureCloudEnvironment**. Hallo **AzureEnvironments.AzureCloudEnvironment** constante is een helper in Hallo .NET SDK tooget Hallo rechts omgevingsvariabele-instellingen voor een openbare Azure-Datacenter. 

Het bevat vooraf gedefinieerde omgevingsinstellingen voor toegang tot Media Services in Hallo openbare datacenters alleen. Voor cloud-regio, soevereine of overheidsinstelling, kunt u **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, of **AzureGermanCloudEnvironment** respectievelijk.

Hallo volgende codevoorbeeld maakt een token:
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
toostart programmering op basis van Media Services, moet u toocreate een **CloudMediaContext** -exemplaar dat Hallo servercontext vertegenwoordigt. Hallo **CloudMediaContext** verwijzingen tooimportant verzamelingen, met inbegrip van taken, assets, bestanden, toegangsbeleid en locators bevat. 

U moet ook toopass hello **resource-URI voor Media Services-REST** toohello **CloudMediaContext** constructor. tooget hello resource-URI voor REST mediaservices aanmelden toohello Azure-portal, selecteert u uw Azure Media Services-account selecteren **API-toegang**, en selecteer vervolgens **tooAzure Media Services verbinden met gebruiker verificatie**. 

Hallo volgende voorbeeld wordt een **CloudMediaContext** exemplaar:

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

Hallo volgende voorbeeld ziet u hoe toocreate hello Azure AD-token en Hallo context:

    namespace AADAuthSample
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Specify your Azure AD tenant domain, for example "microsoft.onmicrosoft.com".
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR AAD TENANT DOMAIN HERE}", AzureEnvironments.AzureCloudEnvironment);
    
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
            }
    
        }
    }

>[!NOTE]
>Als u krijgt een uitzondering met de tekst ' Hallo externe server heeft een fout geretourneerd: (401) niet geautoriseerd, ' Hallo Zie [toegangsbeheer](media-services-use-aad-auth-to-access-ams-api.md#access-control) sectie van de toegang tot Azure Media Services API met overzicht van Azure AD-authenticatie.

## <a name="use-service-principal-authentication"></a>Service-principal-verificatie gebruiken
    
tooconnect toohello Azure Media Services-API met Hallo service principal optie, uw app middelste laag (web-API of webtoepassing) moet een Azure AD-token toorequests Hello volgende parameters:  

- Azure AD-tenant-eindpunt. Hallo tenant gegevens kan worden opgehaald uit hello Azure-portal. Beweeg de muisaanwijzer over Hallo aangemelde gebruiker in de rechterbovenhoek Hallo.
- Media Services resource-URI.
- Waarden van de toepassing Azure AD: Hallo **Client-ID** en **clientgeheim**.

waarden voor Hallo Hallo **Client-ID** en **clientgeheim** parameters kunnen u vinden in hello Azure-portal. Zie voor meer informatie [aan de slag met Azure AD-verificatie met Azure-portal Hallo](media-services-portal-get-started-with-aad.md).

Hallo volgende codevoorbeeld maakt een token met behulp van Hallo **AzureAdTokenCredentials** constructor die **AzureAdClientSymmetricKey** als een parameter: 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

U kunt ook opgeven Hallo **AzureAdTokenCredentials** constructor die **AzureAdClientCertificate** als parameter. 

Voor instructies over het toocreate en een certificaat configureren in een formulier dat kan worden gebruikt door Azure AD, Zie [tooAzure AD in daemon-apps met certificaten - handmatige configuratiestappen verifiëren](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

toostart programmering op basis van Media Services, moet u toocreate een **CloudMediaContext** -exemplaar dat Hallo servercontext vertegenwoordigt. U moet ook toopass hello **resource-URI voor Media Services-REST** toohello **CloudMediaContext** constructor. U krijgt Hallo **resource-URI voor Media Services-REST** waarde van Hallo ook Azure portal.

Hallo volgende voorbeeld wordt een **CloudMediaContext** exemplaar:

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
Hallo volgende voorbeeld ziet u hoe toocreate hello Azure AD-token en Hallo context:

    namespace AADAuthSample
    {
    
        class Program
        {
            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                            new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                            AzureEnvironments.AzureCloudEnvironment);
            
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".      
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
    
                Console.ReadLine();
            }
    
        }
    }

## <a name="next-steps"></a>Volgende stappen

Aan de slag met [tooyour account uploaden van bestanden](media-services-dotnet-upload-files.md).
