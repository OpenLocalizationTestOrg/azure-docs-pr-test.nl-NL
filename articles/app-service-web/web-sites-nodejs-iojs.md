---
title: io.js gebruiken met Web Apps van Azure App Service
description: Informatie over het gebruik van een web-app in Azure App Service met io.js.
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
ms.openlocfilehash: 4800504e1939a46842d15e8c9d4279a4b9cae787
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-iojs-with-azure-app-service-web-apps"></a>io.js gebruiken met Web Apps van Azure App Service
De populaire knooppunt fork [io.js] biedt verschillende verschillen van Joyent Node.js-project, inclusief een meer geopende governance-model, een snellere releasecyclus en een sneller acceptatie van nieuwe en experimentele JavaScript-functies.

Terwijl [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web-Apps heeft veel Node.js-versies die vooraf is geïnstalleerd, kunt u ook voor een gebruiker opgegeven Node.js-binair bestand. Dit artikel bevat twee methoden om het gebruik van io.js op App Service Web Apps: het gebruik van een script voor uitgebreide implementatie, Azure voor het gebruik van de meest recente versie van de beschikbare io.js, evenals het handmatig uploaden van een binaire io.js automatisch te configureren. 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a>Met behulp van een Script voor implementatie
App Service Web Apps uitgevoerd na de implementatie van een Node.js-app, een aantal kleine opdrachten om ervoor te zorgen dat de omgeving juist is geconfigureerd. Met een implementatiescript, kan dit proces zodanig dat het downloaden en de configuratie van io.js worden aangepast.

De [io.js implementatiescript](https://github.com/felixrieseberg/iojs-azure) is beschikbaar op GitHub. Kopieer zodat io.js op uw web-app **.deployment**, **deploy.cmd** en **IISNode.yml** naar de hoofdmap van de map van uw toepassing en implementeren voor Web-Apps.  

Het eerste bestand **.deployment**, geeft u Web-Apps uit te voeren opdracht **deploy.cmd** van implementatie. Dit script wordt uitgevoerd de gebruikelijke stappen voor een Node.js-toepassing, maar ook downloadt de nieuwste versie van io.js. Ten slotte **IISNode.yml** configureert voor het gebruik van alleen de gedownloade io.js binaire in plaats van een vooraf geïnstalleerde binair voor Node.js-Web-Apps.

> [!NOTE]
> Het gebruikte io.js binaire bestand bijwerken, net opnieuw implementeren van uw toepassing - het script wordt een nieuwe versie downloaden van io.js telkens één wanneer die de toepassing wordt geïmplementeerd.
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a>Met behulp van handmatige installatie
De handmatige installatie van een aangepaste io.js versie bevat slechts twee stappen. Eerst, downloaden de **win x64** binaire rechtstreeks vanuit de [io.js distributie]. Vereist zijn twee bestanden - **iojs.exe** en **iojs.lib**. Beide bestanden naar een map in uw web-app bijvoorbeeld opslaan in **bin/iojs**.

Voor het configureren van Web-Apps gebruiken **iojs.exe** in plaats van een vooraf geïnstalleerde versie van de knooppunt maken een **IISNode.yml** -bestand in de hoofdmap van uw toepassing en voeg de volgende regel toe.

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a>Volgende stappen
Io.js met App Service Web Apps met zowel opgegeven implementatiescripts ook als handmatige installatie in dit artikel die hebt u geleerd hoe moet worden gebruikt. 

> [!NOTE]
> IO.js wordt zwaar ontwikkeling en vaker bijgewerkt dan Node.js. Een aantal Node.js-modules werkt mogelijk niet op io.js - Neem Raadpleeg [io.js op GitHub] voor het oplossen van problemen.
> 
> 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

[io.js]: https://iojs.org
[io.js distributie]: https://iojs.org/dist/
[io.js op GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
