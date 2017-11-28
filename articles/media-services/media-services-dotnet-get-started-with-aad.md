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
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a><span data-ttu-id="93fca-103">Azure AD authentication tooaccess API voor Azure Media Services gebruiken met .NET</span><span class="sxs-lookup"><span data-stu-id="93fca-103">Use Azure AD authentication tooaccess Azure Media Services API with .NET</span></span>

<span data-ttu-id="93fca-104">Beginnen met windowsazure.mediaservices 4.0.0.4, Azure Media Services biedt ondersteuning voor verificatie op basis van Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="93fca-104">Starting with windowsazure.mediaservices 4.0.0.4, Azure Media Services supports authentication based on Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="93fca-105">Dit onderwerp leest u hoe toouse Azure AD authentication tooaccess API voor Azure Media Services met Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="93fca-105">This topic shows you how toouse Azure AD  authentication tooaccess Azure Media Services API with Microsoft .NET.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93fca-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="93fca-106">Prerequisites</span></span>

- <span data-ttu-id="93fca-107">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="93fca-107">An Azure account.</span></span> <span data-ttu-id="93fca-108">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="93fca-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="93fca-109">Een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="93fca-109">A Media Services account.</span></span> <span data-ttu-id="93fca-110">Zie voor meer informatie [een Azure Media Services-account maken met Azure-portal Hallo](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="93fca-110">For more information, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="93fca-111">meest recente Hallo [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) pakket.</span><span class="sxs-lookup"><span data-stu-id="93fca-111">hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span>
- <span data-ttu-id="93fca-112">Bekend bent met de Hallo onderwerp [toegang tot Azure Media Services-API met AAD verificatie-overzicht](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="93fca-112">Familiarity with hello topic [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="93fca-113">Wanneer u Azure AD-verificatie met Azure Media Services gebruikt, kunt u verifiëren op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="93fca-113">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="93fca-114">**Gebruikersverificatie** verifieert van een persoon met Hallo app toointeract met Azure Media Services-resources.</span><span class="sxs-lookup"><span data-stu-id="93fca-114">**User authentication** authenticates a person who is using hello app toointeract with Azure Media Services resources.</span></span> <span data-ttu-id="93fca-115">interactieve toepassing Hello moet eerst Hallo gebruiker gevraagd om referenties.</span><span class="sxs-lookup"><span data-stu-id="93fca-115">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="93fca-116">Een voorbeeld is een management console-app die wordt gebruikt door gemachtigde gebruikers toomonitor codering taken of live streamen.</span><span class="sxs-lookup"><span data-stu-id="93fca-116">An example is a management console app that's used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="93fca-117">**Verificatie van de service-principal** verifieert u een service.</span><span class="sxs-lookup"><span data-stu-id="93fca-117">**Service principal authentication** authenticates a service.</span></span> <span data-ttu-id="93fca-118">Toepassingen die veel deze verificatiemethode gebruiken zijn apps die worden uitgevoerd daemon-services, middelste laag services of geplande taken, zoals web-apps, apps van de functie, logische apps, API's of microservices.</span><span class="sxs-lookup"><span data-stu-id="93fca-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span></span>

>[!IMPORTANT]
><span data-ttu-id="93fca-119">Azure Media Service ondersteunt momenteel een model van Azure Access Control Service-verificatie.</span><span class="sxs-lookup"><span data-stu-id="93fca-119">Azure Media Service currently supports an Azure Access Control Service  authentication model.</span></span> <span data-ttu-id="93fca-120">Access Control-autorisatie gaat echter toobe op 1 juni 2018 is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="93fca-120">However, Access Control authorization is going toobe deprecated on June 1, 2018.</span></span> <span data-ttu-id="93fca-121">U wordt aangeraden tooan Azure Active Directory-verificatiemodel zo snel mogelijk te migreren.</span><span class="sxs-lookup"><span data-stu-id="93fca-121">We recommend that you migrate tooan Azure Active Directory authentication model as soon as possible.</span></span>

## <a name="get-an-azure-ad-access-token"></a><span data-ttu-id="93fca-122">De toegang van een Azure AD-token ophalen</span><span class="sxs-lookup"><span data-stu-id="93fca-122">Get an Azure AD access token</span></span>

<span data-ttu-id="93fca-123">tooconnect toohello API voor Azure Media Services met Azure AD-verificatie, Hallo client-app moet toorequest een Azure AD-toegangstoken.</span><span class="sxs-lookup"><span data-stu-id="93fca-123">tooconnect toohello Azure Media Services API with Azure AD authentication, hello client app needs toorequest an Azure AD access token.</span></span> <span data-ttu-id="93fca-124">Wanneer u Media Services .NET SDK, veel Hallo meer informatie over hoe tooacquire een toegangstoken van Azure AD zijn ingepakt en vereenvoudigd voor u in Hallo voor clients in Hallo gebruikt [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) en [AzureAdTokenCredentials ](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) klassen.</span><span class="sxs-lookup"><span data-stu-id="93fca-124">When you use hello Media Services .NET client SDK, many of hello details about how tooacquire an Azure AD access token are wrapped and simplified for you in hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) and [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span></span> 

<span data-ttu-id="93fca-125">Bijvoorbeeld, u hoeft niet tooprovide hello Azure AD-instantie, Media Services resource-URI of systeemeigen Azure AD-App-details.</span><span class="sxs-lookup"><span data-stu-id="93fca-125">For example, you don't need tooprovide hello Azure AD authority, Media Services resource URI, or native Azure AD application details.</span></span> <span data-ttu-id="93fca-126">Dit zijn bekende waarden die al zijn geconfigureerd door hello Azure AD-tokenprovider klasse.</span><span class="sxs-lookup"><span data-stu-id="93fca-126">These are well-known values that are already configured by hello Azure AD access token provider class.</span></span> 

<span data-ttu-id="93fca-127">Als u geen van .NET-SDK van Azure Media gebruikmaakt, raden wij aan dat u Hallo [Azure AD-Verificatiebibliotheek](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="93fca-127">If you are not using Azure Media Service .NET SDK, we recommend that you use hello [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="93fca-128">Zie tooget waarden voor Hallo parameters moet u toouse met Azure AD Authentication Library [hello Azure portal tooaccess Azure AD-verificatie-instellingen gebruiken](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="93fca-128">tooget values for hello parameters that you need toouse with Azure AD Authentication Library, see [Use hello Azure portal tooaccess Azure AD authentication settings](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="93fca-129">U hebt ook de optie Hallo van het vervangen van de standaardimplementatie Hallo Hallo **AzureAdTokenProvider** met uw eigen implementatie.</span><span class="sxs-lookup"><span data-stu-id="93fca-129">You also have hello option of replacing hello default implementation of hello **AzureAdTokenProvider** with your own implementation.</span></span>

## <a name="install-and-configure-azure-media-services-net-sdk"></a><span data-ttu-id="93fca-130">Installeren en configureren van Azure Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="93fca-130">Install and configure Azure Media Services .NET SDK</span></span>

>[!NOTE] 
><span data-ttu-id="93fca-131">toouse Azure AD authentication Hello Media Services .NET SDK, moet u toohave Hallo nieuwste [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) pakket.</span><span class="sxs-lookup"><span data-stu-id="93fca-131">toouse Azure AD authentication with hello Media Services .NET SDK, you need toohave hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span> <span data-ttu-id="93fca-132">Een verwijzing toohello ook toe te voegen **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span><span class="sxs-lookup"><span data-stu-id="93fca-132">Also, add a reference toohello **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span></span> <span data-ttu-id="93fca-133">Als u van een bestaande app gebruikmaakt, opnemen Hallo **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span><span class="sxs-lookup"><span data-stu-id="93fca-133">If you are using an existing app, include hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span></span> 

1. <span data-ttu-id="93fca-134">Maak een nieuwe C#-consoletoepassing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="93fca-134">Create a new C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="93fca-135">Gebruik Hallo [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet-pakket tooinstall **Azure Media Services .NET SDK**.</span><span class="sxs-lookup"><span data-stu-id="93fca-135">Use hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet package tooinstall **Azure Media Services .NET SDK**.</span></span> 

    <span data-ttu-id="93fca-136">tooadd verwijzingen via NuGet, nemen Hallo stappen te volgen: in **Solution Explorer**, met de rechtermuisknop op de projectnaam Hallo en selecteer vervolgens **beheren NuGet-pakketten**.</span><span class="sxs-lookup"><span data-stu-id="93fca-136">tooadd references by using NuGet, take hello following steps: in **Solution Explorer**, right-click hello project name, and then select **Manage NuGet packages**.</span></span> <span data-ttu-id="93fca-137">Zoek vervolgens naar **windowsazure.mediaservices** en selecteer **installeren**.</span><span class="sxs-lookup"><span data-stu-id="93fca-137">Then, search for **windowsazure.mediaservices** and select **Install**.</span></span>
    
    <span data-ttu-id="93fca-138">-of-</span><span class="sxs-lookup"><span data-stu-id="93fca-138">-or-</span></span>

    <span data-ttu-id="93fca-139">Voer hello volgende opdracht in **Package Manager Console** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="93fca-139">Run hello following command in **Package Manager Console** in Visual Studio.</span></span>

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. <span data-ttu-id="93fca-140">Voeg **met** tooyour broncode.</span><span class="sxs-lookup"><span data-stu-id="93fca-140">Add **using** tooyour source code.</span></span>

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a><span data-ttu-id="93fca-141">Verificatie van gebruiker gebruiken</span><span class="sxs-lookup"><span data-stu-id="93fca-141">Use user authentication</span></span>

<span data-ttu-id="93fca-142">tooconnect toohello, Azure Media Service API met Hallo gebruiker verificatieoptie Hallo client-app moet toorequest een Azure AD-token met behulp van Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="93fca-142">tooconnect toohello Azure Media Service API with hello user authentication option, hello client app needs toorequest an Azure AD token by using hello following parameters:</span></span>  

- <span data-ttu-id="93fca-143">Azure AD-tenant-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="93fca-143">Azure AD tenant endpoint.</span></span> <span data-ttu-id="93fca-144">Hallo tenant gegevens kan worden opgehaald uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="93fca-144">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="93fca-145">Beweeg de muisaanwijzer over Hallo aangemelde gebruiker in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="93fca-145">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="93fca-146">Media Services resource-URI.</span><span class="sxs-lookup"><span data-stu-id="93fca-146">Media Services resource URI.</span></span>
- <span data-ttu-id="93fca-147">Media Services (systeemeigen) toepassingsclient-id.</span><span class="sxs-lookup"><span data-stu-id="93fca-147">Media Services (native) application client ID.</span></span> 
- <span data-ttu-id="93fca-148">Media Services (systeemeigen)-toepassing omleidings-URI.</span><span class="sxs-lookup"><span data-stu-id="93fca-148">Media Services (native) application redirect URI.</span></span> 

<span data-ttu-id="93fca-149">Hallo-waarden voor deze parameters vindt u in **AzureEnvironments.AzureCloudEnvironment**.</span><span class="sxs-lookup"><span data-stu-id="93fca-149">hello values for these parameters can be found in **AzureEnvironments.AzureCloudEnvironment**.</span></span> <span data-ttu-id="93fca-150">Hallo **AzureEnvironments.AzureCloudEnvironment** constante is een helper in Hallo .NET SDK tooget Hallo rechts omgevingsvariabele-instellingen voor een openbare Azure-Datacenter.</span><span class="sxs-lookup"><span data-stu-id="93fca-150">hello **AzureEnvironments.AzureCloudEnvironment** constant is a helper in hello .NET SDK tooget hello right environment variable settings for a public Azure Data Center.</span></span> 

<span data-ttu-id="93fca-151">Het bevat vooraf gedefinieerde omgevingsinstellingen voor toegang tot Media Services in Hallo openbare datacenters alleen.</span><span class="sxs-lookup"><span data-stu-id="93fca-151">It contains pre-defined environment settings for accessing Media Services in hello public data centers only.</span></span> <span data-ttu-id="93fca-152">Voor cloud-regio, soevereine of overheidsinstelling, kunt u **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, of **AzureGermanCloudEnvironment** respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="93fca-152">For sovereign or government cloud regions, you can use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, or **AzureGermanCloudEnvironment** respectively.</span></span>

<span data-ttu-id="93fca-153">Hallo volgende codevoorbeeld maakt een token:</span><span class="sxs-lookup"><span data-stu-id="93fca-153">hello following code example creates a token:</span></span>
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
<span data-ttu-id="93fca-154">toostart programmering op basis van Media Services, moet u toocreate een **CloudMediaContext** -exemplaar dat Hallo servercontext vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="93fca-154">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="93fca-155">Hallo **CloudMediaContext** verwijzingen tooimportant verzamelingen, met inbegrip van taken, assets, bestanden, toegangsbeleid en locators bevat.</span><span class="sxs-lookup"><span data-stu-id="93fca-155">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span> 

<span data-ttu-id="93fca-156">U moet ook toopass hello **resource-URI voor Media Services-REST** toohello **CloudMediaContext** constructor.</span><span class="sxs-lookup"><span data-stu-id="93fca-156">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="93fca-157">tooget hello resource-URI voor REST mediaservices aanmelden toohello Azure-portal, selecteert u uw Azure Media Services-account selecteren **API-toegang**, en selecteer vervolgens **tooAzure Media Services verbinden met gebruiker verificatie**.</span><span class="sxs-lookup"><span data-stu-id="93fca-157">tooget hello resource URI for Media REST Services, sign in toohello Azure portal, select your Azure Media Services account, select **API access**, and then select **Connect tooAzure Media Services with user authentication**.</span></span> 

<span data-ttu-id="93fca-158">Hallo volgende voorbeeld wordt een **CloudMediaContext** exemplaar:</span><span class="sxs-lookup"><span data-stu-id="93fca-158">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

<span data-ttu-id="93fca-159">Hallo volgende voorbeeld ziet u hoe toocreate hello Azure AD-token en Hallo context:</span><span class="sxs-lookup"><span data-stu-id="93fca-159">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

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
><span data-ttu-id="93fca-160">Als u krijgt een uitzondering met de tekst ' Hallo externe server heeft een fout geretourneerd: (401) niet geautoriseerd, ' Hallo Zie [toegangsbeheer](media-services-use-aad-auth-to-access-ams-api.md#access-control) sectie van de toegang tot Azure Media Services API met overzicht van Azure AD-authenticatie.</span><span class="sxs-lookup"><span data-stu-id="93fca-160">If you get an exception that says "hello remote server returned an error: (401) Unauthorized," see hello [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section of Accessing Azure Media Services API with Azure AD authentication overview.</span></span>

## <a name="use-service-principal-authentication"></a><span data-ttu-id="93fca-161">Service-principal-verificatie gebruiken</span><span class="sxs-lookup"><span data-stu-id="93fca-161">Use service principal authentication</span></span>
    
<span data-ttu-id="93fca-162">tooconnect toohello Azure Media Services-API met Hallo service principal optie, uw app middelste laag (web-API of webtoepassing) moet een Azure AD-token toorequests Hello volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="93fca-162">tooconnect toohello Azure Media Services API with hello service principal option, your middle-tier app (web API or web application) needs toorequests an Azure AD token with hello following parameters:</span></span>  

- <span data-ttu-id="93fca-163">Azure AD-tenant-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="93fca-163">Azure AD tenant endpoint.</span></span> <span data-ttu-id="93fca-164">Hallo tenant gegevens kan worden opgehaald uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="93fca-164">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="93fca-165">Beweeg de muisaanwijzer over Hallo aangemelde gebruiker in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="93fca-165">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="93fca-166">Media Services resource-URI.</span><span class="sxs-lookup"><span data-stu-id="93fca-166">Media Services resource URI.</span></span>
- <span data-ttu-id="93fca-167">Waarden van de toepassing Azure AD: Hallo **Client-ID** en **clientgeheim**.</span><span class="sxs-lookup"><span data-stu-id="93fca-167">Azure AD application values: hello **Client ID** and **Client secret**.</span></span>

<span data-ttu-id="93fca-168">waarden voor Hallo Hallo **Client-ID** en **clientgeheim** parameters kunnen u vinden in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="93fca-168">hello values for hello **Client ID** and **Client secret** parameters can be found in hello Azure portal.</span></span> <span data-ttu-id="93fca-169">Zie voor meer informatie [aan de slag met Azure AD-verificatie met Azure-portal Hallo](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="93fca-169">For more information, see [Getting started with Azure AD authentication using hello Azure portal](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="93fca-170">Hallo volgende codevoorbeeld maakt een token met behulp van Hallo **AzureAdTokenCredentials** constructor die **AzureAdClientSymmetricKey** als een parameter:</span><span class="sxs-lookup"><span data-stu-id="93fca-170">hello following code example creates a token by using hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientSymmetricKey** as a parameter:</span></span> 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

<span data-ttu-id="93fca-171">U kunt ook opgeven Hallo **AzureAdTokenCredentials** constructor die **AzureAdClientCertificate** als parameter.</span><span class="sxs-lookup"><span data-stu-id="93fca-171">You can also specify hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientCertificate** as a parameter.</span></span> 

<span data-ttu-id="93fca-172">Voor instructies over het toocreate en een certificaat configureren in een formulier dat kan worden gebruikt door Azure AD, Zie [tooAzure AD in daemon-apps met certificaten - handmatige configuratiestappen verifiëren](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span><span class="sxs-lookup"><span data-stu-id="93fca-172">For instructions about how toocreate and configure a certificate in a form that can be used by Azure AD, see [Authenticating tooAzure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span></span>

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

<span data-ttu-id="93fca-173">toostart programmering op basis van Media Services, moet u toocreate een **CloudMediaContext** -exemplaar dat Hallo servercontext vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="93fca-173">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="93fca-174">U moet ook toopass hello **resource-URI voor Media Services-REST** toohello **CloudMediaContext** constructor.</span><span class="sxs-lookup"><span data-stu-id="93fca-174">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="93fca-175">U krijgt Hallo **resource-URI voor Media Services-REST** waarde van Hallo ook Azure portal.</span><span class="sxs-lookup"><span data-stu-id="93fca-175">You can get hello **resource URI for Media REST Services** value from hello Azure portal as well.</span></span>

<span data-ttu-id="93fca-176">Hallo volgende voorbeeld wordt een **CloudMediaContext** exemplaar:</span><span class="sxs-lookup"><span data-stu-id="93fca-176">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
<span data-ttu-id="93fca-177">Hallo volgende voorbeeld ziet u hoe toocreate hello Azure AD-token en Hallo context:</span><span class="sxs-lookup"><span data-stu-id="93fca-177">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="93fca-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="93fca-178">Next steps</span></span>

<span data-ttu-id="93fca-179">Aan de slag met [tooyour account uploaden van bestanden](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="93fca-179">Get started with [uploading files tooyour account](media-services-dotnet-upload-files.md).</span></span>
