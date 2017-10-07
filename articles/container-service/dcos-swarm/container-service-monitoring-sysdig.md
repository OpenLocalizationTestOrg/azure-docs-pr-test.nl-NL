---
title: aaaMonitor een Azure Container Service-cluster met Sysdig | Microsoft Docs
description: Een Azure Container Service-cluster met Sysdig bewaken.
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Containers, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a>Een Azure Container Service-cluster met Sysdig bewaken
In dit artikel implementeert we Sysdig agents tooall Hallo agent knooppunten in uw Azure Container Service-cluster. Voor deze configuratie hebt u een Sysdig-account nodig. 

## <a name="prerequisites"></a>Vereisten
[Implementeer](container-service-deployment.md) en [verbind](../container-service-connect.md) een cluster dat door Azure Container Service is geconfigureerd. Hallo verkennen [Marathon-gebruikersinterface](container-service-mesos-marathon-ui.md). Ga te[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset van een Sysdig cloud-account. 

## <a name="sysdig"></a>Sysdig
Sysdig is een monitoring-service waarmee u toomonitor uw containers in uw cluster. Sysdig toohelp op te lossen is bekend maar heeft ook uw bewaking basismetrieken voor CPU, netwerken, geheugen en i/o. Sysdig maakt het eenvoudig toosee welke containers werkt Hallo hardest of in wezen met Hallo meeste geheugen en CPU. Deze weergave wordt Hallo sectie 'Overzicht', die momenteel in de bètaversie. 

![Gebruikersinterface van Sysdig](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a>Een Sysdig-implementatie met Marathon configureren
Deze stappen wordt uitgelegd hoe u tooconfigure en implementeren van Sysdig toepassingen tooyour cluster met Marathon. 

Toegang tot uw DC/OS-Webgebruikersinterface via [http://localhost:80 /](http://localhost:80/) Navigeer eenmaal in Hallo DC/OS-Webgebruikersinterface toohello 'Universe', die zich op Hallo onderste links en zoek naar 'Sysdig'.

![Sysdig in het DC/OS-universum](./media/container-service-monitoring-sysdig/sysdig1.png)

Nu toocomplete Hallo-configuratie moet u een Sysdig cloud-account of een gratis proefaccount. Nadat u bent aangemeld op toohello Sysdig cloud website, klikt u op uw gebruikersnaam en op de pagina Hallo ziet u uw 'toegangssleutel'. 

![Sysdig API-sleutel](./media/container-service-monitoring-sysdig/sysdig2.png) 

Naast uw toegangssleutel in Hallo Sysdig configuratie binnen Hallo DC/OS Universe invoeren. 

![Configuratie van de Sysdig in Hallo DC/OS Universe](./media/container-service-monitoring-sysdig/sysdig3.png)

Nu Hallo exemplaren too10000000 zodanig instellen wanneer er een nieuw knooppunt wordt toegevoegd toohello cluster Sysdig automatisch een agent implementeren toothat nieuw knooppunt. Dit is een tijdelijke oplossing toomake ervoor dat sysdig tooall nieuwe agents binnen Hallo cluster gaat implementeren. 

![Configuratie van de Sysdig in Hallo DC/OS Universe-exemplaren](./media/container-service-monitoring-sysdig/sysdig4.png)

Zodra u Hallo pakket hebt geïnstalleerd Navigeer terug toohello Sysdig UI en u zult kunnen tooexplore Hallo verschillende gebruik metrische gegevens voor Hallo containers in uw cluster. 

U kunt ook Mesos- en Marathon-specifieke dashboards installeren via de [wizard Nieuw dashboard](https://app.sysdigcloud.com/#/dashboards/new).
