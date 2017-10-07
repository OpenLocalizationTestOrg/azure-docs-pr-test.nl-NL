---
title: aaaMonitor Azure DC/OS-cluster - Operations Management | Microsoft Docs
description: Een Azure Container Service DC/OS-cluster met de Microsoft Operations Management Suite bewaken.
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a>Monitor voor een Azure Container Service DC/OS-cluster met Operations Management Suite

Microsoft Operations Management Suite (OMS) is een cloudoplossing voor IT-beheer van Microsoft waarmee u uw on-premises en cloudinfrastructuur kunt beheren en beveiligen. Container oplossing is een oplossing in OMS Log Analytics, waardoor u inventaris weergeven Hallo-container, prestaties en logboeken op één locatie. U kunt controleren, containers oplossen door bekijkt hello Logboeken in de centrale locatie en veel ruis veroorzaken verbruikt overtollige container op een host vinden.

![](media/container-service-monitoring-oms/image1.png)

Raadpleeg voor meer informatie over de oplossing Container toothe [Container oplossing Log Analytics](../../log-analytics/log-analytics-containers.md).

## <a name="setting-up-oms-from-hello-dcos-universe"></a>Instellen van OMS uit Hallo DC/OS universe


In dit artikel wordt ervan uitgegaan dat u een DC/OS hebt ingesteld en eenvoudige web containertoepassingen op Hallo cluster hebt geïmplementeerd.

### <a name="pre-requisite"></a>Vereiste
- [Microsoft Azure-abonnement](https://azure.microsoft.com/free/) -u kunt dit gratis ophalen.  
- Setup van Microsoft OMS-werkruimte - Zie 'Stap 3' hieronder
- [DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) geïnstalleerd.

1. Hallo DC/OS-dashboard, klik op Universe en zoek naar OMS zoals hieronder wordt weergegeven.

![](media/container-service-monitoring-oms/image2.png)

2. Klik op **Install**. U ziet een pop up met Hallo OMS versie-informatie en een **pakket installeren** of **installatie in de geavanceerde** knop. Wanneer u klikt op **installatie in de geavanceerde**, die leidt u toohello **OMS specifieke configuratie-eigenschappen** pagina.

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. Hier wordt u gevraagd tooenter hello `wsid` (Hallo OMS-werkruimte-ID) en `wskey` (Hallo OMS primaire sleutel voor Hallo werkruimte-id). beide tooget `wsid` en `wskey` u toocreate moet een OMS-account bij <https://mms.microsoft.com>. Volg Hallo stappen toocreate een account. Wanneer u klaar bent met het Hallo-account maken, moet u tooobtain uw `wsid` en `wskey` door te klikken op **instellingen**, klikt u vervolgens **verbonden bronnen**, en vervolgens **Linux-Servers** , zoals hieronder weergegeven.

 ![](media/container-service-monitoring-oms/image5.png)

4. Hallo nummer u OMS exemplaren selecteren dat u wilt en klik op de knop 'Bekijken en installeren' Hallo. Meestal zult u toohave Hallo aantal OMS exemplaren gelijk toohello van de virtuele machine hebt u in uw cluster agent. OMS-Agent voor Linux is geïnstalleerd als afzonderlijke containers op elke VM die deze wil toocollect informatie voor de controle en logboekregistratie.

## <a name="setting-up-a-simple-oms-dashboard"></a>Instellen van een eenvoudige OMS-dashboard

Zodra u Hallo OMS-Agent voor Linux op Hallo virtuele machines hebt geïnstalleerd, wordt in het volgende stap tooset up Hallo OMS dashboard is. Er zijn van twee manieren toodo dit: OMS-Portal of Azure-Portal.

### <a name="oms-portal"></a>OMS-Portal 

Meld u bij toohello OMS-portal (<https://mms.microsoft.com>) en ga toohello **oplossing galerie**.

![](media/container-service-monitoring-oms/image6.png)

Wanneer u naar Hallo **oplossing galerie**, selecteer **Containers**.

![](media/container-service-monitoring-oms/image7.png)

Wanneer u Hallo Container oplossing hebt geselecteerd, worden er Hallo tegel op Hallo OMS overzicht dashboardpagina. Nadat de containergegevens Hallo ingenomen is geïndexeerd, ziet u Hallo tegel ingevuld met informatie over de oplossing weergeven tegels.

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a>Azure Portal 

Aanmelding tooAzure portal op <https://portal.microsoft.com/>. Ga naar **Marketplace**, selecteer **bewaking + management** en klik op **alle Zie**. Typ vervolgens `containers` in de zoekopdracht. U ziet in de zoekresultaten Hallo ' containers'. Selecteer **Containers** en klik op **maken**.

![](media/container-service-monitoring-oms/image9.png)

Nadat u op **maken**, wordt u gevraagt voor uw werkruimte. Selecteer uw werkruimte of als u geen abonnement hebt, maakt u een nieuwe werkruimte.

![](media/container-service-monitoring-oms/image10.PNG)

Nadat u uw werkruimte hebt geselecteerd, klikt u op **maken**.

![](media/container-service-monitoring-oms/image11.png)

Raadpleeg voor meer informatie over Hallo OMS Container oplossing toothe [Container oplossing Log Analytics](../../log-analytics/log-analytics-containers.md).

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a>Hoe tooscale OMS-Agent met ACS DC/OS 

Als u toohave geïnstalleerd OMS-agent niet genoeg Hallo werkelijke infrastructuurmanifest moet of u VMSS zijn schaalt door meer VM toe te voegen, kunt u doen door te schalen Hallo `msoms` service.

Ga tooMarathon of Hallo Services voor DC/OS-gebruikersinterface tabblad en het aantal knooppunten opschalen.

![](media/container-service-monitoring-oms/image12.PNG)

Hiermee implementeert u tooother knooppunten die nog niet zijn geïmplementeerd op Hallo OMS-agent.

## <a name="uninstall-ms-oms"></a>MS OMS verwijderen

toouninstall MS OMS Voer Hallo volgende opdracht:

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a>Laat ons weten.
Wat werkt? Wat ontbreekt? Wat kan er anders moet u voor deze toobe nuttig voor u? Laat ons weten op <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.

## <a name="next-steps"></a>Volgende stappen

 Nu dat u hebt ingesteld OMS toomonitor uw containers[uw dashboard container zien](../../log-analytics/log-analytics-containers.md).
