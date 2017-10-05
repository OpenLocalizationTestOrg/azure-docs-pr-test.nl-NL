---
title: Het gebruik van een aangepaste Docker-afbeelding voor Azure-Web-App op Linux | Microsoft Docs
description: Klik hier voor meer informatie over het gebruik van een aangepaste Docker-afbeelding voor Azure-Web-App op Linux.
keywords: Azure app service, web-app, linux, docker, container
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: b97bd4e6-dff0-4976-ac20-d5c109a559a8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 1458217a31c4781b28877c030a665f5b22819e13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a>Met behulp van een aangepaste Docker-afbeelding voor Azure-Web-App op Linux #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


App Service biedt vooraf gedefinieerde toepassing stacks op Linux met ondersteuning voor specifieke versies, zoals PHP 7.0 en Node.js 4.5. Docker-containers op Linux-App Service gebruikt voor het hosten van deze vooraf gemaakte toepassing stacks. U kunt ook een aangepaste Docker-installatiekopie gebruiken voor het implementeren van uw web-app naar de stack van een toepassing die niet al is gedefinieerd in Azure. Aangepaste Docker-installatiekopieën kunnen worden gehost op ofwel een openbaar of particulier Docker-opslagplaats.


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a>Procedure: een aangepaste Docker-installatiekopie voor een web-app instellen
U kunt de aangepaste Docker-afbeelding voor beide apps nieuwe en bestaande webs instellen. Wanneer u een web-app maken in Linux in de [Azure-portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), klikt u op **configureren container** in te stellen van een aangepaste Docker-installatiekopie:

![Aangepaste Docker-installatiekopie voor een nieuwe WebApp op Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a>Procedure: een aangepaste installatiekopie van Docker van Docker-Hub gebruiken ##
Gebruik een aangepaste installatiekopie Docker van Docker-Hub:

1. In de [Azure-portal](https://portal.azure.com), vervolgens uw web-app op Linux, niet vinden in **instellingen** klikt u op **Docker-Container**.

2.  Selecteer **Docker Hub** als de **Afbeeldingsbron**, klik dan ofwel **openbare** of **persoonlijke** en typt u de **installatiekopie en optionele tagnaam**, zoals `node:4.5`. De **startopdracht** is set automatisch op basis van wat is gedefinieerd in de Docker-bestand, maar u kunt uw eigen opdrachten instellen.  

    ![Afbeelding van de openbare opslagplaats Docker Hub configureren][2]

    Wanneer uw installatiekopie van een persoonlijke bibliotheek is, moet u ook de referenties van de Docker-Hub als invoeren (**aanmelding gebruikersnaam** en **wachtwoord**) voor de opslagplaats voor persoonlijke Docker-Hub.

    ![Afbeelding van de opslagplaats voor persoonlijke Docker Hub configureren][3]

3. Nadat u de container hebt geconfigureerd, klikt u op **opslaan**.

## <a name="how-to-use-a-docker-image-from-a-private-image-registry"></a>Het gebruik van een Docker-installatiekopie uit het register van een persoonlijke afbeelding ##
Een aangepaste Docker-installatiekopie uit het register van een persoonlijke installatiekopie gebruiken:

1. In de [Azure-portal](https://portal.azure.com), vervolgens uw web-app op Linux, niet vinden in **instellingen** klikt u op **Docker-Container**.

2.  Klik op **persoonlijke register** als de **Afbeeldingsbron**. Voer de **installatiekopie en de optionele codenaam**, **Server-URL** voor het persoonlijke register, samen met de referenties (**aanmelding gebruikersnaam** en **wachtwoord**). Klik op **Opslaan**.

    ![Afbeelding van Docker uit persoonlijke register configureren][4]


## <a name="how-to-set-the-port-used-by-your-docker-image"></a>Hoe: Stel de poort die wordt gebruikt door de Docker-afbeelding ##

Wanneer u een aangepaste Docker-installatiekopie voor uw web-app gebruikt, kunt u de `WEBSITES_PORT` omgevingsvariabele in uw Dockerfile die wordt toegevoegd aan de gegenereerde container. Houd rekening met het volgende voorbeeld van een docker-bestand voor een Ruby toepassing:

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

Op de laatste regel van de opdracht ziet u dat de omgevingsvariabele WEBSITES_PORT wordt doorgegeven tijdens runtime. Houd er rekening mee dat hoofdlettergebruik van belang in opdrachten is.

Eerder het platform werd gebruikt `PORT` app instelt, we van plan bent deze app instellen voor het gebruik afschaffen en voor het gebruik van verplaatsen `WEBSITES_PORT` uitsluitend.

Wanneer u een bestaande Docker-installatiekopie gemaakt door iemand anders gebruikt, moet u mogelijk een andere poort dan poort 80 voor de toepassing opgeven. Voeg een toepassingsinstelling met de naam voor het configureren van de poort `WEBSITES_PORT` met de waarde zoals hieronder wordt weergegeven:

![App-poortinstelling voor de installatiekopie van een aangepaste Docker configureren][6]

## <a name="how-to-set-the-startup-time-for-your-docker-image"></a>Procedure: de opstarttijd van uw installatiekopie Docker instellen ##

Standaard, als uw container niet wordt gestart voordat 230 seconden, opnieuw het platform de container. Als uw aangepaste Docker-installatiekopie in meer dan 230 seconden wordt gestart, kunt u de `WEBSITES_CONTAINER_START_TIME_LIMIT` app instelt, de waarde voor deze instelling is in seconden, hierdoor kan de platform-Houd uw container uitgevoerd voordat u deze opnieuw. De standaardwaarde is 230 seconden en de maximale toegestane waarde is 600 seconden.

## <a name="how-to-unmount-the-platform-provided-storage"></a>Hoe: ontkoppelen van de opgegeven platform-opslag ##

Standaard wordt het platform een permanente storage-share te koppelen van de `\home\` directory. Als uw installatiekopie container niet nodig heeft voor een permanente share, kunt u uitschakelen dat opslag koppelen door in te stellen de `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app-instelling op `false`. U hebt nog steeds toegang tot deze opslag van de site scm en alle Docker-Logboeken (indien ingeschakeld) worden geschreven naar de logboekbestanden die worden gegenereerd door het platform.

## <a name="how-to-switch-back-to-using-a-built-in-image"></a>Hoe: Ga terug naar de met de installatiekopie van een ingebouwde ##

Overschakelen van met een aangepaste installatiekopie voor het gebruik van een installatiekopie van het ingebouwde:

1. In de [Azure-portal](https://portal.azure.com), vervolgens uw web-app op Linux, niet vinden in **instellingen** klikt u op **App Service**.

2. Selecteer uw **Runtime Stack** wilt gebruiken voor de installatiekopie van het ingebouwde, klikt u vervolgens op **opslaan**. 

![Afbeelding van de ingebouwde Docker configureren][5]


## <a name="troubleshooting"></a>Problemen oplossen ##

Als uw toepassing om te beginnen met uw aangepaste Docker-installatiekopie is mislukt, Controleer u dat de Docker-Logboeken in de map met logboekbestanden. U kunt toegang tot deze map via uw SCM-site of via de FTP.
Logboek de `stdout` en `stderr` van de container, moet u inschakelen **Docker-Container logboekregistratie** onder **diagnostische logboeken**.

![Logboekregistratie inschakelen][8]

![Met behulp van Kudu Docker-logboeken weergeven][7]

U toegang hebt tot de site SCM bij **geavanceerde hulpmiddelen** in de **ontwikkelingsprogramma's** menu.

## <a name="next-steps"></a>Volgende stappen ##

Volg de volgende koppelingen aan de slag met Web-App op Linux.   

* [Inleiding tot Azure-Web-App op Linux](./app-service-linux-intro.md)
* [Met behulp van PM2-configuratie voor Node.js in Azure-Web-App op Linux](./app-service-linux-using-nodejs-pm2.md)
* [Web-App op Linux Veelgestelde vragen over Azure App Service](app-service-linux-faq.md)

Post een bericht vragen en problemen op [ons forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
