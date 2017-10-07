---
title: configuratie voor Node.js in Azure-Web-App op Linux aaaUsing PM2 | Microsoft Docs
description: Met behulp van PM2-configuratie voor Node.js in Azure-Web-App op Linux
keywords: Azure app service, web-app, nodejs, pm2, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: fb420f32-6d74-49c7-992f-0ed5616e66e7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 923783ffe656e01c43318899d1a656b553ebb5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a>PM2 configuratie gebruiken voor Node.js in Azure-Web-App op Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Als u Hallo toepassing stack tooNode.js voor Azure-Web-App op Linux instellen, krijgt u Hallo optie tooset een Node.js-bestand voor opstarten zoals weergegeven in Hallo installatiekopie te volgen:

![Een Node.js-bestand voor opstarten][1]

U kunt deze optie toodo een Hallo taken te volgen:

* Geef het opstartscript Hallo voor uw Node.js-app (bijvoorbeeld: /bin/server.js).
* Geef Hallo PM2 configuration file toouse voor uw Node.js-app (bijvoorbeeld: /foo/process.json).
  
  > [!NOTE]
  > Als u uw Node.js-processen toorestart automatisch wilt wanneer bepaalde bestanden zijn gewijzigd, moet u Hallo PM2 configuratie gebruiken. Uw toepassing won't anders wordt opnieuw opgestart na ontvangst van meldingen (bijvoorbeeld wanneer uw toepassingscode gewijzigd).
  > 
  > 

U kunt controleren Hallo Node.js [verwerken bestand documentatie](http://pm2.keymetrics.io/docs/usage/application-declaration/) voor alle opties hello, maar hier een voorbeeld volgt van wat u als uw bestand process.json gebruiken kunt:

        {
          "name"        : "worker",
          "script"      : "./bin/server.js",
          "instances"   : 1,
          "merge_logs"  : true,
          "log_date_format" : "YYYY-MM-DD HH:mm Z",
          "watch": ["./bin/server.js", "foo.txt"],
          "watch_options": {
            "followSymlinks": true,
            "usePolling"   : true,
            "interval"    : 5
          }
        }

Belangrijke opmerkingen toonote in deze configuratie zijn:

* de eigenschap 'script' Hello geeft startscript van uw toepassing.
* Hallo 'exemplaren'-eigenschap geeft aan hoeveel exemplaren van Hallo knooppunt proces toolaunch. Als u uw toepassing op grotere virtuele machines die meerdere kernen hebben uitvoert, is het een goed idee toomaximize uw resources door een hogere waarde hier.
* Hallo 'volgen' matrix geeft alle bestanden die u toorestart Hallo knooppunt proces voor wilt zien wanneer ze wijzigen.
* Voor 'watch_options' hello moet momenteel u toospecify 'usePolling' als waar vanwege Hallo manier die de inhoud van uw toepassing is gekoppeld.

## <a name="next-steps"></a>Volgende stappen
* [Wat is Azure-Web-App op Linux?](app-service-linux-intro.md)
* [Web-App op Linux Veelgestelde vragen over Azure App Service](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
