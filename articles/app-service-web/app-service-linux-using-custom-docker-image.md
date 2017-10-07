---
title: aaaHow toouse een aangepaste Docker-afbeelding voor Azure-Web-App op Linux | Microsoft Docs
description: Hoe een aangepaste Docker toouse afbeelding voor Azure-Web-App op Linux.
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
ms.openlocfilehash: 8853095d0e1067cfea4297bbd23b622fe4a0d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a>Met behulp van een aangepaste Docker-afbeelding voor Azure-Web-App op Linux #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


App Service biedt vooraf gedefinieerde toepassing stacks op Linux met ondersteuning voor specifieke versies, zoals PHP 7.0 en Node.js 4.5. Op Linux-App Service gebruikt Docker-containers toohost deze kan toepassing stacks vooraf gebouwd. U kunt een aangepaste installatiekopie toodeploy voor Docker ook uw web-app tooan toepassing stack die niet al is gedefinieerd in Azure gebruiken. Aangepaste Docker-installatiekopieën kunnen worden gehost op ofwel een openbaar of particulier Docker-opslagplaats.


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a>Procedure: een aangepaste Docker-installatiekopie voor een web-app instellen
U kunt aangepaste Docker-installatiekopie Hallo voor zowel nieuwe en bestaande webs apps instellen. Wanneer u een web-app maken in Linux in Hallo [Azure-portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), klikt u op **configureren container** tooset een aangepaste Docker-installatiekopie:

![Aangepaste Docker-installatiekopie voor een nieuwe WebApp op Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a>Procedure: een aangepaste installatiekopie van Docker van Docker-Hub gebruiken ##
toouse een aangepaste installatiekopie Docker van Docker-Hub:

1. In Hallo [Azure-portal](https://portal.azure.com), vervolgens uw web-app op Linux, niet vinden in **instellingen** klikt u op **Docker-Container**.

2.  Selecteer **Docker Hub** als Hallo **Afbeeldingsbron**, klik dan ofwel **openbare** of **persoonlijke** en type Hallo **installatiekopie en optionele tagnaam**, zoals `node:4.5`. Hallo **startopdracht** is set automatisch op basis van wat is gedefinieerd in Hallo Docker-bestand, maar u kunt uw eigen opdrachten instellen.  

    ![Afbeelding van de openbare opslagplaats Docker Hub configureren][2]

    Wanneer uw installatiekopie van een persoonlijke bibliotheek is, moet u ook tooenter hello Docker Hub referenties als (**aanmelding gebruikersnaam** en **wachtwoord**) voor Hallo persoonlijke Docker-Hub-opslagplaats.

    ![Afbeelding van de opslagplaats voor persoonlijke Docker Hub configureren][3]

3. Nadat u de container Hallo hebt geconfigureerd, klikt u op **opslaan**.

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a>Hoe toouse een Docker een installatiekopie van een installatiekopie van het persoonlijke register ##
een aangepaste Docker-installatiekopie uit het register van een installatiekopie van persoonlijke toouse:

1. In Hallo [Azure-portal](https://portal.azure.com), vervolgens uw web-app op Linux, niet vinden in **instellingen** klikt u op **Docker-Container**.

2.  Klik op **persoonlijke register** als Hallo **Afbeeldingsbron**. Voer Hallo **installatiekopie en de optionele codenaam**, **Server-URL** voor persoonlijke register hello, samen met de Hallo referenties (**aanmelding gebruikersnaam** en **wachtwoord** ). Klik op **Opslaan**.

    ![Afbeelding van Docker uit persoonlijke register configureren][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a>Hoe: Hallo-poort die wordt gebruikt door uw installatiekopie Docker instellen ##

Wanneer u een aangepaste Docker-installatiekopie voor uw web-app gebruikt, kunt u Hallo `WEBSITES_PORT` omgevingsvariabele in uw Dockerfile, toohello gegenereerd container wordt toegevoegd. Overweeg het volgende voorbeeld van een docker-bestand voor een Ruby toepassing hello:

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

U ziet op de laatste regel van de opdracht Hallo dat die Hallo WEBSITES_PORT-omgevingsvariabele wordt doorgegeven tijdens runtime. Houd er rekening mee dat hoofdlettergebruik van belang in opdrachten is.

Eerder Hallo platform werd gebruikt `PORT` app instelt, we van plan bent toodeprecate Hallo Gebruik deze app instellen en verplaatsen toousing `WEBSITES_PORT` uitsluitend.

Wanneer u een bestaande Docker-installatiekopie gemaakt door iemand anders gebruikt, moet u mogelijk een andere poort dan poort 80 toospecify voor Hallo-toepassing. tooconfigure Hallo poort, het toevoegen van een benoemde toepassingsinstelling `WEBSITES_PORT` met Hallo waarde zoals hieronder wordt weergegeven:

![App-poortinstelling voor de installatiekopie van een aangepaste Docker configureren][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a>Hoe: Hallo starten van de tijd voor uw installatiekopie Docker instellen ##

Standaard, als uw container niet wordt gestart voordat 230 seconden opnieuw Hallo platform de container. Als uw aangepaste Docker-installatiekopie in meer dan 230 seconden wordt gestart, kunt u Hallo `WEBSITES_CONTAINER_START_TIME_LIMIT` instellen, app Hallo-waarde voor deze instelling is in seconden, wordt hierdoor Hallo platform behouden uw container uitgevoerd voordat u deze opnieuw. Hallo-standaardwaarde is 230 seconden en Hallo maximaal toegestane waarde is 600 seconden.

## <a name="how-to-unmount-hello-platform-provided-storage"></a>Hoe: ontkoppelen Hallo platform opgegeven opslag ##

Standaard gekoppeld Hallo platform een permanente opslag share toohello `\home\` directory. Als uw installatiekopie container niet nodig heeft voor een permanente share, kunt u uitschakelen dat opslag koppelen door de instelling Hallo `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app instellen te`false`. U hebt nog altijd toegang tot toothat opslag van Hallo scm-site en alle Docker-Logboeken (indien ingeschakeld) toohello logboekbestanden gegenereerd door het Hallo-platform worden geschreven.

## <a name="how-to-switch-back-toousing-a-built-in-image"></a>Hoe: gaat u terug toousing een installatiekopie van het ingebouwde ##

tooswitch van het gebruik van een aangepaste installatiekopie toousing een ingebouwde installatiekopie:

1. In Hallo [Azure-portal](https://portal.azure.com), vervolgens uw web-app op Linux, niet vinden in **instellingen** klikt u op **App Service**.

2. Selecteer uw **Runtime Stack** toouse Hallo ingebouwde afbeelding, klikt u vervolgens op **opslaan**. 

![Afbeelding van de ingebouwde Docker configureren][5]


## <a name="troubleshooting"></a>Problemen oplossen ##

Wanneer uw toepassing toostart door uw aangepaste Docker-installatiekopie mislukt, controleert u Hallo die docker Hallo logboekbestanden directory zich aanmeldt. U kunt toegang tot deze map via uw SCM-site of via de FTP.
Hallo toolog `stdout` en `stderr` van de container, moet u tooenable **Docker-Container logboekregistratie** onder **diagnostische logboeken**.

![Logboekregistratie inschakelen][8]

![Met behulp van Kudu tooview Docker-Logboeken][7]

U toegang hebt tot Hallo SCM site uit **geavanceerde hulpmiddelen** in Hallo **ontwikkelingsprogramma's** menu.

## <a name="next-steps"></a>Volgende stappen ##

Ga als volgt Hallo volgen koppelingen tooget de slag met Web-App op Linux.   

* [Inleiding tooAzure Web-App op Linux](./app-service-linux-intro.md)
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
