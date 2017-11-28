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
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a><span data-ttu-id="417d1-103">Verbinding maken met tooMedia Services-Account met Media Services SDK voor .NET</span><span class="sxs-lookup"><span data-stu-id="417d1-103">Connecting tooMedia Services Account using Media Services SDK for .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="417d1-104">REST</span><span class="sxs-lookup"><span data-stu-id="417d1-104">REST</span></span>](media-services-rest-connect-programmatically.md)
> * [<span data-ttu-id="417d1-105">.NET</span><span class="sxs-lookup"><span data-stu-id="417d1-105">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> 
> 

<span data-ttu-id="417d1-106">Dit onderwerp wordt beschreven hoe tooobtain een programmatische verbinding tooMicrosoft Azure Media Services tijdens het programmeren met Media Services SDK voor .NET Hallo.</span><span class="sxs-lookup"><span data-stu-id="417d1-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services SDK for .NET.</span></span>

## <a name="connecting-toomedia-services"></a><span data-ttu-id="417d1-107">Verbinding maken met tooMedia Services</span><span class="sxs-lookup"><span data-stu-id="417d1-107">Connecting tooMedia Services</span></span>
<span data-ttu-id="417d1-108">tooconnect tooMedia Services via een programma, u moet hebben een Azure-account hebt ingesteld, Media Services zijn geconfigureerd op dat account en stel een Visual Studio-project voor de ontwikkeling met Hallo Media Services SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="417d1-108">tooconnect tooMedia Services programmatically, you must have previously set up an Azure account, configured Media Services on that account, and then set up a Visual Studio project for development with hello Media Services SDK for .NET.</span></span> <span data-ttu-id="417d1-109">Zie voor meer informatie Setup voor de ontwikkeling van Hello Media Services SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="417d1-109">For more information, see Setup for Development with hello Media Services SDK for .NET.</span></span>

<span data-ttu-id="417d1-110">Aan het einde van de Hallo van Hallo Media Services-account-installatieproces, die u hebt verkregen Hallo volgende verplichte verbindingswaarden.</span><span class="sxs-lookup"><span data-stu-id="417d1-110">At hello end of hello Media Services account setup process, you obtained hello following required connection values.</span></span> <span data-ttu-id="417d1-111">Gebruik deze toomake programmatische verbindingen tooMedia Services.</span><span class="sxs-lookup"><span data-stu-id="417d1-111">Use these toomake programmatic connections tooMedia Services.</span></span>

* <span data-ttu-id="417d1-112">De naam van uw Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="417d1-112">Your Media Services account name.</span></span>
* <span data-ttu-id="417d1-113">De sleutel van uw Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="417d1-113">Your Media Services account key.</span></span>

<span data-ttu-id="417d1-114">toofind deze waarden, gaat u toohello Azure Management Portal, selecteert u uw Media Service-account en klik op Hallo '**sleutels beheren**'-pictogram op Hallo onder aan de portal Hallo-venster.</span><span class="sxs-lookup"><span data-stu-id="417d1-114">toofind these values, go toohello Azure Managment Portal, select your Media Service account, and click on hello “**MANAGE KEYS**” icon on hello bottom of hello portal window.</span></span> <span data-ttu-id="417d1-115">Op Hallo pictogram volgende tooeach tekst vak kopieën Hallo waarde toohello systeemklembord te klikken.</span><span class="sxs-lookup"><span data-stu-id="417d1-115">Clicking on hello icon next tooeach text box copies hello value toohello system clipboard.</span></span>

## <a name="creating-a-cloudmediacontext-instance"></a><span data-ttu-id="417d1-116">Het maken van een exemplaar CloudMediaContext</span><span class="sxs-lookup"><span data-stu-id="417d1-116">Creating a CloudMediaContext Instance</span></span>
<span data-ttu-id="417d1-117">toostart programmeren met Media Services moet u toocreate een **CloudMediaContext** -exemplaar dat Hallo servercontext vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="417d1-117">toostart programming against Media Services you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="417d1-118">Hallo **CloudMediaContext** verwijzingen tooimportant verzamelingen, met inbegrip van taken, assets, bestanden, toegangsbeleid en locators bevat.</span><span class="sxs-lookup"><span data-stu-id="417d1-118">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span>

> [!NOTE]
> <span data-ttu-id="417d1-119">Hallo **CloudMediaContext** klasse is niet thread-veilig.</span><span class="sxs-lookup"><span data-stu-id="417d1-119">hello **CloudMediaContext** class is not thread safe.</span></span> <span data-ttu-id="417d1-120">Maak een nieuwe CloudMediaContext per thread of set bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="417d1-120">You should create a new CloudMediaContext per thread or per set of operations.</span></span>
> 
> 

<span data-ttu-id="417d1-121">CloudMediaContext heeft vijf constructor overloads.</span><span class="sxs-lookup"><span data-stu-id="417d1-121">CloudMediaContext has five constructor overloads.</span></span> <span data-ttu-id="417d1-122">Het is aanbevolen toouse-constructors die **MediaServicesCredentials** als parameter.</span><span class="sxs-lookup"><span data-stu-id="417d1-122">It is recommended toouse constructors that take **MediaServicesCredentials** as a parameter.</span></span> <span data-ttu-id="417d1-123">Zie voor meer informatie, Hallo **hergebruiken Access Control Service Tokens** die volgt.</span><span class="sxs-lookup"><span data-stu-id="417d1-123">For more information, see hello **Reusing Access Control Service Tokens** that follows.</span></span> 

<span data-ttu-id="417d1-124">Hallo wordt volgende voorbeeld de openbare CloudMediaContext(MediaServicesCredentials credentials) constructor Hallo:</span><span class="sxs-lookup"><span data-stu-id="417d1-124">hello following example uses hello public CloudMediaContext(MediaServicesCredentials credentials) constructor:</span></span>

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a><span data-ttu-id="417d1-125">Access Control Service Tokens hergebruiken</span><span class="sxs-lookup"><span data-stu-id="417d1-125">Reusing Access Control Service Tokens</span></span>
<span data-ttu-id="417d1-126">Deze sectie wordt beschreven hoe tooreuse Access Control Service tokens met behulp van CloudMediaContext-constructors die MediaServicesCredentials als parameter.</span><span class="sxs-lookup"><span data-stu-id="417d1-126">This section shows how tooreuse Access Control Service tokens by using CloudMediaContext constructors that take MediaServicesCredentials as a parameter.</span></span>

<span data-ttu-id="417d1-127">[Azure Active Directory-toegangsbeheer](https://msdn.microsoft.com/library/hh147631.aspx) (ook wel bekend als Access Control Service of ACS) is een cloudservice waarmee u een eenvoudige manier toegang toogain verificatie en autorisatie tootheir webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="417d1-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (also known as Access Control Service or ACS) is a cloud-based service that provides an easy way of authenticating and authorizing users toogain access tootheir web applications.</span></span> <span data-ttu-id="417d1-128">Microsoft Azure Media Services-besturingselementen toegangsservices tooits echter OAuth-protocol dat een ACS-token is vereist.</span><span class="sxs-lookup"><span data-stu-id="417d1-128">Microsoft Azure Media Services controls access tooits services though OAuth protocol that requires an ACS token.</span></span> <span data-ttu-id="417d1-129">Media Services ontvangt Hallo ACS-tokens van een server voor autorisatie.</span><span class="sxs-lookup"><span data-stu-id="417d1-129">Media Services receives hello ACS tokens from an authorization server.</span></span>

<span data-ttu-id="417d1-130">Bij het ontwikkelen van Media Services SDK Hello, kunt u toonot behandelen Hallo tokens omdat Hallo SDK code managers ze voor u.</span><span class="sxs-lookup"><span data-stu-id="417d1-130">When developing with hello Media Services SDK, you can choose toonot deal with hello tokens because hello SDK code managers them for you.</span></span> <span data-ttu-id="417d1-131">Volledig beheren waarin Hallo SDK echter Hallo ACS tokens leads toounnecessary aanvragen voor beveiligingstokens.</span><span class="sxs-lookup"><span data-stu-id="417d1-131">However, letting hello SDK fully manage hello ACS tokens leads toounnecessary token requests.</span></span> <span data-ttu-id="417d1-132">Aanvragen van tokens kost tijd en Hallo client en server bronnen.</span><span class="sxs-lookup"><span data-stu-id="417d1-132">Requesting tokens takes time and consumes hello client and server resources.</span></span> <span data-ttu-id="417d1-133">Hallo ACS-server ook bandbreedte Hallo aanvragen als Hallo snelheid te hoog is.</span><span class="sxs-lookup"><span data-stu-id="417d1-133">Also, hello ACS server throttles hello requests if hello rate is too high.</span></span> <span data-ttu-id="417d1-134">Hallo limiet is 30 aanvragen per seconde, raadpleegt u [ACS-Service beperkingen](https://msdn.microsoft.com/library/gg185909.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="417d1-134">hello limit is 30 requests per second, see [ACS Service Limitations](https://msdn.microsoft.com/library/gg185909.aspx) for more details.</span></span>

<span data-ttu-id="417d1-135">Beginnen met Media Services SDK versie 3.0.0.0-prestatiemeters hello, kunt u de ACS-tokens Hallo hergebruiken.</span><span class="sxs-lookup"><span data-stu-id="417d1-135">Starting with hello Media Services SDK version 3.0.0.0, you can reuse hello ACS tokens.</span></span> <span data-ttu-id="417d1-136">Hallo **CloudMediaContext** constructors die **MediaServicesCredentials** inschakelen als een parameter delen Hallo ACS-tokens tussen verschillende contexten.</span><span class="sxs-lookup"><span data-stu-id="417d1-136">hello **CloudMediaContext** constructors that take **MediaServicesCredentials** as a parameter enable sharing hello ACS tokens between multiple contexts.</span></span> <span data-ttu-id="417d1-137">Hallo MediaServicesCredentials klasse ingekapseld Hallo Media Services-referenties.</span><span class="sxs-lookup"><span data-stu-id="417d1-137">hello MediaServicesCredentials class encapsulates hello Media Services credentials.</span></span> <span data-ttu-id="417d1-138">Als u een ACS-token beschikbaar is en de verlooptijd bekend is, kunt u een nieuw exemplaar van de MediaServicesCredentials maken met Hallo token en toohello constructor van CloudMediaContext doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="417d1-138">If an ACS token is available and its expiration time is known, you can create a new MediaServicesCredentials instance with hello token and pass it toohello constructor of CloudMediaContext.</span></span> <span data-ttu-id="417d1-139">Let op Hallo van Media Services SDK automatisch vernieuwd tokens wanneer ze zijn verlopen.</span><span class="sxs-lookup"><span data-stu-id="417d1-139">Note that hello Media Services SDK automatically refreshes tokens whenever they expire.</span></span> <span data-ttu-id="417d1-140">Er zijn twee manieren tooreuse ACS-tokens, zoals wordt weergegeven in onderstaande Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="417d1-140">There are two ways tooreuse ACS tokens, as shown in hello examples below.</span></span>

* <span data-ttu-id="417d1-141">U kunt Hallo cache **MediaServicesCredentials** object in het geheugen (bijvoorbeeld in een variabele van statische klasse).</span><span class="sxs-lookup"><span data-stu-id="417d1-141">You can cache hello **MediaServicesCredentials** object in memory (for example, in a static class variable).</span></span> <span data-ttu-id="417d1-142">Vervolgens, in de cache opgeslagen Hallo object toohello CloudMediaContext constructor worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="417d1-142">Then, pass hello cached object toohello CloudMediaContext constructor.</span></span> <span data-ttu-id="417d1-143">Hallo MediaServicesCredentials object bevat een ACS-token die opnieuw kan worden gebruikt als het nog geldig is.</span><span class="sxs-lookup"><span data-stu-id="417d1-143">hello MediaServicesCredentials object contains an ACS token that can be reused if it is still valid.</span></span> <span data-ttu-id="417d1-144">Als Hallo-token niet geldig is is, dat wordt deze vernieuwd door Hallo gegeven Media Services SDK met de referenties Hallo toohello MediaServicesCredentials constructor.</span><span class="sxs-lookup"><span data-stu-id="417d1-144">If hello token is not valid, it will be refreshed by hello Media Services SDK using hello credentials given toohello MediaServicesCredentials constructor.</span></span>
  
    <span data-ttu-id="417d1-145">Houd er rekening mee dat Hallo **MediaServicesCredentials** object een geldig token na Hallo RefreshToken heet opgehaald.</span><span class="sxs-lookup"><span data-stu-id="417d1-145">Note that hello **MediaServicesCredentials** object gets a valid token after hello RefreshToken is called.</span></span> <span data-ttu-id="417d1-146">Hallo **CloudMediaContext** aanroepen Hallo **RefreshToken** methode in Hallo-constructor.</span><span class="sxs-lookup"><span data-stu-id="417d1-146">hello **CloudMediaContext** calls hello **RefreshToken** method in hello constructor.</span></span> <span data-ttu-id="417d1-147">Als u van plan bent toosave Hallo token waarden tooan externe opslag, moet u ervoor toocheck of Hallo TokenExpiration waarde geldig is voordat Hallo token gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="417d1-147">If you are planning toosave hello token values tooan external storage, make sure toocheck whether hello TokenExpiration value is valid before saving hello token data.</span></span> <span data-ttu-id="417d1-148">Het is geen geldige, belt RefreshToken voordat het in cache opslaan.</span><span class="sxs-lookup"><span data-stu-id="417d1-148">If it is not valid, call RefreshToken before caching.</span></span>
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* <span data-ttu-id="417d1-149">U kunt ook cache Hallo AccessToken tekenreeks en Hallo TokenExpiration waarden.</span><span class="sxs-lookup"><span data-stu-id="417d1-149">You can also cache hello AccessToken string and hello TokenExpiration values.</span></span> <span data-ttu-id="417d1-150">Hallo-waarden kunnen later worden gebruikte toocreate een nieuwe MediaServicesCredentials object met cache Hallo token gegevens.</span><span class="sxs-lookup"><span data-stu-id="417d1-150">hello values could later be used toocreate a new MediaServicesCredentials object with hello cached token data.</span></span>  <span data-ttu-id="417d1-151">Dit is vooral nuttig voor scenario's waarbij Hallo token kan veilig worden gedeeld tussen meerdere processen en computers.</span><span class="sxs-lookup"><span data-stu-id="417d1-151">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
  
    <span data-ttu-id="417d1-152">Hallo volgende codefragmenten Hallo SaveTokenDataToExternalStorage GetTokenDataFromExternalStorage en UpdateTokenDataInExternalStorageIfNeeded methoden aanroepen die niet zijn gedefinieerd in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="417d1-152">hello following code snippets call hello SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage, and UpdateTokenDataInExternalStorageIfNeeded methods that are not defined in this example.</span></span> <span data-ttu-id="417d1-153">U kunt deze methoden toostore, ophalen en token updategegevens definiëren in een externe opslag.</span><span class="sxs-lookup"><span data-stu-id="417d1-153">You could define these methods toostore, retrieve, and update token data in an external storage.</span></span> 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    <span data-ttu-id="417d1-154">Gebruik Hallo token waarden toocreate MediaServicesCredentials opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="417d1-154">Use hello saved token values toocreate MediaServicesCredentials.</span></span>

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

    <span data-ttu-id="417d1-155">Hallo token exemplaar bijwerken als Hallo-token is bijgewerkt door Hallo Media Services SDK.</span><span class="sxs-lookup"><span data-stu-id="417d1-155">Update hello token copy in case hello token was updated by hello Media Services SDK.</span></span> 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* <span data-ttu-id="417d1-156">Als u meerdere accounts voor Media Services (bijvoorbeeld voor belastingverdeling doeleinden of Geo-distributie) hebt u kan objecten in een cache MediaServicesCredentials hello System.Collections.Concurrent.ConcurrentDictionary collectie (hello gebruiken ConcurrentDictionary collectie bevat een thread-veilige van sleutel-waardeparen die toegankelijk zijn voor meerdere threads tegelijk).</span><span class="sxs-lookup"><span data-stu-id="417d1-156">If you have multiple Media Services accounts (for example, for load sharing purposes or Geo-distribution) you can cache MediaServicesCredentials objects using hello System.Collections.Concurrent.ConcurrentDictionary collection (hello ConcurrentDictionary collection represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently).</span></span> <span data-ttu-id="417d1-157">U kunt vervolgens Hallo GetOrAdd methode tooget Hallo in de cache opgeslagen referenties gebruiken.</span><span class="sxs-lookup"><span data-stu-id="417d1-157">You can then use hello GetOrAdd method tooget hello cached credentials.</span></span> 
  
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

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a><span data-ttu-id="417d1-158">Verbinding maken met tooa Media Services-account zich in de regio Noord, China Hallo</span><span class="sxs-lookup"><span data-stu-id="417d1-158">Connecting tooa Media Services account located in hello North China region</span></span>
<span data-ttu-id="417d1-159">Als uw account in de regio Noord, China hello bevindt zich, gebruikt u Hallo constructor te volgen:</span><span class="sxs-lookup"><span data-stu-id="417d1-159">If your account is located in hello North China region, use hello following constructor:</span></span>

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

<span data-ttu-id="417d1-160">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="417d1-160">For example:</span></span>

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a><span data-ttu-id="417d1-161">Verbindingswaarden in de configuratie opslaan</span><span class="sxs-lookup"><span data-stu-id="417d1-161">Storing Connection Values in Configuration</span></span>
<span data-ttu-id="417d1-162">Het is een verbindingswaarden ten zeerste aanbevolen toostore, met name gevoelige waarden zoals uw accountnaam en wachtwoord in de configuratie.</span><span class="sxs-lookup"><span data-stu-id="417d1-162">It is a highly recommended practice toostore connection values, especially sensitive values such as your account name and password, in configuration.</span></span> <span data-ttu-id="417d1-163">Het is ook een aanbevolen procedure tooencrypt configuratie van gevoelige gegevens.</span><span class="sxs-lookup"><span data-stu-id="417d1-163">Also, it is a recommended practice tooencrypt sensitive configuration data.</span></span> <span data-ttu-id="417d1-164">U kunt de hele configuratiebestand Hallo versleutelen met behulp van Hallo Windows Encrypting File System (EFS).</span><span class="sxs-lookup"><span data-stu-id="417d1-164">You can encrypt hello entire configuration file by using hello Windows Encrypting File System (EFS).</span></span> <span data-ttu-id="417d1-165">tooenable EFS op een bestand, klik met de rechtermuisknop hello, selecteer **eigenschappen**, en schakel versleuteling in Hallo **Geavanceerd** tabblad instellingen. Of u een aangepaste oplossing voor het versleutelen van de geselecteerde gedeelten van een configuratiebestand met behulp van beveiligde configuratie kunt maken.</span><span class="sxs-lookup"><span data-stu-id="417d1-165">tooenable EFS on a file, right-click hello file, select **Properties**, and enable encryption in hello **Advanced** settings tab. Or you can create a custom solution for encrypting selected portions of a configuration file by using protected configuration.</span></span> <span data-ttu-id="417d1-166">Zie [versleutelen met behulp van beveiligde configuratie configuratiegegevens](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span><span class="sxs-lookup"><span data-stu-id="417d1-166">See [Encrypting Configuration Information Using Protected Configuration](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span></span>

<span data-ttu-id="417d1-167">Hallo na App.config-bestand bevat verbindingswaarden Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="417d1-167">hello following App.config file contains hello required connection values.</span></span> <span data-ttu-id="417d1-168">waarden in Hallo Hallo <appSettings> element zijn Hallo vereist waarden die u hebt gekregen Hallo Media Services-account-installatieproces.</span><span class="sxs-lookup"><span data-stu-id="417d1-168">hello values in hello <appSettings> element are hello required values that you got from hello Media Services account setup process.</span></span>

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


<span data-ttu-id="417d1-169">verbindingswaarden tooretrieve uit configuratie, kunt u Hallo **ConfigurationManager** klasse en wijs vervolgens Hallo waarden toofields in uw code:</span><span class="sxs-lookup"><span data-stu-id="417d1-169">tooretrieve connection values from configuration, you can use hello **ConfigurationManager** class and then assign hello values toofields in your code:</span></span>

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a><span data-ttu-id="417d1-170">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="417d1-170">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="417d1-171">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="417d1-171">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

