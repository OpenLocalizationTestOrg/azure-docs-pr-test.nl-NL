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
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a><span data-ttu-id="98b7d-105">Een Azure Container Service DC/OS-cluster met Dynatrace SaaS/beheerde bewaken</span><span class="sxs-lookup"><span data-stu-id="98b7d-105">Monitor an Azure Container Service DC/OS cluster with Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="98b7d-106">In dit artikel wordt uitgelegd hoe u dat toodeploy hello [Dynatrace](https://www.dynatrace.com/) OneAgent toomonitor alle Hallo agent knooppunten in uw Azure Container Service-cluster.</span><span class="sxs-lookup"><span data-stu-id="98b7d-106">In this article, we show you how toodeploy hello [Dynatrace](https://www.dynatrace.com/) OneAgent toomonitor all hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="98b7d-107">Voor deze configuratie moet u een account met Dynatrace SaaS/beheerd.</span><span class="sxs-lookup"><span data-stu-id="98b7d-107">You need an account with Dynatrace SaaS/Managed for this configuration.</span></span> 

## <a name="dynatrace-saasmanaged"></a><span data-ttu-id="98b7d-108">SaaS Dynatrace/beheerd</span><span class="sxs-lookup"><span data-stu-id="98b7d-108">Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="98b7d-109">Dynatrace is een oplossing voor cloud-systeemeigen controle voor maximaal dynamische container en cluster-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="98b7d-109">Dynatrace is a cloud-native monitoring solution for highly dynamic container and cluster environments.</span></span> <span data-ttu-id="98b7d-110">Hiermee kunt u toobetter uw containerimplementaties en geheugentoewijzingen optimaliseren door van realtime-gebruiksgegevens.</span><span class="sxs-lookup"><span data-stu-id="98b7d-110">It allows you toobetter optimize your container deployments and memory allocations by using real-time usage data.</span></span> <span data-ttu-id="98b7d-111">Het is geschikt voor toepassingen en infrastructuur problemen automatisch dicht door geautomatiseerde basislijnen, probleem correlatie en detectie van de hoofdoorzaak te geven.</span><span class="sxs-lookup"><span data-stu-id="98b7d-111">It is capable of automatically pinpointing application and infrastructure issues by providing automated baselining, problem correlation, and root-cause detection.</span></span>

<span data-ttu-id="98b7d-112">Hallo volgende afbeelding toont Hallo Dynatrace UI:</span><span class="sxs-lookup"><span data-stu-id="98b7d-112">hello following figure shows hello Dynatrace UI:</span></span>

![Dynatrace gebruikersinterface](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a><span data-ttu-id="98b7d-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="98b7d-114">Prerequisites</span></span> 
<span data-ttu-id="98b7d-115">[Implementeer](container-service-deployment.md) en [verbinding](./../container-service-connect.md) tooa cluster geconfigureerd door Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="98b7d-115">[Deploy](container-service-deployment.md) and [connect](./../container-service-connect.md) tooa cluster configured by Azure Container Service.</span></span> <span data-ttu-id="98b7d-116">Hallo verkennen [Marathon-gebruikersinterface](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="98b7d-116">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="98b7d-117">Ga te[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset van een Dynatrace SaaS-account.</span><span class="sxs-lookup"><span data-stu-id="98b7d-117">Go too[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset up a Dynatrace SaaS account.</span></span>  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a><span data-ttu-id="98b7d-118">Een implementatie met Dynatrace met Marathon configureren</span><span class="sxs-lookup"><span data-stu-id="98b7d-118">Configure a Dynatrace deployment with Marathon</span></span>
<span data-ttu-id="98b7d-119">Deze stappen ziet u hoe tooconfigure en implementeren van Dynatrace toepassingen tooyour cluster met Marathon.</span><span class="sxs-lookup"><span data-stu-id="98b7d-119">These steps show you how tooconfigure and deploy Dynatrace applications tooyour cluster with Marathon.</span></span>

1. <span data-ttu-id="98b7d-120">Toegang tot uw DC/OS-Webgebruikersinterface via [http://localhost:80 /](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="98b7d-120">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="98b7d-121">Navigeer eenmaal in Hallo DC/OS-Webgebruikersinterface, toohello **Universe** tabblad en zoek vervolgens naar **Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="98b7d-121">Once in hello DC/OS UI, navigate toohello **Universe** tab and then search for **Dynatrace**.</span></span>

    ![Dynatrace in DC/OS Universe](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. <span data-ttu-id="98b7d-123">toocomplete hello configuratie, moet u een Dynatrace SaaS-account of een gratis proefaccount.</span><span class="sxs-lookup"><span data-stu-id="98b7d-123">toocomplete hello configuration, you need a Dynatrace SaaS account or a free trial account.</span></span> <span data-ttu-id="98b7d-124">Zodra u zich bij Hallo Dynatrace dashboard aanmeldt, selecteert u **Dynatrace implementeren**.</span><span class="sxs-lookup"><span data-stu-id="98b7d-124">Once you log into hello Dynatrace dashboard, select **Deploy Dynatrace**.</span></span>

    ![Dynatrace PaaS-integratie instellen](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. <span data-ttu-id="98b7d-126">Selecteer op de pagina Hallo **PaaS-integratie instellen**.</span><span class="sxs-lookup"><span data-stu-id="98b7d-126">On hello page, select **Set up PaaS integration**.</span></span> 

    ![Dynatrace API-token](./media/container-service-monitoring-dynatrace/api-token.png) 

4. <span data-ttu-id="98b7d-128">Uw API-token in Hallo Dynatrace OneAgent configuratie binnen Hallo DC/OS Universe invoeren.</span><span class="sxs-lookup"><span data-stu-id="98b7d-128">Enter your API token into hello Dynatrace OneAgent configuration within hello DC/OS Universe.</span></span> 

    ![Configuratie van Dynatrace OneAgent in Hallo DC/OS Universe](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. <span data-ttu-id="98b7d-130">Hallo exemplaren toohello aantal instellen van knooppunten u van plan bent toorun.</span><span class="sxs-lookup"><span data-stu-id="98b7d-130">Set hello instances toohello number of nodes you intend toorun.</span></span> <span data-ttu-id="98b7d-131">Hoe hoger de waarde ook werkt, maar de DC/OS zal blijven proberen toofind nieuwe exemplaren totdat dit aantal is bereikt.</span><span class="sxs-lookup"><span data-stu-id="98b7d-131">Setting a higher number also works, but DC/OS will keep trying toofind new instances until that number is actually reached.</span></span> <span data-ttu-id="98b7d-132">Als u liever, kunt u ook deze waarde tooa zoals 1000000 instellen.</span><span class="sxs-lookup"><span data-stu-id="98b7d-132">If you prefer, you can also set this tooa value like 1000000.</span></span> <span data-ttu-id="98b7d-133">In dit geval, wanneer een nieuw knooppunt wordt toohello cluster worden toegevoegd, implementeert Dynatrace automatisch een agent toothat nieuw knooppunt voor Hallo prijs van een DC/OS voortdurend probeert toodeploy exemplaren.</span><span class="sxs-lookup"><span data-stu-id="98b7d-133">In this case, whenever a new node is added toohello cluster, Dynatrace automatically deploys an agent toothat new node, at hello price of DC/OS constantly trying toodeploy further instances.</span></span>

    ![Configuratie van de Dynatrace in Hallo DC/OS Universe-exemplaren](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a><span data-ttu-id="98b7d-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="98b7d-135">Next steps</span></span>

<span data-ttu-id="98b7d-136">Nadat u Hallo pakket hebt geïnstalleerd, gaat u terug toohello Dynatrace dashboard.</span><span class="sxs-lookup"><span data-stu-id="98b7d-136">Once you've installed hello package, navigate back toohello Dynatrace dashboard.</span></span> <span data-ttu-id="98b7d-137">Hallo verschillende gebruik metrische gegevens voor Hallo containers vindt u in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="98b7d-137">You can explore hello different usage metrics for hello containers within your cluster.</span></span> 
