---
title: App Service Web-App in Linux Veelgestelde vragen over aaaAzure | Microsoft Docs
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
ms.openlocfilehash: c7798d9144d936eecdc0e191fc870b0ee0b220c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a>Web-App op Linux Veelgestelde vragen over Azure App Service

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Hallo-versie van Web-App op Linux, momenteel niets over het toevoegen van functies en verbeteringen tooour platform maken. Hier volgen enkele veelgestelde vragen (FAQ) die onze klanten is aangevraagd door ons via Hallo laatste maanden.
Als u een vraag, opmerking bij Hallo artikel hebt en we deze zo snel mogelijk moet beantwoorden.

## <a name="built-in-images"></a>Ingebouwde afbeeldingen

**V:** ik wil toofork Hallo ingebouwde Docker-containers die Hallo platform biedt. Waar vind ik die bestanden

**A:** vindt u alle Docker-bestanden op [GitHub](https://github.com/azure-app-service). U vindt alle Docker-containers op [Docker Hub](https://hub.docker.com/u/appsvc/).

**V:** wat Hallo verwachte waarden voor het starten van de sectie Hallo zijn bij het configureren van Hallo runtime stack?

**A:** voor Node.Js u Hallo PM2 configuratiebestand of opgeven het scriptbestand. Geef de naam van uw gecompileerde DLL voor .NET Core. Voor Ruby, kunt u Hallo Ruby script opgeven dat u wilt dat tooinitialize uw app.

## <a name="management"></a>Beheer

**V:** wat gebeurt er wanneer ik schakelaar Hallo opnieuw opstarten in hello Azure-portal?

**A:** dit is Hallo gelijkwaardige Docker opnieuw wordt gestart.

**V:** kan ik Secure Shell (SSH) tooconnect toohello app container virtuele machine (VM) gebruiken?

**A:** Ja, kunt u doen via Hallo SCM-site, artikel selectievakje Hallo volgende voor meer informatie [SSH-ondersteuning voor Web-App op Linux](./app-service-linux-ssh-support.md)

**V:** wil toocreate een Linux-App Service-vlak via SDK of een ARM-sjabloon, hoe kan ik dit bereikt?

**A:** moet u tooset hello `reserved` veld van het Hallo-app service te`true`.

## <a name="continuous-integrationdeployment"></a>Continue integratie/implementatie

**V:** mijn web-app nog steeds de installatiekopie van een oude Docker-container wordt gebruikt nadat ik Hallo-installatiekopie op Docker-Hub hebt bijgewerkt. Continue integratie/implementatie van aangepaste containers ondersteund?

**A:** tooset up continue integratie/implementatie voor installatiekopieën van het register van de Azure-Container of DockerHub door selectievakje Hallo volgende artikel [continue implementatie met de Azure-Web-App op Linux](./app-service-linux-ci-cd.md). U kunt voor persoonlijke registers Hallo container vernieuwen te stoppen en vervolgens uw web-app te starten. Of u kunt wijzigen of toevoegen van een dummy toepassingsinstelling tooforce een vernieuwing van de container.

**V:** ondersteunen testomgevingen?

**A:** Ja.

**V:** kan ik gebruiken **webimplementatie** toodeploy mijn web-app?

**A:** Ja, moet u tooset een app instelling `WEBSITE_WEBDEPLOY_USE_SCM` te`false`.

## <a name="language-support"></a>Taalondersteuning

**V:** bieden u ondersteuning voor niet-gecompileerde .NET Core apps?

**A:** Ja.

**V:** u ondersteunen Composer als een afhankelijkheid manager voor PHP-apps?

**A:** Ja. Tijdens een Git-implementatie moet Kudu detecteren die u een PHP-toepassing (met vriendelijke groet toohello aanwezigheid van een composer.json-bestand implementeert) en een installatie composer geactiveerd voor u.

## <a name="custom-containers"></a>Aangepaste containers

**V:** ik mijn eigen aangepaste container gebruik. Mijn app bevindt zich in Hallo `\home\` directory, maar ik kan mijn bestanden vinden wanneer ik Hallo inhoud bladeren met behulp van Hallo [SCM site](https://github.com/projectkudu/kudu) of een FTP-client. Waar bevinden zich mijn bestanden?

**A:** We een SMB-share toohello koppelen `\home\` directory. Hierdoor wordt de inhoud die is er overschreven.

**V:** ik mijn eigen aangepaste container gebruik. Ik wil niet Hallo platform toomount een SMB-share toohello `\home\`.

**A:** u kunt dit doen door de instelling Hallo `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app instellen te`false`.

**V:** Mijn aangepaste container neemt een toostart lang en Hallo platform herstart Hallo container voordat deze is voltooid wordt opgestart.

**A:** kunt u Hallo lang Hallo platform wachten moet voordat u de container opnieuw configureren. Dit kan worden gedaan door de instelling Hallo `WEBSITES_CONTAINER_START_TIME_LIMIT` app instelling toohello gewenste waarde in seconden. Hallo standaardwaarde is 230 seconden en Hallo max is 600 seconden.

**V:** wat Hallo-indeling voor persoonlijke register server-url is?

**A:** u nodig hebt tooprovide Hallo volledige register url inclusief `http://` of `https://`.

**V:** wat Hallo-indeling voor Hallo installatiekopie met de naam in de optie persoonlijke register is?

**A:** moet u tooadd Hallo volledige installatiekopie met de naam waaronder Hallo persoonlijke register url (bv. myacr.azurecr.IO/DotNet:Latest)

**V:** ik wil tooexpose meer dan één poort op de installatiekopie van mijn aangepaste container. Is dit mogelijk?

**A:** momenteel, die niet wordt ondersteund.

**V:** kan ik mijn eigen opslag brengen?

**A:** momenteel die niet wordt ondersteund.

**V:** ik kan mijn aangepaste container bestand system of actief processen van Hallo SCM site niet doorzoeken. Waarom is dat?

**A:** Hallo SCM site wordt uitgevoerd in een afzonderlijke container. Hallo-bestandssysteem kan niet worden gecontroleerd of het uitvoeren van processen van Hallo app-container.

**V:** Mijn aangepaste container luistert tooa andere poort dan poort 80. Hoe kan ik mijn app tooroute Hallo aanvragen toothat poort configureren?

**A:** hebben We automatische poortdetectie, ook kunt u een toepassing instelling opgeven **WEBSITES_PORT**, en geeft u het Hallo-waarde van het poortnummer Hallo verwacht. Eerder Hallo platform werd gebruikt `PORT` app instelt, we van plan bent toodeprecate Hallo Gebruik deze app instellen en verplaatsen toousing `WEBSITES_PORT` uitsluitend.

**V:** moet ik tooimplement HTTPS in Mijn aangepaste container.

**A:** Nee, Hallo platform HTTPS-beëindiging op Hallo gedeeld frontends verwerkt.

## <a name="pricing-and-sla"></a>Prijzen en SLA

**V:** wat wordt Hallo prijzen terwijl u de openbare preview Hallo?

**A:** u kosten in rekening gebracht half Hallo aantal uren dat uw app wordt uitgevoerd, met prijzen Hallo normale Azure App Service. Dit betekent dat u een korting van 50 procent op normale prijzen van Azure App Service krijgt.

## <a name="other"></a>Overige

**V:** wat Hallo ondersteund tekens in namen van de instellingen van toepassing zijn?

**A:** u kunt alleen A-Z, a-z, 0-9 gebruiken en Hallo onderstrepingsteken voor toepassingsinstellingen.

**V:** waar kan ik nieuwe functies aanvragen?

**A:** dient u uw idee op Hallo [forum met feedback van Web-Apps](https://aka.ms/webapps-uservoice). '[Linux]' toohello titel van uw idee toevoegen.

## <a name="next-steps"></a>Volgende stappen
* [Wat is Azure-Web-App op Linux?](app-service-linux-intro.md)
* [SSH-ondersteuning voor Azure-Web-App op Linux](./app-service-linux-ssh-support.md)
* [Faseringsomgevingen in Azure App Service instellen](./web-sites-staged-publishing.md)
* [Continue implementatie met Azure-Web-App op Linux](./app-service-linux-ci-cd.md)
