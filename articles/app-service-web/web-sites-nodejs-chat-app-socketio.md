---
title: aaaCreate een Node.js-chattoepassing met Socket.IO in Azure App Service
description: Een zelfstudie die u laat zien met socket.io in een node.js-web-app gehost op Azure.
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a>In Azure App Service een Node.js-chattoepassing maken met Socket.IO
Socket.IO biedt realtime-communicatie tussen uw node.js-server en clients met behulp van WebSockets. Het ondersteunt ook terugval tooother transporten (zoals lange polling) die met oudere browsers werken. Deze zelfstudie wordt helpt u bij het hosten van een toepassing op basis van Socket.IO chat als een Azure-web-app en ziet u hoe tooscale Hallo gebruikt toepassing [Azure Redis-Cache]. Zie voor meer informatie over Socket.IO <http://socket.io/>.

> [!NOTE]
> Hallo procedures in deze taak te gelden[App Service Web Apps]; voor Cloud-Services, Zie [bouwen van een Node.js-chattoepassing met Socket.IO op een Azure Cloud Service].
> 
> 

## <a name="download-hello-chat-example"></a>Hallo chat voorbeeld downloaden
Voor dit project, gebruiken we Hallo chat voorbeeld uit Hallo [Socket.IO GitHub-opslagplaats]. Hallo te volgen stappen toodownload Hallo-voorbeeld uitvoeren en voeg deze toohello project dat u eerder hebt gemaakt.

1. Download een [ZIP- of GZ gearchiveerd release] van Hallo Socket.IO project (versie 1.3.5 is gebruikt voor dit document)
2. Hallo archiveren en kopieer Hallo extraheren **voorbeelden\\chat** tooa nieuwe maplocatie. Bijvoorbeeld:  **\\knooppunt\\chat**.

## <a name="modify-appjs-and-install-modules"></a>App.js wijzigen en -modules installeren
1. Wijzig de naam van Hallo **index.js** bestand te**app.js**. Hierdoor kunnen Azure toodetect dat dit een Node.js-toepassing is.
2. Open Hallo **app.js** bestand in een teksteditor. Wijziging Hallo regel die `var io = require('../..')(server);` zoals hieronder wordt weergegeven:
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. Open Hallo **package.json** -bestand en voeg een verwijzing toosocket.io onder `dependencies`, zoals hieronder weergegeven:
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. Wijzig vanaf de opdrachtregel hello, toohello  **\\knooppunt\\chat** directory en gebruik npm tooinstall Hallo modules vereist door deze toepassing:
   
        npm install
   
    Hiermee installeert u Hallo modules in een submap met de naam **node_modules**.

## <a name="create-an-azure-web-app"></a>Een Azure-Web-App maken
Volg deze stappen toocreate een Azure-web-app, Git-publicatie inschakelen en vervolgens WebSocket-ondersteuning voor web-app Hallo inschakelen.

> [!NOTE]
> toocomplete in deze zelfstudie, moet u een Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Gratis proefversie van Azure</a> voor meer informatie.
> 
> 

1. Installeer hello Azure-opdrachtregelinterface (Azure CLI) en verbinding maken met tooyour Azure-abonnement. Zie [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md).
2. Als dit de eerste keer instellen van een opslagplaats in Azure, moet u de aanmeldingsreferenties toocreate. Voer van hello Azure CLI, Hallo volgende opdracht:
   
        azure site deployment user set [username] [password]
3. Wijzigen van toohello  **\\node\chat** directory en gebruik Hallo volgende toocreate opdracht een nieuwe Azure-web-app en een lokale Git-opslagplaats. Met deze opdracht maakt ook een Git remote met de naam 'azure'.
   
        azure site create mysitename --git
   
    U moet 'mysitename' vervangen door een unieke naam voor uw web-app.
4. Hallo bestaande bestanden toohello lokale opslagplaats met behulp van de volgende opdrachten Hallo doorvoeren:
   
        git add .
        git commit -m "Initial commit"
5. Hallo bestanden toohello Azure Web Apps opslagplaats pushen met Hallo volgende opdracht:
   
        git push azure master
   
    Wanneer u wordt gevraagd, typt u uw referenties uit stap 2. U ontvangt statusberichten zoals modules geïmporteerd op Hallo-server. Zodra dit proces is voltooid, wordt de toepassing hello worden gehost op uw Azure-web-app.
   
   > [!NOTE]
   > Tijdens de installatie van de module, merkt u fouten die ' hello... geïmporteerde project is niet gevonden '. Deze kunnen worden genegeerd.
   > 
   > 
6. Socket.IO WebSockets die niet zijn ingeschakeld op Azure standaard gebruikt. tooenable websockets, Hallo volgende opdracht gebruiken:
   
        azure site set -w
   
    Als u wordt gevraagd, geeft u Hallo-naam van Hallo web-app.
   
   > [!NOTE]
   > Hallo-opdracht 'azure site set -w' wordt alleen met versie 0.7.4 werk- of hoger van hello Azure-opdrachtregelinterface. U kunt ook inschakelen met behulp van Hallo WebSocket-ondersteuning [Azure Portal](https://portal.azure.com).
   > 
   > WebSockets met behulp van tooenable hello Azure Portal, klik op Hallo web-app uit de Web-Apps-blade hello, **alle instellingen** > **toepassingsinstellingen**. Onder **Web Sockets**, klikt u op **op**. Klik vervolgens op **Opslaan**.
   > 
   > 
7. tooview hello web-app op Azure, gebruik Hallo volgende opdracht toolaunch uw webbrowser en navigeer toohello gehost web-app:
   
        azure site browse

Uw app wordt nu uitgevoerd in Azure, en kan chatberichten tussen verschillende clients met Socket.IO doorsturen.

## <a name="scale-out"></a>Uitschalen
Socket.IO toepassingen kunnen worden uitgebreid met behulp van een **adapter** toodistribute berichten en gebeurtenissen tussen meerdere exemplaren van een toepassing. Hoewel er verschillende adapters beschikbaar zijn, Hallo [socket.io redis] adapter gemakkelijk kan worden gebruikt met hello Azure Redis-Cache-functie.

> [!NOTE]
> Een aanvullende vereiste voor het uitbreiden van een oplossing met Socket.IO is ondersteuning voor een tijdelijke sessies. Een tijdelijke sessies zijn standaard ingeschakeld voor Azure-Web-Apps via Azure routering van toepassingsaanvragen. Zie voor meer informatie [exemplaar affiniteit in Azure websites].
> 
> 

### <a name="create-a-redis-cache"></a>Een Redis-cache maken
Voer Hallo stappen uit in [maken van een cache in Azure Redis-Cache] toocreate een nieuwe cache.

> [!NOTE]
> Hallo opslaan **hostnaam** en **primaire sleutel** voor uw cache als deze nodig zijn de volgende stappen Hallo.
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a>Hallo redis en socket.io redis modules toevoegen
1. Wijzig vanaf een opdrachtregel toohello  **\\knooppunt\\chat** directory en gebruik Hallo opdracht te volgen.
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > Hallo-versies die zijn opgegeven in deze opdracht zijn Hallo-versies die zijn gebruikt bij het testen van dit artikel.
   > 
   > 
2. Hallo wijzigen **app.js** bestand tooadd Hallo volgende regels onmiddellijk na`var io = require('socket.io')(server);`
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    Vervang **redishostname** en **rediskey** met Hallo-hostnaam en -sleutel voor de Redis-cache.
   
    Hiermee wordt een publiceren en abonneren client toohello Redis-cache eerder hebt gemaakt. Hallo-clients worden vervolgens gebruikt met Hallo adapter tooconfigure Socket.IO toouse hello Redis-cache voor het doorgeven van berichten en gebeurtenissen tussen exemplaren van uw toepassing
   
   > [!NOTE]
   > Tijdens het Hallo **socket.io redis** adapter kan communiceren rechtstreeks tooRedis, Hallo huidige versie ondersteunt geen Hallo-verificatie vereist voor Azure Redis-cache. Dus Hallo initiële verbinding wordt gemaakt met Hallo **redis** -module, klikt u vervolgens Hallo-client wordt doorgegeven toohello **socket.io redis** adapter.
   > 
   > Terwijl Azure Redis-Cache beveiligde verbindingen via poort 6380 ondersteunt, ondersteund Hallo-modules die worden gebruikt in dit voorbeeld beveiligde verbindingen vanaf 14-7-2014 niet. Hallo bovenstaande code maakt gebruik van niet-beveiligde poort van 6379 Hallo standaard.
   > 
   > 
3. Opslaan Hallo gewijzigd **app.js**

### <a name="commit-changes-and-redeploy"></a>Wijzigingen vastleggen en implementeren
Vanaf de opdrachtregel in Hallo Hallo  **\\knooppunt\\chat** directory, gebruiken de volgende opdrachten toocommit wijzigingen Hallo en toepassing hello opnieuw distribueren.

    git add .
    git commit -m "implementing scale out"
    git push azure master

Wanneer wijzigingen Hallo pushbericht hebben ontvangen toohello server, kunt u uw site over meerdere exemplaren met behulp van de volgende opdracht Hallo schalen.

    azure site scale instances --instances #

Waar  **#**  is het aantal exemplaren toocreate Hallo.

U kunt tooyour web-app uit meerdere tooverify browsers of computers die goed tooall clients berichten worden verbinden.

## <a name="troubleshooting"></a>Problemen oplossen
### <a name="connection-limits"></a>Verbindingslimieten
Azure-Web-Apps is beschikbaar in meerdere SKU's Hallo resources beschikbaar tooyour site vast te stellen. Dit omvat Hallo aantal toegestane WebSocket-verbindingen. Zie voor meer informatie, Hallo [pagina met prijzen van Web-Apps].

### <a name="messages-arent-being-sent-using-websockets"></a>Berichten worden niet verzonden met behulp van WebSockets
Als clientbrowsers toolong polling in plaats van WebSockets teruggevallen houden, mogelijk vanwege een van de volgende Hallo.

* **Probeer Hallo transport toojust WebSockets beperken**
  
    Opdat Socket.IO toouse WebSockets als Hallo transport messaging, moeten zowel Hallo-server en client WebSockets ondersteunen. Als een of andere Hallo niet ondersteunt, zal de Socket.IO onderhandelen over een andere transport, zoals lange polling. de standaardlijst Hallo van transporten gebruikt door Socket.IO ` websocket, htmlfile, xhr-polling, jsonp-polling`. U kunt zorgen dat tooonly gebruik WebSockets door toe te voegen Hallo na code toohello **app.js** bestand, na het Hallo-regel die `, nicknames = {};`.
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > Houd er rekening mee dat oudere browsers die bieden geen ondersteuning voor WebSockets niet kunnen tooconnect toohello site worden terwijl Hallo bovenstaande code actief en is als de communicatie tooWebSockets alleen wordt beperkt.
  > 
  > 
* **SSL gebruiken**
  
    WebSockets is afhankelijk van bepaalde minder gebruikte HTTP-headers, zoals Hallo **Upgrade** header. Een aantal tussenliggende netwerkapparaten, zoals web proxy's, kunnen deze koppen worden verwijderd. tooavoid dit probleem op door Hallo WebSocket verbinding kan worden gemaakt via SSL.
  
    Een eenvoudige manier tooaccomplish is dit tooconfigure Socket.IO te`match origin protocol`. Dit Socket.IO toosecure WebSockets communicatie Hallo gelijk zijn aan die afkomstig zijn HTTP/HTTPS Hallo voor de webpagina Hallo aanvragen geïnstrueerd. Als een browser een toovisit HTTPS-URL voor uw website gebruikt, worden daaropvolgende WebSocket-communicatie via Socket.IO beveiligd via SSL.
  
    toomodify in dit voorbeeld tooenable deze configuratie toevoegen na de code toohello Hallo **app.js** bestand na het Hallo-regel die `, nicknames = {};`.
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* **Controleer of web.config-instellingen**
  
    Azure-web-apps die als host Node.js-toepassingen fungeren gebruiken Hallo **web.config** bestand tooroute binnenkomende aanvragen toohello Node.js-toepassing. Hallo voor WebSockets toofunction correct met Node.js-toepassingen, **web.config** Hallo na datum moet bevatten.
  
        <webSocket enabled="false"/>
  
    Hallo WebSockets IIS-module, waaronder een eigen implementatie van WebSockets en veroorzaakt een conflict met Node.js specifieke WebSocket-modules zoals Socket.IO wordt uitgeschakeld. Als deze regel niet aanwezig is of is ingesteld te`true`, kan dit Hallo reden die Hallo WebSocket transport niet voor uw toepassing werkt.
  
    Normaal gesproken Node.js-toepassingen bevatten geen een **web.config** -bestand, zodat Azure Websites wordt automatisch gegenereerd voor Node.js-toepassingen wanneer ze zijn geïmplementeerd. Omdat dit bestand wordt automatisch gegenereerd op Hallo-server, moet u Hallo FTP of FTPS-URL voor uw website tooview dit bestand. U kunt zoeken Hallo FTP en FTPS-URL's voor uw site in de klassieke portal Hallo op uw web-app selecteren en vervolgens Hallo **Dashboard** koppeling. Hallo URL's worden weergegeven in Hallo **snelle weergave** sectie.
  
  > [!NOTE]
  > Hallo **web.config** bestand alleen wordt gegenereerd door Azure Websites als uw toepassing zorgt niet voor. Als u een **web.config** bestand in de hoofdmap van uw toepassingsproject hello wordt gebruikt door Azure Web Apps.
  > 
  > 
  
    Hallo-vermelding is niet aanwezig of is ingesteld tooa waarde `true`, en vervolgens u maakt een **web.config** in de hoofdmap van uw Node.js-toepassing hello en geef een waarde van `false`.  Ter referentie: Hallo hieronder wordt een standaard **web.config** voor een toepassing die gebruikmaakt van **app.js** als Hallo toegangspunt.
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    Als uw toepassing gebruikmaakt van een toegangspunt dan **app.js**, moet u alle instanties van vervangen **app.js** Hello corrigeren toegangspunt. Bijvoorbeeld, vervangen **app.js** met **server.js**.

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen], waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd hoe toocreate een chatprogramma gehost in een Azure-web-app. Ook kunt u deze toepassing als een Azure Cloud Service hosten. Voor stapsgewijze instructies voor het tooaccomplish deze, Zie [bouwen van een Node.js-chattoepassing met Socket.IO op een Azure Cloud Service].

Zie voor meer informatie, ook Hallo [Node.js Developer Center].

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services].

<!-- URL List -->

[Azure Redis-Cache]: /documentation/services/redis-cache/
[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714
[pagina met prijzen van Web-Apps]: http://go.microsoft.com/fwlink/?LinkId=511643
[bouwen van een Node.js-chattoepassing met Socket.IO op een Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[Azure App Service en de invloed ervan op bestaande Azure Services]: http://go.microsoft.com/fwlink/?LinkId=529714
[Node.js Developer Center]: /develop/nodejs/
[App Service uitproberen]: https://azure.microsoft.com/try/app-service/
[exemplaar affiniteit in Azure websites]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[maken van een cache in Azure Redis-Cache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io redis]: https://github.com/socketio/socket.io-redis
[Socket.IO GitHub-opslagplaats]: https://github.com/socketio/socket.io
[ZIP- of GZ gearchiveerd release]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
