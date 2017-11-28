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
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a><span data-ttu-id="320af-104">Een Azure Container Service-cluster met Sysdig bewaken</span><span class="sxs-lookup"><span data-stu-id="320af-104">Monitor an Azure Container Service cluster with Sysdig</span></span>
<span data-ttu-id="320af-105">In dit artikel implementeert we Sysdig agents tooall Hallo agent knooppunten in uw Azure Container Service-cluster.</span><span class="sxs-lookup"><span data-stu-id="320af-105">In this article, we will deploy Sysdig agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="320af-106">Voor deze configuratie hebt u een Sysdig-account nodig.</span><span class="sxs-lookup"><span data-stu-id="320af-106">You need an account with Sysdig for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="320af-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="320af-107">Prerequisites</span></span>
<span data-ttu-id="320af-108">[Implementeer](container-service-deployment.md) en [verbind](../container-service-connect.md) een cluster dat door Azure Container Service is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="320af-108">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="320af-109">Hallo verkennen [Marathon-gebruikersinterface](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="320af-109">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="320af-110">Ga te[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset van een Sysdig cloud-account.</span><span class="sxs-lookup"><span data-stu-id="320af-110">Go too[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset up a Sysdig cloud account.</span></span> 

## <a name="sysdig"></a><span data-ttu-id="320af-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="320af-111">Sysdig</span></span>
<span data-ttu-id="320af-112">Sysdig is een monitoring-service waarmee u toomonitor uw containers in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="320af-112">Sysdig is a monitoring service that allows you toomonitor your containers within your cluster.</span></span> <span data-ttu-id="320af-113">Sysdig toohelp op te lossen is bekend maar heeft ook uw bewaking basismetrieken voor CPU, netwerken, geheugen en i/o.</span><span class="sxs-lookup"><span data-stu-id="320af-113">Sysdig is known toohelp with troubleshooting but it also has your basic monitoring metrics for CPU, Networking, Memory, and I/O.</span></span> <span data-ttu-id="320af-114">Sysdig maakt het eenvoudig toosee welke containers werkt Hallo hardest of in wezen met Hallo meeste geheugen en CPU.</span><span class="sxs-lookup"><span data-stu-id="320af-114">Sysdig makes it easy toosee which containers are working hello hardest or essentially using hello most memory and CPU.</span></span> <span data-ttu-id="320af-115">Deze weergave wordt Hallo sectie 'Overzicht', die momenteel in de bètaversie.</span><span class="sxs-lookup"><span data-stu-id="320af-115">This view is in hello “Overview” section, which is currently in beta.</span></span> 

![Gebruikersinterface van Sysdig](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a><span data-ttu-id="320af-117">Een Sysdig-implementatie met Marathon configureren</span><span class="sxs-lookup"><span data-stu-id="320af-117">Configure a Sysdig deployment with Marathon</span></span>
<span data-ttu-id="320af-118">Deze stappen wordt uitgelegd hoe u tooconfigure en implementeren van Sysdig toepassingen tooyour cluster met Marathon.</span><span class="sxs-lookup"><span data-stu-id="320af-118">These steps will show you how tooconfigure and deploy Sysdig applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="320af-119">Toegang tot uw DC/OS-Webgebruikersinterface via [http://localhost:80 /](http://localhost:80/) Navigeer eenmaal in Hallo DC/OS-Webgebruikersinterface toohello 'Universe', die zich op Hallo onderste links en zoek naar 'Sysdig'.</span><span class="sxs-lookup"><span data-stu-id="320af-119">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate toohello "Universe", which is on hello bottom left and then search for "Sysdig."</span></span>

![Sysdig in het DC/OS-universum](./media/container-service-monitoring-sysdig/sysdig1.png)

<span data-ttu-id="320af-121">Nu toocomplete Hallo-configuratie moet u een Sysdig cloud-account of een gratis proefaccount.</span><span class="sxs-lookup"><span data-stu-id="320af-121">Now toocomplete hello configuration you need a Sysdig cloud account or a free trial account.</span></span> <span data-ttu-id="320af-122">Nadat u bent aangemeld op toohello Sysdig cloud website, klikt u op uw gebruikersnaam en op de pagina Hallo ziet u uw 'toegangssleutel'.</span><span class="sxs-lookup"><span data-stu-id="320af-122">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Sysdig API-sleutel](./media/container-service-monitoring-sysdig/sysdig2.png) 

<span data-ttu-id="320af-124">Naast uw toegangssleutel in Hallo Sysdig configuratie binnen Hallo DC/OS Universe invoeren.</span><span class="sxs-lookup"><span data-stu-id="320af-124">Next enter your Access Key into hello Sysdig configuration within hello DC/OS Universe.</span></span> 

![Configuratie van de Sysdig in Hallo DC/OS Universe](./media/container-service-monitoring-sysdig/sysdig3.png)

<span data-ttu-id="320af-126">Nu Hallo exemplaren too10000000 zodanig instellen wanneer er een nieuw knooppunt wordt toegevoegd toohello cluster Sysdig automatisch een agent implementeren toothat nieuw knooppunt.</span><span class="sxs-lookup"><span data-stu-id="320af-126">Now set hello instances too10000000 so whenever a new node is added toohello cluster Sysdig will automatically deploy an agent toothat new node.</span></span> <span data-ttu-id="320af-127">Dit is een tijdelijke oplossing toomake ervoor dat sysdig tooall nieuwe agents binnen Hallo cluster gaat implementeren.</span><span class="sxs-lookup"><span data-stu-id="320af-127">This is an interim solution toomake sure Sysdig will deploy tooall new agents within hello cluster.</span></span> 

![Configuratie van de Sysdig in Hallo DC/OS Universe-exemplaren](./media/container-service-monitoring-sysdig/sysdig4.png)

<span data-ttu-id="320af-129">Zodra u Hallo pakket hebt geïnstalleerd Navigeer terug toohello Sysdig UI en u zult kunnen tooexplore Hallo verschillende gebruik metrische gegevens voor Hallo containers in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="320af-129">Once you've installed hello package navigate back toohello Sysdig UI and you'll be able tooexplore hello different usage metrics for hello containers within your cluster.</span></span> 

<span data-ttu-id="320af-130">U kunt ook Mesos- en Marathon-specifieke dashboards installeren via de [wizard Nieuw dashboard](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="320af-130">You can also install Mesos and Marathon specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
