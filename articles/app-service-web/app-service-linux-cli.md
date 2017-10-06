---
title: Web-App op Linux met Azure CLI 2.0 aaaManage | Microsoft Docs
description: Web-App beheren op Linux met Azure CLI.
keywords: Azure app service, web-app, cli, linux, oss
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
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 5e8e0da8a362450c56d2e87e087f77598ec874ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a>Web-App beheren op Linux met Azure CLI

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

Hallo-opdrachten gebruiken in dit artikel u kunnen toocreate en beheren van een Web-App op Linux met Azure CLI 2.0.
U kunt starten met de nieuwe versie Hallo Hallo CLI op twee manieren:

* [Installatie van Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) op uw computer.
* Met behulp van [Azure-Cloud-Shell (Preview)](../cloud-shell/overview.md)


## <a name="create-a-linux-app-service-plan"></a>Een Linux-App Service-abonnement maken

toocreate een Linux-App Service-Plan, kunt u Hallo volgende opdracht gebruiken:

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a>Een aangepaste Docker-container Web-App maken

toocreate een web-app en het toorun aangepaste Docker-container te configureren, kunt u Hallo volgende opdracht:

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a>Hallo Docker-container logboekregistratie activeren

tooactivate Hallo Docker-container logboekregistratie, kunt u Hallo volgende opdracht:

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a>Hallo aangepaste Docker-container voor een bestaande Web-App op Linux-App wijzigen

toochange een eerder gemaakte-app vanuit Hallo huidige Docker installatiekopie tooa nieuwe installatiekopie, kunt u Hallo volgende opdracht gebruiken:

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a>Met behulp van Docker-installatiekopieën van een persoonlijke register

U kunt uw app toouse installatiekopieën van een persoonlijke register configureren. In dat geval moet u tooprovide Hallo url in voor uw register, gebruikersnaam en wachtwoord. Dit kan worden gerealiseerd met behulp van de volgende opdracht Hallo:

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a>Continue implementaties voor aangepaste Docker-images inschakelen

U kunt met de volgende opdracht Hallo Hallo CD functionaliteit inschakelen en Hallo webhook-url ophalen. Deze url gebruikte tooconfigure u DockerHub of Azure Container register repo's kan worden.

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a>Maken van een Web-App op Linux-App met een van onze frameworks ingebouwde runtime

een PHP-Web-App voor 5.6 op Linux-App waarmee, u kunt volgende opdracht Hallo toocreate.

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a>Framework-versie voor een bestaande Web-App op Linux-App wijzigen

toochange een eerder gemaakte-app van Hallo huidige framework-versie van het tooNode.js 6.11, kunt u Hallo volgende opdracht gebruiken:

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a>Git-implementaties voor uw Web-App instellen

tooset Git-implementaties voor uw app kunt u Hallo volgende opdracht gebruiken:

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a>Volgende stappen
* [Wat is Azure-Web-App op Linux?](app-service-linux-intro.md)
* [Installeer Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [Azure-Cloud-Shell (Preview)](../cloud-shell/overview.md)
* [Faseringsomgevingen in Azure App Service instellen](./web-sites-staged-publishing.md)
* [Continue implementatie met Azure-Web-App op Linux](./app-service-linux-ci-cd.md)
