---
title: aaaAzure Active Directory B2C | Microsoft Docs
description: Hoe toobuild een Windows-bureaubladtoepassingen die bevat aanmelding, registratie en beheer met behulp van Azure Active Directory B2C-profiel.
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9da14362-8216-4485-960e-af17cd5ba3bd
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: f22b0299ff74bfba2f3fea88f006da609859dda5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="ce07e-103">Azure AD B2C: Een Windows desktop app bouwen</span><span class="sxs-lookup"><span data-stu-id="ce07e-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="ce07e-104">U kunt met behulp van Azure Active Directory (Azure AD) B2C bureaublad tooyour-app van de krachtige Self-service identiteitsbeheer management-functies toevoegen in slechts enkele korte stappen.</span><span class="sxs-lookup"><span data-stu-id="ce07e-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features tooyour desktop app in a few short steps.</span></span> <span data-ttu-id="ce07e-105">In dit artikel wordt uitgelegd hoe u toocreate een 'Takenlijst'.NET Windows Presentation Foundation (WPF)-app die gebruikersregistratie, aanmelding en Profielbeheer bevat.</span><span class="sxs-lookup"><span data-stu-id="ce07e-105">This article will show you how toocreate a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="ce07e-106">Hallo-app biedt ondersteuning voor zich kunnen registreren en aanmelden met een gebruikersnaam of e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="ce07e-106">hello app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="ce07e-107">Het biedt ook ondersteuning voor zich kunnen registreren en aanmelden via sociale accounts zoals Facebook en Google.</span><span class="sxs-lookup"><span data-stu-id="ce07e-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="ce07e-108">Een Azure AD B2C-directory maken</span><span class="sxs-lookup"><span data-stu-id="ce07e-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="ce07e-109">Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken.</span><span class="sxs-lookup"><span data-stu-id="ce07e-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="ce07e-110">Een directory is een container voor alle gebruikers, apps, groepen en meer.</span><span class="sxs-lookup"><span data-stu-id="ce07e-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="ce07e-111">Als u nog geen directory hebt, [maakt u een B2C-directory](active-directory-b2c-get-started.md) voordat u doorgaat in deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="ce07e-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="ce07e-112">Een app maken</span><span class="sxs-lookup"><span data-stu-id="ce07e-112">Create an application</span></span>
<span data-ttu-id="ce07e-113">Vervolgens moet u een app toocreate in uw B2C-directory.</span><span class="sxs-lookup"><span data-stu-id="ce07e-113">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="ce07e-114">Hiermee geeft u Azure AD-informatie of deze behoeften toosecurely met uw app communiceren.</span><span class="sxs-lookup"><span data-stu-id="ce07e-114">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="ce07e-115">toocreate een app, volg [deze instructies](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="ce07e-115">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="ce07e-116">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="ce07e-116">Be sure to:</span></span>

* <span data-ttu-id="ce07e-117">Omvatten een **native client** in Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ce07e-117">Include a **native client** in hello application.</span></span>
* <span data-ttu-id="ce07e-118">Kopiëren Hallo **omleidings-URI** `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="ce07e-118">Copy hello **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="ce07e-119">Het is Hallo-standaard-URL voor dit codevoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ce07e-119">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="ce07e-120">Kopiëren Hallo **toepassings-ID** is toegewezen tooyour app.</span><span class="sxs-lookup"><span data-stu-id="ce07e-120">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="ce07e-121">U hebt dit later nodig.</span><span class="sxs-lookup"><span data-stu-id="ce07e-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="ce07e-122">Het beleid maken</span><span class="sxs-lookup"><span data-stu-id="ce07e-122">Create your policies</span></span>
<span data-ttu-id="ce07e-123">In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="ce07e-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="ce07e-124">Dit codevoorbeeld bevat drie identiteitservaringen: registreren, aanmelden en profiel bewerken.</span><span class="sxs-lookup"><span data-stu-id="ce07e-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="ce07e-125">U moet toocreate een beleid voor elk type, zoals beschreven in de [naslagartikel](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="ce07e-125">You need toocreate a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="ce07e-126">Wanneer u Hallo drie beleidsregels maakt, moet u:</span><span class="sxs-lookup"><span data-stu-id="ce07e-126">When you create hello three policies, be sure to:</span></span>

* <span data-ttu-id="ce07e-127">Kies een **gebruikers-ID registreren** of **registratie via E-mail** in de blade met identiteitsproviders Hallo.</span><span class="sxs-lookup"><span data-stu-id="ce07e-127">Choose either **User ID sign-up** or **Email sign-up** in hello identity providers blade.</span></span>
* <span data-ttu-id="ce07e-128">Kiest u **Weergavenaam** en andere registratiekenmerken in het registratiebeleid.</span><span class="sxs-lookup"><span data-stu-id="ce07e-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="ce07e-129">Kiest u **Weergavenaam**- en **Object-id**-claims als toepassingsclaims voor elk beleid.</span><span class="sxs-lookup"><span data-stu-id="ce07e-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="ce07e-130">U kunt ook andere claims kiezen.</span><span class="sxs-lookup"><span data-stu-id="ce07e-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="ce07e-131">Kopiëren Hallo **naam** van elk beleid nadat u dit hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ce07e-131">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="ce07e-132">Het voorvoegsel Hallo heeft `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="ce07e-132">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="ce07e-133">U hebt deze beleidsnamen later nodig.</span><span class="sxs-lookup"><span data-stu-id="ce07e-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="ce07e-134">Wanneer u hebt gemaakt Hallo drie beleidsregels, bent u klaar toobuild uw app.</span><span class="sxs-lookup"><span data-stu-id="ce07e-134">After you have successfully created hello three policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="ce07e-135">Hallo code downloaden</span><span class="sxs-lookup"><span data-stu-id="ce07e-135">Download hello code</span></span>
<span data-ttu-id="ce07e-136">code voor deze zelfstudie Hallo [wordt bewaard in GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="ce07e-136">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="ce07e-137">toobuild hello voorbeeld als u gaat, kunt u [een basisproject downloaden als ZIP-bestand](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="ce07e-137">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="ce07e-138">U kunt Hallo basisproject ook klonen:</span><span class="sxs-lookup"><span data-stu-id="ce07e-138">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="ce07e-139">Hallo voltooid app is ook [beschikbaar als ZIP-bestand](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) of op Hallo `complete` vertakking van Hallo dezelfde opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="ce07e-139">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

<span data-ttu-id="ce07e-140">Nadat u Hallo voorbeeldcode hebt gedownload, open Hallo Visual Studio .sln-bestand tooget is gestart.</span><span class="sxs-lookup"><span data-stu-id="ce07e-140">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="ce07e-141">Hallo `TaskClient` project is Hallo WPF-bureaubladtoepassing die gebruiker Hallo communiceert met.</span><span class="sxs-lookup"><span data-stu-id="ce07e-141">hello `TaskClient` project is hello WPF desktop application that hello user interacts with.</span></span> <span data-ttu-id="ce07e-142">Aangeroepen voor Hallo toepassing van deze zelfstudie wordt een taak back-end-web-API, gehost in Azure die de takenlijst van elke gebruiker opslaat.</span><span class="sxs-lookup"><span data-stu-id="ce07e-142">For hello purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="ce07e-143">U hoeft geen toobuild Hallo web-API, we hebben al actief voor u.</span><span class="sxs-lookup"><span data-stu-id="ce07e-143">You do not need toobuild hello web API, we already have it running for you.</span></span>

<span data-ttu-id="ce07e-144">toolearn hoe aanvragen voor een web-API veilig verifieert met behulp van Azure AD B2C, bekijk de [web-API aan de slag artikel](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="ce07e-144">toolearn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="ce07e-145">Uitvoeren van beleid</span><span class="sxs-lookup"><span data-stu-id="ce07e-145">Execute policies</span></span>
<span data-ttu-id="ce07e-146">Uw app communiceert met Azure AD B2C door te sturen verificatieberichten die ze willen tooexecute als onderdeel van Hallo HTTP-aanvraag Hallo het beleid opgeven.</span><span class="sxs-lookup"><span data-stu-id="ce07e-146">Your app communicates with Azure AD B2C by sending authentication messages that specify hello policy they want tooexecute as part of hello HTTP request.</span></span> <span data-ttu-id="ce07e-147">Voor .NET-desktoptoepassingen, kunt u Hallo Microsoft Authentication Library (MSAL) toosend OAuth 2.0-verificatieberichten bekijken, beleid uitvoeren en tokens verkrijgen voor de web-API's van deze aanroep.</span><span class="sxs-lookup"><span data-stu-id="ce07e-147">For .NET desktop applications, you can use hello preview Microsoft Authentication Library (MSAL) toosend OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="ce07e-148">MSAL installeren</span><span class="sxs-lookup"><span data-stu-id="ce07e-148">Install MSAL</span></span>
<span data-ttu-id="ce07e-149">Toevoegen van MSAL toohello `TaskClient` project met behulp van Hallo Visual Studio Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="ce07e-149">Add MSAL toohello `TaskClient` project by using hello Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="ce07e-150">Uw B2C-gegevens invoeren</span><span class="sxs-lookup"><span data-stu-id="ce07e-150">Enter your B2C details</span></span>
<span data-ttu-id="ce07e-151">Open Hallo bestand `Globals.cs` en elk Hallo eigenschapswaarden vervangen door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="ce07e-151">Open hello file `Globals.cs` and replace each of hello property values with your own.</span></span> <span data-ttu-id="ce07e-152">Deze klasse wordt gebruikt in `TaskClient` tooreference gebruikte waarden.</span><span class="sxs-lookup"><span data-stu-id="ce07e-152">This class is used throughout `TaskClient` tooreference commonly used values.</span></span>

```C#
public static class Globals
{
    ...

    // TODO: Replace these five default with your own configuration values
    public static string tenant = "fabrikamb2c.onmicrosoft.com";
    public static string clientId = "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6";
    public static string signInPolicy = "b2c_1_sign_in";
    public static string signUpPolicy = "b2c_1_sign_up";
    public static string editProfilePolicy = "b2c_1_edit_profile";

    ...
}
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="create-hello-publicclientapplication"></a><span data-ttu-id="ce07e-153">Hallo PublicClientApplication maken</span><span class="sxs-lookup"><span data-stu-id="ce07e-153">Create hello PublicClientApplication</span></span>
<span data-ttu-id="ce07e-154">de primaire klasse Hallo van MSAL is `PublicClientApplication`.</span><span class="sxs-lookup"><span data-stu-id="ce07e-154">hello primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="ce07e-155">Deze klasse vertegenwoordigt de toepassing in Azure AD B2C Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="ce07e-155">This class represents your application in hello Azure AD B2C system.</span></span> <span data-ttu-id="ce07e-156">Wanneer hello app initalizes, maak een instantie van `PublicClientApplication` in `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="ce07e-156">When hello app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="ce07e-157">Dit kan worden gebruikt in de gehele Hallo-venster.</span><span class="sxs-lookup"><span data-stu-id="ce07e-157">This can be used throughout hello window.</span></span>

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens toopersist when hello user closes hello app,
        // we've extended hello MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="ce07e-158">Een registratie stroom initiëren</span><span class="sxs-lookup"><span data-stu-id="ce07e-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="ce07e-159">Wanneer een gebruiker toosigns up kiest, wilt u tooinitiate een aanmelding stroom die gebruikmaakt van Hallo registratiebeleid die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ce07e-159">When a user opts toosigns up, you want tooinitiate a sign-up flow that uses hello sign-up policy you created.</span></span> <span data-ttu-id="ce07e-160">Met behulp van MSAL die u zojuist hebt aanroepen `pca.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="ce07e-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="ce07e-161">parameters die u te doorgeeft Hallo`AcquireTokenAsync(...)` bepalen welk token wordt weergegeven, Hallo-beleid gebruikt in de verificatieaanvraag Hallo en meer.</span><span class="sxs-lookup"><span data-stu-id="ce07e-161">hello parameters you pass too`AcquireTokenAsync(...)` determine which token you receive, hello policy used in hello authentication request, and more.</span></span>

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use hello app's clientId here as hello scope parameter, indicating that
        // you want a token toohello your app's backend web API (represented by
        // hello cloud hosted task API).  Use hello UiOptions.ForceLogin flag to
        // indicate tooMSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in hello app that hello user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When hello request completes successfully, you can get user
        // information from hello AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After hello sign up successfully completes, display hello user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of hello policy.
    catch (MsalException ex)
    {
        if (ex.ErrorCode != "authentication_canceled")
        {
            // An unexpected error occurred.
            string message = ex.Message;
            if (ex.InnerException != null)
            {
                message += "Inner Exception : " + ex.InnerException.Message;
            }

            MessageBox.Show(message);
        }

        return;
    }
}
```

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="ce07e-162">Starten van een stroom aanmelden</span><span class="sxs-lookup"><span data-stu-id="ce07e-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="ce07e-163">U kunt een stroom aanmelden in Hallo starten dezelfde manier als dat u een aanmelding stroom initiëren.</span><span class="sxs-lookup"><span data-stu-id="ce07e-163">You can initiate a sign-in flow in hello same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="ce07e-164">Wanneer een gebruiker zich aanmeldt, moet dezelfde Hallo aanroepen tooMSAL, ditmaal met behulp van uw beleid voor aanmelden:</span><span class="sxs-lookup"><span data-stu-id="ce07e-164">When a user signs in, make hello same call tooMSAL, this time by using your sign-in policy:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.signInPolicy);
        ...
```

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="ce07e-165">Starten van een stroom profiel bewerken</span><span class="sxs-lookup"><span data-stu-id="ce07e-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="ce07e-166">Opnieuw uitvoeren van een beleid voor het profiel bewerken in Hallo dezelfde manier:</span><span class="sxs-lookup"><span data-stu-id="ce07e-166">Again, you can execute an edit-profile policy in hello same fashion:</span></span>

```C#
private async void EditProfile(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.editProfilePolicy);
```

<span data-ttu-id="ce07e-167">In al deze gevallen retourneert MSAL ofwel een token in `AuthenticationResult` of er een uitzondering gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="ce07e-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="ce07e-168">Telkens wanneer u een token via MSAL krijgen, kunt u Hallo `AuthenticationResult.User` tooupdate Hallo gebruikersgegevens in Hallo-app, zoals Hallo UI-object.</span><span class="sxs-lookup"><span data-stu-id="ce07e-168">Each time you get a token from MSAL, you can use hello `AuthenticationResult.User` object tooupdate hello user data in hello app, such as hello UI.</span></span> <span data-ttu-id="ce07e-169">ADAL ook caches Hallo token voor gebruik in andere gedeelten van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="ce07e-169">ADAL also caches hello token for use in other parts of hello application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="ce07e-170">Controleer voor tokens op app starten</span><span class="sxs-lookup"><span data-stu-id="ce07e-170">Check for tokens on app start</span></span>
<span data-ttu-id="ce07e-171">U kunt ook MSAL tookeep bijhouden van Hallo aanmelden gebruikersstatus gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ce07e-171">You can also use MSAL tookeep track of hello user's sign-in state.</span></span>  <span data-ttu-id="ce07e-172">In deze app willen we Hallo gebruiker tooremain aangemeld nadat ze Hallo-app sluiten en opnieuw openen.</span><span class="sxs-lookup"><span data-stu-id="ce07e-172">In this app, we want hello user tooremain signed in even after they close hello app & re-open it.</span></span>  <span data-ttu-id="ce07e-173">Terug in Hallo `OnInitialized` overschrijven, gebruikt u de MSAL `AcquireTokenSilent` methode toocheck voor tokens in de cache:</span><span class="sxs-lookup"><span data-stu-id="ce07e-173">Back inside hello `OnInitialized` override, use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

```C#
AuthenticationResult result = null;
try
{
    // If hello user has has a token cached with any policy, we'll display them as signed-in.
    TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
    string existingPolicy = tci == null ? null : tci.Policy;
    result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    SignInButton.Visibility = Visibility.Collapsed;
    SignUpButton.Visibility = Visibility.Collapsed;
    EditProfileButton.Visibility = Visibility.Visible;
    SignOutButton.Visibility = Visibility.Visible;
    UsernameLabel.Content = result.User.Name;
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "failed_to_acquire_token_silently")
    {
        // There are no tokens in hello cache.  Proceed without calling hello tooDo list service.
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
    return;
}
```

## <a name="call-hello-task-api"></a><span data-ttu-id="ce07e-174">Hallo taak API aanroepen</span><span class="sxs-lookup"><span data-stu-id="ce07e-174">Call hello task API</span></span>
<span data-ttu-id="ce07e-175">U hebt nu MSAL tooexecute beleidsregels gebruikt en tokens verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="ce07e-175">You have now used MSAL tooexecute policies and get tokens.</span></span>  <span data-ttu-id="ce07e-176">Wanneer u toouse een deze tokens toocall Hallo taak API wilt, kunt u opnieuw gebruiken van MSAL `AcquireTokenSilent` methode toocheck voor tokens in de cache:</span><span class="sxs-lookup"><span data-stu-id="ce07e-176">When you want toouse one these tokens toocall hello task API, you can again use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want toocheck for a cached token, independent of whatever policy was used tooacquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent tooindicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch hello exception and show hello user a message.
    catch (MsalException ex)
    {
        // There is no access token in hello cache, so prompt hello user toosign-in.
        if (ex.ErrorCode == "failed_to_acquire_token_silently")
        {
            MessageBox.Show("Please sign up or sign in first");
            SignInButton.Visibility = Visibility.Visible;
            SignUpButton.Visibility = Visibility.Visible;
            EditProfileButton.Visibility = Visibility.Collapsed;
            SignOutButton.Visibility = Visibility.Collapsed;
            UsernameLabel.Content = string.Empty;
        }
        else
        {
            // An unexpected error occurred.
            string message = ex.Message;
            if (ex.InnerException != null)
            {
                message += "Inner Exception : " + ex.InnerException.Message;
            }
            MessageBox.Show(message);
        }

        return;
    }
    ...
```

<span data-ttu-id="ce07e-177">Wanneer de aanroep te Hallo`AcquireTokenSilentAsync(...)` is gelukt en een token gevonden in cache hello, kunt u Hallo token toohello toevoegen `Authorization` koptekst van Hallo HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="ce07e-177">When hello call too`AcquireTokenSilentAsync(...)` succeeds and a token is found in hello cache, you can add hello token toohello `Authorization` header of hello HTTP request.</span></span> <span data-ttu-id="ce07e-178">Hallo taak web-API gebruikt deze header tooauthenticate Hallo aanvraag tooread Hallo de takenlijst gebruiker:</span><span class="sxs-lookup"><span data-stu-id="ce07e-178">hello task web API will use this header tooauthenticate hello request tooread hello user's to-do list:</span></span>

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a><span data-ttu-id="ce07e-179">Meld u Hallo gebruiker af</span><span class="sxs-lookup"><span data-stu-id="ce07e-179">Sign hello user out</span></span>
<span data-ttu-id="ce07e-180">Ten slotte kunt u MSAL tooend een gebruikerssessie met Hallo app wanneer de gebruiker Hallo selecteert **Afmelden**.  Wanneer u MSAL gebruikt, wordt dit wordt bereikt door het wissen van alle Hallo tokens van Hallo tokencache:</span><span class="sxs-lookup"><span data-stu-id="ce07e-180">Finally, you can use MSAL tooend a user's session with hello app when hello user selects **Sign out**.  When using MSAL, this is accomplished by clearing all of hello tokens from hello token cache:</span></span>

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of hello user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in hello browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update hello UI tooshow hello user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="ce07e-181">Hallo voorbeeld-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ce07e-181">Run hello sample app</span></span>
<span data-ttu-id="ce07e-182">Ten slotte bouwen en uitvoeren van Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ce07e-182">Finally, build and run hello sample.</span></span>  <span data-ttu-id="ce07e-183">Zich registreren voor Hallo-app met behulp van de naam van een e-adres of de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ce07e-183">Sign up for hello app by using an email address or user name.</span></span> <span data-ttu-id="ce07e-184">Meld u af en meld u weer aan als Hallo dezelfde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ce07e-184">Sign out and sign back in as hello same user.</span></span> <span data-ttu-id="ce07e-185">Profiel van de gebruiker bewerken.</span><span class="sxs-lookup"><span data-stu-id="ce07e-185">Edit that user's profile.</span></span> <span data-ttu-id="ce07e-186">Meld u af en meld u aan met behulp van een andere gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ce07e-186">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="ce07e-187">Sociale IDPs toevoegen</span><span class="sxs-lookup"><span data-stu-id="ce07e-187">Add social IDPs</span></span>
<span data-ttu-id="ce07e-188">Op dit moment Hallo app ondersteunt alleen gebruiker registreren en aanmelden met **lokale accounts**.</span><span class="sxs-lookup"><span data-stu-id="ce07e-188">Currently, hello app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="ce07e-189">Dit zijn opgeslagen in uw B2C-directory accounts die gebruikmaken van een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ce07e-189">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="ce07e-190">U kunt met behulp van Azure AD B2C, ondersteuning voor andere id-providers (IDPs) toevoegen zonder uw code.</span><span class="sxs-lookup"><span data-stu-id="ce07e-190">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="ce07e-191">tooadd sociale IDPs tooyour app volg eerst Hallo gedetailleerde instructies in deze artikelen.</span><span class="sxs-lookup"><span data-stu-id="ce07e-191">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="ce07e-192">Voor elke IDP gewenste toosupport, u moet een toepassing tooregister in dat systeem en verkrijgen van een client-ID.</span><span class="sxs-lookup"><span data-stu-id="ce07e-192">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="ce07e-193">Facebook ingesteld als een IDP</span><span class="sxs-lookup"><span data-stu-id="ce07e-193">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="ce07e-194">Google ingesteld als een IDP</span><span class="sxs-lookup"><span data-stu-id="ce07e-194">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="ce07e-195">Amazon ingesteld als een IDP</span><span class="sxs-lookup"><span data-stu-id="ce07e-195">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="ce07e-196">LinkedIn instellen als een IDP</span><span class="sxs-lookup"><span data-stu-id="ce07e-196">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="ce07e-197">Nadat u Hallo identiteit providers tooyour B2C-directory toevoegt, moet u elk van de drie beleidsregels tooinclude Hallo nieuwe IDPs als in Hallo beschreven tooedit [naslagartikel](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="ce07e-197">After you add hello identity providers tooyour B2C directory, you need tooedit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="ce07e-198">Nadat u uw beleid opslaat, Voer u Hallo app opnieuw.</span><span class="sxs-lookup"><span data-stu-id="ce07e-198">After you save your policies, run hello app again.</span></span> <span data-ttu-id="ce07e-199">U ziet Hallo die nieuwe IDPs als opties voor aanmelden en registreren in elk van uw identiteitservaringen toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ce07e-199">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="ce07e-200">U kunt experimenteren met het beleid en observeren Hallo gevolgen voor uw voorbeeld-app.</span><span class="sxs-lookup"><span data-stu-id="ce07e-200">You can experiment with your policies and observe hello effects on your sample app.</span></span> <span data-ttu-id="ce07e-201">Toevoegen of verwijderen van IDPs, toepassingsclaims bewerken of registratiekenmerken wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ce07e-201">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="ce07e-202">Experiment totdat u kunt zien hoe beleidsregels, verificatieaanvragen en MSAL met elkaar verbinden.</span><span class="sxs-lookup"><span data-stu-id="ce07e-202">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="ce07e-203">Ter referentie: voltooid Hallo voorbeeld [wordt geleverd als ZIP-bestand](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="ce07e-203">For reference, hello completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="ce07e-204">U kunt dit ook klonen van GitHub:</span><span class="sxs-lookup"><span data-stu-id="ce07e-204">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
