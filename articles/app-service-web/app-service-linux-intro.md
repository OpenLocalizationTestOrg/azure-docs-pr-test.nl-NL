---
title: aaaIntroduction tooAzure Web-App op Linux | Microsoft Docs
description: Meer informatie over Azure-Web-App op Linux.
keywords: Azure app service, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a>Inleiding tooAzure Web-App op Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Overzicht
Klanten kunnen voor ondersteunde toepassing stacks Web-App gebruiken op Linux toohost web-apps systeemeigen op Linux. Hallo volgende sectie vindt u Hallo toepassing stacks die momenteel worden ondersteund. 

## <a name="features"></a>Functies
Web-App op Linux ondersteunt momenteel Hallo toepassing stacks te volgen:

* Node.js
    * 4.4
    * 4.5
    * 6.2
    * 6.6
    * 6.9
    * 6.10
    * 6.11
    * 8.0
    * 8.1
* PHP
    * 5.6
    * 7.0
* .NET core
    * 1.0
    * 1.1
* Ruby
    * 2.3

Klanten kunnen hun toepassingen implementeren met behulp van:

* FTP
* Lokale Git
* GitHub
* Bitbucket

Voor het schalen van toepassing:

* Klanten kunnen worden geschaald web-apps omhoog en omlaag door het Hallo-laag van de App Service-abonnement wijzigen
* Klanten kunnen toepassingen uitbreiden en meerdere app-exemplaren binnen de grenzen Hallo van hun SKU uitvoeren

Voor Kudu enkele van de basisfunctionaliteit Hallo:

* Omgevingen
* Implementaties
* Basic-console
* SSH

Voor devops:

* Faseringsomgevingen
* ACR en DockerHub CI/CD

## <a name="limitations"></a>Beperkingen
Hello Azure-portal toont alleen functies die nu ook voor Web-App op Linux werken en verbergen Hallo rest. Als we het inschakelen van functies, zijn ze zichtbaar op Hallo-portal.

Sommige functies, zoals de integratie van virtueel netwerk, verificatie van Azure Active Directory/van derden of Kudu-site-uitbreidingen zijn nog niet beschikbaar. Zodra deze functies beschikbaar zijn, werken wij onze documentatie en blog over Hallo wijzigingen.

Deze openbare preview is momenteel alleen beschikbaar in Hallo gebieden te volgen:

* VS - west
* VS - oost
* West-Europa
* Noord-Europa
* Zuid-centraal VS
* Noord-centraal VS
* Zuidoost-Azië
* Oost-Azië
* Australië - oost
* Japan - oost
* Brazilië - zuid
* Zuid-India

Web-Apps op Linux wordt alleen ondersteund in Hallo specifieke app-serviceabonnementen en heeft geen een Free of Shared-laag. App Service-abonnementen voor reguliere- en Linux-web-apps zijn ook sluiten elkaar wederzijds uit, zodat u een Linux-web-app in een niet-Linux-app service-abonnement maken kunt.

Web-Apps op Linux moet worden gemaakt in een resourcegroep die geen niet-Linux web-apps in Hallo bevat dezelfde regio.

## <a name="troubleshooting"></a>Problemen oplossen ##

Wanneer uw toepassing toostart mislukt of als u wilt dat toocheck Hallo logboekregistratie van uw app, controleert u Hallo die docker Hallo logboekbestanden directory zich aanmeldt. U kunt toegang tot deze map via uw SCM-site of via de FTP.
Hallo toolog `stdout` en `stderr` van de container, moet u tooenable **Docker-Container logboekregistratie** onder **diagnostische logboeken**.

![Logboekregistratie inschakelen][2]

![Met behulp van Kudu tooview Docker-Logboeken][1]

U toegang hebt tot Hallo SCM site uit **geavanceerde hulpmiddelen** in Hallo **ontwikkelingsprogramma's** menu.

## <a name="next-steps"></a>Volgende stappen
Zie Hallo volgen koppelingen tooget met op Linux-App Service is gestart. U kunt vragen en problemen op boeken [ons forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Hoe een installatiekopie van een aangepaste Docker toouse voor Azure-Web-App op Linux](app-service-linux-using-custom-docker-image.md)
* [Met behulp van PM2-configuratie voor Node.js in Azure-Web-App op Linux](app-service-linux-using-nodejs-pm2.md)
* [Met behulp van .NET Core in Azure App Service-Web-App op Linux](app-service-linux-using-dotnetcore.md)
* [Met behulp van Ruby in Azure App Service-Web-App op Linux](app-service-linux-ruby-get-started.md)
* [Web-App op Linux Veelgestelde vragen over Azure App Service](app-service-linux-faq.md)
* [SSH-ondersteuning voor Azure-Web-App op Linux](./app-service-linux-ssh-support.md)
* [Faseringsomgevingen in Azure App Service instellen](./web-sites-staged-publishing.md)
* [Docker Hub continue implementatie met Azure-Web-App op Linux](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png