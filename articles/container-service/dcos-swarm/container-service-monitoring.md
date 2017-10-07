---
title: aaaMonitor Azure DC/OS-cluster - Datadog | Microsoft Docs
description: Een Azure Container Service-cluster met Datadog bewaken. Hallo DC/OS web UI toodeploy hello Datadog agents tooyour cluster gebruiken.
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Containers, DC/OS Docker Swarm-Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a>Een Azure Container Service DC/OS-cluster met Datadog bewaken
In dit artikel implementeert we Datadog agents tooall Hallo agent knooppunten in uw Azure Container Service-cluster. U moet een account met Datadog voor deze configuratie. 

## <a name="prerequisites"></a>Vereisten
[Implementeer](container-service-deployment.md) en [verbind](../container-service-connect.md) een cluster dat door Azure Container Service is geconfigureerd. Hallo verkennen [Marathon-gebruikersinterface](container-service-mesos-marathon-ui.md). Ga te[http://datadoghq.com](http://datadoghq.com) tooset van een Datadog-account. 

## <a name="datadog"></a>Datadog
Datadog is een controleservice die bewakingsgegevens moeten worden verzameld uit uw containers in uw Azure Container Service-cluster. Datadog heeft een Docker-integratie Dashboard waarin u de specifieke metrische gegevens binnen uw containers kunt zien. Metrische gegevens die afkomstig zijn van uw containers worden ingedeeld op basis van CPU, geheugen, netwerk en i/o. Datadog splitst metrische gegevens in containers en afbeeldingen. Een voorbeeld van welke Hallo UI lijkt erop dat voor CPU-gebruik hieronder is.

![Datadog gebruikersinterface](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a>Een implementatie met Datadog met Marathon configureren
Deze stappen wordt uitgelegd hoe u tooconfigure en implementeren van Datadog toepassingen tooyour cluster met Marathon. 

Toegang tot uw DC/OS-Webgebruikersinterface via [http://localhost:80 /](http://localhost:80/). Eenmaal in DC/OS-Webgebruikersinterface Navigeer Hallo toohello 'Universe' die op Hallo is onderste links en zoek naar 'Datadog' en op 'Installeren'.

![Datadog pakket binnen Hallo DC/OS Universe](./media/container-service-monitoring/datadog1.png)

Nu toocomplete Hallo configuratie moet u een account Datadog of een gratis proefaccount. Nadat u bent aangemeld Zoek toohello links in toohello Datadog website en ga vervolgens door tooIntegrations -> [API's](https://app.datadoghq.com/account/settings#api). 

![Datadog API-sleutel](./media/container-service-monitoring/datadog2.png)

Naast uw API-sleutel in Hallo Datadog configuratie binnen Hallo DC/OS Universe invoeren. 

![Configuratie van de Datadog in Hallo DC/OS Universe](./media/container-service-monitoring/datadog3.png) 

In Hallo hierboven configuratie exemplaren too10000000 ingesteld zodat wanneer een nieuw knooppunt wordt toegevoegd toohello cluster Datadog een agent toothat knooppunt automatisch implementeren. Dit is een tijdelijke oplossing. Zodra u Hallo pakket hebt geïnstalleerd moet u navigeren back toohello Datadog website en vinden '[Dashboards](https://app.datadoghq.com/dash/list). " Daar ziet u aangepaste en integratie-Dashboards. Hallo [Docker-dashboard](https://app.datadoghq.com/screen/integration/docker) hebben alle Hallo container metrische gegevens u moet voor het bewaken van uw cluster. 

