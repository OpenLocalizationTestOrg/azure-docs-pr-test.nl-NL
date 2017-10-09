---
title: aaaAzure AD Windows Store aan de slag | Microsoft Docs
description: Build Windows Store-apps die integreren met Azure AD voor aanmelden en roept u Azure AD beveiligd met OAuth API's.
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="d7e40-103">Azure AD integreren met Windows Store-apps</span><span class="sxs-lookup"><span data-stu-id="d7e40-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="d7e40-104">Windows Store 8.1 en projecten met een eerdere versie worden niet ondersteund in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d7e40-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="d7e40-105">Zie [Geschikte platforms voor Visual Studio 2017 en compatibiliteit](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d7e40-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="d7e40-106">Als u apps voor Windows Store Hallo ontwikkelt, Azure Active Directory (Azure AD) maakt het eenvoudig en snel tooauthenticate uw gebruikers met hun Active Directory-accounts.</span><span class="sxs-lookup"><span data-stu-id="d7e40-106">If you're developing apps for hello Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward tooauthenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="d7e40-107">Een app door te integreren met Azure AD, kan veilig een web-API die wordt beveiligd door Azure AD, zoals Office 365-API's Hallo of hello Azure API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d7e40-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="d7e40-108">Voor Windows Store-desktoptoepassingen die dat tooaccess beveiligde bronnen nodig hebt, biedt Azure AD Hallo Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="d7e40-108">For Windows Store desktop apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="d7e40-109">Hallo enig doel van ADAL is toomake gemakkelijk Hallo app tooget toegangstokens.</span><span class="sxs-lookup"><span data-stu-id="d7e40-109">hello sole purpose of ADAL is toomake it easy for hello app tooget access tokens.</span></span> <span data-ttu-id="d7e40-110">toodemonstrate hoe eenvoudig het is dit artikel laat zien hoe toobuild een DirectorySearcher Windows Store-app die:</span><span class="sxs-lookup"><span data-stu-id="d7e40-110">toodemonstrate how easy it is, this article shows how toobuild a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="d7e40-111">Krijgt toegang tot tokens voor hello Azure AD Graph API aanroept met behulp van Hallo [OAuth 2.0-verificatieprotocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="d7e40-111">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="d7e40-112">Zoekt een directory voor gebruikers met een opgegeven user principal name (UPN).</span><span class="sxs-lookup"><span data-stu-id="d7e40-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="d7e40-113">Tekenen gebruikers uit.</span><span class="sxs-lookup"><span data-stu-id="d7e40-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="d7e40-114">Voordat u aan de slag gaat</span><span class="sxs-lookup"><span data-stu-id="d7e40-114">Before you get started</span></span>
* <span data-ttu-id="d7e40-115">Hallo downloaden [basisproject](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), of downloaden Hallo [voltooide voorbeeld](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="d7e40-115">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="d7e40-116">Elke download is een Visual Studio 2015-oplossing.</span><span class="sxs-lookup"><span data-stu-id="d7e40-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="d7e40-117">U moet ook een Azure AD-tenant in welke toocreate gebruikers en het Hallo-app registreren.</span><span class="sxs-lookup"><span data-stu-id="d7e40-117">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="d7e40-118">Als u niet al een tenant [meer informatie over hoe tooget een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="d7e40-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="d7e40-119">Wanneer u klaar bent, Hallo Hallo-procedures volgen in de volgende drie secties.</span><span class="sxs-lookup"><span data-stu-id="d7e40-119">When you are ready, follow hello procedures in hello next three sections.</span></span>

## <a name="step-1-register-hello-directorysearcher-app"></a><span data-ttu-id="d7e40-120">Stap 1: Hallo DirectorySearcher app registreren</span><span class="sxs-lookup"><span data-stu-id="d7e40-120">Step 1: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="d7e40-121">tooenable hello app tooget-tokens, moet u eerst tooregister in uw Azure AD-tenant en verleen deze machtiging tooaccess hello Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="d7e40-121">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="d7e40-122">Dit doet u al volgt:</span><span class="sxs-lookup"><span data-stu-id="d7e40-122">Here's how:</span></span>

1. <span data-ttu-id="d7e40-123">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d7e40-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d7e40-124">Klik op de bovenste balk hello, uw account.</span><span class="sxs-lookup"><span data-stu-id="d7e40-124">On hello top bar, click your account.</span></span> <span data-ttu-id="d7e40-125">Klik vervolgens onder Hallo **Directory** lijst, selecteer Hallo Active Directory-tenant waar u tooregister Hallo app.</span><span class="sxs-lookup"><span data-stu-id="d7e40-125">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="d7e40-126">Klik op **meer Services** in Hallo linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d7e40-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="d7e40-127">Klik op **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d7e40-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="d7e40-128">Ga als volgt Hallo prompts toocreate een **systeemeigen clienttoepassing**.</span><span class="sxs-lookup"><span data-stu-id="d7e40-128">Follow hello prompts toocreate a **Native Client Application**.</span></span>
  * <span data-ttu-id="d7e40-129">**Naam** Hallo app toousers beschrijft.</span><span class="sxs-lookup"><span data-stu-id="d7e40-129">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="d7e40-130">**Omleidings-URI** is een schema en de tekenreeks combinatie dat gebruikmaakt van Azure AD tooreturn token antwoorden.</span><span class="sxs-lookup"><span data-stu-id="d7e40-130">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="d7e40-131">Voer een aanduidingswaarde van de tijdelijke voor nu (bijvoorbeeld **http://DirectorySearcher**).</span><span class="sxs-lookup"><span data-stu-id="d7e40-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="d7e40-132">Vervangt u de waarde hello later.</span><span class="sxs-lookup"><span data-stu-id="d7e40-132">You'll replace hello value later.</span></span>
6. <span data-ttu-id="d7e40-133">Nadat u Hallo-registratie hebt voltooid, wijst Azure AD Hallo app een unieke toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="d7e40-133">After you’ve completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="d7e40-134">Hallo-waarde op Hallo kopiëren **toepassing** tabblad omdat u hebt deze later nodig.</span><span class="sxs-lookup"><span data-stu-id="d7e40-134">Copy hello value on hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="d7e40-135">Op Hallo **instellingen** pagina **Required Permissions**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d7e40-135">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="d7e40-136">Voor Hallo **Azure Active Directory** app, selecteer **Microsoft Graph** zoals Hallo API.</span><span class="sxs-lookup"><span data-stu-id="d7e40-136">For hello **Azure Active Directory** app, select **Microsoft Graph** as hello API.</span></span>
9. <span data-ttu-id="d7e40-137">Onder **gedelegeerde machtigingen**, Hallo toevoegen **toegang Hallo directory als de gebruiker is aangemeld Hallo** machtiging.</span><span class="sxs-lookup"><span data-stu-id="d7e40-137">Under **Delegated Permissions**, add hello **Access hello directory as hello signed-in user** permission.</span></span> <span data-ttu-id="d7e40-138">In dat geval kunnen Hallo app tooquery Hallo Graph API voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d7e40-138">Doing so enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="d7e40-139">Stap 2: Installeren en configureren van ADAL</span><span class="sxs-lookup"><span data-stu-id="d7e40-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="d7e40-140">Nu dat u een app in Azure AD hebt, kunt u ADAL installeert en uw identiteitsgerelateerde code schrijven.</span><span class="sxs-lookup"><span data-stu-id="d7e40-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="d7e40-141">ADAL toocommunicate tooenable in Azure AD, geef deze de enige informatie over app-registratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="d7e40-141">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="d7e40-142">ADAL toohello DirectorySearcher project toevoegen met behulp van Hallo Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="d7e40-142">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="d7e40-143">Open in Hallo DirectorySearcher project MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="d7e40-143">In hello DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="d7e40-144">Vervang de waarden Hallo in Hallo **configuratiewaarden** regio met Hallo-waarden die u hebt ingevoerd in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d7e40-144">Replace hello values in hello **Config Values** region with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="d7e40-145">Uw code verwijst toothese waarden wanneer deze gebruikmaakt van ADAL.</span><span class="sxs-lookup"><span data-stu-id="d7e40-145">Your code refers toothese values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="d7e40-146">Hallo *tenant* Hallo domein van uw Azure AD-tenant (bijvoorbeeld: contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="d7e40-146">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="d7e40-147">Hallo *clientId* is Hallo client-ID van Hallo-app, die u hebt gekopieerd uit Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="d7e40-147">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
4. <span data-ttu-id="d7e40-148">U moet nu toodiscover Hallo callback URI voor uw Windows Store-app.</span><span class="sxs-lookup"><span data-stu-id="d7e40-148">You now need toodiscover hello callback URI for your Windows Store app.</span></span> <span data-ttu-id="d7e40-149">Stel een onderbrekingspunt in op deze regel in Hallo `MainPage` methode:</span><span class="sxs-lookup"><span data-stu-id="d7e40-149">Set a breakpoint on this line in hello `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="d7e40-150">Bouwen Hallo-oplossing, om ervoor te zorgen dat alle pakket-verwijzingen zijn hersteld.</span><span class="sxs-lookup"><span data-stu-id="d7e40-150">Build hello solution, making sure that all package references are restored.</span></span> <span data-ttu-id="d7e40-151">Als er pakketten ontbreken, Hallo NuGet Package Manager openen en deze terugzetten.</span><span class="sxs-lookup"><span data-stu-id="d7e40-151">If any packages are missing, open hello NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="d7e40-152">Voer Hallo-app en kopieer Hallo-waarde van `redirectUri` wanneer Hallo onderbrekingspunt is bereikt.</span><span class="sxs-lookup"><span data-stu-id="d7e40-152">Run hello app, and copy hello value of `redirectUri` when hello breakpoint is hit.</span></span> <span data-ttu-id="d7e40-153">Hallo-waarde moet er ongeveer als Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="d7e40-153">hello value should look something like hello following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="d7e40-154">Terug op Hallo **instellingen** tabblad van het Hallo-app in hello Azure-portal, Voeg een **RedirectUri** Hello vóór waarde.</span><span class="sxs-lookup"><span data-stu-id="d7e40-154">Back on hello **Settings** tab of hello app in hello Azure portal, add a **RedirectUri** with hello preceding value.</span></span>  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="d7e40-155">Stap 3: Gebruik ADAL tooget tokens van Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7e40-155">Step 3: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="d7e40-156">Hallo basisprincipe achter ADAL is dat wanneer het Hallo-app moet een toegangstoken, aanroept `authContext.AcquireToken(…)`, en ADAL Hallo rest.</span><span class="sxs-lookup"><span data-stu-id="d7e40-156">hello basic principle behind ADAL is that whenever hello app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="d7e40-157">Initialiseren van de app Hallo `AuthenticationContext`, dit is de primaire klasse Hallo van ADAL.</span><span class="sxs-lookup"><span data-stu-id="d7e40-157">Initialize hello app’s `AuthenticationContext`, which is hello primary class of ADAL.</span></span> <span data-ttu-id="d7e40-158">Deze actie wordt doorgegeven ADAL Hallo coördinaten deze moet toocommunicate met Azure AD en meer over toocache tokens.</span><span class="sxs-lookup"><span data-stu-id="d7e40-158">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="d7e40-159">Zoek Hallo `Search(...)` methode die wordt opgeroepen wanneer gebruikers op Hallo **Search** knop op de gebruikersinterface van de app Hallo.</span><span class="sxs-lookup"><span data-stu-id="d7e40-159">Locate hello `Search(...)` method, which is invoked when users click hello **Search** button on hello app's UI.</span></span> <span data-ttu-id="d7e40-160">Deze methode maakt een get-aanvraag toohello Azure AD Graph API tooquery voor gebruikers wiens UPN met de Hallo zoekterm opgegeven begint.</span><span class="sxs-lookup"><span data-stu-id="d7e40-160">This method makes a get request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span> <span data-ttu-id="d7e40-161">tooquery hello Graph API een toegangstoken opnemen in Hallo-aanvraag **autorisatie** header.</span><span class="sxs-lookup"><span data-stu-id="d7e40-161">tooquery hello Graph API, include an access token in hello request's **Authorization** header.</span></span> <span data-ttu-id="d7e40-162">Dit is waar de ADAL wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="d7e40-162">This is where ADAL comes in.</span></span>

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="d7e40-163">Wanneer Hallo app een token aanvragen door het aanroepen van `AcquireTokenAsync(...)`, ADAL probeert een token tooreturn zonder Hallo gebruiker wordt gevraagd om referenties.</span><span class="sxs-lookup"><span data-stu-id="d7e40-163">When hello app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span> <span data-ttu-id="d7e40-164">Als ADAL dat die gebruiker Hallo moet toosign in een token tooget vaststelt, dit geeft een dialoogvenster aanmelden, verzamelt Hallo gebruikersreferenties en geeft aan dat een token na een verificatie geslaagde.</span><span class="sxs-lookup"><span data-stu-id="d7e40-164">If ADAL determines that hello user needs toosign in tooget a token, it displays a sign-in dialog box, collects hello user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="d7e40-165">Als ADAL niet kan tooreturn een token voor een bepaalde reden, Hallo *AuthenticationResult* status is een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="d7e40-165">If ADAL is unable tooreturn a token for any reason, hello *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="d7e40-166">Het is nu tijd toouse Hallo toegangstoken die u zojuist hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="d7e40-166">Now it's time toouse hello access token you just acquired.</span></span> <span data-ttu-id="d7e40-167">Ook in Hallo `Search(...)` methode koppelen Hallo token toohello Graph API aanvraag ophalen in Hallo **autorisatie** header:</span><span class="sxs-lookup"><span data-stu-id="d7e40-167">Also in hello `Search(...)` method, attach hello token toohello Graph API get request in hello **Authorization** header:</span></span>

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="d7e40-168">U kunt Hallo `AuthenticationResult` object toodisplay informatie over het Hallo-gebruiker in het Hallo-app, zoals Hallo gebruikersnaam:</span><span class="sxs-lookup"><span data-stu-id="d7e40-168">You can use hello `AuthenticationResult` object toodisplay information about hello user in hello app, such as hello user's ID:</span></span>

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="d7e40-169">U kunt ook ADAL toosign gebruikers buiten de Hallo app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d7e40-169">You can also use ADAL toosign users out of hello app.</span></span> <span data-ttu-id="d7e40-170">Wanneer Hallo gebruiker Hallo **Afmelden** knop, moet u zorgen dat Hallo volgende oproep te`AcquireTokenAsync(...)` ziet u een weergave aanmelden.</span><span class="sxs-lookup"><span data-stu-id="d7e40-170">When hello user clicks hello **Sign Out** button, ensure that hello next call too`AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="d7e40-171">Deze actie is met ADAL, net zo eenvoudig als het token Hallo-cache wissen:</span><span class="sxs-lookup"><span data-stu-id="d7e40-171">With ADAL, this action is as easy as clearing hello token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="d7e40-172">Volgend onderwerp</span><span class="sxs-lookup"><span data-stu-id="d7e40-172">What's next</span></span>
<span data-ttu-id="d7e40-173">U hebt nu een werkende Windows Store-app die u kunt verificatie van gebruikers, veilig aanroepen van web-API's met behulp van OAuth 2.0 en basisinformatie over Hallo gebruiker ophalen.</span><span class="sxs-lookup"><span data-stu-id="d7e40-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about hello user.</span></span>

<span data-ttu-id="d7e40-174">Als u al uw tenant met gebruikers nog niet hebt ingevuld, is nu Hallo tijd toodo dus.</span><span class="sxs-lookup"><span data-stu-id="d7e40-174">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>
1. <span data-ttu-id="d7e40-175">Uitvoeren van uw app DirectorySearcher en meld u aan met een van de gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="d7e40-175">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="d7e40-176">Zoeken naar andere gebruikers op basis van de UPN.</span><span class="sxs-lookup"><span data-stu-id="d7e40-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="d7e40-177">Hallo-app sluiten en opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="d7e40-177">Close hello app, and rerun it.</span></span> <span data-ttu-id="d7e40-178">U ziet hoe Hallo gebruikerssessie blijft intact.</span><span class="sxs-lookup"><span data-stu-id="d7e40-178">Notice how hello user’s session remains intact.</span></span>
4. <span data-ttu-id="d7e40-179">Met de rechtermuisknop op de balk onderaan van toodisplay Hallo afmelden en vervolgens weer aanmelden als een andere gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d7e40-179">Sign out by right-clicking toodisplay hello bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="d7e40-180">ADAL maakt het eenvoudig tooincorporate deze algemene identiteit functies in Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="d7e40-180">ADAL makes it easy tooincorporate all these common identity features into hello app.</span></span> <span data-ttu-id="d7e40-181">Zorgt het voor alle Hallo dirty werk voor u, zoals Cachebeheer, OAuth-protocolondersteuning, presenteren Hallo-gebruiker met een aanmelding-gebruikersinterface en vernieuwen van tokens verlopen.</span><span class="sxs-lookup"><span data-stu-id="d7e40-181">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="d7e40-182">U moet tooknow één API-aanroep `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="d7e40-182">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="d7e40-183">Ter referentie: downloaden Hallo [voltooide voorbeeld](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (zonder uw configuratiewaarden).</span><span class="sxs-lookup"><span data-stu-id="d7e40-183">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="d7e40-184">U kunt nu verplaatsen op tooadditional identity-scenario's.</span><span class="sxs-lookup"><span data-stu-id="d7e40-184">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="d7e40-185">Probeer bijvoorbeeld [beveiligen van een .NET-Web-API met Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="d7e40-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
