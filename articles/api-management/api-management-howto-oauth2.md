---
title: ontwikkelaarsaccounts aaaAuthorize met behulp van OAuth 2.0 in Azure API Management | Microsoft Docs
description: Meer informatie over hoe tooauthorize gebruikers met behulp van OAuth 2.0 in API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 934901dd6df399470a3257bf7a3a9b9fb5f40d5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a><span data-ttu-id="8b06e-103">Hoe tooauthorize developer gebruikersaccounts via OAuth 2.0 in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="8b06e-103">How tooauthorize developer accounts using OAuth 2.0 in Azure API Management</span></span>
<span data-ttu-id="8b06e-104">Ondersteuning voor veel API's [OAuth 2.0](http://oauth.net/2/) toosecure Hallo API en ervoor te zorgen dat alleen geldige gebruikers toegang hebben en ze alleen toegang resources toowhich tot ze bent recht.</span><span class="sxs-lookup"><span data-stu-id="8b06e-104">Many APIs support [OAuth 2.0](http://oauth.net/2/) toosecure hello API and ensure that only valid users have access, and they can only access resources toowhich they're entitled.</span></span> <span data-ttu-id="8b06e-105">In volgorde toouse Azure API Management van interactieve Developer-Console met deze API's Hallo service kunt u tooconfigure uw service-exemplaar toowork met uw OAuth 2.0 API ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8b06e-105">In order toouse Azure API Management's interactive Developer Console with such APIs, hello service allows you tooconfigure your service instance toowork with your OAuth 2.0 enabled API.</span></span>

## <span data-ttu-id="8b06e-106"><a name="prerequisites"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="8b06e-106"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="8b06e-107">Deze handleiding laat zien u hoe tooconfigure uw API Management-service-exemplaar toouse OAuth 2.0-autorisatie voor ontwikkelaars accounts, maar niet weergegeven. u hoe tooconfigure een OAuth 2.0-provider.</span><span class="sxs-lookup"><span data-stu-id="8b06e-107">This guide shows you how tooconfigure your API Management service instance toouse OAuth 2.0 authorization for developer accounts, but does not show you how tooconfigure an OAuth 2.0 provider.</span></span> <span data-ttu-id="8b06e-108">Hallo-configuratie voor elke OAuth 2.0-provider verschillend zijn, is Hoewel Hallo stappen vergelijkbaar zijn en Hallo vereist stukjes informatie die wordt gebruikt bij het configureren van OAuth 2.0 in uw API Management-service-exemplaar zijn Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="8b06e-108">hello configuration for each OAuth 2.0 provider is different, although hello steps are similar, and hello required pieces of information used in configuring OAuth 2.0 in your API Management service instance are hello same.</span></span> <span data-ttu-id="8b06e-109">Dit onderwerp bevat voorbeelden met Azure Active Directory als een OAuth 2.0-provider.</span><span class="sxs-lookup"><span data-stu-id="8b06e-109">This topic shows examples using Azure Active Directory as an OAuth 2.0 provider.</span></span>

> [!NOTE]
> <span data-ttu-id="8b06e-110">Zie voor meer informatie over het configureren van OAuth 2.0 met Azure Active Directory Hallo [WebApp-GraphAPI-DotNet] [ WebApp-GraphAPI-DotNet] voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="8b06e-110">For more information on configuring OAuth 2.0 using Azure Active Directory, see hello [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] sample.</span></span>
> 
> 

## <span data-ttu-id="8b06e-111"><a name="step1"></a>Een OAuth 2.0-autorisatie-server configureren in API Management</span><span class="sxs-lookup"><span data-stu-id="8b06e-111"><a name="step1"> </a>Configure an OAuth 2.0 authorization server in API Management</span></span>
<span data-ttu-id="8b06e-112">tooget gestart, klikt u op **publicatieportal** in hello Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="8b06e-112">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Publicatieportal][api-management-management-console]

> [!NOTE]
> <span data-ttu-id="8b06e-114">Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="8b06e-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="8b06e-115">Klik op **beveiliging** van Hallo **API Management** menu aan de linkerkant, klik op Hallo **OAuth 2.0**, en klik vervolgens op **toevoegen autorisatie server**.</span><span class="sxs-lookup"><span data-stu-id="8b06e-115">Click **Security** from hello **API Management** menu on hello left, click **OAuth 2.0**, and then click **Add authorization server**.</span></span>

![OAuth 2.0][api-management-oauth2]

<span data-ttu-id="8b06e-117">Wanneer u op **toevoegen autorisatie server**, Hallo nieuwe autorisatie serverformulier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8b06e-117">After clicking **Add authorization server**, hello new authorization server form is displayed.</span></span>

![Nieuwe server][api-management-oauth2-server-1]

<span data-ttu-id="8b06e-119">Voer een naam en een optionele beschrijving in Hallo **naam** en **beschrijving** velden.</span><span class="sxs-lookup"><span data-stu-id="8b06e-119">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> 

> [!NOTE]
> <span data-ttu-id="8b06e-120">Deze velden zijn gebruikte tooidentify Hallo OAuth 2.0 autorisatie server binnen het huidige exemplaar van API Management-service Hallo en hun waarden niet afkomstig van Hallo OAuth 2.0-server.</span><span class="sxs-lookup"><span data-stu-id="8b06e-120">These fields are used tooidentify hello OAuth 2.0 authorization server within hello current API Management service instance and their values do not come from hello OAuth 2.0 server.</span></span>
> 
> 

<span data-ttu-id="8b06e-121">Voer Hallo **Client de registratie van URL**.</span><span class="sxs-lookup"><span data-stu-id="8b06e-121">Enter hello **Client registration page URL**.</span></span> <span data-ttu-id="8b06e-122">Deze pagina is waar gebruikers kunnen maken en beheren van hun account, varieert, afhankelijk van Hallo OAuth 2.0-provider die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8b06e-122">This page is where users can create and manage their accounts, and varies depending on hello OAuth 2.0 provider used.</span></span> <span data-ttu-id="8b06e-123">Hallo **Client de registratie van URL** punten toohello pagina die door gebruikers kunnen toocreate gebruiken en hun eigen accounts configureren voor OAuth 2.0-providers die ondersteuning bieden voor gebruikersbeheer van accounts.</span><span class="sxs-lookup"><span data-stu-id="8b06e-123">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="8b06e-124">Sommige organisaties niet configureert of deze functionaliteit te gebruiken, zelfs als Hallo OAuth 2.0-provider wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="8b06e-124">Some organizations do not configure or use this functionality even if hello OAuth 2.0 provider supports it.</span></span> <span data-ttu-id="8b06e-125">Als uw OAuth 2.0-provider geen Gebruikersbeheer van accounts die zijn geconfigureerd heeft, voert u een tijdelijke aanduiding voor URL hier, zoals het Hallo-URL van uw bedrijf of een URL, zoals `https://placeholder.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="8b06e-125">If your OAuth 2.0 provider does not have user management of accounts configured, enter a placeholder URL here such as hello URL of your company, or a URL such as `https://placeholder.contoso.com`.</span></span>

<span data-ttu-id="8b06e-126">de volgende sectie Hallo van Hallo formulier bevat Hallo **autorisatiecode verlenen typen**, **autorisatie eindpunt-URL**, en **aanvraag autorisatiemethode** instellingen.</span><span class="sxs-lookup"><span data-stu-id="8b06e-126">hello next section of hello form contains hello **Authorization code grant types**, **Authorization endpoint URL**, and **Authorization request method** settings.</span></span>

![Nieuwe server][api-management-oauth2-server-2]

<span data-ttu-id="8b06e-128">Geef Hallo **autorisatiecode verlenen typen** door te controleren Hallo gewenst typen.</span><span class="sxs-lookup"><span data-stu-id="8b06e-128">Specify hello **Authorization code grant types** by checking hello desired types.</span></span> <span data-ttu-id="8b06e-129">**Autorisatiecode** standaard is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="8b06e-129">**Authorization code** is specified by default.</span></span>

<span data-ttu-id="8b06e-130">Voer Hallo **autorisatie eindpunt-URL**.</span><span class="sxs-lookup"><span data-stu-id="8b06e-130">Enter hello **Authorization endpoint URL**.</span></span> <span data-ttu-id="8b06e-131">Voor Azure Active Directory, worden deze URL vergelijkbare toohello-URL, te volgen waarbij `<client_id>` is vervangen door Hallo client-id die uw toepassing toohello OAuth 2.0-server wordt aangeduid.</span><span class="sxs-lookup"><span data-stu-id="8b06e-131">For Azure Active Directory, this URL will be similar toohello following URL, where `<client_id>` is replaced with hello client id that identifies your application toohello OAuth 2.0 server.</span></span>

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

<span data-ttu-id="8b06e-132">Hallo **aanvraag autorisatiemethode** geeft aan hoe Hallo autorisatieaanvraag toohello OAuth 2.0-server is verzonden.</span><span class="sxs-lookup"><span data-stu-id="8b06e-132">hello **Authorization request method** specifies how hello authorization request is sent toohello OAuth 2.0 server.</span></span> <span data-ttu-id="8b06e-133">Standaard **ophalen** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="8b06e-133">By default **GET** is selected.</span></span>

<span data-ttu-id="8b06e-134">de volgende sectie Hallo is waar hello **Token eindpunt-URL**, **Client verificatiemethoden**, **toegangstoken verzenden methode**, en **standaardbereik** zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="8b06e-134">hello next section is where hello **Token endpoint URL**, **Client authentication methods**, **Access token sending method**, and **Default scope** are specified.</span></span>

![Nieuwe server][api-management-oauth2-server-3]

<span data-ttu-id="8b06e-136">Voor een Azure Active Directory OAuth 2.0-server Hallo **Token eindpunt-URL** Hallo volgende indeling hebben waar `<APPID>` heeft Hallo-indeling van `yourapp.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="8b06e-136">For an Azure Active Directory OAuth 2.0 server, hello **Token endpoint URL** will have hello following format, where `<APPID>`  has hello format of `yourapp.onmicrosoft.com`.</span></span>

`https://login.microsoftonline.com/<APPID>/oauth2/token`

<span data-ttu-id="8b06e-137">standaardinstelling voor Hallo **Client verificatiemethoden** is **Basic**, en **toegangstoken verzenden methode** is **autorisatie-header**.</span><span class="sxs-lookup"><span data-stu-id="8b06e-137">hello default setting for **Client authentication methods** is **Basic**, and  **Access token sending method** is **Authorization header**.</span></span> <span data-ttu-id="8b06e-138">Deze waarden zijn geconfigureerd op deze sectie van Hallo formulier, samen met de Hallo **standaardbereik**.</span><span class="sxs-lookup"><span data-stu-id="8b06e-138">These values are configured on this section of hello form, along with hello **Default scope**.</span></span>

<span data-ttu-id="8b06e-139">Hallo **clientreferenties** sectie bevat Hallo **Client-ID** en **clientgeheim**, die zijn verkregen tijdens Hallo maken en de configuratie van uw OAuth 2.0 -Server.</span><span class="sxs-lookup"><span data-stu-id="8b06e-139">hello **Client credentials** section contains hello **Client ID** and **Client secret**, which are obtained during hello creation and configuration process of your OAuth 2.0 server.</span></span> <span data-ttu-id="8b06e-140">Eenmaal Hallo **Client-ID** en **clientgeheim** zijn opgegeven, hello **redirect_uri** voor Hallo **autorisatiecode** wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="8b06e-140">Once hello **Client ID** and **Client secret** are specified, hello **redirect_uri** for hello **authorization code** is generated.</span></span> <span data-ttu-id="8b06e-141">Deze URI wordt gebruikte tooconfigure Hallo antwoord-URL in de configuratie van uw OAuth 2.0-server.</span><span class="sxs-lookup"><span data-stu-id="8b06e-141">This URI is used tooconfigure hello reply URL in your OAuth 2.0 server configuration.</span></span>

![Nieuwe server][api-management-oauth2-server-4]

<span data-ttu-id="8b06e-143">Als **autorisatiecode verlenen typen** te is ingesteld,**Resource eigenaarswachtwoord**, Hallo **wachtwoordreferenties Resource-eigenaar** sectie is gebruikte toospecify die gegevens worden gebruikt. anders kunt u het leeg laten.</span><span class="sxs-lookup"><span data-stu-id="8b06e-143">If **Authorization code grant types** is set too**Resource owner password**, hello **Resource owner password credentials** section is used toospecify those credentials; otherwise you can leave it blank.</span></span>

![Nieuwe server][api-management-oauth2-server-5]

<span data-ttu-id="8b06e-145">Zodra het Hallo-formulier is voltooid, klikt u op **opslaan** toosave Hallo API Management OAuth 2.0-autorisatie-serverconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="8b06e-145">Once hello form is complete, click **Save** toosave hello API Management OAuth 2.0 authorization server configuration.</span></span> <span data-ttu-id="8b06e-146">Zodra Hallo-serverconfiguratie is opgeslagen, kunt u configureren API's toouse deze configuratie, zoals wordt weergegeven in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="8b06e-146">Once hello server configuration is saved, you can configure APIs toouse this configuration, as shown in hello next section.</span></span>

## <span data-ttu-id="8b06e-147"><a name="step2"></a>Een API-toouse OAuth 2.0-gebruikersautorisatie configureren</span><span class="sxs-lookup"><span data-stu-id="8b06e-147"><a name="step2"> </a>Configure an API toouse OAuth 2.0 user authorization</span></span>
<span data-ttu-id="8b06e-148">Klik op **API's** van Hallo **API Management** menu op Hallo van links, klikt u op naam van Hallo gewenst API hello, klik op **beveiliging**, en controleer vervolgens in Hallo voor **OAuth 2.0**.</span><span class="sxs-lookup"><span data-stu-id="8b06e-148">Click **APIs** from hello **API Management** menu on hello left, click hello name of hello desired API, click **Security**, and then check hello box for **OAuth 2.0**.</span></span>

![Gebruikersautorisatie][api-management-user-authorization]

<span data-ttu-id="8b06e-150">Selecteer Hallo gewenst **autorisatie server** in de vervolgkeuzelijst Hallo en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8b06e-150">Select hello desired **Authorization server** from hello drop-down list, and click **Save**.</span></span>

![Gebruikersautorisatie][api-management-user-authorization-save]

## <span data-ttu-id="8b06e-152"><a name="step3"></a>Hello OAuth 2.0-gebruikersautorisatie testen in Hallo-Portal voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="8b06e-152"><a name="step3"> </a>Test hello OAuth 2.0 user authorization in hello Developer Portal</span></span>
<span data-ttu-id="8b06e-153">Zodra u hebt uw OAuth 2.0-autorisatie-server is geconfigureerd en uw API-toouse die server is geconfigureerd, kunt u het testen door te gaan toohello Developer-Portal en een API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="8b06e-153">Once you have configured your OAuth 2.0 authorization server and configured your API toouse that server, you can test it by going toohello Developer Portal and calling an API.</span></span>  <span data-ttu-id="8b06e-154">Klik op **ontwikkelaarsportal** in Hallo menu rechtsboven.</span><span class="sxs-lookup"><span data-stu-id="8b06e-154">Click **Developer portal** in hello top right menu.</span></span>

![ontwikkelaarsportal][api-management-developer-portal-menu]

<span data-ttu-id="8b06e-156">Klik op **API's** in Hallo bovenste menu en selecteer **Echo-API**.</span><span class="sxs-lookup"><span data-stu-id="8b06e-156">Click **APIs** in hello top menu and select **Echo API**.</span></span>

![Echo-API][api-management-apis-echo-api]

> [!NOTE]
> <span data-ttu-id="8b06e-158">Als er slechts één API is geconfigureerd of zichtbaar tooyour-account op de API's te klikken u rechtstreeks toohello bewerkingen voor die API gaat.</span><span class="sxs-lookup"><span data-stu-id="8b06e-158">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="8b06e-159">Selecteer Hallo **GET Resource** bewerking, klikt u op **Console openen**, en selecteer vervolgens **autorisatiecode** Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="8b06e-159">Select hello **GET Resource** operation, click **Open Console**, and then select **Authorization code** from hello drop-down.</span></span>

![Console openen][api-management-open-console]

<span data-ttu-id="8b06e-161">Wanneer **autorisatiecode** is geselecteerd, wordt een pop-upvenster weergegeven met Hallo aanmelden vorm van Hallo OAuth 2.0-provider.</span><span class="sxs-lookup"><span data-stu-id="8b06e-161">When **Authorization code** is selected, a pop-up window is displayed with hello sign-in form of hello OAuth 2.0 provider.</span></span> <span data-ttu-id="8b06e-162">In dit voorbeeld wordt Hallo aanmelden formulier verstrekt door Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8b06e-162">In this example hello sign-in form is provided by Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="8b06e-163">Als u pop-ups hebt uitgeschakeld, u zult gevraagd tooenable ze door Hallo browser.</span><span class="sxs-lookup"><span data-stu-id="8b06e-163">If you have pop-ups disabled you will be prompted tooenable them by hello browser.</span></span> <span data-ttu-id="8b06e-164">Nadat u deze wilt inschakelen, selecteert u **autorisatiecode** opnieuw en hello aanmelden formulier worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8b06e-164">After you enable them, select **Authorization code** again and hello sign-in form will be displayed.</span></span>
> 
> 

![Aanmelden][api-management-oauth2-signin]

<span data-ttu-id="8b06e-166">Zodra u zich hebt aangemeld, Hallo **aanvraagheaders** zijn gevuld met een `Authorization : Bearer` Hallo aanvraag machtigt-header.</span><span class="sxs-lookup"><span data-stu-id="8b06e-166">Once you have signed in, hello **Request headers** are populated with an `Authorization : Bearer` header that authorizes hello request.</span></span>

![Token voor verbindingsverzoeken-header][api-management-request-header-token]

<span data-ttu-id="8b06e-168">U kunt op dit moment Hallo gewenst waarden voor Hallo resterende parameters configureren en Hallo aanvraag indienen.</span><span class="sxs-lookup"><span data-stu-id="8b06e-168">At this point you can configure hello desired values for hello remaining parameters, and submit hello request.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8b06e-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8b06e-169">Next steps</span></span>
<span data-ttu-id="8b06e-170">Zie voor meer informatie over het gebruik van OAuth 2.0 en API Management Hallo volgende video en bijbehorende [artikel](api-management-howto-protect-backend-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="8b06e-170">For more information about using OAuth 2.0 and API Management, see hello following video and accompanying [article](api-management-howto-protect-backend-with-aad.md).</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: ./media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: ./media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: ./media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: ./media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: ./media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: ./media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: ./media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: ./media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: ./media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: ./media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: ./media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: ./media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: ./media/api-management-howto-oauth2/api-management-apis-echo-api.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

