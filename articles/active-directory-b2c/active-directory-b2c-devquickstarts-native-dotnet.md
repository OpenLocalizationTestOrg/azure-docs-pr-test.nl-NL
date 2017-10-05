---
title: Azure Active Directory B2C | Microsoft Docs
description: Het bouwen van een Windows-bureaubladtoepassing met aanmelden, aanmelding en Profielbeheer met behulp van Azure Active Directory B2C.
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
ms.openlocfilehash: 8e2b5c704230ee2ba1395dc76a1551aaa8e7af7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="232b8-103">Azure AD B2C: Een Windows desktop app bouwen</span><span class="sxs-lookup"><span data-stu-id="232b8-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="232b8-104">U kunt met behulp van Azure Active Directory (Azure AD) B2C beheerfuncties krachtige Self-service identiteitsbeheer toevoegen aan uw bureaublad-app in slechts enkele korte stappen.</span><span class="sxs-lookup"><span data-stu-id="232b8-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features to your desktop app in a few short steps.</span></span> <span data-ttu-id="232b8-105">In dit artikel wordt beschreven hoe u een .NET Windows Presentation Foundation (WPF) 'takenlijst' u app maakt die gebruikersregistratie, aanmelding en Profielbeheer bevat.</span><span class="sxs-lookup"><span data-stu-id="232b8-105">This article will show you how to create a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="232b8-106">De app biedt ondersteuning voor aanmelden en aanmelden met een gebruikersnaam of e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="232b8-106">The app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="232b8-107">Het biedt ook ondersteuning voor zich kunnen registreren en aanmelden via sociale accounts zoals Facebook en Google.</span><span class="sxs-lookup"><span data-stu-id="232b8-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="232b8-108">Een Azure AD B2C-directory maken</span><span class="sxs-lookup"><span data-stu-id="232b8-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="232b8-109">Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken.</span><span class="sxs-lookup"><span data-stu-id="232b8-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="232b8-110">Een directory is een container voor alle gebruikers, apps, groepen en meer.</span><span class="sxs-lookup"><span data-stu-id="232b8-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="232b8-111">Als u nog geen directory hebt, [maakt u een B2C-directory](active-directory-b2c-get-started.md) voordat u doorgaat in deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="232b8-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="232b8-112">Een app maken</span><span class="sxs-lookup"><span data-stu-id="232b8-112">Create an application</span></span>
<span data-ttu-id="232b8-113">Vervolgens maakt u een app in uw B2C-directory.</span><span class="sxs-lookup"><span data-stu-id="232b8-113">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="232b8-114">Hiermee geeft u informatie door aan Azure AD die nodig is om veilig te communiceren met uw app.</span><span class="sxs-lookup"><span data-stu-id="232b8-114">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="232b8-115">Volg [deze instructies](active-directory-b2c-app-registration.md) om een app te maken.</span><span class="sxs-lookup"><span data-stu-id="232b8-115">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="232b8-116">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="232b8-116">Be sure to:</span></span>

* <span data-ttu-id="232b8-117">Omvatten een **native client** in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="232b8-117">Include a **native client** in the application.</span></span>
* <span data-ttu-id="232b8-118">Kopieer de **omleidings-URI** `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="232b8-118">Copy the **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="232b8-119">Dit is de standaard-URL voor dit codevoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="232b8-119">It is the default URL for this code sample.</span></span>
* <span data-ttu-id="232b8-120">U de **toepassings-id** kopieert die is toegewezen aan uw app.</span><span class="sxs-lookup"><span data-stu-id="232b8-120">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="232b8-121">U hebt dit later nodig.</span><span class="sxs-lookup"><span data-stu-id="232b8-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="232b8-122">Het beleid maken</span><span class="sxs-lookup"><span data-stu-id="232b8-122">Create your policies</span></span>
<span data-ttu-id="232b8-123">In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="232b8-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="232b8-124">Dit codevoorbeeld bevat drie identiteitservaringen: registreren, aanmelden en profiel bewerken.</span><span class="sxs-lookup"><span data-stu-id="232b8-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="232b8-125">U moet een beleid voor elk type maken, zoals beschreven in de [naslagartikel](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="232b8-125">You need to create a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="232b8-126">Wanneer u uw drie beleidsregels maakt:</span><span class="sxs-lookup"><span data-stu-id="232b8-126">When you create the three policies, be sure to:</span></span>

* <span data-ttu-id="232b8-127">Kiest u **Registratie met gebruikers-id** of **Registratie via e-mail** op de blade met identiteitsproviders.</span><span class="sxs-lookup"><span data-stu-id="232b8-127">Choose either **User ID sign-up** or **Email sign-up** in the identity providers blade.</span></span>
* <span data-ttu-id="232b8-128">Kiest u **Weergavenaam** en andere registratiekenmerken in het registratiebeleid.</span><span class="sxs-lookup"><span data-stu-id="232b8-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="232b8-129">Kiest u **Weergavenaam**- en **Object-id**-claims als toepassingsclaims voor elk beleid.</span><span class="sxs-lookup"><span data-stu-id="232b8-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="232b8-130">U kunt ook andere claims kiezen.</span><span class="sxs-lookup"><span data-stu-id="232b8-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="232b8-131">Kopieert u de **naam** van elk beleid nadat u dit hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="232b8-131">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="232b8-132">Deze moet het voorvoegsel `b2c_1_` bevatten.</span><span class="sxs-lookup"><span data-stu-id="232b8-132">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="232b8-133">U hebt deze beleidsnamen later nodig.</span><span class="sxs-lookup"><span data-stu-id="232b8-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="232b8-134">Nadat u de drie beleidsregels hebt gemaakt, kunt u uw app maken.</span><span class="sxs-lookup"><span data-stu-id="232b8-134">After you have successfully created the three policies, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="232b8-135">De code downloaden</span><span class="sxs-lookup"><span data-stu-id="232b8-135">Download the code</span></span>
<span data-ttu-id="232b8-136">De code voor deze zelfstudie [wordt bewaard in GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="232b8-136">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="232b8-137">Als u het voorbeeld wilt maken terwijl u aan het werk bent, kunt u [een basisproject downloaden als zip-bestand](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="232b8-137">To build the sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="232b8-138">U kunt het basisproject ook klonen:</span><span class="sxs-lookup"><span data-stu-id="232b8-138">You can also clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="232b8-139">De voltooide app is ook [beschikbaar als zip-bestand](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) of in de `complete`-vertakking van dezelfde opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="232b8-139">The completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on the `complete` branch of the same repository.</span></span>

<span data-ttu-id="232b8-140">Nadat u de voorbeeldcode hebt gedownload, opent u het SLN-bestand in Visual Studio om aan de slag te gaan.</span><span class="sxs-lookup"><span data-stu-id="232b8-140">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="232b8-141">De `TaskClient` project is de WPF-bureaubladtoepassing die de gebruiker werkt.</span><span class="sxs-lookup"><span data-stu-id="232b8-141">The `TaskClient` project is the WPF desktop application that the user interacts with.</span></span> <span data-ttu-id="232b8-142">Voor de doeleinden van deze zelfstudie wordt een taak back-end-web-API, gehost in Azure die de takenlijst van elke gebruiker opslaat aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="232b8-142">For the purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="232b8-143">U hoeft niet voor het bouwen van de web-API, we hebben al actief voor u.</span><span class="sxs-lookup"><span data-stu-id="232b8-143">You do not need to build the web API, we already have it running for you.</span></span>

<span data-ttu-id="232b8-144">Bekijk voor meer informatie over hoe een web-API veilig wordt geverifieerd aanvragen met behulp van Azure AD B2C, de [web-API aan de slag artikel](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="232b8-144">To learn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="232b8-145">Uitvoeren van beleid</span><span class="sxs-lookup"><span data-stu-id="232b8-145">Execute policies</span></span>
<span data-ttu-id="232b8-146">Uw app communiceert met Azure AD B2C door te sturen verificatieberichten die het beleid dat hij of zij wil uit te voeren als onderdeel van de HTTP-aanvraag opgeven.</span><span class="sxs-lookup"><span data-stu-id="232b8-146">Your app communicates with Azure AD B2C by sending authentication messages that specify the policy they want to execute as part of the HTTP request.</span></span> <span data-ttu-id="232b8-147">Voor .NET-desktoptoepassingen, kunt u de voorbeeld Microsoft Authentication Library (MSAL) gebruiken om te verzenden van berichten van OAuth 2.0-verificatie, voert u beleidsregels en ophalen van tokens die aanroepen van web-API's.</span><span class="sxs-lookup"><span data-stu-id="232b8-147">For .NET desktop applications, you can use the preview Microsoft Authentication Library (MSAL) to send OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="232b8-148">MSAL installeren</span><span class="sxs-lookup"><span data-stu-id="232b8-148">Install MSAL</span></span>
<span data-ttu-id="232b8-149">Toevoegen van MSAL naar de `TaskClient` project met de Visual Studio Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="232b8-149">Add MSAL to the `TaskClient` project by using the Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="232b8-150">Uw B2C-gegevens invoeren</span><span class="sxs-lookup"><span data-stu-id="232b8-150">Enter your B2C details</span></span>
<span data-ttu-id="232b8-151">Open het bestand `Globals.cs` en elk van de eigenschapswaarden vervangt door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="232b8-151">Open the file `Globals.cs` and replace each of the property values with your own.</span></span> <span data-ttu-id="232b8-152">Deze klasse wordt gebruikt in de gehele `TaskClient` verwijzing gebruikte waarden.</span><span class="sxs-lookup"><span data-stu-id="232b8-152">This class is used throughout `TaskClient` to reference commonly used values.</span></span>

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

### <a name="create-the-publicclientapplication"></a><span data-ttu-id="232b8-153">De PublicClientApplication maken</span><span class="sxs-lookup"><span data-stu-id="232b8-153">Create the PublicClientApplication</span></span>
<span data-ttu-id="232b8-154">De primaire klasse van MSAL is `PublicClientApplication`.</span><span class="sxs-lookup"><span data-stu-id="232b8-154">The primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="232b8-155">Deze klasse vertegenwoordigt de toepassing in het Azure AD B2C-systeem.</span><span class="sxs-lookup"><span data-stu-id="232b8-155">This class represents your application in the Azure AD B2C system.</span></span> <span data-ttu-id="232b8-156">Wanneer de initalizes app maakt voor een exemplaar van `PublicClientApplication` in `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="232b8-156">When the app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="232b8-157">Dit kan worden gebruikt in het venster.</span><span class="sxs-lookup"><span data-stu-id="232b8-157">This can be used throughout the window.</span></span>

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens to persist when the user closes the app,
        // we've extended the MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="232b8-158">Een registratie stroom initiëren</span><span class="sxs-lookup"><span data-stu-id="232b8-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="232b8-159">Wanneer een gebruiker ervoor om te tekenen van kiest, die u wilt starten een aanmelding stroom die gebruikmaakt van het registratiebeleid die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="232b8-159">When a user opts to signs up, you want to initiate a sign-up flow that uses the sign-up policy you created.</span></span> <span data-ttu-id="232b8-160">Met behulp van MSAL die u zojuist hebt aanroepen `pca.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="232b8-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="232b8-161">De parameters die u doorgeeft aan `AcquireTokenAsync(...)` bepalen welk token wordt weergegeven, het beleid op waarmee de verificatieaanvraag, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="232b8-161">The parameters you pass to `AcquireTokenAsync(...)` determine which token you receive, the policy used in the authentication request, and more.</span></span>

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use the app's clientId here as the scope parameter, indicating that
        // you want a token to the your app's backend web API (represented by
        // the cloud hosted task API).  Use the UiOptions.ForceLogin flag to
        // indicate to MSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in the app that the user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When the request completes successfully, you can get user
        // information from the AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After the sign up successfully completes, display the user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of the policy.
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

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="232b8-162">Starten van een stroom aanmelden</span><span class="sxs-lookup"><span data-stu-id="232b8-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="232b8-163">U kunt een stroom aanmelden op dezelfde manier als dat u een aanmelding stroom initiëren initiëren.</span><span class="sxs-lookup"><span data-stu-id="232b8-163">You can initiate a sign-in flow in the same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="232b8-164">Wanneer een gebruiker zich aanmeldt, moet u dezelfde aanroep MSAL, ditmaal met behulp van uw beleid voor aanmelden:</span><span class="sxs-lookup"><span data-stu-id="232b8-164">When a user signs in, make the same call to MSAL, this time by using your sign-in policy:</span></span>

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

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="232b8-165">Starten van een stroom profiel bewerken</span><span class="sxs-lookup"><span data-stu-id="232b8-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="232b8-166">U kunt een beleid voor het profiel bewerken opnieuw uitvoeren op dezelfde manier:</span><span class="sxs-lookup"><span data-stu-id="232b8-166">Again, you can execute an edit-profile policy in the same fashion:</span></span>

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

<span data-ttu-id="232b8-167">In al deze gevallen retourneert MSAL ofwel een token in `AuthenticationResult` of er een uitzondering gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="232b8-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="232b8-168">Telkens wanneer u een token via MSAL krijgen, kunt u de `AuthenticationResult.User` object bijwerken van de gebruikersgegevens in de app, zoals de gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="232b8-168">Each time you get a token from MSAL, you can use the `AuthenticationResult.User` object to update the user data in the app, such as the UI.</span></span> <span data-ttu-id="232b8-169">Het token voor gebruik in andere onderdelen van de toepassing worden ook opgeslagen in ADAL.</span><span class="sxs-lookup"><span data-stu-id="232b8-169">ADAL also caches the token for use in other parts of the application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="232b8-170">Controleer voor tokens op app starten</span><span class="sxs-lookup"><span data-stu-id="232b8-170">Check for tokens on app start</span></span>
<span data-ttu-id="232b8-171">U kunt ook MSAL gebruiken om-in status van de gebruiker bij te houden.</span><span class="sxs-lookup"><span data-stu-id="232b8-171">You can also use MSAL to keep track of the user's sign-in state.</span></span>  <span data-ttu-id="232b8-172">In deze app willen we de gebruiker blijft aangemeld nadat ze de app sluiten en opnieuw openen.</span><span class="sxs-lookup"><span data-stu-id="232b8-172">In this app, we want the user to remain signed in even after they close the app & re-open it.</span></span>  <span data-ttu-id="232b8-173">Terug in de `OnInitialized` overschrijven, gebruikt u de MSAL `AcquireTokenSilent` methode om te controleren of tokens in de cache opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="232b8-173">Back inside the `OnInitialized` override, use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span></span>

```C#
AuthenticationResult result = null;
try
{
    // If the user has has a token cached with any policy, we'll display them as signed-in.
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
        // There are no tokens in the cache.  Proceed without calling the To Do list service.
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

## <a name="call-the-task-api"></a><span data-ttu-id="232b8-174">De takenlijst-API aanroepen</span><span class="sxs-lookup"><span data-stu-id="232b8-174">Call the task API</span></span>
<span data-ttu-id="232b8-175">U hebt nu MSAL gebruikt om beleidsregels uitvoeren en tokens verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="232b8-175">You have now used MSAL to execute policies and get tokens.</span></span>  <span data-ttu-id="232b8-176">Wanneer u een deze tokens aan te roepen de takenlijst-API gebruiken wilt, kunt u opnieuw gebruiken van MSAL `AcquireTokenSilent` methode om te controleren of tokens in de cache opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="232b8-176">When you want to use one these tokens to call the task API, you can again use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span></span>

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want to check for a cached token, independent of whatever policy was used to acquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent to indicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch the exception and show the user a message.
    catch (MsalException ex)
    {
        // There is no access token in the cache, so prompt the user to sign-in.
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

<span data-ttu-id="232b8-177">Bij het aanroepen van `AcquireTokenSilentAsync(...)` is gelukt en een token gevonden in de cache, kunt u het token voor toevoegen de `Authorization` koptekst van de HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="232b8-177">When the call to `AcquireTokenSilentAsync(...)` succeeds and a token is found in the cache, you can add the token to the `Authorization` header of the HTTP request.</span></span> <span data-ttu-id="232b8-178">De web-API van de taak wordt deze header gebruiken om te verifiëren van de aanvraag voor het lezen van de takenlijst van de gebruiker:</span><span class="sxs-lookup"><span data-stu-id="232b8-178">The task web API will use this header to authenticate the request to read the user's to-do list:</span></span>

```C#
    ...
    // Once the token has been returned by MSAL, add it to the http authorization header, before making the call to access the To Do list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call the To Do list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-the-user-out"></a><span data-ttu-id="232b8-179">De gebruiker afmelden</span><span class="sxs-lookup"><span data-stu-id="232b8-179">Sign the user out</span></span>
<span data-ttu-id="232b8-180">Ten slotte kunt u MSAL naar einde van een gebruikerssessie met de app wanneer de gebruiker selecteert **Afmelden**.</span><span class="sxs-lookup"><span data-stu-id="232b8-180">Finally, you can use MSAL to end a user's session with the app when the user selects **Sign out**.</span></span>  <span data-ttu-id="232b8-181">Wanneer u MSAL gebruikt, wordt dit wordt bereikt door het wissen van alle van de tokens van de tokencache:</span><span class="sxs-lookup"><span data-stu-id="232b8-181">When using MSAL, this is accomplished by clearing all of the tokens from the token cache:</span></span>

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of the user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in the browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update the UI to show the user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="232b8-182">De voorbeeld-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="232b8-182">Run the sample app</span></span>
<span data-ttu-id="232b8-183">Ten slotte bouwen en uitvoeren van het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="232b8-183">Finally, build and run the sample.</span></span>  <span data-ttu-id="232b8-184">Zich registreren voor de app met behulp van de naam van een e-adres of de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="232b8-184">Sign up for the app by using an email address or user name.</span></span> <span data-ttu-id="232b8-185">Meld u af en meld u opnieuw aan als dezelfde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="232b8-185">Sign out and sign back in as the same user.</span></span> <span data-ttu-id="232b8-186">Profiel van de gebruiker bewerken.</span><span class="sxs-lookup"><span data-stu-id="232b8-186">Edit that user's profile.</span></span> <span data-ttu-id="232b8-187">Meld u af en meld u aan met behulp van een andere gebruiker.</span><span class="sxs-lookup"><span data-stu-id="232b8-187">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="232b8-188">Sociale IDPs toevoegen</span><span class="sxs-lookup"><span data-stu-id="232b8-188">Add social IDPs</span></span>
<span data-ttu-id="232b8-189">Op dit moment wordt de app ondersteunt alleen gebruiker registreren en aanmelden met **lokale accounts**.</span><span class="sxs-lookup"><span data-stu-id="232b8-189">Currently, the app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="232b8-190">Dit zijn opgeslagen in uw B2C-directory accounts die gebruikmaken van een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="232b8-190">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="232b8-191">U kunt met behulp van Azure AD B2C, ondersteuning voor andere id-providers (IDPs) toevoegen zonder uw code.</span><span class="sxs-lookup"><span data-stu-id="232b8-191">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="232b8-192">Volg de gedetailleerde instructies in deze artikelen wilt sociale IDPs toevoegen aan uw app, eerst.</span><span class="sxs-lookup"><span data-stu-id="232b8-192">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span></span> <span data-ttu-id="232b8-193">Voor elke IDP die u wilt ondersteunen, moet u een toepassing registreren in dat systeem en het verkrijgen van een client-ID.</span><span class="sxs-lookup"><span data-stu-id="232b8-193">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="232b8-194">Facebook ingesteld als een IDP</span><span class="sxs-lookup"><span data-stu-id="232b8-194">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="232b8-195">Google ingesteld als een IDP</span><span class="sxs-lookup"><span data-stu-id="232b8-195">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="232b8-196">Amazon ingesteld als een IDP</span><span class="sxs-lookup"><span data-stu-id="232b8-196">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="232b8-197">LinkedIn instellen als een IDP</span><span class="sxs-lookup"><span data-stu-id="232b8-197">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="232b8-198">Nadat u de id-providers aan uw B2C-directory toevoegen, moet u elk van de drie beleidsregels om op te nemen van de nieuwe IDPs bewerken, zoals beschreven in de [naslagartikel](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="232b8-198">After you add the identity providers to your B2C directory, you need to edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="232b8-199">Nadat u uw beleid opslaat, voer de app opnieuw.</span><span class="sxs-lookup"><span data-stu-id="232b8-199">After you save your policies, run the app again.</span></span> <span data-ttu-id="232b8-200">U ziet nu de nieuwe IDPs toegevoegd als aanmelden en aanmeldingsopties in elk van uw identiteit ervaringen.</span><span class="sxs-lookup"><span data-stu-id="232b8-200">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="232b8-201">U kunt experimenteren met het beleid en houd rekening met de gevolgen voor uw voorbeeld-app.</span><span class="sxs-lookup"><span data-stu-id="232b8-201">You can experiment with your policies and observe the effects on your sample app.</span></span> <span data-ttu-id="232b8-202">Toevoegen of verwijderen van IDPs, toepassingsclaims bewerken of registratiekenmerken wijzigen.</span><span class="sxs-lookup"><span data-stu-id="232b8-202">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="232b8-203">Experiment totdat u kunt zien hoe beleidsregels, verificatieaanvragen en MSAL met elkaar verbinden.</span><span class="sxs-lookup"><span data-stu-id="232b8-203">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="232b8-204">Voor een verwijzing naar het voltooide voorbeeld [wordt geleverd als ZIP-bestand](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="232b8-204">For reference, the completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="232b8-205">U kunt dit ook klonen van GitHub:</span><span class="sxs-lookup"><span data-stu-id="232b8-205">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
