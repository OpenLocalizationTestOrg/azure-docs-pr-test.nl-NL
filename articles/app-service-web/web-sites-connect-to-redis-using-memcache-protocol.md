---
title: een App Service web app tooRedis via Hallo Memcache-protocol - Azure aaaConnect | Microsoft Docs
description: Verbinding maken met een web-app in Azure App service tooRedis Cache met Hallo Memcache-protocol
services: app-service\web
documentationcenter: php
author: SyntaxC4
manager: erikre
editor: riande
ms.assetid: 0fcdf9fa-2995-4839-ba4d-cfa389c4ba06
ms.service: app-service-web
ms.devlang: php
ms.topic: get-started-article
ms.tgt_pltfrm: windows
ms.workload: na
ms.date: 02/29/2016
ms.author: cfowler
ms.openlocfilehash: 48036d60fbbced59eb1e37584f507fffffff753d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# Verbinding maken met een web-app in Azure App Service tooRedis Cache via Hallo Memcache-protocol
In dit artikel leert u hoe een WordPress tooconnect web-app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) te[Azure Redis-Cache] [ 12] met Hallo [Memcache] [ 13] protocol. Als u een bestaande web-app die een Memcached-server voor caching in het geheugen gebruikt hebt, kunt u het migreren tooAzure App Service en gebruik Hallo eigen cache-oplossing in Microsoft Azure met weinig of geen wijziging tooyour toepassingscode. Bovendien kunt u uw bestaande Memcache-expertise toocreate uiterst schaalbare, gedistribueerde apps in Azure App Service met Azure Redis-Cache voor caching in het geheugen tijdens het gebruik van populaire toepassingsframeworks zoals .NET, PHP, Node.js, Java en Python.  

App Service Web Apps kan in dit toepassingsscenario Hallo Web Apps Memcache-shim, dit een lokale Memcache-server die als een Memcache-proxy is fungeert voor het opslaan van aanroepen tooAzure Redis-Cache. Hierdoor kunnen alle Apps die communiceert met behulp van Hallo Memcache-protocol toocache gegevens met Redis-Cache. Deze Memcache-shim werkt op protocolniveau hello, zodat deze kan worden gebruikt door een toepassing of toepassingsframework, zolang deze communiceert via Hallo Memcache-protocol.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## Vereisten
Hallo Web Memcache-shim Apps kan worden gebruikt met elke toepassing, mits deze communiceert via Hallo Memcache-protocol. Toepassing hello is voor dit voorbeeld wordt een schaalbare WordPress-site die kan worden ingericht vanuit Azure Marketplace Hallo.

Hallo stappen die worden beschreven in deze artikelen:

* [Een exemplaar van hello Azure Redis Cache Service inrichten][0]
* [Een schaalbare WordPress-site implementeren in Azure][1]

U zult gereed tooproceed bij het inschakelen van Hallo Memcache-shim in Azure App Service Web Apps zodra u hebt schaalbare WordPress-site Hallo geïmplementeerd en een Redis-Cache-exemplaar dat is ingericht.

## Hallo Web Apps Memcache-shim inschakelen
In de volgorde tooconfigure Memcache-shim, moet u drie app-instellingen maken. U kunt dit doen met een aantal methoden, waaronder Hallo [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), Hallo [klassieke portal][3], Hallo [Azure PowerShell-Cmdlets] [ 5] of Hallo [Azure-opdrachtregelinterface][5]. Voor Hallo kader van dit artikel, ga ik toouse hello [Azure Portal] [ 4] tooset Hallo app-instellingen. Hallo volgende waarden kunnen worden opgehaald uit **instellingen** blade van uw Redis-Cache-exemplaar.

![Blade Instellingen van Azure Redis Cache](./media/web-sites-connect-to-redis-using-memcache-protocol/1-azure-redis-cache-settings.png)

### App-instelling REDIS_HOST toevoegen
eerste app-instelling die u moet Hallo toocreate is Hallo **REDIS\_HOST** app-instelling. Deze instelling geeft Hallo bestemming toowhich Hallo shim forwards Hallo cache-informatie. waarde voor app-instelling REDIS_HOST Hallo kan worden opgehaald uit Hallo Hallo **eigenschappen** blade van uw Redis-Cache-exemplaar.

![Hostnaam van Azure Redis Cache](./media/web-sites-connect-to-redis-using-memcache-protocol/2-azure-redis-cache-hostname.png)

Set Hallo sleutel van het Hallo app instellen te**REDIS\_HOST** en Hallo-waarde van Hallo app instelling toohello **hostnaam** van Hallo Redis-Cache-exemplaar.

![App-instelling REDIS_HOST van web-app](./media/web-sites-connect-to-redis-using-memcache-protocol/3-azure-website-appsettings-redis-host.png)

### App-instelling REDIS_KEY toevoegen
tweede app-instelling die u moet Hallo toocreate is Hallo **REDIS\_sleutel** app-instelling. Deze instelling biedt Hallo verificatie token vereiste toosecurely toegang Hallo Redis-Cache-exemplaar. U kunt ophalen Hallo waarde vereist voor Hallo app-instelling REDIS_KEY hello **toegangssleutels** blade van Hallo Redis-Cache-exemplaar.

![Primaire sleutel voor Azure Redis Cache](./media/web-sites-connect-to-redis-using-memcache-protocol/4-azure-redis-cache-primarykey.png)

Set Hallo sleutel van het Hallo app instellen te**REDIS\_sleutel** en Hallo-waarde van Hallo app instelling toohello **primaire sleutel** van Hallo Redis-Cache-exemplaar.

![App-instelling REDIS_KEY van Azure-website](./media/web-sites-connect-to-redis-using-memcache-protocol/5-azure-website-appsettings-redis-primarykey.png)

### App-instelling MEMCACHESHIM_REDIS_ENABLE toevoegen
Hallo laatste app-instelling is gebruikte tooenable hello Memcache-Shim in Web-Apps, die gebruikmaakt Hallo hierbij worden REDIS_HOST en REDIS_KEY tooconnect toohello Azure Redis-Cache en voorwaarts Hallo cache aanroepen. Set Hallo sleutel van het Hallo app instellen te**MEMCACHESHIM\_REDIS\_inschakelen** en de waarde te Hallo**true**.

![App-instelling MEMCACHESHIM_REDIS_ENABLE van web-app](./media/web-sites-connect-to-redis-using-memcache-protocol/6-azure-website-appsettings-enable-shim.png)

Wanneer u klaar bent met het toe te voegen Hallo drie (3) app-instellingen, klikt u op **opslaan**.

## Memcache-extensie voor PHP inschakelen
In de volgorde voor Hallo toepassing toospeak hello Memcache-protocol is het nodig tooinstall hello Memcache-extensie tooPHP--Hallo taalframework voor uw WordPress-site.

### Hallo extensie php_memcache downloaden
Te bladeren[PECL][6]. Hallo categorie caching, klik op [memcache][7]. Klik onder de kolom met downloads Hallo Hallo DDL-koppeling.

![PECL-website van PHP](./media/web-sites-connect-to-redis-using-memcache-protocol/7-php-pecl-website.png)

Hallo Non-Thread Safe (NTS) x86 downloadkoppeling voor Hallo-versie van PHP ingeschakeld in de Web-Apps. (De standaardversie is PHP 5.4.)

![Memcache-pakket voor PHP PECL](./media/web-sites-connect-to-redis-using-memcache-protocol/8-php-pecl-memcache-package.png)

### De extensie php_memcache Hallo inschakelen
Nadat u Hallo-bestand hebt gedownload, uitpakken en upload Hallo **php\_memcache.dll** in Hallo **d:\\thuis\\site\\wwwroot\\bin\\ext\\**  directory. Nadat het Hallo php_memcache.dll is geüpload naar Hallo web-app, moet u tooenable Hallo extensie toohello PHP-Runtime. tooenable hello Memcache-extensie in de Azure-Portal openen Hallo Hallo **toepassingsinstellingen** blade voor web-app Hallo, voegt u een nieuwe appinstelling met sleutel op Hallo **PHP\_EXTENSIES** en Hallo waarde **bin\\ext\\php_memcache.dll**.

> [!NOTE]
> Als de web-app Hallo tooload meerdere PHP-uitbreidingen moet, moet Hallo-waarde van PHP_EXTENSIONS een door komma's gescheiden lijst van relatieve paden tooDLL bestanden.
> 
> 

![App-instelling PHP_EXTENSIONS van web-app](./media/web-sites-connect-to-redis-using-memcache-protocol/9-azure-website-appsettings-php-extensions.png)

Wanneer u klaar bent, klikt u op **Opslaan**.

## WordPress-invoegtoepassing voor Memcache installeren
> [!NOTE]
> U kunt ook downloaden Hallo [invoegtoepassing Memcached Object Cache](https://wordpress.org/plugins/memcached/) via WordPress.org.
> 
> 

Klik op de pagina met WordPress invoegtoepassingen hello, **nieuwe toevoegen**.

![Pagina met WordPress-invoegtoepassingen](./media/web-sites-connect-to-redis-using-memcache-protocol/10-wordpress-plugin.png)

Typ in het zoekvak Hallo **memcached** en druk op **Enter**.

![Nieuwe WordPress-invoegtoepassing toevoegen](./media/web-sites-connect-to-redis-using-memcache-protocol/11-wordpress-add-new-plugin.png)

Zoeken naar **Memcached Object Cache** in Hallo-lijst, klik vervolgens op **nu installeren**.

![WordPress invoegtoepassing voor Memcache installeren](./media/web-sites-connect-to-redis-using-memcache-protocol/12-wordpress-install-memcache-plugin.png)

### Hallo Memcache WordPress-invoegtoepassing inschakelen
> [!NOTE]
> Volg de instructies Hallo in deze blog op [hoe een Site-uitbreiding in Web Apps tooenable] [ 8] tooinstall Visual Studio Team Services.
> 
> 

In Hallo `wp-config.php` bestand, het toevoegen van Hallo bovenstaande Hallo stop editing Opmerking bijna Hallo bestandseindemarkering Hallo code te volgen.

```php
$memcached_servers = array(
    'default' => array('localhost:' . getenv("MEMCACHESHIM_PORT"))
);
```

Zodra deze code is geplakt, wordt Hallo document automatisch in monaco opgeslagen.

de volgende stap Hallo is tooenable Hallo object-cache-invoegtoepassing. Dit wordt gedaan door slepen en neerzetten **object-cache.php** van **wp-inhoud/plugins/memcached** map toohello **wp-content** map tooenable Hallo Memcache Object Cache-functionaliteit.

![Hallo-invoegtoepassing voor memcache object-cache.php zoeken](./media/web-sites-connect-to-redis-using-memcache-protocol/13-locate-memcache-object-cache-plugin.png)

Nu dat Hallo **object-cache.php** bestand bevindt zich in Hallo **wp-content** map Hallo Memcached Object Cache is nu ingeschakeld.

![Hallo-invoegtoepassing voor memcache object-cache.php inschakelen](./media/web-sites-connect-to-redis-using-memcache-protocol/14-enable-memcache-object-cache-plugin.png)

## Controleer of Hallo Memcache Object Cache-invoegtoepassing werkt
Alle Hallo stappen tooenable Hallo Web Apps Memcache-shim zijn nu voltooid. Hallo hoeft alleen nog is tooverify Hallo gegevens invullen van uw Redis-Cache-exemplaar.

### Hallo niet-SSL-poort-ondersteuning inschakelen in Azure Redis-Cache
> [!NOTE]
> Hallo Redis CLI biedt geen ondersteuning voor SSL-verbindingen op Hallo moment van publicatie van dit artikel, dus hello volgende stappen zijn vereist.
> 
> 

Blader in hello Azure Portal, toohello Redis-Cache-exemplaar dat u hebt gemaakt voor deze web-app. Nadat de blade Hallo-cache geopend is, klikt u op Hallo **instellingen** pictogram.

![Knop Instellingen van Azure Redis Cache](./media/web-sites-connect-to-redis-using-memcache-protocol/15-azure-redis-cache-settings-button.png)

Selecteer **toegangspoorten** uit Hallo-lijst.

![Toegangspoort voor Azure Redis Cache](./media/web-sites-connect-to-redis-using-memcache-protocol/16-azure-redis-cache-access-port.png)

Klik op **Nee** voor **Alleen toegang met SSL-beveiliging toestaan**.

![Alleen toegang met SSL-beveiliging voor Azure Redis Cache](./media/web-sites-connect-to-redis-using-memcache-protocol/17-azure-redis-cache-access-port-ssl-only.png)

U ziet dat Hallo niet-SSL-poort nu is ingesteld. Klik op **Opslaan**.

![Toegangspoort zonder SSL voor Azure Redis Cache](./media/web-sites-connect-to-redis-using-memcache-protocol/18-azure-redis-cache-access-port-non-ssl.png)

### Verbinding maken met tooAzure Redis-Cache vanuit redis cli
> [!NOTE]
> Bij deze stap wordt ervan uitgegaan dat Redis lokaal is geïnstalleerd op uw ontwikkelcomputer. [Installeer Redis lokaal via deze instructies][9].
> 
> 

Open uw opdrachtregelconsole keuze en type Hallo volgende opdracht:

```shell
redis-cli –h <hostname-for-redis-cache> –a <primary-key-for-redis-cache> –p 6379
```

Vervang Hallo  **&lt;hostnaam voor redis cache&gt;**  met werkelijke Hallo van xxxxx.redis.cache.Windows.NET en Hallo  **&lt;primaire-sleutel-voor-redis-cache&gt;**  met Hallo-toegangssleutel voor Hallo-cache, drukt u vervolgens op **Enter**. Zodra hello CLI is verbonden toohello Redis-Cache-exemplaar, geeft u alle redis-opdracht. In Hallo onderstaande schermafbeelding heb ik ervoor gekozen toolist Hallo sleutels.

![Verbinding maken met tooAzure Redis-Cache vanuit Redis CLI in Terminal](./media/web-sites-connect-to-redis-using-memcache-protocol/19-redis-cli-terminal.png)

Hallo aanroep toolist Hallo sleutels moeten een waarde retourneren. Zo niet, probeer navigeren toohello web-app en probeer het opnieuw.

## Conclusie
Gefeliciteerd. Hallo WordPress-app heeft nu een gecentraliseerde geheugencache tooaid doorvoer te verbeteren. Onthouden, Hallo Memcache-Shim van Web Apps kan worden gebruikt met elke Memcache-client, ongeacht het programmeren van framework taal of toepassing. tooprovide feedback of tooask vragen over Hallo Web Apps Memcache-shim, te posten[MSDN-Forums] [ 10] of [Stackoverflow][11].

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

[0]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache
[1]: http://bit.ly/1t0KxBQ
[2]: http://manage.windowsazure.com
[3]: http://portal.azure.com
[4]: /powershell/azureps-cmdlets-docs
[5]: /downloads
[6]: http://pecl.php.net
[7]: http://pecl.php.net/package/memcache
[8]: http://blog.syntaxc4.net/post/2015/02/05/how-to-enable-a-site-extension-in-azure-websites.aspx
[9]: http://redis.io/download#installation
[10]: https://social.msdn.microsoft.com/Forums/home?forum=windowsazurewebsitespreview
[11]: http://stackoverflow.com/questions/tagged/azure-web-sites
[12]: /services/cache/
[13]: http://memcached.org
