---
title: Implementatie met de Azure-Web-App op Linux aaaContinuous | Microsoft Docs
description: Hoe toosetup continue implementatie in Azure-Web-App op Linux.
keywords: Azure app service, linux, besturingssystemen, acr
services: app-service
documentationcenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: f94d837e27605da58428f507ab2b0eb3af3297e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a>Continue implementatie met de Azure-Web-App op Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

In deze zelfstudie configureert u continue implementatie voor de installatiekopie van een aangepaste container van beheerde [Azure Container register](https://azure.microsoft.com/en-us/services/container-registry/) opslagplaatsen of [Docker Hub](https://hub.docker.com).

## <a name="step-1---sign-in-tooazure"></a>Stap 1: aanmelden tooAzure

Meld u aan toohello Azure-portal op http://portal.azure.com

## <a name="step-2---enable-container-continuous-deployment-feature"></a>Stap 2: de functie voor container continue implementatie inschakelen

U kunt inschakelen Hallo continue implementatie functie gebruik [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) en Hallo volgende opdracht uitvoeren

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

In Hallo  **[Azure-portal](https://portal.azure.com/)**, klikt u op Hallo **App Service** optie op Hallo links van het Hallo-pagina.

Klik op het Hallo-naam van de app die u wilt tooconfigure Docker Hub continue implementatie voor.

In Hallo **appinstellingen**, een instelling app toevoegen `DOCKER_ENABLE_CI` met Hallo waarde `true`.

![afbeelding van app-instelling worden ingevoegd](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a>Stap 3: het voorbereiden van de Webhook-URL

U kunt verkrijgen Hallo Webhook-URL met behulp van [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) en Hallo volgende opdracht uitvoeren

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

Hallo Webhook-URL, moet u toohave Hallo eindpunt te volgen: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.

Kunt u uw `publishingusername` en `publishingpwd` Hallo web-app downloaden publicatieprofiel met hello Azure-portal.

![afbeelding van het toevoegen van de webhook 2 invoegen](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a>Stap 4: een web-haakje toevoegen

### <a name="azure-container-registry"></a>Azure Container Registry

Klik op de portalblade van register **Webhooks**, maak een nieuwe webhook door te klikken **toevoegen**. In Hallo **webhook maken** blade een naam voor uw webhook geven. Hallo Webhook URI, moet u tooprovide Hallo URL verkregen van **stap 3**

Zorg ervoor dat Hallo bereik te definiëren, zoals Hallo opslagplaats met de installatiekopie van de container.

![afbeelding van de webhook invoegen](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

Wanneer het Hallo-installatiekopie wordt bijgewerkt, Hallo web-app automatisch bijgewerkt met de nieuwe installatiekopie Hallo.

### <a name="docker-hub"></a>Docker-Hub

Klik op de pagina Docker Hub **Webhooks**, vervolgens **maken van een WEBHOOK**.

![afbeelding van het toevoegen van de webhook 1 invoegen](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

Hallo Webhook-URL, moet u tooprovide Hallo URL verkregen van **stap 3**

![afbeelding van het toevoegen van de webhook 2 invoegen](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

Wanneer het Hallo-installatiekopie wordt bijgewerkt, Hallo web-app automatisch bijgewerkt met de nieuwe installatiekopie Hallo.

## <a name="next-steps"></a>Volgende stappen
* [Wat is Azure-Web-App op Linux?](./app-service-linux-intro.md)
* [Azure-Container register](https://azure.microsoft.com/en-us/services/container-registry/)
* [Met behulp van PM2-configuratie voor Node.js in Azure-Web-App op Linux](app-service-linux-using-nodejs-pm2.md)
* [Met behulp van .NET Core in Azure-Web-App op Linux](app-service-linux-using-dotnetcore.md)
* [Met behulp van Ruby in Azure-Web-App op Linux](app-service-linux-ruby-get-started.md)
* [Hoe een installatiekopie van een aangepaste Docker toouse voor Azure-Web-App op Linux](./app-service-linux-using-custom-docker-image.md)
* [Web-App op Linux Veelgestelde vragen over Azure App Service](./app-service-linux-faq.md) 
* [Web-App beheren op Linux met Azure CLI 2.0](./app-service-linux-cli.md)



