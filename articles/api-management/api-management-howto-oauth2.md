---
title: Ontwikkelaarsaccounts in Azure API Management met behulp van OAuth 2.0 autoriseren | Microsoft Docs
description: Informatie over het autoriseren van gebruikers met behulp van OAuth 2.0 in API Management.
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
ms.openlocfilehash: a19c453bb3271374b587f3d0b35adad55863b490
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-authorize-developer-accounts-using-oauth-20-in-azure-api-management"></a><span data-ttu-id="e10fd-103">Het autoriseren van ontwikkelaarsaccounts met behulp van OAuth 2.0 in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="e10fd-103">How to authorize developer accounts using OAuth 2.0 in Azure API Management</span></span>
<span data-ttu-id="e10fd-104">Ondersteuning voor veel API's [OAuth 2.0](http://oauth.net/2/) de API beveiligen en ervoor te zorgen dat alleen geldige gebruikers toegang hebben en ze alleen toegang tot resources waarnaar ze bevoegd bent.</span><span class="sxs-lookup"><span data-stu-id="e10fd-104">Many APIs support [OAuth 2.0](http://oauth.net/2/) to secure the API and ensure that only valid users have access, and they can only access resources to which they're entitled.</span></span> <span data-ttu-id="e10fd-105">Om interactieve Azure API Management-Ontwikkelaarsconsole met deze API's gebruiken, kunt de service u voor het configureren van uw service-exemplaar om te werken met uw OAuth 2.0 ingeschakelde API.</span><span class="sxs-lookup"><span data-stu-id="e10fd-105">In order to use Azure API Management's interactive Developer Console with such APIs, the service allows you to configure your service instance to work with your OAuth 2.0 enabled API.</span></span>

## <span data-ttu-id="e10fd-106"><a name="prerequisites"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="e10fd-106"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="e10fd-107">Deze handleiding leest u hoe uw API Management-service-exemplaar voor het gebruik van OAuth 2.0-autorisatie voor ontwikkelaarsaccounts configureren, maar wordt niet beschreven hoe u een OAuth 2.0-provider configureren.</span><span class="sxs-lookup"><span data-stu-id="e10fd-107">This guide shows you how to configure your API Management service instance to use OAuth 2.0 authorization for developer accounts, but does not show you how to configure an OAuth 2.0 provider.</span></span> <span data-ttu-id="e10fd-108">De configuratie voor elke OAuth 2.0-provider is verschillend zijn, hoewel de stappen vergelijkbaar zijn, en de vereiste stukjes informatie die wordt gebruikt bij het configureren van OAuth 2.0 in uw API Management-service-exemplaar hetzelfde zijn.</span><span class="sxs-lookup"><span data-stu-id="e10fd-108">The configuration for each OAuth 2.0 provider is different, although the steps are similar, and the required pieces of information used in configuring OAuth 2.0 in your API Management service instance are the same.</span></span> <span data-ttu-id="e10fd-109">Dit onderwerp bevat voorbeelden met Azure Active Directory als een OAuth 2.0-provider.</span><span class="sxs-lookup"><span data-stu-id="e10fd-109">This topic shows examples using Azure Active Directory as an OAuth 2.0 provider.</span></span>

> [!NOTE]
> <span data-ttu-id="e10fd-110">Zie voor meer informatie over het configureren van OAuth 2.0 met Azure Active Directory de [WebApp-GraphAPI-DotNet] [ WebApp-GraphAPI-DotNet] voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="e10fd-110">For more information on configuring OAuth 2.0 using Azure Active Directory, see the [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] sample.</span></span>
> 
> 

## <span data-ttu-id="e10fd-111"><a name="step1"></a>Een OAuth 2.0-autorisatie-server configureren in API Management</span><span class="sxs-lookup"><span data-stu-id="e10fd-111"><a name="step1"> </a>Configure an OAuth 2.0 authorization server in API Management</span></span>
<span data-ttu-id="e10fd-112">Als u aan de slag wilt gaan, klikt u op **Publicatieportal** in Azure Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="e10fd-112">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Publicatieportal][api-management-management-console]

> [!NOTE]
> <span data-ttu-id="e10fd-114">Als u nog geen service-exemplaar van API Management hebt gemaakt, raadpleegt u [Service-exemplaar van API Management maken][Create an API Management service instance] in de zelfstudie [Aan de slag met Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="e10fd-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="e10fd-115">Klik op **beveiliging** van de **API Management** menu aan de linkerkant, klik op **OAuth 2.0**, en klik vervolgens op **toevoegen autorisatie server**.</span><span class="sxs-lookup"><span data-stu-id="e10fd-115">Click **Security** from the **API Management** menu on the left, click **OAuth 2.0**, and then click **Add authorization server**.</span></span>

![OAuth 2.0][api-management-oauth2]

<span data-ttu-id="e10fd-117">Wanneer u op **toevoegen autorisatie server**, de nieuwe vorm van de autorisatie-server wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e10fd-117">After clicking **Add authorization server**, the new authorization server form is displayed.</span></span>

![Nieuwe server][api-management-oauth2-server-1]

<span data-ttu-id="e10fd-119">Voer een naam en een optionele beschrijving in de **naam** en **beschrijving** velden.</span><span class="sxs-lookup"><span data-stu-id="e10fd-119">Enter a name and an optional description in the **Name** and **Description** fields.</span></span> 

> [!NOTE]
> <span data-ttu-id="e10fd-120">Deze velden worden gebruikt voor het identificeren van de OAuth 2.0-autorisatie-server binnen de huidige service-exemplaar van API Management en hun waarden niet afkomstig zijn van de OAuth 2.0-server.</span><span class="sxs-lookup"><span data-stu-id="e10fd-120">These fields are used to identify the OAuth 2.0 authorization server within the current API Management service instance and their values do not come from the OAuth 2.0 server.</span></span>
> 
> 

<span data-ttu-id="e10fd-121">Voer de **Client de registratie van URL**.</span><span class="sxs-lookup"><span data-stu-id="e10fd-121">Enter the **Client registration page URL**.</span></span> <span data-ttu-id="e10fd-122">Deze pagina is waar gebruikers kunnen maken en beheren van hun account, varieert, afhankelijk van de OAuth 2.0-provider gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e10fd-122">This page is where users can create and manage their accounts, and varies depending on the OAuth 2.0 provider used.</span></span> <span data-ttu-id="e10fd-123">De **Client de registratie van URL** verwijst naar de pagina die gebruikers gebruiken kunnen voor het maken en hun eigen accounts configureren voor OAuth 2.0-providers die ondersteuning bieden voor gebruikersbeheer van accounts.</span><span class="sxs-lookup"><span data-stu-id="e10fd-123">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="e10fd-124">Sommige organisaties niet configureert of deze functionaliteit te gebruiken, zelfs als de provider OAuth 2.0 wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="e10fd-124">Some organizations do not configure or use this functionality even if the OAuth 2.0 provider supports it.</span></span> <span data-ttu-id="e10fd-125">Als uw OAuth 2.0-provider geen Gebruikersbeheer van accounts die zijn geconfigureerd heeft, voert u een tijdelijke aanduiding voor URL hier, zoals de URL van uw bedrijf of een URL, zoals `https://placeholder.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="e10fd-125">If your OAuth 2.0 provider does not have user management of accounts configured, enter a placeholder URL here such as the URL of your company, or a URL such as `https://placeholder.contoso.com`.</span></span>

<span data-ttu-id="e10fd-126">De volgende sectie van het formulier bevat de **autorisatiecode verlenen typen**, **autorisatie eindpunt-URL**, en **aanvraag autorisatiemethode** instellingen.</span><span class="sxs-lookup"><span data-stu-id="e10fd-126">The next section of the form contains the **Authorization code grant types**, **Authorization endpoint URL**, and **Authorization request method** settings.</span></span>

![Nieuwe server][api-management-oauth2-server-2]

<span data-ttu-id="e10fd-128">Geef de **autorisatiecode verlenen typen** door het controleren van de gewenste typen.</span><span class="sxs-lookup"><span data-stu-id="e10fd-128">Specify the **Authorization code grant types** by checking the desired types.</span></span> <span data-ttu-id="e10fd-129">**Autorisatiecode** standaard is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e10fd-129">**Authorization code** is specified by default.</span></span>

<span data-ttu-id="e10fd-130">Voer de **autorisatie eindpunt-URL**.</span><span class="sxs-lookup"><span data-stu-id="e10fd-130">Enter the **Authorization endpoint URL**.</span></span> <span data-ttu-id="e10fd-131">Voor Azure Active Directory, deze URL zijn vergelijkbaar met de volgende URL waar `<client_id>` is vervangen door de client-id die uw toepassing met het OAuth 2.0-server te identificeren.</span><span class="sxs-lookup"><span data-stu-id="e10fd-131">For Azure Active Directory, this URL will be similar to the following URL, where `<client_id>` is replaced with the client id that identifies your application to the OAuth 2.0 server.</span></span>

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

<span data-ttu-id="e10fd-132">De **aanvraag autorisatiemethode** geeft aan hoe de autorisatieaanvraag is verzonden naar de OAuth 2.0-server.</span><span class="sxs-lookup"><span data-stu-id="e10fd-132">The **Authorization request method** specifies how the authorization request is sent to the OAuth 2.0 server.</span></span> <span data-ttu-id="e10fd-133">Standaard **ophalen** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="e10fd-133">By default **GET** is selected.</span></span>

<span data-ttu-id="e10fd-134">De volgende sectie waar is de **Token eindpunt-URL**, **Client verificatiemethoden**, **toegangstoken verzenden methode**, en **standaardbereik** zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e10fd-134">The next section is where the **Token endpoint URL**, **Client authentication methods**, **Access token sending method**, and **Default scope** are specified.</span></span>

![Nieuwe server][api-management-oauth2-server-3]

<span data-ttu-id="e10fd-136">Voor een Azure Active Directory OAuth 2.0-server de **Token eindpunt-URL** hebben de volgende indeling waar `<APPID>` heeft de indeling van `yourapp.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="e10fd-136">For an Azure Active Directory OAuth 2.0 server, the **Token endpoint URL** will have the following format, where `<APPID>`  has the format of `yourapp.onmicrosoft.com`.</span></span>

`https://login.microsoftonline.com/<APPID>/oauth2/token`

<span data-ttu-id="e10fd-137">De standaardinstelling voor **Client verificatiemethoden** is **Basic**, en **toegangstoken verzenden methode** is **autorisatie-header**.</span><span class="sxs-lookup"><span data-stu-id="e10fd-137">The default setting for **Client authentication methods** is **Basic**, and  **Access token sending method** is **Authorization header**.</span></span> <span data-ttu-id="e10fd-138">Deze waarden zijn geconfigureerd op deze sectie van het formulier, samen met de **standaardbereik**.</span><span class="sxs-lookup"><span data-stu-id="e10fd-138">These values are configured on this section of the form, along with the **Default scope**.</span></span>

<span data-ttu-id="e10fd-139">De **clientreferenties** sectie bevat de **Client-ID** en **clientgeheim**, die zijn verkregen tijdens het maken en de configuratie van uw OAuth 2.0-server.</span><span class="sxs-lookup"><span data-stu-id="e10fd-139">The **Client credentials** section contains the **Client ID** and **Client secret**, which are obtained during the creation and configuration process of your OAuth 2.0 server.</span></span> <span data-ttu-id="e10fd-140">Eenmaal de **Client-ID** en **clientgeheim** zijn opgegeven, de **redirect_uri** voor de **autorisatiecode** wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="e10fd-140">Once the **Client ID** and **Client secret** are specified, the **redirect_uri** for the **authorization code** is generated.</span></span> <span data-ttu-id="e10fd-141">Deze URI wordt gebruikt voor het configureren van de antwoord-URL in de configuratie van uw OAuth 2.0-server.</span><span class="sxs-lookup"><span data-stu-id="e10fd-141">This URI is used to configure the reply URL in your OAuth 2.0 server configuration.</span></span>

![Nieuwe server][api-management-oauth2-server-4]

<span data-ttu-id="e10fd-143">Als **autorisatiecode verlenen typen** is ingesteld op **Resource eigenaarswachtwoord**, wordt de **wachtwoordreferenties Resource-eigenaar** sectie wordt gebruikt om op te geven die referenties; anders kunt u het leeg laten.</span><span class="sxs-lookup"><span data-stu-id="e10fd-143">If **Authorization code grant types** is set to **Resource owner password**, the **Resource owner password credentials** section is used to specify those credentials; otherwise you can leave it blank.</span></span>

![Nieuwe server][api-management-oauth2-server-5]

<span data-ttu-id="e10fd-145">Wanneer het formulier voltooid is, klikt u op **opslaan** om op te slaan van de configuratie van de API Management OAuth 2.0-autorisatie-server.</span><span class="sxs-lookup"><span data-stu-id="e10fd-145">Once the form is complete, click **Save** to save the API Management OAuth 2.0 authorization server configuration.</span></span> <span data-ttu-id="e10fd-146">Zodra de serverconfiguratie is opgeslagen, kunt u API's voor het gebruik van deze configuratie kunt configureren, zoals wordt weergegeven in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="e10fd-146">Once the server configuration is saved, you can configure APIs to use this configuration, as shown in the next section.</span></span>

## <span data-ttu-id="e10fd-147"><a name="step2"></a>Een API voor het gebruik van OAuth 2.0-gebruikersautorisatie configureren</span><span class="sxs-lookup"><span data-stu-id="e10fd-147"><a name="step2"> </a>Configure an API to use OAuth 2.0 user authorization</span></span>
<span data-ttu-id="e10fd-148">Klik op **API's** van de **API Management** menu aan de linkerkant, klik op de naam van de gewenste API, klik op **beveiliging**, en vervolgens het selectievakje in voor **OAuth 2.0**.</span><span class="sxs-lookup"><span data-stu-id="e10fd-148">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, click **Security**, and then check the box for **OAuth 2.0**.</span></span>

![Gebruikersautorisatie][api-management-user-authorization]

<span data-ttu-id="e10fd-150">Selecteer de gewenste **autorisatie server** in de vervolgkeuzelijst en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e10fd-150">Select the desired **Authorization server** from the drop-down list, and click **Save**.</span></span>

![Gebruikersautorisatie][api-management-user-authorization-save]

## <span data-ttu-id="e10fd-152"><a name="step3"></a>Het OAuth 2.0-gebruikersautorisatie testen in de Portal voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="e10fd-152"><a name="step3"> </a>Test the OAuth 2.0 user authorization in the Developer Portal</span></span>
<span data-ttu-id="e10fd-153">Zodra u hebt uw OAuth 2.0-autorisatie-server is geconfigureerd en uw API voor het gebruik van die server geconfigureerd, kunt u het testen door te gaan naar de Ontwikkelaarsportal en een API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="e10fd-153">Once you have configured your OAuth 2.0 authorization server and configured your API to use that server, you can test it by going to the Developer Portal and calling an API.</span></span>  <span data-ttu-id="e10fd-154">Klik op **ontwikkelaarsportal** in het menu rechtsboven.</span><span class="sxs-lookup"><span data-stu-id="e10fd-154">Click **Developer portal** in the top right menu.</span></span>

![ontwikkelaarsportal][api-management-developer-portal-menu]

<span data-ttu-id="e10fd-156">Klik op **API's** in het bovenste menu en selecteer **Echo-API**.</span><span class="sxs-lookup"><span data-stu-id="e10fd-156">Click **APIs** in the top menu and select **Echo API**.</span></span>

![Echo-API][api-management-apis-echo-api]

> [!NOTE]
> <span data-ttu-id="e10fd-158">Als er slechts één API is geconfigureerd of zichtbaar is voor uw account, gaat u wanneer u op API's klikt rechtstreeks naar de bewerkingen voor die API.</span><span class="sxs-lookup"><span data-stu-id="e10fd-158">If you have only one API configured or visible to your account, then clicking APIs takes you directly to the operations for that API.</span></span>
> 
> 

<span data-ttu-id="e10fd-159">Selecteer de **GET Resource** bewerking, klikt u op **Console openen**, en selecteer vervolgens **autorisatiecode** in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="e10fd-159">Select the **GET Resource** operation, click **Open Console**, and then select **Authorization code** from the drop-down.</span></span>

![Console openen][api-management-open-console]

<span data-ttu-id="e10fd-161">Wanneer **autorisatiecode** is geselecteerd, wordt een pop-upvenster weergegeven met de vorm aanmelden van de OAuth 2.0-provider.</span><span class="sxs-lookup"><span data-stu-id="e10fd-161">When **Authorization code** is selected, a pop-up window is displayed with the sign-in form of the OAuth 2.0 provider.</span></span> <span data-ttu-id="e10fd-162">In dit voorbeeld wordt het formulier aanmelden verstrekt door Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e10fd-162">In this example the sign-in form is provided by Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="e10fd-163">Als u pop-ups uitgeschakeld hebt wordt u gevraagd deze inschakelen door de browser.</span><span class="sxs-lookup"><span data-stu-id="e10fd-163">If you have pop-ups disabled you will be prompted to enable them by the browser.</span></span> <span data-ttu-id="e10fd-164">Nadat u deze wilt inschakelen, selecteert u **autorisatiecode** opnieuw en het formulier worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e10fd-164">After you enable them, select **Authorization code** again and the sign-in form will be displayed.</span></span>
> 
> 

![Aanmelden][api-management-oauth2-signin]

<span data-ttu-id="e10fd-166">Wanneer u bent aangemeld, de **aanvraagheaders** zijn gevuld met een `Authorization : Bearer` de aanvraag machtigt-header.</span><span class="sxs-lookup"><span data-stu-id="e10fd-166">Once you have signed in, the **Request headers** are populated with an `Authorization : Bearer` header that authorizes the request.</span></span>

![Token voor verbindingsverzoeken-header][api-management-request-header-token]

<span data-ttu-id="e10fd-168">Op dit moment kunt u configureren van de gewenste waarden voor de resterende parameters en dien de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="e10fd-168">At this point you can configure the desired values for the remaining parameters, and submit the request.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e10fd-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e10fd-169">Next steps</span></span>
<span data-ttu-id="e10fd-170">Zie voor meer informatie over het gebruik van OAuth 2.0 en API Management, de volgende video en bijbehorende [artikel](api-management-howto-protect-backend-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="e10fd-170">For more information about using OAuth 2.0 and API Management, see the following video and accompanying [article](api-management-howto-protect-backend-with-aad.md).</span></span>

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


[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

