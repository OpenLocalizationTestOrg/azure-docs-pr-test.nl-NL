---
title: Azure AD Windows Store aan de slag | Microsoft Docs
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
ms.openlocfilehash: 6b5189dc06d7f8b0ed4426944948b904feba847e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="6e7af-103">Azure AD integreren met Windows Store-apps</span><span class="sxs-lookup"><span data-stu-id="6e7af-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="6e7af-104">Windows Store 8.1 en projecten met een eerdere versie worden niet ondersteund in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="6e7af-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="6e7af-105">Zie [Geschikte platforms voor Visual Studio 2017 en compatibiliteit](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6e7af-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="6e7af-106">Als u apps voor de Windows Store ontwikkelt, kunt Azure Active Directory (Azure AD) u eenvoudig en snel om uw gebruikers met hun Active Directory-account te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="6e7af-106">If you're developing apps for the Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward to authenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="6e7af-107">Een app door te integreren met Azure AD, kan veilig een web-API die wordt beveiligd door Azure AD, zoals de Office 365-API of de Azure-API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6e7af-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="6e7af-108">Voor Windows Store-desktoptoepassingen die toegang moeten krijgen tot beveiligde bronnen, levert Azure AD de Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="6e7af-108">For Windows Store desktop apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="6e7af-109">Het enige doel van ADAL is gemakkelijker voor de app toegangstokens ophalen.</span><span class="sxs-lookup"><span data-stu-id="6e7af-109">The sole purpose of ADAL is to make it easy for the app to get access tokens.</span></span> <span data-ttu-id="6e7af-110">Als u wilt laten zien hoe eenvoudig het is, in dit artikel laat zien hoe DirectorySearcher Windows Store-Apps bouwen die:</span><span class="sxs-lookup"><span data-stu-id="6e7af-110">To demonstrate how easy it is, this article shows how to build a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="6e7af-111">Krijgt toegang tot tokens voor de Azure AD Graph-API aanroept met behulp van de [OAuth 2.0-verificatieprotocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="6e7af-111">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="6e7af-112">Zoekt een directory voor gebruikers met een opgegeven user principal name (UPN).</span><span class="sxs-lookup"><span data-stu-id="6e7af-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="6e7af-113">Tekenen gebruikers uit.</span><span class="sxs-lookup"><span data-stu-id="6e7af-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="6e7af-114">Voordat u aan de slag gaat</span><span class="sxs-lookup"><span data-stu-id="6e7af-114">Before you get started</span></span>
* <span data-ttu-id="6e7af-115">Download de [basisproject](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), of download de [voltooide voorbeeld](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="6e7af-115">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="6e7af-116">Elke download is een Visual Studio 2015-oplossing.</span><span class="sxs-lookup"><span data-stu-id="6e7af-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="6e7af-117">U moet ook een Azure AD-tenant waarin gebruikers maken en de app te registreren.</span><span class="sxs-lookup"><span data-stu-id="6e7af-117">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="6e7af-118">Als u niet al een tenant [Lees hoe u een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="6e7af-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="6e7af-119">Wanneer u klaar bent, voert u de procedures in de volgende drie secties.</span><span class="sxs-lookup"><span data-stu-id="6e7af-119">When you are ready, follow the procedures in the next three sections.</span></span>

## <a name="step-1-register-the-directorysearcher-app"></a><span data-ttu-id="6e7af-120">Stap 1: De app DirectorySearcher te registreren</span><span class="sxs-lookup"><span data-stu-id="6e7af-120">Step 1: Register the DirectorySearcher app</span></span>
<span data-ttu-id="6e7af-121">Als u wilt inschakelen voor de app tokens krijgen, moet u eerst registreren in uw Azure AD-tenant en verleent deze machtiging voor toegang tot de Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="6e7af-121">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="6e7af-122">Dit doet u al volgt:</span><span class="sxs-lookup"><span data-stu-id="6e7af-122">Here's how:</span></span>

1. <span data-ttu-id="6e7af-123">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6e7af-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6e7af-124">Klik op uw account op de bovenste balk.</span><span class="sxs-lookup"><span data-stu-id="6e7af-124">On the top bar, click your account.</span></span> <span data-ttu-id="6e7af-125">Klik vervolgens onder de **Directory** , selecteert u de Active Directory-tenant waar u de app te registreren.</span><span class="sxs-lookup"><span data-stu-id="6e7af-125">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="6e7af-126">Klik op **meer Services** in het linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6e7af-126">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="6e7af-127">Klik op **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6e7af-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="6e7af-128">Volg de aanwijzingen voor het maken van een **systeemeigen clienttoepassing**.</span><span class="sxs-lookup"><span data-stu-id="6e7af-128">Follow the prompts to create a **Native Client Application**.</span></span>
  * <span data-ttu-id="6e7af-129">**Naam** beschrijving van de app voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6e7af-129">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="6e7af-130">**Omleidings-URI** is een combinatie schema en de tekenreeks die gebruikmaakt van Azure AD token antwoorden retourneren.</span><span class="sxs-lookup"><span data-stu-id="6e7af-130">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="6e7af-131">Voer een aanduidingswaarde van de tijdelijke voor nu (bijvoorbeeld **http://DirectorySearcher**).</span><span class="sxs-lookup"><span data-stu-id="6e7af-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="6e7af-132">U moet de waarde later vervangen.</span><span class="sxs-lookup"><span data-stu-id="6e7af-132">You'll replace the value later.</span></span>
6. <span data-ttu-id="6e7af-133">Nadat u de registratie hebt voltooid, wijst Azure AD de app een unieke toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="6e7af-133">After you’ve completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="6e7af-134">Kopieer de waarde op de **toepassing** tabblad omdat u hebt deze later nodig.</span><span class="sxs-lookup"><span data-stu-id="6e7af-134">Copy the value on the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="6e7af-135">Op de **instellingen** pagina **Required Permissions**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6e7af-135">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="6e7af-136">Voor de **Azure Active Directory** app, selecteer **Microsoft Graph** als de API.</span><span class="sxs-lookup"><span data-stu-id="6e7af-136">For the **Azure Active Directory** app, select **Microsoft Graph** as the API.</span></span>
9. <span data-ttu-id="6e7af-137">Onder **gedelegeerde machtigingen**, voeg de **toegang tot de map als de gebruiker is aangemeld** machtiging.</span><span class="sxs-lookup"><span data-stu-id="6e7af-137">Under **Delegated Permissions**, add the **Access the directory as the signed-in user** permission.</span></span> <span data-ttu-id="6e7af-138">In dat geval kan de app om op te vragen de Graph-API voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6e7af-138">Doing so enables the app to query the Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="6e7af-139">Stap 2: Installeren en configureren van ADAL</span><span class="sxs-lookup"><span data-stu-id="6e7af-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="6e7af-140">Nu dat u een app in Azure AD hebt, kunt u ADAL installeert en uw identiteitsgerelateerde code schrijven.</span><span class="sxs-lookup"><span data-stu-id="6e7af-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="6e7af-141">Om in te schakelen ADAL om te communiceren met Azure AD, geef deze de enige informatie over de registratie van de app.</span><span class="sxs-lookup"><span data-stu-id="6e7af-141">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="6e7af-142">ADAL toevoegen aan het project DirectorySearcher met behulp van de Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="6e7af-142">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="6e7af-143">Open in het project DirectorySearcher MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="6e7af-143">In the DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="6e7af-144">Vervang de waarden in de **configuratiewaarden** regio met de waarden die u hebt ingevoerd in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6e7af-144">Replace the values in the **Config Values** region with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="6e7af-145">Uw code verwijst naar deze waarden wanneer deze gebruikmaakt van ADAL.</span><span class="sxs-lookup"><span data-stu-id="6e7af-145">Your code refers to these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="6e7af-146">De *tenant* is het domein van uw Azure AD-tenant (bijvoorbeeld: contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="6e7af-146">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="6e7af-147">De *clientId* is de client-ID van de app, die u hebt gekopieerd uit de portal.</span><span class="sxs-lookup"><span data-stu-id="6e7af-147">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
4. <span data-ttu-id="6e7af-148">U moet nu voor het detecteren van de callback-URI voor uw Windows Store-app.</span><span class="sxs-lookup"><span data-stu-id="6e7af-148">You now need to discover the callback URI for your Windows Store app.</span></span> <span data-ttu-id="6e7af-149">Stel een onderbrekingspunt in op deze regel in de `MainPage` methode:</span><span class="sxs-lookup"><span data-stu-id="6e7af-149">Set a breakpoint on this line in the `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="6e7af-150">Bouw de oplossing, om ervoor te zorgen dat alle pakket-verwijzingen zijn hersteld.</span><span class="sxs-lookup"><span data-stu-id="6e7af-150">Build the solution, making sure that all package references are restored.</span></span> <span data-ttu-id="6e7af-151">Als er pakketten ontbreken, opent u NuGet Package Manager en deze terugzetten.</span><span class="sxs-lookup"><span data-stu-id="6e7af-151">If any packages are missing, open the NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="6e7af-152">Voer de app en kopieer de waarde van `redirectUri` wanneer het onderbrekingspunt is bereikt.</span><span class="sxs-lookup"><span data-stu-id="6e7af-152">Run the app, and copy the value of `redirectUri` when the breakpoint is hit.</span></span> <span data-ttu-id="6e7af-153">De waarde moet er ongeveer als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="6e7af-153">The value should look something like the following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="6e7af-154">Terug op de **instellingen** tabblad toevoegen van de app in de Azure portal een **RedirectUri** met de vorige waarde.</span><span class="sxs-lookup"><span data-stu-id="6e7af-154">Back on the **Settings** tab of the app in the Azure portal, add a **RedirectUri** with the preceding value.</span></span>  

## <a name="step-3-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="6e7af-155">Stap 3: Gebruik ADAL tokens ophalen uit Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e7af-155">Step 3: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="6e7af-156">Het basisprincipe achter ADAL is dat wanneer de app een toegangstoken moet, aanroept `authContext.AcquireToken(…)`, en doet de rest van ADAL.</span><span class="sxs-lookup"><span data-stu-id="6e7af-156">The basic principle behind ADAL is that whenever the app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="6e7af-157">Initialiseren van de app `AuthenticationContext`, dit is de primaire klasse van ADAL.</span><span class="sxs-lookup"><span data-stu-id="6e7af-157">Initialize the app’s `AuthenticationContext`, which is the primary class of ADAL.</span></span> <span data-ttu-id="6e7af-158">Deze actie geeft ADAL de coördinaten nodig om te communiceren met Azure AD en hoe deze tokens in de cache.</span><span class="sxs-lookup"><span data-stu-id="6e7af-158">This action passes ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="6e7af-159">Zoek de `Search(...)` methode die wordt opgeroepen wanneer gebruikers op de **Search** knop op de gebruikersinterface van de app.</span><span class="sxs-lookup"><span data-stu-id="6e7af-159">Locate the `Search(...)` method, which is invoked when users click the **Search** button on the app's UI.</span></span> <span data-ttu-id="6e7af-160">Deze methode maakt een get-aanvraag voor Azure AD Graph API aan query voor gebruikers wiens UPN met de opgegeven zoekterm begint.</span><span class="sxs-lookup"><span data-stu-id="6e7af-160">This method makes a get request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span> <span data-ttu-id="6e7af-161">Om te vragen de Graph API, een toegangstoken in de aanvraag opnemen **autorisatie** header.</span><span class="sxs-lookup"><span data-stu-id="6e7af-161">To query the Graph API, include an access token in the request's **Authorization** header.</span></span> <span data-ttu-id="6e7af-162">Dit is waar de ADAL wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="6e7af-162">This is where ADAL comes in.</span></span>

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
                ShowAuthError(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="6e7af-163">Wanneer de app een token aanvragen door het aanroepen van `AcquireTokenAsync(...)`, ADAL probeert te retourneren van een token zonder dat de gebruiker om referenties gevraagd.</span><span class="sxs-lookup"><span data-stu-id="6e7af-163">When the app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span> <span data-ttu-id="6e7af-164">Als ADAL wordt vastgesteld dat de gebruiker zich aanmelden moet bij een token verkrijgen, het geeft een dialoogvenster aanmelden, verzamelt de referenties van de gebruiker en geeft aan dat een token na een verificatie geslaagde.</span><span class="sxs-lookup"><span data-stu-id="6e7af-164">If ADAL determines that the user needs to sign in to get a token, it displays a sign-in dialog box, collects the user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="6e7af-165">Als ADAL kunnen niet worden geretourneerd van een token voor een of andere reden is de *AuthenticationResult* status is een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="6e7af-165">If ADAL is unable to return a token for any reason, the *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="6e7af-166">Nu is het tijd om het gebruik van het toegangstoken dat u zojuist hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="6e7af-166">Now it's time to use the access token you just acquired.</span></span> <span data-ttu-id="6e7af-167">Ook in de `Search(...)` methode, het token koppelen aan de Graph API get-aanvraag in de **autorisatie** header:</span><span class="sxs-lookup"><span data-stu-id="6e7af-167">Also in the `Search(...)` method, attach the token to the Graph API get request in the **Authorization** header:</span></span>

    ```C#
    // Add the access token to the Authorization header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="6e7af-168">U kunt de `AuthenticationResult` object om informatie over de gebruiker in de app, zoals ID van de gebruiker weer te geven:</span><span class="sxs-lookup"><span data-stu-id="6e7af-168">You can use the `AuthenticationResult` object to display information about the user in the app, such as the user's ID:</span></span>

    ```C#
    // Update the page UI to represent the signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="6e7af-169">U kunt ook ADAL voor het ondertekenen van gebruikers buiten de app.</span><span class="sxs-lookup"><span data-stu-id="6e7af-169">You can also use ADAL to sign users out of the app.</span></span> <span data-ttu-id="6e7af-170">Wanneer de gebruiker klikt op de **Afmelden** knop, zorg ervoor dat de volgende aanroep `AcquireTokenAsync(...)` ziet u een weergave aanmelden.</span><span class="sxs-lookup"><span data-stu-id="6e7af-170">When the user clicks the **Sign Out** button, ensure that the next call to `AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="6e7af-171">Deze actie is met ADAL, net zo eenvoudig als het token cache wissen:</span><span class="sxs-lookup"><span data-stu-id="6e7af-171">With ADAL, this action is as easy as clearing the token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from the token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="6e7af-172">Volgend onderwerp</span><span class="sxs-lookup"><span data-stu-id="6e7af-172">What's next</span></span>
<span data-ttu-id="6e7af-173">U hebt nu een werkende Windows Store-app die u kunt verificatie van gebruikers, veilig aanroepen van web-API's met behulp van OAuth 2.0 en algemene informatie over de gebruiker ophalen.</span><span class="sxs-lookup"><span data-stu-id="6e7af-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about the user.</span></span>

<span data-ttu-id="6e7af-174">Als u al uw tenant met gebruikers nog niet hebt ingevuld, is nu tijd om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="6e7af-174">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>
1. <span data-ttu-id="6e7af-175">Uitvoeren van uw app DirectorySearcher en meld u aan met een van de gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6e7af-175">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="6e7af-176">Zoeken naar andere gebruikers op basis van de UPN.</span><span class="sxs-lookup"><span data-stu-id="6e7af-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="6e7af-177">De toepassing sluiten en opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="6e7af-177">Close the app, and rerun it.</span></span> <span data-ttu-id="6e7af-178">U ziet hoe de gebruikerssessie blijft intact.</span><span class="sxs-lookup"><span data-stu-id="6e7af-178">Notice how the user’s session remains intact.</span></span>
4. <span data-ttu-id="6e7af-179">Meld u af met de rechtermuisknop op de balk onderaan weergeven en vervolgens weer aanmelden als een andere gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6e7af-179">Sign out by right-clicking to display the bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="6e7af-180">ADAL kunt eenvoudig deze algemene identiteit functies opnemen in de app.</span><span class="sxs-lookup"><span data-stu-id="6e7af-180">ADAL makes it easy to incorporate all these common identity features into the app.</span></span> <span data-ttu-id="6e7af-181">Zorgt het alle dirty werk voor u, zoals Cachebeheer, OAuth-protocolondersteuning, dat de gebruiker een aanmelding-gebruikersinterface en vernieuwen van tokens verlopen.</span><span class="sxs-lookup"><span data-stu-id="6e7af-181">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="6e7af-182">U moet weten slechts één API-aanroep, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="6e7af-182">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="6e7af-183">Ter referentie: download de [voltooide voorbeeld](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (zonder uw configuratiewaarden).</span><span class="sxs-lookup"><span data-stu-id="6e7af-183">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="6e7af-184">U kunt nu verder met de identiteit van de aanvullende scenario's.</span><span class="sxs-lookup"><span data-stu-id="6e7af-184">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="6e7af-185">Probeer bijvoorbeeld [beveiligen van een .NET-Web-API met Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="6e7af-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
