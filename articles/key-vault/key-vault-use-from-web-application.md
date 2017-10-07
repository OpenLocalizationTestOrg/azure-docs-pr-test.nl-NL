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
# <a name="use-azure-key-vault-from-a-web-application"></a>Azure Sleutelkluis in een webtoepassing gebruiken
## <a name="introduction"></a>Inleiding
Gebruik deze zelfstudie toohelp leert u hoe toouse Azure Key Vault vanuit een webtoepassing in Azure. Dit helpt u bij het Hallo-proces voor het openen van een geheim van een Azure Sleutelkluis, zodat deze kan worden gebruikt in uw webtoepassing.

**Geschatte tijd toocomplete:** 15 minuten

Zie [Wat is Azure Sleutelkluis?](key-vault-whatis.md) voor algemene informatie over Azure Sleutelkluis.

## <a name="prerequisites"></a>Vereisten
toocomplete in deze zelfstudie hebt u hello te volgen:

* Een URI tooa geheim in een Azure Sleutelkluis
* Een Client-ID en een Clientgeheim voor een webtoepassing die zijn geregistreerd bij Azure Active Directory met toegang tooyour Sleutelkluis
* Een webtoepassing. We worden Hallo stappen voor een ASP.NET MVC-toepassing geïmplementeerd in Azure als een Web-App weergegeven.

> [!NOTE]
> Het is essentieel dat u de stappen in Hallo hebt voltooid [aan de slag met Azure Key Vault](key-vault-get-started.md) voor deze zelfstudie zodat er Hallo URI tooa geheim en Hallo Client-ID en Clientgeheim voor een webtoepassing.
> 
> 

Hallo-webtoepassing die toegang krijgen Hallo Sleutelkluis tot is Hallo een dat is geregistreerd in Azure Active Directory en toegang tooyour Sleutelkluis heeft gekregen. Als dit niet Hallo geval is, Ga terug tooRegister een toepassing in Hallo-zelfstudie aan de slag en Herhaal stappen Hallo vermeld.

Deze zelfstudie is ontworpen voor webontwikkelaars die Hallo basisbeginselen van het maken van webtoepassingen in Azure. Zie voor meer informatie over Azure Web Apps [overzicht van Web-Apps](../app-service-web/app-service-web-overview.md).

## <a id="packages"></a>Nuget-pakketten toevoegen
Er zijn twee pakketten die uw webtoepassing toohave geïnstalleerd moet.

* Active Directory Authentication Library - bevat methoden voor interactie met Azure Active Directory en het beheer van gebruikersidentiteiten
* Azure Key Vault Library - bevat methoden voor interactie met Azure Key Vault

Beide van deze pakketten kunnen worden geïnstalleerd met Package Manager-Console met de opdracht Install-Package Hallo Hallo.

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <a id="webconfig"></a>Web.Config wijzigen
Er zijn drie toepassingsinstellingen die als volgt toobe toegevoegde toohello web.config-bestand nodig.

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


Als u geen toohost uw toepassing als een Azure-Web-App randvoorwaarden, moet u Hallo werkelijke ClientId, Clientgeheim en Secret URI waarden toohello web.config toevoegen. Laat deze dummy-waarden anders omdat we de werkelijke waarden Hallo in hello Azure-Portal voor een extra beveiligingsniveau toevoegen.

## <a id="gettoken"></a>Methode tooGet een Access-Token toevoegen
In de volgorde toouse Hallo kluis-API-sleutel moet u een toegangstoken. Hallo Sleutelkluis Client aanroepen toohello kluis-API-sleutel, maar u moet toosupply verwerkt met een functie die Hallo-toegangstoken ontvangt uit.  

Hieronder volgt Hallo code tooget een toegangstoken van Azure Active Directory. Deze code overal in uw toepassing. Ik zoals tooadd een Utils of EncryptionHelper-klasse.  

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
> Met behulp van een Client-ID en Clientgeheim is Hallo gemakkelijkste manier tooauthenticate een Azure AD-toepassing. En u deze in uw webtoepassing kunt u een scheiding van taken en meer controle over uw Sleutelbeheer. Maar deze is afhankelijk van de op Hallo Clientgeheim als in uw configuratie-instellingen die voor bepaalde als riskant zijn kunnen als Hallo geheim dat u tooprotect in uw configuratie-instellingen wilt plaatsen. Hieronder vindt u een bespreking van de manier waarop toouse een Client-ID en het certificaat in plaats van de Client-ID en Clientgeheim tooauthenticate hello Azure AD-toepassing.
> 
> 

## <a id="appstart"></a>Hallo geheim op het starten van de toepassing ophalen
Er moet nu toocall Hallo Sleutelkluis API code en Hallo geheim ophalen. Hallo volgende code kan worden geplaatst overal, zolang deze wordt aangeroepen voordat u toouse moet het. Ik hebben deze code in Hallo toepassing starten gebeurtenis in Hallo Global.asax geplaatst zodat deze eenmaal wordt uitgevoerd op start en zorgt ervoor dat beschikbaar is voor de toepassing hello geheim Hallo.

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <a id="portalsettings"></a>App-instellingen toevoegen in hello Azure-Portal (optioneel)
Als u een Azure-Web-App hebt kunt u nu Hallo werkelijke waarden voor Hallo AppSettings toevoegen in hello Azure Portal. Op deze manier Hallo werkelijke waarden worden niet in het bestand web.config Hallo maar beveiligd via Hallo Portal waar u afzonderlijke access control mogelijkheden hebt. Deze waarden wordt vervangen voor Hallo-waarden die u hebt ingevoerd in de web.config. Zorg ervoor dat namen Hallo zijn dezelfde Hallo.

![Toepassingsinstellingen weergegeven in Azure Portal][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a>Verifiëren met een certificaat in plaats van een Clientgeheim
Er is een andere manier tooauthenticate een Azure AD-toepassing met behulp van een Client-ID en een certificaat in plaats van een Client-ID en Clientgeheim. Hieronder worden Hallo stappen toouse een certificaat in een Azure-Web-App:

1. Maken of een certificaat maken
2. Hallo certificaat koppelen aan een Azure AD-toepassing
3. Code tooyour Web-App toouse Hallo certificaat toevoegen
4. Een certificaat tooyour Web-App toevoegen

**Ophalen of maken van een certificaat** voor onze toepassing maken we een testcertificaat. Hier volgen een aantal opdrachten die u kunt gebruiken in een opdrachtprompt voor ontwikkelaars toocreate een certificaat. Wijzig de directory toowhere HALLO cert bestanden die zijn gemaakt gewenste.  Bovendien Hallo begin en eind van de datum van Hallo certificaat, gebruik voor Hallo huidige datum plus 1 jaar.

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

Noteer Hallo einddatum en het Hallo-wachtwoord voor Hallo .pfx (in dit voorbeeld: 31-07-2016 en test123). U moet ze hieronder.

Zie voor meer informatie over het maken van een testcertificaat [hoe: uw eigen testen certificaat maken](https://msdn.microsoft.com/library/ff699202.aspx)

**Koppelen Hallo certificaat met een Azure AD-toepassing** nu u een certificaat hebt, moet u tooassociate deze met een Azure AD-toepassing. Hello Azure Portal ondersteunt momenteel kan niet in deze werkstroom; Dit kan worden uitgevoerd via PowerShell. Voer Hallo opdrachten tooassoicate Hallo certificaat met de toepassing hello Azure AD te volgen:

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

Nadat u deze opdrachten hebt uitgevoerd, ziet u de toepassing hello in Azure AD. Wanneer u zoekt, zorg ervoor dat u selecteren 'Toepassingen mijn bedrijf eigenaar is van' in plaats van 'Toepassingen mijn bedrijf gebruikt' in het dialoogvenster voor Hallo zoeken.

toolearn meer informatie over Azure AD-toepassingsobjecten en ServicePrincipal-objecten, Zie [toepassingsobjecten en Service-Principal-objecten](../active-directory/active-directory-application-objects.md)

**Voeg code tooyour Web-App toouse Hallo certificaat** nu we toevoegen zullen code tooyour Web-App tooaccess HALLO cert en deze gebruiken voor verificatie.

Er is eerst code tooaccess HALLO cert.

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


Houd er rekening mee dat Hallo StoreLocation CurrentUser in plaats van de hoofdmap van LocalMachine. En dat we van 'false' toohello leveren vinden methode als u een test-certificaat.

Hierna volgt code die gebruikmaakt van Hallo CertificateHelper en maakt een ClientAssertionCertificate die nodig is voor verificatie.

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


Hier volgt Hallo nieuwe code tooget Hallo toegangstoken. Dit vervangt Hallo GetToken methode hierboven. Deze hebt ik op een andere naam voor het gemak gegeven.

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

Alle deze code hebt ik geplaatst in mijn Web-App-project Utils-klasse voor eenvoudig te gebruiken.

Hallo laatste code gewijzigd is Hallo Application_Start methode. Er moet eerst toocall hello GetCert() methode tooload hello ClientAssertionCertificate. En wijzig vervolgens we Hallo retouraanroepmethode die we bij het maken van een nieuwe KeyVaultClient leveren. Houd er rekening mee dat dit Hallo-code die vervangt hierboven zijn.

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


**Toevoegen van een certificaat tooyour Web-App via Azure Portal Hallo** toevoegen van een certificaat tooyour Web-App is een eenvoudig proces. Eerst gaan toohello Azure-Portal en navigeer tooyour Web-App. Klik op Hallo blade van de instellingen voor uw Web-App, op Hallo-vermelding voor 'aangepaste domeinen en SSL'. Op Hallo blade die wordt geopend u kunnen tooupload Hallo certificaat dat u hiervoor KVWebApp.pfx hebt gemaakt, worden zorg ervoor dat u het wachtwoord voor pfx Hallo Hallo onthoudt.

![Toevoegen van een certificaat tooa Web-App in hello Azure Portal][2]

Hallo ding dat u nodig hebt toodo is een toepassingsinstelling tooyour Web-App die Hallo naam WEBSITE is tooadd\_LOAD\_certificaten en een waarde van *. Dit zorgt ervoor dat alle certificaten zijn geladen. Als u deze wilde tooload alleen Hallo van certificaten die u hebt geüpload en vervolgens kunt u een door komma's gescheiden lijst met de vingerafdrukken.

Zie toolearn meer informatie over het toevoegen van een certificaat tooa Web-App [met behulp van certificaten in toepassingen met Azure Websites](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)

**Een certificaat tooKey kluis toevoegen als een geheim** in plaats van uw certificaat toohello Web-App service rechtstreeks uploaden, kunt u opslaan in de Sleutelkluis als een geheim en het implementeren van daaruit. Dit is een proces in twee stappen die wordt beschreven in het volgende blogbericht Hallo [Azure Web App certificaat implementeren via Sleutelkluis](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)

## <a id="next"></a>Volgende stappen
Zie voor het programmeren van verwijzingen [Azure Key Vault C#-Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
