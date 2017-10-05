---
title: Verbinding maken met Media Services-Account met .NET
description: Dit onderwerp wordt beschreven hoe u verbinding maken met met behulp van Media Services .NET.
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
ms.openlocfilehash: 892932116934952265a21ab17aac3434b5760136
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="connecting-to-media-services-account-using-media-services-sdk-for-net"></a>Verbinding maken met Media Services-Account met Media Services SDK voor .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-connect-programmatically.md)
> * [.NET](media-services-dotnet-connect-programmatically.md)
> 
> 

In dit onderwerp wordt beschreven hoe een programmatische verbinding met Microsoft Azure Media Services verkrijgen tijdens het programmeren met de Media Services SDK voor .NET.

## <a name="connecting-to-media-services"></a>Verbinding met mediaservices
Voor verbinding met Media Services via een programma, moet u hebben een Azure-account hebt ingesteld, Media Services zijn geconfigureerd op dat account en stel een Visual Studio-project voor het ontwikkelen met de Media Services SDK voor .NET. Zie voor meer informatie het installatieprogramma voor de ontwikkeling met de Media Services SDK voor .NET.

Aan het einde van het installatieproces van de Media Services-account, moet u de volgende waarden voor vereiste verbinding verkregen. Deze programmatische om verbindingen te maken met Media Services gebruiken.

* De naam van uw Media Services-account.
* De sleutel van uw Media Services-account.

Als u deze waarden zoekt, gaat u naar de Azure Management Portal, selecteert u uw Media Service-account en klik op de '**sleutels beheren**'-pictogram op de onderkant van het venster van de portal. Door op het pictogram naast elk tekstvak te klikken, wordt de waarde gekopieerd naar het systeemklembord.

## <a name="creating-a-cloudmediacontext-instance"></a>Het maken van een exemplaar CloudMediaContext
Beginnen met programmeren op basis van Media Services u wilt maken een **CloudMediaContext** -exemplaar dat de servercontext vertegenwoordigt. De **CloudMediaContext** bevat verwijzingen naar belangrijke verzamelingen, met inbegrip van taken, assets, bestanden, toegangsbeleid en locators.

> [!NOTE]
> De **CloudMediaContext** klasse is niet thread-veilig. Maak een nieuwe CloudMediaContext per thread of set bewerkingen.
> 
> 

CloudMediaContext heeft vijf constructor overloads. Het verdient aanbeveling gebruik constructors die **MediaServicesCredentials** als parameter. Zie voor meer informatie de **hergebruiken Access Control Service Tokens** die volgt. 

Het volgende voorbeeld wordt de openbare CloudMediaContext(MediaServicesCredentials credentials)-constructor:

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a>Access Control Service Tokens hergebruiken
Deze sectie wordt beschreven hoe Access Control Service tokens gebruiken met behulp van CloudMediaContext-constructors die MediaServicesCredentials als parameter.

[Azure Active Directory-toegangsbeheer](https://msdn.microsoft.com/library/hh147631.aspx) (ook wel bekend als Access Control Service of ACS) is een cloudservice waarmee u een eenvoudige manier voor verificatie en autoriseren van gebruikers toegang te krijgen tot hun webtoepassingen. Microsoft Azure Media Services controleert de toegang tot de services al OAuth-protocol dat een ACS-token is vereist. Media Services ontvangt de ACS-tokens van een server voor autorisatie.

Bij het ontwikkelen met de Media Services SDK, kunt u niet omgaan met de tokens omdat de SDK code managers ze voor u. Echter, zodat de SDK volledig beheer van de ACS-tokens leidt tot onnodige aanvragen voor beveiligingstokens. Aanvragen van tokens kost tijd en de client en server resources verbruikt. De ACS-server ook beperkt de aanvragen als de frequentie te hoog is. De limiet is 30 aanvragen per seconde, Zie [ACS-Service beperkingen](https://msdn.microsoft.com/library/gg185909.aspx) voor meer informatie.

U kunt de ACS-tokens vanaf de Media Services SDK versie 3.0.0.0-prestatiemeters kunt hergebruiken. De **CloudMediaContext** constructors die **MediaServicesCredentials** als een parameter Schakel het delen van de ACS-tokens tussen verschillende contexten. De klasse MediaServicesCredentials kapselt de Media Services-referenties. Als u een ACS-token beschikbaar is en de verlooptijd bekend is, kunt u een nieuw exemplaar van de MediaServicesCredentials maken met het token en doorgegeven aan de constructor van CloudMediaContext. Houd er rekening mee dat de Media Services SDK tokens automatisch vernieuwd wanneer ze zijn verlopen. Er zijn twee manieren om ACS-tokens, opnieuw te gebruiken zoals wordt weergegeven in de volgende voorbeelden.

* U kunt cache de **MediaServicesCredentials** object in het geheugen (bijvoorbeeld in een variabele van statische klasse). Vervolgens moet het object in de cache worden doorgegeven aan de constructor CloudMediaContext. Het object MediaServicesCredentials bevat een ACS-token die opnieuw kan worden gebruikt als het nog geldig is. Als het token niet geldig is, wordt deze vernieuwd door de Media Services SDK met de referenties die aan de constructor MediaServicesCredentials gegeven.
  
    Houd er rekening mee dat de **MediaServicesCredentials** object een geldig token opgehaald nadat de RefreshToken is aangeroepen. De **CloudMediaContext** aanroepen de **RefreshToken** methode in de constructor. Als u van plan bent de token waarden opslaan naar een externe opslag, moet u om te controleren of de waarde TokenExpiration geldig is voordat u de token gegevens opslaat. Het is geen geldige, belt RefreshToken voordat het in cache opslaan.
  
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use the cached credentials to create a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* U kunt ook de AccessToken tekenreeks en de waarden TokenExpiration cache. De waarden kunnen later worden gebruikt voor het maken van een nieuw MediaServicesCredentials-object met gegevens in de cache-token.  Dit is vooral nuttig voor scenario's waar het token kan veilig worden gedeeld tussen meerdere processen en computers.
  
    De volgende codefragmenten de SaveTokenDataToExternalStorage GetTokenDataFromExternalStorage en UpdateTokenDataInExternalStorageIfNeeded methoden aanroepen die niet zijn gedefinieerd in dit voorbeeld. U kunt deze methoden voor het opslaan, ophalen en token gegevens bijwerken in een externe opslag definiëren. 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from the context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // The SaveTokenDataToExternalStorage method should check 
        // whether the TokenExpiration value is valid before saving the token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    Gebruik de opgeslagen waarden voor de token MediaServicesCredentials maken.

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

    Het token exemplaar bijwerken als het token is bijgewerkt door de Media Services SDK. 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* Als u meerdere accounts voor Media Services (bijvoorbeeld voor belastingverdeling doeleinden of Geo-distributie) hebt u MediaServicesCredentials objecten met behulp van de verzameling System.Collections.Concurrent.ConcurrentDictionary (de ConcurrentDictionary in cache collectie bevat een thread-veilige van sleutel-waardeparen die toegankelijk zijn voor meerdere threads tegelijk). Vervolgens gebruikt u de methode GetOrAdd ophalen van referenties in de cache. 
  
        // Declare a static class variable of the ConcurrentDictionary type in which the Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials to create a new CloudMediaContext object.
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

## <a name="connecting-to-a-media-services-account-located-in-the-north-china-region"></a>Verbinding maken met een Media Services-account zich in de regio Noord, China
Als uw account in de regio Noord, China bevindt zich, gebruikt u de volgende constructor:

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

Bijvoorbeeld:

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a>Verbindingswaarden in de configuratie opslaan
Het is een sterk aanbevolen procedure voor het opslaan van verbindingswaarden, zoals uw accountnaam en wachtwoord, met name gevoelige waarden in de configuratie. Het is ook een aanbevolen procedure voor het versleutelen van gevoelige configuratiegegevens. U kunt het hele configuratiebestand versleutelen met behulp van Windows Encrypting File System (EFS). Zodat EFS op een bestand met de rechtermuisknop op het bestand, selecteer **eigenschappen**, en schakel versleuteling in de **Geavanceerd** tabblad instellingen. Of u een aangepaste oplossing voor het versleutelen van de geselecteerde gedeelten van een configuratiebestand met behulp van beveiligde configuratie kunt maken. Zie [versleutelen met behulp van beveiligde configuratie configuratiegegevens](https://msdn.microsoft.com/library/53tyfkaw.aspx).

Het volgende App.config-bestand bevat de waarden van de vereiste. De waarden in de <appSettings> element zijn de vereiste waarden die u hebt verkregen van het installatieproces van de Media Services-account.

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


Voor het ophalen van verbindingswaarden van configuratie, kunt u de **ConfigurationManager** klasse en vervolgens de waarden toewijzen aan velden in uw code:

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

