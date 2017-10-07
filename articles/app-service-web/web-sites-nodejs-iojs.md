---
title: aaaHow toouse io.js met Azure App Service Web Apps
description: Meer informatie over hoe een web-app in Azure App Service met io.js toouse.
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a>Hoe toouse io.js met Azure App Service Web Apps
Hallo populaire knooppunt fork [io.js] biedt verschillende verschillen-tooJoyent Node.js-project, inclusief een meer geopende governance-model, een snellere releasecyclus en een sneller acceptatie van nieuwe en experimentele JavaScript-functies.

Terwijl [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web-Apps heeft veel Node.js-versies die vooraf is geïnstalleerd, kunt u ook voor een gebruiker opgegeven Node.js-binair bestand. Dit artikel bevat twee methoden mogelijk hello gebruiken io.js op App Service Web Apps: gebruik van een script voor uitgebreide implementatie, die configureert automatisch de meest recente beschikbare io.js versie van Azure toouse hello, evenals Hallo handmatig uploaden van een binair io.js Hallo. 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a>Met behulp van een Script voor implementatie
App Service Web Apps uitgevoerd na de implementatie van een Node.js-app, een aantal kleine opdrachten tooensure die omgeving Hallo juist is geconfigureerd. Met een implementatiescript, kan dit proces worden aangepaste tooinclude Hallo downloaden en de configuratie van io.js.

Hallo [io.js implementatiescript](https://github.com/felixrieseberg/iojs-azure) is beschikbaar op GitHub. Kopieer in tooenable io.js op uw web-app **.deployment**, **deploy.cmd** en **IISNode.yml** toohello hoofdmap van de toepassingsmap tooWeb Apps en implementeren.  

het eerste bestand Hello, **.deployment**, Hiermee geeft u Web-Apps toorun **deploy.cmd** van implementatie. Dit script alle Hallo gebruikelijke stappen voor een Node.js-toepassing wordt uitgevoerd, maar ook de meest recente versie Hallo van io.js gedownload. Ten slotte **IISNode.yml** Web-Apps toouse alleen Hallo gedownload io.js binaire in plaats van een vooraf geïnstalleerde Node.js binair configureert.

> [!NOTE]
> tooupdate hello io.js binair gebruikt, alleen uw toepassing opnieuw distribueren - Hallo script downloaden een nieuwe versie van io.js die elke één keer Hallo-toepassing wordt geïmplementeerd.
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a>Met behulp van handmatige installatie
Hallo handmatige installatie van een aangepaste io.js versie bevat slechts twee stappen. Eerst downloaden Hallo **win x64** binaire rechtstreeks vanuit Hallo [io.js distributie]. Vereist zijn twee bestanden - **iojs.exe** en **iojs.lib**. Opslaan beide bestanden tooa map in uw web-app, bijvoorbeeld in **bin/iojs**.

tooconfigure Web-Apps toouse **iojs.exe** in plaats van een vooraf geïnstalleerde versie van de knooppunt maken een **IISNode.yml** -bestand op basis van uw toepassing hello en Hallo volgt regel toevoegen.

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe toouse io.js met App Service Web Apps met zowel opgegeven voor de implementatiescripts, evenals een handmatige installatie. 

> [!NOTE]
> IO.js wordt zwaar ontwikkeling en vaker bijgewerkt dan Node.js. Een aantal Node.js-modules werkt mogelijk niet op io.js - Neem Raadpleeg [io.js op GitHub] voor het oplossen van problemen.
> 
> 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

[io.js]: https://iojs.org
[io.js distributie]: https://iojs.org/dist/
[io.js op GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
