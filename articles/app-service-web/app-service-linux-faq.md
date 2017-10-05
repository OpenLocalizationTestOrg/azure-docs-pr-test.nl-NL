---
title: Web-App op Linux Veelgestelde vragen over Azure App Service | Microsoft Docs
description: Op Linux Veelgestelde vragen over Azure App Service Web-App.
keywords: Azure app service, web-app, veelgestelde vragen over, linux, oss
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
ms.date: 05/04/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 6122f28b35d143ec26a379ae9aa8aee9bdaaff9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a>Web-App op Linux Veelgestelde vragen over Azure App Service

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Met het uitbrengen van Web-App op Linux, momenteel niets over het toevoegen van functies en er verbeteringen aangebracht in ons platform. Hier volgen enkele veelgestelde vragen (FAQ) die onze klanten is aangevraagd door ons in de afgelopen maanden.
Als u een vraag, opmerking bij het artikel hebt en we deze zo snel mogelijk moet beantwoorden.

## <a name="built-in-images"></a>Ingebouwde afbeeldingen

**V:** ik wil de ingebouwde Docker-containers die het platform biedt vertakken. Waar vind ik die bestanden

**A:** vindt u alle Docker-bestanden op [GitHub](https://github.com/azure-app-service). U vindt alle Docker-containers op [Docker Hub](https://hub.docker.com/u/appsvc/).

**V:** wat zijn de verwachte waarden voor het starten van bestand sectie bij het configureren van de runtime-stack?

**A:** voor Node.Js, geeft u het configuratiebestand PM2 of het scriptbestand. Geef de naam van uw gecompileerde DLL voor .NET Core. Voor Ruby, kunt u het Ruby script dat u wilt uw app met initialiseren.

## <a name="management"></a>Beheer

**V:** wat gebeurt er wanneer ik de schakelaar opnieuw opstarten in de Azure portal?

**A:** dit is het equivalent van Docker opnieuw opstarten.

**V:** kan ik Secure Shell (SSH) om verbinding met de app-container virtuele machine (VM) te gebruiken?

**A:** Ja, kunt u dat doen via de site SCM, Controleer het volgende artikel voor meer informatie [SSH-ondersteuning voor Web-App op Linux](./app-service-linux-ssh-support.md)

**V:** maken van een Linux-App Service-vlak via SDK of een ARM-sjabloon, hoe kan ik dit bereikt?

**A:** moet u de `reserved` veld van de app-service naar `true`.

## <a name="continuous-integrationdeployment"></a>Continue integratie/implementatie

**V:** mijn web-app nog steeds de installatiekopie van een oude Docker-container wordt gebruikt nadat ik de afbeelding op Docker-Hub hebt bijgewerkt. Continue integratie/implementatie van aangepaste containers ondersteund?

**A:** continue integratie/implementatie instellen voor Azure Container register of DockerHub door het controleren van het volgende artikel afbeeldingen [continue implementatie met de Azure-Web-App op Linux](./app-service-linux-ci-cd.md). U kunt de container voor persoonlijke registers vernieuwen door te stoppen en vervolgens uw web-app te starten. Of u kunt wijzigen of toevoegen van een dummy toepassingsinstelling geforceerd vernieuwen van de container.

**V:** ondersteunen testomgevingen?

**A:** Ja.

**V:** kan ik gebruiken **webimplementatie** mijn web-app implementeren?

**A:** Ja, moet u een app instelling instellen `WEBSITE_WEBDEPLOY_USE_SCM` naar `false`.

## <a name="language-support"></a>Taalondersteuning

**V:** bieden u ondersteuning voor niet-gecompileerde .NET Core apps?

**A:** Ja.

**V:** u ondersteunen Composer als een afhankelijkheid manager voor PHP-apps?

**A:** Ja. Tijdens een Git-implementatie moet Kudu detecteren die u een PHP-toepassing (dankzij de aanwezigheid van een composer.json-bestand implementeert) en een installatie composer geactiveerd voor u.

## <a name="custom-containers"></a>Aangepaste containers

**V:** ik mijn eigen aangepaste container gebruik. Mijn app bevindt zich in de `\home\` directory, maar ik kan mijn bestanden vinden wanneer ik de inhoud met behulp van bladeren de [SCM site](https://github.com/projectkudu/kudu) of een FTP-client. Waar bevinden zich mijn bestanden?

**A:** We een SMB-share te koppelen van de `\home\` directory. Hierdoor wordt de inhoud die is er overschreven.

**V:** ik mijn eigen aangepaste container gebruik. Ik wil niet dat het platform voor het koppelen van een SMB-share op de `\home\`.

**A:** kunt u dat doen door in te stellen de `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app-instelling op `false`.

**V:** Mijn aangepaste container lang duurt om te starten en de container van het platform opnieuw opstarten voordat is gestart.

**A:** kunt u de tijd die het platform wachten moet alvorens het opnieuw starten van de container. Dit kan worden gedaan door het instellen van de `WEBSITES_CONTAINER_START_TIME_LIMIT` app-instelling op de gewenste waarde in seconden. De standaardwaarde is 230 seconden en de maximale waarde is 600 seconden.

**V:** wat is de indeling voor de url van de server persoonlijke register?

**A:** moet u het volledige register url, zoals `http://` of `https://`.

**V:** wat is de indeling voor de naam van de installatiekopie in persoonlijke register optie?

**A:** moet u de naam van de volledige installatiekopie (bv de url van de persoonlijke register inclusief toevoegen. myacr.azurecr.IO/DotNet:Latest)

**V:** ik wil meer dan één poort op de installatiekopie van mijn aangepaste container. Is dit mogelijk?

**A:** momenteel, die niet wordt ondersteund.

**V:** kan ik mijn eigen opslag brengen?

**A:** momenteel die niet wordt ondersteund.

**V:** ik kan mijn aangepaste container bestand system of actief processen van de site SCM niet doorzoeken. Waarom is dat?

**A:** de SCM-site wordt uitgevoerd in een afzonderlijke container. U kunt het bestand systeem of met de processen van de app-container niet controleren.

**V:** Mijn aangepaste container luistert naar een andere poort dan poort 80. Hoe kan ik mijn app voor het routeren van de aanvragen naar deze poort configureren?

**A:** hebben We automatische poortdetectie, ook kunt u een toepassing instelling opgeven **WEBSITES_PORT**, en wijs hieraan de waarde van het verwachte poortnummer. Eerder het platform werd gebruikt `PORT` app instelt, we van plan bent deze app instellen voor het gebruik afschaffen en voor het gebruik van verplaatsen `WEBSITES_PORT` uitsluitend.

**V:** heb ik nodig voor het implementeren van HTTPS in Mijn aangepaste container.

**A:** Nee, het platform HTTPS-beëindiging aan de gedeelde frontends verwerkt.

## <a name="pricing-and-sla"></a>Prijzen en SLA

**V:** wat is de prijzen terwijl u de openbare preview?

**A:** u kosten in rekening gebracht Halveer het aantal uren dat uw app wordt uitgevoerd, met de normale prijzen voor Azure App Service. Dit betekent dat u een korting van 50 procent op normale prijzen van Azure App Service krijgt.

## <a name="other"></a>Overige

**V:** wat zijn de ondersteunde tekens in toepassingsnamen instellingen?

**A:** u kunt alleen A-Z, a-z, 0-9 en het onderstrepingsteken gebruiken voor toepassingsinstellingen.

**V:** waar kan ik nieuwe functies aanvragen?

**A:** dient u uw idee op de [forum met feedback van Web-Apps](https://aka.ms/webapps-uservoice). '[Linux]' toevoegen aan de titel van uw idee.

## <a name="next-steps"></a>Volgende stappen
* [Wat is Azure-Web-App op Linux?](app-service-linux-intro.md)
* [SSH-ondersteuning voor Azure-Web-App op Linux](./app-service-linux-ssh-support.md)
* [Faseringsomgevingen in Azure App Service instellen](./web-sites-staged-publishing.md)
* [Continue implementatie met Azure-Web-App op Linux](./app-service-linux-ci-cd.md)
