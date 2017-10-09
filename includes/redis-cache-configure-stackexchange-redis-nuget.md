<span data-ttu-id="5e990-101">.NET-toepassingen kunnen gebruikmaken van Hallo **StackExchange.Redis** cacheclient, die kan worden geconfigureerd in Visual Studio met een NuGet-pakket dat Hallo configuratie van de cacheclienttoepassingen eenvoudiger maakt.</span><span class="sxs-lookup"><span data-stu-id="5e990-101">.NET applications can use hello **StackExchange.Redis** cache client, which can be configured in Visual Studio using a NuGet package that simplifies hello configuration of cache client applications.</span></span> 

> [!NOTE]
> <span data-ttu-id="5e990-102">Zie voor meer informatie, Hallo [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github pagina en Hallo [documentatie over de cacheclient StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis#documentation).</span><span class="sxs-lookup"><span data-stu-id="5e990-102">For more information, see hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github page and  hello [StackExchange.Redis cache client documentation](http://github.com/StackExchange/StackExchange.Redis#documentation).</span></span>
> 
> 

<span data-ttu-id="5e990-103">een clienttoepassing in Visual Studio met Hallo NuGet-pakket StackExchange.Redis, tooconfigure met de rechtermuisknop op Hallo-project in **Solution Explorer** en kies **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="5e990-103">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, right-click hello project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span> 

![Manage NuGet Packages](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

<span data-ttu-id="5e990-105">Type **StackExchange.Redis** of **StackExchange.Redis.StrongName** in Hallo zoekvak, selecteer de gewenste versie Hallo in Hallo resultaten en klikt u op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="5e990-105">Type **StackExchange.Redis** or **StackExchange.Redis.StrongName** into hello search text box, select hello desired version from hello results, and click **Install**.</span></span>

> [!NOTE]
> <span data-ttu-id="5e990-106">Als u liever een versie met sterke naam Hallo toouse **StackExchange.Redis** -clientbibliotheek kiezen **StackExchange.Redis.StrongName**; Kies anders **StackExchange.Redis**.</span><span class="sxs-lookup"><span data-stu-id="5e990-106">If you prefer toouse a strong-named version of hello **StackExchange.Redis** client library, choose **StackExchange.Redis.StrongName**; otherwise choose **StackExchange.Redis**.</span></span>
> 
> 

![NuGet-pakket StackExchange.Redis](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

<span data-ttu-id="5e990-108">assembly-verwijzingen Hallo NuGet-pakket downloadt en voegt Hallo vereist voor uw client-toepassing tooaccess Azure Redis-Cache met Hallo StackExchange.Redis cacheclient.</span><span class="sxs-lookup"><span data-stu-id="5e990-108">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span>

> [!NOTE]
> <span data-ttu-id="5e990-109">Als u uw project toouse StackExchange.Redis eerder hebt geconfigureerd, kunt u controleren op updates toohello pakket van Hallo **NuGet Package Manager**.</span><span class="sxs-lookup"><span data-stu-id="5e990-109">If you have previously configured your project toouse StackExchange.Redis, you can check for updates toohello package from hello **NuGet Package Manager**.</span></span> <span data-ttu-id="5e990-110">toocheck voor- en installatie bijgewerkt versies van Hallo NuGet-pakket StackExchange.Redis, klikt u op **Updates** in Hallo Hallo **NuGet Package Manager** venster.</span><span class="sxs-lookup"><span data-stu-id="5e990-110">toocheck for and install updated versions of hello StackExchange.Redis NuGet package, click **Updates** in hello hello **NuGet Package Manager** window.</span></span> <span data-ttu-id="5e990-111">Als een update toohello NuGet-pakket StackExchange.Redis beschikbaar is, kunt u uw project toouse Hallo bijgewerkt versie bijwerken.</span><span class="sxs-lookup"><span data-stu-id="5e990-111">If an update toohello StackExchange.Redis NuGet package is available, you can update your project toouse hello updated version.</span></span>
> 
> 

<span data-ttu-id="5e990-112">U kunt ook Hallo NuGet-pakket StackExchange.Redis installeren door te klikken op **NuGet Package Manager**, **Package Manager Console** van Hallo **extra** menu en actieve Hallo de volgende opdracht uit Hallo **Package Manager Console** venster.</span><span class="sxs-lookup"><span data-stu-id="5e990-112">You can also install hello StackExchange.Redis NuGet package by clicking **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu, and running hello following command from hello **Package Manager Console** window.</span></span>
    
```
Install-Package StackExchange.Redis
```
