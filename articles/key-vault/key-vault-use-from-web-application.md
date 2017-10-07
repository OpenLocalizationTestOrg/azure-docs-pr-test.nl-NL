---
title: Azure Sleutelkluis in een webtoepassing aaaUse | Microsoft Docs
description: Gebruik deze zelfstudie toohelp leert u hoe toouse Azure Key Vault vanuit een webtoepassing.
services: key-vault
documentationcenter: 
author: adhurwit
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 9b7d065e-1979-4397-8298-eeba3aec4792
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: adhurwit
ms.openlocfilehash: d5e2299e60b379c4e234d5cd6be03411c5a5c958
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="6c872-103">Azure Sleutelkluis in een webtoepassing gebruiken</span><span class="sxs-lookup"><span data-stu-id="6c872-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="6c872-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="6c872-104">Introduction</span></span>
<span data-ttu-id="6c872-105">Gebruik deze zelfstudie toohelp leert u hoe toouse Azure Key Vault vanuit een webtoepassing in Azure.</span><span class="sxs-lookup"><span data-stu-id="6c872-105">Use this tutorial toohelp you learn how toouse Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="6c872-106">Dit helpt u bij het Hallo-proces voor het openen van een geheim van een Azure Sleutelkluis, zodat deze kan worden gebruikt in uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="6c872-106">It walks you through hello process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="6c872-107">**Geschatte tijd toocomplete:** 15 minuten</span><span class="sxs-lookup"><span data-stu-id="6c872-107">**Estimated time toocomplete:** 15 minutes</span></span>

<span data-ttu-id="6c872-108">Zie [Wat is Azure Sleutelkluis?](key-vault-whatis.md) voor algemene informatie over Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="6c872-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c872-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6c872-109">Prerequisites</span></span>
<span data-ttu-id="6c872-110">toocomplete in deze zelfstudie hebt u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="6c872-110">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="6c872-111">Een URI tooa geheim in een Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="6c872-111">A URI tooa secret in an Azure Key Vault</span></span>
* <span data-ttu-id="6c872-112">Een Client-ID en een Clientgeheim voor een webtoepassing die zijn geregistreerd bij Azure Active Directory met toegang tooyour Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="6c872-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access tooyour Key Vault</span></span>
* <span data-ttu-id="6c872-113">Een webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="6c872-113">A web application.</span></span> <span data-ttu-id="6c872-114">We worden Hallo stappen voor een ASP.NET MVC-toepassing geïmplementeerd in Azure als een Web-App weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6c872-114">We will be showing hello steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="6c872-115">Het is essentieel dat u de stappen in Hallo hebt voltooid [aan de slag met Azure Key Vault](key-vault-get-started.md) voor deze zelfstudie zodat er Hallo URI tooa geheim en Hallo Client-ID en Clientgeheim voor een webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="6c872-115">It is essential that you have completed hello steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have hello URI tooa secret and hello Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="6c872-116">Hallo-webtoepassing die toegang krijgen Hallo Sleutelkluis tot is Hallo een dat is geregistreerd in Azure Active Directory en toegang tooyour Sleutelkluis heeft gekregen.</span><span class="sxs-lookup"><span data-stu-id="6c872-116">hello web application that will be accessing hello Key Vault is hello one that is registered in Azure Active Directory and has been given access tooyour Key Vault.</span></span> <span data-ttu-id="6c872-117">Als dit niet Hallo geval is, Ga terug tooRegister een toepassing in Hallo-zelfstudie aan de slag en Herhaal stappen Hallo vermeld.</span><span class="sxs-lookup"><span data-stu-id="6c872-117">If this is not hello case, go back tooRegister an Application in hello Get Started tutorial and repeat hello steps listed.</span></span>

<span data-ttu-id="6c872-118">Deze zelfstudie is ontworpen voor webontwikkelaars die Hallo basisbeginselen van het maken van webtoepassingen in Azure.</span><span class="sxs-lookup"><span data-stu-id="6c872-118">This tutorial is designed for web developers that understand hello basics of creating web applications on Azure.</span></span> <span data-ttu-id="6c872-119">Zie voor meer informatie over Azure Web Apps [overzicht van Web-Apps](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c872-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <span data-ttu-id="6c872-120"><a id="packages"></a>Nuget-pakketten toevoegen</span><span class="sxs-lookup"><span data-stu-id="6c872-120"><a id="packages"></a>Add Nuget Packages</span></span>
<span data-ttu-id="6c872-121">Er zijn twee pakketten die uw webtoepassing toohave geïnstalleerd moet.</span><span class="sxs-lookup"><span data-stu-id="6c872-121">There are two packages that your web application needs toohave installed.</span></span>

* <span data-ttu-id="6c872-122">Active Directory Authentication Library - bevat methoden voor interactie met Azure Active Directory en het beheer van gebruikersidentiteiten</span><span class="sxs-lookup"><span data-stu-id="6c872-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="6c872-123">Azure Key Vault Library - bevat methoden voor interactie met Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="6c872-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="6c872-124">Beide van deze pakketten kunnen worden geïnstalleerd met Package Manager-Console met de opdracht Install-Package Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="6c872-124">Both of these packages can be installed using hello Package Manager Console using hello Install-Package command.</span></span>

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <span data-ttu-id="6c872-125"><a id="webconfig"></a>Web.Config wijzigen</span><span class="sxs-lookup"><span data-stu-id="6c872-125"><a id="webconfig"></a>Modify Web.Config</span></span>
<span data-ttu-id="6c872-126">Er zijn drie toepassingsinstellingen die als volgt toobe toegevoegde toohello web.config-bestand nodig.</span><span class="sxs-lookup"><span data-stu-id="6c872-126">There are three application settings that need toobe added toohello web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="6c872-127">Als u geen toohost uw toepassing als een Azure-Web-App randvoorwaarden, moet u Hallo werkelijke ClientId, Clientgeheim en Secret URI waarden toohello web.config toevoegen. Laat deze dummy-waarden anders omdat we de werkelijke waarden Hallo in hello Azure-Portal voor een extra beveiligingsniveau toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6c872-127">If you are not going toohost your application as an Azure Web App, then you should add hello actual ClientId, Client Secret, and Secret URI values toohello web.config. Otherwise leave these dummy values because we will be adding hello actual values in hello Azure Portal for an additional level of security.</span></span>

## <span data-ttu-id="6c872-128"><a id="gettoken"></a>Methode tooGet een Access-Token toevoegen</span><span class="sxs-lookup"><span data-stu-id="6c872-128"><a id="gettoken"></a>Add Method tooGet an Access Token</span></span>
<span data-ttu-id="6c872-129">In de volgorde toouse Hallo kluis-API-sleutel moet u een toegangstoken.</span><span class="sxs-lookup"><span data-stu-id="6c872-129">In order toouse hello Key Vault API you need an access token.</span></span> <span data-ttu-id="6c872-130">Hallo Sleutelkluis Client aanroepen toohello kluis-API-sleutel, maar u moet toosupply verwerkt met een functie die Hallo-toegangstoken ontvangt uit.</span><span class="sxs-lookup"><span data-stu-id="6c872-130">hello Key Vault Client handles calls toohello Key Vault API but you need toosupply it with a function that gets hello access token.</span></span>  

<span data-ttu-id="6c872-131">Hieronder volgt Hallo code tooget een toegangstoken van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6c872-131">Following is hello code tooget an access token from Azure Active Directory.</span></span> <span data-ttu-id="6c872-132">Deze code overal in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="6c872-132">This code can go anywhere in your application.</span></span> <span data-ttu-id="6c872-133">Ik zoals tooadd een Utils of EncryptionHelper-klasse.</span><span class="sxs-lookup"><span data-stu-id="6c872-133">I like tooadd a Utils or EncryptionHelper class.</span></span>  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property toohold hello secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //hello method that will be provided toohello KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed tooobtain hello JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> <span data-ttu-id="6c872-134">Met behulp van een Client-ID en Clientgeheim is Hallo gemakkelijkste manier tooauthenticate een Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6c872-134">Using a Client ID and Client Secret is hello easiest way tooauthenticate an Azure AD application.</span></span> <span data-ttu-id="6c872-135">En u deze in uw webtoepassing kunt u een scheiding van taken en meer controle over uw Sleutelbeheer.</span><span class="sxs-lookup"><span data-stu-id="6c872-135">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="6c872-136">Maar deze is afhankelijk van de op Hallo Clientgeheim als in uw configuratie-instellingen die voor bepaalde als riskant zijn kunnen als Hallo geheim dat u tooprotect in uw configuratie-instellingen wilt plaatsen.</span><span class="sxs-lookup"><span data-stu-id="6c872-136">But it does rely on putting hello Client Secret in your configuration settings which for some can be as risky as putting hello secret that you want tooprotect in your configuration settings.</span></span> <span data-ttu-id="6c872-137">Hieronder vindt u een bespreking van de manier waarop toouse een Client-ID en het certificaat in plaats van de Client-ID en Clientgeheim tooauthenticate hello Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6c872-137">See below for a discussion on how toouse a Client ID and Certificate instead of Client ID and Client Secret tooauthenticate hello Azure AD application.</span></span>
> 
> 

## <span data-ttu-id="6c872-138"><a id="appstart"></a>Hallo geheim op het starten van de toepassing ophalen</span><span class="sxs-lookup"><span data-stu-id="6c872-138"><a id="appstart"></a>Retrieve hello secret on Application Start</span></span>
<span data-ttu-id="6c872-139">Er moet nu toocall Hallo Sleutelkluis API code en Hallo geheim ophalen.</span><span class="sxs-lookup"><span data-stu-id="6c872-139">Now we need code toocall hello Key Vault API and retrieve hello secret.</span></span> <span data-ttu-id="6c872-140">Hallo volgende code kan worden geplaatst overal, zolang deze wordt aangeroepen voordat u toouse moet het.</span><span class="sxs-lookup"><span data-stu-id="6c872-140">hello following code can be put anywhere as long as it is called before you need toouse it.</span></span> <span data-ttu-id="6c872-141">Ik hebben deze code in Hallo toepassing starten gebeurtenis in Hallo Global.asax geplaatst zodat deze eenmaal wordt uitgevoerd op start en zorgt ervoor dat beschikbaar is voor de toepassing hello geheim Hallo.</span><span class="sxs-lookup"><span data-stu-id="6c872-141">I have put this code in hello Application Start event in hello Global.asax so that it runs once on start and makes hello secret available for hello application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <span data-ttu-id="6c872-142"><a id="portalsettings"></a>App-instellingen toevoegen in hello Azure-Portal (optioneel)</span><span class="sxs-lookup"><span data-stu-id="6c872-142"><a id="portalsettings"></a>Add App Settings in hello Azure Portal (optional)</span></span>
<span data-ttu-id="6c872-143">Als u een Azure-Web-App hebt kunt u nu Hallo werkelijke waarden voor Hallo AppSettings toevoegen in hello Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6c872-143">If you have an Azure Web App you can now add hello actual values for hello AppSettings in hello Azure Portal.</span></span> <span data-ttu-id="6c872-144">Op deze manier Hallo werkelijke waarden worden niet in het bestand web.config Hallo maar beveiligd via Hallo Portal waar u afzonderlijke access control mogelijkheden hebt.</span><span class="sxs-lookup"><span data-stu-id="6c872-144">By doing this, hello actual values will not be in hello web.config but protected via hello Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="6c872-145">Deze waarden wordt vervangen voor Hallo-waarden die u hebt ingevoerd in de web.config. Zorg ervoor dat namen Hallo zijn dezelfde Hallo.</span><span class="sxs-lookup"><span data-stu-id="6c872-145">These values will be substituted for hello values that you entered in your web.config. Make sure that hello names are hello same.</span></span>

![Toepassingsinstellingen weergegeven in Azure Portal][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="6c872-147">Verifiëren met een certificaat in plaats van een Clientgeheim</span><span class="sxs-lookup"><span data-stu-id="6c872-147">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="6c872-148">Er is een andere manier tooauthenticate een Azure AD-toepassing met behulp van een Client-ID en een certificaat in plaats van een Client-ID en Clientgeheim.</span><span class="sxs-lookup"><span data-stu-id="6c872-148">Another way tooauthenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="6c872-149">Hieronder worden Hallo stappen toouse een certificaat in een Azure-Web-App:</span><span class="sxs-lookup"><span data-stu-id="6c872-149">Following are hello steps toouse a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="6c872-150">Maken of een certificaat maken</span><span class="sxs-lookup"><span data-stu-id="6c872-150">Get or Create a Certificate</span></span>
2. <span data-ttu-id="6c872-151">Hallo certificaat koppelen aan een Azure AD-toepassing</span><span class="sxs-lookup"><span data-stu-id="6c872-151">Associate hello Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="6c872-152">Code tooyour Web-App toouse Hallo certificaat toevoegen</span><span class="sxs-lookup"><span data-stu-id="6c872-152">Add code tooyour Web App toouse hello Certificate</span></span>
4. <span data-ttu-id="6c872-153">Een certificaat tooyour Web-App toevoegen</span><span class="sxs-lookup"><span data-stu-id="6c872-153">Add a Certificate tooyour Web App</span></span>

<span data-ttu-id="6c872-154">**Ophalen of maken van een certificaat** voor onze toepassing maken we een testcertificaat.</span><span class="sxs-lookup"><span data-stu-id="6c872-154">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="6c872-155">Hier volgen een aantal opdrachten die u kunt gebruiken in een opdrachtprompt voor ontwikkelaars toocreate een certificaat.</span><span class="sxs-lookup"><span data-stu-id="6c872-155">Here are a couple of commands that you can use in a Developer Command Prompt toocreate a certificate.</span></span> <span data-ttu-id="6c872-156">Wijzig de directory toowhere HALLO cert bestanden die zijn gemaakt gewenste.</span><span class="sxs-lookup"><span data-stu-id="6c872-156">Change directory toowhere you want hello cert files created.</span></span>  <span data-ttu-id="6c872-157">Bovendien Hallo begin en eind van de datum van Hallo certificaat, gebruik voor Hallo huidige datum plus 1 jaar.</span><span class="sxs-lookup"><span data-stu-id="6c872-157">Also, for hello beginning and ending date of hello certificate, use hello current date plus 1 year.</span></span>

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

<span data-ttu-id="6c872-158">Noteer Hallo einddatum en het Hallo-wachtwoord voor Hallo .pfx (in dit voorbeeld: 31-07-2016 en test123).</span><span class="sxs-lookup"><span data-stu-id="6c872-158">Make note of hello end date and hello password for hello .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="6c872-159">U moet ze hieronder.</span><span class="sxs-lookup"><span data-stu-id="6c872-159">You will need them below.</span></span>

<span data-ttu-id="6c872-160">Zie voor meer informatie over het maken van een testcertificaat [hoe: uw eigen testen certificaat maken](https://msdn.microsoft.com/library/ff699202.aspx)</span><span class="sxs-lookup"><span data-stu-id="6c872-160">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="6c872-161">**Koppelen Hallo certificaat met een Azure AD-toepassing** nu u een certificaat hebt, moet u tooassociate deze met een Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6c872-161">**Associate hello Certificate with an Azure AD application** Now that you have a certificate, you need tooassociate it with an Azure AD application.</span></span> <span data-ttu-id="6c872-162">Hello Azure Portal ondersteunt momenteel kan niet in deze werkstroom; Dit kan worden uitgevoerd via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6c872-162">Presently, hello Azure Portal does not support this workflow; this can be completed through PowerShell.</span></span> <span data-ttu-id="6c872-163">Voer Hallo opdrachten tooassoicate Hallo certificaat met de toepassing hello Azure AD te volgen:</span><span class="sxs-lookup"><span data-stu-id="6c872-163">Run hello following commands tooassoicate hello certificate with hello Azure AD application:</span></span>

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get hello thumbprint toouse in your app settings
    $x509.Thumbprint

<span data-ttu-id="6c872-164">Nadat u deze opdrachten hebt uitgevoerd, ziet u de toepassing hello in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c872-164">After you have run these commands, you can see hello application in Azure AD.</span></span> <span data-ttu-id="6c872-165">Wanneer u zoekt, zorg ervoor dat u selecteren 'Toepassingen mijn bedrijf eigenaar is van' in plaats van 'Toepassingen mijn bedrijf gebruikt' in het dialoogvenster voor Hallo zoeken.</span><span class="sxs-lookup"><span data-stu-id="6c872-165">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in hello search dialog.</span></span>

<span data-ttu-id="6c872-166">toolearn meer informatie over Azure AD-toepassingsobjecten en ServicePrincipal-objecten, Zie [toepassingsobjecten en Service-Principal-objecten](../active-directory/active-directory-application-objects.md)</span><span class="sxs-lookup"><span data-stu-id="6c872-166">toolearn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="6c872-167">**Voeg code tooyour Web-App toouse Hallo certificaat** nu we toevoegen zullen code tooyour Web-App tooaccess HALLO cert en deze gebruiken voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="6c872-167">**Add code tooyour Web App toouse hello Certificate** Now we will add code tooyour Web App tooaccess hello cert and use it for authentication.</span></span>

<span data-ttu-id="6c872-168">Er is eerst code tooaccess HALLO cert.</span><span class="sxs-lookup"><span data-stu-id="6c872-168">First there is code tooaccess hello cert.</span></span>

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since hello test root isn't installed.
                if (col == null || col.Count == 0)
                    return null;
                return col[0];
            }
            finally
            {
                store.Close();
            }
        }
    }


<span data-ttu-id="6c872-169">Houd er rekening mee dat Hallo StoreLocation CurrentUser in plaats van de hoofdmap van LocalMachine.</span><span class="sxs-lookup"><span data-stu-id="6c872-169">Note that hello StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="6c872-170">En dat we van 'false' toohello leveren vinden methode als u een test-certificaat.</span><span class="sxs-lookup"><span data-stu-id="6c872-170">And that we are supplying 'false' toohello Find method because we are using a test cert.</span></span>

<span data-ttu-id="6c872-171">Hierna volgt code die gebruikmaakt van Hallo CertificateHelper en maakt een ClientAssertionCertificate die nodig is voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="6c872-171">Next is code that uses hello CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="6c872-172">Hier volgt Hallo nieuwe code tooget Hallo toegangstoken.</span><span class="sxs-lookup"><span data-stu-id="6c872-172">Here is hello new code tooget hello access token.</span></span> <span data-ttu-id="6c872-173">Dit vervangt Hallo GetToken methode hierboven.</span><span class="sxs-lookup"><span data-stu-id="6c872-173">This replaces hello GetToken method above.</span></span> <span data-ttu-id="6c872-174">Deze hebt ik op een andere naam voor het gemak gegeven.</span><span class="sxs-lookup"><span data-stu-id="6c872-174">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="6c872-175">Alle deze code hebt ik geplaatst in mijn Web-App-project Utils-klasse voor eenvoudig te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6c872-175">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="6c872-176">Hallo laatste code gewijzigd is Hallo Application_Start methode.</span><span class="sxs-lookup"><span data-stu-id="6c872-176">hello last code change is in hello Application_Start method.</span></span> <span data-ttu-id="6c872-177">Er moet eerst toocall hello GetCert() methode tooload hello ClientAssertionCertificate.</span><span class="sxs-lookup"><span data-stu-id="6c872-177">First we need toocall hello GetCert() method tooload hello ClientAssertionCertificate.</span></span> <span data-ttu-id="6c872-178">En wijzig vervolgens we Hallo retouraanroepmethode die we bij het maken van een nieuwe KeyVaultClient leveren.</span><span class="sxs-lookup"><span data-stu-id="6c872-178">And then we change hello callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="6c872-179">Houd er rekening mee dat dit Hallo-code die vervangt hierboven zijn.</span><span class="sxs-lookup"><span data-stu-id="6c872-179">Note that this replaces hello code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="6c872-180">**Toevoegen van een certificaat tooyour Web-App via Azure Portal Hallo** toevoegen van een certificaat tooyour Web-App is een eenvoudig proces.</span><span class="sxs-lookup"><span data-stu-id="6c872-180">**Add a Certificate tooyour Web App through hello Azure Portal** Adding a Certificate tooyour Web App is a simple two-step process.</span></span> <span data-ttu-id="6c872-181">Eerst gaan toohello Azure-Portal en navigeer tooyour Web-App.</span><span class="sxs-lookup"><span data-stu-id="6c872-181">First, go toohello Azure Portal and navigate tooyour Web App.</span></span> <span data-ttu-id="6c872-182">Klik op Hallo blade van de instellingen voor uw Web-App, op Hallo-vermelding voor 'aangepaste domeinen en SSL'.</span><span class="sxs-lookup"><span data-stu-id="6c872-182">On hello Settings blade for your Web App, click on hello entry for "Custom domains and SSL".</span></span> <span data-ttu-id="6c872-183">Op Hallo blade die wordt geopend u kunnen tooupload Hallo certificaat dat u hiervoor KVWebApp.pfx hebt gemaakt, worden zorg ervoor dat u het wachtwoord voor pfx Hallo Hallo onthoudt.</span><span class="sxs-lookup"><span data-stu-id="6c872-183">On hello blade that opens you will be able tooupload hello Certificate that you created above, KVWebApp.pfx, make sure that you remember hello password for hello pfx.</span></span>

![Toevoegen van een certificaat tooa Web-App in hello Azure Portal][2]

<span data-ttu-id="6c872-185">Hallo ding dat u nodig hebt toodo is een toepassingsinstelling tooyour Web-App die Hallo naam WEBSITE is tooadd\_LOAD\_certificaten en een waarde van *.</span><span class="sxs-lookup"><span data-stu-id="6c872-185">hello last thing that you need toodo is tooadd an Application Setting tooyour Web App that has hello name WEBSITE\_LOAD\_CERTIFICATES and a value of *.</span></span> <span data-ttu-id="6c872-186">Dit zorgt ervoor dat alle certificaten zijn geladen.</span><span class="sxs-lookup"><span data-stu-id="6c872-186">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="6c872-187">Als u deze wilde tooload alleen Hallo van certificaten die u hebt geüpload en vervolgens kunt u een door komma's gescheiden lijst met de vingerafdrukken.</span><span class="sxs-lookup"><span data-stu-id="6c872-187">If you wanted tooload only hello Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="6c872-188">Zie toolearn meer informatie over het toevoegen van een certificaat tooa Web-App [met behulp van certificaten in toepassingen met Azure Websites](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span><span class="sxs-lookup"><span data-stu-id="6c872-188">toolearn more about adding a Certificate tooa Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="6c872-189">**Een certificaat tooKey kluis toevoegen als een geheim** in plaats van uw certificaat toohello Web-App service rechtstreeks uploaden, kunt u opslaan in de Sleutelkluis als een geheim en het implementeren van daaruit.</span><span class="sxs-lookup"><span data-stu-id="6c872-189">**Add a Certificate tooKey Vault as a secret** Instead of uploading your certificate toohello Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="6c872-190">Dit is een proces in twee stappen die wordt beschreven in het volgende blogbericht Hallo [Azure Web App certificaat implementeren via Sleutelkluis](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="6c872-190">This is a two-step process that is outlined in hello following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <span data-ttu-id="6c872-191"><a id="next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6c872-191"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="6c872-192">Zie voor het programmeren van verwijzingen [Azure Key Vault C#-Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c872-192">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
