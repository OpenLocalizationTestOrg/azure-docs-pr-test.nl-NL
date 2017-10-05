---
title: Met behulp van Ruby in Azure App Service-Web-App op Linux | Microsoft Docs
description: Met behulp van Ruby in Azure App Service-Web-App op Linux.
keywords: Azure app service, web-app, veelgestelde vragen over, linux, besturingssystemen, ruby
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 56105d1bc153e552e12c0c408c8f6075e4eff9d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a>Met behulp van Ruby in Web-App op Linux #

Er is ondersteuning voor Ruby v.2.3 geïntroduceerd met de meest recente update naar de back-end. De configuratie van uw Linux-web-app instelt, kunt u de toepassing-stack.

## <a name="using-the-azure-portal"></a>Azure Portal gebruiken ##

In het nieuwe menu in de [Azure-portal](https://portal.azure.com), kunt u een Web-App maken in Linux van Web + mobiel optie, zoals wordt weergegeven in de volgende afbeelding:

![Beginnen met het maken van een web-app in de Azure portal][1]

Vervolgens moet de **blade maken** opent, zoals wordt weergegeven in de volgende afbeelding:

![De blade maken][2]

1. Uw web-app een naam geven.
2. Kies een bestaande resourcegroep of maak een nieuwe. (Zie beschikbare regio's in de [sectie beperkingen](app-service-linux-intro.md).)
3. Kies een bestaand Azure App Service-abonnement of een nieuwe maken. (Zie de opmerkingen bij de App Service-plan in de [sectie beperkingen](app-service-linux-intro.md).)
4. Kies de Ruby in de stacks ingebouwde Runtime.

Nadat uw Ruby web-app wordt gemaakt, kunt u met de Git- of FTP-implementeren.

Voor meer informatie over het maken van een app Ruby, Controleer de [get-handleiding](app-service-linux-ruby-get-started.md)

## <a name="next-steps"></a>Volgende stappen
* [Wat is een op Linux-Web-App?](app-service-linux-intro.md)
* [Lokale Git-implementatie op de Azure App Service](app-service-deploy-local-git.md)
* [Web-App op Linux Veelgestelde vragen over Azure App Service](app-service-linux-faq.md)
* [Een Ruby App maken met Azure-Web-App op Linux](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png