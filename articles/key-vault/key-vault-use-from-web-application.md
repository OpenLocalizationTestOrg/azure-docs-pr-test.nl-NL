---
title: Azure Sleutelkluis in een webtoepassing gebruiken | Microsoft Docs
description: Met deze zelfstudie kunt u informatie over het gebruik van Azure Sleutelkluis in een webtoepassing.
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
ms.openlocfilehash: d095bcfe37baefa90cf79bb48bff3f703ce1dad7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="18ab4-103">Azure Sleutelkluis in een webtoepassing gebruiken</span><span class="sxs-lookup"><span data-stu-id="18ab4-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="18ab4-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="18ab4-104">Introduction</span></span>
<span data-ttu-id="18ab4-105">Met deze zelfstudie kunt u informatie over het gebruik van Azure Sleutelkluis in een webtoepassing in Azure.</span><span class="sxs-lookup"><span data-stu-id="18ab4-105">Use this tutorial to help you learn how to use Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="18ab4-106">Dit helpt u bij het proces voor het openen van een geheim van een Azure Sleutelkluis, zodat deze kan worden gebruikt in uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="18ab4-106">It walks you through the process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="18ab4-107">**Geschatte duur:** 15 minuten</span><span class="sxs-lookup"><span data-stu-id="18ab4-107">**Estimated time to complete:** 15 minutes</span></span>

<span data-ttu-id="18ab4-108">Zie [Wat is Azure Sleutelkluis?](key-vault-whatis.md) voor algemene informatie over Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="18ab4-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18ab4-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="18ab4-109">Prerequisites</span></span>
<span data-ttu-id="18ab4-110">U hebt het volgende nodig om deze zelfstudie te voltooien:</span><span class="sxs-lookup"><span data-stu-id="18ab4-110">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="18ab4-111">Een URI naar een geheim in een Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="18ab4-111">A URI to a secret in an Azure Key Vault</span></span>
* <span data-ttu-id="18ab4-112">Een Client-ID en een Clientgeheim voor een webtoepassing die zijn geregistreerd bij Azure Active Directory die toegang tot uw Sleutelkluis heeft</span><span class="sxs-lookup"><span data-stu-id="18ab4-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access to your Key Vault</span></span>
* <span data-ttu-id="18ab4-113">Een webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="18ab4-113">A web application.</span></span> <span data-ttu-id="18ab4-114">We worden de stappen voor een ASP.NET MVC-toepassing geïmplementeerd in Azure als een Web-App weergegeven.</span><span class="sxs-lookup"><span data-stu-id="18ab4-114">We will be showing the steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="18ab4-115">Het is essentieel dat u de stappen in hebt voltooid [aan de slag met Azure Key Vault](key-vault-get-started.md) voor deze zelfstudie zodat u de URI moet een geheim en de Client-ID en Clientgeheim voor een webtoepassing hebt.</span><span class="sxs-lookup"><span data-stu-id="18ab4-115">It is essential that you have completed the steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have the URI to a secret and the Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="18ab4-116">De webtoepassing die toegang krijgen de Sleutelkluis tot is het adres dat is geregistreerd in Azure Active Directory en toegang heeft gekregen tot uw Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="18ab4-116">The web application that will be accessing the Key Vault is the one that is registered in Azure Active Directory and has been given access to your Key Vault.</span></span> <span data-ttu-id="18ab4-117">Als dit niet het geval is, gaat u terug naar Register een toepassing in de zelfstudie aan de slag en Herhaal de stappen die worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="18ab4-117">If this is not the case, go back to Register an Application in the Get Started tutorial and repeat the steps listed.</span></span>

<span data-ttu-id="18ab4-118">Deze zelfstudie is ontworpen voor webontwikkelaars die de basisbeginselen van het maken van webtoepassingen in Azure.</span><span class="sxs-lookup"><span data-stu-id="18ab4-118">This tutorial is designed for web developers that understand the basics of creating web applications on Azure.</span></span> <span data-ttu-id="18ab4-119">Zie voor meer informatie over Azure Web Apps [overzicht van Web-Apps](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="18ab4-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <span data-ttu-id="18ab4-120"><a id="packages"></a>Nuget-pakketten toevoegen</span><span class="sxs-lookup"><span data-stu-id="18ab4-120"><a id="packages"></a>Add Nuget Packages</span></span>
<span data-ttu-id="18ab4-121">Er zijn twee pakketten die u moet uw webtoepassing hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="18ab4-121">There are two packages that your web application needs to have installed.</span></span>

* <span data-ttu-id="18ab4-122">Active Directory Authentication Library - bevat methoden voor interactie met Azure Active Directory en het beheer van gebruikersidentiteiten</span><span class="sxs-lookup"><span data-stu-id="18ab4-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="18ab4-123">Azure Key Vault Library - bevat methoden voor interactie met Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="18ab4-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="18ab4-124">Beide van deze pakketten kunnen worden geïnstalleerd met behulp van de Package Manager-Console met de opdracht Install-Package.</span><span class="sxs-lookup"><span data-stu-id="18ab4-124">Both of these packages can be installed using the Package Manager Console using the Install-Package command.</span></span>

    // this is currently the latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <span data-ttu-id="18ab4-125"><a id="webconfig"></a>Web.Config wijzigen</span><span class="sxs-lookup"><span data-stu-id="18ab4-125"><a id="webconfig"></a>Modify Web.Config</span></span>
<span data-ttu-id="18ab4-126">Er zijn drie toepassingsinstellingen die moeten worden toegevoegd aan het bestand web.config als volgt.</span><span class="sxs-lookup"><span data-stu-id="18ab4-126">There are three application settings that need to be added to the web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer to the web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is the URI for the secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="18ab4-127">Als u geen randvoorwaarden voor het hosten van uw toepassing als een Azure-Web-App, moet u de werkelijke waarden van ClientId, Clientgeheim en Secret URI toevoegen aan het bestand web.config.</span><span class="sxs-lookup"><span data-stu-id="18ab4-127">If you are not going to host your application as an Azure Web App, then you should add the actual ClientId, Client Secret, and Secret URI values to the web.config.</span></span> <span data-ttu-id="18ab4-128">Laat deze dummy-waarden anders omdat we de werkelijke waarden in de Azure-Portal voor een extra beveiligingsniveau toevoegen.</span><span class="sxs-lookup"><span data-stu-id="18ab4-128">Otherwise leave these dummy values because we will be adding the actual values in the Azure Portal for an additional level of security.</span></span>

## <span data-ttu-id="18ab4-129"><a id="gettoken"></a>Methode voor een toegangstoken ophalen toevoegen</span><span class="sxs-lookup"><span data-stu-id="18ab4-129"><a id="gettoken"></a>Add Method to Get an Access Token</span></span>
<span data-ttu-id="18ab4-130">Als u wilt gebruikmaken van de kluis-API-sleutel moet u een toegangstoken.</span><span class="sxs-lookup"><span data-stu-id="18ab4-130">In order to use the Key Vault API you need an access token.</span></span> <span data-ttu-id="18ab4-131">De Sleutelkluis Client aanroepen naar de kluis-API-sleutel verwerkt, maar moet u deze met een functie die het toegangstoken ontvangt uit opgeven.</span><span class="sxs-lookup"><span data-stu-id="18ab4-131">The Key Vault Client handles calls to the Key Vault API but you need to supply it with a function that gets the access token.</span></span>  

<span data-ttu-id="18ab4-132">Hieronder volgt de code voor een toegangstoken ophalen uit Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="18ab4-132">Following is the code to get an access token from Azure Active Directory.</span></span> <span data-ttu-id="18ab4-133">Deze code overal in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="18ab4-133">This code can go anywhere in your application.</span></span> <span data-ttu-id="18ab4-134">Ik wil graag een klasse Utils of EncryptionHelper toevoegen.</span><span class="sxs-lookup"><span data-stu-id="18ab4-134">I like to add a Utils or EncryptionHelper class.</span></span>  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property to hold the secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //the method that will be provided to the KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed to obtain the JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> <span data-ttu-id="18ab4-135">Met behulp van een Client-ID en Clientgeheim is de eenvoudigste manier om te verifiëren van een Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="18ab4-135">Using a Client ID and Client Secret is the easiest way to authenticate an Azure AD application.</span></span> <span data-ttu-id="18ab4-136">En u deze in uw webtoepassing kunt u een scheiding van taken en meer controle over uw Sleutelbeheer.</span><span class="sxs-lookup"><span data-stu-id="18ab4-136">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="18ab4-137">Maar deze maakt gebruik van de Client-Secret als in uw configuratie-instellingen die voor bepaalde als riskant als het plaatsen van het geheim dat u wilt beveiligen in uw configuratie-instellingen kunnen worden.</span><span class="sxs-lookup"><span data-stu-id="18ab4-137">But it does rely on putting the Client Secret in your configuration settings which for some can be as risky as putting the secret that you want to protect in your configuration settings.</span></span> <span data-ttu-id="18ab4-138">Hieronder vindt u een discussie over het gebruik van een Client-ID en het certificaat in plaats van de Client-ID en Clientgeheim om te verifiëren van de Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="18ab4-138">See below for a discussion on how to use a Client ID and Certificate instead of Client ID and Client Secret to authenticate the Azure AD application.</span></span>
> 
> 

## <span data-ttu-id="18ab4-139"><a id="appstart"></a>Ophalen van het geheim op toepassing starten</span><span class="sxs-lookup"><span data-stu-id="18ab4-139"><a id="appstart"></a>Retrieve the secret on Application Start</span></span>
<span data-ttu-id="18ab4-140">Er moet nu code roept u de kluis-API-sleutel en het geheim ophalen.</span><span class="sxs-lookup"><span data-stu-id="18ab4-140">Now we need code to call the Key Vault API and retrieve the secret.</span></span> <span data-ttu-id="18ab4-141">De volgende code kan overal worden geplaatst, zolang deze wordt aangeroepen voordat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="18ab4-141">The following code can be put anywhere as long as it is called before you need to use it.</span></span> <span data-ttu-id="18ab4-142">Ik hebben deze code in de toepassing gestart gebeurtenis in het bestand Global.asax plaatsen, zodat er wordt één keer worden uitgevoerd op start en het geheim voor de toepassing beschikbaar wordt.</span><span class="sxs-lookup"><span data-stu-id="18ab4-142">I have put this code in the Application Start event in the Global.asax so that it runs once on start and makes the secret available for the application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class to hold the secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <span data-ttu-id="18ab4-143"><a id="portalsettings"></a>App-instellingen toevoegen in de Azure-Portal (optioneel)</span><span class="sxs-lookup"><span data-stu-id="18ab4-143"><a id="portalsettings"></a>Add App Settings in the Azure Portal (optional)</span></span>
<span data-ttu-id="18ab4-144">U kunt nu de werkelijke waarden toevoegen voor de AppSettings in de Azure Portal, als u een Azure-Web-App hebt.</span><span class="sxs-lookup"><span data-stu-id="18ab4-144">If you have an Azure Web App you can now add the actual values for the AppSettings in the Azure Portal.</span></span> <span data-ttu-id="18ab4-145">Op deze manier worden de werkelijke waarden worden niet in de web.config maar beveiligd via de Portal waar u afzonderlijke access control mogelijkheden hebt.</span><span class="sxs-lookup"><span data-stu-id="18ab4-145">By doing this, the actual values will not be in the web.config but protected via the Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="18ab4-146">Deze waarden wordt vervangen voor de waarden die u hebt ingevoerd in de web.config.</span><span class="sxs-lookup"><span data-stu-id="18ab4-146">These values will be substituted for the values that you entered in your web.config.</span></span> <span data-ttu-id="18ab4-147">Zorg ervoor dat de namen hetzelfde zijn.</span><span class="sxs-lookup"><span data-stu-id="18ab4-147">Make sure that the names are the same.</span></span>

![Toepassingsinstellingen weergegeven in Azure Portal][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="18ab4-149">Verifiëren met een certificaat in plaats van een Clientgeheim</span><span class="sxs-lookup"><span data-stu-id="18ab4-149">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="18ab4-150">Er is een andere manier om te verifiëren van een Azure AD-toepassing met behulp van een Client-ID en een certificaat in plaats van een Client-ID en Clientgeheim.</span><span class="sxs-lookup"><span data-stu-id="18ab4-150">Another way to authenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="18ab4-151">Hieronder volgen de stappen voor het gebruik van een certificaat in een Azure-Web-App:</span><span class="sxs-lookup"><span data-stu-id="18ab4-151">Following are the steps to use a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="18ab4-152">Maken of een certificaat maken</span><span class="sxs-lookup"><span data-stu-id="18ab4-152">Get or Create a Certificate</span></span>
2. <span data-ttu-id="18ab4-153">Het certificaat koppelen aan een Azure AD-toepassing</span><span class="sxs-lookup"><span data-stu-id="18ab4-153">Associate the Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="18ab4-154">Voeg code toe aan uw Web-App om het certificaat te gebruiken</span><span class="sxs-lookup"><span data-stu-id="18ab4-154">Add code to your Web App to use the Certificate</span></span>
4. <span data-ttu-id="18ab4-155">Een certificaat toevoegen aan uw Web-App</span><span class="sxs-lookup"><span data-stu-id="18ab4-155">Add a Certificate to your Web App</span></span>

<span data-ttu-id="18ab4-156">**Ophalen of maken van een certificaat** voor onze toepassing maken we een testcertificaat.</span><span class="sxs-lookup"><span data-stu-id="18ab4-156">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="18ab4-157">Hier volgen een aantal opdrachten die u in een opdrachtprompt voor ontwikkelaars kunt gebruiken om een certificaat te maken.</span><span class="sxs-lookup"><span data-stu-id="18ab4-157">Here are a couple of commands that you can use in a Developer Command Prompt to create a certificate.</span></span> <span data-ttu-id="18ab4-158">Wijzig de directory aan waar u het certificaat dat bestanden die zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="18ab4-158">Change directory to where you want the cert files created.</span></span>  <span data-ttu-id="18ab4-159">Gebruik ook, voor het begin- en einddatum van het certificaat, de huidige datum plus 1 jaar.</span><span class="sxs-lookup"><span data-stu-id="18ab4-159">Also, for the beginning and ending date of the certificate, use the current date plus 1 year.</span></span>

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

<span data-ttu-id="18ab4-160">Noteer de einddatum en het wachtwoord voor de .pfx (in dit voorbeeld: 31-07-2016 en test123).</span><span class="sxs-lookup"><span data-stu-id="18ab4-160">Make note of the end date and the password for the .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="18ab4-161">U moet ze hieronder.</span><span class="sxs-lookup"><span data-stu-id="18ab4-161">You will need them below.</span></span>

<span data-ttu-id="18ab4-162">Zie voor meer informatie over het maken van een testcertificaat [hoe: uw eigen testen certificaat maken](https://msdn.microsoft.com/library/ff699202.aspx)</span><span class="sxs-lookup"><span data-stu-id="18ab4-162">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="18ab4-163">**Het certificaat koppelen aan een Azure AD-toepassing** nu dat u een certificaat hebt, moet u deze koppelen aan een Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="18ab4-163">**Associate the Certificate with an Azure AD application** Now that you have a certificate, you need to associate it with an Azure AD application.</span></span> <span data-ttu-id="18ab4-164">De Azure Portal ondersteunt momenteel kan niet in deze werkstroom; Dit kan worden uitgevoerd via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="18ab4-164">Presently, the Azure Portal does not support this workflow; this can be completed through PowerShell.</span></span> <span data-ttu-id="18ab4-165">Voer de volgende opdrachten voor assoicate het certificaat met de Azure AD-toepassing:</span><span class="sxs-lookup"><span data-stu-id="18ab4-165">Run the following commands to assoicate the certificate with the Azure AD application:</span></span>

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get the thumbprint to use in your app settings
    $x509.Thumbprint

<span data-ttu-id="18ab4-166">Nadat u deze opdrachten hebt uitgevoerd, ziet u de toepassing in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18ab4-166">After you have run these commands, you can see the application in Azure AD.</span></span> <span data-ttu-id="18ab4-167">Wanneer u zoekt, zorg ervoor dat u selecteert u 'Toepassingen mijn bedrijf eigenaar is van' in plaats van 'Toepassingen mijn bedrijf gebruikt' in het Zoekdialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="18ab4-167">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in the search dialog.</span></span>

<span data-ttu-id="18ab4-168">Zie voor meer informatie over Azure AD-toepassing en ServicePrincipal-objecten, [toepassingsobjecten en Service-Principal-objecten](../active-directory/active-directory-application-objects.md)</span><span class="sxs-lookup"><span data-stu-id="18ab4-168">To learn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="18ab4-169">**Voeg code toe aan uw Web-App om het certificaat te gebruiken** nu we code aan uw Web-App toevoegen wordt voor toegang tot het certificaat en deze gebruiken voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="18ab4-169">**Add code to your Web App to use the Certificate** Now we will add code to your Web App to access the cert and use it for authentication.</span></span>

<span data-ttu-id="18ab4-170">Er is eerst code voor toegang tot het certificaat.</span><span class="sxs-lookup"><span data-stu-id="18ab4-170">First there is code to access the cert.</span></span>

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since the test root isn't installed.
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


<span data-ttu-id="18ab4-171">Houd er rekening mee dat de StoreLocation CurrentUser in plaats van de hoofdmap van LocalMachine is.</span><span class="sxs-lookup"><span data-stu-id="18ab4-171">Note that the StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="18ab4-172">En dat we 'false' aan de methode vinden levert als u een test-certificaat.</span><span class="sxs-lookup"><span data-stu-id="18ab4-172">And that we are supplying 'false' to the Find method because we are using a test cert.</span></span>

<span data-ttu-id="18ab4-173">Hierna volgt code die gebruikmaakt van de CertificateHelper en maakt een ClientAssertionCertificate die nodig is voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="18ab4-173">Next is code that uses the CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="18ab4-174">Hier wordt de nieuwe code voor het ophalen van het toegangstoken.</span><span class="sxs-lookup"><span data-stu-id="18ab4-174">Here is the new code to get the access token.</span></span> <span data-ttu-id="18ab4-175">Hiermee vervangt u de bovenstaande GetToken-methode.</span><span class="sxs-lookup"><span data-stu-id="18ab4-175">This replaces the GetToken method above.</span></span> <span data-ttu-id="18ab4-176">Deze hebt ik op een andere naam voor het gemak gegeven.</span><span class="sxs-lookup"><span data-stu-id="18ab4-176">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="18ab4-177">Alle deze code hebt ik geplaatst in mijn Web-App-project Utils-klasse voor eenvoudig te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="18ab4-177">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="18ab4-178">De laatste codewijziging is in de methode Application_Start.</span><span class="sxs-lookup"><span data-stu-id="18ab4-178">The last code change is in the Application_Start method.</span></span> <span data-ttu-id="18ab4-179">Eerst moet de GetCert() methode aanroepen om de ClientAssertionCertificate laden.</span><span class="sxs-lookup"><span data-stu-id="18ab4-179">First we need to call the GetCert() method to load the ClientAssertionCertificate.</span></span> <span data-ttu-id="18ab4-180">En wijzig vervolgens we de retouraanroepmethode die we bij het maken van een nieuwe KeyVaultClient leveren.</span><span class="sxs-lookup"><span data-stu-id="18ab4-180">And then we change the callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="18ab4-181">Houd er rekening mee dat Hiermee vervangt u de code die hierboven zijn.</span><span class="sxs-lookup"><span data-stu-id="18ab4-181">Note that this replaces the code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="18ab4-182">**Een certificaat toevoegen aan uw Web-App via de Azure-Portal** een certificaat toevoegen aan uw Web-App is een eenvoudig proces.</span><span class="sxs-lookup"><span data-stu-id="18ab4-182">**Add a Certificate to your Web App through the Azure Portal** Adding a Certificate to your Web App is a simple two-step process.</span></span> <span data-ttu-id="18ab4-183">Eerst, gaat u naar de Azure-Portal en navigeer naar uw Web-App.</span><span class="sxs-lookup"><span data-stu-id="18ab4-183">First, go to the Azure Portal and navigate to your Web App.</span></span> <span data-ttu-id="18ab4-184">Klik op de vermelding voor 'aangepaste domeinen en SSL' in de blade instellingen voor uw Web-App.</span><span class="sxs-lookup"><span data-stu-id="18ab4-184">On the Settings blade for your Web App, click on the entry for "Custom domains and SSL".</span></span> <span data-ttu-id="18ab4-185">Op de blade die wordt geopend dat u zich voor het uploaden van het certificaat dat u hiervoor KVWebApp.pfx hebt gemaakt, zorg ervoor dat u het wachtwoord voor de pfx onthoudt.</span><span class="sxs-lookup"><span data-stu-id="18ab4-185">On the blade that opens you will be able to upload the Certificate that you created above, KVWebApp.pfx, make sure that you remember the password for the pfx.</span></span>

![Een certificaat toevoegen aan een Web-App in de Azure Portal][2]

<span data-ttu-id="18ab4-187">De laatste stap die u moet doen is een toepassingsinstelling toevoegen aan uw Web-App met de naam WEBSITE\_LOAD\_certificaten en een waarde van *.</span><span class="sxs-lookup"><span data-stu-id="18ab4-187">The last thing that you need to do is to add an Application Setting to your Web App that has the name WEBSITE\_LOAD\_CERTIFICATES and a value of *.</span></span> <span data-ttu-id="18ab4-188">Dit zorgt ervoor dat alle certificaten zijn geladen.</span><span class="sxs-lookup"><span data-stu-id="18ab4-188">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="18ab4-189">Als u laden, alleen de certificaten die u hebt geüpload wilt, kunt u een door komma's gescheiden lijst met de vingerafdrukken invoeren.</span><span class="sxs-lookup"><span data-stu-id="18ab4-189">If you wanted to load only the Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="18ab4-190">Zie voor meer informatie over het toevoegen van een certificaat aan een Web-App, [met behulp van certificaten in toepassingen met Azure Websites](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span><span class="sxs-lookup"><span data-stu-id="18ab4-190">To learn more about adding a Certificate to a Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="18ab4-191">**Een certificaat toevoegen aan de Sleutelkluis als een geheim** in plaats van rechtstreeks uw certificaat uploaden naar de Web-App service, kunt u opslaan in de Sleutelkluis als een geheim en het implementeren van daaruit.</span><span class="sxs-lookup"><span data-stu-id="18ab4-191">**Add a Certificate to Key Vault as a secret** Instead of uploading your certificate to the Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="18ab4-192">Dit is een proces in twee stappen die wordt beschreven in het volgende blogbericht [Azure Web App certificaat implementeren via Sleutelkluis](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="18ab4-192">This is a two-step process that is outlined in the following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <span data-ttu-id="18ab4-193"><a id="next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="18ab4-193"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="18ab4-194">Zie voor het programmeren van verwijzingen [Azure Key Vault C#-Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span><span class="sxs-lookup"><span data-stu-id="18ab4-194">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
