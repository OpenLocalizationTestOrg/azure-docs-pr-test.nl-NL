---
title: aaaEnterprise klasse WordPress in Azure | Microsoft Docs
description: Meer informatie over hoe toohost een bedrijfsniveau WordPress-site op Azure App Service
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 22d68588-2511-4600-8527-c518fede8978
ms.service: app-service-web
ms.devlang: php
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 4347eddb31d622d1189dc5db4d81b0f3745d6e69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-class-wordpress-on-azure"></a>Bedrijfsniveau WordPress in Azure
Azure App Service biedt een omgeving schaalbare, veilige en eenvoudig te gebruiken voor essentiële en grootschalige [WordPress] [ wordpress] sites. Microsoft zelf wordt uitgevoerd bedrijfsniveau sites zoals Hallo [Office] [ officeblog] en [Bing] [ bingblog] blogs. Dit artikel ziet u hoe toouse Hallo van de functie Web Apps van Microsoft Azure App Service-tooestablish en onderhouden van een enterprise-klasse, cloud-gebaseerde WordPress-site die een groot aantal bezoekers kan verwerken.

## <a name="architecture-and-planning"></a>Architectuur en planning
Een basisinstallatie van WordPress heeft slechts twee vereisten:

* **MySQL-Database**: deze vereiste is beschikbaar via [ClearDB in hello Azure Marketplace][cdbnstore]. Als alternatief kunt u uw eigen MySQL-installatie op Azure Virtual Machines kunt beheren met behulp van [Windows] [ mysqlwindows] of [Linux][mysqllinux].

  > [!NOTE]
  > ClearDB biedt diverse MySQL-configuraties. Elke configuratie heeft verschillende prestatiekenmerken. Zie Hallo [Azure Store] [ cdbnstore] voor meer informatie over de offerings die worden geleverd via hello Azure Store of rechtstreeks weergegeven op Hallo [ClearDB website](http://www.cleardb.com/pricing.view).
  >
  >
* **PHP 5.2.4 of hoger**: Azure App Service biedt momenteel [versie van PHP 5.4, 5.5 en 5.6][phpwebsite].

  > [!NOTE]
  > Het is raadzaam dat u altijd uitvoeren Hallo meest recente versie van PHP zodat u de meest recente beveiligingsupdates Hallo hebt.
  >
  >

### <a name="basic-deployment"></a>Eenvoudige implementatie
Als u alleen het basisvereisten Hallo gebruikt, kunt u een basisoplossing binnen een Azure-regio.

![Een Azure-web-app en MySQL-Database gehost in één Azure-regio][basic-diagram]

Hoewel zo u meerdere exemplaren van de Web-Apps van Hallo site tooscale out van uw toepassing maken kunt, wordt alles gehost binnen Hallo datacenters op een specifieke geografische regio. Trage responstijden bij gebruik van een site Hallo mogelijk ziet u bezoekers buiten deze regio. Als Hallo datacentra in deze regio falen beide, dat geldt ook voor uw toepassing.

### <a name="multi-region-deployment"></a>Implementatie van meerdere landen/regio
Met behulp van Azure [Traffic Manager][trafficmanager], kunt u de schaal van uw WordPress-site voor meerdere geografische regio's en bieden dezelfde URL voor alle bezoekers Hallo. Alle bezoekers komen via het Traffic Manager en worden vervolgens gerouteerde tooa regio die gebaseerd op Hallo taakverdeling configuratie.

![Een Azure-web-app, gehost in meerdere regio's met hoge beschikbaarheid CDBR router tooroute tooMySQL tussen regio 's][multi-region-diagram]

Binnen elke regio Hallo WordPress-site zou nog steeds worden geschaald over meerdere exemplaren van de Web-Apps, maar deze schaling specifieke tooa regio is. Intensief verkeer regio's en regio's weinig verkeer kunnen anders worden uitgebreid.

tooreplicate en route verkeer toomultiple MySQL-databases, kunt u [ClearDB hoge beschikbaarheid-routers (CDBRs)] [ cleardbscale] (links weergegeven) of [MySQL Cluster Carrier hoogwaardige Edition (CGE)] [cge].

### <a name="multi-region-deployment-with-media-storage-and-caching"></a>Meerdere landen/regio-implementatie met de Mediaopslag en opslaan in cache
Als Hallo site uploads of mediabestanden van hosts accepteert, gebruikt u Azure Blob-opslag. Als u nodig hebt in cache opslaan, kunt u overwegen [Redis-cache][rediscache], [Memcache Cloud](http://azure.microsoft.com/gallery/store/garantiadata/memcached/), [MemCachier](http://azure.microsoft.com/gallery/store/memcachier/memcachier/), of een van andere cachebewerkingen aanbiedingen voor Hallo Hallo [Azure Store](http://azure.microsoft.com/gallery/store/).

![Een Azure-web-app, gehost in meerdere regio's met hoge beschikbaarheid CDBR router voor MySQL met beheerde-Cache, Blob-opslag en Content Delivery Network][performance-diagram]

BLOB-opslag is geografisch verspreide tussen regio's standaard zodat er geen tooworry over het repliceren van bestanden op alle sites. U kunt ook inschakelen hello Azure [Content Delivery Network] [ cdn] voor Blob storage, die bestanden tooend knooppunten die dichter tooyour bezoekers distribueert.

### <a name="planning"></a>Planning
#### <a name="additional-requirements"></a>Aanvullende vereisten
| toodo dit... | Gebruikt u... |
| --- | --- |
| **Uploaden of opslaan van grote bestanden** |[WordPress-invoegtoepassing voor het gebruik van Blob-opslag][storageplugin] |
| **E-mail verzenden** |[SendGrid] [ storesendgrid] en Hallo [WordPress-invoegtoepassing voor het gebruik van SendGrid][sendgridplugin] |
| **Aangepaste domeinnamen** |[Een aangepaste domeinnaam configureren in Azure App Service][customdomain] |
| **HTTPS** |[HTTPS inschakelen voor een web-app in Azure App Service][httpscustomdomain] |
| **Validatie van vóór productie** |[Faseringsomgevingen voor web-apps in Azure App Service instellen][staging] <p>Wanneer u een web-app van de staging-tooproduction verplaatst, gaat u ook Hallo WordPress-configuratie. Zorg ervoor dat alle instellingen bijgewerkt toohello vereisten voor uw productie-app zijn voordat u Hallo gefaseerde app tooproduction verplaatst.</p> |
| **Bewaking en probleemoplossing** |[Logboekregistratie van diagnostische gegevens van web-apps in Azure App Service] [ log] en [Web-Apps bewaken in Azure App Service][monitor] |
| **Uw site implementeren** |[Een web-app in Azure App Service implementeren][deploy] |

#### <a name="availability-and-disaster-recovery"></a>Beschikbaarheid en herstel na noodgevallen
| toodo dit... | Gebruikt u... |
| --- | --- |
| **Laden van saldo sites** of **geo-sites distribueren** |[Verkeer leiden met Azure Traffic Manager][trafficmanager] |
| **Back-ups maken en bestanden terugzetten** |[Maak een back-up van een web-app in Azure App Service] [ backup] en [herstellen van een web-app in Azure App Service][restore] |

#### <a name="performance"></a>Prestaties
Prestaties in de cloud Hallo wordt hoofdzakelijk door opslaan in cache en scale-out bereikt. Hallo-geheugen, bandbreedte en andere kenmerken van het hosten van Web-Apps moeten echter wel beschouwd als.

| toodo dit... | Gebruikt u... |
| --- | --- |
| **De mogelijkheden van App Service-exemplaar begrijpen** |[Prijsinformatie, met inbegrip van de mogelijkheden van App Service-lagen][websitepricing] |
| **Cache-resources** |[Redis-cache][rediscache], [Memcache Cloud](/gallery/store/garantiadata/memcached/), [MemCachier](/gallery/store/memcachier/memcachier/), of een van andere cachebewerkingen aanbiedingen voor Hallo Hallo [Azure Store](/gallery/store/) |
| **Uw toepassing schalen** |[Een web-app schalen in Azure App Service] [ websitescale] en [ClearDB hoge beschikbaarheid routering][cleardbscale]. Als u toohost kiest en uw eigen MySQL-installatie beheren, kunt u overwegen [MySQL-Cluster CGE] [ cge] voor scale-out. |

#### <a name="migration"></a>Migratie
Er zijn twee methoden toomigrate van een bestaande tooAzure WordPress-site-App Service:

* **[WordPress exporteren][export]**: deze methode exporteert Hallo inhoud van uw blog. U kunt vervolgens Hallo inhoud tooa nieuwe WordPress-site op Azure App Service importeren met behulp van Hallo [importfunctie van WordPress-invoegtoepassing][import].

  > [!NOTE]
  > Tijdens dit proces u uw inhoud migreert kunt, worden deze alle invoegtoepassingen, thema's of andere aanpassingen niet gemigreerd. Deze onderdelen moet u handmatig opnieuw installeren.
  >
  >
* **Handmatige migratie**: [Back-up van uw site] [ wordpressbackup] en [database][wordpressdbbackup], en deze vervolgens handmatig opnieuw tooa web-app in Azure App Service en de bijbehorende MySQL-database. Deze methode is handig toomigrate maximaal aangepast sites omdat Hallo verspillen handmatig installeren van invoegtoepassingen, thema's en andere aanpassingen wordt voorkomen.

## <a name="step-by-step-instructions"></a>Stapsgewijze instructies
### <a name="create-a-wordpress-site"></a>Een WordPress-site maken
1. Gebruik Hallo [Azure Marketplace] [ cdbnstore] toocreate een MySQL-database van Hallo-grootte die u hebt geïdentificeerd in Hallo [architectuur en planning](#planning) sectie Hallo regio of regio's Wanneer u uw site host.
2. Volg de stappen Hallo in [een WordPress-web-app maken in Azure App Service] [ createwordpress] toocreate een WordPress-web-app. Wanneer u Hallo web-app maakt, selecteert u **gebruik een bestaande MySQL-Database**, en selecteer vervolgens Hallo-database die u in stap 1 hebt gemaakt.

Als u van een bestaande WordPress-site migreert, Zie [migreren van een bestaande WordPress-site tooAzure](#Migrate-an-existing-WordPress-site-to-Azure) nadat u een nieuwe web-app hebt gemaakt.

### <a name="migrate-an-existing-wordpress-site-tooazure"></a>Migreren van een bestaande tooAzure van de WordPress-site
Zoals vermeld in Hallo [architectuur en planning](#planning) sectie, zijn er twee manieren toomigrate een WordPress-site:

* **Gebruik exporteren en importeren** voor sites die niet veel aanpassingen hebben of alleen waar u toomove Hallo inhoud.
* **Gebruik back-up en herstel** voor sites met veel aanpassing waar u toomove alles.

Gebruik een van de volgende secties toomigrate Hallo uw site.

#### <a name="hello-export-and-import-method"></a>Hallo exporteren en importeren van methode
1. Gebruik [WordPress exporteren] [ export] tooexport uw bestaande site.
2. Een web-app maken met behulp van Hallo stappen in Hallo [een WordPress-site maken](#Create-a-new-WordPress-site) sectie.
3. Meld u aan tooyour WordPress-site op Hallo [Azure-portal][mgmtportal], en klik vervolgens op **Plugins** > **nieuwe toevoegen**. Zoek en installeer Hallo **WordPress importfunctie** invoegtoepassing.
4. Nadat u Hallo importfunctie van WordPress-invoegtoepassing hebt geïnstalleerd, klikt u op **extra** > **importeren**, en klik vervolgens op **WordPress** toouse Hallo importfunctie van WordPress-invoegtoepassing.
5. Op Hallo **importeren WordPress** pagina, klikt u op **bestand kiezen**. Hallo WXR bestand dat is geëxporteerd vanuit uw bestaande WordPress-site vinden en klik vervolgens op **uploadbestand en importeer**.
6. Klik op **indienen**. U wordt gevraagd dat Hallo importeren geslaagd is.
7. Nadat u al deze stappen hebt voltooid, start opnieuw op uw site uit de **App Services** blade in Hallo [Azure-portal][mgmtportal].

Nadat u Hallo site geïmporteerd, moet u mogelijk tooperform Hallo stappen tooenable instellingen die niet in het importbestand hello te volgen.

| Als u dit... | Dit doen... |
| --- | --- |
| **Permalinks** |Hallo WordPress-dashboard van de nieuwe site hello, klik op **instellingen** > **Permalinks**, en werk vervolgens Hallo Permalinks structuur. |
| **afbeelding/media koppelingen** |tooupdate koppelingen toohello nieuwe locatie, gebruikt u Hallo [Velvet blauwe bijwerken URL's invoegtoepassing][velvet], een zoeken en vervangen hulpprogramma of Hallo koppelingen in de database handmatig bijwerken. |
| **Thema 's** |Ga te**vormgeving** > **thema**, en werk vervolgens Hallo Websitethema indien nodig. |
| **Menu 's** |Als het thema menu's ondersteunt, kan koppelingen tooyour startpagina Hallo oude submap ingesloten in ze nog steeds. Ga te**vormgeving** > **menu's**, en werk deze bij. |

#### <a name="hello-backup-and-restore-method"></a>Hallo back-up en herstel van methode
1. Maak een back-up van uw bestaande WordPress-site met behulp van informatie op Hallo [WordPress back-ups][wordpressbackup].
2. Maak een back-up van uw bestaande database met behulp van informatie op Hallo [back-ups van uw database][wordpressdbbackup].
3. Een database maken en terugzetten van back-up Hallo.

   1. Een nieuwe database vanuit Hallo kopen [Azure Marketplace][cdbnstore], of een MySQL-database instellen op een [Windows] [ mysqlwindows] of [Linux ] [ mysqllinux] virtuele machine.
   2. Gebruik een MySQL-client, zoals [MySQL Workbench] [ workbench] tooconnect toohello nieuwe database en uw WordPress-database importeren.
   3. Update Hallo database toochange Hallo domein vermeldingen tooyour nieuwe Azure App Service-domein, bijvoorbeeld mywordpress.azurewebsites.net. Gebruik Hallo [zoeken en vervangen voor WordPress Databases Script] [ searchandreplace] toosafely Wijzig alle exemplaren.
4. Een web-app maken in hello Azure-portal en publiceren van Hallo WordPress back-up.

   1. een web-app met een database in Hallo toocreate [Azure-portal][mgmtportal], klikt u op **nieuw** > **Web en mobiel**  >  **Azure Marketplace** > **Web-Apps** > **webtoepassing + SQL** (of **webtoepassing + MySQL**) > **Maken**. Configureer alle vereiste Hallo instellingen toocreate een leeg web-app.
   2. Zoek in uw WordPress back-up, Hallo **wp-config.php** bestand en open het in een teksteditor. Vervang Hallo vermeldingen met Hallo-informatie voor uw nieuwe MySQL-database te volgen:

      * **DB_NAME**: gebruikersnaam Hallo van Hallo-database.
      * **DB_USER**: Hallo gebruiker naam die wordt gebruikt tooaccess Hallo database.
      * **DB_PASSWORD**: gebruikerswachtwoord Hallo.

        Nadat u deze items gewijzigd, opslaan en sluiten Hallo **wp-config.php** bestand.
   3. Gebruik Hallo [een web-app in Azure App Service implementeren] [ deploy] informatie tooenable Hallo implementatiemethode dat u toouse wilt en vervolgens uw WordPress-web-app voor back-tooyour in Azure App Service implementeren.
5. Nadat het Hallo WordPress-site is geïmplementeerd, moet u kunnen tooaccess Hallo nieuwe site (als een App Service-web-app) met behulp van Hallo *. azurewebsite.net-URL voor Hallo-site.

### <a name="configure-your-site"></a>Uw site configureren
Nadat Hallo WordPress-site is gemaakt of gemigreerd, gebruik Hallo informatie tooimprove prestaties na of aanvullende functionaliteit inschakelen.

| toodo dit... | Gebruikt u... |
| --- | --- |
| **App Service plan modus, grootte en schaal inschakelen instellen** |[Een web-app schalen in Azure App Service][websitescale]. |
| **Permanente databaseverbindingen inschakelen** |WordPress gebruikt standaard geen permanente databaseverbindingen, wat leiden uw verbinding toohello database toobecome beperkt na meerdere verbindingen tot kunnen. permanente verbindingen tooenable installeren Hallo [permanente verbindingen adapter invoegtoepassing](https://wordpress.org/plugins/persistent-database-connection-updater/installation/). |
| **De prestaties verbeteren** |<ul><li><p><a href="https://azure.microsoft.com/en-us/blog/disabling-arrs-instance-affinity-in-windows-azure-web-sites/">Hallo ARR cookie uitschakelen</a>, die de prestaties kan verbeteren wanneer WordPress wordt uitgevoerd op meerdere exemplaren van de Web-Apps.</p></li><li><p>Opslaan in cache inschakelt. U kunt <a href="http://msdn.microsoft.com/library/azure/dn690470.aspx">Redis-cache</a> (preview) Hello <a href="https://wordpress.org/plugins/redis-object-cache/">Redis-cache WordPress-invoegtoepassing voor object</a>, of kunt u een van de Hallo andere cachebewerkingen aanbiedingen van Hallo <a href="/gallery/store/">Azure Store</a>.</p></li><li><p>[Maken van WordPress sneller met Wincache](https://wordpress.org/plugins/w3-total-cache/). Wincache is standaard ingeschakeld voor web-apps. Wanneer u WinCache en dynamische Cache samen, uitschakelen van WinCache bestandscache, maar laat Hallo gebruiker en de sessiecache is ingeschakeld. tooturn uit de bestandscache in een bestand op systeemniveau .ini instellen Hallo volgende waarde:<br/><code>wincache.fcenabled = 0</code></p></li><li><p>[Een web-app schalen in Azure App Service] [ websitescale] en gebruik <a href="http://www.cleardb.com/developers/cdbr/introduction">ClearDB hoge beschikbaarheid routering</a> of <a href="http://www.mysql.com/products/cluster/">MySQL-Cluster CGE</a>.</p></li></ul> |
| **Blobs gebruikt voor de opslag** |<ol><li><p>[Een Azure storage-account maken](../storage/common/storage-create-storage-account.md).</p></li><li><p>Meer informatie over hoe te[gebruik Hallo Content distributie Network](../cdn/cdn-create-new-endpoint.md) toogeo-gegevens die zijn opgeslagen in blobs distribueren.</p></li><li><p>Installeer en configureer Hallo <a href="https://wordpress.org/plugins/windows-azure-storage/">Azure Storage voor WordPress-invoegtoepassing</a>.</p><p>Zie voor gedetailleerde informatie over installatie en configuratie voor Hallo-invoegtoepassing, Hallo <a href="http://plugins.svn.wordpress.org/windows-azure-storage/trunk/UserGuide.docx">gebruikershandleiding</a>.</p> </li></ol> |
| **E-mail inschakelen** |Schakel <a href="https://azure.microsoft.com/en-us/marketplace/partners/sendgrid/sendgrid-azure/">SendGrid</a> met behulp van hello Azure Store. Hallo installeren <a href="http://wordpress.org/plugins/sendgrid-email-delivery-simplified">SendGrid-invoegtoepassing</a> voor WordPress. |
| **Een aangepaste domeinnaam configureren** |[Een aangepaste domeinnaam configureren in Azure App Service][customdomain]. |
| **HTTPS inschakelen voor een aangepaste domeinnaam** |[HTTPS inschakelen voor een web-app in Azure App Service][httpscustomdomain]. |
| **Laden van saldo of geo-distribueren van uw site** |[Met Azure Traffic Manager-verkeer routeren][trafficmanager]. Als u een aangepast domein gebruikt, raadpleegt u [een aangepaste domeinnaam configureren in Azure App Service] [ customdomain] voor informatie over het toouse Traffic Manager met aangepaste domeinnamen. |
| **Automatische back-ups inschakelen** |[Maak een back-up van een web-app in Azure App Service][backup]. |
| **Diagnostische logboekregistratie inschakelen** |[Logboekregistratie van diagnostische gegevens van web-apps in Azure App Service][log]. |

## <a name="next-steps"></a>Volgende stappen
* [WordPress-optimalisatie](http://codex.wordpress.org/WordPress_Optimization)
* [Converteren van WordPress toomultisite in Azure App Service](web-sites-php-convert-wordpress-multisite.md)
* [ClearDB wizard voor Azure bijwerken](http://www.cleardb.com/store/azure/upgrade)
* [Hosting WordPress in een submap van uw web-app in Azure App Service](http://blogs.msdn.com/b/webapps/archive/2013/02/13/hosting-wordpress-in-a-subfolder-of-your-windows-azure-web-site.aspx)
* [Stap voor stap: Een WordPress-site met behulp van Azure maken](http://blogs.technet.com/b/blainbar/archive/2013/08/07/article-create-a-wordpress-site-using-windows-azure-read-on.aspx)
* [Host uw bestaande WordPress-blog op Azure](http://blogs.msdn.com/b/msgulfcommunity/archive/2013/08/26/migrating-a-self-hosted-wordpress-blog-to-windows-azure.aspx)
* [Permalinks in WordPress inschakelen](http://www.iis.net/learn/extensions/url-rewrite-module/enabling-pretty-permalinks-in-wordpress)
* [Hoe toomigrate en voer uw WordPress-blog op Azure App Service](http://www.kefalidis.me/2012/06/how-to-migrate-and-run-your-wordpress-blog-on-windows-azure-websites/)
* [Hoe toorun WordPress in Azure App Service voor gratis](http://architects.dzone.com/articles/how-run-wordpress-azure)
* [WordPress in Azure binnen twee minuten of minder](http://www.sitepoint.com/wordpress-windows-azure-2-minutes-less/)
* [Het verplaatsen van een WordPress-blog tooAzure - deel 1: een WordPress-blog op Azure maken](http://www.davebost.com/2013/07/10/moving-a-wordpress-blog-to-windows-azure-part-1)
* [Het verplaatsen van een WordPress-blog tooAzure - deel 2: uw Inhoudsoverdracht](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-transferring-your-content)
* [Het verplaatsen van een WordPress-blog tooAzure - deel 3: uw aangepaste domein instellen](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-3-setting-up-your-custom-domain)
* [Het verplaatsen van een WordPress-blog tooAzure - deel 4: permalinks en regels voor het herschrijven van URL's](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-4-pretty-permalinks-and-url-rewrite-rules)
* [Het verplaatsen van een WordPress-blog tooAzure - onderdeel 5: verplaatsen van een submap toohello-basis](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-5-moving-from-a-subfolder-to-the-root)
* [Hoe tooset van een WordPress web-app in uw Azure-account](http://www.itexperience.net/2014/01/20/how-to-set-up-a-wordpress-website-in-your-windows-azure-account/)
* [Propping van WordPress in Azure](http://www.johnpapa.net/wordpress-on-azure/)
* [Tips voor WordPress in Azure](http://www.johnpapa.net/azurecleardbmysql/)

> [!NOTE]
> Als u wilt dat tooget gestart met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard vereist en er bent nergens toe verplicht.
>
>

## <a name="whats-changed"></a>Wat is er gewijzigd
Zie voor een wijziging van de toohello handleiding van websites tooApp Service [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).

<!-- URL List -->

[performance-diagram]: ./media/web-sites-php-enterprise-wordpress/performance-diagram.png
[basic-diagram]: ./media/web-sites-php-enterprise-wordpress/basic-diagram.png
[multi-region-diagram]: ./media/web-sites-php-enterprise-wordpress/multi-region-diagram.png
[wordpress]: http://www.microsoft.com/web/wordpress
[officeblog]: http://blogs.office.com/
[bingblog]: http://blogs.bing.com/
[cdbnstore]: http://www.cleardb.com/store/azure
[storageplugin]: https://wordpress.org/plugins/windows-azure-storage/
[sendgridplugin]: http://wordpress.org/plugins/sendgrid-email-delivery-simplified/
[phpwebsite]: web-sites-php-configure.md
[customdomain]: app-service-web-tutorial-custom-domain.md
[trafficmanager]: ../traffic-manager/traffic-manager-overview.md
[backup]: web-sites-backup.md
[restore]: web-sites-restore.md
[rediscache]: https://azure.microsoft.com/documentation/services/redis-cache/
[managedcache]: http://msdn.microsoft.com/library/azure/dn386122.aspx
[websitescale]: web-sites-scale.md
[managedcachescale]: http://msdn.microsoft.com/library/azure/dn386113.aspx
[cleardbscale]: http://www.cleardb.com/developers/cdbr/introduction
[staging]: web-sites-staged-publishing.md
[monitor]: web-sites-monitor.md
[log]: web-sites-enable-diagnostic-log.md
[httpscustomdomain]: app-service-web-tutorial-custom-ssl.md
[mysqlwindows]:../virtual-machines/windows/classic/mysql-2008r2.md
[mysqllinux]:../virtual-machines/linux/classic/mysql-on-opensuse.md
[cge]: http://www.mysql.com/products/cluster/
[websitepricing]: /pricing/details/app-service/
[export]: http://en.support.wordpress.com/export/
[import]: http://wordpress.org/plugins/wordpress-importer/
[wordpressbackup]: http://wordpress.org/plugins/wordpress-importer/
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[createwordpress]: web-sites-php-web-site-gallery.md
[velvet]: https://wordpress.org/plugins/velvet-blues-update-urls/
[mgmtportal]: https://portal.azure.com/
[wordpressbackup]: http://codex.wordpress.org/WordPress_Backups
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[workbench]: http://www.mysql.com/products/workbench/
[searchandreplace]: http://interconnectit.com/124/search-and-replace-for-wordpress-databases/
[deploy]: web-sites-deploy.md
[posh]: /powershell/azureps-cmdlets-docs
[Azure CLI]:../cli-install-nodejs.md
[storesendgrid]: https://azure.microsoft.com/marketplace/partners/sendgrid/sendgrid-azure/
[cdn]: ../cdn/cdn-overview.md
