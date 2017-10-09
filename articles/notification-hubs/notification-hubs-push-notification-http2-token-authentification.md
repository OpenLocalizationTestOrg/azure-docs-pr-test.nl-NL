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
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="db594-103">Verificatie op basis van tokens (HTTP/2) voor APNS</span><span class="sxs-lookup"><span data-stu-id="db594-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="db594-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="db594-104">Overview</span></span>
<span data-ttu-id="db594-105">Dit artikel wordt uitgelegd hoe toouse Hallo nieuwe APNS HTTP/2-protocol met tokens gebaseerde verificatie.</span><span class="sxs-lookup"><span data-stu-id="db594-105">This article details how toouse hello new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="db594-106">Hallo belangrijke voordelen van het gebruik van nieuwe Hallo-protocol zijn:</span><span class="sxs-lookup"><span data-stu-id="db594-106">hello key benefits of using hello new protocol include:</span></span>
-   <span data-ttu-id="db594-107">Token genereren is relatief probleemloos vrije (vergeleken toocertificates)</span><span class="sxs-lookup"><span data-stu-id="db594-107">Token generation is relatively hassle free (compared toocertificates)</span></span>
-   <span data-ttu-id="db594-108">Er is geen meer vervaldatums – zijn controle over uw verificatietokens en hun intrekken</span><span class="sxs-lookup"><span data-stu-id="db594-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="db594-109">Nettoladingen kunnen nu worden up too4 KB</span><span class="sxs-lookup"><span data-stu-id="db594-109">Payloads can now be up too4 KB</span></span>
- <span data-ttu-id="db594-110">Synchrone feedback</span><span class="sxs-lookup"><span data-stu-id="db594-110">Synchronous feedback</span></span>
-   <span data-ttu-id="db594-111">U bent op de meest recente protocol van Apple-certificaten gebruiken nog steeds Hallo binaire protocol, dat is gemarkeerd voor afschaffing</span><span class="sxs-lookup"><span data-stu-id="db594-111">You’re on Apple’s latest protocol – certificates still use hello binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="db594-112">Met deze nieuwe mechanisme kan worden uitgevoerd in twee stappen in een paar minuten:</span><span class="sxs-lookup"><span data-stu-id="db594-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="db594-113">Hallo benodigde informatie verkrijgen van Hallo Apple Developer-accountportal</span><span class="sxs-lookup"><span data-stu-id="db594-113">Obtain hello necessary information from hello Apple Developer Account portal</span></span>
2.  <span data-ttu-id="db594-114">Uw notification hub configureren met de nieuwe informatie Hallo</span><span class="sxs-lookup"><span data-stu-id="db594-114">Configure your notification hub with hello new information</span></span>

<span data-ttu-id="db594-115">Notification Hubs is nu alle set toouse Hallo nieuwe verificatiesysteem met APNS.</span><span class="sxs-lookup"><span data-stu-id="db594-115">Notification Hubs is now all set toouse hello new authentication system with APNS.</span></span> 

<span data-ttu-id="db594-116">Houd er rekening mee dat als u een migratie van met referenties van certificaat voor APNS:</span><span class="sxs-lookup"><span data-stu-id="db594-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="db594-117">Hallo token eigenschappen overschrijven uw certificaat in ons systeem</span><span class="sxs-lookup"><span data-stu-id="db594-117">hello token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="db594-118">maar uw toepassing blijft tooreceive meldingen naadloos.</span><span class="sxs-lookup"><span data-stu-id="db594-118">but your application continues tooreceive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="db594-119">Verificatie-informatie verkrijgen van Apple</span><span class="sxs-lookup"><span data-stu-id="db594-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="db594-120">tooenable op tokens gebaseerde verificatie, moet u Hallo volgende eigenschappen uit uw Apple Developer-Account:</span><span class="sxs-lookup"><span data-stu-id="db594-120">tooenable token-based authentication, you need hello following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="db594-121">Sleutel-id</span><span class="sxs-lookup"><span data-stu-id="db594-121">Key Identifier</span></span>
<span data-ttu-id="db594-122">Hallo sleutel-id kan worden verkregen via Hallo 'Sleutels' pagina in uw Apple Developer-Account</span><span class="sxs-lookup"><span data-stu-id="db594-122">hello key identifier can be obtained from hello "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="db594-123">Toepassings-id & toepassingsnaam</span><span class="sxs-lookup"><span data-stu-id="db594-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="db594-124">de naam van de toepassing Hello is beschikbaar via Hallo App-id's pagina in Hallo Developer-Account.</span><span class="sxs-lookup"><span data-stu-id="db594-124">hello application name is available via hello App IDs page in hello Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="db594-125">Hallo-toepassings-id is beschikbaar via de pagina voor de details van Hallo lidmaatschap in Hallo Developer-Account.</span><span class="sxs-lookup"><span data-stu-id="db594-125">hello application identifier is available via hello membership details page in hello Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="db594-126">Verificatietoken</span><span class="sxs-lookup"><span data-stu-id="db594-126">Authentication token</span></span>
<span data-ttu-id="db594-127">Hallo-verificatietoken kan worden gedownload nadat u een token voor uw toepassing genereren.</span><span class="sxs-lookup"><span data-stu-id="db594-127">hello authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="db594-128">Raadpleeg voor informatie over hoe toogenerate dit token, te[van Apple-documentatie voor ontwikkelaars](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span><span class="sxs-lookup"><span data-stu-id="db594-128">For details on how toogenerate this token, refer too[Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a><span data-ttu-id="db594-129">Uw notification hub toouse op tokens gebaseerde verificatie configureren</span><span class="sxs-lookup"><span data-stu-id="db594-129">Configuring your notification hub toouse token-based authentication</span></span>
### <a name="configure-via-hello-azure-portal"></a><span data-ttu-id="db594-130">Via hello Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="db594-130">Configure via hello Azure portal</span></span>
<span data-ttu-id="db594-131">tooenable token gebaseerde verificatie in Hallo-portal aanmelden toohello Azure-portal en gaat u tooyour Notification Hub > Notification Services > APNS Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="db594-131">tooenable token based authentication in hello portal, log in toohello Azure portal and go tooyour Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="db594-132">Er is een nieuwe eigenschap – *verificatiemodus*.</span><span class="sxs-lookup"><span data-stu-id="db594-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="db594-133">Token kunt u tooupdate uw hub met alle eigenschappen voor relevante Hallo-token.</span><span class="sxs-lookup"><span data-stu-id="db594-133">Selecting Token allows you tooupdate your hub with all hello relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="db594-134">Hallo-eigenschappen die u hebt opgehaald via het Apple developer-account invoeren</span><span class="sxs-lookup"><span data-stu-id="db594-134">Enter hello properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="db594-135">Kies uw toepassingsmodus (productie of Sandbox)</span><span class="sxs-lookup"><span data-stu-id="db594-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="db594-136">Klik op Opslaan tooupdate uw APNS-referenties.</span><span class="sxs-lookup"><span data-stu-id="db594-136">click Save tooupdate your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="db594-137">Configureren via beheer-API (REST)</span><span class="sxs-lookup"><span data-stu-id="db594-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="db594-138">U kunt onze [management API's](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate uw notification hub toouse op tokens gebaseerde verificatie.</span><span class="sxs-lookup"><span data-stu-id="db594-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate your notification hub toouse token-based authentication.</span></span>
<span data-ttu-id="db594-139">Afhankelijk van of Hallo-toepassing die u configureert is een Sandbox of productie-app (opgegeven in uw ontwikkelaarsaccount Apple), een van de bijbehorende eindpunten hello te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="db594-139">Depending on whether hello application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of hello corresponding endpoints:</span></span>

- <span data-ttu-id="db594-140">Sandboxeindpunt: [3-https://api.development.push.apple.com:443-apparaat](https://api.development.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="db594-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="db594-141">Productie-eindpunt: [3-https://api.push.apple.com:443-apparaat](https://api.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="db594-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="db594-142">Verificatie op basis van tokens vereist een API-versie van: **2017 04 of hoger**.</span><span class="sxs-lookup"><span data-stu-id="db594-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="db594-143">Hier volgt een voorbeeld van een PUT-aanvraag tooupdate een hub met verificatie op basis van tokens:</span><span class="sxs-lookup"><span data-stu-id="db594-143">Here’s an example of a PUT request tooupdate a hub with token-based authentication:</span></span>


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
        

### <a name="configure-via-hello-net-sdk"></a><span data-ttu-id="db594-144">Configureren via Hallo .NET SDK</span><span class="sxs-lookup"><span data-stu-id="db594-144">Configure via hello .NET SDK</span></span>
<span data-ttu-id="db594-145">U kunt uw hub toouse token gebaseerde authenticatie met onze [nieuwste client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span><span class="sxs-lookup"><span data-stu-id="db594-145">You can configure your hub toouse token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="db594-146">Hier volgt een voorbeeld van code ter illustratie van Hallo correct te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="db594-146">Here’s a code sample illustrating hello correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a><span data-ttu-id="db594-147">Omzetten toousing certificaat gebaseerde verificatie</span><span class="sxs-lookup"><span data-stu-id="db594-147">Reverting toousing certificate-based authentication</span></span>
<span data-ttu-id="db594-148">U kunt herstellen op een tijd toousing certificaat gebaseerde verificatie met behulp van een voorgaande methode en geven Hallo certificaat in plaats van token Hallo-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="db594-148">You can revert at any time toousing certificate-based authentication by using any preceding method and passing hello certificate instead of hello token properties.</span></span> <span data-ttu-id="db594-149">Dat actie Hallo overschrijft eerder opgeslagen referenties.</span><span class="sxs-lookup"><span data-stu-id="db594-149">That action overwrites hello previously stored credentials.</span></span>
