---
title: aaaHow toodebug een Node.js-web-app in Azure App Service
description: Meer informatie over hoe toodebug een Node.js web-app in Azure App Service.
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a>Hoe toodebug een Node.js web-app in Azure App Service
Azure biedt ingebouwde diagnostics tooassist met Node.js-toepassingen die worden gehost foutopsporing [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web-Apps. In dit artikel leert u hoe tooenable logboekregistratie van stdout en stderr, informatie over fout in de browser Hallo weergeven en hoe toodownload en weergave logboekbestanden.

Diagnostische gegevens voor Node.js-toepassingen die worden gehost op Azure wordt geleverd door [IISNode]. Hoewel dit artikel wordt beschreven Hallo veelgebruikte instellingen voor het verzamelen van diagnostische gegevens, biedt geen een volledig overzicht voor het werken met IISNode. Zie voor meer informatie over het werken met IISNode hello [IISNode Readme] op GitHub.

<a id="enablelogging"></a>

## <a name="enable-logging"></a>Logboekregistratie inschakelen
Standaard bevat een App Service-web-app alleen diagnostische gegevens over implementaties, zoals wanneer u een web-app met Git implementeert. Deze informatie is nuttig als u problemen tijdens de implementatie, zoals een fout ondervindt bij het installeren van een module waarnaar wordt verwezen in **package.json**, of als u een aangepaste implementatiescript gebruikt.

tooenable hello logboekregistratie van stdout en stderr stromen, moet u een **IISNode.yml** -bestand op basis van uw Node.js-toepassing hello en voeg de volgende Hallo:

    loggingEnabled: true

Hallo logboekregistratie van stderr en stdout van uw Node.js-toepassing is nu ingeschakeld.

Hallo **IISNode.yml** bestand kan ook worden gebruikt toocontrol of beschrijvende fouten of ontwikkelaars fouten worden toohello browser geretourneerd wanneer er een fout optreedt. tooenable developer-fouten, toevoegen Hallo volgende regel toohello **IISNode.yml** bestand:

    devErrorsEnabled: true

Zodra deze optie is ingeschakeld, wordt de IISNode Hallo laatste 64K van informatie die wordt verstuurd toostderr in plaats van een aangepaste fout, zoals 'Er is een interne serverfout opgetreden' geretourneerd.

> [!NOTE]
> DevErrorsEnabled is handig bij het oplossen van problemen tijdens de ontwikkeling, waardoor het in een productieomgeving mogelijk fouten tot gevolg ontwikkeling tooend gebruikers worden verzonden.
> 
> 

Als hello **IISNode.yml** bestand al bestaat niet in uw toepassing, moet u uw web-app opnieuw starten na het publiceren van de toepassing hello bijgewerkt. Als u instellingen in een bestaand gewoon wijzigt **IISNode.yml** bestand dat eerder is gepubliceerd, niet opnieuw opstarten is vereist.

> [!NOTE]
> Als uw web-app is gemaakt met hello Azure opdrachtregelprogramma's of Azure PowerShell-Cmdlets standaard **IISNode.yml** bestand wordt automatisch gemaakt.
> 
> 

toorestart hello web-app, selecteer Hallo web-app in Hallo [Azure Portal](https://portal.azure.com), en klik vervolgens op **opnieuw** knop:

![knop opnieuw opstarten][restart-button]

Als hello Azure opdrachtregelprogramma's zijn geïnstalleerd in uw ontwikkelomgeving, kunt u Hallo opdracht toorestart Hallo web-app te volgen:

    azure site restart [sitename]

> [!NOTE]
> Hoewel loggingEnabled en devErrorsEnabled Hallo meest gebruikte IISNode.yml configuratieopties zijn voor het vastleggen van diagnostische gegevens zijn IISNode.yml gebruikte tooconfigure tal van opties voor uw hostingomgeving. Zie voor een volledige lijst van de configuratieopties Hallo Hallo [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) bestand.
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a>Toegang tot logboeken
Logboeken met diagnostische gegevens kunnen worden geopend op drie manieren; Hallo FTP File Transfer Protocol (), downloadt een Zip-archief met of bijgewerkt als een live stream van Hallo logboek (ook wel bekend als een tail). Hallo Zip-archief van de logboekbestanden Hallo downloaden of de livestream Hallo weergeven vereisen hello Azure opdrachtregelprogramma's. Deze kunnen worden geïnstalleerd met behulp van de volgende opdracht Hallo:

    npm install azure-cli -g

Na de installatie configureert zijn Hallo-hulpprogramma's toegankelijk via 'azure' Hallo-opdracht. opdrachtregelprogramma's Hallo moet eerst worden geconfigureerde toouse uw Azure-abonnement. Zie voor informatie over hoe de tooaccomplish bij deze taak Hallo **hoe toodownload en importeer publicatie-instellingen** sectie Hallo [hoe tooUse hello Azure opdrachtregelprogramma's](../xplat-cli-connect.md) artikel.

### <a name="ftp"></a>FTP
Diagnostische gegevens over tooaccess Hallo via FTP, gaat u naar Hallo [Azure Portal](https://portal.azure.com), selecteer uw web-app en selecteer vervolgens Hallo **DASHBOARD**. In Hallo **snelle koppelingen** sectie hello **FTP-logboeken met diagnostische gegevens** en **FTPS diagnostische LOGBOEKEN** koppelingen bieden toegang toohello logboeken met Hallo FTP-protocol.

> [!NOTE]
> Als u niet eerder geconfigureerd gebruikersnaam en wachtwoord voor FTP- of implementatie, kunt u doen vanaf Hallo **Quick Start** pagina beheren door te selecteren **implementatiereferenties instellen**.
> 
> 

Hallo FTP-URL geretourneerd in Hallo dashboard is voor Hallo **logboekbestanden** directory waarin Hallo submappen te volgen:

* [Implementatiemethode](web-sites-deploy.md) -als u een implementatiemethode zoals Git, een directory van Hallo dezelfde naam wordt gemaakt en vindt u informatie toodeployments gerelateerd.
* nodejs - Stdout en stderr informatie vastgelegd van alle exemplaren van uw toepassing (wanneer loggingEnabled is ingesteld op true.)

### <a name="zip-archive"></a>Het ZIP-archief
toodownload een Zip-archief van diagnostische logboeken hello, gebruik Hallo volgende opdracht uit hello Azure opdrachtregelprogramma's:

    azure site log download [sitename]

Dit wordt gedownload een **diagnostics.zip** in de huidige map Hallo. Dit archief bevat Hallo directory-structuur te volgen:

* implementaties - een logboek van informatie over implementaties van uw toepassing
* Logboekbestanden
  
  * [Implementatiemethode](web-sites-deploy.md) -als u een implementatiemethode zoals Git, een directory van Hallo dezelfde naam wordt gemaakt en vindt u informatie toodeployments gerelateerd.
  * nodejs - Stdout en stderr informatie vastgelegd van alle exemplaren van uw toepassing (wanneer loggingEnabled is ingesteld op true.)

### <a name="live-stream-tail"></a>Live stream (tail)
tooview een live stream van diagnostische logboekgegevens, gebruik Hallo volgende opdracht uit hello Azure opdrachtregelprogramma's:

    azure site log tail [sitename]

Hiermee herstelt u een reeks gebeurtenissen die worden bijgewerkt wanneer deze zich op Hallo-server voordoen. Deze stroom retourneren informatie over de implementatie, evenals stdout en stderr informatie (wanneer loggingEnabled is ingesteld op true.)

<a id="nextsteps"></a>

## <a name="next-steps"></a>Volgende stappen
In dit artikel u leert hoe tooenable en toegang diagnostische gegevens voor Azure. Terwijl deze informatie is nuttig voor informatie over problemen die zich voordoen met uw toepassing, het tooa probleem met een module die u gebruikt of die versie Hallo van Node.js die wordt gebruikt door App Service Web Apps kan verwijzen is anders dan Hallo gebruikt in uw implementatie -omgeving.

Zie voor meer informatie in het werken met modules in Azure [Node.js-Modules gebruiken met Azure-toepassingen](../nodejs-use-node-modules-azure-apps.md).

Zie voor meer informatie over het opgeven van een Node.js-versie voor uw toepassing [een Node.js-versie opgeven in een Azure-toepassing].

Zie voor meer informatie, ook Hallo [Node.js Developer Center](/develop/nodejs/).

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[een Node.js-versie opgeven in een Azure-toepassing]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

