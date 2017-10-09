.NET-toepassingen kunnen gebruikmaken van Hallo **StackExchange.Redis** cacheclient, die kan worden geconfigureerd in Visual Studio met een NuGet-pakket dat Hallo configuratie van de cacheclienttoepassingen eenvoudiger maakt. 

> [!NOTE]
> Zie voor meer informatie, Hallo [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github pagina en Hallo [documentatie over de cacheclient StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis#documentation).
> 
> 

een clienttoepassing in Visual Studio met Hallo NuGet-pakket StackExchange.Redis, tooconfigure met de rechtermuisknop op Hallo-project in **Solution Explorer** en kies **NuGet-pakketten beheren**. 

![Manage NuGet Packages](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

Type **StackExchange.Redis** of **StackExchange.Redis.StrongName** in Hallo zoekvak, selecteer de gewenste versie Hallo in Hallo resultaten en klikt u op **installeren**.

> [!NOTE]
> Als u liever een versie met sterke naam Hallo toouse **StackExchange.Redis** -clientbibliotheek kiezen **StackExchange.Redis.StrongName**; Kies anders **StackExchange.Redis**.
> 
> 

![NuGet-pakket StackExchange.Redis](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

assembly-verwijzingen Hallo NuGet-pakket downloadt en voegt Hallo vereist voor uw client-toepassing tooaccess Azure Redis-Cache met Hallo StackExchange.Redis cacheclient.

> [!NOTE]
> Als u uw project toouse StackExchange.Redis eerder hebt geconfigureerd, kunt u controleren op updates toohello pakket van Hallo **NuGet Package Manager**. toocheck voor- en installatie bijgewerkt versies van Hallo NuGet-pakket StackExchange.Redis, klikt u op **Updates** in Hallo Hallo **NuGet Package Manager** venster. Als een update toohello NuGet-pakket StackExchange.Redis beschikbaar is, kunt u uw project toouse Hallo bijgewerkt versie bijwerken.
> 
> 

U kunt ook Hallo NuGet-pakket StackExchange.Redis installeren door te klikken op **NuGet Package Manager**, **Package Manager Console** van Hallo **extra** menu en actieve Hallo de volgende opdracht uit Hallo **Package Manager Console** venster.
    
```
Install-Package StackExchange.Redis
```
