---
title: aaaConnecting tooMedia Services-Account met .NET
description: Dit onderwerp wordt beschreven hoe tooconnect tooMedia Services met behulp .NET.
services: media-services
documentationcenter: 
author: juliako
manager: erikre
editor: 
ms.assetid: a8412a29-59dc-44a0-ace0-be79a97dab63
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: a23bd285f7cae17ae5831e1e50e73947afbb9a3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a>Verbinding maken met tooMedia Services-Account met Media Services SDK voor .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-connect-programmatically.md)
> * [.NET](media-services-dotnet-connect-programmatically.md)
> 
> 

Dit onderwerp wordt beschreven hoe tooobtain een programmatische verbinding tooMicrosoft Azure Media Services tijdens het programmeren met Media Services SDK voor .NET Hallo.

## <a name="connecting-toomedia-services"></a>Verbinding maken met tooMedia Services
tooconnect tooMedia Services via een programma, u moet hebben een Azure-account hebt ingesteld, Media Services zijn geconfigureerd op dat account en stel een Visual Studio-project voor de ontwikkeling met Hallo Media Services SDK voor .NET. Zie voor meer informatie Setup voor de ontwikkeling van Hello Media Services SDK voor .NET.

Aan het einde van de Hallo van Hallo Media Services-account-installatieproces, die u hebt verkregen Hallo volgende verplichte verbindingswaarden. Gebruik deze toomake programmatische verbindingen tooMedia Services.

* De naam van uw Media Services-account.
* De sleutel van uw Media Services-account.

toofind deze waarden, gaat u toohello Azure Management Portal, selecteert u uw Media Service-account en klik op Hallo '**sleutels beheren**'-pictogram op Hallo onder aan de portal Hallo-venster. Op Hallo pictogram volgende tooeach tekst vak kopieën Hallo waarde toohello systeemklembord te klikken.

## <a name="creating-a-cloudmediacontext-instance"></a>Het maken van een exemplaar CloudMediaContext
toostart programmeren met Media Services moet u toocreate een **CloudMediaContext** -exemplaar dat Hallo servercontext vertegenwoordigt. Hallo **CloudMediaContext** verwijzingen tooimportant verzamelingen, met inbegrip van taken, assets, bestanden, toegangsbeleid en locators bevat.

> [!NOTE]
> Hallo **CloudMediaContext** klasse is niet thread-veilig. Maak een nieuwe CloudMediaContext per thread of set bewerkingen.
> 
> 

CloudMediaContext heeft vijf constructor overloads. Het is aanbevolen toouse-constructors die **MediaServicesCredentials** als parameter. Zie voor meer informatie, Hallo **hergebruiken Access Control Service Tokens** die volgt. 

Hallo wordt volgende voorbeeld de openbare CloudMediaContext(MediaServicesCredentials credentials) constructor Hallo:

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a>Access Control Service Tokens hergebruiken
Deze sectie wordt beschreven hoe tooreuse Access Control Service tokens met behulp van CloudMediaContext-constructors die MediaServicesCredentials als parameter.

[Azure Active Directory-toegangsbeheer](https://msdn.microsoft.com/library/hh147631.aspx) (ook wel bekend als Access Control Service of ACS) is een cloudservice waarmee u een eenvoudige manier toegang toogain verificatie en autorisatie tootheir webtoepassingen. Microsoft Azure Media Services-besturingselementen toegangsservices tooits echter OAuth-protocol dat een ACS-token is vereist. Media Services ontvangt Hallo ACS-tokens van een server voor autorisatie.

Bij het ontwikkelen van Media Services SDK Hello, kunt u toonot behandelen Hallo tokens omdat Hallo SDK code managers ze voor u. Volledig beheren waarin Hallo SDK echter Hallo ACS tokens leads toounnecessary aanvragen voor beveiligingstokens. Aanvragen van tokens kost tijd en Hallo client en server bronnen. Hallo ACS-server ook bandbreedte Hallo aanvragen als Hallo snelheid te hoog is. Hallo limiet is 30 aanvragen per seconde, raadpleegt u [ACS-Service beperkingen](https://msdn.microsoft.com/library/gg185909.aspx) voor meer informatie.

Beginnen met Media Services SDK versie 3.0.0.0-prestatiemeters hello, kunt u de ACS-tokens Hallo hergebruiken. Hallo **CloudMediaContext** constructors die **MediaServicesCredentials** inschakelen als een parameter delen Hallo ACS-tokens tussen verschillende contexten. Hallo MediaServicesCredentials klasse ingekapseld Hallo Media Services-referenties. Als u een ACS-token beschikbaar is en de verlooptijd bekend is, kunt u een nieuw exemplaar van de MediaServicesCredentials maken met Hallo token en toohello constructor van CloudMediaContext doorgegeven. Let op Hallo van Media Services SDK automatisch vernieuwd tokens wanneer ze zijn verlopen. Er zijn twee manieren tooreuse ACS-tokens, zoals wordt weergegeven in onderstaande Hallo voorbeelden.

* U kunt Hallo cache **MediaServicesCredentials** object in het geheugen (bijvoorbeeld in een variabele van statische klasse). Vervolgens, in de cache opgeslagen Hallo object toohello CloudMediaContext constructor worden doorgegeven. Hallo MediaServicesCredentials object bevat een ACS-token die opnieuw kan worden gebruikt als het nog geldig is. Als Hallo-token niet geldig is is, dat wordt deze vernieuwd door Hallo gegeven Media Services SDK met de referenties Hallo toohello MediaServicesCredentials constructor.
  
    Houd er rekening mee dat Hallo **MediaServicesCredentials** object een geldig token na Hallo RefreshToken heet opgehaald. Hallo **CloudMediaContext** aanroepen Hallo **RefreshToken** methode in Hallo-constructor. Als u van plan bent toosave Hallo token waarden tooan externe opslag, moet u ervoor toocheck of Hallo TokenExpiration waarde geldig is voordat Hallo token gegevens worden opgeslagen. Het is geen geldige, belt RefreshToken voordat het in cache opslaan.
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* U kunt ook cache Hallo AccessToken tekenreeks en Hallo TokenExpiration waarden. Hallo-waarden kunnen later worden gebruikte toocreate een nieuwe MediaServicesCredentials object met cache Hallo token gegevens.  Dit is vooral nuttig voor scenario's waarbij Hallo token kan veilig worden gedeeld tussen meerdere processen en computers.
  
    Hallo volgende codefragmenten Hallo SaveTokenDataToExternalStorage GetTokenDataFromExternalStorage en UpdateTokenDataInExternalStorageIfNeeded methoden aanroepen die niet zijn gedefinieerd in dit voorbeeld. U kunt deze methoden toostore, ophalen en token updategegevens definiëren in een externe opslag. 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    Gebruik Hallo token waarden toocreate MediaServicesCredentials opgeslagen.

        var accessToken = "";
        var tokenExpiration = DateTime.UtcNow;

        // Retrieve saved token values.
        GetTokenDataFromExternalStorage(out accessToken, out tokenExpiration);

        // Create a new MediaServicesCredentials object using saved token values.
        MediaServicesCredentials credentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey)
        {
            AccessToken = accessToken,
            TokenExpiration = tokenExpiration
        };

        CloudMediaContext context2 = new CloudMediaContext(credentials);

    Hallo token exemplaar bijwerken als Hallo-token is bijgewerkt door Hallo Media Services SDK. 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* Als u meerdere accounts voor Media Services (bijvoorbeeld voor belastingverdeling doeleinden of Geo-distributie) hebt u kan objecten in een cache MediaServicesCredentials hello System.Collections.Concurrent.ConcurrentDictionary collectie (hello gebruiken ConcurrentDictionary collectie bevat een thread-veilige van sleutel-waardeparen die toegankelijk zijn voor meerdere threads tegelijk). U kunt vervolgens Hallo GetOrAdd methode tooget Hallo in de cache opgeslagen referenties gebruiken. 
  
        // Declare a static class variable of hello ConcurrentDictionary type in which hello Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials toocreate a new CloudMediaContext object.
        static public CloudMediaContext CreateMediaServicesContext(string accountName, string accountKey)
        {
            CloudMediaContext cloudMediaContext;
            MediaServicesCredentials mediaServicesCredentials;

            mediaServicesCredentials = mediaServicesCredentialsCache.GetOrAdd(
                accountName,
                valueFactory => new MediaServicesCredentials(accountName, accountKey));

            cloudMediaContext = new CloudMediaContext(mediaServicesCredentials);

            return cloudMediaContext;
        }

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a>Verbinding maken met tooa Media Services-account zich in de regio Noord, China Hallo
Als uw account in de regio Noord, China hello bevindt zich, gebruikt u Hallo constructor te volgen:

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

Bijvoorbeeld:

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a>Verbindingswaarden in de configuratie opslaan
Het is een verbindingswaarden ten zeerste aanbevolen toostore, met name gevoelige waarden zoals uw accountnaam en wachtwoord in de configuratie. Het is ook een aanbevolen procedure tooencrypt configuratie van gevoelige gegevens. U kunt de hele configuratiebestand Hallo versleutelen met behulp van Hallo Windows Encrypting File System (EFS). tooenable EFS op een bestand, klik met de rechtermuisknop hello, selecteer **eigenschappen**, en schakel versleuteling in Hallo **Geavanceerd** tabblad instellingen. Of u een aangepaste oplossing voor het versleutelen van de geselecteerde gedeelten van een configuratiebestand met behulp van beveiligde configuratie kunt maken. Zie [versleutelen met behulp van beveiligde configuratie configuratiegegevens](https://msdn.microsoft.com/library/53tyfkaw.aspx).

Hallo na App.config-bestand bevat verbindingswaarden Hallo vereist. waarden in Hallo Hallo <appSettings> element zijn Hallo vereist waarden die u hebt gekregen Hallo Media Services-account-installatieproces.

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


verbindingswaarden tooretrieve uit configuratie, kunt u Hallo **ConfigurationManager** klasse en wijs vervolgens Hallo waarden toofields in uw code:

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

