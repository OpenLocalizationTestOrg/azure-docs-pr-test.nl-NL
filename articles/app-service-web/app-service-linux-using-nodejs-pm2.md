---
title: Met PM2 configuratie voor Node.js in Azure-Web-App op Linux | Microsoft Docs
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
ms.openlocfilehash: 5002400a673e2c5cc4290bab488b839fb2282966
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a>PM2 configuratie gebruiken voor Node.js in Azure-Web-App op Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Als u de toepassing-stack ingesteld op Node.js voor Azure-Web-App op Linux, krijgt u de mogelijkheid om in te stellen van een Node.js opstartbestand, zoals weergegeven in de volgende afbeelding:

![Een Node.js-bestand voor opstarten][1]

U kunt deze optie gebruiken om een van de volgende taken:

* Geef het opstartscript voor uw Node.js-app (bijvoorbeeld: /bin/server.js).
* Geef de PM2 configuratiebestand moet worden gebruikt voor uw Node.js-app (bijvoorbeeld: /foo/process.json).
  
  > [!NOTE]
  > Als u wilt dat uw Node.js-processen worden automatisch opnieuw opgestart wanneer bepaalde bestanden zijn gewijzigd, gebruikt u de configuratie van de PM2. Uw toepassing won't anders wordt opnieuw opgestart na ontvangst van meldingen (bijvoorbeeld wanneer uw toepassingscode gewijzigd).
  > 
  > 

U kunt de Node.js controleren [verwerken bestand documentatie](http://pm2.keymetrics.io/docs/usage/application-declaration/) voor alle opties maar volgende is een voorbeeld van wat u kunt gebruiken als uw bestand process.json:

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

Belangrijke opmerkingen in deze configuratie zijn:

* De scripteigenschap '' geeft startscript van uw toepassing.
* De eigenschap 'exemplaren' bepaalt hoeveel exemplaren van het knooppunt proces te starten. Als u uw toepassing op grotere virtuele machines die meerdere kernen hebben uitvoert, is het een goed idee om uw resources maximaliseren door een hogere waarde hier.
* De matrix 'volgen' geeft alle bestanden die u het proces van het knooppunt voor het opnieuw opstarten wilt als ze wijzigen.
* Voor de 'watch_options' moet u momenteel 'usePolling' opgeeft als waar vanwege de manier waarop die de inhoud van uw toepassing is gekoppeld.

## <a name="next-steps"></a>Volgende stappen
* [Wat is Azure-Web-App op Linux?](app-service-linux-intro.md)
* [Web-App op Linux Veelgestelde vragen over Azure App Service](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
