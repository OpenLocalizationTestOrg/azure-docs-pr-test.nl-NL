---
title: aaaAzure AD Windows Phone-aan de slag | Microsoft Docs
description: "Hoe toobuild een Windows Phone-toepassing die kan worden geïntegreerd met Azure AD voor aanmelden en Azure AD-aanroepen beveiligd met OAuth API's."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: e766bfcdfae10483772154f4b5facdec05fc846f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="b1c25-103">Azure AD integreren met een Windows Phone-App</span><span class="sxs-lookup"><span data-stu-id="b1c25-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="b1c25-104">Projecten met Windows Phone 8.1 en een eerdere versie worden niet ondersteund in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b1c25-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="b1c25-105">Zie [Geschikte platforms voor Visual Studio 2017 en compatibiliteit](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b1c25-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="b1c25-106">Als u een Windows Phone 8.1-app ontwikkelt, kunt Azure AD u eenvoudig en snel voor tooauthenticate u uw gebruikers met hun Active Directory-accounts.</span><span class="sxs-lookup"><span data-stu-id="b1c25-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="b1c25-107">Uw toepassing toosecurely ook kunt gebruiken van een web-API die zijn beveiligd door Azure AD, zoals Office 365-API's Hallo of hello Azure API.</span><span class="sxs-lookup"><span data-stu-id="b1c25-107">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="b1c25-108">Deze voorbeeldcode maakt gebruik van ADAL versie 2.0.</span><span class="sxs-lookup"><span data-stu-id="b1c25-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="b1c25-109">Voor de nieuwste technologie hello, kunt u tooinstead Probeer onze [universele Windows-zelfstudie met behulp van ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span><span class="sxs-lookup"><span data-stu-id="b1c25-109">For hello latest technology, you may want tooinstead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="b1c25-110">Als u een app voor Windows Phone 8.1 inderdaad bouwt, is dit de juiste plaats Hallo.</span><span class="sxs-lookup"><span data-stu-id="b1c25-110">If you are indeed building an app for Windows Phone 8.1, this is hello right place.</span></span>  <span data-ttu-id="b1c25-111">ADAL v2.0 wordt nog steeds volledig ondersteund en hello aanbevolen manier van ontwikkelen apps agianst Windows Phone 8.1 gebruikmaakt van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1c25-111">ADAL v2.0 is still fully supported, and is hello recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="b1c25-112">Azure AD levert voor .NET-systeemeigen clients waarvoor tooaccess beveiligde bronnen, Hallo Active Directory Authentication Library of ADAL.</span><span class="sxs-lookup"><span data-stu-id="b1c25-112">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="b1c25-113">Enig doel in het leven van ADAL toomake is het eenvoudig voor uw app tooget-toegangstokens.</span><span class="sxs-lookup"><span data-stu-id="b1c25-113">ADAL’s sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="b1c25-114">toodemonstrate hoe gemakkelijk het is, hier gaan we gaat verder met een 'Directory Searcher' Windows Phone 8.1-app die:</span><span class="sxs-lookup"><span data-stu-id="b1c25-114">toodemonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="b1c25-115">Krijgt toegang tot tokens voor het aanroepen van hello Azure AD Graph API met behulp van Hallo [OAuth 2.0-verificatieprotocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="b1c25-115">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="b1c25-116">Zoekt een directory voor gebruikers met een opgegeven UPN.</span><span class="sxs-lookup"><span data-stu-id="b1c25-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="b1c25-117">Tekenen gebruikers uit.</span><span class="sxs-lookup"><span data-stu-id="b1c25-117">Signs users out.</span></span>

<span data-ttu-id="b1c25-118">toobuild hello volledige werkende toepassing, moet u naar:</span><span class="sxs-lookup"><span data-stu-id="b1c25-118">toobuild hello complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="b1c25-119">Uw toepassing registreren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1c25-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="b1c25-120">Installeren en configureren van ADAL.</span><span class="sxs-lookup"><span data-stu-id="b1c25-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="b1c25-121">Gebruik ADAL tooget tokens van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1c25-121">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="b1c25-122">tooget gestart, [een basisproject downloaden](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) of [Hallo voltooid voorbeeld downloaden](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="b1c25-122">tooget started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="b1c25-123">Elk is een Visual Studio 2013-oplossing.</span><span class="sxs-lookup"><span data-stu-id="b1c25-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="b1c25-124">U moet ook een Azure AD-tenant kunt u gebruikers maken en een toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="b1c25-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="b1c25-125">Als u niet al een tenant [meer informatie over hoe tooget een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="b1c25-125">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directory-searcher-application"></a><span data-ttu-id="b1c25-126">1. Hallo Directory Searcher-toepassing registreren</span><span class="sxs-lookup"><span data-stu-id="b1c25-126">1. Register hello Directory Searcher Application</span></span>
<span data-ttu-id="b1c25-127">tooenable uw app tooget-tokens, moet u eerst tooregister in uw Azure AD-tenant en verleen deze machtiging tooaccess hello Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="b1c25-127">tooenable your app tooget tokens, you’ll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="b1c25-128">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b1c25-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b1c25-129">Op de bovenste balk hello, klikt u op voor uw account en Hallo **Directory** Kies Hallo Active Directory-tenant waar u wenst dat tooregister uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="b1c25-129">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="b1c25-130">Klik op **meer Services** in linkerkant nav Hallo en kies **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b1c25-130">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="b1c25-131">Klik op **App registraties** en kies **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b1c25-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="b1c25-132">Volg de aanwijzingen Hallo en maak een nieuwe **systeemeigen clienttoepassing**.</span><span class="sxs-lookup"><span data-stu-id="b1c25-132">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="b1c25-133">Hallo **naam** Hallo bevat toepassing een beschrijving van uw toepassing tooend-gebruikers</span><span class="sxs-lookup"><span data-stu-id="b1c25-133">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="b1c25-134">Hallo **omleidings-Uri** is een schema en de tekenreeks combinatie dat tooreturn token antwoorden bij Azure AD wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b1c25-134">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="b1c25-135">Een tijdelijke aanduidingswaarde opgeven voor nu, bijvoorbeeld `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="b1c25-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="b1c25-136">We Vervang deze waarde hoger.</span><span class="sxs-lookup"><span data-stu-id="b1c25-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="b1c25-137">Zodra u inschrijving hebt voltooid, toewijst AAD uw app een unieke id</span><span class="sxs-lookup"><span data-stu-id="b1c25-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="b1c25-138">U moet deze waarde in de volgende secties hello, dus kopieer het van Hallo toepassingstabblad.</span><span class="sxs-lookup"><span data-stu-id="b1c25-138">You’ll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="b1c25-139">Van Hallo **instellingen** pagina **Required Permissions** en kies **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b1c25-139">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="b1c25-140">Selecteer Hallo **Microsoft Graph** als Hallo API en voeg Hallo **Directory-gegevens lezen** machtiging onder **gedelegeerde machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="b1c25-140">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="b1c25-141">Hiermee schakelt u uw toepassing tooquery Hallo Graph API voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b1c25-141">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="b1c25-142">2. Installeren en configureren van ADAL</span><span class="sxs-lookup"><span data-stu-id="b1c25-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="b1c25-143">Nu dat u een toepassing in Azure AD hebt, kunt u ADAL installeert en uw identiteitsgerelateerde code schrijven.</span><span class="sxs-lookup"><span data-stu-id="b1c25-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="b1c25-144">Voor ADAL toobe kunnen toocommunicate met Azure AD, moet u tooprovide met enige informatie over de registratie van uw app.</span><span class="sxs-lookup"><span data-stu-id="b1c25-144">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="b1c25-145">Beginnen met het ADAL toohello DirectorySearcher project met behulp van Hallo Package Manager-Console toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="b1c25-145">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="b1c25-146">Open in Hallo DirectorySearcher project `MainPage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="b1c25-146">In hello DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="b1c25-147">Vervang de waarden Hallo in Hallo `Config Values` regio tooreflect Hallo waarden die u hebt de invoer in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="b1c25-147">Replace hello values in hello `Config Values` region tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="b1c25-148">Uw code zal naar deze waarden verwijzen wanneer deze gebruikmaakt van ADAL.</span><span class="sxs-lookup"><span data-stu-id="b1c25-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="b1c25-149">Hallo `tenant` Hallo domein van uw Azure AD-tenant, bijvoorbeeld contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="b1c25-149">hello `tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="b1c25-150">Hallo `clientId` hello clientId van uw toepassing die u hebt gekopieerd uit de portal Hallo is.</span><span class="sxs-lookup"><span data-stu-id="b1c25-150">hello `clientId` is hello clientId of your application you copied from hello portal.</span></span>
* <span data-ttu-id="b1c25-151">U moet nu toodiscover Hallo callback uri voor uw Windows Phone-app.</span><span class="sxs-lookup"><span data-stu-id="b1c25-151">You now need toodiscover hello callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="b1c25-152">Stel een onderbrekingspunt in op deze regel in Hallo `MainPage` methode:</span><span class="sxs-lookup"><span data-stu-id="b1c25-152">Set a breakpoint on this line in hello `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="b1c25-153">Voer Hallo-app en kopieer gereserveerd Hallo-waarde van `redirectUri` wanneer Hallo onderbrekingspunt is bereikt.</span><span class="sxs-lookup"><span data-stu-id="b1c25-153">Run hello app, and copy aside hello value of `redirectUri` when hello breakpoint is hit.</span></span>  <span data-ttu-id="b1c25-154">Moet er ongeveer als</span><span class="sxs-lookup"><span data-stu-id="b1c25-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="b1c25-155">Terug op Hallo **configureren** tabblad van uw toepassing in hello Azure-beheerportal, vervang de waarde Hallo Hallo **RedirectUri** met deze waarde.</span><span class="sxs-lookup"><span data-stu-id="b1c25-155">Back on hello **Configure** tab of your application in hello Azure Management Portal, replace hello value of hello **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="b1c25-156">3. Gebruik ADAL tooGet Tokens van AAD</span><span class="sxs-lookup"><span data-stu-id="b1c25-156">3. Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="b1c25-157">Hallo basisprincipe achter ADAL is dat wanneer uw app een toegangstoken moet, aanroept `authContext.AcquireToken(…)`, en ADAL Hallo rest.</span><span class="sxs-lookup"><span data-stu-id="b1c25-157">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="b1c25-158">de eerste stap Hallo tooinitialize van uw app is `AuthenticationContext` -ADAL de primaire klasse.</span><span class="sxs-lookup"><span data-stu-id="b1c25-158">hello first step is tooinitialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="b1c25-159">Dit is waar het doorgeven van ADAL Hallo coördinaten moet toocommunicate met Azure AD en meer over toocache tokens.</span><span class="sxs-lookup"><span data-stu-id="b1c25-159">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="b1c25-160">Nu zoeken Hallo `Search(...)` methode, die wordt aangeroepen wanneer Hallo gebruiker cliks knop "Zoeken" in de gebruikersinterface van de app Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b1c25-160">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="b1c25-161">Deze methode maakt een GET-aanvraag toohello Azure AD Graph API tooquery voor gebruikers wiens UPN met de Hallo zoekterm opgegeven begint.</span><span class="sxs-lookup"><span data-stu-id="b1c25-161">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="b1c25-162">Maar in de volgorde tooquery Hallo Graph API, moet u een access_token in Hallo tooinclude `Authorization` header Hallo-aanvraag: dit is waar de ADAL wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="b1c25-162">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try tooget a token without triggering any user prompt.
    // ADAL will check whether hello requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained hello QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="b1c25-163">Als interactieve verificatie nodig is, ADAL van Windows Phone Web Authentication Broker (Windows-Adresboek) wordt gebruikt en [voortzetting model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="b1c25-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD sign in page.</span></span>  <span data-ttu-id="b1c25-164">Wanneer Hallo gebruiker zich aanmeldt, moet uw app toopass ADAL Hallo resultaten van de interactie van de Windows-Adresboek Hallo.</span><span class="sxs-lookup"><span data-stu-id="b1c25-164">When hello user signs in, your app needs toopass ADAL hello results of hello WAB interaction.</span></span>  <span data-ttu-id="b1c25-165">Dit is net zo eenvoudig als het implementeren van Hallo `ContinueWebAuthentication` interface:</span><span class="sxs-lookup"><span data-stu-id="b1c25-165">This is as simple as implementing hello `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when hello application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass hello authentication interaction results tooADAL, which will
    // conclude hello token acquisition operation and invoke hello callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="b1c25-166">Nu gaat u tijd toouse hello `AuthenticationResult` dat ADAL tooyour app geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b1c25-166">Now it's time toouse hello `AuthenticationResult` that ADAL returned tooyour app.</span></span>  <span data-ttu-id="b1c25-167">In Hallo `QueryGraph(...)` retouraanroep, koppel Hallo access_token verkregen van toohello GET-aanvraag in Hallo autorisatie-header:</span><span class="sxs-lookup"><span data-stu-id="b1c25-167">In hello `QueryGraph(...)` callback, attach hello access_token you acquired toohello GET request in hello Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add hello access token toohello Authorization Header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="b1c25-168">U kunt ook Hallo `AuthenticationResult` object toodisplay informatie over Hallo-gebruiker in uw app.</span><span class="sxs-lookup"><span data-stu-id="b1c25-168">You can also use hello `AuthenticationResult` object toodisplay information about hello user in your app.</span></span> <span data-ttu-id="b1c25-169">In Hallo `QueryGraph(...)` methode, gebruik Hallo resultaat tooshow Hallo-id van gebruiker op de pagina Hallo:</span><span class="sxs-lookup"><span data-stu-id="b1c25-169">In hello `QueryGraph(...)` method, use hello result tooshow hello user's id on hello page:</span></span>

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="b1c25-170">Ten slotte kunt u ADAL toosign Hallo gebruiker buiten de toepassing ook gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b1c25-170">Finally, you can use ADAL toosign hello user out of hte application as well.</span></span>  <span data-ttu-id="b1c25-171">Wanneer Hallo gebruiker op de knop 'Afmelden' hello, willen we tooensure die de volgende oproep te Hallo`AcquireTokenSilentAsync(...)` zal mislukken.</span><span class="sxs-lookup"><span data-stu-id="b1c25-171">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="b1c25-172">Met ADAL, is dit is net zo eenvoudig als het token Hallo-cache wissen:</span><span class="sxs-lookup"><span data-stu-id="b1c25-172">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="b1c25-173">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="b1c25-173">Congratulations!</span></span> <span data-ttu-id="b1c25-174">U nu beschikken over een werkende Windows Phone-app die Hallo mogelijkheid tooauthenticate gebruikers heeft, veilig aanroepen van Web-API's met behulp van OAuth 2.0 en basisinformatie over Hallo gebruiker ophalen.</span><span class="sxs-lookup"><span data-stu-id="b1c25-174">You now have a working Windows Phone app that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="b1c25-175">Als u nog niet gedaan hebt, is nu Hallo tijd toopopulate uw tenant waarbij sommige gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b1c25-175">If you haven’t already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="b1c25-176">Uitvoeren van uw app DirectorySearcher en meld u aan met een van deze gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b1c25-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="b1c25-177">Zoeken naar andere gebruikers op basis van de UPN.</span><span class="sxs-lookup"><span data-stu-id="b1c25-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="b1c25-178">Hallo-app sluiten en voer deze opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="b1c25-178">Close hello app, and re-run it.</span></span>  <span data-ttu-id="b1c25-179">U ziet hoe Hallo gebruikerssessie blijft intact.</span><span class="sxs-lookup"><span data-stu-id="b1c25-179">Notice how hello user’s session remains intact.</span></span>  <span data-ttu-id="b1c25-180">Meld u af en meld u opnieuw aan als een andere gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b1c25-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="b1c25-181">ADAL maakt het eenvoudig tooincorporate al deze algemene identiteit functies in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="b1c25-181">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="b1c25-182">Dit zorgt voor alle Hallo dirty werk voor u - Cachebeheer, OAuth-protocolondersteuning, presenteren Hallo-gebruiker met een aanmelding-gebruikersinterface vernieuwen van tokens verlopen en meer.</span><span class="sxs-lookup"><span data-stu-id="b1c25-182">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="b1c25-183">Alles wat u moet tooknow één API-aanroep is `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="b1c25-183">All you really need tooknow is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="b1c25-184">Ter referentie: Hallo voltooid voorbeeld (zonder uw configuratiewaarden) is opgegeven [hier](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="b1c25-184">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="b1c25-185">U kunt nu verplaatsen op tooadditional identity-scenario's.</span><span class="sxs-lookup"><span data-stu-id="b1c25-185">You can now move on tooadditional identity scenarios.</span></span>  <span data-ttu-id="b1c25-186">U kunt tootry:</span><span class="sxs-lookup"><span data-stu-id="b1c25-186">You may want tootry:</span></span>

[<span data-ttu-id="b1c25-187">Een .NET-Web-API met Azure AD beveiligen >></span><span class="sxs-lookup"><span data-stu-id="b1c25-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

