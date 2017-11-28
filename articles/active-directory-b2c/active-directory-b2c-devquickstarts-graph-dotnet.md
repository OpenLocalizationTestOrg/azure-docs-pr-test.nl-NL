---
title: 'Azure Active Directory B2C: Gebruik Hallo Graph API | Microsoft Docs'
description: Hoe Hallo toocall Graph API voor een B2C-tenant met behulp van een toepassing identiteit tooautomate Hallo-proces.
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a><span data-ttu-id="97e9d-103">Azure AD B2C: Hallo Graph API gebruiken</span><span class="sxs-lookup"><span data-stu-id="97e9d-103">Azure AD B2C: Use hello Graph API</span></span>
<span data-ttu-id="97e9d-104">Azure Active Directory (Azure AD) B2C tenants vaak zeer grote toobe.</span><span class="sxs-lookup"><span data-stu-id="97e9d-104">Azure Active Directory (Azure AD) B2C tenants tend toobe very large.</span></span> <span data-ttu-id="97e9d-105">Dit betekent dat veel algemene beheertaken voor tenant toobe via een programma wordt uitgevoerd moeten.</span><span class="sxs-lookup"><span data-stu-id="97e9d-105">This means that many common tenant management tasks need toobe performed programmatically.</span></span> <span data-ttu-id="97e9d-106">Een voorbeeld van een primaire is Gebruikersbeheer.</span><span class="sxs-lookup"><span data-stu-id="97e9d-106">A primary example is user management.</span></span> <span data-ttu-id="97e9d-107">Mogelijk moet u een bestaande gebruiker store tooa B2C-tenant toomigrate.</span><span class="sxs-lookup"><span data-stu-id="97e9d-107">You might need toomigrate an existing user store tooa B2C tenant.</span></span> <span data-ttu-id="97e9d-108">U kunt toohost gebruikersregistratie wilt op de pagina en gebruikersaccounts maken in uw Azure AD B2C-directory achter de schermen Hallo.</span><span class="sxs-lookup"><span data-stu-id="97e9d-108">You may want toohost user registration on your own page and create user accounts in your Azure AD B2C directory behind hello scenes.</span></span> <span data-ttu-id="97e9d-109">Deze typen taken vereist Hallo mogelijkheid toocreate, lezen, bijwerken en verwijderen van gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="97e9d-109">These types of tasks require hello ability toocreate, read, update, and delete user accounts.</span></span> <span data-ttu-id="97e9d-110">U kunt deze taken uitvoeren met behulp van hello Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="97e9d-110">You can do these tasks by using hello Azure AD Graph API.</span></span>

<span data-ttu-id="97e9d-111">Voor B2C-tenants zijn er twee primaire modi voor de communicatie met de Hallo Graph API.</span><span class="sxs-lookup"><span data-stu-id="97e9d-111">For B2C tenants, there are two primary modes of communicating with hello Graph API.</span></span>

* <span data-ttu-id="97e9d-112">Voor interactieve, eenmalige taken, moet u fungeren als een administrator-account in Hallo B2C-tenant wanneer u Hallo taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="97e9d-112">For interactive, run-once tasks, you should act as an administrator account in hello B2C tenant when you perform hello tasks.</span></span> <span data-ttu-id="97e9d-113">In deze modus moet een beheerder toosign met referenties waarover de beheerder om een toohello aanroepen Graph API kan uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="97e9d-113">This mode requires an administrator toosign in with credentials before that admin can perform any calls toohello Graph API.</span></span>
* <span data-ttu-id="97e9d-114">Voor de geautomatiseerde, continue taken, moet u een type van service-account dat u opgeeft met Hallo benodigde bevoegdheden tooperform beheertaken.</span><span class="sxs-lookup"><span data-stu-id="97e9d-114">For automated, continuous tasks, you should use some type of service account that you provide with hello necessary privileges tooperform management tasks.</span></span> <span data-ttu-id="97e9d-115">In Azure AD kunt u dit doen door een toepassing registreren en tooAzure AD verifiëren.</span><span class="sxs-lookup"><span data-stu-id="97e9d-115">In Azure AD, you can do this by registering an application and authenticating tooAzure AD.</span></span> <span data-ttu-id="97e9d-116">Dit wordt gedaan met behulp van een **toepassings-ID** die gebruikmaakt van Hallo [OAuth 2.0-clientreferenties verlenen](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="97e9d-116">This is done by using an **Application ID** that uses hello [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="97e9d-117">In dit geval fungeert Hallo toepassing als zichzelf niet als een gebruiker toocall Hallo Graph API.</span><span class="sxs-lookup"><span data-stu-id="97e9d-117">In this case, hello application acts as itself, not as a user, toocall hello Graph API.</span></span>

<span data-ttu-id="97e9d-118">In dit artikel bespreken we hoe tooperform Hallo geautomatiseerde gebruiksvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="97e9d-118">In this article, we'll discuss how tooperform hello automated-use case.</span></span> <span data-ttu-id="97e9d-119">toodemonstrate, gaan we gaat verder met een .NET 4.5 `B2CGraphClient` die de gebruiker voert maken, lezen, bijwerken en verwijderen (CRUD)-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="97e9d-119">toodemonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="97e9d-120">Hallo-client heeft een Windows-opdrachtregelinterface (CLI) waarmee u tooinvoke verschillende methoden.</span><span class="sxs-lookup"><span data-stu-id="97e9d-120">hello client will have a Windows command-line interface (CLI) that allows you tooinvoke various methods.</span></span> <span data-ttu-id="97e9d-121">Hallo-code is echter toobehave geschreven in een niet-interactieve, geautomatiseerde manier.</span><span class="sxs-lookup"><span data-stu-id="97e9d-121">However, hello code is written toobehave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="97e9d-122">Een Azure AD B2C-tenant verkrijgen</span><span class="sxs-lookup"><span data-stu-id="97e9d-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="97e9d-123">Voordat u kunt maken van toepassingen of gebruikers of helemaal met Azure AD communiceren, moet u een Azure AD B2C-tenant en een globale beheerdersaccount in Hallo-tenant.</span><span class="sxs-lookup"><span data-stu-id="97e9d-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in hello tenant.</span></span> <span data-ttu-id="97e9d-124">Als u nog geen een tenant hebt, [aan de slag met Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="97e9d-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="97e9d-125">Uw toepassing registreren in uw tenant</span><span class="sxs-lookup"><span data-stu-id="97e9d-125">Register your application in your tenant</span></span>
<span data-ttu-id="97e9d-126">Nadat u een B2C-tenant hebt, moet u tooregister uw toepassing via Hallo [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="97e9d-126">After you have a B2C tenant, you need tooregister your application via hello [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97e9d-127">toouse hello Graph API met uw B2C-tenant, moet u een specifieke toepassing tooregister met behulp van algemene Hallo *App registraties* blade in Azure Portal Hallo **niet** Azure AD B2C  *Toepassingen* blade.</span><span class="sxs-lookup"><span data-stu-id="97e9d-127">toouse hello Graph API with your B2C tenant, you will need tooregister a dedicated application by using hello generic *App Registrations* blade in hello Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="97e9d-128">U niet opnieuw gebruiken Hallo reeds bestaande B2C toepassingen die u hebt geregistreerd in Azure AD B2C Hallo *toepassingen* blade.</span><span class="sxs-lookup"><span data-stu-id="97e9d-128">You can't reuse hello already-existing B2C applications that you registered in hello Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="97e9d-129">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="97e9d-129">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="97e9d-130">Uw account selecteren in Hallo rechtsboven Hallo pagina kiest u uw Azure AD B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="97e9d-130">Choose your Azure AD B2C tenant by selecting your account in hello top right corner of hello page.</span></span>
3. <span data-ttu-id="97e9d-131">In Hallo links navigatiedeelvenster kiest **meer Services**, klikt u op **App registraties**, en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="97e9d-131">In hello left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="97e9d-132">Volg de aanwijzingen Hallo en maak een nieuwe toepassing.</span><span class="sxs-lookup"><span data-stu-id="97e9d-132">Follow hello prompts and create a new application.</span></span> 
    1. <span data-ttu-id="97e9d-133">Selecteer **Web-App / API** zoals Hallo toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="97e9d-133">Select **Web App / API** as hello Application Type.</span></span>    
    2. <span data-ttu-id="97e9d-134">Geef **een omleidings-URI** (bijvoorbeeld https://B2CGraphAPI) als het is niet relevant zijn voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="97e9d-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="97e9d-135">Hallo toepassing wordt nu weergegeven in de lijst Hallo van toepassingen, klikt u op de tooobtain hello **toepassings-ID** (ook wel bekend als een Client-ID).</span><span class="sxs-lookup"><span data-stu-id="97e9d-135">hello application will now show up in hello list of applications, click on it tooobtain hello **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="97e9d-136">Kopieer de verbindingsreeks als u hebt deze nodig in een volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="97e9d-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="97e9d-137">Klik op de blade instellingen hello, op **sleutels** en voeg een nieuwe sleutel (ook wel bekend als clientgeheim).</span><span class="sxs-lookup"><span data-stu-id="97e9d-137">In hello Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="97e9d-138">Ook het kopiëren voor gebruik in een volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="97e9d-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="97e9d-139">Configureer maken, lezen en bijwerken van machtigingen voor uw toepassing</span><span class="sxs-lookup"><span data-stu-id="97e9d-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="97e9d-140">Nu u tooconfigure moet uw toepassing tooget die alle Hallo machtigingen toocreate vereist, lezen, bijwerken en verwijderen van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="97e9d-140">Now you need tooconfigure your application tooget all hello required permissions toocreate, read, update and delete users.</span></span>

1. <span data-ttu-id="97e9d-141">Als u doorgaat in Azure portal App registraties blade hello, selecteer uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="97e9d-141">Continuing in hello Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="97e9d-142">Klik op de blade instellingen hello, op **vereist machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="97e9d-142">In hello Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="97e9d-143">Klik in de blade Hallo vereiste machtigingen op **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="97e9d-143">In hello Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="97e9d-144">Selecteer Hallo Hallo toegang inschakelen Blade **lezen en schrijven directorygegevens** machtiging van **Toepassingsmachtigingen** en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="97e9d-144">In hello Enable Access  blade, select hello **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="97e9d-145">Ten slotte terug in de blade van de vereiste machtigingen hello, klik op Hallo **machtiging verlenen** knop.</span><span class="sxs-lookup"><span data-stu-id="97e9d-145">Finally, back in hello Required permissions blade, click on hello **Grant Permissions** button.</span></span>

<span data-ttu-id="97e9d-146">U hebt nu een toepassing die gemachtigd toocreate, lezen en bijwerken gebruikers van uw B2C-tenant is.</span><span class="sxs-lookup"><span data-stu-id="97e9d-146">You now have an application that has permission toocreate, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="97e9d-147">Verwijdermachtigingen voor uw toepassing configureren</span><span class="sxs-lookup"><span data-stu-id="97e9d-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="97e9d-148">Op dit moment Hallo *lezen en schrijven directorygegevens* machtiging heeft **niet** Hallo mogelijkheid toodo omvatten alle verwijderingen zoals het verwijderen van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="97e9d-148">Currently, hello *Read and write directory data* permission does **NOT** include hello ability toodo any deletions such as deleting users.</span></span> <span data-ttu-id="97e9d-149">Als u wilt dat toogive toepassing hello mogelijkheid toodelete gebruikers, moet u toodo deze extra stappen die betrekking hebben op PowerShell, anders kunt u de volgende sectie toohello overslaan.</span><span class="sxs-lookup"><span data-stu-id="97e9d-149">If you want toogive your application hello ability toodelete users, you'll need toodo these extra steps that involve PowerShell, otherwise, you can skip toohello next section.</span></span>

<span data-ttu-id="97e9d-150">Eerst downloaden en installeren van Hallo [Microsoft Online Services-aanmeldhulp](http://go.microsoft.com/fwlink/?LinkID=286152).</span><span class="sxs-lookup"><span data-stu-id="97e9d-150">First, download and install hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="97e9d-151">Download en installeer Hallo vervolgens [64-bits Azure Active Directory-module voor Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span><span class="sxs-lookup"><span data-stu-id="97e9d-151">Then download and install hello [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="97e9d-152">Nadat u Hallo PowerShell-module geïnstalleerd, opent u PowerShell en verbinding maken met tooyour B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="97e9d-152">After you install hello PowerShell module, open PowerShell and connect tooyour B2C tenant.</span></span> <span data-ttu-id="97e9d-153">Nadat u hebt uitgevoerd `Get-Credential`, wordt u gevraagd om een gebruikersnaam en wachtwoord, Enter Hallo-gebruikersnaam en wachtwoord van uw B2C-tenant administrator-account.</span><span class="sxs-lookup"><span data-stu-id="97e9d-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter hello user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97e9d-154">U moet toouse een B2C-tenant administrator-account dat is **lokale** toohello B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="97e9d-154">You need toouse a B2C tenant administrator account that is **local** toohello B2C tenant.</span></span> <span data-ttu-id="97e9d-155">Deze accounts moeten uitzien: myusername@myb2ctenant.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="97e9d-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="97e9d-156">Nu we hello gebruiken **toepassings-ID** in onderstaande tooassign Hallo toepassing hello account administrator gebruikersrol waarmee deze toodelete gebruikers Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="97e9d-156">Now we'll use hello **Application ID** in hello script below tooassign hello application hello user account administrator role which will allow it toodelete users.</span></span> <span data-ttu-id="97e9d-157">Deze rollen hebben een bekende id's, dus u hoeft alleen toodo wordt ingevoerd uw **toepassings-ID** in onderstaande Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="97e9d-157">These roles have well-known identifiers, so all you need toodo is input your **Application ID** in hello script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="97e9d-158">Nu uw toepassing heeft ook machtigingen toodelete gebruikers van uw B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="97e9d-158">Your application now also has permissions toodelete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-hello-sample-code"></a><span data-ttu-id="97e9d-159">Downloaden, configureren en voorbeeldcode Hallo bouwen</span><span class="sxs-lookup"><span data-stu-id="97e9d-159">Download, configure, and build hello sample code</span></span>
<span data-ttu-id="97e9d-160">Eerst Hallo voorbeeldcode downloaden en deze uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="97e9d-160">First, download hello sample code and get it running.</span></span> <span data-ttu-id="97e9d-161">Het duurt we vervolgens een nader bekijken.</span><span class="sxs-lookup"><span data-stu-id="97e9d-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="97e9d-162">U kunt [Hallo voorbeeldcode als ZIP-bestand downloaden](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="97e9d-162">You can [download hello sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="97e9d-163">U kunt dit ook klonen naar een map van uw keuze:</span><span class="sxs-lookup"><span data-stu-id="97e9d-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="97e9d-164">Open Hallo `B2CGraphClient\B2CGraphClient.sln` Visual Studio-oplossing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97e9d-164">Open hello `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="97e9d-165">In Hallo `B2CGraphClient` project, open Hallo bestand `App.config`.</span><span class="sxs-lookup"><span data-stu-id="97e9d-165">In hello `B2CGraphClient` project, open hello file `App.config`.</span></span> <span data-ttu-id="97e9d-166">Hallo drie app-instellingen vervangen door uw eigen waarden:</span><span class="sxs-lookup"><span data-stu-id="97e9d-166">Replace hello three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="97e9d-167">Vervolgens met de rechtermuisknop op Hallo `B2CGraphClient` oplossing en rebuild Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="97e9d-167">Next, right-click on hello `B2CGraphClient` solution and rebuild hello sample.</span></span> <span data-ttu-id="97e9d-168">Als u geslaagde, u hebt nu een `B2C.exe` uitvoerbare bestand zich in `B2CGraphClient\bin\Debug`.</span><span class="sxs-lookup"><span data-stu-id="97e9d-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a><span data-ttu-id="97e9d-169">Gebruiker CRUD-bewerkingen met behulp van Hallo Graph API bouwen</span><span class="sxs-lookup"><span data-stu-id="97e9d-169">Build user CRUD operations by using hello Graph API</span></span>
<span data-ttu-id="97e9d-170">toouse hello B2CGraphClient, open een `cmd` Windows command prompt en wijzigen van uw directory toohello `Debug` directory.</span><span class="sxs-lookup"><span data-stu-id="97e9d-170">toouse hello B2CGraphClient, open a `cmd` Windows command prompt and change your directory toohello `Debug` directory.</span></span> <span data-ttu-id="97e9d-171">Voer Hallo `B2C Help` opdracht.</span><span class="sxs-lookup"><span data-stu-id="97e9d-171">Then run hello `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="97e9d-172">Hiermee wordt een korte beschrijving van elke opdracht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="97e9d-172">This will display a brief description of each command.</span></span> <span data-ttu-id="97e9d-173">Telkens wanneer u een van deze opdrachten aanroepen `B2CGraphClient` maakt u een aanvraag toohello Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="97e9d-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request toohello Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="97e9d-174">Een toegangstoken opvragen</span><span class="sxs-lookup"><span data-stu-id="97e9d-174">Get an access token</span></span>
<span data-ttu-id="97e9d-175">Een aanvraag toohello Graph API vereist een toegangstoken voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="97e9d-175">Any request toohello Graph API requires an access token for authentication.</span></span> <span data-ttu-id="97e9d-176">`B2CGraphClient`maakt gebruik van Hallo open source Active Directory Authentication Library (ADAL) toohelp toegangstokens te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="97e9d-176">`B2CGraphClient` uses hello open-source Active Directory Authentication Library (ADAL) toohelp acquire access tokens.</span></span> <span data-ttu-id="97e9d-177">ADAL gemakkelijker token overname door te geven van een eenvoudige API en wordt gelet op een aantal belangrijke details, zoals caching toegangstokens.</span><span class="sxs-lookup"><span data-stu-id="97e9d-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="97e9d-178">U hebt geen toouse ADAL tooget tokens, hoewel.</span><span class="sxs-lookup"><span data-stu-id="97e9d-178">You don't have toouse ADAL tooget tokens, though.</span></span> <span data-ttu-id="97e9d-179">U kunt ook tokens ophalen door HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="97e9d-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="97e9d-180">Deze voorbeeldcode maakt gebruik van ADAL v2 in volgorde toocommunicate Hello Graph API.</span><span class="sxs-lookup"><span data-stu-id="97e9d-180">This code sample uses ADAL v2 in order toocommunicate with hello Graph API.</span></span>  <span data-ttu-id="97e9d-181">U moet in volgorde tooget toegangstokens die kunnen worden gebruikt met Azure AD Graph API Hallo ADAL v2 of v3 gebruiken.</span><span class="sxs-lookup"><span data-stu-id="97e9d-181">You must use ADAL v2 or v3 in order tooget access tokens which can be used with hello Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="97e9d-182">Wanneer `B2CGraphClient` wordt uitgevoerd, maakt het een exemplaar van Hallo `B2CGraphClient` klasse.</span><span class="sxs-lookup"><span data-stu-id="97e9d-182">When `B2CGraphClient` runs, it creates an instance of hello `B2CGraphClient` class.</span></span> <span data-ttu-id="97e9d-183">Hallo-constructor voor deze klasse stelt u een steigers ADAL-verificatie:</span><span class="sxs-lookup"><span data-stu-id="97e9d-183">hello constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="97e9d-184">We gebruiken Hallo `B2C Get-User` opdracht als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="97e9d-184">We'll use hello `B2C Get-User` command as an example.</span></span> <span data-ttu-id="97e9d-185">Wanneer `B2C Get-User` wordt aangeroepen zonder eventuele extra ingangen, Hallo CLI aanroepen Hallo `B2CGraphClient.GetAllUsers(...)` methode.</span><span class="sxs-lookup"><span data-stu-id="97e9d-185">When `B2C Get-User` is invoked without any additional inputs, hello CLI calls hello `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="97e9d-186">Deze methode aanroept `B2CGraphClient.SendGraphGetRequest(...)`, die een HTTP GET-aanvraag toohello Graph API worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="97e9d-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request toohello Graph API.</span></span> <span data-ttu-id="97e9d-187">Voordat u `B2CGraphClient.SendGraphGetRequest(...)` verzendt Hallo GET-aanvraag, eerst krijgt een token met behulp van ADAL:</span><span class="sxs-lookup"><span data-stu-id="97e9d-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends hello GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="97e9d-188">U kunt een toegangstoken ophalen voor Hallo Graph API door aanroepen Hallo ADAL `AuthenticationContext.AcquireToken(...)` methode.</span><span class="sxs-lookup"><span data-stu-id="97e9d-188">You can get an access token for hello Graph API by calling hello ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="97e9d-189">ADAL retourneert een `access_token` die Hallo toepassingsidentiteit vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="97e9d-189">ADAL then returns an `access_token` that represents hello application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="97e9d-190">Lezen van gebruikers</span><span class="sxs-lookup"><span data-stu-id="97e9d-190">Read users</span></span>
<span data-ttu-id="97e9d-191">Als u een lijst met gebruikers tooget of een bepaalde gebruiker uit Hallo Graph API ophalen, kunt u een HTTP verzenden `GET` toohello aanvragen `/users` eindpunt.</span><span class="sxs-lookup"><span data-stu-id="97e9d-191">When you want tooget a list of users or get a particular user from hello Graph API, you can send an HTTP `GET` request toohello `/users` endpoint.</span></span> <span data-ttu-id="97e9d-192">Een aanvraag voor alle gebruikers in een tenant Hallo ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="97e9d-192">A request for all of hello users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="97e9d-193">toosee dit verzoek uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="97e9d-193">toosee this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="97e9d-194">Er zijn twee belangrijke zaken toonote:</span><span class="sxs-lookup"><span data-stu-id="97e9d-194">There are two important things toonote:</span></span>

* <span data-ttu-id="97e9d-195">Hallo toegangstoken is verkregen via de ADAL wordt toegevoegd toohello `Authorization` header met behulp van Hallo `Bearer` schema.</span><span class="sxs-lookup"><span data-stu-id="97e9d-195">hello access token acquired via ADAL is added toohello `Authorization` header by using hello `Bearer` scheme.</span></span>
* <span data-ttu-id="97e9d-196">Voor B2C-tenants, moet u de queryparameter Hallo `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="97e9d-196">For B2C tenants, you must use hello query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="97e9d-197">Beide van deze gegevens worden verwerkt in de Hallo `B2CGraphClient.SendGraphGetRequest(...)` methode:</span><span class="sxs-lookup"><span data-stu-id="97e9d-197">Both of these details are handled in hello `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="97e9d-198">Maak gebruikersaccounts van consumenten</span><span class="sxs-lookup"><span data-stu-id="97e9d-198">Create consumer user accounts</span></span>
<span data-ttu-id="97e9d-199">Wanneer u gebruikersaccounts in uw B2C-tenant maken, kunt u een HTTP verzenden `POST` toohello aanvragen `/users` eindpunt:</span><span class="sxs-lookup"><span data-stu-id="97e9d-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request toohello `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="97e9d-200">De meeste van deze eigenschappen in deze aanvraag zijn vereiste toocreate consumer gebruikers.</span><span class="sxs-lookup"><span data-stu-id="97e9d-200">Most of these properties in this request are required toocreate consumer users.</span></span> <span data-ttu-id="97e9d-201">toolearn meer, klikt u op [hier](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span><span class="sxs-lookup"><span data-stu-id="97e9d-201">toolearn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="97e9d-202">Houd er rekening mee dat Hallo `//` opmerkingen zijn opgenomen ter illustratie.</span><span class="sxs-lookup"><span data-stu-id="97e9d-202">Note that hello `//` comments have been included for illustration.</span></span> <span data-ttu-id="97e9d-203">Neem ze niet in een werkelijke-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="97e9d-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="97e9d-204">toosee hello aanvraag, voer een van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="97e9d-204">toosee hello request, run one of hello following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="97e9d-205">Hallo `Create-User` opdracht gebruikt u een .json-bestand als invoerparameter.</span><span class="sxs-lookup"><span data-stu-id="97e9d-205">hello `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="97e9d-206">Dit document bevat een JSON-weergave van een gebruikersobject.</span><span class="sxs-lookup"><span data-stu-id="97e9d-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="97e9d-207">Er zijn twee voorbeeldbestanden .json in de voorbeeldcode Hallo: `usertemplate-email.json` en `usertemplate-username.json`.</span><span class="sxs-lookup"><span data-stu-id="97e9d-207">There are two sample .json files in hello sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="97e9d-208">Uw behoeften, kunt u deze bestanden toosuit wijzigen.</span><span class="sxs-lookup"><span data-stu-id="97e9d-208">You can modify these files toosuit your needs.</span></span> <span data-ttu-id="97e9d-209">Bovendien toohello bovenstaande velden vereist, verschillende optionele velden die u kunt gebruiken, zijn opgenomen in deze bestanden.</span><span class="sxs-lookup"><span data-stu-id="97e9d-209">In addition toohello required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="97e9d-210">Meer informatie over de optionele velden Hallo vindt u in Hallo [entiteitsverwijzing Azure AD Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span><span class="sxs-lookup"><span data-stu-id="97e9d-210">Details on hello optional fields can be found in hello [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="97e9d-211">U kunt zien hoe Hallo POST-aanvraag is geconstrueerd in `B2CGraphClient.SendGraphPostRequest(...)`.</span><span class="sxs-lookup"><span data-stu-id="97e9d-211">You can see how hello POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="97e9d-212">Het toevoegen van een token toohello toegang `Authorization` koptekst van Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="97e9d-212">It attaches an access token toohello `Authorization` header of hello request.</span></span>
* <span data-ttu-id="97e9d-213">Hiermee `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="97e9d-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="97e9d-214">Hallo JSON gebruikersobject in Hallo hoofdtekst van Hallo aanvraag opgenomen.</span><span class="sxs-lookup"><span data-stu-id="97e9d-214">It includes hello JSON user object in hello body of hello request.</span></span>

> [!NOTE]
> <span data-ttu-id="97e9d-215">Als het Hallo-computeraccounts die u wilt dat toomigrate uit een bestaande gebruiker store heeft lagere Wachtwoordsterkte dan Hallo [sterk Wachtwoordsterkte afgedwongen door Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), kunt u uitschakelen Hallo sterk wachtwoord vereist met Hallo `DisableStrongPassword`waarde in Hallo `passwordPolicies` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="97e9d-215">If hello accounts that you want toomigrate from an existing user store has lower password strength than hello [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable hello strong password requirement using hello `DisableStrongPassword` value in hello `passwordPolicies` property.</span></span> <span data-ttu-id="97e9d-216">Bijvoorbeeld, kunt u Hallo gebruikersaanvraag hierboven beschreven als volgt maken: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span><span class="sxs-lookup"><span data-stu-id="97e9d-216">For instance, you can modify hello create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="97e9d-217">Gebruikersaccounts van consumenten bijwerken</span><span class="sxs-lookup"><span data-stu-id="97e9d-217">Update consumer user accounts</span></span>
<span data-ttu-id="97e9d-218">Tijdens het bijwerken van gebruikersobjecten wordt hello vergelijkbaar toohello account dat u gebruikersobjecten toocreate gebruikt.</span><span class="sxs-lookup"><span data-stu-id="97e9d-218">When you update user objects, hello process is similar toohello one you use toocreate user objects.</span></span> <span data-ttu-id="97e9d-219">Maar dit proces maakt gebruik van HTTP Hallo `PATCH` methode:</span><span class="sxs-lookup"><span data-stu-id="97e9d-219">But this process uses hello HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

<span data-ttu-id="97e9d-220">Probeer tooupdate een gebruiker door het bijwerken van uw JSON-bestanden met nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="97e9d-220">Try tooupdate a user by updating your JSON files with new data.</span></span> <span data-ttu-id="97e9d-221">Vervolgens kunt u `B2CGraphClient` toorun een van deze opdrachten:</span><span class="sxs-lookup"><span data-stu-id="97e9d-221">You can then use `B2CGraphClient` toorun one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="97e9d-222">Hallo inspecteren `B2CGraphClient.SendGraphPatchRequest(...)` methode voor meer informatie over het toosend deze aanvraag.</span><span class="sxs-lookup"><span data-stu-id="97e9d-222">Inspect hello `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how toosend this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="97e9d-223">Gebruikers zoeken</span><span class="sxs-lookup"><span data-stu-id="97e9d-223">Search users</span></span>
<span data-ttu-id="97e9d-224">U kunt zoeken naar gebruikers in uw B2C-tenant in een aantal manieren.</span><span class="sxs-lookup"><span data-stu-id="97e9d-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="97e9d-225">Een met behulp van de object-ID of twee, met behulp van de gebruiker van het Hallo-aanmelden-id van gebruiker hello (dat wil zeggen, Hallo `signInNames` eigenschap).</span><span class="sxs-lookup"><span data-stu-id="97e9d-225">One, using hello user's object ID or two, using hello user's sign-in identifer (i.e., hello `signInNames` property).</span></span>

<span data-ttu-id="97e9d-226">Voer een van de Hallo opdrachten toosearch voor een specifieke gebruiker volgen:</span><span class="sxs-lookup"><span data-stu-id="97e9d-226">Run one of hello following commands toosearch for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="97e9d-227">Hier volgen enkele voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="97e9d-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="97e9d-228">Gebruikers verwijderen</span><span class="sxs-lookup"><span data-stu-id="97e9d-228">Delete users</span></span>
<span data-ttu-id="97e9d-229">Hallo-proces voor het verwijderen van een gebruiker is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="97e9d-229">hello process for deleting a user is straightforward.</span></span> <span data-ttu-id="97e9d-230">Gebruik Hallo HTTP `DELETE` methode en constructie Hallo-URL met Hallo corrigeren object-ID:</span><span class="sxs-lookup"><span data-stu-id="97e9d-230">Use hello HTTP `DELETE` method and construct hello URL with hello correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="97e9d-231">toosee bijvoorbeeld Voer deze opdracht en weergave Hallo delete-aanvraag die is afgedrukt toohello console:</span><span class="sxs-lookup"><span data-stu-id="97e9d-231">toosee an example, enter this command and view hello delete request that is printed toohello console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="97e9d-232">Hallo inspecteren `B2CGraphClient.SendGraphDeleteRequest(...)` methode voor meer informatie over het toosend deze aanvraag.</span><span class="sxs-lookup"><span data-stu-id="97e9d-232">Inspect hello `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how toosend this request.</span></span>

<span data-ttu-id="97e9d-233">U kunt veel andere acties Hello Azure AD Graph API in toevoeging toouser beheer uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="97e9d-233">You can perform many other actions with hello Azure AD Graph API in addition toouser management.</span></span> <span data-ttu-id="97e9d-234">De [Azure AD Graph API-referentiemateriaal](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) worden details weergegeven over elke actie, samen met de voorbeeld-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="97e9d-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="97e9d-235">Aangepaste kenmerken gebruiken</span><span class="sxs-lookup"><span data-stu-id="97e9d-235">Use custom attributes</span></span>
<span data-ttu-id="97e9d-236">De meeste toepassingen van de consument moeten toostore een type aangepaste gebruikersprofielgegevens.</span><span class="sxs-lookup"><span data-stu-id="97e9d-236">Most consumer applications need toostore some type of custom user profile information.</span></span> <span data-ttu-id="97e9d-237">Een manier die u kunt dit doen is toodefine een aangepast kenmerk in uw B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="97e9d-237">One way you can do this is toodefine a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="97e9d-238">U kunt vervolgens dat kenmerk Hallo behandelen dezelfde manier als u een andere eigenschap van een gebruikersobject behandelen.</span><span class="sxs-lookup"><span data-stu-id="97e9d-238">You can then treat that attribute hello same way you treat any other property on a user object.</span></span> <span data-ttu-id="97e9d-239">U kunt bijwerken Hallo-kenmerk verwijderen Hallo kenmerk query door het Hallo-kenmerk Hallo kenmerk verzenden als claim in aanmelden tokens en meer.</span><span class="sxs-lookup"><span data-stu-id="97e9d-239">You can update hello attribute, delete hello attribute, query by hello attribute, send hello attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="97e9d-240">een aangepast kenmerk in uw B2C-tenant, toodefine Zie Hallo [B2C aangepast kenmerkverwijzing](active-directory-b2c-reference-custom-attr.md).</span><span class="sxs-lookup"><span data-stu-id="97e9d-240">toodefine a custom attribute in your B2C tenant, see hello [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="97e9d-241">U kunt bekijken Hallo aangepaste kenmerken die worden gedefinieerd in uw B2C-tenant met behulp van `B2CGraphClient`:</span><span class="sxs-lookup"><span data-stu-id="97e9d-241">You can view hello custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="97e9d-242">Hallo-uitvoer van deze functies blijkt Hallo details van elk aangepast kenmerk, zoals:</span><span class="sxs-lookup"><span data-stu-id="97e9d-242">hello output of these functions reveals hello details of each custom attribute, such as:</span></span>

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

<span data-ttu-id="97e9d-243">U kunt Hallo volledige naam, zoals `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, als een eigenschap van de gebruikersobjecten.</span><span class="sxs-lookup"><span data-stu-id="97e9d-243">You can use hello full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="97e9d-244">.Json-bestand bijwerken met de nieuwe eigenschap Hallo en een waarde voor eigenschap Hallo en voer vervolgens:</span><span class="sxs-lookup"><span data-stu-id="97e9d-244">Update your .json file with hello new property and a value for hello property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="97e9d-245">Met behulp van `B2CGraphClient`, hebt u een servicetoepassing die uw gebruikers B2C-tenant programmatisch kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="97e9d-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="97e9d-246">`B2CGraphClient`maakt gebruik van een eigen toepassing identiteit tooauthenticate toohello Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="97e9d-246">`B2CGraphClient` uses its own application identity tooauthenticate toohello Azure AD Graph API.</span></span> <span data-ttu-id="97e9d-247">Ook krijgt deze tokens met behulp van een clientgeheim.</span><span class="sxs-lookup"><span data-stu-id="97e9d-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="97e9d-248">Als u deze functionaliteit in uw toepassing opnemen, houd rekening met enkele belangrijke punten voor B2C-apps:</span><span class="sxs-lookup"><span data-stu-id="97e9d-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="97e9d-249">U moet toogrant Hallo toepassing hello juiste machtigingen in Hallo-tenant.</span><span class="sxs-lookup"><span data-stu-id="97e9d-249">You need toogrant hello application hello proper permissions in hello tenant.</span></span>
* <span data-ttu-id="97e9d-250">Nu moet u toouse ADAL (geen MSAL) tooget toegangstokens.</span><span class="sxs-lookup"><span data-stu-id="97e9d-250">For now, you need toouse ADAL (not MSAL) tooget access tokens.</span></span> <span data-ttu-id="97e9d-251">(U kunt ook verzenden protocolberichten rechtstreeks, zonder gebruik van een bibliotheek.)</span><span class="sxs-lookup"><span data-stu-id="97e9d-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="97e9d-252">Wanneer u Hallo Graph API aanroept, gebruik `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="97e9d-252">When you call hello Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="97e9d-253">Wanneer u maken en consumenten gebruikers bij te werken, is enkele eigenschappen zijn vereist, zoals hierboven is beschreven.</span><span class="sxs-lookup"><span data-stu-id="97e9d-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="97e9d-254">Als u vragen of aanvragen voor acties die u tooperform wilt via Hallo Graph API op uw B2C-tenant, een opmerking voor dit artikel laat bestanden of een probleem in Hallo GitHub code voorbeeld-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="97e9d-254">If you have any questions or requests for actions you would like tooperform by using hello Graph API on your B2C tenant, leave a comment on this article or file an issue in hello GitHub code sample repository.</span></span>

