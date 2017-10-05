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
# <a name="connecting-to-media-services-account-using-media-services-sdk-for-net"></a><span data-ttu-id="f216f-103">Verbinding maken met Media Services-Account met Media Services SDK voor .NET</span><span class="sxs-lookup"><span data-stu-id="f216f-103">Connecting to Media Services Account using Media Services SDK for .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f216f-104">REST</span><span class="sxs-lookup"><span data-stu-id="f216f-104">REST</span></span>](media-services-rest-connect-programmatically.md)
> * [<span data-ttu-id="f216f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f216f-105">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> 
> 

<span data-ttu-id="f216f-106">In dit onderwerp wordt beschreven hoe een programmatische verbinding met Microsoft Azure Media Services verkrijgen tijdens het programmeren met de Media Services SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="f216f-106">This topic describes how to obtain a programmatic connection to Microsoft Azure Media Services when you are programming with the Media Services SDK for .NET.</span></span>

## <a name="connecting-to-media-services"></a><span data-ttu-id="f216f-107">Verbinding met mediaservices</span><span class="sxs-lookup"><span data-stu-id="f216f-107">Connecting to Media Services</span></span>
<span data-ttu-id="f216f-108">Voor verbinding met Media Services via een programma, moet u hebben een Azure-account hebt ingesteld, Media Services zijn geconfigureerd op dat account en stel een Visual Studio-project voor het ontwikkelen met de Media Services SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="f216f-108">To connect to Media Services programmatically, you must have previously set up an Azure account, configured Media Services on that account, and then set up a Visual Studio project for development with the Media Services SDK for .NET.</span></span> <span data-ttu-id="f216f-109">Zie voor meer informatie het installatieprogramma voor de ontwikkeling met de Media Services SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="f216f-109">For more information, see Setup for Development with the Media Services SDK for .NET.</span></span>

<span data-ttu-id="f216f-110">Aan het einde van het installatieproces van de Media Services-account, moet u de volgende waarden voor vereiste verbinding verkregen.</span><span class="sxs-lookup"><span data-stu-id="f216f-110">At the end of the Media Services account setup process, you obtained the following required connection values.</span></span> <span data-ttu-id="f216f-111">Deze programmatische om verbindingen te maken met Media Services gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f216f-111">Use these to make programmatic connections to Media Services.</span></span>

* <span data-ttu-id="f216f-112">De naam van uw Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="f216f-112">Your Media Services account name.</span></span>
* <span data-ttu-id="f216f-113">De sleutel van uw Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="f216f-113">Your Media Services account key.</span></span>

<span data-ttu-id="f216f-114">Als u deze waarden zoekt, gaat u naar de Azure Management Portal, selecteert u uw Media Service-account en klik op de '**sleutels beheren**'-pictogram op de onderkant van het venster van de portal.</span><span class="sxs-lookup"><span data-stu-id="f216f-114">To find these values, go to the Azure Managment Portal, select your Media Service account, and click on the “**MANAGE KEYS**” icon on the bottom of the portal window.</span></span> <span data-ttu-id="f216f-115">Door op het pictogram naast elk tekstvak te klikken, wordt de waarde gekopieerd naar het systeemklembord.</span><span class="sxs-lookup"><span data-stu-id="f216f-115">Clicking on the icon next to each text box copies the value to the system clipboard.</span></span>

## <a name="creating-a-cloudmediacontext-instance"></a><span data-ttu-id="f216f-116">Het maken van een exemplaar CloudMediaContext</span><span class="sxs-lookup"><span data-stu-id="f216f-116">Creating a CloudMediaContext Instance</span></span>
<span data-ttu-id="f216f-117">Beginnen met programmeren op basis van Media Services u wilt maken een **CloudMediaContext** -exemplaar dat de servercontext vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="f216f-117">To start programming against Media Services you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="f216f-118">De **CloudMediaContext** bevat verwijzingen naar belangrijke verzamelingen, met inbegrip van taken, assets, bestanden, toegangsbeleid en locators.</span><span class="sxs-lookup"><span data-stu-id="f216f-118">The **CloudMediaContext** includes references to important collections including jobs, assets, files, access policies, and locators.</span></span>

> [!NOTE]
> <span data-ttu-id="f216f-119">De **CloudMediaContext** klasse is niet thread-veilig.</span><span class="sxs-lookup"><span data-stu-id="f216f-119">The **CloudMediaContext** class is not thread safe.</span></span> <span data-ttu-id="f216f-120">Maak een nieuwe CloudMediaContext per thread of set bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="f216f-120">You should create a new CloudMediaContext per thread or per set of operations.</span></span>
> 
> 

<span data-ttu-id="f216f-121">CloudMediaContext heeft vijf constructor overloads.</span><span class="sxs-lookup"><span data-stu-id="f216f-121">CloudMediaContext has five constructor overloads.</span></span> <span data-ttu-id="f216f-122">Het verdient aanbeveling gebruik constructors die **MediaServicesCredentials** als parameter.</span><span class="sxs-lookup"><span data-stu-id="f216f-122">It is recommended to use constructors that take **MediaServicesCredentials** as a parameter.</span></span> <span data-ttu-id="f216f-123">Zie voor meer informatie de **hergebruiken Access Control Service Tokens** die volgt.</span><span class="sxs-lookup"><span data-stu-id="f216f-123">For more information, see the **Reusing Access Control Service Tokens** that follows.</span></span> 

<span data-ttu-id="f216f-124">Het volgende voorbeeld wordt de openbare CloudMediaContext(MediaServicesCredentials credentials)-constructor:</span><span class="sxs-lookup"><span data-stu-id="f216f-124">The following example uses the public CloudMediaContext(MediaServicesCredentials credentials) constructor:</span></span>

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a><span data-ttu-id="f216f-125">Access Control Service Tokens hergebruiken</span><span class="sxs-lookup"><span data-stu-id="f216f-125">Reusing Access Control Service Tokens</span></span>
<span data-ttu-id="f216f-126">Deze sectie wordt beschreven hoe Access Control Service tokens gebruiken met behulp van CloudMediaContext-constructors die MediaServicesCredentials als parameter.</span><span class="sxs-lookup"><span data-stu-id="f216f-126">This section shows how to reuse Access Control Service tokens by using CloudMediaContext constructors that take MediaServicesCredentials as a parameter.</span></span>

<span data-ttu-id="f216f-127">[Azure Active Directory-toegangsbeheer](https://msdn.microsoft.com/library/hh147631.aspx) (ook wel bekend als Access Control Service of ACS) is een cloudservice waarmee u een eenvoudige manier voor verificatie en autoriseren van gebruikers toegang te krijgen tot hun webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="f216f-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (also known as Access Control Service or ACS) is a cloud-based service that provides an easy way of authenticating and authorizing users to gain access to their web applications.</span></span> <span data-ttu-id="f216f-128">Microsoft Azure Media Services controleert de toegang tot de services al OAuth-protocol dat een ACS-token is vereist.</span><span class="sxs-lookup"><span data-stu-id="f216f-128">Microsoft Azure Media Services controls access to its services though OAuth protocol that requires an ACS token.</span></span> <span data-ttu-id="f216f-129">Media Services ontvangt de ACS-tokens van een server voor autorisatie.</span><span class="sxs-lookup"><span data-stu-id="f216f-129">Media Services receives the ACS tokens from an authorization server.</span></span>

<span data-ttu-id="f216f-130">Bij het ontwikkelen met de Media Services SDK, kunt u niet omgaan met de tokens omdat de SDK code managers ze voor u.</span><span class="sxs-lookup"><span data-stu-id="f216f-130">When developing with the Media Services SDK, you can choose to not deal with the tokens because the SDK code managers them for you.</span></span> <span data-ttu-id="f216f-131">Echter, zodat de SDK volledig beheer van de ACS-tokens leidt tot onnodige aanvragen voor beveiligingstokens.</span><span class="sxs-lookup"><span data-stu-id="f216f-131">However, letting the SDK fully manage the ACS tokens leads to unnecessary token requests.</span></span> <span data-ttu-id="f216f-132">Aanvragen van tokens kost tijd en de client en server resources verbruikt.</span><span class="sxs-lookup"><span data-stu-id="f216f-132">Requesting tokens takes time and consumes the client and server resources.</span></span> <span data-ttu-id="f216f-133">De ACS-server ook beperkt de aanvragen als de frequentie te hoog is.</span><span class="sxs-lookup"><span data-stu-id="f216f-133">Also, the ACS server throttles the requests if the rate is too high.</span></span> <span data-ttu-id="f216f-134">De limiet is 30 aanvragen per seconde, Zie [ACS-Service beperkingen](https://msdn.microsoft.com/library/gg185909.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f216f-134">The limit is 30 requests per second, see [ACS Service Limitations](https://msdn.microsoft.com/library/gg185909.aspx) for more details.</span></span>

<span data-ttu-id="f216f-135">U kunt de ACS-tokens vanaf de Media Services SDK versie 3.0.0.0-prestatiemeters kunt hergebruiken.</span><span class="sxs-lookup"><span data-stu-id="f216f-135">Starting with the Media Services SDK version 3.0.0.0, you can reuse the ACS tokens.</span></span> <span data-ttu-id="f216f-136">De **CloudMediaContext** constructors die **MediaServicesCredentials** als een parameter Schakel het delen van de ACS-tokens tussen verschillende contexten.</span><span class="sxs-lookup"><span data-stu-id="f216f-136">The **CloudMediaContext** constructors that take **MediaServicesCredentials** as a parameter enable sharing the ACS tokens between multiple contexts.</span></span> <span data-ttu-id="f216f-137">De klasse MediaServicesCredentials kapselt de Media Services-referenties.</span><span class="sxs-lookup"><span data-stu-id="f216f-137">The MediaServicesCredentials class encapsulates the Media Services credentials.</span></span> <span data-ttu-id="f216f-138">Als u een ACS-token beschikbaar is en de verlooptijd bekend is, kunt u een nieuw exemplaar van de MediaServicesCredentials maken met het token en doorgegeven aan de constructor van CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="f216f-138">If an ACS token is available and its expiration time is known, you can create a new MediaServicesCredentials instance with the token and pass it to the constructor of CloudMediaContext.</span></span> <span data-ttu-id="f216f-139">Houd er rekening mee dat de Media Services SDK tokens automatisch vernieuwd wanneer ze zijn verlopen.</span><span class="sxs-lookup"><span data-stu-id="f216f-139">Note that the Media Services SDK automatically refreshes tokens whenever they expire.</span></span> <span data-ttu-id="f216f-140">Er zijn twee manieren om ACS-tokens, opnieuw te gebruiken zoals wordt weergegeven in de volgende voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="f216f-140">There are two ways to reuse ACS tokens, as shown in the examples below.</span></span>

* <span data-ttu-id="f216f-141">U kunt cache de **MediaServicesCredentials** object in het geheugen (bijvoorbeeld in een variabele van statische klasse).</span><span class="sxs-lookup"><span data-stu-id="f216f-141">You can cache the **MediaServicesCredentials** object in memory (for example, in a static class variable).</span></span> <span data-ttu-id="f216f-142">Vervolgens moet het object in de cache worden doorgegeven aan de constructor CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="f216f-142">Then, pass the cached object to the CloudMediaContext constructor.</span></span> <span data-ttu-id="f216f-143">Het object MediaServicesCredentials bevat een ACS-token die opnieuw kan worden gebruikt als het nog geldig is.</span><span class="sxs-lookup"><span data-stu-id="f216f-143">The MediaServicesCredentials object contains an ACS token that can be reused if it is still valid.</span></span> <span data-ttu-id="f216f-144">Als het token niet geldig is, wordt deze vernieuwd door de Media Services SDK met de referenties die aan de constructor MediaServicesCredentials gegeven.</span><span class="sxs-lookup"><span data-stu-id="f216f-144">If the token is not valid, it will be refreshed by the Media Services SDK using the credentials given to the MediaServicesCredentials constructor.</span></span>
  
    <span data-ttu-id="f216f-145">Houd er rekening mee dat de **MediaServicesCredentials** object een geldig token opgehaald nadat de RefreshToken is aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f216f-145">Note that the **MediaServicesCredentials** object gets a valid token after the RefreshToken is called.</span></span> <span data-ttu-id="f216f-146">De **CloudMediaContext** aanroepen de **RefreshToken** methode in de constructor.</span><span class="sxs-lookup"><span data-stu-id="f216f-146">The **CloudMediaContext** calls the **RefreshToken** method in the constructor.</span></span> <span data-ttu-id="f216f-147">Als u van plan bent de token waarden opslaan naar een externe opslag, moet u om te controleren of de waarde TokenExpiration geldig is voordat u de token gegevens opslaat.</span><span class="sxs-lookup"><span data-stu-id="f216f-147">If you are planning to save the token values to an external storage, make sure to check whether the TokenExpiration value is valid before saving the token data.</span></span> <span data-ttu-id="f216f-148">Het is geen geldige, belt RefreshToken voordat het in cache opslaan.</span><span class="sxs-lookup"><span data-stu-id="f216f-148">If it is not valid, call RefreshToken before caching.</span></span>
  
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use the cached credentials to create a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* <span data-ttu-id="f216f-149">U kunt ook de AccessToken tekenreeks en de waarden TokenExpiration cache.</span><span class="sxs-lookup"><span data-stu-id="f216f-149">You can also cache the AccessToken string and the TokenExpiration values.</span></span> <span data-ttu-id="f216f-150">De waarden kunnen later worden gebruikt voor het maken van een nieuw MediaServicesCredentials-object met gegevens in de cache-token.</span><span class="sxs-lookup"><span data-stu-id="f216f-150">The values could later be used to create a new MediaServicesCredentials object with the cached token data.</span></span>  <span data-ttu-id="f216f-151">Dit is vooral nuttig voor scenario's waar het token kan veilig worden gedeeld tussen meerdere processen en computers.</span><span class="sxs-lookup"><span data-stu-id="f216f-151">This is especially useful for scenarios where the token can be securely shared among multiple processes or computers.</span></span>
  
    <span data-ttu-id="f216f-152">De volgende codefragmenten de SaveTokenDataToExternalStorage GetTokenDataFromExternalStorage en UpdateTokenDataInExternalStorageIfNeeded methoden aanroepen die niet zijn gedefinieerd in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f216f-152">The following code snippets call the SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage, and UpdateTokenDataInExternalStorageIfNeeded methods that are not defined in this example.</span></span> <span data-ttu-id="f216f-153">U kunt deze methoden voor het opslaan, ophalen en token gegevens bijwerken in een externe opslag definiëren.</span><span class="sxs-lookup"><span data-stu-id="f216f-153">You could define these methods to store, retrieve, and update token data in an external storage.</span></span> 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from the context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // The SaveTokenDataToExternalStorage method should check 
        // whether the TokenExpiration value is valid before saving the token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    <span data-ttu-id="f216f-154">Gebruik de opgeslagen waarden voor de token MediaServicesCredentials maken.</span><span class="sxs-lookup"><span data-stu-id="f216f-154">Use the saved token values to create MediaServicesCredentials.</span></span>

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

    <span data-ttu-id="f216f-155">Het token exemplaar bijwerken als het token is bijgewerkt door de Media Services SDK.</span><span class="sxs-lookup"><span data-stu-id="f216f-155">Update the token copy in case the token was updated by the Media Services SDK.</span></span> 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* <span data-ttu-id="f216f-156">Als u meerdere accounts voor Media Services (bijvoorbeeld voor belastingverdeling doeleinden of Geo-distributie) hebt u MediaServicesCredentials objecten met behulp van de verzameling System.Collections.Concurrent.ConcurrentDictionary (de ConcurrentDictionary in cache collectie bevat een thread-veilige van sleutel-waardeparen die toegankelijk zijn voor meerdere threads tegelijk).</span><span class="sxs-lookup"><span data-stu-id="f216f-156">If you have multiple Media Services accounts (for example, for load sharing purposes or Geo-distribution) you can cache MediaServicesCredentials objects using the System.Collections.Concurrent.ConcurrentDictionary collection (the ConcurrentDictionary collection represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently).</span></span> <span data-ttu-id="f216f-157">Vervolgens gebruikt u de methode GetOrAdd ophalen van referenties in de cache.</span><span class="sxs-lookup"><span data-stu-id="f216f-157">You can then use the GetOrAdd method to get the cached credentials.</span></span> 
  
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

## <a name="connecting-to-a-media-services-account-located-in-the-north-china-region"></a><span data-ttu-id="f216f-158">Verbinding maken met een Media Services-account zich in de regio Noord, China</span><span class="sxs-lookup"><span data-stu-id="f216f-158">Connecting to a Media Services account located in the North China region</span></span>
<span data-ttu-id="f216f-159">Als uw account in de regio Noord, China bevindt zich, gebruikt u de volgende constructor:</span><span class="sxs-lookup"><span data-stu-id="f216f-159">If your account is located in the North China region, use the following constructor:</span></span>

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

<span data-ttu-id="f216f-160">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f216f-160">For example:</span></span>

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a><span data-ttu-id="f216f-161">Verbindingswaarden in de configuratie opslaan</span><span class="sxs-lookup"><span data-stu-id="f216f-161">Storing Connection Values in Configuration</span></span>
<span data-ttu-id="f216f-162">Het is een sterk aanbevolen procedure voor het opslaan van verbindingswaarden, zoals uw accountnaam en wachtwoord, met name gevoelige waarden in de configuratie.</span><span class="sxs-lookup"><span data-stu-id="f216f-162">It is a highly recommended practice to store connection values, especially sensitive values such as your account name and password, in configuration.</span></span> <span data-ttu-id="f216f-163">Het is ook een aanbevolen procedure voor het versleutelen van gevoelige configuratiegegevens.</span><span class="sxs-lookup"><span data-stu-id="f216f-163">Also, it is a recommended practice to encrypt sensitive configuration data.</span></span> <span data-ttu-id="f216f-164">U kunt het hele configuratiebestand versleutelen met behulp van Windows Encrypting File System (EFS).</span><span class="sxs-lookup"><span data-stu-id="f216f-164">You can encrypt the entire configuration file by using the Windows Encrypting File System (EFS).</span></span> <span data-ttu-id="f216f-165">Zodat EFS op een bestand met de rechtermuisknop op het bestand, selecteer **eigenschappen**, en schakel versleuteling in de **Geavanceerd** tabblad instellingen.</span><span class="sxs-lookup"><span data-stu-id="f216f-165">To enable EFS on a file, right-click the file, select **Properties**, and enable encryption in the **Advanced** settings tab.</span></span> <span data-ttu-id="f216f-166">Of u een aangepaste oplossing voor het versleutelen van de geselecteerde gedeelten van een configuratiebestand met behulp van beveiligde configuratie kunt maken.</span><span class="sxs-lookup"><span data-stu-id="f216f-166">Or you can create a custom solution for encrypting selected portions of a configuration file by using protected configuration.</span></span> <span data-ttu-id="f216f-167">Zie [versleutelen met behulp van beveiligde configuratie configuratiegegevens](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span><span class="sxs-lookup"><span data-stu-id="f216f-167">See [Encrypting Configuration Information Using Protected Configuration](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span></span>

<span data-ttu-id="f216f-168">Het volgende App.config-bestand bevat de waarden van de vereiste.</span><span class="sxs-lookup"><span data-stu-id="f216f-168">The following App.config file contains the required connection values.</span></span> <span data-ttu-id="f216f-169">De waarden in de <appSettings> element zijn de vereiste waarden die u hebt verkregen van het installatieproces van de Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="f216f-169">The values in the <appSettings> element are the required values that you got from the Media Services account setup process.</span></span>

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


<span data-ttu-id="f216f-170">Voor het ophalen van verbindingswaarden van configuratie, kunt u de **ConfigurationManager** klasse en vervolgens de waarden toewijzen aan velden in uw code:</span><span class="sxs-lookup"><span data-stu-id="f216f-170">To retrieve connection values from configuration, you can use the **ConfigurationManager** class and then assign the values to fields in your code:</span></span>

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a><span data-ttu-id="f216f-171">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="f216f-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f216f-172">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="f216f-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

