---
title: aaaCache ASP.NET Session State-Provider | Microsoft Docs
description: Meer informatie over hoe toostore ASP.NET Session State met behulp van Azure Redis-Cache
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 192f384c-836a-479a-bb65-8c3e6d6522bb
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/01/2017
ms.author: sdanie
ms.openlocfilehash: 9ea84cf67b9314b15dce696f596d399921194510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-session-state-provider-for-azure-redis-cache"></a>ASP.NET-sessiestatusprovider voor Azure Redis-Cache
Azure Redis-Cache biedt een sessiestatus-provider gebruiken toostore uw sessiestatus in een cache in plaats van in het geheugen of in een SQL Server-database. toouse Hallo cachebewerkingen sessiestatus-provider, moet u uw cache eerst configureren en configureer vervolgens uw ASP.NET-toepassing voor cache met Hallo Redis-Cache sessie status NuGet-pakket.

Is het vaak niet handig zijn in een echte cloud app tooavoid een vorm van de status op te slaan voor een gebruikerssessie, maar sommige benaderingen invloed op prestaties en schaalbaarheid meer dan andere. Als er toostore staat, wordt de beste oplossing Hallo is tookeep Hallo hoeveelheid status klein en sla het in cookies. Als dat niet mogelijk is, is de volgende aanbevolen oplossing Hallo toouse ASP.NET-sessiestatus met een provider voor gedistribueerde, in het geheugen-cache. Hallo slechtste oplossing uit oogpunt van prestaties en schaalbaarheid is toouse een database back-sessiestatus-provider. In dit onderwerp bevat richtlijnen over het gebruik van Hallo ASP.NET Session State-Provider voor Azure Redis-Cache. Zie voor informatie over andere opties van de status sessie [opties voor ASP.NET-sessiestatus](#aspnet-session-state-options).

## <a name="store-aspnet-session-state-in-hello-cache"></a>ASP.NET-sessiestatus opslaan in cache van de Hallo
tooconfigure een clienttoepassing in Visual Studio met Hallo Redis-Cache sessie status NuGet-pakket, klikt u op **NuGet Package Manager**, **Package Manager Console** van Hallo **extra** menu.

Voer hello na de opdracht van Hallo `Package Manager Console` venster.
    
```
Install-Package Microsoft.Web.RedisSessionStateProvider
```

> [!IMPORTANT]
> Als u Hallo functie van de premium-laag Hallo clustering gebruikt, moet u [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 of hoger, of een uitzondering gegenereerd. Too2.0.1 verplaatsen of hoger is een belangrijke wijziging; Zie voor meer informatie [v2.0.0 Details van de wijziging op te splitsen](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details). Hallo huidige versie van dit pakket is momenteel Hallo van deze update artikel, 2.2.3.
> 
> 

Hallo Redis sessie status Provider NuGet-pakket heeft een afhankelijkheid op Hallo StackExchange.Redis.StrongName pakket. Als Hallo StackExchange.Redis.StrongName pakket niet aanwezig in uw project is, wordt deze geïnstalleerd.

>[!NOTE]
>In aanvulling toohello sterke naam StackExchange.Redis.StrongName pakket is er ook Hallo StackExchange.Redis niet-sterke naam versie. Als uw project Hallo niet-sterke naam StackExchange.Redis versie dat moet u deze verwijderen, ophalen anders u naamconflicten in uw project. Zie voor meer informatie over deze pakketten [cacheclients configureren .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Hallo NuGet-pakket downloadt en voegt Hallo vereiste assembly verwijst naar Hallo volgende sectie in het web.config-bestand wordt toegevoegd. Deze sectie bevat de vereiste configuratie Hallo voor uw ASP.NET-toepassing toouse hello Redis-Cache sessiestatus-Provider.

```xml
<sessionState mode="Custom" customProvider="MySessionStateStore">
    <providers>
    <!--
    <add name="MySessionStateStore"
           host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        throwOnError = "true" [true|false]
        retryTimeoutInMilliseconds = "0" [number]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
    />
    -->
    <add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
</sessionState>
```

Hallo toegelicht sectie bevat een voorbeeld van het Hallo-kenmerken en voorbeelden van instellingen voor elk kenmerk.

Hallo-kenmerken configureren met waarden uit de cacheblade van uw in Microsoft Azure-portal Hallo Hallo en configureer andere waarden naar wens Hallo. Zie voor instructies over de toegang tot de eigenschappen van uw cache [configureren Redis-cache-instellingen](cache-configure.md#configure-redis-cache-settings).

* **host** – Geef uw cache-eindpunt.
* **poort** – uw niet-SSL-poort of uw SSL-poort, afhankelijk van het ssl-instellingen hello gebruiken.
* **accessKey** – beide Hallo primaire of secundaire sleutel gebruiken voor uw cache.
* **SSL** : true als u wilt dat toosecure cache/clientcommunicatie met ssl; anders ONWAAR. Ervoor toospecify Hallo de juiste poort zijn.
  * Hallo niet-SSL-poort is standaard uitgeschakeld voor nieuwe caches. Geef op waar om deze instelling toouse Hallo SSL-poort. Zie voor meer informatie over het inschakelen van niet-SSL-poort Hallo Hallo [toegangspoorten](cache-configure.md#access-ports) sectie in Hallo [een cache configureren](cache-configure.md) onderwerp.
* **throwOnError** : true als u wilt dat de toobe van een uitzondering gegenereerd als er een fout of ONWAAR als u wilt dat Hallo bewerking toofail achtergrond. U kunt controleren wegens een fout door Hallo statische Microsoft.Web.Redis.RedisSessionStateProvider.LastException eigenschap te controleren. Hallo standaardwaarde is true.
* **retryTimeoutInMilliseconds** – bewerkingen die mislukken worden opnieuw uitgevoerd tijdens dit interval, in milliseconden opgegeven. Hallo eerste poging plaatsvindt na 20 milliseconden en vervolgens nieuwe pogingen uitgevoerd voor elke seconde totdat Hallo retryTimeoutInMilliseconds interval is verstreken. Hallo-bewerking is één van de laatste keer opnieuw geprobeerd onmiddellijk na dit interval. Als Hallo bewerking steeds mislukt, Hallo uitzondering terug toohello beller, afhankelijk van Hallo throwOnError instelling. Hallo-standaardwaarde is 0, wat betekent er geen nieuwe pogingen dat.
* **databaseId** – geeft aan welke database toouse voor cache uitvoergegevens. Als niet wordt opgegeven, wordt de standaardwaarde Hallo van 0 gebruikt.
* **applicationName** – sleutels worden opgeslagen in redis als `{<Application Name>_<Session ID>}_Data`. Deze schematische kan meerdere toepassingen tooshare Hallo hetzelfde Redis-exemplaar. Deze parameter is optioneel en als u niet beschikken over een standaardwaarde wordt gebruikt.
* **connectionTimeoutInMilliseconds** – deze instelling kunt u toooverride hello connectTimeout instellen in de client StackExchange.Redis Hallo. Als niet wordt opgegeven, wordt de Hallo standaardinstelling connectTimeout van 5000 gebruikt. Zie voor meer informatie [configuratiemodel StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** – deze instelling kunt u toooverride hello syncTimeout instellen in de client StackExchange.Redis Hallo. Als niet wordt opgegeven, wordt Hallo standaardinstelling syncTimeout 1000 gebruikt. Zie voor meer informatie [configuratiemodel StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).

Zie voor meer informatie over deze eigenschappen Hallo oorspronkelijke blogberichtaankondiging op [aankondigen van ASP.NET Session State-Provider voor Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx).

Vergeet niet toocomment uit Hallo standaard InProc sessie state-provider-sectie in het web.config-bestand.

```xml
<!-- <sessionState mode="InProc"
     customProvider="DefaultSessionProvider">
     <providers>
        <add name="DefaultSessionProvider"
              type="System.Web.Providers.DefaultSessionStateProvider,
                    System.Web.Providers, Version=1.0.0.0, Culture=neutral,
                    PublicKeyToken=31bf3856ad364e35"
              connectionStringName="DefaultConnection" />
      </providers>
</sessionState> -->
```

Zodra deze stappen worden uitgevoerd, is uw toepassing hello geconfigureerde toouse Redis-Cache sessiestatus-Provider. Wanneer u sessiestatus in uw toepassing gebruikt, wordt deze opgeslagen in een Azure Redis-Cache-exemplaar.

> [!IMPORTANT]
> Gegevens die zijn opgeslagen in de cache Hallo moet serializable zijn, in tegenstelling tot Hallo-gegevens die kunnen worden opgeslagen in Hallo standaard ASP.NET Session State-Provider in het geheugen. Wanneer Hallo sessiestatus-Provider voor Redis wordt gebruikt, moet u dat Hallo gegevenstypen die worden opgeslagen in de sessiestatus serialiseerbaar zijn.
> 
> 

## <a name="aspnet-session-state-options"></a>Opties voor ASP.NET-sessiestatus
* In het geheugen Session State-Provider - slaat deze provider Hallo sessiestatus in het geheugen. Hallo voordeel van het gebruik van deze provider is en eenvoudig en snel. U kunt uw Web-Apps echter kan niet schalen als u in het geheugen provider omdat deze niet wordt gedistribueerd.
* SQL Server Session State-Provider - deze provider slaat Hallo sessiestatus in Sql Server. Gebruik deze provider als u wilt dat toostore Hallo sessiestatus in de permanente opslag. U kunt uw Web-App schalen maar invloed op de prestaties met Sql Server voor sessie heeft op uw Web-App.
* Gedistribueerd In geheugen sessiestatus-Provider zoals Redis-Cache sessiestatus-Provider - provider hebt u het beste van beide werelden Hallo. Uw Web-App kan een eenvoudige, snelle en schaalbare sessiestatus-Provider hebben. Omdat deze provider winkels Hallo sessiestatus in een Cache, uw app tootake in overweging heeft Hallo alle kenmerken die zijn gekoppeld bij het bespreken van tooa gedistribueerde In cachegeheugen, zoals tijdelijke netwerkfouten. Zie voor aanbevolen procedures voor het gebruik van Cache [opslaan in cache richtlijnen](../best-practices-caching.md) van Microsoft Patterns & procedures [Azure Cloud toepassingsontwerp en implementatie richtlijnen](https://github.com/mspnp/azure-guidance).

Zie voor meer informatie over de status van de sessie en andere aanbevelingen [aanbevolen procedures voor de ontwikkeling van Web (gebouw echte Cloud-Apps met Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices).

## <a name="next-steps"></a>Volgende stappen
Bekijk Hallo [ASP.NET-Cacheprovider voor Azure Redis-Cache](cache-aspnet-output-cache-provider.md).

