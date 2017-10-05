---
title: Een Azure-web-app uitgevoerd op Linux maken | Microsoft Docs
description: Web-app maken van workflow voor Azure-Web-App op Linux.
keywords: Azure app service, web-app, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 49091d4a85bed23927850f9c0bbc5ea8b6e8c9e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a>Een Azure-web-app uitgevoerd op Linux maken

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-the-azure-portal-to-create-your-web-app"></a>De Azure portal gebruiken om uw web-app maken
U kunt beginnen met het maken van uw web-app op Linux van de [Azure-portal](https://portal.azure.com) zoals weergegeven in de volgende afbeelding:

![Beginnen met het maken van een web-app in de Azure portal][1]

Vervolgens moet de **blade maken** opent, zoals wordt weergegeven in de volgende afbeelding:

![De blade maken][2]

1. Uw web-app een naam geven.
2. Kies een bestaande resourcegroep of maak een nieuwe. (Zie beschikbare regio's in de [sectie beperkingen](app-service-linux-intro.md).)
3. Kies een bestaand Azure App Service-abonnement of een nieuwe maken. (Zie de opmerkingen bij de App Service-plan in de [sectie beperkingen](app-service-linux-intro.md).)
4. Kies de stack van de toepassing die u wilt gebruiken. U kunt kiezen tussen verschillende versies van Node.js, PHP, .net Core en Ruby.

Nadat u de app hebt gemaakt, kunt u de toepassing-stack van de toepassingsinstellingen zoals weergegeven in de volgende afbeelding:

![Toepassingsinstellingen][3]

## <a name="deploy-your-web-app"></a>Uw web-app implementeren
Kiezen **implementatieopties** in de management portal biedt u de optie voor lokale Git- of GitHub-opslagplaats gebruiken voor het implementeren van uw toepassing. De rest van de instructies zijn vergelijkbaar met die voor een niet-Linux-web-app. U kunt de instructies in [lokale Git-implementatie](app-service-deploy-local-git.md) of [continue implementatie](app-service-continuous-deployment.md) om uw app te implementeren.

U kunt ook FTP gebruiken voor het uploaden van uw toepassing naar uw site. U kunt het FTP-eindpunt voor uw web-app krijgen van de diagnostische logboeken sectie zoals weergegeven in de volgende afbeelding:

![Diagnostische logboeken][4]

## <a name="next-steps"></a>Volgende stappen
* [Wat is Azure-Web-App op Linux?](app-service-linux-intro.md)
* [Met behulp van PM2-configuratie voor Node.js in Azure-Web-App op Linux](app-service-linux-using-nodejs-pm2.md)
* [Met behulp van Ruby in Azure App Service-Web-App op Linux](app-service-linux-ruby-get-started.md)
* [Web-App op Linux Veelgestelde vragen over Azure App Service](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
