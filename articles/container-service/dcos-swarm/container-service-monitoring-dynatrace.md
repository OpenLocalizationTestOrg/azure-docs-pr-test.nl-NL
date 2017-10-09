---
title: aaaMonitor Azure DC/OS-cluster - Dynatrace | Microsoft Docs
description: Een Azure Container Service DC/OS-cluster met Dynatrace bewaken. Hallo Dynatrace OneAgent implementeren met behulp van Hallo DC/OS-dashboard.
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: Containers, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 9e2e2d1c8b454422d1db30dac7c385d31d336853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a>Een Azure Container Service DC/OS-cluster met Dynatrace SaaS/beheerde bewaken
In dit artikel wordt uitgelegd hoe u dat toodeploy hello [Dynatrace](https://www.dynatrace.com/) OneAgent toomonitor alle Hallo agent knooppunten in uw Azure Container Service-cluster. Voor deze configuratie moet u een account met Dynatrace SaaS/beheerd. 

## <a name="dynatrace-saasmanaged"></a>SaaS Dynatrace/beheerd
Dynatrace is een oplossing voor cloud-systeemeigen controle voor maximaal dynamische container en cluster-omgevingen. Hiermee kunt u toobetter uw containerimplementaties en geheugentoewijzingen optimaliseren door van realtime-gebruiksgegevens. Het is geschikt voor toepassingen en infrastructuur problemen automatisch dicht door geautomatiseerde basislijnen, probleem correlatie en detectie van de hoofdoorzaak te geven.

Hallo volgende afbeelding toont Hallo Dynatrace UI:

![Dynatrace gebruikersinterface](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a>Vereisten 
[Implementeer](container-service-deployment.md) en [verbinding](./../container-service-connect.md) tooa cluster geconfigureerd door Azure Container Service. Hallo verkennen [Marathon-gebruikersinterface](container-service-mesos-marathon-ui.md). Ga te[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset van een Dynatrace SaaS-account.  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a>Een implementatie met Dynatrace met Marathon configureren
Deze stappen ziet u hoe tooconfigure en implementeren van Dynatrace toepassingen tooyour cluster met Marathon.

1. Toegang tot uw DC/OS-Webgebruikersinterface via [http://localhost:80 /](http://localhost:80/). Navigeer eenmaal in Hallo DC/OS-Webgebruikersinterface, toohello **Universe** tabblad en zoek vervolgens naar **Dynatrace**.

    ![Dynatrace in DC/OS Universe](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. toocomplete hello configuratie, moet u een Dynatrace SaaS-account of een gratis proefaccount. Zodra u zich bij Hallo Dynatrace dashboard aanmeldt, selecteert u **Dynatrace implementeren**.

    ![Dynatrace PaaS-integratie instellen](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. Selecteer op de pagina Hallo **PaaS-integratie instellen**. 

    ![Dynatrace API-token](./media/container-service-monitoring-dynatrace/api-token.png) 

4. Uw API-token in Hallo Dynatrace OneAgent configuratie binnen Hallo DC/OS Universe invoeren. 

    ![Configuratie van Dynatrace OneAgent in Hallo DC/OS Universe](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. Hallo exemplaren toohello aantal instellen van knooppunten u van plan bent toorun. Hoe hoger de waarde ook werkt, maar de DC/OS zal blijven proberen toofind nieuwe exemplaren totdat dit aantal is bereikt. Als u liever, kunt u ook deze waarde tooa zoals 1000000 instellen. In dit geval, wanneer een nieuw knooppunt wordt toohello cluster worden toegevoegd, implementeert Dynatrace automatisch een agent toothat nieuw knooppunt voor Hallo prijs van een DC/OS voortdurend probeert toodeploy exemplaren.

    ![Configuratie van de Dynatrace in Hallo DC/OS Universe-exemplaren](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a>Volgende stappen

Nadat u Hallo pakket hebt geïnstalleerd, gaat u terug toohello Dynatrace dashboard. Hallo verschillende gebruik metrische gegevens voor Hallo containers vindt u in uw cluster. 
