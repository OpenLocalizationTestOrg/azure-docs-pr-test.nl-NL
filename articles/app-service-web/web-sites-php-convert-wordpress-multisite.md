---
title: aaaConvert WordPress tooMultisite in Azure App Service
description: Meer informatie over hoe tootake een bestaande WordPress-web-app via Hallo-galerie in Azure is gemaakt en converteert u deze tooWordPress implementatie voor meerdere locaties
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 1153f0a8043de875f081704cd0a124776758878c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-wordpress-toomultisite-in-azure-app-service"></a>Converteren van WordPress tooMultisite in Azure App Service
## <a name="overview"></a>Overzicht
*Door [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*

In deze zelfstudie leert u hoe tootake een bestaande WordPress-web-app gemaakt door de galerie Hallo in Azure en omzetten in een implementatie voor meerdere locaties WordPress installeren. Bovendien leert u hoe tooassign een aangepast domein tooeach Hallo subsites in de installatie.

Ervan wordt uitgegaan dat u een bestaande installatie van WordPress hebt. Als u dit niet doet, volgt u Hallo richtlijn voor formaatbepaling in [een WordPress-website uit de galerie Hallo in Azure maken][website-from-gallery].

Converteren van een bestaande WordPress tooMultisite van één site-installatie wordt doorgaans redelijk eenvoudig en veel van Hallo eerste stappen die hier afkomstig zijn direct van Hallo [maken van een netwerk] [ wordpress-codex-create-a-network] pagina op Hallo [WordPress Codex](http://codex.wordpress.org).

Aan de slag.

## <a name="allow-multisite"></a>Implementatie voor meerdere locaties toestaan
U moet eerst tooenable implementatie voor meerdere locaties via Hallo `wp-config.php` bestand Hello **WP\_toestaan\_implementatie voor meerdere locaties** constante. Er zijn twee methoden tooedit uw web-app-bestanden: Hallo wordt eerst via de FTP- en Hallo tweede via Git. Als u niet bekend met het bent toosetup van deze methoden Raadpleeg toohello volgende zelfstudies:

* [PHP-website met de MySQL- en FTP-][website-w-mysql-and-ftp-ftp-setup]
* [PHP-website met de MySQL en Git][website-w-mysql-and-git-git-setup]

Open Hallo `wp-config.php` -bestand met de Hallo-editor van uw keuze en voeg de volgende Hallo hierboven Hallo `/* That's all, stop editing! Happy blogging. */` regel.

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

Of toosave Hallo het bestand zijn en upload het vorige toohello server!

## <a name="network-setup"></a>Netwerk instellen
Meld u bij toohello *wp-beheerder* ruimte van uw web-app en u ziet een nieuw item onder Hallo **hulpprogramma's** menu aangeroepen **netwerk instellen**. Klik op **netwerkinstellingen** en vul Hallo details van uw netwerk.

![Scherm voor het netwerk instellen][wordpress-network-setup]

Deze zelfstudie wordt gebruikgemaakt van Hallo *submappen* schema site omdat deze altijd werkt en we om de aangepaste domeinen van de bovenliggende verderop in de zelfstudie Hallo instellen. Deze moet echter mogelijk toosetup een subdomein installeren als u een domein via Hallo toewijst [Azure Portal](https://portal.azure.com) en jokerteken DNS correct setup.

Submap instellingen Zie voor meer informatie over het subdomein tegenover Hallo [soorten multisiteconfiguratie] [ wordpress-codex-types-of-networks] artikel op Hallo WordPress Codex.

## <a name="enable-hello-network"></a>Hallo netwerk inschakelen
Hallo-netwerk is nu geconfigureerd in de database hello, maar er is een resterende stap tooenable Hallo netwerkfunctionaliteit. Hallo voltooien `wp-config.php` instellingen en zorg ervoor dat `web.config` correct routeert elke site.

Wanneer u op Hallo **installeren** knop op Hallo *netwerkinstellingen* pagina WordPress probeert tooupdate hello `wp-config.php` en `web.config` bestanden. U moet echter altijd controleren Hallo bestanden tooensure Hallo updates met succes zijn uitgevoerd. Als dat niet het geval is, wordt dit scherm u Hallo vereiste updates worden aangeboden. Bewerk en Hallo bestanden op te slaan.

Na het maken wordt deze updates moet u toolog af en meld back in Hallo wp-beheerder dashboard.

Er worden nu een menu Extra op Hallo beheerder balk met het label **Mijn Sites**. Dit menu kunt u toocontrol uw nieuwe netwerk via Hallo **netwerk Admin** dashboard.

## <a name="adding-custom-domains"></a>Toevoegen van aangepaste domeinen
Hallo [WordPress MU domein toewijzing] [ wordpress-plugin-wordpress-mu-domain-mapping] invoegtoepassing kunt u een eenvoudig tooadd aangepaste domeinen tooany site in uw netwerk. Voor Hallo invoegtoepassing toooperate goed is, moet u toodo enkele aanvullende instellingen op Hallo Portal en bij uw domeinregistrar.

## <a name="enable-domain-mapping-toohello-web-app"></a>Domein toewijzing toohello web-app inschakelen
Hallo **vrije** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) plan modus biedt geen ondersteuning voor het toevoegen van aangepaste domeinen tooWeb Apps. U moet tooswitch te**gedeelde** of **standaard** modus. toodo dit:

* Meld u bij toohello Azure-Portal en zoek uw web-app. 
* Klik op Hallo **opschalen** tabblad **instellingen**.
* Onder **algemene**, selecteert u *gedeelde* of *STANDARD*
* Klik op **opslaan**

U kunt wordt een bericht weergegeven waarin u wordt gevraagd tooverify Hallo wijzigen en uw web-app kan nu een kosten, afhankelijk van het gebruik in rekening gebracht en andere configuratieset Hallo bevestigen.

Het duurt een paar seconden tooprocess Hallo nieuwe instellingen, is dit nu een goed moment toostart-instellen van uw domein.

## <a name="verify-your-domain"></a>Verifieer uw domein
Voordat u Azure Web Apps kunt u de site van een domein toohello toomap, moet u eerst tooverify Hallo autorisatie toomap Hallo-domein. toodo geval is, moet u een nieuwe CNAME-record tooyour DNS-vermelding toevoegen.

* Aanmelden van tooyour domein-DNS-beheer
* Maakt een nieuwe CNAME *awverify*
* Punt *awverify* te*awverify. YOUR_DOMAIN.azurewebsites.NET*

Het kan even duren om Hallo DNS-wijzigingen toogo volledige kracht, dus als Hallo stappen werken niet onmiddellijk, gaat u koffie, maken en vervolgens keert u terug en probeer het opnieuw.

## <a name="add-hello-domain-toohello-web-app"></a>Hallo domein toohello web-app toevoegen
Retour tooyour web-app via hello Azure-Portal klikt u op **instellingen**, en klik vervolgens op **aangepaste domeinen en SSL**.

Wanneer Hallo *SSL-instellingen* worden weergegeven, ziet u Hallo velden waar u invoer op alle Hallo-domeinen die u wenst dat tooassign tooyour web-app. Als een domein is hier niet worden vermeld, is het niet mogelijk voor de toewijzing binnen WordPress, ongeacht hoe Hallo domein-DNS ingesteld is.

![Dialoogvenster aangepaste domeinen beheren][wordpress-manage-domains]

Nadat u uw domein in het tekstvak hello te typen, controleert Azure Hallo CNAME-record die u eerder hebt gemaakt. Als Hallo DNS is niet volledig is doorgegeven, wordt een rode indicator wordt weergegeven. Als deze voltooid is, ziet u een groen vinkje. 

Let op Hallo die IP-adres onder Hallo van Hallo dialoogvenster weergegeven. U moet deze toosetup Hallo een record voor uw domein.

## <a name="setup-hello-domain-a-record"></a>Hallo domein A-record instellen
U kunt hello andere stappen is gelukt, nu Hallo domein tooyour Azure-web-app via een DNS A-record te toewijzen. 

Het is belangrijk toonote hier die Azure-web-apps worden geaccepteerd CNAME zowel A-records, maar u *moet* een toewijzing van een record tooenable juiste domein gebruiken. Worden een CNAME kan niet doorgestuurd tooanother CNAME, dit is wat Azure met YOUR_DOMAIN.azurewebsites.net voor u gemaakt.

Met de Hallo IP-adres van de vorige stap hello, retourneren tooyour DNS-beheer en setup Hallo een record toopoint toothat IP-adres.

## <a name="install-and-setup-hello-plugin"></a>Installeren en instellen Hallo-invoegtoepassing
Implementatie voor meerdere locaties WordPress nog momenteel geen gebruikmaakt van een ingebouwde methode toomap aangepaste domeinen. Er is echter een invoegtoepassing aangeroepen [WordPress MU domein toewijzing] [ wordpress-plugin-wordpress-mu-domain-mapping] waarmee Hallo functionaliteit toegevoegd voor u. Meld u bij toohello netwerk Admin deel van uw site en installeer Hallo **WordPress MU domein toewijzing** invoegtoepassing.

Nadat het installeren en activeren van de invoegtoepassing hello, gaat u naar **instellingen** > **domein toewijzing** tooconfigure Hallo-invoegtoepassing. In de eerste tekstvak hello, *IP-adres*, invoer Hallo IP-adres gebruikt van toosetup Hallo een record voor Hallo-domein. Stel een *Domeinopties* u wenst (Hallo zijn standaard vaak fijn) en klik op **opslaan**.

## <a name="map-hello-domain"></a>Hallo domein toewijzen
Ga naar Hallo **Dashboard** voor Hallo-site die u wenst toomap Hallo-domein. Klik op **extra** > **domein toewijzing** en type Hallo nieuw domein in Hallo tekstvak en klik op **toevoegen**.

Standaard wordt het nieuwe domein Hallo herschreven toohello automatisch gegenereerde site domein te zijn. Als u wilt dat toohave alle verkeer dat wordt verzonden toohello nieuw domein, controleert u Hallo *primair domein voor deze blog* vak voordat u opslaat. U kunt een onbeperkt aantal domeinen tooa site toevoegen, maar slechts één primaire kan zijn.

## <a name="do-it-again"></a>Opnieuw doen
Azure-Web-Apps kunt u tooadd een onbeperkt aantal domeinen tooa web-app. tooadd een ander domein, moet u tooexecute hello **Verifieer uw domein** en **Setup Hallo domein A-record** secties voor elk domein.    

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png


