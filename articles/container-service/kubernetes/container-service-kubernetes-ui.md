---
title: aaaManage Azure Kubernetes cluster met de webgebruikersinterface | Microsoft Docs
description: Met behulp van Hallo Kubernetes-webgebruikersinterface in Azure Container Service
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a>Met behulp van Hallo Kubernetes-webgebruikersinterface met Azure Container Service

## <a name="prerequisites"></a>Vereisten
In dit scenario wordt ervan uitgegaan dat u hebt [gemaakt van een Kubernetes-cluster met behulp van Azure Container Service](container-service-kubernetes-walkthrough.md).


Ook wordt ervan uitgegaan dat u hello Azure CLI 2.0 hebt en `kubectl` hulpprogramma's geïnstalleerd.

U kunt testen, hebt u Hallo `az` hulpprogramma is geïnstalleerd door te voeren:

```console
$ az --version
```

Als u geen Hallo `az` hulpprogramma is geïnstalleerd, er zijn instructies [hier](https://github.com/azure/azure-cli#installation).

U kunt testen, hebt u Hallo `kubectl` hulpprogramma is geïnstalleerd door te voeren:

```console
$ kubectl version
```

Als u geen `kubectl` geïnstalleerd, u kunt uitvoeren:

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a>Overzicht

### <a name="connect-toohello-web-ui"></a>Verbinding maken met toohello webgebruikersinterface
U kunt Hallo Kubernetes webgebruikersinterface starten door te voeren:

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

Dit moet een browser geconfigureerd tootalk tooa beveiligde webproxy verbinding maken met uw lokale machine toohello Kubernetes webgebruikersinterface openen.

### <a name="create-and-expose-a-service"></a>Maken en weergeven van een service
1. Klik in het Hallo Kubernetes web UI op **maken** knop in het bovenste rechtervenster Hallo.

    ![Kubernetes maken gebruikersinterface](./media/container-service-kubernetes-ui/create.png)

    Een dialoogvenster weergegeven waarin u kunt starten maken van de toepassing.

2. Geef het Hallo-naam `hello-nginx`. Gebruik Hallo [ `nginx` container in Docker](https://hub.docker.com/_/nginx/) en drie replica's van deze webservice implementeren.

    ![Dialoogvenster maken Kubernetes schil](./media/container-service-kubernetes-ui/nginx.png)

3. Onder **Service**, selecteer **externe** en voert u poort 80.

    Deze instelling taakverdelingen verkeer toohello drie replica's.

    ![Dialoogvenster maken Kubernetes Service](./media/container-service-kubernetes-ui/service.png)

4. Klik op **implementeren** toodeploy deze containers en -services.

    ![Kubernetes implementeren](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a>Uw containers weergeven
Nadat u op **implementeren**, Hallo UI ziet u een weergave van uw service zoals deze implementeert:

![Kubernetes Status](./media/container-service-kubernetes-ui/status.png)

Kunt u Hallo status van elk object Kubernetes in Hallo cirkel onder aan de linkerkant Hallo van de gebruikersinterface bekijken **gehele product**. Als het een gedeeltelijk volledige cirkel, is nog steeds Hallo object implementeren. Wanneer een object volledig is geïmplementeerd, wordt een groen vinkje weergegeven:

![Kubernetes geïmplementeerd](./media/container-service-kubernetes-ui/deployed.png)

Zodra u alles wordt uitgevoerd, klikt u op een van uw gehele product toosee details over het Hallo-webservice wordt uitgevoerd.

![Kubernetes gehele product](./media/container-service-kubernetes-ui/pods.png)

In Hallo **gehele product** weergave ziet u informatie over het Hallo-containers in Hallo schil, evenals Hallo CPU en geheugenbronnen kost gebruikt door deze containers:

![Kubernetes Resources](./media/container-service-kubernetes-ui/resources.png)

Als u Hallo resources niet ziet, moet u mogelijk toowait een paar minuten voor Hallo gegevens toopropagate bewaking.

toosee hello logboeken voor de container, klik **logboeken bekijken**.

![Kubernetes Logboeken](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a>Uw service weergeven
In aanvulling toorunning uw containers Hallo Kubernetes UI heeft gemaakt een externe `Service` die voorziet in een load balancer toobring verkeer toohello containers in uw cluster.

Klik in het Hallo navigatiedeelvenster links op **Services** tooview alle services (er moet slechts één).

![Kubernetes Services](./media/container-service-kubernetes-ui/service-deployed.png)

In deze weergave ziet u een extern eindpunt (IP-adres) tooyour-service is toegewezen.
Als u op dat IP-adres, ziet u het Nginx-container die achter de load balancer.

![nginx weergeven](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a>Uw service vergroten of verkleinen
In toevoeging tooviewing Hallo uw objecten in de gebruikersinterface, kunt u bewerken en bijwerken Hallo Kubernetes API-objecten.

Klik eerst **implementaties** in Hallo links navigatie deelvenster toosee Hallo implementatie voor uw service.

Wanneer u zich in die weergave, klikt u op Hallo replicaset en klik vervolgens op **bewerken** in de bovenste navigatiebalk Hallo:

![Kubernetes bewerken](./media/container-service-kubernetes-ui/edit.png)

Hallo bewerken `spec.replicas` veld toobe `2`, en klik op **Update**.

Dit zorgt ervoor dat het aantal replica's toodrop tootwo Hallo door een van uw gehele product te verwijderen.

 

