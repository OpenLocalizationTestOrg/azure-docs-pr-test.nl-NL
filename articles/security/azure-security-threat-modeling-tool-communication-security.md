---
title: Azure Security - Microsoft Threat Modeling Tool - aaaCommunication | Microsoft Docs
description: oplossingen voor bedreigingen die worden weergegeven in Hallo Threat Modeling hulpprogramma
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 667829c75123f4dbe0b383fdaf8cd899802f9b16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-communication-security--mitigations"></a>Beveiliging Frame: Beveiligde communicatie | Oplossingen 
| Product/Service | Artikel |
| --------------- | ------- |
| **Azure Event Hub** | <ul><li>[Veilige communicatie tooEvent Hub met behulp van SSL/TLS](#comm-ssltls)</li></ul> |
| **Dynamics CRM** | <ul><li>[Serviceaccount respecteren bevoegdheden en controleer of de Hallo aangepaste Services of ASP.NET-pagina's van CRM-beveiliging controleren](#priv-aspnet)</li></ul> |
| **Azure Data Factory** | <ul><li>[Data management gateway tijdens het maken van verbinding On-premises SQL Server tooAzure Data Factory gebruiken](#sqlserver-factory)</li></ul> |
| **Identiteitsserver** | <ul><li>[Zorg ervoor dat alle verkeer tooIdentity Server via HTTPS-verbinding](#identity-https)</li></ul> |
| **Webtoepassing** | <ul><li>[Controleer of X.509-certificaten gebruikt tooauthenticate SSL, TLS en DTLS verbindingen](#x509-ssltls)</li><li>[SSL-certificaat voor een aangepast domein configureren in Azure App Service](#ssl-appservice)</li><li>[Afdwingen van alle verkeer tooAzure App Service via HTTPS-verbinding](#appservice-https)</li><li>[HTTP-strikte transportbeveiliging (HSTS) inschakelen](#http-hsts)</li></ul> |
| **Database** | <ul><li>[Zorg ervoor dat SQL server-versleuteling en certificaat verbindingsvalidatie](#sqlserver-validation)</li><li>[Versleutelde communicatie tooSQL server forceren](#encrypted-sqlserver)</li></ul> |
| **Azure Storage** | <ul><li>[Zorg ervoor dat communicatie tooAzure die opslag via HTTPS is](#comm-storage)</li><li>[Valideren van MD5-hash na het downloaden van blob als HTTPS kan niet worden ingeschakeld.](#md5-https)</li><li>[Gebruik SMB 3.0-compatibele client tooensure in transit data encryption tooAzure bestandsshares](#smb-shares)</li></ul> |
| **Mobiele clients** | <ul><li>[Certificaat vastmaken implementeren](#cert-pinning)</li></ul> |
| **WCF** | <ul><li>[HTTPS inschakelen - transportkanaal beveiligen](#https-transport)</li><li>[WCF: Set-bericht beveiliging beveiliging niveau tooEncryptAndSign](#message-protection)</li><li>[WCF: Gebruik een account met minder rechten toorun WCF-service](#least-account-wcf)</li></ul> |
| **Web-API** | <ul><li>[Afdwingen van alle verkeer tooWeb API's via HTTPS-verbinding](#webapi-https)</li></ul> |
| **Azure Redis-cache** | <ul><li>[Zorg ervoor dat communicatie tooAzure die redis-Cache via SSL is](#redis-ssl)</li></ul> |
| **Veld IoT Gateway** | <ul><li>[Gateway-apparaatcommunicatie tooField beveiligen](#device-field)</li></ul> |
| **IoT-Cloudgateway** | <ul><li>[Apparaat tooCloud Gateway communicatie met behulp van SSL/TLS beveiligen](#device-cloud)</li></ul> |

## <a id="comm-ssltls"></a>Veilige communicatie tooEvent Hub met behulp van SSL/TLS

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Event Hub | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Verificatie en beveiliging model overzicht van Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Stappen** | AMQP of HTTP-verbindingen tooEvent Hub met behulp van SSL/TLS beveiligen |

## <a id="priv-aspnet"></a>Serviceaccount respecteren bevoegdheden en controleer of de Hallo aangepaste Services of ASP.NET-pagina's van CRM-beveiliging controleren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Dynamics CRM | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Serviceaccount respecteren bevoegdheden en controleer of de Hallo aangepaste Services of ASP.NET-pagina's van CRM-beveiliging controleren |

## <a id="sqlserver-factory"></a>Data management gateway tijdens het maken van verbinding On-premises SQL Server tooAzure Data Factory gebruiken

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Data Factory | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | Gekoppelde servicetypen - Azure en On-premises |
| **Verwijzingen**              |[Verplaatsen van gegevens tussen On premises en Azure Data Factory](https://azure.microsoft.com/documentation/articles/data-factory-move-data-between-onprem-and-cloud/#create-gateway), [Data management gateway](https://azure.microsoft.com/documentation/articles/data-factory-data-management-gateway/) |
| **Stappen** | <p>Hallo Data Management Gateway (DMG)-hulpprogramma is vereist tooconnect toodata bronnen die zijn beveiligd achter een firewall of een corpnet.</p><ol><li>Hallo machine vergrendelen Hallo DMG hulpprogramma isoleert en voorkomt dat niet-functionerende programma van beschadigen of controle op Hallo gegevens bronmachine. (Bijvoorbeeld) meest recente updates worden geïnstalleerd, enable minimale vereiste poorten, beheerde accounts inrichten, controle is ingeschakeld, schijfversleuteling ingeschakeld enz.)</li><li>De gatewaycode gegevens moet worden gedraaid met regelmatige tussenpozen of wanneer het wachtwoord van serviceaccount DMG Hallo verlengd</li><li>Passages van gegevens via de koppeling Service moeten worden versleuteld.</li></ol> |

## <a id="identity-https"></a>Zorg ervoor dat alle verkeer tooIdentity Server via HTTPS-verbinding

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Identiteitsserver | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [IdentityServer3 - sleutels, handtekeningen en cryptografische](https://identityserver.github.io/Documentation/docsv2/configuration/crypto.html), [IdentityServer3 - implementatie](https://identityserver.github.io/Documentation/docsv2/advanced/deployment.html) |
| **Stappen** | IdentityServer moet standaard alle binnenkomende verbindingen toocome via HTTPS. Het is absoluut verplicht dat communicatie met IdentityServer via beveiligde transporten alleen wordt uitgevoerd. Er zijn bepaalde implementatiescenario's zoals het SSL-offloading waar deze vereiste kan minder streng worden gemaakt. Zie Hallo Identiteitsserver implementatie pagina in Hallo verwijzingen voor meer informatie. |

## <a id="x509-ssltls"></a>Controleer of X.509-certificaten gebruikt tooauthenticate SSL, TLS en DTLS verbindingen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Toepassingen die gebruikmaken van SSL, TLS en DTLS moeten volledig Hallo X.509-certificaten van Hallo entiteiten die ze verbinding met maken controleren. Dit omvat de verificatie van Hallo certificaten voor:</p><ul><li>Domeinnaam</li><li>Geldigheidsdatums (begin- en verloopdatum datums)</li><li>Kan de intrekkingsstatus</li><li>Gebruik (bijvoorbeeld Serverauthenticatie voor servers, Client-verificatie voor clients)</li><li>-Keten vertrouwen. Certificaten moeten zijn geketend tooa basiscertificeringsinstantie (CA) die wordt vertrouwd door Hallo platform of expliciet is geconfigureerd door Hallo beheerder</li><li>Sleutellengte van de openbare sleutel van het certificaat moet > 2048 bits</li><li>Hash-algoritme moet SHA256 en hoger |

## <a id="ssl-appservice"></a>SSL-certificaat voor een aangepast domein configureren in Azure App Service

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | EnvironmentType - Azure |
| **Verwijzingen**              | [HTTPS inschakelen voor een app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-configure-ssl-certificate/) |
| **Stappen** | Standaard Azure al ingeschakeld door HTTPS voor elke app met een jokertekencertificaat voor Hallo *. azurewebsites.net domein. Net als alle Jokertekendomeinen, het is echter niet zo veilig zijn als het gebruik van een aangepast domein met eigen certificaat [Raadpleeg](https://casecurity.org/2014/02/26/pros-and-cons-of-single-domain-multi-domain-and-wildcard-certificates/). Het verdient aanbeveling tooenable SSL Hallo aangepaste domein welke app Hallo geïmplementeerd via|

## <a id="appservice-https"></a>Afdwingen van alle verkeer tooAzure App Service via HTTPS-verbinding

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | EnvironmentType - Azure |
| **Verwijzingen**              | [Enforce HTTPS in Azure App Service] https://azure.microsoft.com/documentation/articles/web-sites-configure-ssl-certificate/#4-enforce-https-on-your-app) |
| **Stappen** | <p>Hoewel Azure kan al HTTPS voor apps van Azure-services met een jokertekencertificaat voor Hallo domein *. azurewebsites.net, het HTTPS niet afdwingen. Bezoekers mogelijk nog steeds toegang tot het Hallo-app met behulp van HTTP gevaar Hallo appbeveiligng en daarom HTTPS heeft toobe expliciet worden afgedwongen. ASP.NET MVC-toepassingen gebruikmaken van Hallo [RequireHttps filter](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) die zorgt ervoor dat een niet-beveiligde HTTP-aanvraag toobe opnieuw verzonden via HTTPS.</p><p>Hallo herschrijven van URL's module, dat opgenomen in Azure App Service is kan ook gebruikte tooenforce HTTPS. Module herschrijven van URL's kan ontwikkelaars toodefine regels die moeten toegepast tooincoming aanvragen worden voordat Hallo aanvragen tooyour toepassing worden doorgegeven. Regels voor het herschrijven van URL's zijn gedefinieerd in een web.config-bestand dat is opgeslagen in de hoofdmap van de toepassing hello Hallo</p>|

### <a name="example"></a>Voorbeeld
Hallo volgende voorbeeld bevat een eenvoudige herschrijven van URL's regel dat ervoor zorgt alle binnenkomende verkeer toouse HTTPS dat
```XML
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```
Deze regel werkt door te retourneren van een HTTP-statuscode 301 (permanente omleiding) wanneer Hallo gebruiker een pagina via HTTP-aanvragen. Hallo 301 omleidingen Hallo aanvraag toohello dezelfde URL als Hallo bezoeker aangevraagd, maar vervangt Hallo HTTP-gedeelte van de aanvraag Hallo met HTTPS. Bijvoorbeeld is HTTP://contoso.com omgeleid tooHTTPS://contoso.com. 

## <a id="http-hsts"></a>HTTP-strikte transportbeveiliging (HSTS) inschakelen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [OWASP HTTP strikte transportbeveiliging cheats blad](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) |
| **Stappen** | <p>HTTP strikte Transport beveiliging (HSTS) is een opt-in voor beveiligingsuitbreiding die is opgegeven door een webtoepassing via Hallo gebruik van een speciale antwoordheader. Wanneer een ondersteunde browser deze header ontvangt die browser wordt voorkomen dat de communicatie wordt verzonden via HTTP toohello opgegeven domein en het alle communicatie via HTTPS in plaats daarvan verzendt. Dit voorkomt ook dat HTTPS klik door de aanwijzingen in browsers.</p><p>tooimplement HSTS, Hallo na antwoordheader heeft toobe geconfigureerd voor een website globaal in code of in de configuratie. Strikt-Transport-beveiliging: maximumleeftijd = 300; includeSubDomains HSTS adressen Hallo bedreigingen te volgen:</p><ul><li>Gebruiker bladwijzers of handmatig http://example.com typen en onderwerp tooa man-in-the-middle aanvaller: HSTS tooHTTPS voor HTTP-aanvragen voor het doeldomein Hallo automatisch omgeleid</li><li>Webtoepassing die is bedoeld toobe puur HTTPS bevat de HTTP-koppelingen per ongeluk of fungeert inhoud via HTTP: HSTS tooHTTPS voor HTTP-aanvragen voor het doeldomein Hallo automatisch omgeleid</li><li>Een aanvaller man-in-the-middle toointercept verkeer van een gebruiker van het slachtoffer met behulp van een ongeldig certificaat probeert en hoopt Hallo gebruiker accepteert Hallo verkeerd certificaat: HSTS staat niet toe dat een gebruiker toooverride Hallo-bericht van ongeldig certificaat</li></ul>|

## <a id="sqlserver-validation"></a>Zorg ervoor dat SQL server-versleuteling en certificaat verbindingsvalidatie

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | SQL Azure  |
| **Kenmerken**              | SQL-versie - V12 |
| **Verwijzingen**              | [Aanbevolen procedures op schrijven verbindingsreeksen voor SQL-Database beveiligen](http://social.technet.microsoft.com/wiki/contents/articles/2951.windows-azure-sql-database-connection-security.aspx#best) |
| **Stappen** | <p>Alle communicatie tussen de SQL-Database en een clienttoepassing worden versleuteld met behulp van Secure Sockets Layer (SSL) te allen tijde. SQL-Database biedt geen ondersteuning voor niet-versleutelde verbindingen. toovalidate certificaten met toepassingscode of hulpprogramma's voor aanvragen van een versleutelde verbinding expliciet en Hallo servercertificaten niet vertrouwt. Als uw toepassingscode of hulpprogramma's voor een versleutelde verbinding geen aanvragen, steeds ze nog versleutelde verbindingen</p><p>Echter, ze Hallo servercertificaten mogelijk niet worden gevalideerd en dus worden vatbaar te 'man-in Hallo middle'-aanvallen. certificaten met ADO.NET toepassingscode toovalidate ingesteld `Encrypt=True` en `TrustServerCertificate=False` in Hallo databaseverbindingsreeks. toovalidate certificaten via SQL Server Management Studio Hallo Connect tooServer-dialoogvenster geopend. Klik op verbinding op Hallo verbindingseigenschappen tabblad versleutelen</p>|

## <a id="encrypted-sqlserver"></a>Versleutelde communicatie tooSQL server forceren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | OnPrem |
| **Kenmerken**              | SQL-versie - MsSQL2016, SQL-versie - MsSQL2012, SQL-versie - MsSQL2014 |
| **Verwijzingen**              | [Versleutelde verbindingen toohello Database-Engine inschakelen](https://msdn.microsoft.com/library/ms191192)  |
| **Stappen** | Inschakelen van SSL verhoogt de versleuteling Hallo beveiliging van gegevens die worden overgedragen via netwerken tussen exemplaren van SQL Server en toepassingen. |

## <a id="comm-storage"></a>Zorg ervoor dat communicatie tooAzure die opslag via HTTPS is

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Storage | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Azure Storage transportniveau codering – via HTTPS](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_encryption-in-transit) |
| **Stappen** | Hallo HTTPS-protocol tooensure Hallo beveiliging van Azure Storage-gegevens in transit, altijd gebruiken tijdens het aanroepen van Hallo REST-API's of toegang tot objecten in de opslag. Ook Shared Access Signatures, wat kan gebruikte toodelegate tooAzure opslagobjecten te openen, bevatten een optie toospecify die alleen Hallo HTTPS-protocol kan worden gebruikt bij het gebruik van handtekeningen voor gedeelde toegang, ervoor te zorgen dat iedereen verstuurt koppelingen met SAS-tokens worden Gebruik het juiste protocol Hallo.|

## <a id="md5-https"></a>Valideren van MD5-hash na het downloaden van blob als HTTPS kan niet worden ingeschakeld.

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Storage | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | StorageType - Blob |
| **Verwijzingen**              | [Overzicht van Windows Azure-blobopslag MD5](https://blogs.msdn.microsoft.com/windowsazurestorage/2011/02/17/windows-azure-blob-md5-overview/) |
| **Stappen** | <p>Windows Azure Blob-service biedt mechanismen tooensure gegevensintegriteit zowel in de toepassing hello en transport. Als voor een of andere reden moet u toouse HTTP in plaats van HTTPS en u werkt met blok-blobs, kunt u MD5 controleren toohelp controleren de integriteit van de Hallo Hallo BLOBs worden overgedragen</p><p>Dit helpt met bescherming tegen netwerk/transport layer fouten, maar niet noodzakelijkerwijs met tussenliggende aanvallen. Als u HTTPS, waardoor transport level security, dan is het gebruik van MD5 controleren redundante en onnodige gebruiken kunt.</p>|

## <a id="smb-shares"></a>Gebruik van SMB 3.0-client compatibel tooensure in transit gegevens versleuteling tooAzure bestandsshares

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Mobiele clients | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | StorageType - bestand |
| **Verwijzingen**              | [Azure File Storage](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/#comment-2529238931), [Azure File Storage SMB-ondersteuning voor Windows-Clients](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/#_mount-the-file-share) |
| **Stappen** | Azure File Storage ondersteunt HTTPS wanneer Hallo REST-API gebruiken, maar is veelgebruikte als een SMB-bestandsshare tooa VM gekoppelde. SMB 2.1 biedt geen ondersteuning voor versleuteling, zodat de verbindingen zijn alleen toegestaan binnen Hallo dezelfde regio in Azure. Echter SMB 3.0 ondersteunt codering en kan worden gebruikt met Windows Server 2012 R2, Windows 8, Windows 8.1 en Windows 10, zodat de regio-overschrijdende toegang en zelfs toegang op Hallo bureaublad. |

## <a id="cert-pinning"></a>Certificaat vastmaken implementeren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Storage | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemeen, Windows Phone |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Certificaat en openbare sleutel vastmaken](https://www.owasp.org/index.php/Certificate_and_Public_Key_Pinning#.Net) |
| **Stappen** | <p>Certificaat vastmaken beveiligingsinfrastructuur tegen Man-In-The-Middle (MITM)-aanvallen. Hallo-proces van het koppelen van een host met de verwachte X509 vastmaken is certificaat of de openbare sleutel. Wanneer een certificaat of de openbare sleutel is bekend of die u voor een host, is Hallo certificaat of de openbare sleutel gekoppeld of 'vastgemaakt' toohello host. </p><p>Dus als een adversary probeert toodo SSL MITM-aanvallen tijdens de SSL-handshake Hallo sleutel van de hacker server van afwijken zullen Hallo vastgemaakt certificaatsleutel, en Hallo aanvraag worden genegeerd, waardoor wordt voorkomen dat MITM certificaat vastmaken kan worden bereikt implementatie van de ServicePointManager `ServerCertificateValidationCallback` delegeren.</p>|

### <a name="example"></a>Voorbeeld
```C#
using System;
using System.Net;
using System.Net.Security;
using System.Security.Cryptography;

namespace CertificatePinningExample
{
    class CertificatePinningExample
    {
        /* Note: In this example, we're hardcoding a hello certificate's public key and algorithm for 
           demonstration purposes. In a real-world application, this should be stored in a secure
           configuration area that can be updated as needed. */

        private static readonly string PINNED_ALGORITHM = "RSA";

        private static readonly string PINNED_PUBLIC_KEY = "3082010A0282010100B0E75B7CBE56D31658EF79B3A1" +
            "294D506A88DFCDD603F6EF15E7F5BCBDF32291EC50B2B82BA158E905FE6A83EE044A48258B07FAC3D6356AF09B2" +
            "3EDAB15D00507B70DB08DB9A20C7D1201417B3071A346D663A241061C151B6EC5B5B4ECCCDCDBEA24F051962809" +
            "FEC499BF2D093C06E3BDA7D0BB83CDC1C2C6660B8ECB2EA30A685ADE2DC83C88314010FFC7F4F0F895EDDBE5C02" +
            "ABF78E50B708E0A0EB984A9AA536BCE61A0C31DB95425C6FEE5A564B158EE7C4F0693C439AE010EF83CA8155750" +
            "09B17537C29F86071E5DD8CA50EBD8A409494F479B07574D83EDCE6F68A8F7D40447471D05BC3F5EAD7862FA748" +
            "EA3C92A60A128344B1CEF7A0B0D94E50203010001";


        public static void Main(string[] args)
        {
            HttpWebRequest request = (HttpWebRequest)WebRequest.Create("https://azure.microsoft.com");
            request.ServerCertificateValidationCallback = (sender, certificate, chain, sslPolicyErrors) =>
            {
                if (certificate == null || sslPolicyErrors != SslPolicyErrors.None)
                {
                    // Error getting certificate or hello certificate failed basic validation
                    return false;
                }

                var targetKeyAlgorithm = new Oid(certificate.GetKeyAlgorithm()).FriendlyName;
                var targetPublicKey = certificate.GetPublicKeyString();
                
                if (targetKeyAlgorithm == PINNED_ALGORITHM &&
                    targetPublicKey == PINNED_PUBLIC_KEY)
                {
                    // Success, hello certificate matches hello pinned value.
                    return true;
                }
                // Reject, either hello key or hello algorithm does not match hello expected value.
                return false;
            };

            try
            {
                var response = (HttpWebResponse)request.GetResponse();
                Console.WriteLine($"Success, HTTP status code: {response.StatusCode}");
            }
            catch(Exception ex)
            {
                Console.WriteLine($"Failure, {ex.Message}");
            }
            Console.WriteLine("Press any key tooend.");
            Console.ReadKey();
        }
    }
}
```

## <a id="https-transport"></a>HTTPS inschakelen - transportkanaal beveiligen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | WCF | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | NET Framework 3 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Voeg Koninkrijk](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Stappen** | de configuratie van de toepassing Hello moet ervoor zorgen dat HTTPS voor alle toegang tot toosensitive informatie wordt gebruikt.<ul><li>**UITLEG:** als een toepassing omgaat met gevoelige gegevens en gebruikt geen berichtniveau versleuteling, wordt deze alleen toe te staan toocommunicate via een versleutelde transportkanaal.</li><li>**AANBEVELINGEN:** Zorg ervoor dat de HTTP-transport is uitgeschakeld en in plaats daarvan HTTPS-transport inschakelen. Vervang bijvoorbeeld Hallo `<httpTransport/>` met `<httpsTransport/>` label. Vertrouw niet op een netwerk-configuratie (firewall) tooguarantee Hallo toepassing kan alleen worden benaderd via een beveiligd kanaal. Vanuit een levensbeschouwelijke oogpunt van moet toepassing hello niet afhankelijk Hallo netwerk voor de beveiliging.</li></ul><p>Vanuit een praktische oogpunt van volgen Hallo mensen die verantwoordelijk zijn voor het beveiligen van Hallo netwerk niet altijd Hallo beveiligingsvereisten van de toepassing hello als ze ontwikkelen.</p>|

## <a id="message-protection"></a>WCF: Set-bericht beveiliging beveiliging niveau tooEncryptAndSign

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | WCF | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | .NET framework 3 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [MSDN](https://msdn.microsoft.com/library/ff650862.aspx) |
| **Stappen** | <ul><li>**UITLEG:** wanneer beveiligingsniveau is ingesteld te 'none' wordt uitgeschakeld beveiliging bericht. Vertrouwelijkheid en integriteit wordt bereikt met een passend niveau van de instelling.</li><li>**AANBEVELINGEN:**<ul><li>Wanneer `Mode=None` -bericht beveiliging uitgeschakeld</li><li>Wanneer `Mode=Sign` -tekenen maar heeft het Hallo-bericht niet versleutelen; moet worden gebruikt als de integriteit van gegevens is belangrijk</li><li>Wanneer `Mode=EncryptAndSign` -tekens en versleutelt het Hallo-bericht</li></ul></li></ul><p>Houd rekening met het uitschakelen van versleuteling en het bericht alleen ondertekening wanneer, u alleen toovalidate Hallo integriteit van Hallo informatie zonder problemen van vertrouwelijkheid hoeft. Dit kan handig zijn voor bewerkingen of servicecontracten waarin u moet toovalidate Hallo oorspronkelijk afzender, maar geen vertrouwelijke gegevens worden verzonden. Hallo beveiligingsniveau verminderen, wees dan voorzichtig dat Hallo-bericht bevat geen persoonsgegevens (PII).</p>|

### <a name="example"></a>Voorbeeld
Configureren van Hallo service en het Hallo bewerking tooonly aanmelding Hallo-bericht wordt weergegeven in Hallo volgen voorbeelden. Voorbeeld van de service Contract van `ProtectionLevel.Sign`: Hallo Hieronder volgt een voorbeeld van het gebruik van ProtectionLevel.Sign op Hallo servicecontract niveau: 
```
[ServiceContract(Protection Level=ProtectionLevel.Sign] 
public interface IService 
  { 
  string GetData(int value); 
  } 
```

### <a name="example"></a>Voorbeeld
Voorbeeld van de bewerking Contract van `ProtectionLevel.Sign` (voor gedetailleerde controle): Hallo Hieronder volgt een voorbeeld van het gebruik van `ProtectionLevel.Sign` op Hallo OperationContract niveau:

```
[OperationContract(ProtectionLevel=ProtectionLevel.Sign] 
string GetData(int value);
``` 

## <a id="least-account-wcf"></a>WCF: Gebruik een account met minder rechten toorun WCF-service

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | WCF | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | .NET framework 3 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [MSDN](https://msdn.microsoft.com/library/ff648826.aspx ) |
| **Stappen** | <ul><li>**UITLEG:** WCF-services onder beheer of een account met hoge bevoegdheden niet uitvoeren. in geval van inbreuk op services zal het leiden tot hoge impact.</li><li>**AANBEVELINGEN:** gebruik een account met minder rechten toohost uw WCF-service omdat deze wordt Verminder de kwetsbaarheid van uw toepassing en verminderen Hallo potentiële schade voorkomen als u wordt aangevallen. Als het serviceaccount Hallo extra toegangsrechten voor de infrastructuurresources, zoals MSMQ vereist, moeten hello gebeurtenislogboek, prestatiemeteritems en het bestandssysteem hello, gemachtigd krijgen toothese resources zodat Hallo WCF-service kan worden uitgevoerd is.</li></ul><p>Als uw service tooaccess specifieke bronnen namens de oorspronkelijke aanvrager hello moet, maken gebruik van imitatie en overdracht tooflow Hallo aanroeper ID voor een downstream-autorisatie-controle. Gebruik in een ontwikkelingsscenario Hallo lokale netwerkservice-account, dit is een speciale ingebouwde account met rechten is verminderd. Maak een aangepast domein minder rechten-serviceaccount in een productiescenario.</p>|

## <a id="webapi-https"></a>Afdwingen van alle verkeer tooWeb API's via HTTPS-verbinding

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Web-API | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | MVC5, MVC6 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Afdwingen van SSL in een Web API-Controller](http://www.asp.net/web-api/overview/security/working-with-ssl-in-web-api) |
| **Stappen** | Als een toepassing zowel een HTTPS- en een HTTP-binding heeft, kunnen clients nog steeds HTTP tooaccess Hallo-site gebruiken. tooprevent dit, gebruik een actie filter tooensure waarin tooprotected API's zijn altijd via HTTPS.|

### <a name="example"></a>Voorbeeld 
Hallo toont volgende code een verificatie-filter van Web-API waarmee wordt gecontroleerd of SSL: 
```C#
public class RequireHttpsAttribute : AuthorizationFilterAttribute
{
    public override void OnAuthorization(HttpActionContext actionContext)
    {
        if (actionContext.Request.RequestUri.Scheme != Uri.UriSchemeHttps)
        {
            actionContext.Response = new HttpResponseMessage(System.Net.HttpStatusCode.Forbidden)
            {
                ReasonPhrase = "HTTPS Required"
            };
        }
        else
        {
            base.OnAuthorization(actionContext);
        }
    }
}
```
Dit filter tooany Web API-acties die SSL vereisen toevoegen: 
```C#
public class ValuesController : ApiController
{
    [RequireHttps]
    public HttpResponseMessage Get() { ... }
}
```
 
## <a id="redis-ssl"></a>Zorg ervoor dat communicatie tooAzure die redis-Cache via SSL is

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Redis-cache | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Azure Redis-SSL-ondersteuning](https://azure.microsoft.com/documentation/articles/cache-faq/#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis) |
| **Stappen** | Redis-server biedt geen ondersteuning voor SSL out of box hello, maar biedt Azure Redis-Cache. Als u verbinding tooAzure Redis-Cache maakt en de client SSL, zoals StackExchange.Redis ondersteunt, moet u SSL gebruiken. Niet-SSL-poort is standaard uitgeschakeld voor nieuwe exemplaren van Azure Redis-Cache. Zorg ervoor dat Hallo veilige standaardinstellingen niet zijn gewijzigd, tenzij er een afhankelijkheid op SSL-ondersteuning voor redis-clients. |

Houd er rekening mee dat Redis ontworpen toobe toegankelijk is voor vertrouwde clients binnen vertrouwde omgevingen is. Dit betekent dat meestal het niet een goed is idee tooexpose hello Redis exemplaar rechtstreeks toohello internet of in het algemeen tooan omgeving waarbij niet-vertrouwde clients rechtstreeks toegang tot Hallo Redis TCP-poort- of UNIX-socket. 

## <a id="device-field"></a>Gateway-apparaatcommunicatie tooField beveiligen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Veld IoT Gateway | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Voor IP-gebaseerde apparaten, is dit doorgaans in een SSL/TLS-kanaal tooprotect gegevens onderweg Hallo communicatieprotocol kan ingekapseld. Onderzoek als er beveiligde versies van het Hallo-protocol waarmee beveiliging op transport of bericht-laag voor andere protocollen die SSL/TLS niet ondersteunen. |

## <a id="device-cloud"></a>Apparaat tooCloud Gateway communicatie met behulp van SSL/TLS beveiligen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | IoT-Cloudgateway | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Kies uw communicatieprotocol](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#messaging) |
| **Stappen** | Protocollen die beveiligde HTTP-/ AMQP of MQTT met behulp van SSL/TLS. |
