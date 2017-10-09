---
title: een Azure aaaCreate web-app uitgevoerd op Linux | Microsoft Docs
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
ms.openlocfilehash: de1bd030345d5e2a8024012067b5bcaa2cca09dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a>Een Azure-web-app uitgevoerd op Linux maken

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a>Hello Azure portal toocreate uw web-app gebruiken
U kunt beginnen met het maken van uw web-app op Linux van Hallo [Azure-portal](https://portal.azure.com) zoals weergegeven in Hallo installatiekopie te volgen:

![Beginnen met het maken van een web-app op Hallo Azure-portal][1]

Vervolgens Hallo **blade maken** wordt geopend zoals weergegeven in Hallo installatiekopie te volgen:

![blade Hallo-maken][2]

1. Uw web-app een naam geven.
2. Kies een bestaande resourcegroep of maak een nieuwe. (Zie beschikbare regio's in Hallo [sectie beperkingen](app-service-linux-intro.md).)
3. Kies een bestaand Azure App Service-abonnement of een nieuwe maken. (Zie de opmerkingen bij de App Service-plan in Hallo [sectie beperkingen](app-service-linux-intro.md).)
4. Kies de toepassing hello stack die u van plan toouse bent. U kunt kiezen tussen verschillende versies van Node.js, PHP, .net Core en Ruby.

Nadat u Hallo app hebt gemaakt, kunt u Hallo toepassing stack van Hallo toepassingsinstellingen zoals weergegeven in Hallo installatiekopie te volgen:

![Toepassingsinstellingen][3]

## <a name="deploy-your-web-app"></a>Uw web-app implementeren
Kiezen **implementatieopties** van Hallo management portal biedt u Hallo optie toouse lokale Git- of GitHub-opslagplaats toodeploy uw toepassing. Hallo overige Hallo-instructies zijn vergelijkbaar toothose voor een niet-Linux-web-app. U kunt Hallo instructies in [lokale Git-implementatie](app-service-deploy-local-git.md) of [continue implementatie](app-service-continuous-deployment.md) toodeploy uw app.

U kunt uw toepassing tooyour site ook FTP-tooupload. U kunt krijgen Hallo FTP-eindpunt voor uw web-app van Hallo diagnostics sectie logs zoals weergegeven in Hallo volgende afbeelding:

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
