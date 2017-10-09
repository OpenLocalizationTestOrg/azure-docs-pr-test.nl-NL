---
title: aaaSigning overschakeling van de sleutel in Azure AD | Microsoft Docs
description: Dit artikel wordt beschreven Hallo ondertekening sleutelrollover aanbevolen procedures voor Azure Active Directory
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a>Ondertekening sleutelrollover in Azure Active Directory
In dit onderwerp wordt beschreven wat u moet tooknow over Hallo openbare sleutels die worden gebruikt in Azure Active Directory (Azure AD) toosign beveiligingstokens. Het is belangrijk toonote die deze rollover voor sleutels op periodieke basis en, in geval van nood, kan worden vernieuwd onmiddellijk. Alle toepassingen die gebruikmaken van Azure AD moeten kunnen tooprogrammatically ingang Hallo sleutelrollover proces of een overschakeling van de periodieke handmatige proces tot stand brengen. Doorgaan toounderstand lezen hoe Hallo sleutels werkt, hoe tooassess gevolgen van het Hallo rollover tooyour toepassing hello en hoe tooupdate uw toepassing of een sleutelrollover van periodieke overschakeling van de handmatige proces toohandle maken indien nodig.

## <a name="overview-of-signing-keys-in-azure-ad"></a>Overzicht van ondertekeningssleutels in Azure AD
Azure AD maakt gebruik van cryptografie van openbare sleutels is gebouwd op branche standaarden tooestablish vertrouwensrelatie tussen zichzelf en Hallo toepassingen die worden gebruikt. In de praktijk dit werkt in de volgende manieren Hallo: Azure AD maakt gebruik van een ondertekeningssleutel die uit een openbare en persoonlijke sleutelpaar bestaat. Wanneer een gebruiker zich aanmeldt tooan-toepassing die gebruikmaakt van Azure AD voor verificatie, wordt een beveiligingstoken dat informatie over Hallo gebruiker bevat gemaakt in Azure AD. Dit token is ondertekend door Azure AD met behulp van de persoonlijke sleutel voordat deze terug toohello toepassing wordt verzonden. tooverify die Hallo token geldig is en daadwerkelijk oorsprong van Azure AD, Hallo toepassing hello-token handtekening met de Hallo openbare sleutel die worden weergegeven door Azure AD dat is opgenomen in het Hallo-tenant moet valideren [discovery-document OpenID Connect](http://openid.net/specs/openid-connect-discovery-1_0.html) of WS-SAML-Fed [document met federatieve metagegevens](active-directory-federation-metadata.md).

Om veiligheidsredenen kan ondertekening sleutel rollen op periodieke basis en, in geval van nood, Hallo van Azure AD worden vernieuwd onmiddellijk. Alle toepassingen die kan worden geïntegreerd met Azure AD moet worden voorbereid toohandle een sleutelrollover-gebeurtenis niet van belang hoe vaak het optreden. Als dit niet het geval, en uw toepassing een verlopen sleutels tooverify Hallo handtekening op een token toouse probeert, mislukt Hallo aanmeldingsverzoek.

Er is altijd meer dan een geldige sleutel beschikbaar in het discovery-document met OpenID Connect Hallo en Hallo document met federatieve metagegevens. Uw toepassing moet worden voorbereid toouse Hallo sleutels opgegeven in Hallo document, omdat één sleutel, wordt mogelijk teruggedraaid binnenkort een andere kan worden de vervanging ervan, enzovoort.

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a>Hoe tooassess als uw toepassing worden beïnvloed en welke toodo erover
Hoe uw toepassing sleutelrollover verwerkt, is afhankelijk van variabelen zoals Hallo-type van de toepassing of welke identiteit protocol en de bibliotheek is gebruikt. de volgende secties voor Hallo te beoordelen of Hallo meest voorkomende typen toepassingen worden beïnvloed door Hallo sleutelrollover en advies geven over de wijze waarop tooupdate toepassing toosupport automatische rollover Hallo Hallo sleutel handmatig bijwerken.

* [Systeemeigen clienttoepassingen toegang krijgen tot bronnen](#nativeclient)
* [Webtoepassingen / API's toegang tot bronnen](#webclient)
* [Webtoepassingen / API's voor het beveiligen van resources en gebouwd met behulp van Azure App Services](#appservices)
* [Webtoepassingen / API's voor het beveiligen van resources met behulp van .NET OWIN OpenID Connect, WS-Fed of WindowsAzureActiveDirectoryBearerAuthentication middleware](#owin)
* [Webtoepassingen / API's voor het beveiligen van resources met behulp van .NET Core OpenID Connect of JwtBearerAuthentication middleware](#owincore)
* [Webtoepassingen / API's voor het beveiligen van resources met behulp van Node.js passport-azure-ad-module](#passport)
* [Webtoepassingen / API's voor het beveiligen van resources en gemaakt met Visual Studio 2015 of Visual Studio 2017](#vs2015)
* [Webtoepassingen bescherming van bronnen en met Visual Studio 2013 gemaakt](#vs2013)
* [Web-API's voor het beveiligen van resources en gemaakt met Visual Studio 2013](#vs2013_webapi)
* [Webtoepassingen bescherming van bronnen en met Visual Studio 2012 gemaakt](#vs2012)
* [Webtoepassingen bescherming van bronnen en met Visual Studio 2010, 2008 o met behulp van Windows Identity Foundation gemaakt](#vs2010)
* [Webtoepassingen / API's voor het beveiligen van resources met behulp van een andere bibliotheken of handmatig implementeren van Hallo ondersteund protocollen](#other)

Dit advies is **niet** van toepassing op:

* Toepassingen die zijn toegevoegd vanuit Azure AD-Toepassingsgalerie (met inbegrip van aangepaste) hebben afzonderlijke richtlijnen met betrekking toosigning sleutels. [Meer informatie.](../active-directory-sso-certs.md)
* Een on-premises toepassingen die zijn gepubliceerd via toepassingsproxy tooworry over het ondertekenen van sleutels niet hebt.

### <a name="nativeclient"></a>Systeemeigen clienttoepassingen toegang krijgen tot bronnen
Toepassingen die alleen toegang bronnen (eenledige tot zijn Microsoft Graph, KeyVault, API Outlook en andere Microsoft-APIs) in het algemeen alleen een token verkrijgen en het resource-eigenaar toohello doorgegeven. Gezien het feit dat ze niet alle bronnen beveiligen, ze doen Hallo token niet controleren en hoeven dus geen tooensure die goed zijn ondertekend.

Native client-toepassingen, of desktop of mobile, vallen in deze categorie en worden dus niet van invloed op Hallo rollover.

### <a name="webclient"></a>Webtoepassingen / API's toegang tot bronnen
Toepassingen die alleen toegang bronnen (eenledige tot zijn Microsoft Graph, KeyVault, API Outlook en andere Microsoft-APIs) in het algemeen alleen een token verkrijgen en het resource-eigenaar toohello doorgegeven. Gezien het feit dat ze niet alle bronnen beveiligen, ze doen Hallo token niet controleren en hoeven dus geen tooensure die goed zijn ondertekend.

Webtoepassingen en -API's die van de app alleen-lezen stroom hello gebruikmaken (clientreferenties / clientcertificaat), vallen in deze categorie en worden dus niet van invloed op Hallo rollover.

### <a name="appservices"></a>Webtoepassingen / API's voor het beveiligen van resources en gebouwd met behulp van Azure App Services
Azure App Services verificatie / autorisatie (EasyAuth)-functionaliteit is al Hallo benodigde logica toohandle sleutelrollover automatisch.

### <a name="owin"></a>Webtoepassingen / API's voor het beveiligen van resources met behulp van .NET OWIN OpenID Connect, WS-Fed of WindowsAzureActiveDirectoryBearerAuthentication middleware
Als uw toepassing van .NET OWIN OpenID Connect, WS-Fed of WindowsAzureActiveDirectoryBearerAuthentication-middleware Hallo gebruikmaakt al er Hallo benodigde logica toohandle sleutelrollover automatisch.

U kunt bevestigen dat uw toepassing van een van deze gebruikmaakt door te zoeken naar een van de volgende codefragmenten in uw toepassing Startup.cs of Startup.Auth.cs Hallo

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <a name="owincore"></a>Webtoepassingen / API's voor het beveiligen van resources met behulp van .NET Core OpenID Connect of JwtBearerAuthentication middleware
Als uw toepassing van .NET Core OWIN OpenID Connect Hallo of JwtBearerAuthentication middleware gebruikmaakt, al er Hallo benodigde logica toohandle sleutelrollover automatisch.

U kunt bevestigen dat uw toepassing van een van deze gebruikmaakt door te zoeken naar een van de volgende codefragmenten in uw toepassing Startup.cs of Startup.Auth.cs Hallo

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <a name="passport"></a>Webtoepassingen / API's voor het beveiligen van resources met behulp van Node.js passport-azure-ad-module
Als uw toepassing hello Node.js passport-ad-module gebruikt, deze is al Hallo benodigde logica toohandle sleutelrollover automatisch.

U kunt bevestigen dat uw toepassing passport-ad door te zoeken naar het volgende codefragment in uw toepassing app.js Hallo

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <a name="vs2015"></a>Webtoepassingen / API's voor het beveiligen van resources en gemaakt met Visual Studio 2015 of Visual Studio 2017
Als uw toepassing is gemaakt met een sjabloon in Visual Studio 2015 of Visual Studio 2017 en u hebt geselecteerd **werk-en Schoolaccounts** van Hallo **verificatie wijzigen** menu al Hallo benodigde logica toohandle sleutelrollover heeft automatisch. Deze logica, ingesloten in Hallo OWIN OpenID Connect middleware opgehaald en in de cache opgeslagen Hallo sleutels van de discovery-document met OpenID Connect Hallo en ze worden regelmatig vernieuwd.

Als u de oplossing tooyour verificatie handmatig hebt toegevoegd, is uw toepassing wellicht niet Hallo rollover van de benodigde logica. U moet toowrite het uzelf of Hallo Volg de stappen in [webtoepassingen / API's met behulp van een andere bibliotheken of handmatig implementeren van Hallo ondersteunde protocollen.](#other).

### <a name="vs2013"></a>Webtoepassingen bescherming van bronnen en met Visual Studio 2013 gemaakt
Als uw toepassing is gemaakt met behulp van een sjabloon in Visual Studio 2013 en u hebt geselecteerd **Organisatieaccounts** van Hallo **verificatie wijzigen** menu heeft al Hallo nodig logica toohandle key rollover automatisch. Deze logica slaat de unieke id van uw organisatie en Hallo ondertekening sleutelgegevens in twee databasetabellen die zijn gekoppeld aan het Hallo-project. U vindt Hallo-verbindingsreeks voor Hallo-database in het Web.config-bestand van het project Hallo.

Als u de oplossing tooyour verificatie handmatig hebt toegevoegd, is uw toepassing wellicht niet Hallo rollover van de benodigde logica. U moet toowrite het uzelf of Hallo Volg de stappen in [webtoepassingen / API's met behulp van een andere bibliotheken of handmatig implementeren van Hallo ondersteunde protocollen.](#other).

Hallo stappen volgen helpt u of Hallo logica juist werkt in uw toepassing.

1. Open Hallo oplossing in Visual Studio 2013, en klik vervolgens op Hallo **Server Explorer** tabblad op Hallo rechtervenster.
2. Vouw **gegevensverbindingen**, **DefaultConnection**, en vervolgens **tabellen**. Zoek Hallo **IssuingAuthorityKeys** tabel, met de rechtermuisknop en klik vervolgens op **tabelgegevens weergeven**.
3. In Hallo **IssuingAuthorityKeys** tabel, gaan er ten minste een rij die overeenkomt met de vingerafdrukwaarde toohello voor Hallo-sleutel. Alle rijen in Hallo tabel verwijderen.
4. Klik met de rechtermuisknop Hallo **Tenants** tabel en klik vervolgens op **tabelgegevens weergeven**.
5. In Hallo **Tenants** tabel, gaan er ten minste een rij die overeenkomt met tooa unieke directory-tenant-id. Alle rijen in Hallo tabel verwijderen. Als u niet Hallo rijen in beide Hallo verwijdert **Tenants** tabel en **IssuingAuthorityKeys** tabel, ontvangt u een fout opgetreden tijdens runtime.
6. Toepassing bouwen en uitvoeren Hallo. Nadat u zich hebt aangemeld in tooyour-account, kunt u de toepassing hello stoppen.
7. Retourneren van toohello **Server Explorer** en bekijkt hello waarden in Hallo **IssuingAuthorityKeys** en **Tenants** tabel. U zult zien dat ze hebben is automatisch opnieuw gevuld met de juiste informatie Hallo van Hallo document met federatieve metagegevens.

### <a name="vs2013"></a>Web-API's voor het beveiligen van resources en gemaakt met Visual Studio 2013
Als u een web API-toepassing in Visual Studio 2013 met Hallo Web API-sjabloon hebt gemaakt en vervolgens geselecteerd **Organisatieaccounts** van Hallo **verificatie wijzigen** menu u al hebt Hallo benodigde logica in uw toepassing.

Als u verificatie handmatig hebt geconfigureerd, volgt u onderstaande toolearn Hallo instructies hoe tooconfigure uw Web-API-tooautomatically bijwerken van de belangrijke informatie.

Hallo volgende codefragment wordt gedemonstreerd hoe tooget Hallo nieuwste sleutels van het document met federatieve metagegevens hello, en gebruik vervolgens Hallo [JWT-Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate Hallo-token. Hallo-codefragment wordt ervan uitgegaan dat u uw eigen mechanisme voor het persistent maken Hallo sleutel toovalidate toekomstige caching tokens van Azure AD gebruikt ongeacht of deze in een database, configuratiebestand of elders.

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <a name="vs2012"></a>Webtoepassingen bescherming van bronnen en met Visual Studio 2012 gemaakt
Als uw toepassing is gemaakt in Visual Studio 2012, u waarschijnlijk gebruikt Hallo identiteit en toegang tot hulpprogramma tooconfigure uw toepassing. Ook is het waarschijnlijk dat u van Hallo gebruikmaakt [valideren van certificaatverlener naam register (VINR)](https://msdn.microsoft.com/library/dn205067.aspx). Hallo VINR is verantwoordelijk voor het onderhouden van informatie over vertrouwde id-providers (Azure AD) en Hallo sleutels toovalidate tokens die zijn uitgegeven door ze gebruikt. Hallo VINR maakt het ook eenvoudig tooautomatically update Hallo belangrijke informatie opgeslagen in een Web.config-bestand downloaden Hallo nieuwste document met federatieve metagegevens die zijn gekoppeld aan uw directory, als Hallo-configuratie verouderd Hello laatste is controleren document en bijwerken Hallo toouse Hallo nieuwe Toepassingssleutel indien nodig.

Als u uw toepassing met behulp van een Hallo-codevoorbeelden of walkthrough documentatie van Microsoft hebt gemaakt, wordt Hallo sleutelrollover logica is al opgenomen in uw project. U ziet dat Hallo onderstaande code in uw project al bestaat. Als uw toepassing geen al deze logica heeft, stappen Hallo hieronder tooadd en tooverify die correct werkt.

1. In **Solution Explorer**, Voeg een verwijzing toohello **System.IdentityModel** assembly voor de juiste Hallo-project.
2. Open Hallo **Global.asax.cs** -bestand en voeg de volgende Hallo met behulp van instructies:
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. Hallo na methode toohello toevoegen **Global.asax.cs** bestand:
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. Hallo aanroepen **RefreshValidationSettings()** methode in Hallo **Application_Start()** methode in **Global.asax.cs** zoals wordt weergegeven:
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

Zodra u deze stappen hebt uitgevoerd, wordt Web.config van uw toepassing worden bijgewerkt met de meest recente gegevens Hallo van Hallo document met federatieve metagegevens, met inbegrip van de meest recente sleutels Hallo. Deze update wordt uitgevoerd telkens wanneer de groep van toepassingen wordt gerecycled in IIS. IIS is standaard ingesteld toorecycle toepassingen om 29 uur.

Hallo stappen hieronder tooverify hello sleutelrollover logica werkt.

1. Nadat u hebt gecontroleerd dat uw toepassing van Hallo code hierboven, open Hallo gebruikmaakt **Web.config** bestands- en navigeer toohello  **<issuerNameRegistry>**  blok, zoekt specifiek Hallo paar regels te volgen:
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. In Hallo  **<add thumbprint=””>**  instelling Hallo vingerafdrukwaarde wijzigen door willekeurig teken vervangen door een andere naam. Hallo opslaan **Web.config** bestand.
3. Hallo-toepassing bouwen en uitvoeren. Als u Hallo aanmelden proces voltooien kunt, wordt uw toepassing hello sleutel is bijgewerkt door Hallo vereist informatie te downloaden via document met federatieve metagegevens van uw directory. Als u problemen met aanmelden ondervindt, zorg er dan Hallo wijzigingen in uw toepassing correct zijn door te lezen Hallo [toe te voegen aanmelding tooYour Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) onderwerp of bij het downloaden en Hallo volgende codevoorbeeld te bekijken: [ Multitenant Cloudtoepassing voor Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).

### <a name="vs2010"></a>Webtoepassingen bescherming van bronnen en zijn gemaakt met Visual Studio 2008 of 2010 en Windows Identity Foundation (WIF) v1.0 voor .NET 3.5
Als u een toepassing op WIF v1.0 gebouwd, is er geen tooautomatically opgegeven mechanisme vernieuwing toouse van de configuratie van uw toepassing een nieuwe sleutel.

* *Eenvoudigst* hello FedUtil tooling opgenomen in Hallo WIF SDK, die de meest recente metagegevensdocument Hallo ophalen en bijwerken van uw configuratie gebruiken.
* Uw toepassing too.NET 4.5, waaronder de nieuwste versie van WIF zich in de naamruimte System Hallo Hallo bijwerken. Vervolgens kunt u Hallo [valideren van certificaatverlener naam register (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform automatische updates van de configuratie van de toepassing hello.
* Voer een handmatige rollover volgens de instructies Hallo aan Hallo einde van dit document richtlijnen.

Instructies toouse Hallo FedUtil tooupdate uw configuratie:

1. Controleer of u Hallo WIF v1.0 SDK is geïnstalleerd op uw ontwikkelcomputer voor Visual Studio 2008 of 2010. U kunt [downloaden vanaf hier](https://www.microsoft.com/en-us/download/details.aspx?id=4451) als u nog niet hebt geïnstalleerd het.
2. Open in Visual Studio Hallo-oplossing, klik met de rechtermuisknop op Hallo van toepassing project en selecteer **federatiemetagegevens bijwerken**. Als deze optie niet beschikbaar is, is FedUtil en/of Hallo WIF v1.0 SDK niet geïnstalleerd.
3. Selecteer in het Hallo-prompt **Update** toobegin bijwerken van uw federatiemetagegevens. Als u toegang toohello server-omgeving waar de toepassing hello wordt gehost hebt, kunt u eventueel gebruiken van FedUtil [metagegevens van de automatische update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).
4. Klik op **voltooien** toocomplete Hallo updateproces.

### <a name="other"></a>Webtoepassingen / API's voor het beveiligen van resources met behulp van een andere bibliotheken of handmatig implementeren van Hallo ondersteund protocollen
Als u van een aantal andere bibliotheek gebruikmaakt of geïmplementeerd handmatig van de protocollen Hallo ondersteund, moet u tooreview Hallo-bibliotheek of uw implementatie tooensure die sleutel Hallo is opgehaald van de discovery-document met OpenID Connect Hallo of Hallo document met federatieve metagegevens. Eenzijdige toocheck voor dit is een zoekopdracht in uw code of code Hallo-bibliotheek voor alle aanroepen tooeither hello OpenID discovery-document of een document met federatieve metagegevens Hallo toodo.

Als deze sleutel is ergens wordt opgeslagen of vastgelegd in uw toepassing, u handmatig kunt ophalen Hallo sleutel en het dienovereenkomstig door uitvoeren van een handmatige rollover volgens de instructies aan einde van dit document richtlijnen Hallo Hallo-update. **Het wordt ten zeerste aangemoedigd verbeteren van uw toepassing toosupport automatische rollover** met behulp van een Hallo nadert overzicht in dit artikel tooavoid toekomstige onderbrekingen en overhead als Azure AD de rollover uitgebracht verhoogt of heeft een de overschakeling van de out-of-band noodgevallen.

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a>Hoe tootest uw toepassing toodetermine als deze worden beïnvloed
U kunt nagaan of uw toepassing automatische sleutelrollover ondersteunt door het Hallo-scripts downloaden en instructies te volgen Hallo in [deze GitHub-opslagplaats.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a>Hoe tooperform een handmatige rollover als u een toepassing biedt geen ondersteuning voor automatische rollover
Als uw toepassing wel **niet** automatische rollover ondersteunen, moet u tooestablish een proces dat periodiek monitors Azure AD het ondertekenen van sleutels en voert een handmatige rollover dienovereenkomstig. [Deze GitHub-opslagplaats](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) bevat scripts en instructies voor het toodo dit.

